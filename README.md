# Websocket tutorial

**The WebSocket object**

`var socket = new WebSocket("ws://echo.websocket.org");`

**The WebSocket event**

After creating the WebSocket object, we need to handle the events it exposes. There are four main events in the WebSocket API: Open, Message, Close and Error. You can handle them either by handling the onopen, onmessage, onclose and onerror functions respectively, or by using the addEventListener method. Both ways are equivalent, but the first one is much clearer.

**onopen**

The onopen event is raised right after the connection between the server and the client has been successfully established.

    socket.onopen = function(event) {
        var label = document.getElementById("status-label");
        label.innerHTML = "Connection establisjed!";
    }

**onmessage**

The onmessage event is the client’s ear to the server. Whenever the server sends some data, the onmessage event is fired. Messages might contain plain text, images or binary data. It’s up to you how that data will be interpreted and visualized.

    socket.onmessage = function (event) {
        if (typeof event.data === "string") {
            // The server has sent a string.
            var label = document.getElementById("status-label");
            label.innerHTML = event.data;
        }
    }

**onclose**

The onclose event marks the end of the conversation. Whenever this event is fired, no messages can be transferred between the server and the client unless the connection is reopened.

    socket.onclose = function(event) {
        console.log("Connection closed.");
        
        var code = event.code;
        var reason = event.reason;
        var wasClean = event.wasClean;
        var label = document.getElementById("status-label");
    
        if (wasClean) {
            label.innerHTML = "Connection closed normally.";
        }
        else {
            label.innerHTML = "Connection closed with message " + reason + "(Code: " + code + ")";
        }
    }

**onerror**

The onerror event is fired when something wrong (usually unexpected behavior or failure) occurs. Note that onerror is always followed by an onclose event!


socket.onclose = function(event) {
	console.log("Error occurred.");

	var label = document.getElementById("status-label");
	label.innerHTML = "Error: " + event;
}


**The WebSocket actions**

Events are raised when something happens. We make explicit calls to actions (or methods) when we want something to happen! The WebSocket protocol supports two main actions: send and close.

While a connection is open, you can exchanges messages with the server. The send() method allows you to transfer a variety of data to the web server. Here is how we can send a chat message (actually, the contents of the HTML text field) to everyone in the chat room

    var textView = document.getElementById("text-view");
    var buttonSend = document.getElementById("send-button");
    
    buttonSend.onclick = function() {
        // Check if the connection is open.
        if (socket.readyState === WebSocket.OPEN) {
            socket.send(textView.value);
        }
    }

**close()**

The close() method stands as a “goodbye” handshake. It terminates the connection and no data can be exchanged unless the connection opens again.


    var buttonStop = document.getElementById(“stop-button”);
    
    buttonStop.onclick = function() {
        // Close the connection, if open.
        if (socket.readyState === WebSocket.OPEN) {
            socket.close();
        }
    }
    
![notes](https://s-media-cache-ak0.pinimg.com/originals/1e/63/73/1e637353238afa7755d6e6e5d306733b.jpg)















































    