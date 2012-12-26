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

Instead of storing the content of a document, Substance stores all user operations (e.g. insert section, update image) since the creation of the document. By doing so, we can access the full evoluationary history of a document and do time travels. Not only document content is versioned, also annotations and comments that stick on the content.