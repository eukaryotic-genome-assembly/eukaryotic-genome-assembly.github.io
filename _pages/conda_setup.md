---
title: ""
layout: archive
permalink: /conda_setup/
---


![](/images/conda_logo.svg)

Conda is a package and environment management system. As a package management system, Conda allows us to quickly install, run and update programs and their dependencies. As an environment management system, Conda allows us to easily switch and export environments, where one or a set of software packages are installed and ready to be used. 

![](/images/conda_system.png)

We encourage you to [read more](https://docs.conda.io/en/latest/) about Conda and use it as a management system for your work beyond this course. Here, the only thing you need to know is that the instructors have already set up a Conda environment containing most of the software that will be used through this workshop. The job left for you is to initialize conda for your own user and activate the workshop environment.  

### Setting up Conda for this course

Since this is the first time you are running conda with your user, you need to initialize conda:

```bash 
user@bash:~$ conda init  
```  
Which should return something like this:  
```bash
no change     /home/ubuntu/miniconda3/condabin/conda
no change     /home/ubuntu/miniconda3/bin/conda
no change     /home/ubuntu/miniconda3/bin/conda-env
no change     /home/ubuntu/miniconda3/bin/activate
no change     /home/ubuntu/miniconda3/bin/deactivate
no change     /home/ubuntu/miniconda3/etc/profile.d/conda.sh
no change     /home/ubuntu/miniconda3/etc/fish/conf.d/conda.fish
no change     /home/ubuntu/miniconda3/shell/condabin/Conda.psm1
no change     /home/ubuntu/miniconda3/shell/condabin/conda-hook.ps1
no change     /home/ubuntu/miniconda3/lib/python3.7/site-packages/xontrib/conda.xsh
no change     /home/ubuntu/miniconda3/etc/profile.d/conda.csh
modified      /home/user1/.bashrc

==> For changes to take effect, close and re-open your current shell. <==
```  

Then, as conda asked you, close your session and open it again. When you open it you should see something like:
```
(base) user@bash:~$
``` 
Indicating you're in the `base` environment of conda. To activate the main conda environment for our course, where most of the programs we'll be using are installed:
```
(base) user@bash:~$ conda activate eukaryotic_genome_assembly
(eukaryotic_genome_assembly) user@bash:~$
```  

Now you are set to go :wink:  

PS: every time you re-open the terminal, you will be at your `base` environment. To move back to our course environment, just run `conda activate eukaryotic_genome_assembly` again.
