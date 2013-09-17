# Filesystem Interaction
- Done through the `File` class
- File size is returned in bytes
- `nil` is returned when file size is zero(0)
## Reading from a file
To prevent needing to call close, a block can be passed to `File#open` or `IO#foreach` can be used

```ruby
# All of the following are equivalent
myfile = File.open("textfile.txt", "r")
myfile.each_line {|line| puts line}
myfile.close

File.open("textfile.txt") do |myfile|
  myfile.each_line {|line| puts line}
end

IO.foreach("textfile.txt") {|line| puts line}
```
## Writing to a file
Any data can be written to a file as long as it has a `to_s` method

```ruby
# The following are equivalent
count = 10

# using the write method
File.open("textfile.txt", "w") do |myfile|
  myfile.write("Howdy!\n")
  myfile.write("There are ")
  myfile.write(count)
  myfile.write(" pandas!")
end

# using the << operator
File.open("textfile.txt", "w") do |myfile|
  myfile << "Howdy!\n" << "There are " << count << " pandas!"
end
```
# Threads, Forks, and Processes
## Threads
- To create a thread, just pass a code block to the `Thread` class's constructor

  ```ruby
  mythread = Thread.new() do
    # some awesome thread logic
  end
  ```
- Threads start right after they are created
- Call `mythread.join()` to have your program wait for a thread to complete before exiting. Otherwise, all threads are exited when the main thread exits
### Controlling threads
