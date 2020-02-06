---
layout: post
title: "Designing Durable Code"
date: 2020-02-06
---
&emsp; Recently, I started reading Sandi Metz's <em>Practical Object-Oriented Design in Ruby</em> (aka POODR), and it's easy to see why this text is considered a game-changer within the coding community. Although it's impossible to tell exactly what changes an application will undergo in the future, as developers, we have the power to design durable code <em>today</em> in order to reduce the cost of change over time.
<br>
&emsp; It's all about managing dependencies. When it comes to OOD, objects need to know about eachother in order to communicate. And as Metz states, this knowlege creates dependencies between objects.
<br>
&emsp; This book has challenged me to consider my own design choices for past projects. Sure, an application may work fine today, but what if new features need to be introduced down the road? Would my code be up to the challenge of change, or would it merely crumble at the thought? As I continue reading POODR, I've decided to apply Metz's methods to a command line Minesweeper game I recently finished.
