---
layout: post
title: "Designing Durable Code: What Should Be a Class?"
date: 2020-02-06
---

&emsp; In my last post, I stated that as I make my way through POODR, I will be revisiting a command line Minesweeper game I've recently completed in order to make the existing code more durable.
<br>
<br>
&emsp; First, let me give a brief overview of the program in its current form:
<br>
<br>
<figure>
<img class="center" height="500" width="500" src="https://user-images.githubusercontent.com/34899774/73974146-d836a700-48f1-11ea-8d36-10defb2f9791.png" alt="Minesweeper Program">
&emsp;<figcaption class="center">&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;Screenshot of program running in console</figcaption>
 </figure>
<p>&emsp;In this Minesweeper program, there are ten mines hidden within the tiles of a 10 by 10 board, and a player must successfully flag all of these tiles in order to win the game.</p>
<img class="center" height="400" width="400" src="https://user-images.githubusercontent.com/34899774/74046053-d1fd0500-499b-11ea-862e-1ec53968fdf6.png" alt="Minesweeper Program">
<p>&emsp;As the user reveals each tile on the board, they may contain numbers indicating how many mines immediately surround it. If a tile has no neighboring mines, its surrounding tiles will be revealed recursively.</p>
<p>The program contains five classes:
<ol>
 <li>Minesweeper (driver class)</li>
 <li>Game</li>
 <li>Tile</li>
 <li>Board</li>
 <li>Player</li>
</ol>
<p>&emsp;Metz's first rule is to look at the nouns in the description of your application when deciding what should and shouldn't be a class.</p>
<p>&emsp;Therefore, let's revisit my program's description from above:<p>
<p>&emsp;"In this <b>Minesweeper program</b>, there are ten <b>mines</b> hidden within the <b>tiles</b> of a <b>board</b>, and a <b>player</b> must successfully flag all of these <b>tiles</b> in order to win the <b>game</b>. As the <b>player</b> reveals each <b>tile</b> on the <b>board</b>, they may contain <b>numbers</b> indicating how many <b>mines</b> immediately surround it. If a <b>tile</b> has no neighboring <b>mines</b>, its surrounding <b>tiles</b> will be revealed recursively"</p>
<p>&emsp;As you can see, I have created classes to represent each of the nouns in the description, except for <b>mines</b> and <b>numbers</b>. This is due to Metz's second rule: a noun that has both <em>data</em> and <em>behavior</em> associated with it deserves to be a class.</p>
<p>&emsp;Whereas each of the other nouns adhere to this rule, mines and numbers fall short. It's true that a tile may contain a mine or a number, and, if selected, will reveal this symbol to the player. Yet both lack the necessary data and behavior which would make them eligible for their own classes.</p>
<p>&emsp;So far, so good! I'm happy with the classes I created for my Minesweeper application. But now comes the hard part: determining if each class has a single responsibility.</p>


 
