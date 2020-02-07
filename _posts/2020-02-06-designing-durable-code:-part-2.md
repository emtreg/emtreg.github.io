---
layout: post
title: "Designing Durable Code: Part 2"
date: 2020-02-06
---

<p><b>Designing Classes with a Single Responsibility</b></p>
&emsp; In my last post, I stated that as I make my way through POODR, I will be revisiting a command line Minesweeper game I've recently completed in order to make the existing code more durable.
<br>
<br>
&emsp; First, let me give a brief overview of the program in its current form:
<br>
<br>
<img class="center" height="400" width="400" src="https://user-images.githubusercontent.com/34899774/73974146-d836a700-48f1-11ea-8d36-10defb2f9791.png" alt="Minesweeper Program">
<p class="center">Screenshot of program running in console</p>
<p>The program has all of the functionality of a classic Minesweeper game. That is, there are 10 mines hidden within the tiles of a board, and a user must successfully flag all of these tiles in order to win the game.</p>
<img class="center" height="400" width="400" src="https://user-images.githubusercontent.com/34899774/74046053-d1fd0500-499b-11ea-862e-1ec53968fdf6.png" alt="Minesweeper Program">
<p>As the user reveals each tile on the board, it may contain a number indicating how many mines immediately surround it. If a tile has no neighboring mines, its surrounding tiles will be revealed recursively using a flood fill algorithm.</p>


 
