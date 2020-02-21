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

<!--more-->

<p>&emsp;The second point in this list is especially important, since methods that require internal comments often have more than one responsibility. If you have to explicitly describe certain behavior, it's best to create a separate method for that code.</p>
<p>&emsp; In order to determine if the methods in my Minesweeper application adhere to the SRP, I will be taking a closer look at the comments I've written for each method. Let's start with the Player class: </p>

{% highlight ruby %}


	class Player
		
	 attr_accessor :first_move
	 
	 #sets first_move to true
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

<p>&emsp;As you can see, Player's methods are very straightforward and require minimal commentation. They are also closely related to the class's central purpose (allowing a player to make a move). I therefore see no reason to change this class.</p>

<p>&emsp;Next up is the Tile class: </p>

{% highlight ruby %}

	require_relative 'Board'

	class Tile

	 attr_accessor :visible_symbol, :hidden_symbol

	 #sets the tile's initial symbols
	 def initialize(visible_symbol, hidden_symbol)
	  @visible_symbol = visible_symbol
	  @hidden_symbol = hidden_symbol
	 end

	 #indicates if a tile contains a mine
	 def has_mine
	  if hidden_symbol == "*"
	   return true
	  end
	  return false
	 end

	 #'selects' a tile by revealing the tile's hidden symbol
	 def select
	  @visible_symbol = @hidden_symbol
	 end

	 #'flags' the tile by changing its visible symbol to a flag symbol
	 def flag
	  @visible_symbol = "F"
	  return
	 end

	 #'unflags' the tile by reverting its visible symbol to its original symbol
	 def unflag
	  if visible_symbol == "F"
	   @visible_symbol = "."
	  end
	 end
	
        end
	
{% endhighlight %}

<p>&emsp; Once again, each method is very straightforward. I feel no need to break them up further.</p>



