---
layout: module
title: Substance
abstract: The new Substance runs locally, natively supporting your operating system. However Substance is still built almost exclusively using web technology.
author_twitter: _mql
author: Michael Aufreiter
links:
  source: http://github.com/substance/document
  download: https://raw.github.com/substance/document/gh-pages/document.js
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/modules/0100-01-01-substance.md
version: not yet released
progress: 1
contributors:
- name: Michael Aufreiter
  user: michael
  avatar: https://secure.gravatar.com/avatar/d5a959d7e57daa5433fcb9f8da40be4b?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png
categories:
- modules
published: true
---


# The Substance Application

Below you can see the lastest dev-build of the Substance application. We're working out the kinks to provide you with a solid release as soon as possible.

![](http://f.cl.ly/items/142r2w3m1q2Z1v0g1v2p/substanceApp.jpg)

# Keyboard navigation

Not only Substance keeps the UI-noise as low as possible, it also can also controlled via keyboard. There are shortcuts for adding, moving and deleting content elements, as well as for working with annotations and comments.

# Fast

Substance is fast. With Substance all operations are performed locally, giving it a huge speed advantage on centralized systems that constantly have to communicate with a server somewhere. The Substance editor applies operations locally first, then distributes the changes over the network.

# Secure

Documents are stored locally on your computer. They are safe and secure until you hit publish and replciate them with a trusted Substance Hub.


# Install

    git clone git@github.com:substance/substance.git
    npm install
    node server.js


## Build native OSX Application


    mkdir build
    cd build
    cmake ..
    make


## Enable Webkit Inspector


    defaults write quasipartikel.substance.Substance WebKitDeveloperExtras -bool true


# License

The Substance App will be released under the MIT license. We chose a very libaral license because we wanted to make it easy for you to use Substance in your environment and also get involved into the development.