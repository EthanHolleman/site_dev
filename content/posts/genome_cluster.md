---
title: "Using local R packages on UC Davis Genome Center cluster"
date: 2020-11-03
tags: ['programming', 'blogs', 'guides']
draft: false
---

I ran into a few issues trying to figure out
how to run batch scripts on the Genome Center
cluster. One of the least documented and hardest to figure out was how to successfully 
load R packages I had installed to my user directory. 

For example I would start R and install a package I needed and load the library with
no problem. 

The code below would run without a problem.

```R
install.packages("glmnet")
library(glmnet)
```

But  then calling the running the same script from a batch file fails to import the library.

I tried multiple possible fixes with no success
until I was tipped of by a current lab member
about the magic word.

```
aklog
```

For some reason putting this right after
the SBATCH lines in the script changed something that allowed SLURM to see the
R packages in my user directory.

It is not currently documented, but when it hopefully is I will link to the page here.