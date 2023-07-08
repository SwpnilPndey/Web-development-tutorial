## Client requirement is to launch his token and after presale (via pinksale), list the token on uniswap. Also, he will ask for a fixed/ flexible percentage of taxes on every trade that happens uniswap. 

This is the the general requirment of any client trying to launch his own token from scratch 


## As a developer, we need to create smart contract with customizable tax on every trade (transfer/ transferFrom) as : 

// SPDX-License-Identifier: MIT
pragma solidity <=0.9.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract Haawks is ERC20, ERC20Burnable {
    using SafeMath for uint256;
    uint256 private tax_rate;
    address private walletForTax;
    constructor(uint taxpercentage,address walletfortax) ERC20("haawks", "hwk") {
        _mint(msg.sender, 10000);
        tax_rate=taxpercentage;
        walletForTax=walletfortax;
    }
    function transfer(address recipient, uint256 amount) public override returns (bool) {
        uint256 taxAmount = amount.mul(tax_rate).div(100);
        uint256 netAmount = amount.sub(taxAmount);

        _transfer(_msgSender(), recipient, netAmount);
        _transfer(_msgSender(), walletForTax, taxAmount);

        return true;
    }

    function transferFrom(address sender, address recipient, uint256 amount) public override returns (bool) {
        uint256 taxAmount = amount.mul(tax_rate).div(100);
        uint256 netAmount = amount.sub(taxAmount);

        _transfer(sender, recipient, netAmount);
        _transfer(sender, walletForTax, taxAmount);

        uint256 allowance = allowance(sender, _msgSender());
        _approve(sender, _msgSender(), allowance.sub(amount, "ERC20: transfer amount exceeds allowance"));

        return true;
    }

    function changeTax(uint newTax) public returns (bool) {
        tax_rate=newTax;
        return true;
    }
}

