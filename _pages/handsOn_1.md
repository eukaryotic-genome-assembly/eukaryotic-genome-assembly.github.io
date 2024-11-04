---
title: "Hands On"
layout: archive
permalink: /handsOn_1/
---  

# Kmer analysis: running jellyfish <a name="where-are-we?"></a> 

Right, so today you learned about how to analyse kmer composition of your genome sequenced reads! Now you are going to put your 'Hands On' data and will, yourself, count and analyse kmers.
You have to chose between the species: (i) *Vanessa atalanta*, (ii) *Urtica urens* and (iii) *Notonda dromedarius* to work on until the end of the week. Once you have chosen it, create a folder where you will run your analysis. My suggestion would be to create a folder with your species name in your home directory (`~/<species_name>/`) and inside it, a series of other folders to structure your analyses. For example:

v_atalanta/

v_atalanta/kmers/
  
v_atalanta/assembly/
  
The above basically means you have created a folder called 'v_atalanta' (if you choose vanessa atalanta as your working species) and inside it you have created two other folders side by side called 'kmers' and 'assembly'. If you would like to do that, then do:
 
 ```console  
mkdir <species_folder>
cd <species_folder>
mkdir kmers
mkdir assembly
```  
 
Great, now you need to go and copy the working data for your species. The data will be inside `/home/ubuntu/Share/`

```console  
cd /home/ubuntu/Share/
ls -ltr
```  
Do you see the 3 species folders? If you do, then copy the file <species-code>.600.fasta (see bellow the Attention note, which explains about the species codes) to the `kmers` directory you have created and move back to the `kmers` directory. One example:


```console  
cp ilVanAtal1_data/ilVanAtal1.600.fasta <Path_to_your_folder>/v_atalanta/kmers/
cd <Path_to_your_folder>/v_atalanta/kmers/ 
ls -ltr
```

PS: if you followed our recommendation and created the species folder in the home directory, `<Path_to_your_folder>` should be your home directory, so `user2` should now be located in the `/home/user2/<species_name>/kmers/` directory (remember you can double check your current working directory with the `pwd` command). 

### Attention :grey_exclamation: 

Each species data will have a code on its name representing each of the 4 species we will work on during this week, this is the code they have at the Darwin Tree of Life Project. The codes are:

* ilVanAtal1 - *Vanessa atalanta*

* drUrtUren1 - *Urtica urens*

* ilNotDrom1 - *Notodonta dromedarius*

* iHemFuc1 - *Hemaris fuciformis* (we are not going to use this species in the current analysis)


Keep these codes in mind as the files will most likely to be named after them.

Now you need to activate our main `conda` environment. To do that you need to run: 

```
conda activate eukaryotic_genome_assembly
``` 

Your prompt should now look like:  

```bash  
(eukaryotic_genome_assembly) userX@IP-address:working_directory$
```
 
With the `eukaryotic_genome_assembly`environment active, try calling Jellyfish:

```console  
jellyfish --help
``` 

Do you see the help message? Great! (If not, call Joāo!)

Jellyfish has many steps. The first one we want to run is the *count* to count our genome reads kmers. The kmer size we are going to use is 31. 

1-) Jellyfish count

So here comes the command:

```console  
jellyfish count -C -m 31 -s 1000 -t 1 -o <species>.jf <species>.600.fasta
``` 


### Attention :grey_exclamation: 

In the command line above you see \<species\>.600.fasta. This needs to be replaced by the fasta file of the species you have chosen. This is just a generic way to point out that a fasta file must be imputed in that position in the command line above. The same with the \<species\>.jf. If your species is Vanessa atalanta, you can choose to have the output (-o) called v_atalanta.jf and this will be your output name.

### More

Please try:

```console  
jellyfish count --help 
```

on your command line to understand what are the parameters you have imputed in the previous line. Help messages are a useful way for you to understand what you are running, and to see if you would like to add any other parameter for your specific analysis case. Also remember that beyond this course, the internet is always on your side. If you google ‘jellyfish user guide’, for example, you will find [JellyfishUserGuide]( http://www.genome.umd.edu/docs/JellyfishUserGuide.pdf)

### Back

2-) Jellyfish histo

Now that you have counted your 31-letters kmers, we want to transform it to a histogram file so you can plot it. Then you have your second command:


```console  
jellyfish histo <species>.jf > <species>.histo
```

### Attention :grey_exclamation: 

Note in the command above we have used the symbol “>” before the output. This is a command line symbol that will redirect your output to a file instead of printing it to the screen.

Note that the input for your command **jellyfish histo** is the output from your previous command, that was **jellyfish count**. Now you have the necessary result to plot a histogram on genomescope and have a look at the distribution of your genome kmers. 

# BUT STOP!

# STOP STOP! 

...

Before you plot this result, I want you to plot a genomescope plot for another file FIRST!! 

Inside the shared directory for your species (`/home/ubuntu/Share/<species-Code>_data/`), you are going to find two files called:

```console  
<species>.ccs.total.fasta.gz
<species>.total.histo
```

Download the file \<species\>.total.histo to your local machine (if you need help for that, we have instructions on downloading/uploading files in [this](https://eukaryotic-genome-assembly.github.io/logging_on/) tutorial), go to the [Genomescope](http://qb.cshl.edu/genomescope/) page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot. People working with drUrtUren1 also need to set the kmer max count to 10000.

Save the image of both versions of the plot - normal and log scale - somewhere in your computer.

Cool, you have plotted the kmer distribution of the \<species\>.total.histo file, and genomescope has calculated for your (i) the estimated genome size, (ii) the heterozygosity and (iii) the percentage of repeats of your species genome. 

The histogram you have just plotted is for a jellyfish count of the **total** PacBio HiFi reads sequenced to assemble your species. We have generated it for you because it takes time. However, when you are back to real life and need to run it for your sample, you will run the same commands ran for the subsample (`*600.fasta`) as you just did! =) Yeah!! 

## Now

I would like you to generate some general statistics for the \*.ccs.total.fasta.gz reads. I have a script for you to do that. It's called `asmstats`. 

Before running asmstats, move to your species directory and create a soft link for the \*.ccs.total.fasta.gz file:

```bash
cd <Path_to_your_species_folder>/
ln -s /home/ubuntu/Share/<species-Code>_data/<species-Code>.ccs.total.fasta.gz
``` 

You can check if the soft link is working by print the first two lines of the file. If the first two lines are returned the link has been successfully created:

```bash
zcat <species-Code>.ccs.total.fasta.gz | head -2
```
 
Now you need to add the directory where the `asmstats` script is located (`/home/ubuntu/Share/scripts/asmstats`) to your environment variable:  

```bash  
export PATH=$PATH:/home/ubuntu/Share/scripts/
```  

Then check if the directory has been added to your environment variable:  

```bash  
echo $PATH
```

If you can see the `/home/ubuntu/Share/scripts/` in the output of the previous command, you should be ready to run the asmstats script (but first double-check that the conda environment `eukaryotic_genome_assembly` is active):

```console  
asmstats <species>.ccs.total.fasta.gz > <species>.total.fasta.stats
```

Note: We are calling your output file \<species\>.total.fasta.stats

Once the command finishes to run (it could take a few minutes), have a look at the output:

```console  
less <species>.total.fasta.stats
```

Also: use this tutorial to plot your reads length distribution: [Plot reads](https://eukaryotic-genome-assembly.github.io/handsOn_plotReadLength/)

You have now generated the kmer plot, reads statistics and reads plot distribution for your complete PacBio HiFi read set. Which conclusions can you now draw from these results?


a- What is the expected genome size?

b- What is the estimated heterozygosity?

c- What is the estimated repeat content?

d- Taking into consideration the estimated genome size, and the statistics of the total reads you have just generated, how much read coverage you have to assemble this genome?

# Now,

I want you to go back to the *.histo* file you have generated today (for your subsample), download it to your local machine and plot it on genomescope. Also, I want you to run asmstats on the fasta file (the 600 subset) you imputed to jellyfish. 

e- What genomescope tells you when you try to plot a kmer histogram for just a handful of sequences? 

f- Looking at the asmstats result for this smaller file, how much coverage of the genome you have in this file giving the estimated genome size?

Great. Now let’s look at it all together: considering the kmer plot of the total file and its statistics, we can have a good look at the kmer composition of the DNA in the genome. How does it look? Discuss with your partners and then later in the big group.  


