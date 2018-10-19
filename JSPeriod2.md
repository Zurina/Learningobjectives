# Period-2 Node.js, Express + JavaScript Backend Testing, NoSQL, MongoDB and Mongoose

- **Why would you consider a Scripting Language as JavaScript as your Backend Platform?**
    
    - I guess it gives a boost in effiency if both the frontend and the backend is coded in the same language. The developers can easily switch from frontend to backend if necessary without any confusion or learning aspect. 
    - Another plus is the fact that javascript is the most popular programming language which makes it very attractive and easy to hire new employees. 
    - Frontend developers and backend developers can also help each other out since it's the same language. 

- **Explain Pros & Cons in using Node.js + Express to implement your Backend compared to a strategy using for example Java/JAX-RS/Tomcat**

    pros 
        
    - Same as above
    - easy to learn
    - Nodejs is javascript, which means it handles reading and manipulating JSON quickly.
    - Nodejs has the event loop, which means when some async task comes in, Node can handle other requests meanwhile the async task returns a response which makes it able to respond quicker and efficient.
    - 

    cons

    - Node is shit at very high big computational tasks because it is single-threaded and will therefor make every other request wait by queueing them. 
    - Java is way better at this since it uses threads and will therefor be able to respond to other requests meanwhile handling the heavy request.

- **Node.js uses a Single Threaded Non-blocking strategy to handle asynchronous task. Explain strategies to implement a Node.js based server architecture that still could take advantage of a multi-core Server.**

    - Use the native cluster from NodeJS: https://nodejs.org/api/cluster.html native cluster
    http://pm2.keymetrics.io/docs/usage/cluster-mode/ pm2
    - It will take advantage of the cores available on the system. Utilizing them. 
    - or using child processes: https://nodejs.org/api/child_process.html

- **Explain briefly how to deploy a Node/Express application including how to solve the following deployment problems:**

    - Ensure that you Node-process restarts after a (potential) exception that closed the application

        - http://pm2.keymetrics.io/docs/usage/cluster-mode/
        - It will handle server crashes or reboots by running a script to recover/restart.
    - Ensure that you Node-process restarts after a server (Ubuntu) restart

        - same as previous one
    - Ensure that you can take advantage of a multi-core system

        - Either using pm2 or native cluster module, which both utilizes the cores available on the system.
    - Ensure that you can run “many” node-applications on a single droplet on the same port (80)

        - I guess pm2 could be used for this, or some sort of loadbalancer

- **Explain the difference between “Developer outputs” and application logging. What’s wrong with console.log(..) statements in our backend-code,**

    - Developer outputs is for developer purposes by making it easier for the developer to understand his mistakes or whatever is going or how far the program got before the program crashed. It could be a certain error/stacktrace, which is only relevant to the developer. Showing the stacktrace in the browser is very insecure since it can contain vulnerable data or information about the system/application.
    - Application logging is for security reasons and to be able to track back in time for some flaw in the system. Or if someone hacks the system, some data about his breach may have been logged.
    - Console.log is only for developer purposes. It serves no function on the server - and the logging from it is not saved anywhere - so it doesnt serve as application logging.

- **Explain, using relevant examples, concepts related to testing a REST-API using Node/JavaScript + relevant packages** 

    - We've used the test library Mocha, the assertion library Chai, and the Nock library for testing the database request. EXAMPLES


- **Explain, using relevant examples, the Express concept; middleware.**

    - Basically middleware are functions that are run for every request send to the server. Another important thing is the the sequence of the middleware function matters. 
    - Middleware functions are functions that have access to the request object (req), the response object (res), and the next middleware function in the application’s request-response cycle. The next middleware function is commonly denoted by a variable named next.
    
    Middleware functions can perform the following tasks:

    - Execute any code.
    - Make changes to the request and the response objects.
    - End the request-response cycle.
    - Call the next middleware function in the stack.

    If the current middleware function does not end the request-response cycle, it must call next() to pass control to the next middleware function. Otherwise, the request will be left hanging.

    An Express application can use the following types of middleware:

    - Application-level middleware
    - Router-level middleware
    - Error-handling middleware
    - Built-in middleware
    - Third-party middleware

    See here for reference: 
    
    https://expressjs.com/en/guide/using-middleware.html

    Examples 

        var express = require('express')
        var app = express()
        var cookieParser = require('cookie-parser')

        // load the cookie-parsing middleware
        app.use(cookieParser())

- **Explain, using relevant examples, how to implement sessions, and the legal implications of doing this.**

    - A middleware could be used to handle sessions. Fx. express-session - see here for reference: https://www.npmjs.com/package/express-session
    - JWT tokens - better for scaling (more than one server - no guarentee that we would end at the same server twice, which means the server wouldnt recognize the session. REST)

    Example 

        app.use(cookieSession({
            name: 'session',
            secret : "I_should_never_be_visible_in_code",
            // Cookie Options
            maxAge: 30 * 60 * 1000 // 30 minutes
        }))
    This is not a very secure session - I reckon this was one of the sessions we "stole" using XSS.

- **Explain (conceptually) how you would handle sessions if you run your app in clusters to solve some of problems related to deployment.**

    - Use JWT tokens (in each request)
    - Send the session with each request
    - Store the session in another DB, which means they wouldnt be affected by server crash or restarts.

- **Compare the express strategy toward (server side) templating with the one you used with Java on second semester.**

    - I used pug, and I found it a bit cleaner and easier to read and maintain than JSP. It all comes down to syntax, because both are just html with embedded javascript/java. although pug does make it a lot cleaner with a new syntax, but is still just html in the end.

- **Demonstrate a simple Server Side Rendering example using a technology of your own choice.**

        router.get("/joke", (req, res) => {
            if(req.url.startsWith('/api/'))
                next()
            if(req.session.agreement === 'on')
                countRouteByName(req, "joke")
            res.render("joke", {
                joke: jokes.getRandomJoke()
        });
})

- **Explain, using relevant examples, your strategy for implementing a REST-API with Node/Express and show how you can "test" all the four CRUD operations programmatically using for example the Request package.**

    - A default express setup can be generated using this: https://expressjs.com/en/starter/generator.html
    - We use the package express to make a REST api, including routes and middlewares

            const express = require("express");

            let app = express();

            // Routes
            var views = require('./routes/views')
            var rest = require('./routes/rest')

            // Middleware
            app.set("view engine", "pug");
            app.set("views", path.join(__dirname, "views"));

            // Use of routes
            app.use('/', views)
            app.use('/api', rest)

            module.exports = app
    
    Testing (using request package example)

        it("add a joke to the store and return the      store", function (done) {
            request(addJoke, function (error, res,body) {
            var addedJoke = body[3];
            expect(addedJoke).to.be.equal("Its better to be late than to arrive ugly");
            //You should also check whether the joke actually was added to the Data-store
            done();
            });
        })
    For other testing, see MiniProject for further reference. 

    https://github.com/Zurina/Hogwarts

- **Explain, using relevant examples, about testing JavaScript code, relevant packages (Mocha etc.) and how to test asynchronous code.**

    - We can use the Mocha testing library
    - The Chai assertion library
    - The Nock library to fake async requests for database etc. 
    - Asynchronous code can be tested using async/await or promises or the done() function in the "it" test.
    See MiniProject for further reference

    https://github.com/Zurina/Hogwarts

- **Explain, using relevant examples, different ways to mock out databases, HTTP-request etc.**

    - Nock

    Mocking these URL/URI, which means we have written our own response, instead of requesting the resource on the internet. Moch has a connection with the http module, which means the fetch knows about the "nocked" URIs.

            const n = nock('https://swapi.co');
            beforeEach(function () {
                n.get('/api/people/1').reply(200, testPerson);
                n.get('/api/starships/3').reply(200, testStarship);
                n.get('/api/planets/2').reply(200, testPlanet);
            });

    - Or instead use a test database which we, using the before hook, wipe the database for data and then push up the test data again, so we always test on the same data. 

## NoSQL, MongoDB and Mongoose
- **Explain, generally, what is meant by a NoSQL database.**

    - It means that you cant query the database with sql. NoSQL are very efficient and speedy, but they lack consistency. Unlike SQL databases which have traded off speed and efficieny with consistency. So they each have their use cases. NoSQL is a lot more free than SQL. They dont use like fixed schemas - data can be stored if different ways, like documents, or key-values etc.

    see here for reference: 
    https://www.infoworld.com/article/3240644/nosql/what-is-nosql-nosql-databases-explained.html

- **Explain Pros & Cons in using a NoSQL database like MongoDB as your data store, compared to a traditional Relational SQL Database like MySQL.**

    - Some explained above
    - SQL requires you to use predefined schemas unlike NoSQL. 
    - NoSQL data can be stored in many ways, unlike SQL requires fixed schemas.
    - SQL databases are vertically scalable, while NoSQL databases are horizontally scalable.  

    see here for more references: https://medium.com/xplenty-blog/the-sql-vs-nosql-difference-mysql-vs-mongodb-32c9980e67b2

- **Explain reasons to add a layer like Mongoose, on top on of a schema-less database like MongoDB**

    - Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It manages relationships between data, provides schema validation, and is used to translate between objects in code and the representation of those objects in MongoDB.
    - A Mongoose model is a wrapper on the Mongoose schema. A Mongoose schema defines the structure of the document, default values, validators, etc., whereas a Mongoose model provides an interface to the database for creating, querying, updating, deleting records, etc.

    see here for more references: https://medium.freecodecamp.org/introduction-to-mongoose-for-mongodb-d2a7aa593c57

- **These two topics will be introduced in period-3**

    - Explain about indexes in MongoDB, how to create them, and demonstrate how you have used them.
    - Explain, using your own code examples, how you have used some of MongoDB's "special" indexes like TTL and 2dsphere

- **Demonstrate, using a REST-API you have designed, how to perform all CRUD operations on a MongoDB**

    - Checkout MiniProject JS
    https://github.com/Zurina/Hogwarts

- **Explain the benefits from using Mongoose, and demonstrate, using your own code, an example involving all CRUD operations**

    - Checkout MiniProject https://github.com/Zurina/Hogwarts
    - Mongoose has strongly types and validators, which gives us more consistent and correct database data. 
    - It makes querying possible. 
    - great article https://www.quora.com/What-is-the-benefit-of-using-Mongoose-over-a-%E2%80%9Ctraditional%E2%80%9D-SQL-schema-design

- **Explain the “6 Rules of Thumb: Your Guide Through the Rainbow” as to how and when you would use normalization vs. denormalization.**

    - Favor embedding unless there is a compelling reason not to
    - The need to access an object on its own, is a compelling reason not to embed it

    - Arrays should not grow without bound. If there are more than a couple of hundred documents on the “many” side, don’t embed them; if there are more than a few thousand documents on the “many” side, don’t use an array of ObjectID references. High-cardinality arrays are a compelling reason not to embed.

    - Don’t be afraid of application-level joins: if you index correctly and use the projection specier (as shown in part 2) then application-level joins are barely more expensive than server-side joins in a relational database.

    - Consider the write/read ratio when denormalizing. A eld that will mostly be read and only seldom updated is a good candidate for denormalization

    - How you eventaully model your data depends – entirely – on your particular application’s data access patterns.

- **Demonstrate, using your own code-samples, decisions you have made regarding → normalization vs denormalization**

        var LocationblogSchema = new Schema({
            info: {type: String, required: true},
            pos: {
                longitude: {type: Number, required: true},
                latitude: {type: Number, required: true}
            },
            // Not embedding, this represents a one to many relationship with the reference on the many side. DENORMALIZING
            author: {type: Schema.Types.ObjectId, ref: 'User', required: true},
            // verify whether unique works this way
            likedBy: [{type: Schema.Types.ObjectId, ref: 'User'}],
            created: {type: Date, default: Date.now}
        })
    Here is an example of DENORMALIZATION. I chose to do this, because it is rational that if you request a locationblog, you would want to know the author of it. And thus I only have to make 1 query instead of 2. 

- **Explain, using a relevant example, a full JavaScript backend including relevant test cases to test the REST-API (not on the production database)**

    - Checkout the MiniProject JS
    https://github.com/Zurina/Hogwarts


