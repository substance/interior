---
layout: feature
title: Distributed Architecture
abstract: Substance is a distributed system for creating and sharing documents among peers.
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/features/0100-01-03-distributed.md
author_twitter: _mql
author: Michael Aufreiter
status: Work in progress
categories:
- features
published: true
---

Substance is being designed as a distributed system. Every peer can act as a server or client. Nodes can either run locally on your computer or somwhere on the web. It's the same piece of software, except that public nodes may use more sophisticated backends as they most likely need to scale.

With Substance our goal is the provision of a modern technology stack, enabling collaborative document composition in realtime between multiple peers. The system is split into separate modules, which talk to each other using message passing. So our System is all about exchanging and manipulating digital documents over the network. To ensure all parties can communicate fluently, we defined a common vocabulary that is spoken by all parties, the [Substance Document Protocol](/modules/document.html).


![Substance Architecture](http://f.cl.ly/items/1U1R140i1s0j011d131V/substance-architecture.png)


# Substance Peer

A Peer depicts a regular Substance node. It can be run on a local machine, or deployed to the web (public document hub). Every peer owns a number of documents. Each peer consists of a client (document composer), a server and a library for storing documents.


## Substance Client

A Substance Client is a program that runs in a web-browser and provides a user-interface for manipulating digital documents. There's no serverside code involved, but your client needs to be able to connect to a server backend that talks the Substance Document Protocol. The [Substance Composer](/modules/composer.html) is such a client. Our current plan is to only support WebSockets and set aside support for http for the first phase. This might sound like a crazy decision, but it allows us to focus on building a reliable realtime system depending on message passing in both directions. We'll add a compatibility layer once the system is working reliably.


## Substance Server

In order to access and collaboratively edit documents clients must connect to a trusted server that processes their requests. A server accepts Websocket connections from clients and talk to the library for accessing and manipulating document content. You can talk to the server on your local substance instance or connect to a remote server. They'll all gladly serve you.

A conversation between a client and a server could look like this.

    John:     Hey, John is here.
    Server:   Welcome John. What can I do for you?
    John:     I'd like to create a new document please.
    Server:   Sure. Here it is.
    John:     Thanks. Now please insert a section named "Introduction" for me.
    Server:   Done.
    John:     Thanks a lot.
    Server:   John, Paul has just edited your document. He added a text element saying "Hello World".
    John:     Oh thanks, good to know


## Substance Library

The Library is a home for digital Substance Documents. The Substance Library is different from traditional libraries, in that there are no books stored but digital documents that are always up-to-date. Everyone with permission can read and write documents at any time. Open 24/7.

Only librariens have access to it. They can read / and update documents at any time. For every document accessed (by one or more clients) a new librarian needs to start working. The Library knows of all currently employed librarians, and thus about documents that are processed at time.


# Document Sessions

A session is yielded every time a document gets edited. Every Substance peeer is capable of hosting sessions. Sessions are usually hosted by the node that owns the master copy of the document if available. If that node is not online and there are replicas available (e.g. on a hosted node) the session is hosted there. Arbitrary Substance users can join a session.


# Master copies and replicas

A document is created on a particular Substance node. This is refered to as the **master copy**. This document has the highest score of authenticity. Replicas on other nodes are kept in sync as good as possible, but the master copy is the original version.


# Example

Let's walk through a simple example:

1. `John` connects to a Substance Server using WebSockets
1. After a handshake, the client is securely connected to his server.
1. Now `John` creates a new document by sending the message `document:create`.
1. The server talks to the library and a new document gets filed. Once this is done the server starts a new document editing session, having one participator at this time. The client gets sent a message confirming the document creation and containing the brand new blank document.
1. Well, now `John` has a fresh document.
1. Some time later `Paul` joins the party. He also connects to that server.
1. `Paul` opens the document just created by `John`. The server is aware that there's an active document session so John just joins that session and as a response gets the current state of the document.
1. `Paul` just adds an image at the bottom of the document then, which triggers an operation `node:insert` broadcasted to all active clients, in our case `John`. Under the hood the document session is aware of clients participating in a session and sends distributes messages accordingly. For every session a document instance is kept in memory, which gets transformed as operations come in.
