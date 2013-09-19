#String Manipulation
2 ways to manipulate strings, instance methods and regular expressions

## Instance Methods
- Slicing
  - The splice operator, used just like the array operator: `"ABCDEFGHI"[0..2] -> 'ABC'`
  - The `slice` method: `"ABCDEFGHI".slice(0..2) -> 'ABC'`
- String case: `String#downcase`, `String#upcase`, `String#swapcase`, `String#capitalize`, `String#capitalize!`
- Use `String#squeeze` to remove sets of the same character and replace them with a single intance of the character
- Most methods also offer an 'in place' version with the same name postfixed with '!'
- `String#insert` allows you to insert a string at a given index
  - The string is modified in place, but the method breaks the convention of ending with a '!'
- Remove last letter using `String#chop` or `String#chomp`
- Trim whitespace using `String#lstrip`, `String#rstrip`, or `String#strip`
- Split with delimiter using `String#split(delim)`
- `String#to_i` to convert to integer and `String#to_f` to convert string to float

## Regular Expressions
- Using the `=~` operator will return the index of the first match
- Using `String.match(regexp)` returns a `MatchData` of the string, which allows a number of options for accessing matches
- Using `String.scan(regexp)` will return an array of matches without having to access the `MatchData` middle man
- String substitution using `String#sub(regexp, newstring)` or (greedy) `String#gsub(regexp, newstring)`

# Date/Time
- 3 classes: `Date`, `Time`, and `DateTime`
- Can parse a string to a date with `Date#parse(str)`
- `Time#new` (alias `#now`) will create a time object with the current time
- Can output a `Time` object in any desired format using `Time#strftime(formatstr)`
- `DateTime` extends `Date` and adds functionality from `Time`
- `DateTime` is far less efficient then just using `Date` or `Time`

# Hashing and Cryptography

## Hashing
- Ruby provides MD5 and SHA-1 built-in
- Use `Digest::(digest of choice).digest(string)` for hashed string
- Use `Digest::(digest of choice).hexdigest(string)` to get a more friendly base64 representation of teh hashed string

## Cryptography
- Not built-in. Use the Crypt gem
- Create instance of desired crypt method with key, then just `#encrypt_block` and `#decrypt_block`

# Unit Testing
- `Test::Unit` is in the standard library
- Extend test case classes from `Test::Unit::TestCase`
- Use the various provided assesrt_* methods in test case classes to create tests
