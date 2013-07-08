---
layout: module
category: modules
published: false
title: Client
version: 0.1.0
progress: 1
author: Michael Aufreiter
author_twitter: _mql
prose_link: "http://prose.io/#substance/substance.github.com/edit/master/_posts/modules/0100-01-05-client.md"
abstract: Interact with Substance programatically.
links: 
  source: "http://github.com/substance/client"
contributors: 
  - name: Michael Aufreiter
    user: michael
    avatar: "https://secure.gravatar.com/avatar/d5a959d7e57daa5433fcb9f8da40be4b?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png"
---

The Substance Client can be used to interact with the Substance server programmatically. While the Client API itself is ready, it takes some more time to release the latest version of the Substance Hub.

Create a new client

    var client = new Substance.Client({
      hub_api: 'https://substance.io/api/v1'
    });

Authenticate

    client.authenticate('your_user', 'your_password', cb);


# Document API

## Create a new document

    client.createDocument('hello-world', function(err, doc) {
      console.log('new doc created', doc);
    });


## Get an existing document

    client.getDocument('hello-world', function(err, doc) {
      console.log('current doc');
    });


## List documents

    client.listDocuments(function(err, documents) {
      console.log('Documents:', documents);
    });


## Delete an existing document

    client.deleteDocument('hello-world', function(err) {
      console.log('document deleted');
    });


## List commits for a documents

    client.documentCommits('hello-world', 'head', 'commit-25', function(err, commits) {
      console.log('commits from head to commit-25');
    })


## Update document
  
    var commits = {
      "18055b209dae666744c0913672985cb5": {
       "op": [
        "update",
        {
         "id": "text:628df690",
         "data": {
            "content": [
              "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In in neque mauris. Nullam semper tellus ac quam consectetur at dictum purus imperdiet. Proin quis arcu sit amet turpis rutrum ullamcorper at vitae sapien. Curabitur tempor lectus nec dolor suscipit sed interdum nulla auctor. Etiam id fermentum sapien. Nam eleifend mi sit amet felis auctor at tincidunt odio ornare. Sed ac est sed libero rhoncus euismod."
            ]
          }
        }
       ],
       "sha": "18055b209dae666744c0913672985cb5",
       "parent": "477fdfda09b92eb6eebd3e0b4bbd112e"
      }
    };

    var meta = {
      "title": "Lorem Ipsum"
    };

    var refs = {
      "master": {
        "head": "18055b209dae666744c0913672985cb5",
        "last": "18055b209dae666744c0913672985cb5"
      }
    };

    client.updateDocument('hello-world', commits, meta, refs, function(err) {
      console.log('document has been updated successfully.');
    });

## Create Blob

In order to create a blob on the server do this:

    client.createBlob('my-new-blob', 'BASE64-encoded-blobdata', function(err) {
      console.log('Blob created.');
    });


## Get an existing blob

    client.getBlob('my-new-blob', function(err, blob) {
      console.log('Blob', blob);
    });



# Publications API

## Create a new publication

    client.createPublication('hello-world', 'public', function(err) {
      console.log('Created a publication of hello-world in the public network');
    });


## Delete publication

    client.deletePublication('hello-world', 'public', function(err) {
      console.log('deleted publication');
    });


## Load publications

For a given document, load all available publications

    client.loadPublications('hello-world', function(err, publications) {
      console.log('pubs', publications);
    });


## Load networks

    client.loadNetworks(function(err, networks) {
      console.log('Load all available networks');
    });


# Versions API

## Create a new version

    client.createVersion('hello-world', 'JSON_DATA', function(err) {
      console.log('version created successfully');
    });

## Unpublish documennt


    client.unpublish('hello-world', function(err) {
      console.log('unpublished all versions for document hello-world');
    });


# Collaborators API

## Load collaborators

    client.loadCollaborators('hello-world', function(err, collaborators) {
      console.log('collaborators', collaborators);
    });


## Create collaborator

    client.createCollaborator('hello-world', 'johndoe', function(err) {
      console.log('johndoe has been added as a collaborator');
    });


## Delete collaborator

    client.deleteCollaborator('hello-world', 'johndoe', function(err) {
      console.log('removed collaborator johndoe from document');
    });
