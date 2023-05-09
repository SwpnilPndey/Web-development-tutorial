## What is a vesting/locking contract?

When investors invest money in a company then company doesnot release tokens immediately but rather releases gradually, as per a vesting schedule

Investors typically use a lock function to lock their tokens in the vesting contract and after the lock period is over, they can withdraw their tokens if they want or keep them invested if they want to earn interests on it.

This is generally done so that investors donot sell all their tokens immediately after ICO and hurt other investors and destabilize the market caused by inflation.


## Process to lock and withdraw tokens 

1. Owner of the company mints 10,000 tokens to its address (lets say ERC20 tokens) with a name and symbol  

// SPDX-License-Identifier: MIT
pragma solidity <=0.9.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";

contract Haawks is ERC20, ERC20Burnable {
    constructor() ERC20("name", "symbol") {
        _mint(msg.sender, 10000*10**(decimals()));
    }
}


2. Same company owner address or some other address (consultant) creates a vesting contract which use the instance of the token 

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
contract vesting {
    IERC20 public token;
    constructor (address _token) {
        token = IERC20(_token);
    }
}  


3. Now we add two functions for locking and withdrawing tokens for the investor to use

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
contract vesting {
    IERC20 public token;
    address public investor;
    uint public investedAmount;
    constructor (address _token) {
        token = IERC20(_token);
    }

    function lock(address _owner,uint _amount) external {
    investor=msg.sender;
    investedAmount=_amount;
    token.transferFrom(_owner, address(this),_amount);
    }

    function withdraw() external {
        token.transfer(investor,investedAmount);
    }
}   


4. We deploy this contract and then use the TOKEN contract to approve the vesting smart contract to be able to lock tokens from owner account into itself on behalf of an investor and then after lock time is over, to be able to transfer those tokens to the investors.

It means we use the approve function in TOKEN contract for the vesting contract address with the allowance equal to the amount of tokens which can be locked overall by all investors 


5. Then we can see the lock function : 

function lock(address _owner,uint _amount) external {
    investor=msg.sender;
    investedAmount=_amount;
    token.transferFrom(_owner, address(this),_amount);
}

Investor uses this function and enters the address of token owner and the amount of tokens he wants to lock. Then token.transferFrom function transfers those tokens from owner contract to the vesting contract. 

However, in real case, the investor will not enter the amount of tokens he wants to lock but rather based on the amount of ether he has transferred, the equivalent amount of tokens will be calculated and those amount of tokens will be locked in the smart contract.


6. And then later we can have the withdraw function as : 

function withdraw() external {
        token.transfer(investor,investedAmount);
}

This function will also be used by the investor to withdraw tokens. Based on whether lock time is over and the amount the investor is withdrawing is less or equal to the token percentage unlocked as per vesting schedule, the investor can withdraw some or all tokens which belong to him. 

This is what a simple vesting contract looks like. However many added functionalities can be added as per need.