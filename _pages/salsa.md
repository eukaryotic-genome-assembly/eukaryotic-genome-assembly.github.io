---
title: "Part 5 - SALSA2 Scaffolding"
layout: archive
permalink: /salsa/
---


# SALSA2 Scaffolding

Right, so now you have learned about Chromosome conformation capture and scaffolding genomes with the Hi-C technology. Today you will start one of the softwares that is used to scaffold genomes with Hi-C that is called SALSA2. You can have a look [here](https://github.com/marbl/SALSA) on what we will be running. 

First you need to activate our SALSA environment:

```console
conda activate salsa  
```

Then run:

```console  
run_pipeline.py -h
``` 

See the help message? Nice! 

Now let's create a `scaff` subdirectory in your species home directory so that we can work on scaffolding from there:

```console  
mkdir ~/<species_folder>/scaff/
cd ~/<species_folder>/scaff/  
```

To run SALSA2 you need first to symlink 3 files to your working directory. All files will be inside the shared species directory, in a subdirectory called `HiC` (`/home/ubuntu/Share/<species_id>_data/HiC/`). The files are `<species_id>_*purged.polish.fa`, `<species_id>_*purged.polish.fa.fai` and `merge.mkdup.bed`. Once you have symlinked all files, run:

```console  
run_pipeline.py -a <species_id>_*purged.polish.fa -l <species_id>_*purged.polish.fa.fai -b merge.mkdup.bed -e GATC,GANTC -i 5 -p yes -o out
``` 

> Attention :exclamation:  
> Remember to replace `<species_id>` with the ID of your species. For instance, for *Vanessa atalanta* that would be `ilVanAtal1`.


> **What exactly are you scaffolding?**
> You will notice that the contigs you are scaffolding are called polish. In fact, if/when you run a summary statistics for them you will see that they have a different number of bases compared with the purged assembly you analyzed. Why is that? That is because at Darwin Tree of Life we used to polish the purged genomes before scaffolding (remember I showed you this in the lecture?). We have dropped polishing now, but you are working with data that was polished. :) 

Right, SALSA2 will start running. However, since SALSA2 run should take a long time, we'll **stop SALSA2 run** now with `Ctr+C`. From this point on we'll be using SALSA2 results generated in advance by your instructors. Those files can be found under `/home/ubuntu/Share/<species_id>_data/HiC/out.break.salsa/` directory. 

Now let's generate assembly statistics for the genome prior Hi-C scaffolding, and after Hi-C scaffolding. 

First let's add the folder that contains `asmstats` script to our `PATH`:  

```bash  
export PATH=$PATH:/home/ubuntu/Share/scripts
```

And make sure our conda environment is activated:  
```  
conda activate eukaryotic_genome_assembly  
```

Then symlink the file from the genome after Hi-C scaffolding to your working directory:  
```bash  
ln -s /home/ubuntu/Share/<species_id>_data/HiC/out.break.salsa/scaffolds_FINAL.fasta .
```

Now we can run `asmstats` for both the genome prior Hi-C scaffolding (`<species_id>_hicanu.purged.polish.fa`) and after Hi-C scaffolding (`scaffolds_FINAL.fasta`):

```console  
asmstats <species_id>*.purged.polish.fa > <species_id>*.purged.polish.fa.stats
asmstats scaffolds_FINAL.fasta > scaffolds_FINAL.fasta.stats
``` 

Now I want you to download to your local machine the assembly Hi-C heatmaps for (i) prior and (ii) after scaffolding. 

1-) Hi-C heatmap of your species contigs **before** they were scaffolded with SALSA2

The pre-scaffolding is a file that ends with \*.pretext (not for drUrtUren1, see next sentence!) and it is located in your species shared directory (`/home/ubuntu/Share/<species_id>_data/HiC/<species_id>.preScaf.pretext`). 

The pre-scaffolding file for drUrtUren1 ends with \*.hic and it is located in your species shared directory (`/home/ubuntu/Share/<species_id>_data/HiC/drUrtUren1.preScaf.hic`). This is to be open at Juicer.

2-) Hi-C heatmap of your species scaffolds **after** the contigs were scaffolded with SALSA2

The post-scaffolding will be in the `out.break.salsa` directory (`/home/ubuntu/Share/<species_id>_data/HiC/out.break.salsa/`) and it is a file that ends in \*.hic. This file is a heatmap image representation of the final scaffolded assembly (`scaffolds_FINAL.fasta`).

Once you download the two files (pre and after scaffolding) to your local computer, you are going to use the PretextView program to open the pre-scaffolding heatmap, and the JuiceBox program to open the post-scaffolding heatmap. You should already have PretextView installed in your local computer. If not, follow [this link](https://eukaryotic-genome-assembly.github.io/pretextView_installation/) to install it. You can run Juicebox using its [website](https://www.aidenlab.org/juicebox/) or (optionally) you can also run it locally. If you choose to run Juicebox locally, you will need to access [this link](https://github.com/aidenlab/Juicebox/wiki/Download) to download the executable for Juicebox compatible with your operating system, and after you download it, just double click on the executable file to open Juicebox.

### Using Juicebox  
##### Using the webserver
Go do the Juicebox's [website](https://www.aidenlab.org/juicebox/). Click on `Load Map > Local File` and locate your downloaded \*.hic file.

##### Using locally installed Juicebox (optional)
Once you open Juicebox, click on `File > Open`. A new window will open, then you should click on the `Local...` button. Now you are ready to select the downloaded \*.hic file. Once you do it, the heatmap should be plotted. 

### Using PretextView
After opening PretextView, click on the `Load Map` button and then select the downloaded \*.pretext file.

## Now 
Analyze all the results, discuss with your team and answer the questions in your presentation:

1. What are the assembly statistics before scaffolding?
2. What are the assembly statistics after scaffolding?
3. Looking at the final agp file (`/home/ubuntu/Share/<species_id>_data/HiC/out.break.salsa/scaffolds_FINAL.agp`) (maybe you want to read a little about the AGP format [here](https://www.ncbi.nlm.nih.gov/assembly/agp/AGP_Specification/)): what scaffolds were scaffolded with more than one component (a contig of a piece of a contig)? And what scaffolds are unchanged in relation to the contigs?
4. How do the Hi-C maps look prior and after scaffolding?
5. Do you think you see a sex chromosome on the Hi-C heatmap? If so, point to it in your presentation.

After that, come back to the wider group.
