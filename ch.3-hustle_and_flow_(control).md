# Conditionals
## Ifs
- `if` is the initiator of a conditional block that needs to be ended with `end`
- `else` for else and `elsif` for else if

|| *Conditional Operators in Ruby* |
| --- | --- |
| `a == b` | Is true if the value of a to the value of b |
| `a === b` | Is true if the value of a to the value of b and they are the same type |
| `a != b` <br/> `a <> b` | Is true if a is not equal to b |
| `a !== b` | Is true if a is not equal to b or they are not the same type |
| `a < b` | Is true if a is less than b |
| `a > b` | Is true if a is greater than b |
| `a <= b` | Is true if a is less than or equal to b |
| `a >= b` | Is true if a is greater than or equal to b |

Ruby supports both C-style and strings for logical operators
- `&&` and `and`
- `||` and `or`
- `!` and `not`
Ruby supports the ternary operator: `(condition) ? (true result) : (false result)`

## Unless
Operates as a "reverse" if
- the main branch only executes if the provided condition is false
- Can prevent writing a bunch of negative ifs

## Statement Modifiers
- Syntactic sugar that allows tagging an `if` on the end of a statement for conditional execution
- Modifiers can also be placed at the end of blocks

  ```ruby
  thelma_louise = 13
  puts "She's less than 15 alright!" if thelma_louise < 15
  puts "She ain't more than 12, though!" if thelma_louise < 12
  
  begin
    puts "It's so true!"
  end if (true == true)
  ```

## The `case` Statement
- Case blocks are started with the `case` keyword
- Conditions are specified with the `when` keyword
- Each case is checked in order from the top down
- `when` should be followed by `:` or `then` (optional if the statement starts on the next line)
- `else` is used for the like `default` in Java switch statements
- There is no fall through in Ruby case statements
- There are 2 forms of case statements in Ruby
  - Standard: set a target variable on the case and each when is a possible target value
  - Flexible: set no target and each when has conditional statement(s)

    ```ruby
    the_tao = 1234
    case the_tao
      when 666: puts "That's such a lie!"
      when 1337
        puts "Liarrrr!"
      when 32767 then
        puts "Whatevurrrr!"
      else
        puts "You are harmonized with the Tao."
    end

    enlightenment = 42
    case
      when enlightenment > 60:
        puts "You are too hasty, grasshopper."
      when enlightenment < 40 or enlightenment == nil:
        puts "You are like the sloth, my friend. Diligence is key!"
      when enlightenment == 42:
        puts "Hello, Enlightened One."
      else
        puts "Yeah, not quite, pal. Maybe next time."
     end
    ```
# Loops
## Conditional Loops
- Execute based on a provided conditional statement
- A `while` loop executes while a conditional is true
- An `until` loop executes while a conditional is false
- Ruby does not have C-style `for` loops
## Iterating Loops and Blocks
- Ruby `for` loop: `for element in collection: (logic on element) end`
- `each` iterator: `collection.each do |element| (logic on element) end`
- Alternative each: `collection.each {|element| (logic on element)}`
## Statement Modifiers
- `while` and `until` may be used as modifiers on statements and blocks
- When used on blocks, the block will be executed at least once (like do while loops)
## Controlling Loops
- `next` can be used to skip the current iteration
- `break` can be used to exit the loop
- `next` and `break` can have conditional modifiers attached to them

# Exceptions
All exceptions derive from the base class `Exception` (go figure)
## Handle Exceptions
- Handle exceptions using a `rescue` block
- To create a `rescue` block, place the `rescue` keyword at the start of a line followed by the exception class to be handled
- If multiple `rescue` blocks are specified, Ruby follows the first one encountered able to handle the raised exception's type
- A variable can be specified to hold exception details: `rescue NoMethodError => e: (logic)`
- `rescue` blocks can be tagged with an `else` to be executed if no exception is encountered
- `ensure` blocks can be added to make sure something is always executed, like Java's `finally`
## Rescue Statement Modifier
- `rescue` can be used as a statement modifier, however the type of the exception can not be specified
- Can be used to return a default value if calling a method that may throw an exception
## Retry
- Using `rescue` and `retry` you can make an attempt to fix any errors that may cause exceptions and retry the block
- Take care that if the errors cannot be fixed that infinite retires do not occur
## Raising Exceptions

```ruby
# Raise a RuntimeError w/ message
raise "Error message"

# Re-raise the current exception or raise new RuntimeError w/ no message
raise

# Raise a typed error w/ message and a stack trace object (which is usually just caller, a reference to Kernel.caller method)
raise NoMethodError, "That method ain\'t here!", caller
```
## My Own Exceptions
To create a new exception, simply derive from any of the exception classes
## Throw and Catch
- Create a catch block using `catch :identifier do ... end`
- If the identifier is thrown (`throw :identifier`) than the block is exited without executing anymore code
Useful if you need to simply exit the code block if an error occurs or if your code is buried in deeply nested loops and you want to break out of them quickly and easily
