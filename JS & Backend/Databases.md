- [Databases](#databases)
    - [Intro to Databases](#intro-to-databases)
    - [SQL (relational) vs NoSQL (non-relational)](#sql-relational-vs-nosql-non-relational)
      - [SQL](#sql)
      - [NoSQL](#nosql)
    - [Data Association](#data-association)
  - [MongoDB](#mongodb)
    - [Running Mongo](#running-mongo)
    - [Mongo Commands](#mongo-commands)

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

### Mongoose

Mongoose is a tool which helps to interact with MongoDB in the JS app
- It is a MongoDB object modeling in Node.js (Object Data Mapper, ODM)

#### Usage of Mongoose

```javascript
var mongoose = require('Mongoose');
mongoose.connect('mongodb://localhost/cat_app'); // creates cat_app if there's no such DB

// *********************
// debug mode allows us to see what's happening at any given point when things are being sent to a database, when they're failing instead of just silently failing
// it's better to set it up in our models/index.js file
mongoose.set('debug', true);
// *********************

// define what a cat looks like (telling JS that we want to be able add cats to the DB)
// this is not defining a table, this is defining a pattern (anything else can be added if needed), by default they are not required
var catSchema = new mongoose.Schema({
    // we can also add an object in, and say type: string, and give it other pieces of data like if it's required, and give a message or if it has some default value
    name: {
        type: String,
        required: 'Name cannot be blank!'
    }
    age: Number,
    temperament: String
});


// we take the schema (pattern) and compile it into a model and save it into a variable (now it is an object which has all the methods we need)
var Cat = mongoose.model('Cat', catSchema); 
// 'Cat' is a single version of the collection name (collection will be 'cats')
// *** don't forget to export it ***

// add a new cat to the DB
var george = new Cat({
    name: 'George',
    age: 11,
    temperament: 'Grouchy',
});

george.save((err, cat) => {
    if (err) {
        console.log('Something went wrong');
        console.log(err);
    } else {
        console.log('We just saved a cat to the DB');
        console.log(cat); // cat is what's coming from the DB, and 'george' isn't (it is what we're trying to save to the DB)
    }
});

// another way to add a cat:
Cat.create({
    name: 'Snow White',
    age: 15,
    temperament: 'Nice'
}, (err, cat) => {
    if (err) {
        console.log(err);
    } else if {
        console.log(cat);
    }
});

// retrieve all cats from the DB
Cat.find({}, (err, cats) => {
    if (err) {
        console.log('Something went wrong');
        console.log(err);
    } else {
        console.log('All the cats are...');
        console.log(cats);
    }
});
```
