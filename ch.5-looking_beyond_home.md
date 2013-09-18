# Networking and the Web
- Networking is done through sockets, all of which are based on the `BasicSocket` class
- It is generally much easier to use the higher level abstractions built on `BasicSocket` rather than `BasicSocket` itself
## Server
- Created using `TCPServer#new` or alias `TCPServer#open` class in the `socket` module
- Generally best to start a new thread for every connection using `Thread.start(myserver.accept) {logic block}`
## Client
- Offered by the `TCPSocket` class in the `socket` library, which will give you a stream on which to operate
## HTTP Networking
- Use the `WEBrick` module to create an `HTTPServer`
- Ruby's HTTP client library is the `Net::HTTP` class
- Can use `URI#parse` to use normal URLs with `Net::HTTP`
- `Net::FTP` for FTP and `Net::SMTP` for SMTP (go figure)
- Basicly the Net library has everything you want
# Distributed Ruby
- Part of the DRb (Distributed Ruby) package
- All applications consist of a server and clients
- The server starts a TCP server which exposes objects, accepts connections and responds to actions requested over those connections
## Server Example
```ruby
require 'drb/drb'
require 'thread'

class SizeService
  def initialize(filename)
    @file = filename
  end
  
  def get_space
    return File.size(@file)
  end
end

# start a drb service with the specified URI and expose the indicated object
DRb.start_service("druby://:9876", SizeService.new('cats.log'))

# print the URI for reference and for your benefit when trying to connect
puts DRb.uri

# join the server thread to the main thread so the app doesn't exit
DRb.thread.join

# the server then idles until connected to
``
## Client Example

```ruby
require 'drb/drb'

# make sure the service is started
Drb.start_service

# bind to the remote object
remote_obj = DRbObject.new(nil, 'druby://domo:9876')

# use the remote object just like a local object
puts "Log file usage is #{remote_obj.get_space()} bytes."
```
# Databases
- Access many different database backends through the Ruby's DBI
- All apps can also use Rails' ORM, ActiveRecord
- Just have classes extend `ActiveRecord::Base`
