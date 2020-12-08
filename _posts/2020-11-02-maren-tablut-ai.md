---
layout: post
title: "Maren Tablut AI"
subtitle: "An artificial intelligence that plays Tablut"
author: "Luca"
header-img: "img/tablut.jpg"
header-mask: 0.3
tags:
  - Java
  - Game theory
---

## What is Tablut?

Tablut is an ancient Northen Europe **board game** in which two players (white and black, respectively Swedes and Muscovites) play against each other on a 9x9 board.

- **Swedes**' goal: make the king reaching one of the escapes
- **Muscovites**' goal: capture the king 



![](/img/in-post/board_tablut.png)

The above image shows the **initial configuration** of the board, where:
- light blue squares are escapes
- gray squares are camps
- the orange square is the castle


## Rules

The **main rules** of Tablut are the following:
- any piece can move horizontally or verically, but not diagonally
- no piece can ever pass over another piece in its path
- a piece is captured if it is actively sorrounded by two opponent pieces in the same row or column (not diagonal)
- if the king is near the castle, it has to be sorrounded by 3 enemies, while if it is inside the castle it has to be sorrounded by 4 Muscovites 

For further information see [here](https://en.wikipedia.org/wiki/Tafl_games).



## Search Strategy

The adopted strategy consists in the use of the **Min-Max** algorithm with **alpha-beta pruning**.


```java
// pseudocode of minmax algorithm
function alphabeta(node, depth, α, β, maximizingPlayer) is

if depth == 0 or node is a terminal node then  
  return evaluation of node  
  
if MaxPlayer then      // Max Player  
  value = - inf     
  for each child of node do  
    value = max(value, alphabeta(child, depth - 1, α, β, false))
    α = max(α, value)
    if α >= β then
      break // β cutoff
  return value  
  
else                   // Min player  
  value = + inf
  for each child of node do
    value = min(value, alphabeta(child, depth - 1, α, β, true))
    β = min(β, value)
    if β <= α then
      break // α cutoff
  return value  
```

## Evaluation function

#### What is an evaluation function?

An evaluation function (also called **heuristic**) is a function that tells you how good or bad a particular move is, and it selects the most promising node among the available nodes. The goal of the evaluation function is to reduce either the dimension of the search space and the time spent by exploring it. For this reason, the computation of the heuristic should not last longer than the exploration of the nodes that are not considered anymore. Therefore, it is important to establish a trade-off between **complexity** and **efficiency**. 

I used similar (but opposite) heuristics for either Swedes and Muscovites.

#### Swedes' evaluation function:

- **Positive weights**:
	- white victory
	- number of white pawns
	- number of king's free paths to escapes
- **Negative weights**:
	- number of black pawns
	- number of black pawns that are adjacent to the king
	- minimum king's Manhattan distance to escape	



#### Muscovites' evaluation function:

- **Positive weights**:
	- black victory
	- number of black pawns
	- number of black pawns that are adjacent to the king
	- minimum king's Manhattan distance to escape	
- **Negative weights**:
	- white victory
	- number of white pawns
	- number of king's free paths to escapes


## Link to my project

You can find my project [here](https://github.com/lucamarini22/TablutAI).