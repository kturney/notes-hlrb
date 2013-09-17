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
- 
