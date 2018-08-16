# Creating a Restful API with Node.js and Express

* [What is a Restful API?](#rest-api)
* [HTTP Methods](#methods)
* [Express](#express)
* [MongoDB](#mongo)
* [Configure MongoDB](#configure-mongo)
* [Clone the REST API starting repository](#clone)
* [Import MongoDB test data](#import-data)
* [Install NPM dependencies](#install-dependencies)
* [Create the initial server](#create-server)
* [Create the Model](#create-model)
* [Create the Controller](#create-controller)
* [Create the Route](#create-route)
* [Update the server](#update-server)
* [Further reading](#further)

## Session Objective
This session will give you an overview of what a RESTful API is and we will
create a RESTful service hosted on your machine that handles requests to view
data stored in a MongoDB database.

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

The **GET** method requests data without producing any side effects.  
e.g `GET /recipes` could return a list of all Recipes in the database.

The **POST** method requests the server to create a new resource in the
database.  
e.g `POST /recipes` could create a new Recipe.

The **PUT** method requests the server to update a resource or create it if it
doesn’t exist.  
e.g. `PUT /recipes/123456` could request the server to update or create the
Recipe with the unique ID *123456* in the Recipes collection.

The **DELETE** method requests the server to remove the resource from the
database.  
e.g `DELETE /recipes/123456/` could request the server to delete the Recipe with
the unique ID *123456* in the Recipes collection.

<a name="express"></a>
## Express
Express is a JavaScript web framework for Node.js. It helps you to organise your
web application into an Model-View-Controller (MVC) architecture on the server
side.

Express helps you to manage things like handling routes and requests. Without it
you would have to manually parse payloads, handle cookies and sessions and
select the correct route pattern based on something like regular expressions.

We will be using Express as the framework for our REST API.

<a name="mongo"></a>
## MongoDB
MongoDB is a document database.

MongoDB stores data in flexible, JSON-like documents, meaning fields can vary
from document to document and data structure can be changed over time.

This fits well with building a REST API as we often want to return JSON
documents as our responses. We're able to return these very quickly if we're
storing them in exactly the same format we need to supply them in.

We will be using MongoDB as the database for our REST API.

<a name="configure-mongo"></a>
## Configure MongoDB

Create the “db” directory. This is where the Mongo data
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

<a name="clone"></a>
## Clone the REST API starting repository
A REST API starter project has been created for you. First navigate to the
parent folder you wish to clone the repository into, and then run:
```
$ git clone git@github.ibm.com:Stephen-Kitchen-CIC-UK/dev-toolcamp-rest-api.git
```

Before we get started with the code though we're going to import some test data
into a MongoDB database.

<a name="import-data"></a>
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

<a name="install-dependencies"></a>
## Install NPM dependencies
Before being able to use the REST API project we've cloned we need to install
the dependencies it needs to run. These are defined in the `package.json` file
and can be installed by running within the project folder:
```
$ npm install
```

<a name="create-server"></a>
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

<a name="create-model"></a>
## Create the Model
The model defines the structure of the data that the REST API works with. It
defines the shape of the data provided to the REST API and also returned by the
REST API to the clients querying it.

### Mongoose
We'll be using Mongoose which provides us with an easier way to interact with
data in MongoDB. It allows us to create Schemas and Models which dictate the
structure that the data must take to be considered valid.

### Add the model code
We'll now add the code for our recipe model, using mongoose to define the
schema.

Copy the code below into the `recipeModel.js` file:  

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

export default mongoose.model('Recipes', recipeSchema, 'recipes');
```
Here we've defined a new schema which lists the fields that a recipe stored in
the database can have. The fields in our case are:
`dateAdded, difficulty, image, ingredients, method, title`  

For each field the type of the field is defined too.  

We've also provided default values for `dateAdded` and `difficulty` if they're
not supplied. For dateAdded it will be the current date and for difficulty it
will default to `1`.

Lastly we've specified that the `title` is a required field. If it is not
supplied then the message `Please enter the recipe title.` will be returned.

The last line in the file adds the schema to the mongoose model with the key
`Recipes`. It is the model which will be imported by other files importing this
module (recipeModel.js). It also maps this schema to the `recipes` collection
that we've imported our data into using the `mongoimport` command we ran
earlier.

<a name="create-controller"></a>
## Create the Controller
The controller defines the methods that interact with the model to read data
from it and make updates to it.

We're just going to define one method which will return all of the recipe
records in the database.

Copy the following code into the `recipeController.js` file:

**recipeController.js**
```javaScript
import mongoose from 'mongoose';

const RecipeModel = mongoose.model('Recipes');

export function listAllRecipes(request, response) {
  RecipeModel.find({}, (error, recipe) => {
    if (error) {
      response.send(error);
    }
    response.json(recipe);
  });
}
```

We've created a function called `listAllRecipes` which uses the model we just
defined. It calls a `find` on the mongo collection with the first argument set
to `{}` which means find everything!  

It then handles the error scenario by responding with the error if there is one.
If there's no error then it responds with a JSON payload of all the recipes that
are returned from the database.

<a name="create-route"></a>
## Create the Route
The routes will determine what action the REST API takes in response to a client
request.  
The client request will include a path (URI) and a HTTP method (GET, PUT, POST,
DELETE etc). Together the path and method are referred to as an _endpoint_.

We will now add some code to match requests to GET http://localhost:9000/recipes
to the use the `listAllRecipes` function we just wrote in the controller.

Copy the following code into the `recipeRoutes.js` file:

**recipeRoutes.js**
```javaScript
import { listAllRecipes } from './recipeController';

function recipeRoutes(app) {
  app.route('/recipes').get(listAllRecipes)
}

export default recipeRoutes;
```

We're importing `listAllRecipes` that we've just added to the controller module.
We're then creating a function called `recipeRoutes` which will hold all routes
for our REST API.  

Currently there is just one route where `/recipes` defines the path we will go
to in the browser and the `.get()` relates to the fact that it is for `GET`
requests.  

We've now set up a route for `GET` requests to `/recipes` to call our
`listAllRecipes` function.

We export the `recipeRoutes` function so that we can call it from the server.

<a name="update-server"></a>
## Update the server
### Add the updated server code
Copy the following code into the `server.js` file:

**server.js**
```javaScript
import cors from 'cors';
import express from 'express';
import mongoose from 'mongoose';
import recipeModel from './recipeModel';
import recipeRoutes from './recipeRoutes';

const app = express();
const port = 9000;

mongoose.connect('mongodb://localhost/RecipesDB');

app.use(cors());
recipeRoutes(app);
app.listen(port);

console.log(`Recipe RESTful API server started on: ${port}`);
```

### Connect to MongoDB
We're using mongoose again. This time to connect to the MongoDB database. We've
specified `RecipesDB` as the name of the database we want to connect to. This
matches with the name of the database that we imported data into with the import
command earlier:
```javaScript
mongoose.connect('mongodb://localhost/RecipesDB');
```

### CORS
CORS stands for Cross-Origin Resource Sharing. It uses additional HTTP headers
to tell a browser to give a web application permission to access selected
resources from a **different origin** (domain, protocol, port) than its own.  

For security reasons, browsers restrict cross-origin HTTP requests triggered by
scripts. So a web application by default can often only make requests to its own
origin. To extend this, responses from another origin need to include the
correct CORS headers.

The following line enables CORS for all origins and routes:  
```javaScript
app.use(cors());
```

This prevents errors in the browser when any other client applications attempt
to access our REST API. This quickly solves the problem but it is an insecure
approach to use for an application that is deployed publicly.  

More information on how to set up CORS properly using a _whitelist_ can be found
in the [further reading](#further) section.

### Routes
Lastly we've added the `recipeRoutes` to the app to allow us to hook in the code
we just wrote in the routes, controller and model modules.
```javaScript
recipeRoutes(app);
```

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
If we now try accessing the same address as before, http://localhost:9000/recipes
in the browser, you should now see a JSON response listing all recipes in the
MongoDB database.

Success!! We now have a REST API which we will be able to query from other
applications.

<a name="further"></a>
## Further reading
[Best Practice for REST API design](https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9)  
[Tutorial to create a REST API with GET, POST, PUT, DELETE](https://www.codementor.io/olatundegaruba/nodejs-restful-apis-in-10-minutes-q0sgsfhbd)  
[What is MongoDB?](https://www.mongodb.com/what-is-mongodb)  
[How to implement CORS](https://www.npmjs.com/package/cors#usage)
