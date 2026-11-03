---
title: "Hands On"
layout: archive
permalink: /curated/
---

# Final results

Right guys, so here we are. I don't know if you realize you have come a long way this week. You have learned:

i) How to count and plot Kmers to understand genome composition (heterozygosity, genome size, repeat content)

ii) You have assembled your genome with 2 different pieces of software

iii) You have learned about purging genomes to (i) separate haplotypes or (ii) exclude retained haplotypes

iv) You have learned how to evaluate genome quality with (i) kmers (Merqury), (ii) general statistics and (iii) BUSCO

v) You have learned how to scaffold genomes with Hi-C data and SALSA2

vi) You have heard of genome polishing and curation


Look at that! That is A LOT! WELL DONE! :clap: 

This material will always be here for you to come back to it and consolidate your knowledge, and you can ALWAYS email us with questions; it will be lovely to hear from you.

# Now,

It's time for you and your team to gather all the results and make a final presentation. **I have some extra results for your species**: it's the final curated primary assembly (haplotigs are not curated at the moment). For the curated assembly you have available the following files:

* The general statistics: `/home/ubuntu/Share/<species_id>_data/HiC/curated/*.curated_primary.fa.stats`  
  * e.g. for `Urtica urens` that would be: `/home/ubuntu/Share/drUrtUren1_data/HiC/curated/drUrtUren1.curated_primary.fa.stats` 
* The file to be opened with PretextView to see the HiC heatmap: `/home/ubuntu/Share/<species_id>_data/HiC/curated/*.pretext`
* The BUSCO results: `/home/ubuntu/Share/<species_id>_data/HiC/curated/BUSCO/short_summary.specific..BUSCO.txt`

So you have the curated statistics, a BUSCO run for it and the final curated Hi-C heatmap. So I want you to gather ALL the results for your species and make a final presentation answering all the questions below:

     1\. What is the name of your species? And what else have you learned online for it (do a small search to find a picture and maybe some interesting evolutionary facts about it)?

     2\. What is the genomescope plot for the TOTAL Pacbio Hifi reads histogram? What is the expected genome size? What is the expected heterozygosity? What is the estimated repeat content?

     3\. What does the read length distribution plot look like? What is the average read length that was input to the assembly?

     4\. What are the statistics for the Hicanu total reads output? What is the merqury qv? The completeness? What does BUSCO look like?

     5\. What are the statistics for the hicanu purged results for primary and haplotigs? What are the qvs? Completeness? What does BUSCO look like for the primary and haplotigs assembly?

Now, let's go to the scaffolding part. One note: in the official Darwin Tree of Life Pipeline, we have run one round of Illumina polishing after purging the assembly and before running salsa on it. This is why you may find a slightly different number of bases in the statistics of the assembly after purging, and just before salsa.

     6\. What are the primary genome statistics just before salsa scaffolding? What does the Hi-C heat map look like?

     7\. What are the primary genome statistics after salsa scaffolding? What does the Hi-C heat map look like?

     8\. What are the primary genome statistics after manual curation? What does the Hi-C heat map look like? Has BUSCO changed at all?

     9\. What is the QV difference of the primary genome (i) after purging and (ii) after scaffolding?

     10\. For the subset of reads you have assembled for your species, which kind of reads were they? What have you assembled there?

   

WELL DONE! 

You have a robust knowledge and skill set to perform eukaryotic genome assembly using Pacbio HiFi and Hi-C. Looking at kmer profiles and Hi-C heatmaps takes practice and time. So, just keep doing it and you will become more confident with time. 


##########



