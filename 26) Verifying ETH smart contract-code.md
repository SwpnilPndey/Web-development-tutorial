## Deploy the smart contract using hardhat

## In the hardhat.config.js file, add the following lines at the top:

require('@nomiclabs/hardhat-etherscan');
const { etherscanApiKey } = require('./secrets.json');

### Make sure you have an API key from Etherscan. You can obtain one by creating an account on Etherscan and generating an API key.


## Create a file named secrets.json in your project directory and add the following content:

{
  "etherscanApiKey": "YOUR_ETHERSCAN_API_KEY"
}

## Compile your contracts using : 

npx hardhat compile

## Next, run the following command to verify the contract :

npx hardhat verify --network mainnet CONTRACT_ADDRESS "Constructor argument 1" "Constructor argument 2" ...

### Hardhat will use the Etherscan plugin to upload the contract source code and verify it on the Etherscan website. It will use the API key provided in the secrets.json file for authentication.