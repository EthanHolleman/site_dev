---
title: "What would recursive academic citations look like?"
date: 2021-02-13
tags: ['R', 'blogs', 'Python']
draft: false
---

The way academic citations are measured currently is pretty standardized. 
Authors of article A accrue a citation whenever their article is directly cited 
in article B. But there is likely a large amount of work that was cited by 
article A but not by article B. The authors of this work which indirectly contributed
to article B by contributing to article A (which B cites) will not see a
citation.

What if instead citing one article triggered a recursive call all the way down
the network formed by articles and their citations? Would this end up eventually
citing almost all articles in a field? This is basically the six degrees of
separation question but the academic articles. 

I was wondering about this and so experimented on a small scale using the
[PMC](https://www.ncbi.nlm.nih.gov/pmc/) API and a little bit of Python.
Conveniently, PMC articles are indented by a unique ID, and you can use the
PMC API to get the IDs of all the articles a specific article cites. With this
basic functionality we can build up citation networks that branch out
an arbitrary distance from one specific "root article". This can give 
an idea of an articles connectedness to other academic literature and 
what it would look like if citing one article triggered 
this recursive citation cascade.

Practically, this is limited because not all articles an article cites will
be in PMC and therefore the network will be incomplete, but it is good enough
for a fun experiment.

I tested this out on [this article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4423606/) 
and created the graph below by only
traversing three "layers" deep into the network.

![](/posts/images/k3.png)

That would be a lot of extra citations!

If you would like to try this on your favorite PMC article you can download
the code from the GitHub page [at this link](https://github.com/EthanHolleman/pmcTree). 

