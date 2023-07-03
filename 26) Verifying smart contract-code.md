## Deploy the smart contract using hardhat

## In the hardhat.config.js file, add the following lines at the top:

require('@nomiclabs/hardhat-etherscan');
const { etherscanApiKey } = require('./secrets.json');

### Make sure you have an API key from Etherscan. You can obtain one by creating an account on Etherscan and generating an API key.


