---
layout: post
title: "What Should Be a Class?"
date: 2020-02-06
---

<p>&emsp; In my last post I stated that as I make my way through POODR, I will be revisiting a command line Minesweeper game I've recently completed in order to make the existing code more durable.</p>

<!--more-->

<p>&emsp; First, let me give a brief overview of the program in its current form:</p>

<img class="center" src="https://user-images.githubusercontent.com/34899774/74170631-38339300-4bfb-11ea-9c76-4bffc12f9511.png" alt="Minesweeper Program">
<p>&emsp;In this Minesweeper program, there are ten mines hidden within the tiles of a 10 by 10 board, and a player must successfully flag all of these tiles in order to win the game. A counter keeps track of how many mines are left on the board.</p>
<img class="center" src="https://user-images.githubusercontent.com/34899774/74046053-d1fd0500-499b-11ea-862e-1ec53968fdf6.png" alt="Minesweeper Program">
<p>&emsp;As the player selects each tile, a tile may reveal a number indicating how many mines immediately surround it. If a tile has no neighboring mines, its surrounding tiles will be revealed recursively.</p>
<p>The program contains six classes:</p>
<ol>
 <li>Minesweeper</li>
 <li>Game</li>
 <li>Tile</li>
 <li>Board</li>
 <li>Player</li>
 <li>MineCounter</li>
</ol>
<p>&emsp;Metz's first rule for determining what should be a class is to look at the nouns in the description of the application.</p>
<p>&emsp;Let's revisit my program's description from above:</p>
<p>&emsp;"In this <b>Minesweeper program</b>, there are ten <b>mines</b> hidden within the <b>tiles</b> of a <b>board</b>, and a <b>player</b> must successfully flag all of these <b>tiles</b> in order to win the <b>game</b>. A <b>counter</b> keeps track of how many mines are left on the board. As the <b>player</b> selects each <b>tile</b>, a tile may reveal a <b>number</b> indicating how many <b>mines</b> immediately surround it. If a <b>tile</b> has no neighboring <b>mines</b>, its surrounding <b>tiles</b> will be revealed recursively"</p>
<p>&emsp;I have created classes to represent each of the nouns in the description, except for <b>mines</b> and <b>numbers</b>. This is due to Metz's second rule: a noun that has both <em>data</em> and <em>behavior</em> associated with it deserves to be a class.</p>
<p>&emsp;Whereas each of the other nouns adhere to this rule, mines and numbers fall short. It's true that a tile may contain a mine or a number, and that, if selected, it will reveal this symbol to the player. Yet both lack the necessary data and behavior which would make them eligible for their own classes.</p>
<p>&emsp;So far, so good! I'm happy with the classes I created for my Minesweeper application. But now comes the hard part: determining if each class has a single responsibility.</p>


 
