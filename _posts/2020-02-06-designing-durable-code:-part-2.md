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
<p>In this Minesweeper program, there are ten mines hidden within the tiles of a board, and a player must successfully flag all of these tiles in order to win the game</p>
<img class="center" height="400" width="400" src="https://user-images.githubusercontent.com/34899774/74046053-d1fd0500-499b-11ea-862e-1ec53968fdf6.png" alt="Minesweeper Program">
<p>As the user reveals each tile on the board, it may contain a number indicating how many mines immediately surround it. If a tile has no neighboring mines, its surrounding tiles will be revealed recursively using a flood fill algorithm.</p>
<p>The program contains five classes:
<ol>
 <li>Minesweeper (driver)</li>
 <li>Game</li>
 <li>Tile</li>
 <li>Board</li>
 <li>Player</li>
</ol>

<p>According to Sandi Metz, when deciding what should be a class, you should look at the nouns in the description of your application.</p>
<p>Let's revisit the description of my Minesweeper application from above:<p>
<p>"In this <b>Minesweeper program</b>, there are ten <b>mines</b> hidden within the <b>tiles</b> of a <b>board</b>, and a <b>player</b> must successfully flag all of these <b>tiles</b> in order to win the <b>game</b>"</p>


 
