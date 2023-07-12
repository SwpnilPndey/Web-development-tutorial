## What is rust ?

Rust is a systems programming language that aims to provide safety, concurrency, and performance.

**Concurrency** means ability to utilize system resources efficiently when several parallel tasks are being executed. 

It is designed for building "close to hardware" softwares, including operating systems, device drivers, embedded systems, and other performance-critical software.


## Variables in Rust

Variables are memory locations that store some data 

Here in rust, every variable that you declare is immutable by default

This way Rust guarantees safe concurrency and multi threading. Since all variables (by default) are immutable, you do not need to worry about a thread changing a value unknowingly

Any variable can be made mutable using **mut** keyword

let my_age:i32=31;
let mut my_age:i32=31;


**Every variable should be initialised with some value otherwise compiler throws error**
**If some variable is not to be initialised then its name must begin with an underscore(_)**


### Scope of variable is limited to the block it is declared in 

### Constants variables are to be UPPERCASE only


Just like other languages, the data types are : 

Integers, unsigned integers (i32, u32)
Float (f32)
Boolean(true)
Character (char)


### Arrays and tuple : arrays must be of same type while tuple can have data of different data types 

let my_array:[i32;4]=[1,2,3,4];

let my_tuple=(1,"Swapnil",true,my_array);


### Print in rust (called print line macro)

println!("The age of the person is {}",my_age);

println!("The required array is {:?}",my_array);

println!("First element of tuple is {}",my_tuple.0); // tuple elements are accessed using dot notation

**Here println is called macro and {:?} is called token**




## Functions in Rust 

Any program in Rust starts with the “main function”, and it is necessary to declare the main function to start a program

fn main() {
    ...
    ...
    ...
}

Any function inside main function is declared as : 

fn function_name(x:i32,y:i32)->i32 {
    return (x+y);
}



## Control flow using if else in Rust

if, else, else if are similar to other languages 


## Loop in Rust 

while (condition) {
    execution if true;
}

for i in 1..=10 {
    execution while i lies in range;
}

### Loop is new looping statement but used to continue an iteration till the break condition is satified 

loop {
    statements;
    if (condition){
        break;
    }
}


## Run a rust program 

Cargo is the package manager for rust (like npm)

- Install rustup
- Create a project folder (like truffle) : cargo init <name of project> 
- Write the code in the main.rs file located inside src folder 
- Then run the program using : cargo run

**to run a specific file, use : cargo run --bin <filename without .rs>**

**cargo run -q** is used to simply display the output in terminal




