## What is NodeJS

Node.Js is a runtime environment for JS codes in local computer


## To run a node locally : 

1. Goto terminal 
2. node


## TO run a index.js locally : 

1. Goto terminal 
2. node index.js 


## How to setup a new nodeJS project : 

1. Goto terminal 
2. npm init 
3. Package.json will be created 
4. Install dependencies using : npm i <dependency name> or add in package.json and use npm install


## Difference to browser JS : 

The browser JS (client side application) has access to various objects of webpage like window, DOM, DOM events like onclick() etc. 

NodeJS is a runtime for server side JS code and it doesnot have access to the client side objects. 

**NodeJS is used to create a web server connected to a database**. Webserver handles data request from client side application and gives response accordingly from the database. 


## Modules in nodeJS : 

In node.JS every declaration whether a normal integer variable or string or object or array variable or any function; **everything is a module** 

So, as we know we can define any variable or object or function using the same manner as: 
const/let <name>=<some value or some object or array or function>

**There are different type of modules : file based, built in and third party**


### File based modules : 

modules which are being exported by JS files in the local folder

In JS, we can export and import file based modules as follows : 

So, suppose I have a file named index.js : 

const a=100;
module.exports=a;

And then I create another file named app.js : 

const b=require(“./index”) // no need to write .js 

console.log(b);

It will give output as 100 in console if we use : node .\app.js

So, this way we can use module exports and import (using keyword require) of file based modules 

**Therefore it is a good practice to export only one module from one file and have multiple files for multiple modules**


### Built in modules : 

we can directly import these modules using require. 

const file_system=require(“fs”); // fs stands for file system

Then we can use the methods of the file system module like file_system.readFile() etc. 

**Sometimes we only need some specific method or property of a big module**. 

So, then we use module destructuring : 

const {readFile} = require(“fs”);

And now we can directly use readFile() without using dot notation as fs.readFile()


### Third party modules : 

they can be first installed and then we can import using : 
const {module name}=require(“third party package”); 