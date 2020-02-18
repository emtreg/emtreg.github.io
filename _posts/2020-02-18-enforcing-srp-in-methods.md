---
layout: post
title: "Enforcing Srp in Methods"
date: 2020-02-18
---

<p>&emsp;According to Metz, methods with a single responsibility have the following benefits:</p>
<ol>
  <li>They have a clarifying effect on the class</li>
  <li>They help avoid the need for comments (especially comments within methods)</li>
  <li>They encourage reuse</li>
  <li>They are easy to move to another class</li>
</ol>

<p>&emsp;The second point in this list is especially important, since methods that require internal comments often have more than one responsibility. If you have to describe certain behavior within a method, it's best to create a separate method for that code.</p>
