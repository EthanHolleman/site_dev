---
title: "Recursively extract markdown tables to separate csv or tsv files"
date: 2021-07-19
tags: ["blogs", "Python", "Markdown"]
draft: true
---

I use the Markdown language a lot. Most often for this website and for
my [benchwork lab notebook](https://github.com/EthanHolleman/lab-notes).
I wanted a way to easily convert all the markdown formatted tables within a
directory filled with files to more easily readable delimited type files. I did
not see a command line program to do this so I created a small Python script
to get the job done.

For example, lets say you wanted to extract all the markdown tables from
this website's content directory to tsv files.

```
content/posts
├── california_legislature_search.md
├── christmas_card.md
├── CIDA_hackathon.md
├── cluster_computing_uc_davis.md
├── code
│   ├── covid_hos.r
│   ├── farm_install_gromacs.sh
│   ├── teams.py
│   ├── uk_cog.r
│   └── vietnam.r
├── cog_sars.md
├── conway_game_of_life_implementation.md
├── covid_data.md
├── crick-setup.md
├── data
│   ├── parse_table.txt
│   ├── PHMIS_data.csv
│   └── playingcards-io-export.zip
├── davis-wifi-on-linux.md
├── death_valley.md
├── docs
│   └── RAND_MG1086.pdf
├── EPO.md
├── extract-markdown-tables.md
├── genome_cluster.md
├── gromacs_install.md
├── GSA_rep.md
├── images
│   └── myPlot.html
├── _index.md
├── leafly_data.md
├── letter_to_d113.md
├── ligand_plotting.md
├── nbi_encoding.md
├── PanSeer_test.md
├── polo_published.md
├── potodds.md
├── putah_fishing.md
├── recursive_citations.md
├── running_winnings.md
├── skribbl.io_words.md
├── tonkatsu.md
├── vietnam_data.md
├── yosemite.md
└── zoom_poker.md
```

You could then run `python mdTablePuller.py content/posts tables` to extract
all tables to `tsv` files and store them in an existing directory called 
`tables`.

