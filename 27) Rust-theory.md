## What is rust ?

Rust is a systems programming language that aims to provide safety, concurrency, and performance.

**Concurrency** means ability to utilize system resources efficiently when several parallel tasks are being executed. 

It is designed for building "close to hardware" softwares, including operating systems, device drivers, embedded systems, and other performance-critical software.


## Basic Data type variables in Rust

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



## Arrays and tuple : arrays must be of same type while tuple can have data of different data types 

let my_array:[i32;4]=[1,2,3,4];

let my_tuple=(1,"Swapnil",true,my_array);



## Print in rust 

println!("The age of the person is {}",my_age);

println!("The required array is {:?}",my_array);

println!("First element of tuple is {}",my_tuple.0); // tuple elements are accessed using dot notation

**Here println is called macro and {:?} is called token**

**{} is called display trait and used to diplay simple values. {:?} is called debug trait and used for complex values like arrays, tuples, structs, enum**

**Prefer using {:?} trait inside loops as well as the value of variables is going to change in every iteration**




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


### Match function :

fn main() {

let myage=31;

match myage {
    age if age > 18 =>println!("Eligible to vote"), // No need to initilise age before (age is expression variable)
    age if age < 18 =>println!("Not eligible"),
    _ => println!("Unknown age"), // _ means everything else
}
}

**However, match is mostly used to match expressions :

let myage=31;

match myage {
    1 => println!("Age is 1"),
    ...
    ..
    .
}



### enum in rust 

enum Direction {
    Left,
    Right
}

fn main() {
    let go = Direction::Left;

    match go {
        Direction::Left=>println!("Go left"),
        Direction::Right=>println!("Go right"),
        _=>println!("Stay"),
    }
}




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



## Expressions in rust 

We can create expression variables in rust as well

let is_greater_than = value > 100;




## Run a rust program 

Cargo is the package manager for rust (like npm)

- Install rustup
- Create a project folder (like truffle) : cargo init <name of project> 
- Write the code in the main.rs file located inside src folder 
- Then run the program using : cargo run

**to run a specific file, use : cargo run --bin <filename without .rs>**

**cargo run -q** is used to simply display the output in terminal






## Struct in rust 

struct Grocery {
    stock:i32,
    price:f64,
}

fn main() {
    let cereal=Grocery {
                        stock:10,
                        price:2.99,
    };

    println!("The stock and price of cereal is {:?},{:?}",cereal.stock,cereal.price);
}




## Ownership and borrowing in rust 

Rust uses ownership model to manage memory 

The function which creates the variable (memory) owns the data. 

If that variable is passed to some other function called in the first function then the ownership is moved to the called function and that function drops the value and memory is freed after it is completely executed 

However if the variable (memory) is borrowed, then the variable can be used multiple times in the original owner function 


struct Mystruct {
    age:i32,
    intitials:char,
}


fn myfunction(person:Mystruct) {
    println!("{:?}",person.age);
}

fn yourfunction(person:Mystruct) {
   println!("{:?}",person.age);
}

fn main() {
    let swapnil=Mystruct {
                        age:31,
                        intitials:'S',
    };
    myfunction(swapnil);
    yourfunction(swapnil);
}


### There is no such implementation issue in basic data types like integer, char, bool etc as they use the copy trait. But, these are an issue in data types like struct, array, strings, tuple, enum etc. 


### So, to resolve this, we use borrowing : use &

struct Mystruct {
    age:i32,
    intitials:char,
}


fn myfunction(person:&Mystruct) {
    println!("{:?}",person.age);
}

fn yourfunction(person:&Mystruct) {
   println!("{:?}",person.age);
}

fn main() {
    let swapnil=Mystruct {
                        age:31,
                        intitials:'S',
    };
    myfunction(&swapnil);
    yourfunction(&swapnil);
}





## impl keyword in rust 

Implement a functionality in enums and structs 

What we can do is that we can include a function which is taking struct as arguments, and include that implementation inside the struct 

struct Mystruct {
    age:i32,
}


fn myfunction(person:Mystruct) {
    println!("{:?}",person.age);
}

fn main() {
    let swapnil=Mystruct {
                        age:31,
                        intitials:'S',
    };
    myfunction(swapnil);
}

Here we can put all implementations involving Mystruct inside the imple block and then we can call that specific function inside impl block 

struct Mystruct {
    age:i32,
}

impl Mystruct {
fn myfunction(&self) { // reference to itself
    println!("{:?}",self.age);
}
}

fn main() {
    let swapnil=Mystruct {
                        age:31,
                        intitials:'S',
    };
    swapnil.myfunction(); // or Mystruct::myfunction(swapnil);
}

### We can create various functions inside impl block to implement some specific functions that take the Mystruct as argument 



### One useful use case of functions inside impl block for structs is when we need various struct variables 

Ideally, when we need to create a struct, what do we do : 

let swapnil=Mystruct {
                        age:31,
                        intitials:'S',
    };

If we have to create multiple struct variables then instead we can create a function called new inside impl in the returning expression of that function, we can return a new struct of Mystruct type 

impl Mystruct {
    fn new(age:i32, initials:char) = > Self {age,initials}
}


fn main() {
    let swapnil=Mystruct::new(31,'S');
    swapnil.myfunction(); // or Mystruct::myfunction(swapnil);
}

**This is a useful way to write rust code**




## Vector data type in rust 

It is similar to dynamic array concept of other languages 

It has various inbuilt implementations like push, pop, len

let mydynamicarray=vec![1,2,3,4];

### To create new empty vector, we can use the new keyword => 

let mut myvector=Vec::new();










 
