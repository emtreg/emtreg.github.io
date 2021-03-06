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

<p>&emsp;The second point in this list is especially important, since methods that require internal commentation often have more than one responsibility. If you have to explicitly describe certain behavior, it's best to create a separate method for that code.</p>
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

<p>&emsp;Player's methods are very straightforward and require minimal commentation. They are also closely related to the class's central purpose (allowing a player to make a move). I therefore see no reason to change this class.</p>

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

<p>&emsp;Finally, I've saved the tricker classes for last. For instance, if we take a look at the Board class, it's methods are much more complex than any encountered so far. </p>

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
        #coordinates equal first move coordinates
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

<p>&emsp;I need to make many changes to this class, so let's take a look at each method individually: </p>

<p>&emsp;1. <code><mark>def initialize</mark></code></p>

{% highlight ruby %}

    attr_accessor :height, :width, :tile_array
   
    #initializes the board's dimensions and an array of tiles  
    def initialize(height, width)
     @height = height
     @width = width
     @tile_array = Array.new(height){Array.new(width)}
    end

{% endhighlight %}

<p>&emsp;The <code><mark>initialize</mark></code> method sets the values of the class's instance variables. Metz states that instance variables whould be wrapped in encapsulation methods (i.e. getters and setters) which make it easier to change their values. Ruby's <code><mark>attr_accessor</mark></code> method takes care of this by automatically setting up getters and setters for the indicated variables. There aren't any obvious changes that need to be made to this method, so let's move on.</p>

<p>&emsp;2. <code><mark>def populate</mark></code></p>

{% highlight ruby %}

    #populates the tile_array with Tile objects
    # sets tile's initial symbols
    def populate
     (0..9).each do |row|
      (0..9).each do |column|
       tile_array[row][column] = Tile.new(".","")
      end
     end
    end

{% endhighlight %}

<p>&emsp;The <code><mark>populate</mark></code> method is responsible for populating the tiles in an array of Tile objects (essentially creating the gameboard). One issue I see with this class is that it doesn't follow Metz's recommendation that <b>iteration should be separated from the action being performed on each individual element</b>.</p>

<p>&emsp;To fix this, I created the method <code><mark>add_tile</mark></code> to contain the code within the <code><mark>.each do</mark></code> loop. I also created a <code><mark>get_tile</mark></code> method to access each index in the <code><mark>tile_array</mark></code>. Here are the three resulting methods: </p> 

{% highlight ruby %}

    #populates the tile_array with Tile objects
    def populate
     (0..9).each do |row|
      (0..9).each do |column|
       add_tile(row, column)
      end
     end	
    end

    #adds a new tile to the tile_array
    def add_tile(row, column)
     tile = get_tile(row, column) 
     tile = Tile.new(".","")
    end

    #gets tile from tile_array
    def get_tile(row, column)
     return tile_array[row][column]
    end

{% endhighlight %}

<p>Next is the <code><mark>put_mines</mark></code> method, which needs to be broken down much further.</p>

<p>&emsp;3. <code><mark>def put_mines</mark></code></p>

{% highlight ruby %}

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
      #coordinates equal first move coordinates
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

{% endhighlight %}

<p>&emsp;I've included ample commentation within the method. This tells me that I'll need to break it down into smaller methods in order to enforce the SRP.</p>

<p>&emsp;Here are a few of my thoughts on the changes that should be made to <code><mark>put_mines</mark></code></p>

<ol>
<li> <code><mark>first_move</mark></code> doesn't need to be passed to <code><mark>put_mines</mark></code> 
<br>
&emsp;&emsp; - <code><mark>first_move</mark></code> is an attribute of the <code><mark>Player</mark></code> class, so I will take care of this logic elsewhere
</li>
<br>
<li> I can move the array <code><mark>mine_coordinates</mark></code> to the <code><mark>initialize</mark></code> method
</li>
<br>
<li> I should create separate methods to house the code for:
<br>
&emsp;&emsp; - Generating a random number between 0 and 99
<br>
&emsp;&emsp; - Converting a random number to tile coordinates
<br>
&emsp;&emsp; - Adding tiles to the <code><mark>mine_coordinates</mark></code> array
<br>
&emsp;&emsp; - Setting a tile's hidden symbol to a mine
<br>
</li>
<li> The code within the <code><mark>10.times</mark></code> loop should be placed in a separate method(s)	
</li>
</ol>

<p>&emsp; After implementing the changes listed above, here is the resulting code: </p>

{% highlight ruby %}
    
    #assigns mines to tiles on the board
    def put_mines_on_board(first_move_coordinates)
     10.times {
      put_mine(first_move_coordinates)
     }
     end

     #performs operations for placing a mine
     def put_mine(first_move_coordinates)
      coordinates = get_valid_coordinates(first_move_coordinates)
      add_mine_coordinates(coordinates)
      assign_mine_to_tile(coordinates[0].to_i, coordinates[1].to_i])
     end

     #returns valid coordinates (coordinates that don't already contain a mine and don't equal the first move coordinates)
     def get_valid_coordinates(first_move_coordinates)
      random_number = generate_random_number
      coordinates = generate_random_coordinates(random_number)
      while mine_coordinates.include?(coordinates) || coordinates == first_move_coordinates
       random_number = generate_random_number
       coordinates = generate_random_coordinates(random_number)
      end
      return coordinates
     end

     #adds coordinates to mine_coordinates array
     def add_mine_coordinates(coordinates)
      mine_coordinates.push(coordinates)
     end

     #changes a tile's hidden symbol to a mine
     def assign_mine_to_tile(row, column)
      tile = get_tile(row, column)
      tile.hidden_symbol = "*"
     end
     
     def generate_random_number
      random_number = rand(100)
      return random_number
     end

     #generates random coordinates
     def generate_random_coordinates(random_number)
      coordinates = convert_to_coordinates(random_number)
      return coordinates
     end

     #converts a random number to tile coordinates (ex. 1 -> 01)
     def convert_to_coordinates(number)
      number = number.to_s
      if number.length == 1
       row = "0"
       column = number
      else
       row = number[0]
       column = number[1]
      end
      coordinates = row + column
      return coordinates
     end

{% endhighlight %}

<p>&emsp;By breaking down <code><mark>put_mines</mark></code> into several smaller methods, I have managed to both clean up my code and limit dependencies.</p>

<p>&emsp;Now for the <code><mark>display</mark></code> method: </p>

{% highlight ruby %}

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
     
{% endhighlight %}

<p>&emsp;When it comes to displaying elements, the SRP recommends separating formatting (ex. displaying certain text in red) from the actual data it's being applied on. </p>

<p>&emsp; For now I'm going to break down this method further in order to untangle some of its responsibilites. Then I can revisit the issue at a later point.</p>

{% highlight ruby %}

     #displays the board
     def display
      puts "\n", "\t\t" + "     A   B   C   D   E   F   G   H   I   J" + "\n"
      puts "\n"
      print "\t\t" + row_count.to_s + "    "
      (0..9).each do |row|
       increase_row_count(row_count)
       (0..9).each do |column|
        print_tile(row, column)
       end
      end
      puts "\n\n"
     end

     def increase_row_count(row_count)
      row_count+=1
     end

     def print_tile(row, column)
      tile = get_tile(row, column)
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
     
{% endhighlight %}

<p>&emsp;After refactoring I'm left with three methods. The <code><mark>display</mark></code> method prints the column and row headers as well as the outer symbol associated with each tile. <code><mark>display</mark></code> now calls two additional methods - <code><mark>increase_row_count</mark></code> and <code><mark>print_tile</mark></code> - from within its nested <code><mark>each do</mark></code> loop.</p>








