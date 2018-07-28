# Creating a Restful API with Node.js and Express

* [What is a Restful API?](#rest-api)
* [HTTP Methods](#methods)
* [Express](#express)
* [MongoDB](#mongo)
* [Further reading](#further)

## Session Objective
This session will give you an overview of what a RESTful API is and we will
create a RESTful service hosted on your machine that handles requests to view
and modify data.

<a name="rest-api"></a>
## What is a Restful API?
For a system to be RESTful it must adhere to the following 6 constraints:
1. **Client–server architecture**  
    Separation of user interface concerns from data storage concerns.
1. **Statelessness**  
    Each request from any client contains all the information necessary to
    service the request.
1. **Cache-ability**  
    Server responses must define themselves as cacheable (or not) to prevent
    clients from getting stale or inappropriate data in response to further
    requests.
1. **Layered system**  
    A client cannot tell whether it is connected directly to the end server, or
    to an intermediary. Intermediary servers may provide load balancing, shared
    caches and/or enforce security.
1. **Code on demand (optional)**  
    Servers can transfer executable code like Java applets or JavaScript.
1. **Uniform interface**  
    Describes 4 constraints:
    * **Resource identification in requests** individual resources are uniquely
    identified in requests. Meaning they can be represented differently from how
    they are stored in a database.
    * **Resource manipulation through representations**
    A client receives enough information about a resource to modify or delete it.
    * **Self-descriptive messages**
    Each response includes enough information for the client to know how to
    process it. E.g. media type states JSON encoding.
    * **Hypermedia as the engine of application state** The ability to follow
    links in responses to other actions that are available. Instead of this
    being hard-coded in the client.

<a name="methods"></a>
## HTTP Methods
A RESTful API uses HTTP requests to perform CRUD operations on data. CRUD stands
for Create, Read, Update and Delete.

**GET** method requests data without producing any side effects.  
e.g `GET /recipes` returns a list of all Recipes in the database.

**POST** method requests the server to create a new resource in the database.  
e.g `POST /recipes` creates a new Recipe.

**PUT** method requests the server to update a resource or create it if it
doesn’t exist.  
e.g. `PUT /recipes/123456` will request the server to update or create the
Recipe with the unique ID *123456* in the Recipes collection.

**DELETE** method requests the server to remove the resource from the database.  
e.g `DELETE /recipes/123456/` will request the server to delete the Recipe with
the unique ID *123456* in the Recipes collection.

<a name="express"></a>
## Express
Express is a JavaScript web framework for Node.js
TODO - expand further.

<a name="mongo"></a>
## MongoDB
MongoDB is a document database.

MongoDB stores data in flexible, JSON-like documents, meaning fields can vary
from document to document and data structure can be changed over time.

This fits well with building a REST API as we often want to return JSON
documents as our responses. We're able to return these very quickly if we're
storing them in exactly the same format we need to supply them in.

## Clone the REST API starting repository
We have created a starter project for building a REST API. Navigate to the
parent folder you wish to clone into and then run:
```
$ git clone git@github.ibm.com:Stephen-Kitchen-CIC-UK/dev-toolcamp-rest-api.git
```

Before we get started with the code we're going to set up the MongoDB database
and add some test data to it.

## Install MongoDB
We'll use [home brew](https://brew.sh/) to install mongo. You will need to
install it if you haven't already. You can use the following to check if it is
installed:
```
$ brew -v
```

You can also check if MongoDB is installed by running:
```
$ mongo --version
```

If MongoDB is not installed run the following:
```
$ brew install mongodb
```

After downloading Mongo, create the “db” directory. This is where the Mongo data
files will live. You can create the directory in the default location by
running:
```
$ mkdir -p /data/db
```

Make sure that the /data/db directory has the right permissions by running:
```
$ sudo chown -R `id -un` /data/db
```

Now start the Mongo daemon that runs the Mongo server by running:
```
$ mongod
```
You can stop this by pressing `ctrl-c` but we want to leave it running whenever
we need to use Mongo.

To check everything is working you can enter the Mongo shell by opening another
terminal (this is so that **mongod** can remain running) and then run:
```
$ mongo
```

The Mongo shell application allows you to access data in MongoDB. Now that we
have verified everything is working we can exit the Mongo shell by running:
```
> quit()
```

## Import MongoDB test data
Some test data has been pre-created for you as part of the REST API starter
project you cloned. It is the file called `importData.json` within the cloned
folder.

The data is JSON encoded and contains an Array with multiple recipes represented
as individual objects. To import this data into MongoDB we need to make sure
`mongod` is running and then run the following command:
```
$ mongoimport --db RecipesDB --collection recipes --drop --file ./importData.json --jsonArray
```
This command imports the data into a new database called *RecipesDB* and a
collection within that database called *recipes*. It also includes the argument
`--drop` which will cause any existing data in that collection to be deleted.
Removing this argument would cause the data to be appended to what was already
there.

## Install dependencies
Before being able to use the REST API project we've cloned we need to install
the dependencies it needs to run. These are defined in the `package.json` file
and can be installed by running within the project folder:
```
$ npm install
```

## Create the initial server
### Add the server code
First we will create an initial server using _express_ by copying the code below into the `server.js` file.

**server.js**
```javaScript
import express from 'express';

const app = express();
const port = 9000;

app.listen(port);

console.log(`Recipe RESTful API server started on: ${port}`);
```

Here we've imported _express_ and created an express application which will
listen for incoming requests from clients on port 9000.  

We've also added a message to display on the command line so that we know our
REST API has started.

### Start the REST API
We can now start the REST API by running the following command within the
project folder:
```
$ npm start
```  

### Access the REST API
Next try accessing http://localhost:9000/recipes in your browser. You should see
the following message: `Cannot GET /recipes`. This shows us that the REST API is
running but doesn't yet know how to respond when we send a GET request to the
`/recipes` path (or any other path).  

We'll now add the code needed to return the data we imported into MongoDB
earlier.

## Create the Model
The model will define the structure of the data.
### Mongoose
TODO

### Add the model code
**recipeModel.js**
```javaScript
import mongoose, { Schema } from 'mongoose';

const recipeSchema = new Schema({
  dateAdded: {
    type: Date,
    default: Date.now,
  },
  difficulty: {
    type: Number,
    default: 1,
  },
  image: {
    type: String,
  },
  ingredients: {
    type: Array,
  },
  method: {
    type: Array,
  },
  title: {
    type: String,
    required: 'Please enter the recipe title.',
  },
});

export default mongoose.model('Recipes', recipeSchema);
```

## Create the Controller
**recipeController.js**
```javaScript
import mongoose from 'mongoose';

const RecipeModel = mongoose.model('Recipes');

export function listAllRecipes(request, response) {
  RecipeModel.find({}, (err, recipe) => {
    if (err) {
      response.send(err);
    }
    response.json(recipe);
  });
}
```

## Create the Route
The routes will determine what action the REST API takes in response to a client
request.  
The client request will include a path (URI) and a HTTP method (GET, PUT, POST,
DELETE etc). Together the path and method are referred to as an _endpoint_.

We will now add some code to match requests to GET http://localhost:9000/recipes
to the use the `listAllRecipes` function we just wrote in the controller.

**recipeRoutes.js**
```javaScript
import { listAllRecipes } from './recipeController';

function recipeRoutes(app) {
  app.route('/recipes').get(listAllRecipes)
}

export default recipeRoutes;
```

## Update the server
TODO
### Add the updated server code
TODO  
**server.js**
```javaScript
import bodyParser from 'body-parser';
import cors from 'cors';
import express from 'express';
import mongoose from 'mongoose';
import recipeModel from './recipeModel';
import recipeRoutes from './recipeRoutes';

const app = express();
const port = 9000;

mongoose.connect('mongodb://localhost/RecipesDB');

app.use(cors());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

recipeRoutes(app);

app.listen(port);

console.log(`Recipe RESTful API server started on: ${port}`);
```
### body-parser
TODO
### CORS
TODO
### Re-start the server
In order for the code changes we've just made to take effect we need to stop
and then re-start the server.

Find the terminal which the server is running in and press `ctrl-c` to stop the
process.

Start the server again by running the same command as earlier:
```
$ npm start
```

### View updated results
If we now try accessing the same adress as before, http://localhost:9000/recipes
in the browser, you should now see a JSON response listing all recipes in the
MongoDB database.

Success!! We now have a REST API which will be able to query from other
applications.

<a name="further"></a>
## Further reading
https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9
https://www.codementor.io/olatundegaruba/nodejs-restful-apis-in-10-minutes-q0sgsfhbd
https://www.mongodb.com/what-is-mongodb
