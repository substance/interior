---
layout: feature
title: Distributed Architecture
abstract: One of the nicest features of any distributed system, Substance included, is that it's distributed. This means that instead of doing a "checkout" of the current state of a document, you have the full evolutionary history available on every peer.
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/features/0100-01-03-distributed.md
author_twitter: _mql
author: Michael Aufreiter
status: Work in progress
categories:
- features
published: true
---

![Substance Architecture](/images/illustrations/architecture.png)

The architecture basically consists of two parts.

# The Composer

The Substance Composer can be installed on your computer as a native application. It doesn't even need an internet connection to create documents. When it comes to collaborative editing and sharing your documents, you will need to connect your application to a [Substance Hub](/modules/hub) like [Substance.io](http://substance.io).


# The Hub

The Substance Hub is the server counterpart of the Substance Application (the client). Of course there's not just one global Substance Hub, you can setup a hub for your university or company.

The Hub has two main purposes:

- Make available published documents so people can read them in their web-browsers.
- Connects editors so they can collaboratively work on one document.

# Operational Transformation

Instead or in addition to storing the current state of the document, it advantageous to capture a sequence of operations that have been applied to the document. Instead of describing a document by its state (e.g. it has a section, followed by a paragraph) it can be described using a sequence of operations executed by the user (insert section, insert paragraph after section respectively). By doing so, the full evoluationary history of a document can be accessed and time travels are possible. Not only document content is versioned, also annotations and comments that stick on the content. Furthermore Operational Transformation forms the basis for collaborative editing features.