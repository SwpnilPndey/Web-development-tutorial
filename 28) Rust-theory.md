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
        other=>println!("{:?}",other),
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

let mydynamicarray:Vec<i32>=vec![1,2,3,4];

### To create new empty vector, we can use the new keyword => 

let mut myvector=Vec::new();





## String data types in rust 

Strings can be owned or referenced 

To use owned strings, we use String keyword 

to use referenced string, we use &str

**We use String when using in struct and &str when passing as an argument in function**


### To create owned string inside a function, we can use : 

- let owned_string="owned string".to_owned(); // or
- let owned_string2=String::from("owned string");

- "string inside double quotes" is by default as a borrowed string 


So, for example : 

fn printname(name:&str) {
    println!("{:?}",name);
}

fn main() {
    let my_name=String::from("Swapnil");
    printname(&my_name);
    // or we could have directly used : printname("Swapnil");
}


### String slice : 

let somestring=String::from("Swapnil");

let sliced=&somestring[0..=3]; // 0 to 3 where 3 is also included. only .. is used to exclude 3
println!("{:?}",sliced);






## Hashmap type in rust 

It is like mapping of solidity (key value pairs)

use std::collection::HashMap;

fn main() {
    let mut locker=HashMap::new();
    locker.insert(1,"Swapnil");
    locker.insert(2,"Anupma");
    locker.insert(3,"Tasvica");

    println!("{:?}",locker.get(&2)); // borrowing to be used 
}


### to update the values attached to keys, use locker.insert(key, value) // owned values of both key and value 
### to remove a key value pair, locker.use remove(&key)
### to accesss the value, use locker.get(&key)






## Derive keyword in rust 

We can use some added functionality to complex data types like enum, struct etc using derive keyword : 

- Normally we can't print a complete struct using println! macro but with Derive keyword, we can use the Debug trait and print complete struct 

#[derive(Debug)]
struct Mystruct {
    age:i32,
}

fn main() {
    let swapnil=Mystruct {age:32};
    println!("{:?}",swapnil.age);
    println!("{:?}",swapnil);
}

Output : 
32
Mystruct { age: 32 }


### Similarly we can use Clone, Copy traits to create copy of variables when being used by other functions. This avoids the confusion that may occur with borrowing functionality as instead of move, copy is implemented 

### #derive[(Debug, Clone, Copy)]

### Also, if some struct has enums or other structs, then those enums and structs should also follow the same traits other compiler throws errors 

### However, making expensive copies should be avoided to the extent possible 




## Option keyword in Rust 

 It is used for data which may take some value some time or no value sometime. It is mostly used in scenarios where the user may or may not provide a value 

 struct Survey {
    q1:Option<i32>,
    q2:Option<bool>,
 }

 fn main() {
    let response_1=Survey {
                        q1:Some(23),
                        q2:Some(true),
    };

    let response_2=Survey {
                        q1:None,
                        q2:Some(false),
    };
}


### It can used along with Match keyword to check whether users have responded or not




## Using standard libraries in rust 

- Goto terminal and type : rustup doc 

- Click on extensive API documentation

- Use the libraries as directed 


## Using user created libraries in rust 

This is done using crates.io (build by rust community)

So, to use suppose random number generation library, we need to include : rand="0.8.4"or atest version, below the dependencies in Cargo.toml file 

Then in the program, we can use the library as : use rand; (at the top of program)






## How to take inputs from user in rust 

use std::io;

fn main() {
    
    let mut input = String::new();

    
    println!("Enter your name:");
    io::stdin().read_line(&mut input).expect("Failed to read input");

    println!("Hello, {}", input);
}











 
