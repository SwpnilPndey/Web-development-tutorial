## Solidity is a High Level Language

Programmers code in High Level Languages like JS, Python, Solidity, Rust etc. Compilers convert the HLL to Low Level code ie. assembly language (byte code). The assembler (virtual machine like EVM) then converts the byte code to machine code


## Why License Identifier at beginning 

Any source code always touches on legal problems with regards to copyright. Therefore, the solidity compiler encourages the use of machine-readable SPDX license identifiers.


## Accessing variables and functions in smart contract from outside

(Importing from other contracts, interfaces, libraries from other files)
import “file with address.sol”;

Then we can : 

- use **inheritance** (modify some functionalities) 
contract newContract is oldContract(constructor arguments in contract1) {...}

- use **new keyword** to create new instance (only use state variables and functionalities of the original contract)
contract1 public instanceInContract2=new contract1(constructor arguments);


### Sometimes, there is one more way the contracts are inherited which have a separate constructor function. It is very complex syntax and is generally avoided. 

contract newContract is oldContract {}
constructor contract1(constructor arguments in contract1) {}

### However, when there is a parent of a parent which has a constructor then such syntax is the only way out.


## Function qualifiers   

function myFunction() public payable view virtual modifiers returns(..) {..} (PPVVMR)


## Payable 	

any function when used to transfer ethers from one address to other (EOA or contract), should include the payable identifier in function declaration to be identified as a function involving transfer of ethers


## Modifiers 

modifier onlySeller() {
require(msg.sender == seller, "Only seller can call this.");
_;
}


## Events in EVM logs

event HighestBidIncreased(address bidder, uint amount);
function bid() public payable {
        ///...
        emit HighestBidIncreased(msg.sender, msg.value);
    }


## Interfaces, abstracts and libraries 

**Libraries** are used to use different type of function declarations 

// Library declaration
library MyLibrary {

  // Library function
  function add(uint256 a, uint256 b) public pure returns (uint256) {
    return a + b;
  }

}

// Contract that uses the library
contract MyContract {

  // Import the library
  using MyLibrary for uint256;

  function test() public view returns (uint256) {
    // Use the library function
    return 10.add(5);
  }

}

**Interface** contracts are used by a project owner to instruct the developers to use specific function names which take specific arguments and have specific qualifiers. 
They only have function declarations and events not implementations nor state variables 

Interfaces are declared as : 

interface IERC20 {
/'/ events and functions declarations
}

Then I can use this interface in other contract as : 

IERC20 public token; 

token=IERC20(_tokenAddress); 

// here _tokenAddress is the address of the token contract which complies to the interface. This way we get a new instance of ERC20 token created at the _tokenAddress. This way we can call the IERC20 functions on the ERC20 token using dot notation. 


**Abstracts** contracts are like interfaces but they can state variables as well. They can be used to give blueprint to developers and collaborators 
Ideally all functions in abstract contracts and interfaces should have virtual keywords. 


## Revert, Assert and Require 

**Revert** is used to revert (cancel) a transaction. It is used inside an IF loop and has a message as argument 
function transfer(address payable recipient, uint amount) public {
  if (amount > balance) {
    revert("NotEnoughFunds");  
}}

**Assert** is used to check and revert without a message. It is used to check internal errors and code errors. 

function divide(uint x, uint y) public pure returns (uint) {
  assert(y != 0);
  return x / y;
}

**Require** is used to check invalid inputs or conditions 

require(condition,”revert message”);


## Using <library> for <data type>

The most common example of this is : **using SafeMath for uint256;** 

When we use this library, we can prevent underflow and overflow errors for uint256. 
It means if we try to store uint256 with value more than 2^256-1, the function will throw error instead of throwing incorrect value


## Data types 

### Address data type : 20 byte value (size of an Ethereum address or contract address)
address data type has method called **balance**
**address payable** data type has methods called **balance and transfer**, used as 
address payable public myAddress;
myAddress.transfer(<value>);


### Enums : create user defined variables for better clarity

contract test {
    enum ActionChoices { GoLeft, GoRight, GoStraight, SitStill }
    ActionChoices choice;
function setGoStraight() public {
        choice = ActionChoices.GoStraight;
    }}

### Array :  T[k] is a fixed size array where T is datatype and k is size. 

Suppose we have  : uint256[10] means 10 rows. Each row is one value of length 256 bits

T[] is dynamic array. Example : string[] means variable rows. However each row has one string

Both type of arrays have method called **.length**

Dynamic array has method called **.push(value)**

### Bytes : bytes32 <variable name> means 32 row sized array of each row having 8 bits 

bytes <variable name> means dynamic size array of each row having 8 bits

**uint8, uint256 (uint) etc are convertible to bytes** using wrapping unsigned integer to bytes type

Same way, **string type is also convertible to bytes** since each character is one byte long

**Bool is also one byte long**, TRUE=0x01 and FALSE=0x00


### 2-D Array : Lets say the array is T[m][n] where T is the type and m is the now of rows and n is the now of rows within each row of the 2-D array 

Therefore, uint[5][7] means there are a total of 5 rows. Each row has one element each. This element is an array of 7 rows and each row has one unsigned integer 


### Struct data type :

struct <name of structure> {
primitive data types; 
}

Then to create a struct variable of above structure, use : 
<name of structure> public <variable name>; 

Struct primitive data types can be accessed using dot notation. 

### Mapping data type : 

mapping(primitive data type=>any data type) <name of mapping variable>;


## Wrapping and unwrapping 

It is the conversions between data types for compatibility 

int a=-20;
uint b=30;
int c=a+int(b); // Since b was of uint type 

### Conversions from address payable to address are allowed directly without any keyword, whereas conversions from address to address payable must be via payable(<address>)

### Contract type can be converted to address type using : address(this) and then to payable as payable(address(this))

### If we transfer ethers to contract in some function using : payable(address(this)).transfer(<value>) then the receive function (or fallback function) is executed along with the current function call


## Structs and Arrays inside functions i.e. created at runtime 

Structs and arrays data types when needed inside functions are declared in different ways. 

### Structs inside functions : 

struct Person {
  string name;
  uint age;
}

function exampleFunction() public {
  Person memory myPerson = Person("Alice", 25); // Person({age:25,name:”Alice”}) is also OK
}


## Arrays inside functions : 

function exampleFunction() public {
  uint[] memory myArray = new uint[](3);
//  
}

However this array is created at runtime


## Storage and memory keyword inside functions 

Memory keyword is used for the variables which are just needed at runtime and are not stored on blockchain. EVM uses some RAM space for these variables. 

Five type of variables use memory keyword : string, bytes, array, struct and mapping 


## Abi.encode.Packed(comma separated data) and keccak256 functions 

These are inbuilt functions in solidity 

The **abi.encodePacked()** function takes any number of arguments of any type, and packs them tightly into a byte array without adding any padding (all types are inherently stream of bits)

**Keccak256** functions takes input of any type (all are inherently stream of bits) and gives a 32 byte unique hash value (not predictable) using PreImage Resistance property 


## Global variables inside function call 

**msg.sender, msg.value and msg.data** (function identifier or data input or any other data send with function call transaction called message)


## Receive and fallback functions 

They are the special functions to handle transactions whose function call does not match any function of the contract. 

Both are specific to the calls from outside from outside so both are of type external

receive() external payable {}

fallback() external {
emit(msg.sender,msg.value);
}


## Using Contract.call inbuilt function to call another contracts function

Although we can call function of other contract using inheritance of creating a new instance of contract and then using its functions but sometimes the contract address is not known at compile time but only at run time. 

Therefore we take the address of the contract as argument of a function and use the .call function to execute the function of the contract whose address was given as argument. 

Other use of this function is that it can be used to catch errors which may occur during calling functions of the contract. 

The syntax is different for two type of functions : 

### When function doesn't return anything but takes argument : 

 (bool success, ) = myContractAddress.call(abi.encodeWithSignature("setData(uint256)", _myData));
require(success, "Call to MyContract failed");

### When function returns a value : 

(bool success, bytes memory data) = myContractAddress.call(abi.encodeWithSignature("getData()"));



## pragma abicoder v2

Above line of code is to be used to use nested arrays in our smart contract. 
