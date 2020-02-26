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

	require_relative 'board'

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

<p>&emsp;Once again, each method in the Tile class performs a simple function. I'll be leaving this class as is.</p>

<p>&emsp;Let's move on to the MineCounter class: </p>

{% highlight ruby %}

	require 'colorize'
	require_relative 'game'

	class MineCounter

	attr_accessor :num_mines

	 #initializes the number of mines
	 def initialize(num_mines)
	  @num_mines = num_mines
	 end

	 #displays the mine count
	 def display
	  puts "\n"
	  puts "     MINES LEFT: ".green + num_mines.to_s.red
	 end

	 #decreases the mine count
	 def decrease
	  self.num_mines = self.num_mines - 1
	  return self.num_mines	
	 end

	 #increases the mine count
	 def increase
	  self.num_mines = self.num_mines + 1
	  return self.num_mines
	 end
	
        end
	
{% endhighlight %}

<p>&emsp;As I mentioned in my last post, the MineCounter class appears to have multiple resonsibilities (which I will address later). However, the methods themselves do not need to be broken down further.</p>

<p>&emsp;I've saved the tricker classes for last. If we take a look at the Board class for instance, it's methods are much more complex than any encountered so far. </p>

{% highlight ruby %}

	require 'colorize'
        require_relative 'tile'

        class Board

        attr_accessor :height, :width, :tile_array

         #initializes the board's dimensions and an array of tiles  
	 def initialize(height, width)
	  @height = height
	  @width = width
	  @tile_array = Array.new(height){Array.new(width)}
	 end

	 #populates the tile_array with Tile objects
	 # sets tile's initial symbols
	 def populate
	  (0..9).each do |row|
	   (0..9).each do |column|
	    tile_array[row][column] = Tile.new(".","")
	    end
	   end
	  end
	  
	 #assigns mines to tiles on the board (changes their hidden symbol to "*")
	 def put_mines(coordinates, first_move)
	  if first_move == true
	   #create array to hold coordinates of tiles containing mines
	   mine_coordinates = Array.new(10)
	   #generate a random number between 0 and 99
	   random_coordinate = rand(100).to_s
	   #convert random number to tile coordinates
	   random_coordinate = convert_random_coordinate(random_coordinate)
           10.times {
            #check if mine_coordinates array already includes randomly generated coordinates or if randomly generated  
	    coordinates equal first move coordinates
	    while mine_coordinates.include?(random_coordinate) || random_coordinate == coordinates
	     #generate a random number between 0 and 99
	     random_coordinate = rand(100).to_s
	     #convert random number to tile coordinates
	     random_coordinate = convert_random_coordinate(random_coordinate)
	    end
	    #add coordinates to mine_coordinates array
	    mine_coordinates.push(random_coordinate)
	    #set tile's hidden symbol to a mine
	    tile_array[random_coordinate[0].to_i][random_coordinate[1].to_i].hidden_symbol = "*"
	   }		
	  end

	  #converts random number to a two digit number (tile coordinates) (ex. 1 -> 01)
	  def convert_random_coordinate(random_coordinate)
	   if random_coordinate.length == 1
	    row = "0"
	    column = random_coordinate
	   else
	    row = random_coordinate[0]
	    column = random_coordinate[1]
	    end
           random_coordinate = row + column
	   return random_coordinate
	  end

	  #displays the board
	  def display	
	   row_count = 0
	   puts "\n", "\t\t" + "     A   B   C   D   E   F   G   H   I   J" + "\n"
	   puts "\n"
	   print "\t\t" + row_count.to_s + "    "

	   (0..9).each do |row|
	    row_count+=1
	    (0..9).each do |column|
	     tile = tile_array[row][column]
	     symbol = tile.visible_symbol
	     if symbol == "."
	      print symbol + "   "
	     elsif symbol == "*"
	      print symbol.red.bold + "   "
	     elsif symbol == " "
	      print symbol + "   "
	     elsif symbol == "F"
	      print symbol.bold.on_light_red + "   "
	     elsif symbol == "1"
	      print symbol.cyan + "   "
	     elsif symbol == "2"
	      print symbol.light_magenta + "   "
	     elsif symbol == "3"
	      print symbol.light_yellow + "   "
	     elsif symbol == "4"
	      print symbol.light_green + "   "
	     elsif symbol == "5" || symbol == "6" || symbol == "7" || symbol == "8"
	      print symbol.red + "   "
	     end
	     if column == 9 && row_count < 10
	      print "\n\n" + "\t\t" + row_count.to_s + "    "
	     end
            end
	   end
	   puts "\n\n"			
	  end

	  #assigns numbers (number of neighboring mines) to tiles on board
	  def put_numbers
	   (0..9).each do |row|
	    (0..9).each do |column|
	     tile = tile_array[row][column]
	     if tile.has_mine != true
	      index = (row.to_s + column.to_s).to_i
	      n  = index-10
	      s  = index+10
	      w  = index-1
	      e  = index+1
	      ne = index-9
	      sw = index+9
	      nw = index-11
	      se = index+11

	      if row == 0 && column == 0
	       neighbors = [e,se,s]
	      elsif row == 0 && column == 9
	       neighbors = [w,sw,s]
	      elsif row == 9 && column == 0
	       neighbors = [n,ne,e]
	      elsif row == 9 && column == 9
	       neighbors = [w,nw,n]
	      elsif row == 0 && (1..8) === column 
	       neighbors = [w,sw,s,se,e]
	      elsif row == 9 && (1..8) === column
	       neighbors = [w,nw,n,ne,e]
	      elsif (1..8) === row && column == 0
	       neighbors = [n,ne,e,se,s]
	      elsif (1..8) === row && column == 9
	       neighbors = [w,nw,n,sw,s]
	      else
	       neighbors = [n,ne,e,se,s,sw,w,nw]
	      end

	      if count_neighboring_mines(neighbors) == 0
	       tile.hidden_symbol = " "
	      else
	       num_neighboring_mines = count_neighboring_mines(neighbors).to_s
	       tile.hidden_symbol = num_neighboring_mines
	      end
	     end
	    end
	   end
	  end

          #counts number of neighboring tiles that contain mines
	  def count_neighboring_mines(neighbors)
	   count = 0
	   neighbors.each {|neighbor|
	    length = neighbor.to_s.length
	    if length == 1
	     row = 0
	     column = neighbor
	    else
	     row = (neighbor.to_s[0]).to_i
	     column = (neighbor.to_s[1]).to_i
	    end
	    tile = tile_array[row][column]
	    if tile.has_mine
	     count+=1
	    end
	   }
	   return count
	  end

          #utilization of flood-fill algorithm
	  def flood_fill_util(x, y)
	   rows = 10
	   columns = 10
	   if coordinates_out_of_bounds(x, y, rows, columns)
	    return
	   else
	    tile = tile_array[x][y]
	    if tile_visited(tile) == true || tile.has_mine
	     return
	    elsif (1..8) === tile.hidden_symbol.to_i
	     tile.select
	     return
	    end
	    tile.select
	    #south
	    flood_fill_util(x+1, y)
	    #north
	    flood_fill_util(x-1, y)
	    #east
	    flood_fill_util(x, y+1)
	    #west
	    flood_fill_util(x, y-1)
	    #southeast
	    flood_fill_util(x+1, y+1)
	    #southwest
	    flood_fill_util(x-1, y+1)
	    #northeast
	    flood_fill_util(x-1, y+1)
	    #northwest
	    flood_fill_util(x-1, y-1)
	   end
	  end

          #performs flood-fill on board
	  def flood_fill(x, y)
	   flood_fill_util(x, y)
	  end

          #determines if a tile has been visited by flood-fill algorithm
	  def tile_visited(tile)
	   if tile.visible_symbol == " "
	    return true
	   end
	    return false
	  end

          #determines if coordinates are out of bounds 
	  def coordinates_out_of_bounds(x, y, rows, columns)
	   if x < 0 || x >= rows || y < 0 || y >= columns
	    return true
	   end
	    return false
	  end

          #reveals all mines on the board
	  def reveal_all_mines
	   (0..9).each do |row|
	    (0..9).each do |column|
	     tile = tile_array[row][column]
	     if tile.has_mine
	      tile.select
	     end
	    end
           end
	  end
        end
	
{% endhighlight %}

<p>&emsp;There's a lot that needs to be changed in this class, so let's take a look at each individual method: </p>

<code class="language-plaintext highlighter-rouge">def initialize</code>

{% highlight ruby %}

        attr_accessor :height, :width, :tile_array
   
         #initializes the board's dimensions and an array of tiles  
         def initialize(height, width)
          @height = height
          @width = width
          @tile_array = Array.new(height){Array.new(width)}
         end

{% endhighlight %}

<p></p>



