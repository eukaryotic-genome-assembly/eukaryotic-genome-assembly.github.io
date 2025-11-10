---
title: "Hands On"
layout: archive
permalink: /handsOn_plotReadLength/
---  

In our previous tutorial we have generated a k=31 kmer distribution for a subset of reads, and we have analysed the same k=31 kmer distribution for the total reads sequenced for our chosen species. With the genomescope of our total results, we have estimated genome size, heterozygosity and repeat content. Now, we are ready to go and assemble those reads. 

Well, it would be nice to check one more thing: the size distribution of our reads!

**Imagine if we have a good genome coverage but our reads are all small? It would not be very useful to assemble across repeats**

So let’s plot the size distribution of our <species>.total.fasta file using a python script named `plot_fasta_length.py`. First, let's copy the script to our working directory:  
  
```bash  
cp /home/ubuntu/Share/scripts/plot_fasta_length.py .
```

Then, activate the conda environment that contains the python packages required for the script:  
```bash
conda activate fasta_plot_env
```

Now we can finally run the script:

```console  
python plot_fasta_length.py <species>.ccs.total.fasta.gz <species>.ccs.total.fasta.length.png
```
This might take a bit of time. So if you prefer, you can use tools such as `nohup` or `screen` to run the process in the background (e.g. `nohup <command> &`).

> Note: 
> My script `plot_fasta_length.py` and also Shane’s script `asmstats` are two of many options you can use to plot fasta lengths and generate statistics. Remember, internet is on your side in this journey. While you wait the script to run, have a look at other options: [like this one](https://bioinformatics.stackexchange.com/questions/45/read-length-distribution-from-fasta-file) or the stats from [BBMap](https://github.com/BioInfoTools/BBMap)  

Once you have plotted the reads length distribution, download it to your local computer and have a look.  
a- How does the reads distribution look like?  
b- Which length most of the reads have?  

Now, gather all the results you have so far and let’s discuss them as a group!!
