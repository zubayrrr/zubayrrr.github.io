---
created: '2022-02-19T00:00:00.000Z'
desc: ''
id: fjb0h481dug12tdjl464uci
tags:
- TIL
title: Conway S Game of Life
updated: 1652817940732
---
   
Topics::  [maths](../topics/maths.md)   
   
   
---   
   
The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970. It is a zero-player game, meaning that its evolution is determined by its initial state, requiring no further input. One interacts with the Game of Life by creating an initial configuration and observing how it evolves. It is Turing complete and can simulate a universal constructor or any other Turing machine.   
   
## Rules   
   
The universe of the Game of Life is [an infinite, two-dimensional orthogonal grid of square](/wiki/Square_tiling) _cells_, each of which is in one of two possible states, _live_ or _dead_ (or _populated_ and _unpopulated_, respectively). Every cell interacts with its eight _[neighbours](/wiki/Moore_neighborhood)_, which are the cells that are horizontally, vertically, or diagonally adjacent. At each step in time, the following transitions occur:   
   
1.  Any live cell with fewer than two live neighbours dies, as if by underpopulation.   
2.  Any live cell with two or three live neighbours lives on to the next generation.   
3.  Any live cell with more than three live neighbours dies, as if by overpopulation.   
4.  Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.   
   
These rules, which compare the behavior of the automaton to real life, can be condensed into the following:   
   
1.  Any live cell with two or three live neighbours survives.   
2.  Any dead cell with three live neighbours becomes a live cell.   
3.  All other live cells die in the next generation. Similarly, all other dead cells stay dead.   
   
The initial pattern constitutes the _seed_ of the system. The first generation is created by applying the above rules simultaneously to every cell in the seed, live or dead; births and deaths occur simultaneously, and the discrete moment at which this happens is sometimes called a _tick_. Each generation is a _[pure function](/wiki/Pure_function)_ of the preceding one. The rules continue to be applied repeatedly to create further generations.