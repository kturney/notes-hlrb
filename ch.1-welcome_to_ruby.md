In Ruby, EVERYTHING that will be manipulated is an object

Types
- All types in Ruby originate from the `Object` class
- Strings
  - sequences of bytes that represent a sequence of characters
  - String literals may be created using either single quotes or double quotes
  - Single quotes are not interpolated and may only contain escapes for the single quote and backslash
  - Single quoted string literals are slightly more performant
  - Double quoted string literals offer far more escape sequences for interpolation
  - Ruby code can be embedded in double quoted strings using `"some text #{ruby code} some more text"`
  - Multiplying a string creates multiple copies of the string
  - Alternatively, single quote strings can be created with `%q{text}` and double quote strings with `%Q{text}`
  - Ruby also supports heredoc string creation by specifying a delimiter after a set of '<<' characters to start the string and putting the delimiter on a line of its own to end it
  - All objects also have a `to_s` method to get a string representation of the object
- Numbers
  - `Fixnum` for integers between -2^30 and (20^30)-1 and `Bignum` for anything outside of `Fixnum`
  - Ruby ignores underscores(_) in numbers so they may be used in place of commas: `1_299_000`
  - For floats, each side of the decimal must contain a number
  - All math operators are really just functions
- Collections
  - Range
    - Hold a sequential collection of values, such as all numbers between 1 and 9
    - Created by placing a series of dots between the lower and upper limit of the range: `letters = A..Z` or `digits = 1...10`
    - 2 dots are for an inclusive range including beginning and end value
    - 3 dots are for a range that excludes the last value
    - Think about it as the extra dot pushing the last element out of the range
    - Ranges are considered equal (using `==` or `.eql?`) if their beginning and end values are the same
    - Check whether a value is in the range using `===` or `.include?` (aliased by `.member?`)
  - Array
    - An integer indexed and ordered collection of elements
    - The elements in a Ruby array do not have to be the same type
    - Many ways to create an array

    ```ruby
    its_so_empty = []
    oh_so_empty = Array.new
    hello = ['ni hao', 'bonjour', 'hi', 'howdy']
    random_types = [13, 'napkin', (1336 + 1).to_s]
    
    # from strings
    my_haiku = %w( my dog digs it here\n )
    → ["my", "dog", "digs", "it", "here" ]
    my_haiku = %w( he is nice to me & cats\n )
    → ["he", "is", "nice", "to", "me", "&", "cats"]
    my_haiku = %W( but he ate #{(2*3)/6} once )
    → ["but", "he", "ate", "1", "once"]
    my_haiku = %w( but he ate #{(2*3)/6} once )
    → ["but", "he", "ate", "#{(2*3)/6}", "once"]
    
    # to_a method
    my_range = 1..10
    → 1..10
    my_dazzling_array = my_range.to_a
    → [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    ```
    - Can append new elements by assigning a value to a non-existent index, using the `.push` method, or `<<` operator
    - Array elements can be accessed using either and integer or a range
  - The Hash (AKA associative array or dictionary)
    - Collections of values of any type indexed by other values of (almost) any type rather than solely numbers like arrays
    - Keys have 2 requirements: must implement `.eql?` and must have a constant hash code
    - Hashes are created using `{}` or `{ 'key1' => 'val1', 'key2' => 'val2' }`
    - Can also create a hash with a default value for non-existant keys using `Hash.new('default val')`
    - When an element is deleted (using `(hash name).delete['key']`) the key's value is returned
    - Calling `.clear` returns the newly empty hash

Variables and Assignment
- Variables can be set in parallel using `a, b = 1, 2` or `a, b = [1, 2, 3]`
- Any array can be assigned to a list of variables. Ruby ignores any extra elements in the array past the number of variables
- Ruby has `+=` and `-=` but not `++` or `--`
- Can prevent assigning to an object by calling the `.freeze` method
