---
title: "Implementing and visualizing Conway's Game of Life"
date: 2021-04-16
tags: ['programming', 'Python', 'blogs']
draft: false
---

I took the day off today to recover from second round of the covid vaccine and
spent a little while implementing my own version of 
[Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)
in Python.

Here's an example of a simulation involving a grid of 500 x 500 cells. When
initializing the first generation each cell had a 0.3 probability of starting
as a living cell (start-as-living probability). Increasing this value will
increase the number of cells the grid is initialized with.
I ran the simulation for 100 generations.

![](/posts/images/conway_0.3.gif)

and with a 0.1 start-as-living probability.

![](/posts/images/conway_0.1.gif)

I was curious how changing the starting probability of a cell starting the
simulation as living would effect the game as it progressed. So I ran
250 generation simulations with start-as-living-cell probabilities of
0.1, 0.3, 0.5 and 0.8. Each start-as-living-cell probability plot is composed
of 100 simulations.

![](/posts/images/conway_sim.png)

The results where pretty much as one might expect given the game's rules. 
Intermediate starting populations level off as the number of generations increase.
What was interesting to see was how quickly the number of cells drop if the
population exceeds the "carrying capacity" of the grid.

If you are interested you can download my implementation from 
[GitHub at this link](https://gist.github.com/EthanHolleman/154938f1d630a7ccc3a0f5892be87af6).
