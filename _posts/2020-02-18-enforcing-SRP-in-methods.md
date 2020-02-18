---
layout: post
title: "Enforcing SRP in Methods"
date: 2020-02-18
---

<p>&emsp;According to Metz, methods with a single responsibility have the following benefits:</p>
<ol>
  <li>They have a clarifying effect on the class</li>
  <li>They help avoid the need for comments (especially comments within methods)</li>
  <li>They encourage reuse</li>
  <li>They are easy to move to another class</li>
</ol>

<p>&emsp;The second point in this list is especially important, since methods that require internal comments often have more than one responsibility. If you have to explicitly describe certain behavior, it's best to create a separate method for that code.</p>
<p>&emsp; In order to determine if the methods in my Minesweeper application adhere to the SRP, I will be taking a closer look at the comments I've written for each method. Let's start with the Player class (which is very straighforward): </p>

{% highlight ruby %}

	class Player
		
	attr_accessor: :first_move
		
	def initialize
	@first_move = true
	end
	
	#selects a tile
	def select_tile(tile)
	tile.select
	return
	end

	#flags a tile
	def flag_tile(tile)
	tile.flag
	return
	end

	#unflags a tile
	def unflag_tile(tile)
	tile.unflag
	end
	end
{% endhighlight %}
