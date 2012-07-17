---
layout: feature
title: Content is data
abstract: Substance considers content as data, so you can query documents like a database.
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/features/0100-01-01-content-is-data.md
author_twitter: _mql
author: Michael Aufreiter
categories:
- features
published: true
---

Substance is a fully web-based document authoring and publishing platform. With Substance, Writers, Scientists, Journalists and everyone who's interested in publishing can use an open platform for writing and sharing articles in a collaborative way. 

# Structured composition

Instead of sequential text-editing, documents are composed of Content Nodes. While existing solutions (like Google Docs) bring traditional word-processing to the web, Substance focusses on content, by leaving the layout part to the system, not the user. Because of the absence of formatting utilities, it suggests structured content-oriented writing. 


![](http://substance-assets.s3.amazonaws.com/29/0cff0d34004080f40be83968f81af2/editing.png)

Substance uses a uniform data format that allows Cross Media Publishing to arbitrary targets such as Print (PDF, LaTex), E-Book (ePub, Kindle) or integration with a website. Thus it's also fundamentally different from conventional Wiki Systems, that are based on Hypertext. Substance is Open Source, free to use and doesn't introduce vendor lock-ins.

# Eventually consistent

Most things in life are not perfect. That's also true for every document ever written or to be written. Substance supports a workflow that assumes documents will be consistent eventually. We claim that it's way easier to reach consistency if you publish early and provide an easy way for collaboration. Substance helps with implementing a peer-review process, with every reader being a peer.


# Content is data

Substance considers content as data, which allows for interesting things like semantic data analysis and novel visualizations. Imagine you can query documents like a database. With Substance you can.


![](/images/illustrations/content-is-data.png)


# Content Types

New content node types should be support through a plugin system. Applications using the editor require different content types. Examples for such plugins would be:

- Chemical Structures
- Formulas
- Maps
- Tables
- Charts


![](http://substance-assets.s3.amazonaws.com/62/583a4ca6c6a0bef0868fc8eb8402a7/mom.png)

# Imitating paper

Traditional digital formats have always tried to imitate paper. Think of footnotes and references that are listed at the bottom of the document. We're going to break with this transition and introduce only general concepts that work with a digital version too.

