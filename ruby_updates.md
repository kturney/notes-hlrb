# [Do you know what’s new in Ruby 1.9?](http://rubylearning.com/blog/2010/10/26/do-you-know-whats-new-in-ruby-1-9/)
- Rubygems and Rake are now officially part of Ruby
- Change the root in the class hierarchy to be `BasicObject`
- Added `Object#tap` to allow for more method call chaining
  - `#tap` takes an object and then yields that same object
  - "taps into" a method chain, potentially for extra debugging
  - "do something else too" with the object in the chain
  - [docs](http://ruby-doc.org/core-2.0.0/Object.html#method-i-tap)
- Symbols are now interpreted as string with regard to regular expressions
- Added homonym class for arrays: `a = Array('apple', 'banana')`
- Hashes
  - now stable: elements keep insertion order
  - New declaration if the keys are symbols: `data = {jan: 201234, feb: 234234, mar: 234345}`
  - Can easily access keys in a string: `puts "First two months of this year was: %{jan} and %{feb}" % data`
  - `Hash#select`, which aims to act like a filter, now returns a hash instead of an array
  - `#to_s` now returns an internal representation of the hash
- Block parameters were fixed to be local and not collide with external references within the same name
- Fibers
  - New construct for parallelism
  - Lightweight processes: memory footprint is only 4kB
  - "think of them like `Procs` that maintain status over calls

# [Ruby 1.9](http://slideshow.rubyforge.org/ruby19.html)
- Methods can be injected on an `Enumerable` by symbol name
- New lambda shorthand: `p = lambda{|a,b,c| a+b+c}` can become `p = -> a,b,c {a+b+c}`

# [Ruby 2.0.0 Is Released](https://www.ruby-lang.org/en/news/2013/02/24/ruby-2-0-0-p0-is-released/#label-8)
- Lang core
  - Keyword arguments: name method args with symbols
  - Added `Module#prepend`
  - UTF-8 default encoding
- Built-in libraries
  - Added `Enumerable#lazy` and `Enumerator::Lazy` for (possibly infinite) lazy streams
  - Added `#to_h` as new convention for conversion to `Hash`
  - Asynchronous exception handling

# [Ruby 2.0.0 by Example](http://blog.marc-andre.ca/2013/02/23/ruby-2-by-example/)

## Language Changes
- New keyword args makes method definition pattern this:
  ```ruby
  def name({required_arguments, ...}
           {optional_arguments, ...}
           {*rest || additional_required_arguments...} # Did you know?
           {keyword_arguments: "with_defaults"...}
           {**rest_of_keyword_arguments}
           {&block_capture})
  ```
- Easier symbol list creation: `KEYS = [:foo, :bar, :baz]` to become `KEYS = %i[foo bar baz]`
- Ruby will avoid issuing warnings for unused variables starting with an `_`

## Core classes changes
