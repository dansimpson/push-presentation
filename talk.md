!SLIDE

# Just Push It
Dan Simpson

!SLIDE

# What is "push"?

!SLIDE

# The Usual Suspects
* Comet (XHR Long Polling)
* EventSource
* WebSocket

!SLIDE

# Comet

### Pros
* Battle Tested
* It's HTTP
* Browser Support (It's AJAX)

### Cons
* HTTP Overhead on Reconnect
* Cross Origin Issues
* Wasteful Timeouts

!SLIDE

@@@ js
    function comet(...) {
      $.ajax({
        ...
        callback: function(...) {
          // invoke actual callback and
          // immediately request data again
          comet(...);
        }
        ...
      });
    }
@@@


!SLIDE

# EventSource

### Pros
* Augments HTTP
* Simple Protocol
* Simple API

### Cons
* Browser Support. Fuck IE. (It's getting better)
* Server Support

!SLIDE code

@@@ js
    var source = new EventSource( "/eventsource" );
    
    source.onmessage = function (e) {
    	alert( "no event " + e.data);
    }
    
    source.addEventListener("evt", function(e) {
    	alert("evt " + e.data);
    }, false); 
@@@

!SLIDE

# WebSocket

### Pros
* Augments HTTP
* Full Duplex
* Robust Protocol

### Cons
* Browser Support
* Complex Protocol
* Moving Target

!SLIDE code

@@@ js
    var ws = new WebSocket("ws://server.com/ws");
    
    ws.onmessage = function (e) {
    	alert(e.data);
    }
    
    ws.onopen = function(e) {};
    ws.onclose = function(e) {};
    
    ws.send(data); 
@@@

!SLIDE

#Notable Hybrids
* Socket.IO
* Shove (Shameless Plug)

!SLIDE

#Socket.IO
### Pros
* Multi-Transport
* Nice Abstraction Layer
* Community

### Cons
* Expects Special Server Side Code
* Requires Socket.IO Server

!SLIDE code

@@@ js
    var socket = io.connect("http://host/path");
    
    socket.on("news", function (data) {
      console.log(data);
      socket.emit("my other event", { my: "data" });
    });
@@@

!SLIDE

#Shove
### Pros
* Multi-Transport
* Hosted Service
* Failover + Redundancy + Scale
* Multi-App, Multi-Channel
* Support

### Cons
* It's Not Free

!SLIDE

@@@ js
    Shove.connect("myapp");
    
    Shove.channel("mychannel").on("message", function(e) {
      chatroom.append(e.data, e.user);
    });
    
    Shove.channel("mychannel").send("message", "Hi!");
@@@


!SLIDE

# Questions?
Dan Simpson - dan@shove.io - github.com/dansimpson


