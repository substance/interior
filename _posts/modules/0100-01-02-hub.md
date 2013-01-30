---
layout: module
title: Substance.io
abstract: Substance.io is the where your published documents go and where people can read them.
author_twitter: _mql
author: Michael Aufreiter
links:
  demo: http://substance.io
prose_link:
  http://prose.io/#substance/substance.github.com/edit/master/_posts/modules/0100-01-02-hub.md
version: not yet released
progress: 0
contributors:
- name: Michael Aufreiter
  user: michael
  avatar: https://secure.gravatar.com/avatar/d5a959d7e57daa5433fcb9f8da40be4b?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png
- name: Pier Paolo Ramon 
  user: yuchi
  avatar: https://secure.gravatar.com/avatar/fc40b1fe79ea6b10825141d86f767354?s=420&d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-user-420.png
categories:
- modules
published: true
---

Anyone can create a free account on the Substance.io server and start publishing their content online in one click straight from the Composer. You can think of it as an open document repository from where you will be able to manage your published content, add it to existing networks, find other people’s public documents or export yours in any imaginable format (print, web, tablet, mobile and more).

<!--## Networks

Documents can be published to topic-related networks, so people can find them easily. Substance users can subscribe to Networks, so they can see new documents as well as updates made to existing ones. We're aware that today we're overwhelmed by the precesence of [too much information](http://en.wikipedia.org/wiki/Information_overload), so our goal is letting the user decide what to see and what not to see.

![](http://f.cl.ly/items/1I0q3L1U3d3O0U3p0J3Y/Screen%20Shot%202012-10-20%20at%209.56.34%20PM.png)
-->

## Less noise

Substance is optimized for distraction-free exploring and reading. We're trying to add only what's indispenable and leave everything else out. More importantly, you won't see any ads while reading a document. Ever.

# Substance API

Substance is exposing a simple API so you can process Substance documents in your own application.

Here's what you can do:

- Create a publication programatically: The document will show up at Substance.io
- Update an existing publication with new content
- Search for documents
- Delete a document or specific version
- Create a new user at Substance.io
- Update user details


## Authentication

There are two ways to authenticate through Substance API v1.

### Basic Authentication

    $ curl -u "username" https://substance.io/api/v1

### Using a token

    $ curl -H "Authorization: token YOUR-TOKEN" https://substance.io/api/v1

Tokens can be obtained using OAuth for web-applications, or our secure authenication service for native apps.


## User API

### Authenitcate

    POST /authenticate

*Input*

    {
      "username": "john",
      "password": "secretpassword"
    }

*Response*

    Status: 200 OK
    ---
    {
      "token": "YOUR_SECURE_TOKEN"
    }

Provide this token as a header to all authenticated requests.


### Get user

    GET /users/:user

*Response*

    {
      "username": "michael",
      "name": "Michale Aufreiter",
      "company": "Substance.io",
      "location": "Vienna",
      "followers": 20,
      "public_documents": 24,
      "created_at": "2008-01-14T04:33:35Z"
    }


### Get the authenticated user

    GET /user


*Response*

    {
      "username": "michael",
      "name": "Michale Aufreiter",
      "email": "topsecret@gmail.com",
      "company": "Substance.io",
      "location": "Vienna",
      "followers": 20,
      "public_documents": 24
      "created_at": "2008-01-14T04:33:35Z",
    }


### Create user

This service is not public yet.

    POST /users

*Input*

    {
      "username": "john",
      "email": "johndoe@mail.com",
      "name": "John Doe"
      "password": "secretpassword",
      "challenge": "secretanswer"
    }

*Response*

    Status: 200 OK



### Update user

Update the authenticated user.

    PUT /user

*Input*

    {
      "username": "john",
      "email": "johndoe@mail.com",
      "name": "John Doe"
      "password": "secretpassword"
    }



## Document API

### Create a document

    curl -X POST -H "Content-Type: application/json" -d '{"username": "victor"}' curl -X POST http://duese.quasipartikel.at:3000/api/v1/documents/create

*Input*

    {
      "username": "YOUR_SUBSTANCE_USER"
    }

*Response*

    Status: 200 OK
    ---
    {
      "id": "dd9e821d5e01300cf06a4c61477d18a9",
      "meta": {
        "created_at": "2013-01-23T15:43:05.908Z",
        "updated_at": "2013-01-23T15:43:05.908Z"
      }
    }


### Delete a document

    DELETE /documents/:document


### Delete a specific version of a given doc

    DELETE /documents/:document/:version


### Get latest version of a document

    GET /documents/:document


### Get a specific version of a given doc

    GET /documents/:document/:version


### Search documents

Search for documents by query.

    GET /documents?q=SEARCH_STR

*Response*

    Status: 200 OK
    ---
    [
      {
        "title: "Doc 1",
        "created_at": "2013-01-13T18:19:26.624Z"
      },
      ...
    ]