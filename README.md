# Game of Life
An experimental toy project that implements a totally original idea--Game of Life by John Horton Conway. As an attempt to review some nice practices, the following decisions are made regarding the implementation:
- We will use c++20, and will try to capitalize its features, as an attempt to gauge the usability of modern c++;
- We will follow a design that is as close to OOP as possible, as an attempt to revisit the difficulty of c++ code design;
- We will follow nice git practices, while not being too ceremonial;
- We will honor a rapid release model of development, ideally, opimizations on the simulation can be made modularly.


## Objectives
1. From a given user input (see [Specifications](#specifications) for formats) board, render a gif that demonstrate the state of game as the Game progress. 
2. In the rendered gif, we should detect any potential periodic behaviour, and loop on that when needed. If no periodicity is detected in a reasonably large number of steps, the gif should either halt at a set number of steps or loop back to the start of the game. 
3. We should implement a function that checks the convergence of two starting states. Ideally, we should apply some theoretic criteria before going brute-force check. 


## Specification

### Input Format
User supplies a plain text file that looks like the following example:
```
4 5
-----
--*--
-**--
-----
```
Where the first line consists of two integers, between [1, 5000], which discribes the dimension of the board by `<number of rows> <number of columns>`.

`-` symbol represents an empty cell, where `*` encodes a filled cell. 


## Design

### Data Structure
Due to the time-sequential nature of the board state, we will encode the board object in the following container: 

`Board` object structure:
- `period`: int ~ the length of repeatition
- `starting state`: State ~ the very initial configuration of the board, specified by the user
- `non-periodic states`: ordered list of States ~ the first State in this list represents the State of board initially specified by the user
- `periodic states`: ordered list of States ~ guarantees that the size equals to `period`. Also ensures that the last State in this list will evolve into the first State in this list (cyclic nature)
- function interfaces:
    - `constructor`: builds the `Board` object by filling in `starting stage`, leaving everything else the same. 
    - `evolve`: calculate the `non-periodic states` and `periodic staes` based on the `starting state`, once the `periodic states` is determined, fill in `period` value as well.

