---
title: "Hands On"
layout: archive
permalink: /handsOn_4/
---  

# Mapping and IGV

Mapping and dealing with samtools and IGV.

Right, so we have already generated statistics for our raw data, assembled it with two different assemblers and even done a BLAST search to try to identify what we have assembled. Those are all good metrics to check our assembly. 

Another metric commonly used is to map all the reads back to our assembly and determine the percentage of mapping. As this was the data we inputted to assemble the contigs, we want most of the reads to map back to it, if not, it raises a red flag to us about the sanity of our assembly. So let’s learn how to use two new tools: `minimap2` and `samtools`.

Choose one of your two assembly results (or run for both) and go to its directory (`cd ~/<species_folder>/<hifiasm/hicanu>/`). Identify the raw reads (`<species_id>.600.fasta`) you have used to produce that assembly. Identify the assembly file. And let’s run `minimap2` to map the reads against the assembly.

However, before running `minimap2` activate our conda environment:  

```bash
conda activate eukaryotic_genome_assembly
```

Now you should be ready to run `minimap2`. Try:

```console  
minimap2
```  

See the help message? Then let’s run it:

```console  
minimap2 -t 1 --secondary=no -ax map-pb <contigs_fasta> <raw_reads>.fasta -o <outputname_you_chose>.sam
```  

Where `<contigs_fasta>` should be your assembly and `<raw_reads>.fasta` the sequencing reads used to build the assembly. 

Right. As soon as it finishes, we are going to use a tool called `samtools` to manipulate the output file:

```console  
samtools view -h -Sb <outputname_you_chose>.sam -o <outputname_you_chose>.bam
samtools sort <outputname_you_chose>.bam -o <outputname_you_chose>.sorted.bam
samtools index <outputname_you_chose>.sorted.bam
``` 
Right. What we did above was (i) to convert the output mapped file from the format `sam` to `bam`, then we (ii) sorted this file and (iii) created an index for it. This will be a standard procedure most of the time that you will be producing and visualizing a mapping: samtools `view`, `sort` and `index`. The BAM file is basically a binary representation of the SAM file, holding all of its information but taking a lot less disk space. Having the mapping file sorted and then creating an index for it will allow downstream tools (such as genome browsers, like `IGV`) to read those files much more efficiently, and that's why many downstream software tools will assume your mapping file is sorted and indexed.
To know more about samtools, go to its [webpage](https://samtools.github.io)

Now, we want to visualize one contig with the reads mapped back to it. So we need to extract one contig from the `<outputname_you_chose>.sorted.bam` file (which contains mappings for all contigs assembled). Extracting the mapping information from a specific contig will make it easier/faster to load that information on IGV, which is the software we'll use to inspect our contig. The steps for doing the extraction are:  

1. Extract the fasta file for the contig you have chosen and make an index for it (`samtools faidx`);  
2. Extract a bam file for one contig from `<outputname_you_chose>.sorted.bam` and create an index for it (`samtools index`);  

Below you see the steps detailed:

Let's get the fasta first:
First let's list the descriptions of all our contigs by grepping the lines that contain the `>` character:  

```console  
grep ">" <contigs_fasta> 
```

> Attention :exclamation:  
> Quoting the `>` character is needed here since an unquoted `>` would be interpreted as the redirection mechanism by the shell. Quoting the patterns to be searched by grep is actually a good practice. 

The output of the `grep` command will print to the screen the names of all your assembled contigs. Choose one and create a file with its ID. Let’s say my grep result looks like this:

```
>Contig1
>Contig2
```

> Attention :exclamation:  
> Remember from our FASTA class: the contig ID will be everything that comes before the first whitespace in the description of the sequence. For instance, given a contig whose description line is `>ContigX Some Other Info`, the contig ID will be just `ContigX`. 

So for this example I’ll choose `Contig1` (although it does **not** necessarily exist in your assembly file: choose any contig that does exist there). To create a text file that contains this ID we can use nano. We need a text file with the ID because the next script we are going to use to extract the contig needs it as an input. 

```console  
nano contig_id
```  

Nano will open an empty file for you. Inside it type the ID of the contig you have chosen, in my case this will be `Contig1`. Then to save  the file in nano you need to press `Ctrl+O`. After saving the changes you are ready to quit nano and go back to the terminal by pressing `Ctrl+X`. 

For the `Contig1` example, the content of the `contig_id` file should look like:  

```console
Contig1
```

Now, let’s run our script `filterfasta.py`, that will extract that contig from our assembly result. 

First, copy the script to your working directory:  

```bash  
cp ~/Share/scripts/filterfasta.py .
```

Then run it:

```console  
python filterfasta.py -i <contig_id> <contigs_fasta> > <contig_ID>.fasta
```  

Right. Now use the `less` command to inspect the file `<contig_ID>.fasta`.

```console  
less <contig_ID>.fasta
``` 

`less` allows you to browse through the lines using the up/down keys. Once you are happy navigating through the file, you can quit from `less` by pressing the `q` key. 

Now let's create an index for our contig fasta file. The index file will hold some information about the sequence, such as its ID, length and number of characters per line.

```console  
samtools faidx <contig_ID>.fasta
``` 

If you list your directory now, do you see a `<contig_ID>.fasta.fai` file there as well? Great!

Then extract a BAM file only for this contig (with the `samtools view` command) and create an index for it:

```console  
samtools view -b -h <outputname_you_chose>.sorted.bam <contig_ID> > <contig_ID>.bam
samtools index <contig_ID>.bam
``` 

Now you have four files you must download to your local machine to open them on IGV:

* Your contig fasta file (`<contig_ID>.fasta`)
* Your contig fasta.fai file (`<contig_ID>.fasta.fai`)
* Your contig bam file (`<contig_ID>.bam`)
* Your contig bam.bai file (`<contig_ID>.bai`)

Take your time…

On IGV, on the top, click on `Genomes > Load Genome from File` and add your fasta file. Then click on `File > Load from File` to include your bam file. And… you are done!!! 

Let's play with IGV a bit (alone and as a group).

# Further

But, how can I see how many reads have mapped to all my contigs? 
A few ways.
Minimap2 would have printed you some log files while it was running.
You can also run `samtools flagstat` on the mapping files:

```console  
samtools flagstat <outputname_you_chose>.sorted.bam
samtools flagstat <contig_ID>.bam
``` 

You can learn more about `samtools flagstat` and its output on its [official documentation](http://www.htslib.org/doc/samtools-flagstat.html). You can also find some useful definitions (e.g. what a secondary mapping is) in the [SAM specification document](https://samtools.github.io/hts-specs/SAMv1.pdf), specifically in the topic `1.2 Terminologies and Concepts`.

# GOOD!

Let’s discuss the results!

