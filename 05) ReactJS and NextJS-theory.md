## React is a front end library where we can divide pages into different components

## Here we make use of JSX files. 

With the help of JSX, we can write HTML codes but in the form very similar to JS

## As we know every components of web page is written as if it ia nodeJS module. for example : 

import React from 'react';

function MyComponent() {
  const element=<h2>We can do this as well</h2>;
  return (
    <div>
      <h1>Hello world</h1>
      <div>{element}</div>
    </div>
  );
}

export default MyComponent;

### We can return only one div. So, if we want multiple lines of code, we need to wrap them inside a div or an empty tag (<>.. </>)



## Very interestingly, we can even define functions inside components and call this as JSX inside the HTML we are going to render

import React from 'react';

function MyComponent() {
 function getUser(user) {
    return user.firstname+" " + user.lastname;
 }
 const myUser= {
    firstname="swapnil",
    lastname="pandey"
 }

  return (
    <div>
    Hello, {getUser(myUser)}
    </div>
  );
}

export default MyComponent;


### We can even have conditional rendering like :

function getUser(user) {
    if(user){
        return <h1> Hello friend</h1>
    }
    else {
        return <h1> Hello stranger</h1>
    }
}



## We can use various inbuilt JSX functions in JS in the HTML element by using JSX i.e using the JSX function/ module/ object of JS inside {..}



## Now, in React we know we can create components : 

import React from 'react'

const compName = () => {
  return (
    <div>
      
    </div>
  )
}

export default compName


### In the main app component which we are rendering, we can import other component and render to the web page : 

**Suppose we create a component called Navbar in Navbar.jsx :**

import React from 'react'

const Navbar = () => {
  return (
    <div>
      Navbar
    </div>
  )
}

export default Navbar


**In the app component I can call the navbar component as :**

import Navbar from '../Components/Navbar'
import React from 'react'

const app = () => {
  return (
    <Navbar/>
  )
}

export default app



## 
