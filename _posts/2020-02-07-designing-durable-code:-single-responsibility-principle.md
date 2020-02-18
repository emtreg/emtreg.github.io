---
layout: post
title: "Single Responsibility Principle"
date: 2020-02-07

---

<p>&emsp;In POODR Metz states that ideally, a class should do the smallest possible useful thing. This helps to limit dependencies by ensuring that classes are "reusable, pluggable units of well-defined behavior that have few entanglements". In order to achieve this, developers should aim to follow the <b>Single Responsiblity Principle</b> (SRP) when designing and creating classes. The goal of this principle is to increase cohesion within classes by ensuring that everything in a class (i.e. its data and behavior) is related to that class's central purpose.</p>

<p>&emsp;Metz recommends two methods for determining if a class has a single responsibility:</p>
<p><b>1. "Interrogate" the class</b></p>
<p>&emsp;This strategy involves rephrasing each method in a class as a question. If it makes sense to pose a resulting question to the class, then that method is likely related to the class's central purpose. For example, in the case of my Minesweeper program the Tile class contains a method that flags a tile. It would therefore make sense to ask the Tile class, <em>"Tile, are you flagged?"</em>. The same, however, could not be said of the Board class (<em>"Board, are you flagged?"</em>).
<p><b>2. Describe the class in one sentence</b></p>
<p>&emsp; If the sentence contains the word 'and' then the class most likely has more than one responsibility. If it contains the word 'or', then it has multiple responsibilities which may not even be related.</p>

<p>Now, let's apply the second method to each of the classes in my Minesweeper program:</p>

<p><b>Tile:</b></p>
<p>&emsp;The Tile class <b>updates a tile's symbols in response to the tile being selected/flagged/unflagged</b>.</p>

<p><b>Board:</b></p>
<p>&emsp;The Board class <b>populates the gameboard</b>, <b>performs flood-filling</b> and <b>displays the board</b>.</p>

<p><b>MineCounter:</b></p>
<p>&emsp;The MineCounter class <b>keeps track of how many mines are left on the board</b> and <b>displays that number to the user</b>.</p>

<p><b>Player:</b></p>
<p>&emsp;The Player class <b>allows the player to make a move</b> (i.e. select, flag, unflag a tile).</p>

<p><b>Game:</b></p>
<p>&emsp;The Game class <b>carries out the operations of the game until it is won/lost</b>.</p>

<p><b>Minesweeper:</b></p>
<p>&emsp;The Minesweeper class <b>begins a new game</b>.</p>

<p>&emsp;After applying this method to each class, it's clear that both the Board and MineCounter classes have multiple responsibilities. It's important to note, however, that how I choose to address this problem is far from clear-cut. <a href="https://deviq.com/single-responsibility-principle/">If a particular class is stable and isn’t causing needless pain as a result of changes, there is little need to change it.</a> </p>
