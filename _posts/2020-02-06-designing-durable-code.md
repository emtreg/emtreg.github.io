---
layout: post
title: "Designing Durable Code"
date: 2020-02-06
---

<!--<img src="https://user-images.githubusercontent.com/34899774/73970643-7d01b600-48eb-11ea-9339-f730a6dae4ba.png" alt="laptop" align="left">-->
<p>&emsp; Recently, I started reading Sandi Metz's <em>Practical Object-Oriented Design in Ruby</em> (aka POODR), and it's easy to see why this text is considered a game-changer within the coding community.</p>
  <!--more--> 
<p>&emsp;Although it's impossible to tell exactly what changes an application may undergo in the future, developers have the power to design durable code <em>today</em> in order to reduce the cost of change over time.</p>

<p>&emsp; It's all about managing dependencies. When it comes to OOD, objects need to know about eachother in order to communicate. As Metz states, this knowlege creates dependencies between objects (which can inevitably make them resistant to change and picky). So, although objects need to know about eachother in order for a program to function effectively, the key is to limit just how much outside information they're privy to.</p>

<p>&emsp; This book has challenged me to consider my own design choices for past projects. An application may function correctly for the time being, but what if new features need to be introduced down the road? Would my code be up to the challenge, or would these changes make it a nightmare to refactor? As I continue reading POODR, I've decided to apply Metz's methods to a command line Minesweeper game I recently coded in Ruby.</p>
