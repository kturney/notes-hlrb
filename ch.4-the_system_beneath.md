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
- `Thread#pass` to pause a thread and let another thread run
- `Thread#stop` to stop a thread until it is restarted
- `Thread#run` to restart a stopped thread
- To exit a thread completely, `Thread#exit` from in a thread or `Thread.kill(threadToKill)` from outside
### Getting information from threads
- Call `#value` on a thread to block and get the value it returns (like a Java Future)
## Processes
- `system` spawns an external application in a subprocess
- `IO#popen` will spawn an application and then give you a stream which you can read from and write to just like any other stream
- Can use `exec` if you need to execute a process and then wait for it to finish using `Process.wait` before continuing
# Environment
- Access environment variables using `ENV['varname']` and `ENV['varname'] = newvalue`
- All changes stay local to the Ruby application
- Access command line args using the global array `ARGV`
- Access config vars by including the `Config` module and using global array `CONFIG`
- There are a bunch of Windows specific libraries. Stupid Windows
