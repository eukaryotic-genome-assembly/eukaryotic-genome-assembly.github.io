---
title: "Hands On"
layout: archive
permalink: /mitohifi/
---  

## Background

Ok, so on the second day of our course you have assembled the mitogenome of your species with Hifiasm and Hicanu. Well, the contigs are the mitochondria, but they don't represent a final mitochondrial sequences we usually find on databases, right? Firts: for some of you, hifiasm or hicanu is likely to have outputed more than one contig, and second, the contig size if much larger than a mitogenom usually is. True! This happens because of the circular nature of the molecule, and because of how assemblies work! Basically the overlaps of the circular molecule makes the assemblers confused and they end up concatenating the circular molecule many times!

So I have written a pipeline that can finish the assembly of your mitochondria for you! It basically blasts your assembled Pacbio HiFi contigs to close-related species mitogenome, it does a series of parsings to be sure you have a contig that is only the mitogenome and not a NUMT, they it will circularise the contig, cut it and anotate it with MitoFinder.

For more information on MitoHifi, have a look here: [https://github.com/marcelauliano/MitoHiFi](https://github.com/marcelauliano/MitoHiFi)

## 1. Setting up the environment for running MitoHiFi  

We will not install any software or conda environments.  
Instead, we will use **Singularity**, which runs software inside an isolated “container environment”.

### ❓ What is a container?  
A container is a mini-Linux environment that already contains everything the software needs:  
✔ the programs  
✔ the libraries  
✔ the dependencies  
✔ the correct versions of everything

This guarantees that MitoHiFi will behave the same way for everyone.

## 2. Create a working directory  

At your home directory, create a new directory to work on MitoHiFi and move to it:  

```console  
mkdir ~/mitohifi_test_01/
cd ~/mitohifi_test_01/  
```

The instructors prepared a container image (.sif file) with MitoHiFi already installed. You'll need to create a symlink to it for running mitohifi:  
```console  
ln -s /home/ubuntu/Share/singularity-images/mitohifi.sif
```

### ❓ What is the `.sif` file?  
A `.sif` file is a Singularity Image File.  
Think of it as a single file that contains an entire Linux environment, including:  
✔ MitoHiFi  
✔all dependencies  
✔ Python  
✔ BLAST  
✔ system libraries  

So no installation is needed — you just “enter” the container to run the software.

### (Optional) Using MitoHiFi on your own computer later  
When you are back to your own computer/server, you can download the up-to-date mitohifi image file with the command:
```console
singularity pull mitohifi.sif docker://ghcr.io/marcelauliano/mitohifi:master
``` 

This command will download the complete MitoHiFi container from the internet and save it locally as a single `.sif` file, and you only need to run it once. Then, every time you need to run mitohifi, all you need to do is target that file:  
```console   
singularity exec /path/to/local/mitohifi.sif mitohifi.py -h
```

## 3. Finding a related mitogenome  
To run MitoHiFi, first you need a close-related mitochondria in fasta and genbank format. We have a script that can help you find this input. Giving the name of the species you are assembling, the script is going to look for the closest mitochondria it can find on NCBI. You can give the parameter `-s` to the script if you would like to restrict your mitochondria search for species within your given genus, but this means the script can download partial mitochondrial sequences. Otherwise, without `-s`, the script is going to search for complete mitochondrias only and as close as possible to your species on interest.

We'll need to mitohifi.sif file to run this script:

```console  
singularity exec mitohifi.sif findMitoReference.py --species "Phalera bucephala" --email <your_email> --outfolder refData --min_length 15000
```

Where `<your_email>` should be replaced by your email (your personal/work email should work just fine)

### `findMitoReference.py` output  
This command will output a fasta (OQ830676.1.fasta) and a genbank (OQ830676.1.gb) file from the closely related mitogenome. When running MitoHiFi, you will use those files as input using, respectively, the `-f` and `-g` options. 

## 4. Running MitoHiFi

Now let's run MitoHiFi using an example dataset. First, you may want to check the general syntax for running MitoHiFi, as well as all options that this pipeline provides:

```console  
singularity exec mitohifi.sif mitohifi.py -h
```

### ❗ Important clarification  
There are two “mitohifi”s here:  
i) `mitohifi.sif` is the Singularity image, which contains the full software environment;  
ii) `mitohifi.py` is the actual MitoHiFi program, which runs inside the Singularity container.

Now, copy the the `test.fa` file to your current directory. The `test.fa` is a multifasta file that contains 3 assembled contigs. It's been generated in advance by your instructors. 

PS: of course in the real world you assembly file will have a much higher number of contigs, but here we are working with a limited number for computational and time constraints.

```console  
cp /home/ubuntu/Share/MitoHiFi_data/test.fa .
```

Finally, run MitoHiFi for the contigs test dataset: 

```console  
singularity exec mitohifi.sif mitohifi.py -c test.fa -f refData/OQ830676.1.fasta -g refData/OQ830676.1.gb -t 1 -o 5
```

The pipeline will probably take a few minutes to run. Once it's done, it will output a message saying `Pipeline finished!`.

## Questions:  
1) What's the meaning of each parameter used to run MitoHiFi? Hint: if in doubt, run `python mitohifi.py -h` and/or check the official MitoHiFi documentation at [github](https://github.com/marcelauliano/MitoHiFi).    
2) Has MitoHiFi succeded creating final mitogenome fasta/genbank files? What are the names of those files?  
3) Open the final mitogenome genbank file and answer: i) what's the total length of the mitogenome?; ii) what's the first gene in that mitogenome?  
4) Go to BLAST [webserver](https://blast.ncbi.nlm.nih.gov/Blast.cgi) and do a blastn of the final mitogenome fasta file (`final_mitogenome.fasta`) against the Nucleotide collection (nr/nt). What's the first hit you get from the alignment? What species does that hit come from? Click on the hit accession number hyperlink. You should be redirected to a new page. Go to the `COMMENT` section and answer: how was this sequence assembled?    
5) Open the `contigs_stats.tsv` file and answer: is there another mitogenome assembly besides the final_mitogenome? 
 
We can discuss the results together. =)  

## Bonus Activity (if you finish early!)  
In **Part 2 – Genome Assembly**, you assembled a small subset of HiFi reads and discovered that the resulting contigs were **mitochondrial**.  
Now that you have learned how to run MitoHiFi on an example dataset, you can try applying the *same pipeline* to the contigs **you assembled earlier in Part 2**.  

Your goal:  
**Use MitoHiFi to generate the complete, circularized and annotated mitogenome of your species using your own assembly.**  

### Steps
1. Create a new work directory and go to it  
2. Locate the contigs you assembled in Part 2 (using either HiCanu or HiFiasm). You can either copy them to your working directory or create a symlink
3. Find a reference mitogenome for your species
4. Run `mitohifi.py` using your own contigs
5. Explore your results. Check whether MitoHiFi produced:  
    - a circularized FASTA
    - a complete GenBank file
    - annotation results
    - quality metrics in contigs_stats.tsv

