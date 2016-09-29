+++
title = "First steps with No-SQL MongoDB"
description = "First steps with No-SQL MongoDB"
tags = [
    "development",
    "javascript",
    "no-sql",
]
date = "2016-04-20"
categories = [
    "Development",
]

toc = true # optional, When set to TRUE this parameter, table of contents appears in only this article.
+++

It’s easier that you think to start with a No-SQL database like MongoDB.

The first step is to install MongoDB. I am going to install it in Ubuntu 14.04 with this few lines of code in bash.

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```
If you want to install it with other OS or a specific version you should visit the [official page](https://docs.mongodb.org/manual/installation/)

Once you have installed it you can start the service as usual with this command
sudo service mongod start
Ok, now we have a local MongoDB in out system, let’s do a quick example with nodeJS and mongoDB.

In order to make our program as easy as possible, we will insert manually the data in our database using the mongo shell.
Type mongo to open the shell and then write this commands.

```bash
show dbs
use hello
db.world.find()
db.world.insert({test: "welcome to mongoDB!"})
db.world.find()
exit
```

Now that we have the sample data inserted in our database we will begin with our application in node.

I am supposing that you have nodeJS already installed. But if you need to install it, just follow a simple guide to install node and npm before following with this tutorial.

Ok, the first step is to create a main file, i have called it app.js

touch app.js

Then insert this code with your favourite editor.

```js
var MongoClient = require('mongodb').MongoClient;

// Open the connection to mongoDB to database named 'hello'
MongoClient.connect('mongodb://127.0.0.1:27017/hello', function(err, db) {
    if(err) throw err;
    // Find one document in our collection 'world'
    db.collection('world').findOne({}, function(err, doc) {
        if(err) throw err;
        // Print the result if found or null if not found.
        console.dir(doc);

        // It's important to close the DB after you have finished
        db.close();
    });
});
```

If you try to execute this file, you will receive an error, the reason is that you must install the package ‘mongodb’ managed by npm

Now create a second file named package.json and fill it with this lines

```json
{
  "name": "hi",
  "version": "0.0.0",
  "description": "tutorial with mongodb and node",
  "main": "app.js",
  "dependencies": {
    "mongodb": "~1.3.10"
  },
  "author": "Samuel Martin",
  "license": "BSD"
}
```

Now to install the mongo package just type npm install or sudo npm install

Ok, we are almost finished. The last step is to execute our program with node app.js or nodejs app.js depending of how you have installed nodejs.

And the output should be something like

```json
{ _id: 5711f731318961da656a8426, test: 'welcome to mongoDB!' }
```
