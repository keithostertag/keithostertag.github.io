---
layout: post
title: "Programmatically generating cells vs static definition in Python"
date: 2017-08-15
tags: python performance timeit
---

 Here is a link to a discussion on Treehouse which points out several issues related to the performance difference between programmatically generating cells vs static definition, as used for a game: [Programmatically Generate CELLS](https://teamtreehouse.com/community/programmatically-generate-cells)

 Gives an example of using the timeit function to compare the performance of programmatically generating a 4x4 grid of cells versus hard-coding the static definition. In this case, the static definition was about 23 times faster to execute.
