socket.io에서 사용하는 이벤트 

1) connection

2) disconnect



socket.io에서 사용하는 메소드

1) on

2) emit



[connection 이벤트]

```javascript
io.on('connection', function(socket){
   //소켓이 연결되었을 때 수행해야할 일을 적을 수 있습니다
});
```

클라이언트와 소켓 연결 시 'socket'이 생기고, 클라이언트와 통신할 때 생성된 socket을 사용한다.



[socket.io에서 사용할 수 있는 메소드]

```javascript
socket.emit('message', "this is a test"); //sending to sender-client only
socket.broadcast.emit('message', "this is a test"); //sending to all clients except sender
socket.broadcast.to('game').emit('message', 'nice game'); //sending to all clients in 'game' room(channel) except sender
socket.to('game').emit('message', 'enjoy the game'); //sending to sender client, only if they are in 'game' room(channel)
socket.broadcast.to(socketid).emit('message', 'for your eyes only'); //sending to individual socketid
io.emit('message', "this is a test"); //sending to all clients, include sender
io.in('game').emit('message', 'cool game'); //sending to all clients in 'game' room(channel), include sender
io.of('myNamespace').emit('message', 'gg'); //sending to all clients in namespace 'myNamespace', include sender
socket.emit(); //send to all connected clients
socket.broadcast.emit(); //send to all connected clients except the one that sent the message
socket.on(); //event listener, can be called on client to execute on server
io.sockets.socket(); //for emiting to specific clients
io.sockets.emit(); //send to all connected clients (same as socket.emit)
io.sockets.on() ; //initial connection from a client.
```

전달하고자하는 방식에 따라 다른 메소드를 선택하여 사용할 수 있다.

그 중 수업에 내가 많이 쓰는 것은

* io.emit()
  * io.emit()과 socket.broadcast.emi()의 차이는 sender에게 메시지를 포함하느냐 마느냐 
  * 여러 개의 웹 페이지를 띄워놓고 하나에서 새로고침을 할 때 메시지가 어떻게 전달되는지 확인하면 알 수 있음
* io.on()
* socket.emit()
* socket.on()



connection 이벤트와 setInterval()

connection 이벤트 안에 

```javascript
io.on('connection', function(socket){

});
setInterval();
```

