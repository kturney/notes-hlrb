Blocks
- Pieces of code segmented away from their context by an initiator and the `end` keyword
- Can be passed a variable number of requirements (arguments)

Methods
- Ruby uses message passing instead of actual method calls (Schemeish)
- If a method is not found, a `NoMethodError` is thrown
- Defined by `def` followed by the method name and parameters, ended with `end`

  ```ruby
  def my_new_method(name)
      puts "Hey, #{name}, this is my new method..."
  end
  ```
- Naming (By convention)
  - All lowercase
  - Seperated by underscores
  - If querying an attribute, end in '?'
  - If modifies receiver in place, end in '!'
- Args
  - Can set defaults

  ```ruby
  def new_method(a="This", b="is", c="fun")
      puts "#{a} #{b} #{c}."
  end
  ```
  - Params must be in the same order
  - Params cannot be skipped
  - Parameter lists can be variable length by placing an '*' before the identifier of the last element it will be a variable length list

  ```ruby
  def print_relations(relation, *names)
      puts "My #{relation} include: #{names.join(', ')}."
  end

  print_relations("cousins", "Morgan", "Miles", "Lindsey")
  ```
- Calling
  - If no parameters, no parentheses are needed
  - Methods throw 'ArguementError' if they don't get the correct number of arguements
- Return value
  - A value is always returned
  - If no value explicitly specified, returns `nil` or the last value used inside the method (if that exists)

Blocks and Proc Objects
- Blocks are much like a method without a name tagged on it
- Blocks can also be defined with `{`/`}` instead of `do`/`end`
- Proc
  - `Proc` objects are like blocks that are pushed into variables
  - Proc is especially useful when you want to create a block of code and pass it around or generate new blocks from it
  - Another way to create a `Proc` object is to bind a block of code using the lambda method

  ```ruby
  myproc = lambda {|x| puts "Argument #{x}"}
  # same as
  proc = Proc.new {|x| puts "Argument #{x}"}
  ```
  - `Proc` objects created with `lambda` have stricter argument checking than those created with `Proc.new`
  - Objects created with `lambda` don't affect the flow of the application outside of the block when returning a value
  - `Proc` objects created with `Proc.new` will exit their enclosing method when returning
  
  ```ruby
  def procnew
      new_proc = Proc.new { return "I got here..." }
      new_proc.call
      return "...but not here."
  end

  def lambdaproc
      new_proc = lambda { return "You get here..." }
      new_proc.call
      return "And I got here!"
  end

  puts lambdaproc
    → And I got here!
  puts procnew
    → I got here...
  ```
- Using Blocks
  - Take a `Proc` as an argument, but this does not perform well
  - Implicit block usage: use `yield` to give control to the block
  - If `&` is is the first character of a block argument name, then the block is converted to a `Proc`

Types
- Ruby uses "duck typing": if it walks like a duck and talks like a duck then its a duck
- In Ruby, every class is an object which is an instance of the `Class` class which is derived from the `Object` class
- Ruby only supports single inheritance
- A class inherits all of its super's methods and variables
- Define a class using

  ```ruby
  class MyFirstClass < Object
  end
  ```

Methods and Variables
- Constructor logic for Ruby classes is contained in the `initialize` method
- `initialize` is invoked by calling `(class name).new` with any required arguments
- Define instance variables (state held within an object) are defined by prefixing the name with `@`
- Instance variables do not have to be declared in the class definition. Just use them
- Classes in Ruby are never closed. You can always add or redefine methods on a class

Attributes
- Basicly getters and setters for instance variables
- Get: define a method with the same name as the instance variable and return it
- Set: define a method with the same name as the instance variable appended with an '='

  ```ruby
  class Boogeyman
      def scare_factor
          @scare_factor
      end
      
      def scare_factor=(factor)
          @scare_factor = factor
      end
  end
  ```
- Can alternatively use `attr_reader` and `attr_writer` to have Ruby generate the attributes for you

  ```ruby
  class Boogeyman
      attr_reader :scare_factor
      attr_writer :scare_factor
  end
  ```

Access Control
- Methods and attributes are public by default
- Can make methods/attributes protected (accessible by instance and sub-classes) by placing the `protected` keyword on a line and putting protected methods/attributes after that line
- Private methods/attributes can be similarly defined by using the `private` keyword instead of protected

Class Scoped Objects
- Class constants can be defined by placing the constant name and value in the class definition
- To create class varaibles (same as Java static variables) place `@@` before the variable name
- Class methods are defined using `(class name).(method name)`
  - Strange note that class methods are not visible to instance scoped objects so the methods full call must be used

  ```ruby
  class Boogeyman
      MY_BOSS = 'Mr. Boogeyman'
      
      def Boogeyman.latest_monster
          puts "The latest monster is #{@@latest}"
          puts "He is in #{@@location}"
      end
      
      def initialize(name, location)
          @name = name;
          @location = location
          
          @@latest = @name
          @@location = @location
      end
  end
  ```
  
Modules
- Modules are used to create namespaces to prevent naming conflicts
- Modules are defined by

  ```ruby
  module ModuleName
  ...
  end
  ```
- Mixins
  - Modules also allow for mixins, code that is "mixed into" a class as if it is part of its original code
  - To use a mixin, define a module and then use the `include` keyword followed by the module's name
  - After inclusion, the class has access to all of the module's constants and methods
  - It is best to use a unique naming scheme for module constants to prevent naming conflicts when mixed into classes
  - Methods do not have to be unique because Ruby will use the instance defined method first

Files
- To include a file in Ruby use `load` or `require`
- `load` includes a source code file unconditionally
- `require` will only include a source code file once (so not duplication of variables and methods)
- Both keywords accept both relative and absolute paths
- `require` can also be used in conditionals, loops, or other constructs and use variables in its path
- Local variables in included files do not trickle into the context in which they are included. They are locked into the context in which they were written.
