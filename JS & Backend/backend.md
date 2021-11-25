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
  - [Express](express-js)
     -[Folder Structure](folder-structure)
   
  - [APIs](#apis)
    - [Intro to API's](#intro-to-apis)
      - [API Endpoint](#api-endpoint)
    - [JSON and XML](#json-and-xml)
      - [XML](#xml)
      - [JSON](#json)
    - [Making Requests with Node.js](#making-requests-with-nodejs)
  - [Databases](#databases)
    - [Intro to Databases](#intro-to-databases)
    - [SQL (relational) vs NoSQL (non-relational)](#sql-relational-vs-nosql-non-relational)
      - [SQL](#sql)
      - [NoSQL](#nosql)
    - [Data Association](#data-association)
  - [MongoDB](#mongodb)
    - [Running Mongo](#running-mongo)
    - [Mongo Commands](#mongo-commands)
     


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
### Package.json

Package.json is a file with metadata about the project (description, name, version, license, dependencies)

Dependencies are the packages the application relies and needs to work (at runtime)
- React, Express, Redux, etc.

Devdependencies are modules which are only required during development
- Nodemon, Babel, ESLint, Mocha, etc.

The node modules folder is not included in GitHub repositories\
Rather that uploading all of the packages, we can just include information about the required packages in package.json and install them with one command

When installing a package we can add flags to take the package name and version and save it into our package.json file
- --save (``npm i -S``) to save it as a depenpency
- --save-dev (``npm i -D``) to save it as a devDependency
- After node version 9 we can omit ``--save`` flag

To create a package.json we can use ``npm init`` command and then follow the instructions

```bash
$npm init

name: #name of the folder by default
version: #(1.0.0) by default
description:
enrty point: #the file where our application starts, index.js by default
test command:
git repository:
keywords:
author:
license: #ISC by default
```

# Express

A library is a code that someone else wrote and we can include and use in our app

A framework is almost the same, but the way that we use it is different\
The most inportant difference is Inversion of Control
- When you call a library, you are in control
    - Library is a collection of functionality that you can call
- When with a framework, the control is inverted: the framework calls you
    - This is called the Hollywood principle: Don't call Us, We'll call You
    - Basically, all the control flow is already in the framework, and there's just a bunch of predefined white spots that you can fill out with your code.


Our Very first express-App
```
const express = require('express');

const app = express();


app.get('/', (req,res) => {
    res.send('It Worked...')
})

app.listen(3000, ()=> {
    console.log('server is Listening on Port 3000');
})
```


use is a method to configure the middleware used by the routes of the Express HTTP server object.
```
app.use(() => {
    console.log('We Got New Request');
})

```

#### Folder Structure

One pattern of folder structure of an Express app

- handlers
    - functions that we pass to our routes
- routes
    - routes for our app
- middleware
    - middleware functions
- models
    - database models
- views
    - page templates, if we don't use front-end framework
- public
    - assets for our app if we don't use front-end framework
- index.js


## APIs

### Intro to API's

Application Programming Interface(API) in a broad sense is a set of routines, protocols, and tools for building software and applications

It is a way to connect with other applications, interface which allows two systems to communicate with one another
- It could be a database API (locally)
- Video card API
- API to incorporate graphical elements
- Web APIs

Web APIs generally communicate via HTTP
- Twitter API 'give me all tweets that mention "ice cream"'
- Reddit API 'what is the current top post?'
- Weather API 'what is the weather in New York?'
- Some APIs can be found at programmableweb.com

#### API Endpoint


An endpoint is one end of a communication channel
- When an API interacts with another system, the touchpoints of this communication are considered endpoints
- For APIs, an endpoint can include a URL of a server or service
- Each endpoint is the location from which APIs can access the resources they need to carry out their function
- Endpoints specify where resources can be accessed by APIs and play a key role in guaranteeing the correct functioning of the software that interacts with it
- API performance relies on its ability to communicate effectively with API Endpoints

### JSON and XML

When we use the internet, we make HTTP request and get HTML back

APIs don't respond with HTML because HTML contains info about the structure of the page, and APIs respond with data, not structure
- They use simpler data formats like XML and JSON

#### XML

XML stands for Extended Markup Language
- It is syntacticly similar to HTML, but it does not describe presentation like HTML does

```xml
<person>
    <age>21</age>
    <name>Travis</name>
    <city>Los Angeles</city>
</person>
```

#### JSON

JSON stands for Javascript Object Notation
- JSON looks exactly like JavaScript objects, but everything is a string

```json
{
    "person": {
        "age": "21",
        "name": "Travis",
        "city": "Los Angeles"
    }
}
```

### Making Requests with Node.js

We can make requests from a browser, from a command line

```bash
$curl http://www.google.com
```

Inside of an application we can make requests by using a package 'request'
- usually we recieve data as a string
- to get data as a JSON use ``JSON.parse(data)``

```javascript
var request = require('request');
request('http://www.google.com', function (error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body); // show the HTML for the Google homepage
    }
});

request('http://someAPI.com', function (error, response, body) {
    // another way of writing
    if (error) {
        console.log('Something went wrong');
        console.log(error);
    } else {
        if (response.statusCode == 200) {
            var parsedData = JSON.parse(body);
            console.log(body); // string
            console.log(parsedData); // object
            console.log(['query']['results']); // prints data in 'query -> results'
        }
    }
})
```

---

## Databases

### Intro to Databases

Database is a collection of information/data which has an interface to interact with this data (add, remove, edit data)

### SQL (relational) vs NoSQL (non-relational)

#### SQL

SQL are tabular (we have to define patterns ahead of time) and flat databases

<table>
    USERS TABLE
    <tr>
        <td>id</td>
        <td>name</td>
        <td>age</td>
        <td>city</td>
    </tr>
    <tr>
        <td>1</td>
        <td>John</td>
        <td>24</td>
        <td>NYC</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Helen</td>
        <td>23</td>
        <td>Missoula</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Peter</td>
        <td>34</td>
        <td>Moscow</td>
    </tr>
<table>

<table>
    COMMENTS TABLE
    <tr>
        <td>id</td>
        <td>text</td>
    </tr>
    <tr>
        <td>1</td>
        <td>'come visit Montana!'</td>
    </tr>
    <tr>
        <td>2</td>
        <td>'lol'</td>
    </tr>
    <tr>
        <td>3</td>
        <td>'I love puppies'</td>
    </tr>
    <tr>
        <td>4</td>
        <td>'seriously Montana is great!!'</td>
    </tr>
<table>

If we want to express relationship between users and comments, the only way to do it is through another table

<table>
    USER/COMMENTS JOIN TABLE
    <tr>
        <td>userId</td>
        <td>commentID</td>
    </tr>
    <tr>
        <td>1</td>
        <td>3</td>
    </tr>
    <tr>
        <td>2</td>
        <td>1</td>
    </tr>
    <tr>
        <td>2</td>
        <td>4</td>
    </tr>
    <tr>
        <td>3</td>
        <td>2</td>
    </tr>
<table>

We need to follow the established pattern very closely
- If we want to add a new property to someone (e.g. favColor of Peter), we would need to create a favColor for everyone which should be empty for everyone else (null, undefined, false) - and that's not flexible

#### NoSQL

NoSQL databases are more flexible, we don't have to define any patterns ahead of time, and things could be nested (it's not flat)
- It looks similar to JS, it is BSON (Binary JavaScript Object Notation)
- Flexibility doesn't make it better than SQL, for some cases it's better, for some - not

```javascript
{
    name: "Helen",
    age: 23,
    city: Missoula,
    comments: [
        {text: 'come visit Montana!'},
        {text: 'seriously Montana is great!!'},
        // if we want to add new data we would just push it into this object
        {text: 'why does no one care about Montana?'}
    ],
    favColor: 'purple'
}

{
    name: "Sally",
    age: 23,
    city: Missoula,
    comments: [
        {text: "I don't like Montana at all"},
    ],
    favFood: 'steak'
}
```

### Data Association

- One to one (One item relates to one another item)
    - One book - one publisher
- One to many (One entity is related to many entities)
    - One user - many uploaded photos
- Many to many (Association goes both ways)
    - Students have multiple courses, and each course has many students

---

## MongoDB

### Running Mongo

To run the DB: 
- "C:\Program Files\MongoDB\Server\4.0\bin\mongod.exe" --dbpath="``YOUR PATH``"
- [initandlisten] waiting for connections
- run mongo

### Mongo Commands

- help
- show dbs
    - Shows databases that you have
- use \<db name>
    - Uses the selected db
    - If there is no such db, Mongo creates it
- db.\<collection>.insert({data})
    - Create
    - We add things in by creating collections (they group data together)
    - If there is no such collection, Mongo creates it
    - db.dogs.insert({name: "Rusty", breed: "Mutt"})
- db.\<collection>.find()
    - Read
    - Returns everything in a collection if ()
    - Looks for an item (or items)
    - db.dogs.find({name: "Rusty"})
- db.\<collection>.update()
    - Update
    - Updates data of an item
    - db.\<collection>.update({name: "Lulu"}, {breed: Labradoodle"})
        - Will update the breed of "Lulu" but will lose everything else (name, age, etc.)
    - If we want to update items without overwriting them:
        - db.dogs.update({name: "Rusty", {$set: {name: "Tater", isCute: true}}})
- db.\<collection>.remove()
    - Destroy (delete)
    - db.dogs.remove({breed: "Labradoodle"})
    - Removes everything matching by default
- db.\<collection>.drop()
    - Drops (deletes) the whole collection
 
 


