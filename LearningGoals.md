# Period-1 Vanilla JavaScript, es2015/15.., Node.js, Babel + Webpack and TypeScript

## Explain and Reflect:
- **Explain differences between Java and JavaScript. You should include both topics related to the fact that Java is a compiled language and JavaScript a scripted language, and general differences in language features.**

    - JavaScript is dynamicly typed, and is a functional scripting/programming language where you can use a function as a parameter. JavaScript is “the” scripting language to use in web development, where as Java is mostly used for backends, and IoT. Java is statically typed. Java needs to be compiled(to machine lang in the Virtual Machine), where as JavaScript is text based and does not need compilation. Java has block based scoping, where JS har function based scoping.
    
    - Java is a compiled language, meaning java code is first compiled to class files containing byte code which is then executed by the JVM. 
    Javascript is a scripting language and javascript code is executed directly in the browser.
    - Java is a statically typed language, which means the programmer has to specify the type of variables, because the type of the variable is known at compile time. 
    Javascript is dynamically typed, wich means the type-checking is done at runtime.
    - Java is maninly block-scoped, while javascript is mainly function scoped.  
    - Java uses bytecode to be platform independent, while javascript is dependent on the browser supporting it and it's features. 
- **Explain the two strategies for improving JavaScript: ES6 (es2015) + ES7, versus Typescript. What does it require to use these technologies: In our backend with Node and in (many different) Browsers**

    - JavaScript versions are way ahead of the versions that are supported in the browsers. But for the comfort of developers, and to use the new features of ES6+ES7, we can write these in development, then we can transpile the code to an elder version of JS(ES5), so that the elder browsers can run our code as well. Typescript is a superset of JS, that "lays on top" of ES6 and adds even more features, as stricter types, and interfaces, and as with Babel we can use Typescript to transpile the codebase into ES5, once again making til runnable in elder browsers.

    - http://es6-features.org/#ArrayMatching
    - ES6/ES7 adds fx arrow functions which help with the issue of the bind(this) to all methods.
    - It helps destructuring objects and destructuring arrays into usable variables. 
    - It helps with String formatting, var msg = `hey, my name is ${mathæus}` etc
    - Typescript helps writing correct code and ensuring correct types of arguments in methods/constructors

- **Explain generally about node.js, when it “makes sense” and npm, and how it “fits” into the node echo system.**

    - Node.js is a server-side platform, created on the Google Chrome V8 engine. It is a tool that allows us to make applications, not only for browser but also desktop, and other devices. It also allows us to do asynchronous functions in JS, using the event-loop. We also get to use npm witch gives us access to alot of premade JS code/modules. Npm is also a package manager, and holds version control over your added packages.
    
    - Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.
    - Node.js is javascript run on the server, and therefore makes fullstack javascript possible. 
    - npm is a package manager for nodejs packages/modules.
    - npm is very useful at using other peoples code, so you dont have to invent everything yourself. 


- **Explain about the Event Loop in Node.js**

    - JavaScript is a single threaded language, meaning that originally we could not preform async. requests. Thats where we use a web API, supplied by the V8 engine. This allows us to kick our async. functions over in a C++ code that executes them, and returns them when ready. The loop goes as so : Func() enters the Call Stack in JS, if it is a async function, it will be sent to the web API, witch will execute the async code, then it will get sent to the call Queue, where it sits until the CallStack is empty and ready to execute the next task.

    https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/
    - Node.js is an event-based platform. This means that everything that happens in Node is the reaction to an event.
    - There is only one thread that executes JavaScript code and this is the thread where the event loop is running.
    - it has 6 phases: 
        - timers: this phase executes callbacks scheduled by setTimeout() and setInterval().
        - pending callbacks: executes I/O callbacks deferred to the next loop iteration.
        - idle, prepare: only used internally.
        - poll: retrieve new I/O events; execute I/O related
        - callbacks (almost all with the exception of close callbacks, the ones scheduled by timers, and setImmediate()); node will block here when appropriate.
        - check: setImmediate() callbacks are invoked here.
        - close callbacks: some close callbacks, e.g. socket.on('close', ...).

- **Explain (some) of the purposes with the tools Babel and WebPack, using  examples from the exercises**

    - Babel is used when we want to transpile our JS code, into an older version. This is practical, because most modern browsers do not support the newest JS code, and we want our application to run in all browsers, and our development to be with the most modern tech. Webpack (webpack guide), is a bundler or "packaging tool", webpack allows us to compress our codebase to be as small as possible, because then our .js file will be smaller, thus faster to download/upload. The bundler also shortens variablenames and removes all spaces, making the code humanly undreadable, but still understandable for the computer

    https://survivejs.com/webpack/what-is-webpack/
    - Babel makes it possible to write javascript code with ES6/ES7 features even though a browser doesn't support it. Babel will transpile the javascript written to ES5, which is compatible with almost any browser.
    - Webpack is a module bundler. It has an entry point from which it digs through other files and bundles them all together in one file. Webpack can have Rules or Loaders which it can match the files' content to fx Babel-loader or CSS-loader. 

    - example: 

            const path = require('path');

            module.exports = {
            entry: './src/index.js',
            devtool: 'inline-source-map',
            devServer: {
                    contentBase: './dist'
            },
            output: {
                filename: 'main.js',
                path: path.resolve(__dirname, 'dist')
            },
            module: {
                    rules: [
                    {
                        test: /\.css$/,
                        use: [
                        'style-loader',
                        'css-loader'
                        ]
                    },
                    {
                        test: /\.(png|svg|jpg|gif)$/,
                        use: [
                            'file-loader'
                            ]
                    },
                    {
                        test: /\.js$/,
                        exclude: /(node_modules|bower_components)/,
                        use: {
                        loader: 'babel-loader',
                        options: {
                            presets: ['@babel/preset-env']
                        }
                        }
                    }
                    ]
                }
            };   

- **Explain the purpose of “use strict” and Linters, exemplified with ESLint** 

    - Linting is the process of checking the source code for Programmatic as well as Stylistic errors. This is most helpful in identifying some common and uncommon mistakes that are made during coding. ESLint, helps developers, when coding by showing typing mistakes, and scoping errors and such, before runtime, and Throw them as errors or underline errors with red. This helps you to remember to define variables, and not trying to do things that are not possible, as setting a variable that is readonly to a new value. It also helps you to not use the reserved keywords of JS as variable names and such.

    - A strict mode directive is a "use strict" literal at the beginning of a script or function body. It enables strict mode semantics.
    
            function foo() {
                "use strict";
                // strict mode
            }

            function foo2() {
                // not strict mode
            };

            (function() {
                "use strict";
                function bar() {
                    // strict mode
                }
            }());
    - Eslint is a spellchecker or syntax checker. 
        - Linters are excellent tools for finding certain classes  of bugs
            - Such as those related to variable scope.
            - Assignment to undeclared variables
            - Use of undefined variables are examples of errors that are detectable at lint time.

## Explain using sufficient code examples the following features in JavaScript. 

- **Variable/function-Hoisting**
    - hoisting means all "var x;" i lifted to the top of the script.
    - All functions with this syntax - function hello() {} are also hoisted to the top of the script.
            
            x = 5; // Assign 5 to x

            elem = document.getElementById("demo"); // Find an element 
            elem.innerHTML = x;                     // Display x in the element

            var x; // Declare x

            hello()
            hello2() // hello2 is not a function
            only var hello2; is hoisted

            function hello() {
                console.log("Hello world!") hoisted to the top
            }

            var hello2 = () {
                console.log("Hello world again!")
            }

- **This in JavaScript and how it differs from what we know from Java/.net.**

    - This mainly points to the global object. When making objects/classes this points to that class. 
    If a property function of a class takes a callback, that callback has to be binded to the object's "this" or using a arrow function.
    Lexical scoping is about inner functions scope is to it's parent functions scope. Which means arrow functions work in classes/object. Although not here:

            foo.method = function(name, cb){
            this[name] = cb;
            };
            
            foo.method("bar", () => {
            // not what you expected, maybe?
            console.log(this.test); Points to window object (lexical)
            });
            Parent scope of above is global I guess.
    

- **Function Closures and the JavaScript Module Pattern**

    - Javascript closures is Javascript's way of making private variables. You call a function that returns a function/object with scope to the parent/called function. Hence the return function/object is the only one having access to the parent function. Javascript closures are essentially just functions/objects having access to the parent function's scope.
            
            var makeCounter = function() {
                var counter = 0;
                return {
                    addOne: function() {
                        counter++
                    }
                    getCounter: function() {
                        return counter
                    }
                }
            }
    - Javascript module pattern is about encapsulating a piece of code. It can be used to hiding away implementation, and only reveal what you need to via certain methods and variables (private methods/variables - closures). The module pattern makes it easier to test the code, since the code inside the pattern is independent from other code. It is also great for reuseability, just export it. 
    You can say that the module pattern makes use of closures. 

            var Module = (function() {
                    // Following function is private, but can be accessed by the public functions
                function privateFunc() { ... };
                    // Return an object that is assigned to Module
                return {
                    publicFunc: function() {
                        privateFunc(); // publicFunc has direct access to privateFunc
                    }
                };
            }());
- **Immediately-Invoked Function Expressions (IIFE)**

    - IIFE can prevent function hoisting
            
            var count = (function() {
                return 2
            })())
    - This function is immediatly called. 
- **JavaScripts Prototype**

    - Prototyping in javascript can be used to apply new variables or methods to object constructors.
    - Prototyping can also be use for inheritance

            ShowDog.prototype = new Dog(); // Our ShowDog instances inherits from ShowDog.prototype which inherits from Dog.prototype, Chaining.
- **User defined Callback Functions (This can both be synchronous callbacks or async)**

    - synchronous callback

            var names = ['Lars', 'Jan', 'Peter', 'Bo', 'Frederik']

            function myFilterCallback(name) {
                return name.length >= 3;
            }

            function myFilter(arr, callback) {
                let filteredArray = []
                for(let idx in arr) {
                    if(callback(arr[idx])) {
                        filteredArray.push(arr[idx]);
                    }
                }
                return filteredArray;
            }
            console.log(names.myFilter(myFilterCallback));

    - You can also make callbacks to fetch requests or promises:

            fetch('Someapi.com')
            .then(callback)

            callback(response) {
                return response.json..
            }

- **Explain the methods map, filter and reduce**   

    - map is called upon an array and makes an operation on each element of it and returns a new array with all modified elements of same size.
    - filter is called upon an array and checks each element for a specified condition and returns a new array with a size of all elements that passed the condition.
    - The reduce() method executes a reducer function (that you provide) on each element of the array resulting in a single output value. Can be a number or object..
- **Provide examples of user defined reusable modules implemented in Node.js**

    - This could for example be the built-in HTTP Module from node. The example also includes a self made module. 

            var http = require('http');
            var dt = require('./myfirstmodule');

            http.createServer(function (req, res) {
                res.writeHead(200, {'Content-Type': 'text/html'});
                res.write("The date and time are currently: " + dt.myDateTime());
                res.end();
            }).listen(8080);
## ES6-7 and TypeScript
- **Provide examples and explain the es2015 features: let, arrow functions, this, rest parameters, de-structuring assignments, maps/sets etc.**

    - 'let' uses block-scoping while 'var' uses function-scoping.

            let callbacks = [] // LET
            for (let i = 0; i <= 2; i++) {
                callbacks[i] = function () { return i * 2 } 
            }
            console.log(callbacks[0]() === 0) true
            console.log(callbacks[1]() === 2) true
            console.log(callbacks[2]() === 4) true

            let callbacks = [] // VAR
            for (var i = 0; i <= 2; i++) {
                callbacks[i] = function () { return i * 2 } 
            }
            console.log(callbacks[0]() === 0) false
            console.log(callbacks[1]() === 2) false
            console.log(callbacks[2]() === 4) false

    - arrow functions has an implicit bind to this to the outer scope/parent scope (lexical scoping). And is also syntactic sugar making it quicker to write functions.
    - rest parameters works like this: 
    everything after a and b is put into an array, which also makes the function more generic

            function myFun(a, b, ...manyMoreArgs) {
                console.log("a", a); 
                console.log("b", b);
                console.log("manyMoreArgs", manyMoreArgs); 
            }

            myFun("one", "two", "three", "four", "five", "six");

            // Console Output:
            // a, one
            // b, two
            // manyMoreArgs, [three, four, five, six]
    - destructuring assignments

            [fName, lName] = ["Wonnegut", "Kurt"]

            let obj = { first: 'Jane', last: 'Doe' };
            let { first } = obj;
    - Map

            > let map = new Map();

            > map.set('foo', 123);
            > map.get('foo')
            123

            > map.has('foo')
            true
            > map.delete('foo')
            true
            > map.has('foo')
            false
    - Set (allows no duplicates)

            > let set = new Set();
            > set.add('red')

            > set.has('red')
            true
            > set.delete('red')
            true
            > set.has('red')
            false
- **Explain and demonstrate how es2015 supports modules (import and export) similar to what is offered by NodeJS.**
    - ES6 (es2015)

            //------ lib.js ------
            export const sqrt = Math.sqrt;
            export function square(x) {
                return x * x;
            }
            export function diag(x, y) {
                return sqrt(square(x) + square(y));
            }
            ----------
            could also have been exported like this:
            module.exports = {
                sqrt: sqrt,
                square: square,
                diag: diag,
            };
            OLDSCHOOL
            and then imported like this: 
            var square = require('lib').square;
            var diag = require('lib').diag;
            ----------

            //------ main.js ------
            NEW SCHOOL
            import { square, diag } from 'lib';
            console.log(square(11)); // 121
            console.log(diag(4, 3)); // 5
- **Provide an example of ES6 inheritance and reflect over the differences between Inheritance in Java and in ES6.**

    - Javascript classes can only have 1 constructor, unlike in Java multiple constructors are possible. 

            class Vehicle {
    
            constructor (name, type) {
                this.name = name;
                this.type = type;
            }
            
            getName () {
                return this.name;
            }
            
            getType () {
                return this.type;
            }
            
            }
            class Car extends Vehicle {
            
            constructor (name) {
                super(name, 'car');
            }
            
            getName () {
                return 'It is a car: ' + super.getName();
            }
            
            }
            let car = new Car('Tesla');
            console.log(car.getName()); // It is a car: Tesla
            console.log(car.getType()); // car

- **Provide examples with es6, running in a browser, using Babel and Webpack**

    - Well. Babel converts ES6/ES7 to ES5, and this convertion can be inserted as a rule in Webpacks config file. Examples??

            var myfunction = (firstname, lastname) => {
                [fname, lname] = [firstname, lastname]
                console.log(fname, lname);
            }

            WILL TRANSPILE TO THIS (es6 -> es5)

            var myfunction = function myfunction(firstname, lastname) {
                fname = firstname;
                lname = lastname;
                console.log(fname, lname);
            };

- **Provide an number of examples to demonstrate the benefits of using TypeScript, including, types, interfaces, classes and generics**

    - makes sure the greeter function takes an argument containing the inner structure of the interface Person.

            function printType<T>(input: any): void {
                console.log(input.constructor.name)
            }

            function printTypes<T, K, Q>(a: T, b: K, c: Q): any[any] {
                return [a.constructor.name, b.constructor.name, c.constructor.name]
            }

            function reverseArr<T>(arr: T[]): T[] {
                return arr.reverse()
            }

            // class with generic value

            class DataHolder<T> { 
                _value: T
                constructor(value: T) {
                    this._value = value
                }
                getValue(): T {
                    return this._value
                }
                setValue(value: T): void {
                    this._value = value
                }
            }

            // Interface Owner

            interface Owner {
                owner: String;
            }

            function printOwner(owner: Owner): void { // requires the argument to have a key/value pair with key of owner, and value of string.
                console.log(owner)
            }

            let owner = {
                owner: "hey",
                name: "lut"
            }
            let owner2 = { // wont work, has to have owner property
                name: "lut"
            }

            printOwner(owner)

            printType<String>("PUTA") // Prints String
            console.log(printTypes<String, Date, Number>("Hello", new Date(), 13));
            console.log(reverseArr<string>(["a","b","c"]));
            console.log(reverseArr<number>([1,2,3]));
            console.log(reverseArr<boolean>([true,true,false]));
            // console.log(reverseArr<number>(["a","b","c"])); fails 

            let d = new DataHolder<string>("Hello");
            console.log(d.getValue());
            d.setValue("World");
            console.log(d.getValue());

            let d2 = new DataHolder<number>(123);
            console.log(d2.getValue());
            d2.setValue(500);
            console.log(d2.getValue());


## Callbacks, Promises and async/await

- **Explain about promises in ES-6 including, the problems they solve, a quick explanation of the Promise API and:**

    - A promise can be in one of 3 states:

        - Pending - the promise’s outcome hasn’t yet been determined, because the asynchronous operation that will produce its result hasn’t completed yet.
        - Fulfilled - the asynchronous operation has completed, and the promise has a value.
        - Rejected - the asynchronous operation failed, and the promise will never be fulfilled. In the rejected state, a promise has a reason that indicates why the operation failed.

                var p = new Promise(function(resolve, reject) {  
                if (/* condition */) {
                    resolve(/* value */);  // fulfilled successfully
                }
                else {
                    reject(/* reason */);  // error, rejected
                }
                });
- **Example(s) that demonstrate how to avoid the callback hell  (“Pyramid of Doom")**

    - Avoid it by having additional 'then's, or by using the await keyword. too many 'then's can make await useful. Await is using promises under the hood.

            This could be an example of callback hell

                    doSomething(param1, param2, function(err, paramx){
                        doMore(paramx, function(err, result){
                            insertRow(result, function(err){
                                yetAnotherOperation(someparameter,  function(s){
                                    somethingElse(function(x){
                                    });
                                });
                            });
                        });
                    });

            -------------------------------------------------

            function getPlanetforFirstSpeciesInFirstMovieForPerson(id) {
            var starwars = {}
            fetchHelper('https://swapi.co/api/people/' + id)
            .then(data => {
                starwars['Name'] = data.name
                fetchHelper(data.films[0])
                .then(data => {
                    starwars['First film'] = data.title
                    fetchHelper(data.species[0])
                    .then(data => {
                        starwars['First species'] = data.name
                        fetchHelper(data.homeworld)
                        .then(data => {
                            starwars['Homeworld for specie'] = data.name
                            console.log(starwars)
                        })
                        .catch(error => console.log('Something went wrong... ' + error))
                    })
                })
            });
            }

            // USING AWAIT

            async function getPlanetforFirstSpeciesInFirstMovieForPersonAsyncWithAwait(id) {
                try {
                const n = await fetch(URL + id).then(res => res.json());
                const f = await fetch(n.films[0]).then(res => res.json());
                const s = await fetch(f.species[0]).then(res => res.json());
                const p = await fetch(s.homeworld).then(res => res.json());
                return "Name: " + n.name + ", Title: " + f.title + ", Specie: " + s.name + ", Planet: " + p.name;
                }
                catch (err) {
                console.log(err);
                }
            }

- **Example(s) that demonstrate how to execute asynchronous (promise-based) code in serial or parallel**

    - Making promise-based code serial would require you to use 'then's . new Promise(resolve, reject).then().then() ->
    sequantial. And here every promise would have to wait for the previous one.
    - making it parralel on the other hand would make each promise independent. Here is an example:

            let pf = function(msg) {
                return new Promise((resolve, reject)=> {
                    var ok = true;
                    if (ok) {
                        resolve(msg.toUpperCase());
                    }
                    else {
                        reject("UPPPPs");
                    }
                });
            };
 

            let promisesQuick = [pf.pfQuick('Hello1'),
            pf.pfQuick('Hello2'),
            pf.pfQuick('Hello3')
            ]
            Promise.all(promisesQuick).then(data => console.log("Quick version: " + data.join(', ')));

        Here Promise.all takes an array of promises and waits for them all to resolve/reject. And hereby makes the three promises parralel instead of sequantial. This is of course only a good thing if the promises dont rely on each other. 


        

- **Example(s) that demonstrate how to implement our own promise-solutions.**

    - The below example has a settimeout to image a async call.

            let promiseFactory = function(msg,delay) {
                return new Promise((resolve, reject)=> {
                    setTimeout(()=> { 
                        var ok = true; 
                        if (ok) {
                        resolve(msg.toUpperCase());
                        }
                        else {
                        reject("UPPPPs");
                        }
                    }, delay);
                });
            };
            let operation = promiseFactory("Hello", 1000)
            operation.then(res => dosomething())
- **Example(s) that demonstrate error handling with promises**

    - The above example shows that 'reject' can handle error.
    It could also take a 'new Error("Error)' as a argument. Which we then would catch by: function(promiseblah).then().catch

## Explain about JavaScripts async/await, how it relates to promises and reasons to use it compared to the plain promise API.

- **Provide examples to demonstrate** 

        async function printNames() {
            console.log("Before");
            const person1 = await fetchPerson(URL+1);
            const person2 = await fetchPerson(URL+2);
            console.log(person1.name);
            console.log(person2.name)
            console.log("After all"); 
        }
- **Why this often is the preferred way of handling promises**

    - the await keyword makes promise code easier to maintain/handle especially if you have async requests dependent on each other. 

            async function getPlanetforFirstSpeciesInFirstMovieForPersonAsyncWithAwait(id) {
                try {
                    const n = await fetch(URL + id).then(res => res.json());
                    const f = await fetch(n.films[0]).then(res => res.json());
                    const s = await fetch(f.species[0]).then(res => res.json());
                    const p = await fetch(s.homeworld).then(res => res.json());
                    return "Name: " + n.name + ", Title: " + f.title + ", Specie: " + s.name + ", Planet: " + p.name;
                }
                catch (err) {
                    console.log(err);
                }
  }
- **Error handling with async/await**

    - you can use traditional try/catch
    
            async function(request, response, next) {
                try {
                    await validate();
                } catch (error) {
                    return response.status(400).send(error);
                }

                try {
                    const result = await doRealWork();
                    return response.send(result);
                } catch (error) {
                    return next(error);
                }
                }

                Handling the same code with promises: Much more complex..

                function(request, response, next) {
                    return validate()
                        .then(() => true)
                        .catch((error) => {
                        response.status(400).send(error);
                        return false;
                        })
                        .then((validationSuccess) => {
                        if (!validationSuccess) {
                            return;
                        }
                        return doRealWork()
                            .then((result) => response.send(result));
                        })
                        .catch(next);
                    }
- **Serial or parallel execution with async/await.**

        async function serial(count) {
        swappiPeople = [];
        for (let i = 1; i < count; i++) {
            swappiPeople.push(
            //Observe the await 
            await fetch("https://swapi.co/api/people/" + i)
                .then(res => { return res.json() }));
        }
        console.log(swappiPeople.map(p=>p.name).join(", "));
        }
        async function parallel(count) {
        swappiPeople = [];
        for (let i = 1; i < count; i++) {
            swappiPeople.push(
            //Observe no await
            fetch("https://swapi.co/api/people/" + i)
                .then(res => { return res.json() }));
        }
        const allEntries = await Promise.all(swappiPeople);
        console.log(allEntries.map(p=>p.name).join(", "));  
        
        }
        //Time each of the two strategies
        //serial(15); SLOW
        parallel(15); // FAST





