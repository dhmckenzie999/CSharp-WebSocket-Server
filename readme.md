<h1>C# WebSocket Server</h1>

<h3>Introduction</h3>
<p>C# WebSocket Server is a easy and user-friendly Listen server for WebSocket clients written in Microsoft’s C# language. 
The code itself is located in 3 class files - Server.cs, Client.cs and Helpers.cs. 
A listen server is easily created by simply creating a new Server object. After the object is created, 
you will have to bind the events that the server object has where you choose what to do with the data.</p>

<h3>Listen server example</h3>
<p>Here's an example of a listen server</p>

```c#
// Console application entry point
static void Main(string[] args) 
{
    // Create a new websocket server
    Server server = new Server(new IPEndPoint(IPAdress.Parse(“127.0.0.1”), 80));

    // Bind the event for when a client connected with lambda
    server.OnClientConnected += (object sender, OnClientConnectedHandler e) =>
    {
        string clientGuid = e.GetClient().GetGuid();
        Console.WriteLine(“Client with guid {0} connected!”, clientGuid);
    };

    // Bind the event for when a message is received with a callback method
    server.OnMessageReceived += MessageReceivedCallback;

}

// Callback method for when a message was received
static void MessageReceivedCallback(object sender, OnMessageReceivedHandler e)
{
    string message = e.GetMessage();
    string guid = e.GetClient().GetGuid();
    Console.WriteLine(“Message received: {0} - Sender Guid: {1}”, message, guid);
}
```

<a>Copyright © 2017 - MazyModz. Created by Dennis Andersson. All rights reserved.</a>