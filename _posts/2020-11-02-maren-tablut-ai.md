---
layout: post
title: "Maren Tablut AI"
subtitle: "An artificial intelligence that plays Tablut"
author: "Luca"
header-img: "img/tablut.jpg"
header-mask: 0.3
tags:
  - Java
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

The main rules of Tablut are:
- any piece can move horizontally or verically, but not diagonally
- no piece can ever pass over another piece in its path
- a piece is captured if it is actively sorrounded by two opponent pieces in the same row or column (not diagonal)
- if the king is near the castle, it has to be sorrounded by 3 enemies, while if it is inside the castle it has to be sorrounded by 4 Muscovites 

For further information see [here](https://en.wikipedia.org/wiki/Tafl_games)



## Strategy

The adopted strategy consists in the use of the **Min-Max** algorithm with **alpha-beta pruning**.

You can find my project [here](https://github.com/lucamarini22/TablutAI).


## Evaluation function

I used similar heuristics for either Swedes and Muscovites.

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