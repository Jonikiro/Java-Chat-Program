# Chat-Client
A simple chat application which utilizes multithreading, sockets, and a GUI to allow multiple users to chat with each other over a single server.

**INTRODUCTION**

The following is a breakdown of the two primary modules and the functionality they provide. This code was part of an exercise in Head First Java (2nd Edition) meant to utilize multiple features of Java: 

- GUI development with Swing
- event handling
- inner classes
- serialization
- I/O
- networking sockets
- multithreading

The Chat Client program is broken up into two modules: SimpleChatClient.java and VerySimpleChatServer.java.

**CLIENT SIDE MODULE**

The SimpleChatClient module is responsible for establishing a connection with the server module over which the user will send and receive data. This data will be submitted and displayed through a GUI which will be updated in real time. To accomplish this, the module does three things: Build a GUI using Swing components, set up the networking functionality by initializing a socket and input stream Reader + Buffer, and implement the ActionListener and Runnable interfaces to handle outgoing and incoming data, respectively.

The GUI is made up of a Frame to hold all components, a TextArea contained within a ScrollPane to hold the messages sent to and received by the server, a TextField for users to enter new messages, and a Button to submit them. An ActionListener is attached to the Button, which we'll cover shortly.

A separate method is responsible for the networking. It creates a new Socket which points to the localhost (127.0.0.1) and a port that the server will be listening on (5000). The method then initializes an InputStreamReader which takes incoming data from the socket connection, followed by a BufferedReader which buffers that data so that it may be read more efficiently. It also initializes a PrintWriter responsible for sending data through the Socket's output sream.

While the networking method is responsible for establishing those connections, the implementations of ActionListener and Runnable are responsible for using them. The first uses the PrintWriter to get any text entered by the user in the TextField and print it to the output stream. The latter utilizes a new Thread set up beforehand to listen to any incoming requests from the server and append data from them to the TextArea for display in real time.

**SERVER SIDE MODULE**

The VerySimpleChatServer module is responsible for accepting connections from multiple chat clients and handling the data received from them simultaneously using multiple Threads to do so. To accomplish this, the module does four things: Establish a ServerSocket which listens for incoming requests on port 5000, initialize a new Thread to handle each incoming client Socket, add to an ArrayList which will hold PrintWriters initialized for each client Socket, and iterate through those PrintWriters so that each time data is received by the server, it will be printed back to every client via their own connection.

The ServerSocket is initialized to listen to incoming requests on port 5000. When that ServerSocket accepts an incoming request, it initializes a new Socket with the incoming client Socket and chains its OutputStream to a new PrintWriter. It adds that PrintWriter to an ArrayList, which we'll cover shortly.

A new Thread is initialized which will handle the InputStream from this client Socket by initializing an InputStreamReader/BufferedReader combination. Data processed through those Readers is then used by every PrintWriter to print said data back through every client's OutputStream to be displayed on their end.

**CONCLUSION**
While this is a small program designed to be run on a single computer, future updates to this program will focus on making the server more robust and possibly extending functionality to run over multiple computers. Thank you for your interest.
