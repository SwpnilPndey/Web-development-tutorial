## React is a front end library where we can divide pages into different components

## Here we make use of JSX files. 

With the help of JSX, we can write HTML codes but in the form very similar to JS

JavaScript files typically contain code that is meant to be run on the server-side or client-side

JSX files, on the other hand, contain code that is meant to be rendered on the client-side. 

So, JSX has the HTML portions while JS has the code to render these components.

However, JS nowadays is very powerful and can understand JSX code directly. But, for complex UIs, better to use JSX for HTML frontend and JS for rendering and data handling logic



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


### We can do conditional rendering as well

return (
  <div>
  {flag==true ? <Counter /> : <h1>This is not done </h1>}
  </div>
)



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




## **Props** are used to pass data from a parent component to a child component


To pass the props in the previous example, first come to parent component as :

import Navbar from '../Components/Navbar'
import React from 'react'

const app = () => {

  const userInfo={
    firstname="Swapnil",
    lastname="Pandey"
  }

  return (
    <Navbar title={userInfo}/>
  )
}

export default app


Then in the Navbar component, I can take the props as : 

import React from 'react'

const Navbar = (props) => {
  return (
    <div>
      Navbar made by {props.title.firstname} {props.title.lastname}
    </div>
  )
}

export default Navbar

**This way when Navbar is rendered by the app component, it displays the new element**






## **State** and life cycle of components

The value of the variable element which any component is returning, might change with time. But, once rendered, the changed value wont change automatically. For example, we have Date function in {} in JSX code. Thne the time will keep on changing. But, only first time is rendered on frontend. 

So, for this we use a hook called : **useState**

import {useState} from 'react'


To use useState, inside the main component declaration we define, 

const [variable, function to set variable]=useState(initial value of variable state);

Now, we just need to define the set variable function which will take real time values and if the variable value changes, the new value is rendered on the web page 


import React from 'react'
import {useState} from 'react'

const Navbar = (props) => {
  const [mytime,setmytime]=useState(new Date().toString());
  setmytime(new Date().toString());
  return (
    <div>
      Navbar made at {mytime}
    </div>
  )
}

export default Navbar


### Another example will explain it more clearly : 

import React, {useState} from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counter</h1>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  )
}

export default Counter;




## Next is the **useEffect** hook

useEffect hook that allows you to perform side effects like any action that affects something outside of the component, such as fetching data from an API, modifying the DOM, or setting a timer.

The useEffect hook takes two arguments: a callback function and an optional dependency array. 

The callback function is executed after the component is rendered and any time the component updates

The dependency array specifies the state variables that the effect depends on. If it depends on all states then keep it empty array.


useEffect(()=>{
  console.log("This is use effect hook");
},[count]);


### So, the callback in useEffect hook will execute everytime the count state variable changes state

**The useEffect call back runs only when the state variable in dependency array changes** 



## Event handling in React 

Any event like onClick of button can be assigned to a function and this function can be used to set the state of execute useEffect callback, as and whatever we want

That is all the basics of ReactJS