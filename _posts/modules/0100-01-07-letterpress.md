---
layout: module
title: Letterpress
abstract: Letterpress transforms Substance documents to different output formats, such as PDF, LaTeX, ePub.
author_twitter: _mql
author: Michael Aufreiter
links: # specify links for demo and source
  source: http://github.com/substance/surface
  demo: http://composer.substance.io
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/modules/0100-01-07-letterpress.md
version: 0.2.0
progress: 2
contributors:
- name: Tim Baumann
  user: timjb
  avatar: https://secure.gravatar.com/avatar/d6eea5713cdf2f25ebf001263fbaa9f4?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png
- name: Michael Aufreiter
  user: michael
  avatar: https://secure.gravatar.com/avatar/d5a959d7e57daa5433fcb9f8da40be4b?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png
categories:
- modules
---

Letterpress is the service that converts Substance documents to various formats (including Markdown, HTML and EPUB) and typesets them using LaTeX. Substance uses this service for it's export / import functionality. This document discusses how to install Letterpress and its implementation.


# Implementation
The implementation is split in two parts:

- A server written in CoffeeScript whose job is to fetch documents, download images, converts and render PDFs.
- An executable written in Haskell which produces the output in the desired format, using Pandoc, an universal markup converter written in Haskell. This enables Letterpress to support many other ouput formats as well as LaTeX.

The first part uses the second for converting the documents. The first part uses a JSON representation of Pandoc's internal abstract syntax tree to communicate with the second. The rules for the serialization/deserialization of Pandoc's AST to/from JSON are derived from Pandoc's type declarations in an automatic fashion. It's therefore important to have a basic understanding of Haskell's type definitions.