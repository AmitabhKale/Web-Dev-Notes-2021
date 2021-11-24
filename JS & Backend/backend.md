# JS & Backend for Web Dev

#### Contents

- [JS and Backend](#js-and-backend)
      - [Table of Contents](#table-of-contents)
  - [HTTP in Depth](#http-in-depth)
  - [Command Line](#command-line)
  - [Node.js](#nodejs)
    - [What Is Node.js](#what-is-nodejs)
    - [Node Console](#node-console)
    - [NPM](#npm)


## HTTP in Depth

The most important thing that's happening when you go to some website is the 'request-response' cycle and it's independent from a browser

HTTP is hypertext transfer protocol

HTTP verbs are various HTTP requests\
They tell the server what to do, what we're requesting, e.g:
- Get request - we are asking server to get us some data
    - the only request accessible from a browser navbar or search bar
    - searching something is a GET request
        - query string starts with ? and is separated by &
- Post reqiest - we are sending some data with a request to server to be added to database or something
    - some sign up forms or something
- Put and Patch requests are used to update some data
    - update a post on Facebook

When a server gets a 'Delete' request, we expect something to be deleted (but it doesn't happen just because of the request)

Important parts of a response:
- Body of the response (what's sent back)
    - e.g. HTML, CSS, and JS when we are visiting some website
- Headers (metadata about the response)
    - e.g. content type, date, status
- Status (it's a number, a part of the protocol, a standardized way of transferring a status of a response)

---

## Command Line

Note: Still not sure what to use: cmd, powershell, gitbash or WSL or even Babun (possibly with ConEmu)

- ls shows all of the contents of the current folder we're inside of
    - ``ls dirname`` to see the contents of specific folder
- cd is used to change directories
    - ``cd ..`` to go back one level
    - you can start writing the name of a directory and hit tab to autocomplete it
- touch is used to create new files
    - ``touch orange.txt``
- mkdir is used to create a new folder
    - ``mkdir FavColors``
- rm is used to delete a specific file
    - ``rm orange.txt``
- rm -rf allows us to remove entire directories
    - ``rm -rf colors/``
    - ``rm -rf /`` deletes everything!
    - -rf is a flag, a way to change what the command does
        - stands for 'recursive force'

---


## Node.js

### What Is Node.js

Node.js is a JS runtime built on Chrome's JS engine
- allowed JS to run not only in the browser
- it is a way to write and run JS on the server side

Node.js's package system, npm, is the largest ecosystem of open source libraries in the world

### Node Console

Based on command line, basically we can write JS code in a command line or run a file with node
- although we can't use some things which are available in a browser console like document, alert, etc.

```bash
$node
>'hello ' + 'world'
>'hello world'
# Ctrl+C twice to exit
$node hello.js
```
It is called REPL - Read-Evaluate-Print Loop - is a simple, interactive computer programming environment that takes single user inputs (i.e., single expressions), evaluates them, and returns the result to the user
- exists in many server side languages, e.g. in ruby

### NPM

NPM stands for Node Package Manager; it is a way to include 'libraries' when we write server-side JS

To install a package (the list could be found at npmjs.com):

```bash
$npm install <package name>
# npm install <package name>@version
```

To include a package:

```javascript
var cat = require('cat-me'); // cat-me is the name of a package
```
