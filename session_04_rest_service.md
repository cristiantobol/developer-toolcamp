# Creating a Restful API with Node.js and Express

* [What is a Restful API?](#rest-api)
* [Further reading](#further)

<a name="rest-api"></a>
## What is a Restful API?
For a system to be RESTful it must adhere to the following 6 constraints:
1. **Client–server architecture**  
    Separation of user interface concerns from data storage concerns.
1. **Statelessness**  
    Each request from any client contains all the information necessary to service the request.
1. **Cacheability**  
    Server responses must define themselves as cacheable (or not) to prevent clients from getting stale or inappropriate data in response to further requests.
1. **Layered system**  
    A client cannot tell whether it is connected directly to the end server, or to an intermediary. Intermediary servers may provide load balancing, shared caches and/or enforce security.
1. **Code on demand (optional)**  
    Servers can transfer executable code like Java applets or JavaScript.
1. **Uniform interface**  
    Describes 4 constraints:
    * **Resource identification in requests** individual resources are uniquely identified in requests. Meaning they can be represented differently from how they are stored in a database.
    * **Resource manipulation through representations**
    A client receives enough information about a resource to modify or delete it.
    * **Self-descriptive messages**
    Each response includes enough information for the client to know how to process it. E.g. media type states JSON encoding.
    * **Hypermedia as the engine of application state** The ability to follow links in responses to other actions that are available. Instead of this being hard-coded in the client.

## HTTP Methods
A RESTful API uses HTTP requests to perform CRUD operations on data. CRUD stands for Create, Read, Update and Delete.

POST, GET, PUT and DELETE

**GET** method requests data without producing any side effects.
E.g `GET /companies/3/employees` returns a list of all employees from company 3.

## Express


<a name="further"></a>
## Further reading
https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9
https://www.codementor.io/olatundegaruba/nodejs-restful-apis-in-10-minutes-q0sgsfhbd
