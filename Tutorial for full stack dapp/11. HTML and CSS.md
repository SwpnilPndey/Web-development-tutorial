## What is HTML 

Hypertext means linking text to other files and markup means a set of tags. So, we can write any HTML in a text editor and link files to different texts 

Since everything on a HTML page is a text and each text has a link to some document, we define the texts (contents) inside different tags to identify what this text is linking to.


## HTML tags

identify what the text (content) is about & define its attributes (characteristics of the text)

### Tags come is pair mostly but some tags don't have closing tags like <br />, <hr />, <img />


## HTML attributes 

characteristics of an element (opening tag+content+closing tag). These are placed in the opening tag of element 

It has a name and a value, for example : <p id= "html"> This is HTML tutorial </p>


## Text (content of element) to be used as hyperlink

Anchor tag is specifically used for HTML text to be used as a hyperlink 

<a> Text which acts as hyperlink </a>

## HTML images as individual element: 

<img />, self closing tag is used to add image elements to HTML page 

It has two mandatory attributes : **src and alt**


## HTML audio and video as individual elements : 

We can add audio and video to an HTML page as : 

<audio>Fallback text for old browsers</audio>
<video>Fallback text for old browsers</video>


## HTML lists as individual elements : 

<ul>
<li>Pen</li>
<li>Pencil</li>
</ul>


## HTML tables as individual elements : 

<table>
<tr>
<th>Name</th> 
<th>Age</th>
</tr>
<tr>
<td>Swapnil</td>
<td>30</td>
</tr>
</table>


## HTML forms as individual elements :  

We can create forms for user to enter data which we can store in the database connected to the backend server. 

Inputs fields can be a text, password, email, checkbox button, button, radi button, file upload, search button, date, dropdown etc 

The inputs are taken inside form tag for better handling at backend. Individual labels are put under <label> tag and inputs are taken using input tags, select tags etc.  

<form>
<label>Enter Name : </label>
<input>
<select>
<option>Option 1</option>
<option>Option 2</option>
</select>

### How the element behaves is handled using its attributes 


## Button tag as individual element : 

When a text is to be used as a button (trigger for a JS event), we write the text inside button tag. How the button behaves is handled by its attributes 

<button>Connect Metamask</button>


### These are the major elements which a website can have. However there are various other tags like canvas, main, header, div, p, footer etc. They can be used to add new elements to HTML UI/ UX based on the need. 



## What is CSS 

Cascade styling sheets. Cascading because if there are multiple styles put on an element then the last one prevails 

## Selectors in CSS 

Styling can be applied to all type of elements like text, image, audio, video etc. 

Selectors are used to identify the element to which the styling needs to be applied 

Selectors can be : 

selector {
property:value;
}

There are 7 types of selectors primarily : 

1. Element selector (directly element name) (not to their children automatically)
2. ID selector (#<ID name>)
3. Class selector (.<class name>)
4. Universal  (*)
5. Group selector (combination of above selectors separated by commas)
6. Child selector (parent>child) 
7. Descendant selector (div p) (targets all p elements inside div element)
8. Adjacent sibling (div+p) (just next to it)
9. General sibling (div~p) (all inside div)


### To target a tag having a particular atrribute, 

input[type="reset"] { 
background-color: red;
    font-size: larger;
    color: white;
}


### There are some pseudo class as well like hover, visited, active: 

h1 : hover {
color:black;
}


## Sizes in CSS

- px : pixels
- em, % : relative to font size of parent 
- rem : relative to font size of root element 
- vw : relative to 1% of width of viewport (area of website visible to us)
- vh : relative to 1% of height of viewport 


## Position property in CSS 

**Position** : position can be static, fixed, relative, absolute and sticky

1. Static : elements are positioned just as they are written in HTML, one after other (doc flow)

2. Relative : similar to static. But we can use top, bottom, left and bottom of it which will move the element relative to its static position and move out of the doc flow 
(but using relative overflows elements and is not mostly used)

3. Absolute : doc flow completely ignores this element (the next element moves to the position this element had occupied, although the element content is overlapped to its original position). Now, we can use top, bottom, left and right to this element and it will be positioned w.r.t to its parent element (which is not position : static)

4. Fixed : fixed to the view port. That it will stay at that position even if we scroll (useful for chat boxes)

5. Sticky : It is the combination of relative and fixed. It remains relative till the element reaches the top of viewport after which it remains at same place on view port 


## Display : flex property in CSS 

it makes it easier to layout, align and style elements inside a flex container

### To make simple flexible and responsive parent child CSS : 

<div class="parent">
    <div class="child">
        //element to be in child 1
    </div>
    <div class="child">
        //element to be in child 2
    </div>
    ...
</div>

<style>
.parent {
    display:flex;
    justify-content:space-around;
    flex-wrap:wrap;
    height:auto;
    width:90vw;
}

.child {
    height:200px;
    flex:1 1 200px;
    margin:20px;
}





## CSS Media Queries 

Add responsiveness to the website for styling when certain conditions are true.

@media (max-width:800px) {
p {
//Styling 
}
}


## CSS Transform  

To restructure elements 

- transform: translate(x,y); // move by x and y length
- transform: rotate(-10deg); // rotate by degrees
- transform: scale(1.4, 1.2); // increase/ decrease height and width
- transform: skew(10deg, 5deg); // slanting 



## CSS Transitions 

control the time to transform from one style to other on some event. like when we define hover pseudo class, wee can use this property

transition : 3s;

It can be applied to a particular property too :

transition: width 3s;


## CSS Animations 

animate elements from one frame to another

@keyframes demo { // demo is the name of animation.
            from {
                background-color: red;
            }
            to {
                background-color: blue;
            }
}
 
Another way to use animations is by using % in keyframes : 

@keyframes demo {
            0%{
                background-color: red;
            }
            25%{
                background-color: blue;
            }
            50%{
                background-color: yellow;
            }
            75%{
                background-color: black;
            }
	        100%{
                background-color: white;
            }
}

To identify the animation we assign it with the name, 

div{
animation-name: demo;
animation-duration:5s; // the % values are divided based on this 
animation-iteration-count:infinite; // number of loops of animation
}

