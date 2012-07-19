---
layout: feature
title: Realtime Collaboration
abstract: Support for realtime collaboration
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/features/0100-01-02-realtime-collaboration.md
author_twitter: _mql
author: Michael Aufreiter
categories:
- features
published: true
---

Substance has a strong focus on collaboration. That means people should be able to work on a document together very easily, even in realtime.

# Operations

Documents are transformed through atomic operations, which allows us to implement interesting things, such as realtime updates and patches.

# Collaborative editing in realtime

Co-authors can simultaneously edit one document at the same time. Text is synchronized in realtime among all co-authors. You can invite other Substance users to co-author your document. Changes made by others appear in realtime. To make this possible we're using a technique called [Operational Transformation](http://ot.substance.io).

![](/images/illustrations/ot.png)

However, for non-text content types (such as Formulas) we don't think it's a good idea to synchronize changes in realtime. It would dramatically complicate Plugin Development. Our proposed solution would be an explicit lock by one user until editing (e.g. the formula) is complete.

# Comments

Substance targets open collaboration. Everyone (including readers) can add comments to a document and refer to a particular piece of information contained in that document.

# Patches

Readers are able to participate and comment on certain text passages. While readers can't edit the document directly, they're able to make changes and submit them as a patch. Patches are then reviewed by original authors and can easily be applied to the document. Unlike with Wikis, by using such patches ownership of the original author(s) can be preserved.

![](http://substance-assets.s3.amazonaws.com/be/eee70a51ed570f7096ff3bce36a99d/Roadmap-03.png)