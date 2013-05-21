---
layout: post
title: I love javascript
excerpt: Js code highlight test
categories: blog
---

# Simple chat in node.js
pygments testing !

{% highlight javascript linenos %}
var
  port = 8124,
  net = require('net'),
  clients=[],
  listener=function (socket) {
    var nickname = '';
    console.log('New client connected.');
    clients.push(socket);
    socket.on('end', function() {
      clients.splice(clients.indexOf(socket),1);
      console.log('Client disconnected.');
    });
    socket.on('data', function(data) {
      if(!nickname){
        nickname = data.toString().replace(/[\n\r]+/,'');
        socket.write('Hello '+nickname+', you can now chat with others bitch.\r\n');
        broadcast('Another bitch "'+nickname+'" joined.\r\n',socket);
        return;
      }
      broadcast(nickname+': '+data);
    });
    socket.write('Welcome 2 Ali.MD Chat Server ;)\r\nEnter your name : ');
  },
  broadcast= function(msg,exept){
    clients.forEach(function (client) {
      client==exept || client.write(msg);
    });
  },
  init= function(){
    net.createServer(listener).listen(port, function() {
      console.log('Server launched.');
    });
  };

init();
{% endhighlight %}
