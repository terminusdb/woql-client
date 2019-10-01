terminus-client
===============

[![build status](https://api.travis-ci.org/terminusdb/terminus-client.svg?branch=master)](https://travis-ci.org/terminusdb/terminus-client)
[![Coverage Status](https://coveralls.io/repos/github/terminusdb/terminus-client/badge.svg?branch=master)](https://coveralls.io/repos/github/terminusdb/terminus-client/badge.svg?branch=master)
[![code helpers]

Promise based terminus client for the browser and node.js

## Requirements
- [TerminusDB](https://github.com/terminusdb/terminusdb)
- [NodeJS 8.1.4+](https://nodejs.org/en/)

## Installation

This is a Node.js module available through the npm registry.

Before installing, download and install Node.js. Node.js 0.10 or higher is required.

Installation is done using the npm install command:

Using npm:

```bash
$ npm install --save @terminusdb/terminus-client
```

Using cdn:

```html
<script src="https://unpkg.com/@terminusdb/terminus-client/dist/terminus-client.min.js"></script>
```

## Docs & Community

## Usage

```javascript
//
const TerminusClient = require('@terminusdb/terminus-client');

//Create a new instance of terminus client
const client = new TerminusClient.WOQLClient();

//Connect to a Terminus server at the given URI with an API key
client.connect("http://localhost:6363/", 'secret').
 .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .finally(function () {
    // always executed
  });


//use async/await.
async function getCapabilities() {
  try {
    const response = await client.connect("http://localhost:6363/", 'secret');
    console.log(response);
  } catch (err) {
    console.error(err);
  }
}

```



## Options
connections options.

To initialize `TerminusDB client` with custom options use

```js
const TerminusClient = require('@terminusdb/terminus-client')

const client = new TerminusClient.WOQLClient({
    server:"http://localhost/",
    dbid:"test_db",
    include_key:true
});

```

## API

##### `createDatabase([dburl:String, details:Object, key:String]):Object`
Create a new terminusDB database in the current terminusDB server

```js
var currentTerminusServerUrl=client.connectionConfig.dbURL();

var details={
   "@context":{
      "rdfs":"http://www.w3.org/2000/01/rdf-schema#",
      "terminus":"http://terminusdb.com/schema/terminus#",
      "_":"http://localhost:6363/test_new_db/"
   },
   "terminus:document":{
      "@type":"terminus:Database",
      "rdfs:label":{
         "@language":"en",
         "@value":"new db tests"
      },
      "rdfs:comment":{
         "@language":"en",
         "@value":"new db description"
      },
      "terminus:allow_origin":{
         "@type":"xsd:string",
         "@value":"*"
      },
      "@id":"http://localhost:6363/test_new_db"
   },
   "@type":"terminus:APIUpdate"
}


client.createDatabase("newD",details,'root');

...

```

##### `deleteDatabase():{[dbUrl:string]}`
For delete a terminusDB 

```js
//if authorized you can delete a terminusDB in the server myTerminusServer
client.deleteDatabase("http://localhost:6363/dbID");

or

//you can delete a database in the current seleted server
client.deleteDatabase("dbID");
...

```

##### `getSchema():{[schurl:String, opts:Object]}`
For get a terminusDB schema 

```js

//Retrieves the schema of the specified database by Full Url
client.getSchema("http://localhost:6363/dbID");

or

//you can get a database schema in the current seleted server
client.getSchema("dbID").then((response)=>{
  console.log("response")
}).catch((err)=>{
  console.log(err);
});
...

```

//https://github.com/terminusdb/terminus-schema
const opts={terminus:encoding: "terminus:turtle"}


##### `updateSchema():{[schurl:String, doc:String, opts:Object])`
For Update a terminusDB schema
schurl TerminusDB server URL or a valid TerminusDB Id or omitted 
doc is OWL schema String 
Some example[TerminusDB OWL Schema] (https://github.com/terminusdb/terminus-schema)

```js

const doc="@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.........."

const opts={terminus:encoding: "terminus:turtle"}

client.updateSchema(false,doc,opts).then((response)=>{
  console.log(response)
}).catch((err)=>{
  console.log(err)
});

...

```




## Testing
* Clone this repository

* Install all development dependencies
```sh
$ npm install
```

* Then run test
```sh
$ npm run test
```

## Contribute
It will be nice, if you open an issue first so that we can know what is going on, then, fork this repo and push in your ideas. Do not forget to add a bit of test(s) of what value you adding.

## Licence

The APACHE 2.0 License 

Copyright (c) 2019 ........
 
