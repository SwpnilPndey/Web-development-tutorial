## Variables in JS : 

any type of variable is declared as var, let and const (no separate uint, string)

let is used when one default value is there but its value can be changed 

const used when the value of variable is const 

### However we can declare variables directly as well such as : name =”Swapnil” but it is a wrong practice and can cause unexpected behavior and conflicts as it declares the variable as global variable


## Data Types in JS : 

All data types are declared like : let <variable name> or const <variable name> and there is no need to declare the data type in declaration (JS can understand from the initialized value that what type of data is to be stored in the variable)


### Strings : Written within “ “ or ‘ ‘ are strings

**+** is used for concatenation of strings 

2+”a” will return => 2a


## Arrays : 

let arr = [1,2,3,4,5];

To access one element, we can access arr[2];


Although in JS, we can store different data types in array but it is not a good practice 

let arr =[1,2,”swap”,true];

then arr[3] will return true;


### Nested arrays (matrix) : we can store arrays within arrays

let arr1=[1,2,3,”swap”];
let arr2 = [1,2,3,arr1];

Then, console.log(arr2[3][3]) will return “swap”


### Methods in Array data structure : 

Arrays being a bit complex data type, there are some inbuilt methods (functions in simple language) to access and manipulate arrays 

- arr.push(element);
- arr.pop();
- arr.length
- arr.sort and many more 


- **Map method of arrays** : 

it is used to create a new array using a callback function called on each element in the original array. The argument of map is a function which takes elements of array as argument and returns the corresponding new element (similar to forEach)

let myArray = [1, 2, 3, 4, 5];
let multipliedArray = myArray.map(function(element) {
    return element * 2;
});
console.log(multipliedArray); // [2, 4, 6, 8, 10]


- **Slice and Filter method in** :

const numbers = [1, 2, 3, 4, 5];
const truncatedNumbers = numbers.slice(0, 3); 

const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(function(number) {
  return number % 2 === 0; // condition to be checked on elements 
});


- **Reduce () method** : 

It is a built in function in JS that returns a single value from an array

const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce(function(accumulator, num) {
  return accumulator + num; // accumulator =accumulator+num;
}, 0); // 0 is initial value of accumulator

console.log(sum); // output: 15


## Objects in JS : 

objects in JS are like structs of solidity. It can be used to store datas of different types and each of these data can be accessed using <objectname.element>. 

Here each variable is called property (alias attribute) of the object


let student = {
name:”Swapnil”,
age:23,
class:”Ninth”
};

console.log(student.class) will return Ninth


### To add new element in JS object, simply say : student.city=”Bikaner”;

It will add the new element to the student object.

Even we can change the values of already present elements by redefining them :

student.name=”Anupma” will change the value in name key of student object 

**The keys can even be an array (array inside objects)**

Now the question comes, can we keep objects in arrays. The answer is YES .

### Objects in arrays : 

let arr = [1,
	{
	name:”Swapnil”,
	age:31
	}
]

Now, arr[1].age will return 31

### We can even write functions in objects and access then using object.functionname();

**This is infact most used property in JS, functions inside objects**

However for ease of understanding, these functions inside objects are called **methods of the objects** (variables are properties and functions are methods in OOP, we already know it)


### Inbuilt objects in JS : 

- Date{it has its own methods to display date as per need like Date()}, 
- Math {Math.random()}, 
- Number {Number()} method convert a value to Number type [useful in converting the prompt method output since the output of prompt by default in String] etc.


## Inbuilt functions in JS to change data types

- ### Number() function : 

integers are compatible in JS. However, when we pass integers in some non number format like in a string (const numbr=”12345.34”;) then we need to use Number() function which will return 12345.34 and then we use it in mathematical operations
	
- ### parseInt() and parseFloat() functions 

they also exist to convert other data types (mainly string) to integers and float. One advantage of using parseInt() instead of Number() is that parseInt() can parse initial numbered strings but Number can’t i.e. parseInt(“123swap456”) will return 123 while Number(“123swap456”) returns NaN. 

Another advantage using parseInt() is that we can define the radix of the number as the second argument of parseInt(). parseInt(“10”,2) returns 2 (radix 2 means binary)


## User defined functions in JS : 

those reusable lines of code which run only when we call them. It can take arguments as actual values or variables and will return dynamic values based on the arguments. We can then use these dynamic values to assign them to a new variable of the data type of return of the function. 

let name=function(a,b) {
	alert(“New type of functions”);
	return (a+b);
	}

### Now, if the function is having a return (which in this is true) then we can get the return value in another variable and execute the function as well in single line of code : let c = name(2,3); // function execution goes into call stack

This will first give alert message and then assigns sum of 2 and 3 to variable c, which we can use where ever we want

### However, if we have a function which does not have a direct return which we want to use, then we can only execute the function using : name(a,b); 


## Conditional statements in JS : 

- >, < , === (three equal-tos used in JS for comparison in condition)

3!==2 will return true


## For Each loop : 

it is used in conjugation with arrays. It takes a function as an argument which in itself takes a randomly named variable (mostly named element) as argument whose value will iterate till each element of the array being used 

let arr=[1,2,3,4];

arr.forEach(function(i) {
console.log(i);
})

it is similar to : 

function loop(i) {
console.log(i);
}

arr.forEach(loop);


## Array.from(<DOM array>) 

Sometimes we have an array (like DOM element array) which is not a true JS array. So, forEach is not a method to this array. Hence, we make use of : Array.from(<DOM array>) and then we can use forEach

example : 

let boxes = document.getElementsByClassName("box");

Array.from(boxes).forEach((element) => {...});


### It is to note that .from(<DOM array>) method has nothing to do with the map method. Map method converts a normal array into another array. 



## DOM modifications using JS : 

with DOM handling we can change our HTML and CSS files 

JS can change HTML elements, attributes, CSS styles, can react to HTML events and even create new events in HTML


### document object in JS : 

**document is an object in JS which gives access to all elements of HTML**. 

So whole webpage is a document object for JS

This is why we can access any element in HTML using its ID, class etc. 

document.getElementByID(“<ID of element>”).innerHTML = “<new text in that ID>”

Using above line of code we can change the element

document.getElementByID(“<ID of element>”).innerText = “<new text in that ID>”
// this directly targets the text inside the element and not the whole element

As above line of code is a method (**getElementByID()**), we need to write the above method in a function and then we can assign the function to an HTML event like onClick of button or other 


### If the getElementsByClass method returns more than one element, we can access any element by giving the index of the that class in the class array returned by getElementByClass

So, in JS file we write, 

function buttonClickEvent() {
document.getElementByID(“check”).innerHTML = “<new text in that ID>”;
}

And in HTML file we write,

<div id=”check”> Hello World</div>
<button onclick="buttonClickEvent()”> Change text</button>


## Document object methods in JS : 

There are many methods like getElementByID, getElementsByClass, getElementsByTagName, querySelector, querySelectorAll

Through document.querySelectorAll(<tag name>) or (“.<class name>”) or (“#<ID name>”), we can access multiple elements in array format
 

## Get and Set HTML Attributes in JS : 

We can get value of any attribute of HTML using getAttribute and setAttribute 

<div class=”Great-class”> Learning JS </div>

Then we can access “Great-class” using : 

document.querySelector(“.Great-class”).getAttribute(“class”);

This will return the string with value “Great class”

Clearly we can now set the attribute value as well using setAttribute

document.querySelector(“.Great class”).setAttribute(“class”,”Awesome-class”);


### Create and add HTML element using JS : 

We can create new HTML tags using createElement method on document

let newDiv = document.createElement("div");
newDiv.innerHTML = "This is my new div.";

And then we can place it in DOM based on identification methods like appendChild, insertBefore etc. 


## Change CSS using JS : 

in most websites the **class is used for CSS and ID is used for changing HTML element** 

As we know we can add multiple classes to an element as : 

<div class=”class1 class2 class3” id=”ID”> Wow it works </div>

Now we can define difference styling for these classes in CSS file and then add/ remove the classes (basically doing this removes the CSS attached to the element) 

in JS we write : 

document.querySelector(#ID).classList.remove(“class3”); 

This way the styling defined in CSS under .class3 will not apply to div element 

We also can toggle a style (on and off the application of style on the element)

document.querySelector(#ID).classList.toggle(“class3”);


## DOM events :

We have seen earlier that we can add events to perform some function by defining attributes in button tag itself

<button onclick="Click()">Return</button>  // where Click() function was defined in the linked JS

### There is another standard way developed where we make use of event listener methods of the DOM tags which create events like mouse button clicks, scroll up and down, keyboard keys pressed.

Some common events are : 

click(), mouseover(), mouseout(), keydown() {pressed}, keyup() {released}, submit{form}

So for example we have a button in HTML,

<button> Click me </button>

Then in the JS file,

let buttonInHTML=document.querySelector(“button”); // calling the button object
buttonInHTML.addEventListener(“<event name like click>”, function to execute when click event occurs);


### It is to note that other tags like input also have respective methods when called as a DOM. Like to extract value from an input tag, we can use : 

let inputValue=document.querySelector(“input”).value;


## Window Object : represents current browser window tab

**window.location.href** represents the current URL. 

We can redirect our page to other page by reassigning value to this object property as : 

window.location.href=”www.facebook.com”

This will redirect to the new URL immediately


## Adding delay between execution of function statements :

let Click = function () {
  let x = document.querySelector("#check");
  let message = prompt("Enter your message");
  x.innerHTML = message;

// We want delay here 

  window.location.href = "http://www.youtube.com";

}

Then we use method setTimeout(<function to execute>, <delay before function execution>)

let Click = function () {
  let x = document.querySelector("#check");
  let message = prompt("Enter your message");
  x.innerHTML = message;

let lastfunction= function() {
 window.location.href = "http://www.youtube.com";
}

setTimeout(lastfunction,5000); //function to be executed is used not with the () but just the name
}

### If we want to execute any line of function after a delay or on some condition, we have to write a line of code in another function.

### It is to note that document object, alert method, prompt method, confirm() methods are all part of the window object. However they can be accessed directly and there is no need to use window.document.  or window.prompt. etc 


## Prompt function : 

it gives a prompt popup box to the user to provide a value. The default data type understood is string. So, if we are dealing with numbers, we need to convert data type using inbuilt functions like Number(prompt(“Enter value in numbers”)); 


## Alert : it is used to print a popup to user 


## Object Destructuring in JS 

This concept is very much used in React JS

Suppose I have an object like this : 

const car = { 
name: 'Honda', 
model: 'Civic' 
};

Now, when I have to access its parameters then I use car.name, car.model

But, there is a more efficient way to do it. This is called destructuring

const { name, model } = car; 

Now, we can access name and model directly without using car.name, car.model

Similarly in a function, we can use : 

function check(car) {
console.log(car.name,car.model);
}

Then using check(car) will give the result as Honda, Civic

### However by using destructuring, we can write as : 

function check({name,model}) {
console.log(name,model);
}

check(car);

This will also give same result; 

Basically, function check({name,model}) means destructure the object into its properties named name and model and extract those values. 

So, calling check(car); goes to function definition and tells that the object is car and it has two properties called name and model which you need to call by destructuring


## Template String

Normally how do we write a string in JS 

const name=”Swapnil”;
const age=18;
console.log(“Hello my name is “+name+” and my age is “+age+”years old”);

This is however quite complex 

So, we use a template string which can have variables inside of it 

console.log(`Hello my name is ${name} and my age is ${age-6} years old`); 


## Arrow function 

function add(a,b) {
return (a+b);
}

const add =function(a,b) {
return(a+b);
}

const add=(a,b)=> {
return (a+b);
}

Since, there is only one statement in function, we can write : 

const add = (a,b)=> return(a+b);

For return, there is one more shorthand since it is used so many times 

const add =(a,b)=>(a+b);


All above function declarations are identical. All create functions named add which can take arguments as a and b and return their sum.


## Callback function : 

it is the function which is passed as an argument to another function 

const function1=(sum)=> {
return sum*2;
}

const function2=(num1,num2,<any name to denote callback function, lets say callback>) => {
let sum=num1+num2;
final=callback(sum);
}

function2(2,3,function1);// remember its not function1() as it is being passed as callback function
console.log(final); 

### What it does is, it goes to function2 which makes a local variable sum as 2+3=5, then this sum goes to function as argument and it returns 10.

This concept is used in React. The most commonly used syntax is :

const function2=(num1,num2,function1=(sum)=> {
return sum*2;
}) => {
let sum=num1+num2;
final=callback(sum);
}

Then we can simply call : function2(2,3); // no need of using function declaration again. 

### But there is a problem with callbacks. 

If there are multiple nested callbacks then it creates a lot of confusion (callback hell) and delays since different functions can take different times to execute and hence malfunctions.

So, to get rid of this, **PROMISES are used**


## Promises 

const function1 = (sum) => {
return Promise.resolve(sum*2);
}

const function2 = (num1, num2, callback) => {
let sum = num1 + num2;
callback(sum)
.then((final) => { // final is the return value of callback(sum) if resolved
console.log(final);
})
.catch((error) => {
console.log(error);
});
}

function2(2, 3, function1);


## Async/await 

It is a syntax for working with promises in a more synchronous style. It was introduced in ES2017 

const function1=(sum)=> {
return sum*2;
}

const function2 = async (num1, num2, callback) => {
let sum = num1 + num2;
try {
let result = await callback(sum);
console.log(result);
} catch (error) {
console.log(error);
}
}

function2(2, 3, function1);


### Async/ await are used to handle callback functions so that we can te program execution can move ahead after function2(2,3,function1) since function2 is declared as async function. And this function waits for the function1 to resolve and then is executed. This way the code doesnot stop for function2 (or rather function1) to execute first before any other code can be run. 


## Ternary operator : 

Very commonly used in programming. If is an alternative for if-else

### condition ? value1 : value2;

let message = (number >= 0) ? "The number is positive" : "The number is negative";



## Spread operator : 

It allows you to expand the any element into individual elements

const array1 = [1, 2, 3];
const array2 = [...array1, 4, 5, 6]

const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const mergedObj = { ...obj1, ...obj2 };

const string = 'Hello';
const arrayOfSubstrings = [...string]; // ["H", "e", "l", "l", "o"]