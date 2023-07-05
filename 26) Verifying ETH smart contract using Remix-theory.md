## Using Remix plugin 

- Deploy the smart contract from remix (Injected web3)

- Register on Etherscan 

- Create an API on etherscan

- Come to Remix and activate CONTRACT VERIFICATION - ETHERSCAN plugin 

- In the settings, enter API key and save 

- In the home window of Etherscan plugin, enter the contract details (constructor arguments and contract address)\

- Click on verify at the bottom 



## Using Etherscan Verify and publish

- Go to contract on etherscan

- Click on Verify and publish

- Select single file in dropdown if openzeppelin library is there 

- Go to Remix IDE, right click on the deployed contract file and select flatten

- Copy the flattened (expanded contract) contract to Etherscan

- Mostly the Constructor ABI section will have automatic values

- If automatic values dont fill in, go to : https://abi.hashex.org/ and copy the ABI code to Etherscan 

- Click on Verify




## Using hardhat

- Deploy the smart contract using hardhat

- In the hardhat.config.js file, add the following lines at the top:

require('@nomiclabs/hardhat-etherscan');
const { etherscanApiKey } = require('./secrets.json');

### Make sure you have an API key from Etherscan. You can obtain one by creating an account on Etherscan and generating an API key.


- Create a file named secrets.json in your project directory and add the following content:

{
  "etherscanApiKey": "YOUR_ETHERSCAN_API_KEY"
}

- Compile your contracts using : 

npx hardhat compile

- Next, run the following command to verify the contract :

npx hardhat verify --network mainnet CONTRACT_ADDRESS "Constructor argument 1" "Constructor argument 2" ...

### Hardhat will use the Etherscan plugin to upload the contract source code and verify it on the Etherscan website. It will use the API key provided in the secrets.json file for authentication.

