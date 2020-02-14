---
layout: post
title: "Single Responsibility Principle"
date: 2020-02-07

---

<p>&emsp;In POODR Metz states that ideally, a class should do the smallest possible useful thing. This helps to limit dependencies by ensuring that classes are "reusable, pluggable units of well-defined behavior that have few entanglements". In order to achieve this, developers should follow the <b>Single Responsiblity Principle</b> (SRP) when designing and creating classes. This principle aims to increase cohesion within classes by ensuring that everything in a class (i.e. its data and behavior) is related to its central purpose.</p>

<p>&emsp;Metz recommends two methods for determining if a class has a single responsibility:</p>
<p><b>1. "Interrogate" the class</b></p>
<p>&emsp;This strategy involves rephrasing each method in a class as a question. If, when posed to the class, the resulting question makes sense, then that method is likely related to the class's central purpose. For example, in the case of my Minesweeper program the Tile class contains a method that flags a tile. It would therefore make sense to ask the Tile class, <em>"Mr. Tile, are you flagged?"</em>. The same, however, could not be said of the Board class (<em>"Mr. Board, are you flagged?"</em>).
<p><b>2. Describe the class in one sentence</b></p>
<p>&emsp; If the sentence contains the word 'and' then the class most likely has more than one responsibility. If it contains the word 'or', then it has multiple responsibilities which may not even be related.</p>

<p>Now, let's apply the second method to each of the classes in my Minesweeper program:</p>

<p><b>Tile Class:</b></p>
<p>&emsp;The Tile class <b>updates a tile's symbols in response to an action being performed on it</b> (i.e. the tile is selected/flagged/unflagged).</p>

<p><b>Board Class:</b></p>
<p>&emsp;The Board class <b>populates the gameboard</b>, <b>performs flood-filling</b> and <b>displays the board</b>.</p>

<p><b>MineCounter Class:</b></p>
<p>&emsp;The MineCounter class <b>keeps track of how many mines are left on the board</b> and <b>displays that number to the user</b>.</p>

<p><b>Player Class:</b></p>
<p>&emsp;The Player class <b>allows the player to make a move</b> (i.e. select, flag, unflag a tile).</p>

<p><b>Game Class:</b></p>
<p>&emsp;The Game class <b>carries out the operations of the game until it is over</b> (won/lost).</p>

<p><b>Minesweeper Class:</b></p>
<p>&emsp;The Minesweeper class <b>begins a new game</b>.</p>

<!--
<p>Tile class:</p> 
<table class="center">
  <tr>
    <th>Method</th>
    <th>Question</th>
    <th>Makes Sense?</th>
  </tr>
  <tr>
    <td>has_mine</td>
    <td>"Mr. Tile, do you have a mine?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>select</td>
    <td>"Mr. Tile, are you selected?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>flag</td>
    <td>"Mr. Tile, are you flagged?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>unflag</td>
    <td>"Mr. Tile, are you unflagged?"</td>
    <td align="center">✅</td>
  </tr>
</table>
<p>Board class:</p>
<table class="center">
  <tr>
    <th>Method</th>
    <th>Question</th>
    <th>Makes Sense?</th>
  </tr>
  <tr>
    <td>populate</td>
    <td>"Mr. Board, are you populated?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>put_mines</td>
    <td>"Mr. Board, have mines been placed on you?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>put_numbers</td>
    <td>"Mr. Board, have numbers been placed on you?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>display</td>
    <td>"Mr. Board, are you displayed?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>reveal_all_mines</td>
    <td>"Mr. Board, are all of your mines revealed?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>flood_fill / flood_fill_util</td>
    <td>"Mr. Board, have you been flood filled?"</td>
    <td align="center">❓</td>
  </tr>
</table>
<p>MineCounter class:</p>
<table>
  <tr>
    <th>Method</th>
    <th>Question</th>
    <th>Makes Sense?</th>
  </tr>
  <tr>
    <td>display</td>
    <td>"Mr. MineCounter, are you displayed?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>increase</td>
    <td>"Mr. MineCounter, has your count been increased?"</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>decrease</td>
    <td>"Mr. MineCounter, has your count been decreased?"</td>
    <td align="center">✅</td>
  </tr>
</table>
<p>Player class:</p>
<table>
  <tr>
    <th>Method</th>
    <th>Question</th>
    <th>Makes Sense?</th>
  </tr>
  <tr>
    <td>make_move</td>
    <td>"Mr. Player, have you made a move?"</td>
    <td align="center">✅</td>
  </tr>  
</table>
<p>Game class:</p>
<p>Minesweeper class:</p>
-->
