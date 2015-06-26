**CODE BLOCKS**
```
do ... end

-or-

{ ...}
```
```
<variable>.each do |x|
        ...
end
```

**HASH TABLES AND SYMBOLS**
```
<variable>.to_s - convert to string
<variable>.respond_to (:<symbol>) - can <symbol> be performed on <variable>
<variable>.nil - check nil value

<string>.to_sym - convert to symbol
<string>.intern - convert to symbol

<hash_table>.each_key - each key in a hash table
<hash_table>.each_value - each value in a hash table

<number>.times { ... }  - repeat <number> times
<number>.upto(<maximum>) { ... }
<number>.downto(<minimum>) { ... }

<array>.collect { ... }
<array>.map(&<proc>)

<proc>.call
 
.select - from a list

:<symbol>
:<symbol>.to_s      converts to a string
"<string>".to_sym   converts to a symbol

```
```
strings = ["HTML", "CSS", "JavaScript", "Python", "Ruby"]
# Add your code below!
symbols = []   # initialize array
strings.each do |x|
    symbols.push(x.to_sym)
end
```

**HASH TABLES**
```
<hash_table_name> = {
    <key> => <value>    # rocket notation
    :<key> => <value>   # pre Ruby 1.9 notation
    <key>: => <value>   # post Ruby 1.9 notation
}
```

**TIMING EXAMPLE**
```
require 'benchmark'

string_AZ = Hash[("a".."z").to_a.zip((1..26).to_a)]
symbol_AZ = Hash[(:a..:z).to_a.zip((1..26).to_a)]

string_time = Benchmark.realtime do
  100_000.times { string_AZ["r"] }
end

symbol_time = Benchmark.realtime do
  100_000.times { symbol_AZ[:r] }
end

puts "String time: #{string_time} seconds."
puts "Symbol time: #{symbol_time} seconds."
```

Selecting from a hash table
```
movie_ratings = {
  memento: 3,
  primer: 3.5,
  the_matrix: 5,
  truman_show: 4,
  red_dawn: 1.5,
  skyfall: 4,
  alex_cross: 2,
  uhf: 1,
  lion_king: 3.5
}
# Add your code below!
good_movies = []
good_movies = movie_ratings.select {|name, rating| rating > 3}
```

**PROGAM EXAMPLE**
```
movies = {
  Memento: 3,
  Primer: 4,
  Ishtar: 1
}

puts "What would you like to do?"
puts "-- Type 'add' to add a movie."
puts "-- Type 'update' to update a movie."
puts "-- Type 'display' to display all movies."
puts "-- Type 'delete' to delete a movie."

choice = gets.chomp.downcase
case choice
when 'add'
  puts "What movie do you want to add?"
  title = gets.chomp
  if movies[title.to_sym].nil?
    puts "What's the rating? (Type a number 0 to 4.)"
    rating = gets.chomp
    movies[title.to_sym] = rating.to_i
    puts "#{title} has been added with a rating of #{rating}."
  else
    puts "That movie already exists! Its rating is #{movies[title.to_sym]}."
  end
when 'update'
  puts "What movie do you want to update?"
  title = gets.chomp
  if movies[title.to_sym].nil?
    puts "Movie not found!"
  else
    puts "What's the new rating? (Type a number 0 to 4.)"
    rating = gets.chomp
    movies[title.to_sym] = rating.to_i
    puts "#{title} has been updated with new rating of #{rating}."
  end
when 'display'
  movies.each do |movie, rating|
    puts "#{movie}: #{rating}"
  end
when 'delete'
  puts "What movie do you want to delete?"
  title = gets.chomp
  if movies[title.to_sym].nil?
    puts "Movie not found!"
  else
    movies.delete(title.to_sym)
    puts "#{title} has been removed."
  end
else
  puts "Sorry, I didn't understand you."
end
```

**LOOP STATEMENT**
```
<variable1>.each do |<variable2>|
    (use variable2)
    ...
end
```

**CASE WHEN STATEMENT**
```
case <variable>
    when <condition> then ...
    when <condition>
        ...
    else
        ...
end
```

**IF STATEMENT**
```
if <condition>
    ...
else
    ...
end

-or-

... if <condition>

-or-

... unless <condition>
```

** ternary expression**
<boolean> ? <if true> : <if false>

**conditional assignment** only if not already assigned
<variable> ||= <value>

**concatenate operator**
[1,2,3,4] << 5

**string interpolation**
#{<variable>}

**DEFINE METHOD**
```
def <method_name> (arg,...)
        ...
end
```
**LAMBDAS**
lambda { |<param>| ... }

**CLASSES**
```{P}
class Language
  def initialize(name, creator)
    @name = name
    @creator = creator
  end
	
  def description
    puts "I'm #{@name} and I was created by #{@creator}!"
  end
end

ruby = Language.new("Ruby", "Yukihiro Matsumoto")
python = Language.new("Python", "Guido van Rossum")
javascript = Language.new("JavaScript", "Brendan Eich")

ruby.description
python.description
javascript.description
```

**VARIABLE SCOPE**
```
class Computer
  $manufacturer = "Mango Computer, Inc."
  @@files = {hello: "Hello, world!"}
  
  def initialize(username, password)
    @username = username
    @password = password
  end
  
  def current_user
    @username
  end
  
  def self.display_files
    @@files
  end
end

# Make a new Computer instance:
hal = Computer.new("Dave", 12345)

puts "Current user: #{hal.current_user}"
# @username belongs to the hal instance.

puts "Manufacturer: #{$manufacturer}"
# $manufacturer is global! We can get it directly.

puts "Files: #{Computer.display_files}"
# @@files belongs to the Computer class.
```

@<instance variable>
@@<class variable>
$<global variable>

**CLASS**
```
class Computer
    @@users = Hash.new
    def initialize(username, password)
        @username = username
        @password = password
        @files = []
        
        @@users[username] = password
    end
    
    def create(filename)
        @time = Time.now
        @files[filename] = time
        puts "created!"
    end
    
    def Computer.get_users
        @@users
    end
end

my_computer = Computer.new("Peter", "P")
```

```
attr_reader :<name>
attr_writer :<name>
attr_accessor :<name>
```

```
:: - scope resultion operator

require <module name>
```

```
module Action
  def jump
    @distance = rand(4) + 2
    puts "I jumped forward #{@distance} feet!"
  end
end

class Rabbit
  include Action
  attr_reader :name
  def initialize(name)
    @name = name
  end
end

class Cricket
  include Action
  attr_reader :name
  def initialize(name)
    @name = name
  end
end

peter = Rabbit.new("Peter")
jiminy = Cricket.new("Jiminy")

peter.jump
jiminy.jump
```


# Ruby On Rails

