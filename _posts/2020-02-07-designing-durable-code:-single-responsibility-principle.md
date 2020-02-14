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

<p>I am now going to apply the second method to each class in my Minesweeper program:</p>

<p>Tile class:</p>
<p>Board class:</p>
<p>Player class:</p>
<p>Game class:</p>
<p>Minesweeper class:</p>
