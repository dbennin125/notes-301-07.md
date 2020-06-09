# notes-301-07.md
#### Video
Middleware explained - middleware is any number of functions that are invoked by Express.js routing layer before the final request handler is made.<br> 
Example: before sending some to a route that was requested, you could check for an authorization. Middleware might look like app.use() (example for authorization might look like auth.isAuthenticated())<br>
Make sure to use the "next" parameter (req, res, next) to make sure it will go to the next function.<br>

Sample code :
<code><br>
var express = require('express')<br>
var app = express()

app.use(function (req, res, next) {<br>
  console.log('Time:', Date.now())<br>
  next()<br>
}) </code>
#### Website resources
https://www.restapitutorial.com/httpstatuscodes.html --list of HTTP Status Codes for reference.<br>
https://expressjs.com/en/resources/middleware.html -- Express Middleware modules reference.<br>
https://github.com/visionmedia/supertest -- supertest docs, can be used with express for routes.<br>
https://www.tutorialspoint.com/expressjs/expressjs_middleware.html -- tutorial for Express Middleware<br>
https://expressjs.com/en/guide/routing.html -- how to use Express's routing.<br>


#### Express Routing 
Event driven system<br>
* will look like: app.get('/resource', (req, res) => {})
* works when .get happens on /resource, it will run function

The Request Object<br>

* (req, ...) and can be
    * /parameters 
        * example: app.get('/api/:resource', ...) is req.params.resource
    * Query Strings
        * example: http://server/route?ball=round = req.query.ball (kinda like a google search)<br>

The Response Object
* (..., res) --the other part of (req, res)
* This is the data that is sent back to client.
* Has methods like send() and status() that Express uses to format the output to the browser properly (what we worked on in class today)
* It also sends: Headers, Cookies and Status Codes.

CRUD operations with REST mentioned I've written these before and get them. I get it, we will use these a lot.

#### Server Testing
* Generally, avoid starting the actual server for testing
* Instead, export your server as a module in a library
* Then, you can use <b>SUPERTEST</b> to run your tests and you won't have to use the server.
* That’s one less thing to go wrong (eliminate variables when testing!)

* Additionally, you can wrap superagent in a module (the demo code created an agent.js module that does this)
    * My thoughts: So basically we can do mock tests to make sure the fake calls are working 100% of the time even if the API isn't up and running. You will know that that call will work regardless if the server/API is actually responsive. 
