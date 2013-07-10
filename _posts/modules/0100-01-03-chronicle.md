---
layout: module
category: modules
published: true
title: Chronicle
version: 0.1.0
progress: 1
author: Oliver Buchtala
prose_link: "http://prose.io/#substance/substance.github.com/edit/master/_posts/modules/0100-01-03-chronicle.md"
abstract: A git inspired versioning API.
links: 
  source: "http://github.com/substance/chronicle"
contributors: 
  - name: Oliver Buchtala
    user: oliver
    avatar: /assets/images/team/oliver.png
  - name: Michael Aufreiter
    user: michael
    avatar: "https://secure.gravatar.com/avatar/d5a959d7e57daa5433fcb9f8da40be4b?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png"
---

Substance.Chronicle is a git-inspired versioning API based on [Operational Transformations](http://interior.substance.io/modules/operator.html). The actual content to be versioned or a persistence mechanism is not addressed in this module. Instead one would create an adapter which is implementing an OT interface.

## Getting Started

Consider a simple collaborative editing session of John and Jane.


<iframe width="800" height="250" frameborder="0" scrolling="no" src="http://interior.substance.io/chronicle/">
</iframe>


John starts writing a text (Commit `John - 1`).

    Hsta la vista.

Jane receives the update and instantly fixes John's typo (Commit `Jane`).

    Hasta la vista.
    
In the very same moment John continues writing (Commits `John - 2` and `John - 3`).

    Hsta la vista, baby!

This leads to a situation with concurrent changes which are merged into a common result (Commit `Merge`).

    Hasta la vista, baby!

Substance.Chronicle allows to view versions and resolve more complex version deviations via merging.

## Getting Really Started

Substance.Chronicle can be considered a low-level API. Some integration and glueing is necessary to get things moving.

Installation is easy.

	npm install substance-chronicle
    
In your Node.js script:

	var Chronicle = require('substance-chronicle');

Basically it is necessary to define some kind of `Change` type and an adapter that can deal with that:

    function YourVersioningAdapter() {
    
      	// applies the change to your data
    	this.apply = function(change) {};

		// inverts a change
        this.invert = function(change) {};

		// transforms changes according to operational transformation
        this.transform = function(a, b, options) {}

		// resets your document
		this.reset = function() {}
	};

The difficult part is to specify `Change` types that are invertible and transformable. Here, Substance.Operator comes in providing basic operations for text, arrays, and objects.

Having your adapter you can begin chronicling using

    var chronicle = Chronicle.create();
    chronicle.manage(yourAdapter);
    
To get things recorded you need to tell the Chronicle to do so:

    chronicle.record(someChange);

For more sophisticated examples see the [testsuite](https://github.com/substance/chronicle/tree/master/tests).
