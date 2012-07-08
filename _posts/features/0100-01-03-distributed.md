---
layout: feature
title: Distributed Architecture
abstract: Substance is a distributed system, for creating and sharing documents among peers.
author_twitter: _mql
author: Michael Aufreiter
status: Work in progress
categories:
- features
---

Substance is a distributed system. Every node can act as a server or client.


# Substance Conductor

In order to coordinate the clients and let them communicate to each other peer to peer there needs to be a Conductor instance. A conductor maintains a list of all connected nodes, and also acts as a nameserver.
In short, in order to use the Substance infrastructure you need to register for a unique account and claim your username. However, account data is the only data hosted by Substance, all you documents belong to you. You can keept them private on your machine or publish them to multiple noes in the network.


# Substance Peer

A Peer depicts a regular Substance node. It can be run on a local machine, or be deployed to the web (public document hub). Every peer owns a number of documents.


# Master copies and replicas

A document is created on a particular Substance node. This is refered to as the **master copy**. This document has the highest score of authenticity. Replicas on other nodes are kept in sync as good as possible, but the master copy is the original version.


# Document sessions

A session is yielded every time a document gets edited. Every substance node is capable of hosting sessions. Sessions are usually hosted by the node that owns the master copy of the document if available. If that node is not online and there are replicas available (e.g. on a hosted node) the session is hosted there. Arbitrary Substance users can join a session.