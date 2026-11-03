---
title: "Hands On"
layout: archive
permalink: /polishing/
---  

# Activating conda env  
Before starting the tutorial, make sure you have activated the conda environment: 

```console 
conda activate eukaryotic_genome_assembly  
```

# Polishing CLR assembly

Ok, we have talked a little about polishing and how much polishing is still vital if you are working with PacBio CLR reads, which can have up to 15% of errors. Now, you are going to investigate the impacts of polishing on the *Hemaris fuciformis* genome, which was assembled with PacBio CLR reads as part of the [25 Genomes Project of the Sanger Institute](https://www.sanger.ac.uk/collaboration/25-genomes-for-25-years/)  

For this, you are going to compare some statistics for *H. fuciformis* **before** and **after polishing**, which has been done by the [GRIT](https://www.sanger.ac.uk/group/genome-reference-informatics-team/) Team at the Sanger Institute. All the files you will need are in `/home/ubuntu/Share/iHemFuc1_data` subdirectories. The stats I want you to compare are: 

* Merqury completeness and QV
    * Merqury has been run in advance by your instructors, so here you just need to collect the data.    
    * Those files are located in the `before_polishing/merqury_before/` and `after_polishing/merqury_after/` subdirectories (remember that the parent directory is `/home/ubuntu/Share/iHemFuc1_data`, so the complete path is, e.g., `/home/ubuntu/Share/iHemFuc1_data/before_polishing/merqury_before/`)
* General statistics  
    * For that you will need to run the `asmstats` script for the FASTA (\*.fasta or \*.fa) files located at `before_polishing` and `after_polishing`: 
    * For before polishing, you should have two FASTAs:    
        * iHemFuc1.primary.BF.fa.gz - this is the primary assembly before polishing (BF)
        * iHemFuc1.htigs.BF.fa.gz - this is the haplotigs assembly before polishing (BF)
    * For after polishing, you should also have two FASTAs:    
        * iHemFuc1.prim.polished.fa.gz - this is the primary  
        * iHemFuc1.htigs.polished.fa.gz - this is the haplotigs 
    * PS: Remember that when running `asmstats`, you will produce an output file. Because that output file cannot be saved on the `/home/ubuntu/Share/iHemFuc1_data/` directory, you will need to save the output file on your home directory. Then before running `asmstats` I recommend that you i) create a new directory in your home directory named `~/polishing/`; ii) move to that directory (`cd ~/polishing/`); iii) create symlinks for the four requested FASTA files (e.g. `ln -s /home/ubuntu/Share/iHemFuc1_data/before_polishing/iHemFuc1.primary.BF.fa.gz`); and finally iv) run `asmstats` (e.g. `asmstats iHemFuc1.primary.BF.fa.gz > iHemFuc1.primary.BF.fa.stats`)

* BUSCO
    * Just like Merqury, BUSCO analysis has been run by your instructors, so your job here is to collect the results.   
    * BUSCO's results can also be found at `/home/ubuntu/Share/iHemFuc1_data`, in the subdirectories `before_polishing/busco/` and `after_polishing/busco/` 

Now look at all the results and answer:

1. What were the general statistics (number of scaffolds, total assembled size, N50) for before and after polishing?

2. Have the QVs improved with polishing?

3. Putting one of each spectra plots for before and after polishing side by side in a slide, where can you see in the plot the evidence for the change in QV? (Look at kmers around 0).

4. Has BUSCO changed before and after polishing?

Make one slide with all the information you have analysed here.


