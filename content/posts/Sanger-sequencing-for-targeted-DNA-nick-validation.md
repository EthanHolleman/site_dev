---
title: "Utilizing Sanger sequencing for targeted DNA nick validation"
date: 2022-03-08
tags: ['Molecular biology', 'blogs']
draft: true
---

# TLDR?

Hate fluff and just want the protocol? Click this link.



# Protocol

## Experimental setup

To get started it is best to validate you will actual be able to detect nicks in your sequence
using a positive control.

Select a plasmid containing a [Nt.BspQI](https://www.neb.com/products/r0644-ntbspqi#Product%20Information).
Next identify a region 100-200 bp away from the target site that is suitable 
for a primer. It is critical that your primer bind to the strand that is
nicked. For example Nt.BspQI nicks the top strand so we would want to design
a reverse primer to interogate this nick as it will force DNA polymerase
to use the top strand as the template strand during the Sanger sequencing
reaction. If we were to use a forward primer the bottom strand would
be used as the template. Since there is no nick our read will appear normal.

Once your primer and plasmid are in hand treat your plasmid with Nt.NspQI
according to the manufactours recommendations. Make sure to treat enough plasmid
to sequence as Sanger sequencing providers often require relatively high concentrations
(80 ng/ul). 

Confirm your digestion was successful by running your treated plasmid sample on an agarose
gel against the untreated control. You should see 100% of the treated sample
shift up to the linear height while the untreated runs at the supercoiled
height.

Finally prepare and submit your samples for sequencing according to the
providers instructions. Before submitting your samples reach out to your
sequencing provider and ask about the specifics of their reactions and if they
preform any pre-processing or have any additives (ligases) in their reactions
to make them more robust. Commercial sequencing providers are incenivised to
make their reactions as robust as possible to minor DNA damage such as nicks
in order to provide consistent sequenicing results but this is exactly what
we don't want in this specific, unorthdox usage of Sanger.

Intially I used a commerical service for my nicked samples and no reads
terminated at Nt.BspQI target sites. I had much better success using the on-campus
sequencing center as I could more specificaly relay what I was doing and
the requirements for the reaction.



Just prior to sample submission boil samples for 5 minutes
and then immediately place into -80C freezer. This denaturization and freeze step
seems to help keep the strands seperated and improve nick detection during the
sequencing reaction. After freezing keep your samples on ice and submit them
to the sequencing provider on ice if possible.



It is best to submit at least one untreated control
to confirm your reaction worked correctly. However before sending your
samples out please contact the sequencing provider to determine 

## Data analysis



