---
layout: post
title: "Designing Durable Code: Single Responsibility Principle"
date: 2020-02-07

---

<p>&emsp;In POODR Metz states that ideally, a class should do the smallest possible useful thing. This helps to limit dependencies by ensuring that classes are "reusable, pluggable units of well-defined behavior that have few entanglements". Developers can achieve this by adhering to the <b>Single Responsiblity Principle</b> (SRP) when designing and creating classes. This principle aims to increase cohesion within classes. A class is said to be highly cohesive when everything in the class is related to its central purpose.</p>

<p>&emsp;Metz recommends two strategies for determining if a class has a single responsibility:</p>
<p>1. "Interrogate" the class</p>
<p>&emsp;Simply put, ask each class, <em>"What is your function?"</em></p>
<p>&emsp;If the answer to this question is neither straightforward nor concise, it does not follow the SRP.</p>
<p>2. Attempt to describe the class in one sentence</p>
<p>&emsp; If this sentence contains the words 'and' or 'or', the class has more than one responsibility.</p>
