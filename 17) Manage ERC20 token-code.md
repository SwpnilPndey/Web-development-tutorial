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


2. Users can buy the tokens by paying required token fees 

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
contract Invest {
    IERC20 public token;
    address public investor;
    uint public investedAmount;
    uint public tokenPrice;
    constructor (address _token,uint _tokenPrice) {
        token = IERC20(_token);
        tokenPrice=_tokenPrice;
    }

    function invest(address _owner) external payable {
    investor=msg.sender;
    investedAmount=msg.value;
    _tokenAmount=msg.value/tokenPrice;
    token.transferFrom(_owner,investor,_tokenAmount);
    }

} 

## How to buy/ transfer ERC20 tokens in solidity

1. Here Invest smart contract should first be approved by the Token contract to spend the tokens on owner's behalf

2. In Remix, we can directly go to the token contract and approve the vesting contract to spend tokens from the address whose tokens are to be locked

3. For web3.JS/ ethers.JS while using hardhat/ truffle we can create separate instances of the token contract and vesting contract and then use approve function of the token contract from the address of investor and then we can use transferFrom function from the owner address to the vesting contract

4. This way we can transfer ERC20 tokens