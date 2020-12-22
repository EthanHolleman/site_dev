---
title: "Plotting COG-UK Data"
date: 2020-12-21
tags: ['programming', 'R', 'blogs']
draft: false
---

The [Covid-19 Genomics UK Consortium](https://www.cogconsortium.uk/data/)
has been collecting and sequencing thousands of COVID-19 genomes from
patients in the UK and around the world. 

All of their data is publicly available. Here I played around with the
phylogenetic tree they have created from global alignments of all the genomes
they have sequenced. 

You can download the tree in Newick format from their [data page](https://www.cogconsortium.uk/data/) which also hosts sequences and the alignment files.

## Visualizing the COVID-19 phylogenetic tree by country of origin

![](/posts/images/cog_tree_by_country.png)


## Genome count by country

Note this plot is log scale in the y-axis.

![](/posts/images/genomes_by_country.png)

Code used to make the above plots can be viewed [here](/posts/code/uk_cog.r).

## 16 most prevalent UK COVID-19 lineages

Density plots showing the number of genomes of the 16 most prevalent lineages
detected by COG-UK.

![](/posts/images/top_16_strains.png)

[Cov-lineages](https://cov-lineages.org/lineages/lineage_B.1.177.html) has
a lot of good information on all of these lineages, including `B.1.177` which
has recently set off alarms as the new "mutant UK strain".





