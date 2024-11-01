---
title: "Hands On"
layout: archive
permalink: /handsOn_2/
---  

# Assembling genomes

Right, so here we are! Let’s assemble the species you have chosen. You are going to run two assemblers for Pacbio HiFi data: Hicanu and Hifiasm.

Have a look at their websites:

* [Hicanu github repository](https://github.com/marbl/canu)
* [Hicanu documentation](https://canu.readthedocs.io/en/latest/)

* [Hifiasm github repository](https://github.com/chhylp123/hifiasm)
* [Hifiasm documentation](https://hifiasm.readthedocs.io/en/latest/)

Now let’s run the assembly on our subsamples.


First, make sure you are in your species directory that you created at your home directory in our first hands-on tutorial (`~/<species_folder>/`, e.g. `~/v_atalanta/`). Then let’s create a directory for each assembly we are going to run, as both assemblers create a lot of different outputs:

```console  
mkdir hicanu
mkdir hifiasm
```  

Make sure the conda environment is activated:

```console
conda activate eukaryotic_genome_assembly
```

Now let’s change to the hicanu folder and add HiCanu executable to the path:

```console
cd hicanu
export PATH=/home/ubuntu/Share/softwares/canu-2.2/bin:$PATH 
```

In the `export` command, what you are doing is adding the directory where the HiCanu software is installed to an environment variable named PATH. The PATH variable defines a set of directories where the operating system will search for executable files in order to run the softwares. Since we've added HiCanu directory to the PATH, now we should be able to run it by directly calling the HiCanu executable (`canu`), with no need to type the whole path to the executable file (`/home/ubuntu/Share/softwares/canu-2.2/bin/canu`). 

Now please test if you can run canu:

```console  
canu
```  

This will print you all the parameters that one can use to run canu. 

Then, create a symlink to the subsample read dataset and 

1-) run the bellow for ilVanAtal1 and ilNotDrom1:

```console  
ln -s /home/ubuntu/Share/<species_id>_data/<species_id>.600.fasta
canu -d run1 -p <species_id> genomeSize=16000 -pacbio-hifi <species_id>.600.fasta useGrid=false corThreads=2
```  

2-) run the bellow for drUrtUren1:

```console  
ln -s /home/ubuntu/Share/<species_id>_data/<species_id>.600.fasta
canu -d run1 -p <species_id> genomeSize=300000 -pacbio-hifi <species_id>.600.fasta useGrid=false corThreads=2
```  

The files created by `canu` will be saved on the `run1` directory. They will all be named using the *prefix* defined by the `-p` option. 
  
### Attention :grey_exclamation: 

Remember whenever you see `<>` it means you should replace it with some information. For instance, `<species_id>` should be replaced by the ID of your species. For *Notodonta dromedarius* that would be ilNotDrom1. In that case, `<species_id>_data` should be replaced by `ilNotDrom1_data`. 

Right, so let’s wait for Hicanu to run. While we do that, let’s start the hifiasm assembly!

In a second tab/window, let’s change to the hifiasm folder and create a symlink to the subsample dataset of reads:

```console  
cd ~/<species_folder>/hifiasm/
ln -s /home/ubuntu/Share/<species_id>_data/<species_id>.600.fasta
```

Now let’s call hifiasm and have a look at the parameters it prints:

```console  
hifiasm
```

And this is the line you will run:

```console  
hifiasm -f0 --primary -t 1 -o <species>.hifiasm <species_id>.600.fasta
```

PS: the `-o` option defines the *prefix* which will be used to name all the output files generated by Hifiasm.

Let’s wait a few minutes for both assemblers to run. While you do that, you can take some time to search what the parameters we used for running canu and hifiasm mean. You can do that by either looking at their websites or by opening a third tab/window and running canu and hifiasm on help mode (e.g. `canu -h`)

## Interpreting our results

Each assembler will output different intermediate files together with the final assembly result. 

1-) Hifiasm

Let’s look at the Hifiasm result first:

Am I in the hifiasm folder? 

```console
pwd  
```

If not, then I need to change there. Now, list the contents of `hifiasm` directory:

```console
ls -ltrh  
```

Among the results hifiasm produce, you will find the `<prefix>.p_ctg.gfa` file (remember that the prefix has been defined using the `-o` option when running Hifiasm). This is our assembly output file. Hifiasm gives us the [assembly graph](http://gfa-spec.github.io/GFA-spec/GFA1.html) as an output. This means you need to convert the graph into a fasta file. For that, we have an awk script named `gfa2fa`.

Add the directory containing that script to the PATH and run it:


```console 
export PATH=/home/ubuntu/Share/scripts/:$PATH
gfa2fa <prefix>.p_ctg.gfa > <prefix>.p_ctg.fa
```

Right. So now, what to do with the assembly file?
Well, first you should have a look at the statistics for this assembly. Let’s run our asmstats script on it

```console  
asmstats <prefix>.p_ctg.fa > <prefix>.p_ctg.fa.stats
```

2-) Hicanu

Now, let’s move to the hicanu directory and let’s have a look at the results. Remember you have stored the results in the `run1/` subdirectory:

```console  
cd ~/<species_folder>/hicanu/run1/
ls -ltrh
```

Differently than Hifiasm, Hicanu is going to give you a fasta file at the end. It’s called * *.contigs.fasta.* So, go on and generate the statistics for this result:

```console  
asmstats <prefix>.contigs.fasta > <prefix>.contigs.fasta.stats
```

## WELL DONE!
You have just done eukaryotic genome assembly using PacBio HiFi reads and two different assemblers! **That is fantastic!**

I want you to gather the statistics results of different files:

1-) The statistics of the raw reads you have used as input for your assembly.

a- How many reads are there?

b- What is their average length?

OBS: remember you already have these results as we have generated them in the previous Hands On session.

2-) The statistics of Hicanu and Hifiasm assembled files.

a-) Have both assemblers assembled exactly the same number of contigs?

b-) What are the assembly statistics: N50, total assembled size, contig counts ...


# BEFORE YOU GO BACK TO THE GROUP

As you know, because of time and computer resources, we have assembled only a subset of reads (`<species_id>.600.fasta`) for the species you have chosen. But I have generated previous assemblies for the complete set of reads, and I would like you to generate assembly statistics for those assemblies. The files will be on the shared species folder (`/home/ubuntu/Share/<species_id>_data/`) and will be named `<species_id>.hicanu.total.contigs.fasta.gz` and `<species_id>.hifiasm.total.[a/p]_ctg.fa.gz` (Hifiasm produces two different files, one with suffix `a_ctg.fa.gz` and another one with the suffix `p_ctg.fa.gz`). In your species home directory (`~/<species>/`), create a symlink for those files (with the `ln -s` command) and run `asmstats` on them (e.g. `asmstats <species_id>.hicanu.total.contigs.fasta.gz > <species_id>.hicanu.total.contigs.fasta.stats`). Then answer:
  
  1-) What is the assembled size, number of contigs and N50 for the hicanu assembly? 
  
  1a-) Is the Hicanu result close to the estimated genome size? Why?
  
  2-) Hifiasm generates two files. Why? What are the assembly metrics for these two files?
  
Now gather all these results, let’s go to the larger group and let’s discuss them together!
