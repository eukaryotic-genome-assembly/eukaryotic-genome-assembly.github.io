---
title: "Hands On"
layout: archive
permalink: /handsOn_3/
---  

# BLAST (Basic Local Alignment Search Tool)

Last but not least!

I know you have chosen a specific species and you have assembled a partial set of Pacbio HiFi reads for it. Do you think you have just assembled some portions of your species nuclear genome? Or something special? Aren’t you curious? Well, the parameter `genomeSize=` you have used for Hicanu already gives you a hint about what you have assembled. 

But we will do something even more fun to find out. Let’s do a stand-alone BLAST of our assembled contigs (choose one or run for both, as you wish!).

We already have BLAST installed in our `eukaryotic_genome_assembly` conda environment. If you do not have that conda environment activated yet, run:  

```bash  
conda activate eukaryotic_genome_assembly
```

If `eukaryotic_genome_assembly` is activated, try:

```console  
blastn -h
```  

Has `blastn` returned some USAGE information with a list of accepted parameters? If yes, great.
The next thing will be to make sure you are in your assembly directory, which can be either the hifiasm or canu:

```console
cd ~/<species_folder>/<hifiasm>/
cd ~/<species_folder>/<hicanu>/

```

Right. So now we want to BLAST our contigs to find out what they are. This means we need to blast them against a database of sequences we must think are present in our assembly. I have already created a database for you. It’s called `database.fasta`. So all you have to do to use it is to create this database in the format blast understands and uses it. So you do:

```console  
cp /home/ubuntu/Share/database.fasta .
makeblastdb -in database.fasta -dbtype nucl
```  

Now, list your directory. Have a look. Do you see different files with the database name but with specific blast file extensions (e.g. `*.nsq`, `*.nhr`)?

```console  
ls -ltrh
```  

Now that we have formatted our database, let’s run blast. Blast has many parameters. We are going to run it twice to produce two types of output files. First run to generate a standard output:

```console  
blastn -query <contigs_fasta> -db database.fasta -out <contigs_fasta>.DB.blastn -evalue 1e-05
```  

PS: here you should replace `<contigs_fasta>` by the assembly you've generated at the `Part 2 - Genome Assembly` tutorial. If you are blasting the hifiasm assembly, this file should be named `<species_id>.hifiasm.p_ctg.fa`. If you are blasting the canu assembly, this file should be named `<species_id>.contigs.fasta` (but remember that the canu output has been saved on the `run1/` subdirectory).

Now run it with an output format 6:

```console  
blastn -query <contigs_fasta> -db database.fasta -out <contigs_fasta>.DB.blastn6 -evalue 1e-05 -outfmt 6
```

The command above will tell you the accession number of the subject sequences (i.e. the sequences in the database), then you can check on NCBI what those sequences are. Alternatively, you may change the `blastn` command to directly print the title of the subject sequences in the output file (by replacing `-outfmt 6` by `-outfmt "6 std stitle"`):  

```
blastn -query <contigs_fasta> -db database.fasta -out <contigs_fasta>.DB.blastn6_2 -evalue 1e-05 -outfmt "6 std stitle"
```

### Attention :grey_exclamation: 

The blast database files and the contigs must be in the same folder. If they aren’t you have some options: (i) you can specify the path to the target files, (ii) you can copy files (assembly or database) to the same folder, (iii) you can symlink files. If you get stuck, let us know.

# Good! 

So now let’s have a look at our outputs!

1-) Based on your blast results, what have you assembled? (If you don't understand the subject ID, search it on NCBI).

2-) Let’s inspect the differences between the two outputs

3-) What does each column on the output `<contigs_fasta>.DB.blastn6` mean?  
    Here you can either google it or (even better) run `blastn -help` to see what the default columns for the `-outfmt` are. By exploring the `blast -help` output you can even discover some non-default options that you may find interesting to include in your future blast alignments outputs. 

Discuss this with your colleagues and then let's discuss this as a group!

