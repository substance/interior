The Substance Architecture
============

Here's a working draft of the upcoming Substance architecture. Our goal is the provision of a modern technology stack, enabling collaborative document composition in realtime. The system is split into separate modules, which talk to each other using message passing. While performance is not a high priority at this early stage, the architecture is designed to allow scaling up to multiple nodes.

Our System is all about exchanging and manipulating digital documents over the network. Editors (Clients) talk to their agents. Agents talk to Librarians, which finally have access to the Substance Library. To ensure all parties can communicate fluently, we defined a vocabulary that is spoken by all parties, the Substance Document Protocol.

![Substance Architecture](http://f.cl.ly/items/1U1R140i1s0j011d131V/substance-architecture.png)


Document
------------

The Substance Document Model is an abstract model for representing arbitrary structured digital documents. Users can define their own document structure and manipulate it using commands. The Substance Document Model forms the heart of the system, it defines a generic protocol that is used by all sub-modules.


Master
------------

The Master is the public face to the outside. All the master does is picking an agent for you that is available for processing your requests. Probably this will be a smart version of [node-http-proxy](https://github.com/nodejitsu/node-http-proxy).


Agent
------------

As a user, you're talking to a trusted agent that processes your requests. An agent accepts socket.io connections from clients and talks to librarians that have access to the library.


A conversation between a client and an agent could look like this.

```
John:     Hey, John is here.
Agent X:  Welcome John. What can I do for you?
John:     I'd like to create a new document please.
X:        Sure. Here it is.
John:     Thanks. Now please insert a section named "Introduction" for me.
X:        Done. That's one dollar.  ... I'm just kidding.
John:     Very funny Agent X. But thanks.
X:        John, Paul has just edited your document. He added a text element saying "Hello World".
John:     Oh thanks
```

Library
------------

The Library is a home for digital Substance Documents. Only librariens have access to it. They can read / and update documents at any time. For every document accessed (by one or more clients) a new librarian needs to start working. The library knows of all currently employed librarians, and thus about documents that are processed at time.


Librarian
------------

While agents are serving customers (authors, readers) librarians do the important work behind the curtain. Librarians have full access to the Substance Library allowing them to read and update documents. Our library has just one rule, there can only be one librarian be responsible for a document at a time. If an Agent wants to access a particular document, he either gets the librarian dealing with that document already, or a new librarian that picks that document from the shelf.

In Computer Science terms, a librarian conforms to a worker. It allocates memory necessary for processing one document.

Here's a conversation between Agent X and his librarian that we've monitored some days ago.

```
Agent X:    Please give me the full contents of document A
Librarian:  Sure. Here you are.
Agent X:    My client wants to delete the last section of the dcoument. Can you do that for me?
Librarian:  Done. I've removed the last section, and notified Agent Y about it, so his client gets the update as well.
Agent X:    That's all for today. See you next time.
```


Client
------------

A client can be any . The Substance Composer is a compatible client, that allows documents to be transformed right in the browser. It talks to a Substance Agent, either using Websockets (for realtime composition) or AJAX.


Example
------------

Let's exemplify the architecture based on an example:

1. `John` connects to the Master using Socket.io
2. The Master, which serves as a load balancer picks a suitable agent node that serves the client. This time `Agent X` is chosen.
3. After a handshake, the client is securely connected to his agent.
4. Now the client creates a new document by sending the message `document:create`.
5. The Agent forwards this message to a librarian, which creates a new document instance, stores it in the library and confirms by sending a message all the way back to the client, containing the new document.
6. Well, now `John` has a fresh document.
7. `Paul` joins to the party. The Master assigns `Agent Y` this time.
8. `Paul` opens the document just created by `John`. In order to access it, `Agent Y` reaches out to the librarian, which can immediately serve it as there is an active session by John. In the case that there's no responsible librarian working on a particular document a new librarian gets hired. It just needs to pick the document from the shelf (the database) first. Not a big deal.
9. After all `Paul` has the latest version of the document. He just adds an image at the bottom of the document, which triggers an operation `node:insert` broadcasted to all active clients, in our case `John`. Under the hood this works like this:
     - Paul's Agent forwards the `node:insert` message to the Librarian. And this guys knows how to deal with it. 
     - The operation is getting applied on the current server state of the document. Once this has been done, the message gets broadcasted to all connected client sessions. Luckily the Librarian has kept track about all sessions belonging to a certain document, so he knows that the message needs to be sent over to Agent X, in order to reach `John`.
