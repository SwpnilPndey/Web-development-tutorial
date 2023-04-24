## What is web development : 

- Web development means making webapps (alias interactive websites) which are nothing but interactive interfaces for users using HTML, CSS and JS files.  

- To interact with the webapp, users will use a web browser and enter the unique URL given by the web server which is hosting the webapp we have made. 

- Browser acts as the client-side application that sends HTTP requests to the web server and receives raw bytes from the web server which are converted to tokens and further to nodes. 

- The nodes are arranged in the form of a tree data structure called DOM. Browser then renders each node and displays it into an interactive GUI.

- Users can now interact with the webapp. 

### When we type : http://localhost:3000 on the address bar, we have a local web server running first which will have a host name and a PORT no. assigned to it (VS code live server extension button at the bottom basically runs this local web server and this is why we are able to view our HTML code in the browser at a local host). So, if we don't have the live server extension of VS code, we have to make a local web server first. This we create using Node.JS. 


### Therefore, if we want to host our webapp (let others use it), we must first have a web server. 

This is why when we have to host a webapp with full stack functionality like login authentication, we first create our own server in nodeJS which can host the HTML based webapps. Then we host this full stack app (nodeJS server, HTML webapp) on a cloud based platform like render. Render gives a unique URL for different routes on the nodeJS server. Users can now type this URL in the browser and the nodeJS server responds with the webapp HTML, CSS and JS files which are rendered by the browser into a GUI. 


## What is the role of Web server in a dynamic web app : 

Web server is typically a program (nodeJS or others) which can take HTTP requests from client side web apps and then if they have their own database, respond with the required data in JSON format from its own database or communicate with API web servers which will provide required information if the API key provided by user is correct. 

After the initial HTML is rendered to the client side app, if the user wants some other data or wants to use some service (like searching on the search bar in facebook), clicking on the search button sends a HTTP request from the client side app to the web server. Web server processes the request, communicates with the necessary services and/or databases, and generates a response.

So, when a user searches for something on Facebook, the client-side web app sends an HTTP request to Web Server 1, which then communicates with Web Server 2 (the API server) to perform the search. The API server then sends back the search results to Web Server 1, which displays the results to the user through the client-side web app.



## What are APIs

Talking about API, API is not a database in itself but an access point (URL) from which a webapp can access the database accessible from the API web server

In web development terms, API means a URL which when opened in a browser, displays JSON data. To use this data in our website, we need to use browser libraries like fetch which will send the GET request to this endpoint (URL) and the JSON data can be parsed into the JS object and handled


## What is a front end only app and a full stack app 

There can be two types of front end only apps : 

1. Websites that use dynamic data - data is gone once website is refreshed 
2. Websites that use database data using database linked via a CDN (Content Delivery Network)

### A full stack application means three things : 

1. A front end UI/ UX
2. A backend server to handle HTTP requests from front end 
3. A database connected to the backend server 

**So, although all functionalities can be created via both front end only apps (using CDN) or the full stack apps, but using a full stack gives certain advantages** : 

1. Better data security 
2. Scalability of project 
3. Complex design can be handled well 
