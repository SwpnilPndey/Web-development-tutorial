## Why create a nodeJS server 

to render a HTML page, we need a web server. Even when we use live server extension of VS code, VS code is creating a web server for us. 

Therefore, to render any webpage, we need to create a nodeJS server first and then render our web page on it 

## How to create a web server 

1. Open project folder in VS code

2. Goto terminal and initiate node : **npm init**

3. This will ask a few questions and then create a package.json 

4. Install express dependency as : **npm i express**

5. Make a new folder src in the root

6. Make **server.js** in root folder

6. Make all required html pages inside a **src** folder in root

7. In the server.js, initialise with following code :

const express=require("express");
const path=require("path");
const server=express();
const port=process.env.PORT||3000;

//... middleware and server.get methods (HTML pages to render)

server.listen(port,()=> {
	console.log(`Server running at ${port}`);
});


8. Make public folder in root (parallel to src) and create all required JS, CSS and JSON files (these JSON will act as API endpoints) in this folder


9. We will empower our nodeJS server to render static files in root and public folder : 

server.use(express.static(__dirname));
server.use(express.static(__dirname + '/public'));


10. NodeJS web server by default is not configured to render JS and CSS files on HTTP request. So, we need to use a middleware to render JS and CSS files as well with index.html 

### Although we can avoid this step if we add script and style part of HTML in header and body tag but it is a good practice to keep different parts of code separate 

**So, add following middleware to render JS and CSS files**

server.use((req, res, next) => {
  const ext = req.url.split('.').pop();
  if (ext === 'css') {
    res.set('Content-Type', 'text/css');
  } else if (ext === 'js') {
    res.set('Content-Type', 'application/javascript');
  }
  next();
});


11. Now goto root directory and install nodemon : npm install nodemon

12. Goto package.json and inside the scripts object, write following : 
	
    "scripts": {
    "dev": "nodemon server.js -e js,",
  },


13. Now, we can now run the server using : npm run dev


14. Then based on our design, we can create different routes for different htmls to be rendered to them on GET request

server.get("/",(req,res)=> {
    res.sendFile(path.join(__dirname+"/src/index.html"))
})

server.get("/about",(req,res)=> {
  res.sendFile(path.join(__dirname+"/src/about.html"))
})

### We can use anchor tags in any of the HTMLs to redirect to these routes using href : 
 <a href="/about">About</a>


15. Also, if we need some JSON data (JSON files are in public folder), we can use following code in front end JS (these JS files are although stored in public folder but are linked to HTMLs in src folder). So, using respective JS files we can fetch data from JSON as : 

const variableJSON = await fetch("/myJSON.json");
const variableObj = await variableJSON.json();
// Obviously inside an async function


16. The NodeJS needs to be setup to render this JSON file when HTTP GET request comes to /myJSON.json. This can be achieved using : 

server.get("/myJSON.json", (req, res) => {
  res.sendFile(path.join(__dirname+"/public/myJSON.json"));
});

This way we can get any JSON data stored locally to our front end 


17. This completes the basic methods to setup a nodeJS web server for front end only web application