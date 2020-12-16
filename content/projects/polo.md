---
title: "Polo"
date: 2020-11-22T13:49:27-08:00
tags: ['programming', 'crystallography', 'research']
draft: false
---

This was a project I worked on as part of the [BioXFEL](https://www.bioxfel.org/)
summer internship program. I worked with [Dr. Sarah Bowman](https://hwi.buffalo.edu/scientist-directory/sbowman/)
and other members of Hauptman-Woodward Medical Research Institute (HWI).

If you are short on time and don't want to read these entire post here are the
important links.

- [Polo website](https://hauptman-woodward.github.io/Marco_Polo/)
- [Polo poster]()
- [Video Presentation]()









# So what is "high-throughput crystallography"?

Before answering this question, it will be helpful to understand what is crystallography
in the context of the biological sciences and why it is so important to our
understanding of the sub-microscopic natural world. 





Broadly, crystallography refers to the science of determining the arrangement of
atoms in any crystalline solid. This is important to a number of fields such as
mineralogy, metallurgy but also has great importance to the biological sciences
due to how the special properties of molecules in crystals allows for 






Lets say you are trying to develop a drug to treat a disease where too much of
a protein is being made, or maybe it is made when at the wrong time (this
is typical of many cancerous cells). 

You know your protein of interest contains a region
that is binding to other molecules, receptors, etc and then causing some 
downstream biological response. If you knew exactly what that
important region looked like you could more easily design a drug that was so
effective at binding to your protein of interest you could stop it dead in the
cell. 

Currently, the most common way to "see" your protein of interest remains 
X-ray crystallography (although keep your eye on [cryo-EM](https://www.nature.com/articles/s41467-019-10368-w)), which
requires crystallization of your protein of interest.

{{< figure src="/projects/images/Lysozyme.jpg" height="400" width="400"
title="Crystal structure of Lysozyme as rendered by David Goodsell doi:10.2210/rcsb_pdb/mom_2000_9">}}


However, in general, large macromolecules like proteins are do not like
transforming into amino acid rock candy and would instead be much happier floating
around in solution except under *extremely special* conditions.

It is currently not feasible to predict the conditions that will cause a
marcomolecule to crystalize and so growing these biological crystals is a
common bottleneck for academic and industrial researchers alike.

High-throughput crystallography takes an enlightened spaghetti at the wall
approach. Using liquid handling robotics and automated microscopy, proteins are screened
against thousands of conditions in large plates. This allows researchers to both
outsource the tedious work of screening samples to high-throughput screening centers
like the one at HWI and screen thousands more 
chemical conditions than they could manually greatly increasing the chances of
a successful crystallization. 

# The spaghetti problem and solutions

The number of conditions that high-throughput approaches is at the same time
its selling point and greatest challenge. So much spaghetti gets thrown at the
wall that it quickly becomes overwhelming for those unprepared to carbo-load. 

{{< figure src="/about/projects/images/lots_of_data.png" height="400" width="400" 
title="Representation of the image data that would be created by a typical high-throughput screen of one protein sample at HWI. Each pixel represents one image a researcher would have to manually review.">}}

In a typical week a user screening three samples could receive over 5000 images
that would need to be manually reviewed for evidence of a successful crystallization;
an extremely time consuming task with the dreaded combination of requiring
focused concentration while being extremely monotonous.

Fortunately, advances in machine learning have allowed for the development of
models that can do this work automatically and with reasonable accuracy. The
most recent iteration of this has been the MARCO (Machine Recognition of 
Crystallization Outcomes) model published by [Andrew Bruno *et al* in 2018](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0198883). 

# Polo motivation

The MARCO model opened the door for experts to automatically classify
crystallization images, but lack of a graphical interface and data mangement
program made it largely inaccessibly to users without Python and or command
line experience. Therefore the goal of my project was to produce a free, easy to use
graphical interface for both HWI and non-HWI users that would integrate the MARCO
model with the best features of existing image review software.

# Outcome

Despite the short development timeline (largely 12 weeks over the summer) I would
say Polo was a success. 

Over that period of time I was able to release versions of the program for
Linux, Mac and Windows, created a website to host the documentation ([which you
can view here](https://hauptman-woodward.github.io/Marco_Polo/)) and began drafting
a manuscript which is currently under review by the Journal of Applied Crystallography.

Here are a few images of some of the Polo interfaces, for full details, user-guides,
code documentation and video tutorials please visit the 
[Polo website](https://hauptman-woodward.github.io/Marco_Polo/).

{{< figure src="/about/projects/images/Fig2_update.png" height="600" width="600" 
title="Composited image of different viewing options of the Polo slideshow viewer interface">}}

{{< figure src="/about/projects/images/Fig3.png" height="600" width="600" 
title="Composited image of different viewing options of the Polo plate viewer interface">}}

The most recent version of Polo can be downloaded [from this link](https://github.com/Hauptman-Woodward/Marco_Polo/releases).
Beyond automatic image classification via MARCO, Polo includes a number of useful
tools and interfaces. HWI and non-HWI users alike can

- Download images directly from Polo using the integrated FTP client
- Export their results to powerpoint presentations, csv or json files
- View images as slideshows or in arrays of up to 96 images
- Easily associate visible light microscopy images to alternative spectrums such as UV-TPEF and quickly swap between the two


Polo is also fully open source and free for academic and commercial use!

# Future goals and collaboration

I still work to maintain Polo and do my best to respond to questions and fix
bugs reported by users. If any of the above is interesting to you or you have
questions about how Polo might be able to help you, your lab or organization
please reach out! I would love to talk. 

In the future I would like involve researchers from other high-throughout
facilities to extend the functionality and flexibility of Polo.















