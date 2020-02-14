---
layout: post
title: "Designing Durable Code: Single Responsibility Principle"
date: 2020-02-07

---

<p>&emsp;In POODR Metz states that ideally, a class should do the smallest possible useful thing. This helps to limit dependencies by ensuring that classes are "reusable, pluggable units of well-defined behavior that have few entanglements". In order to achieve this, developers should follow the <b>Single Responsiblity Principle</b> (SRP) when designing and creating classes. This principle aims to increase cohesion within classes by ensuring that everything in a class (i.e. its data and behavior) is related to its central purpose.</p>

<p>&emsp;Metz recommends two methods for determining if a class has a single responsibility:</p>
<p>1. "Interrogate" the class</p>
<p>&emsp;This strategy involves rephrasing each of a class's methods as questions and then posing each question to the class. For example, in the case of my Minesweeper program the Tile class contains a method that flags a tile. I may therefore ask the Tile class, <em>"Mr. Tile, are you flagged?"</em> You can tell if a method is related to a class's central purpose if its corresponding question makes sense. If I were to ask the same question of the Board class, (<em>"Mr. Board, are you flagged?"</em>) it no longer makes sense within this context.
<p>2. Attempt to describe the class in one sentence</p>
<p>&emsp; If the sentence contains the words 'and' or 'or', the class has more than one responsibility.</p>

<p>I am now going to apply the second method to each class in my Minesweeper program:</p>

<p>Tile class:</p>
<p>Board class:</p>
<p>Player class:</p>
<p>Game class:</p>
<p>Minesweeper class:</p>
