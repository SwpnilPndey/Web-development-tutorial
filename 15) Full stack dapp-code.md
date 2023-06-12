## We are going to use NextJS for front, hardhat for smart contract and ethers.js for web3 library

1. Install next app : npm create next-app name-of-app

2. It will ask for some questions and our structure will be ready. 

- Tailwind : NO (We will install it separately) 
- App router : NO
- src directory : NO
- Typescript/ ESLint : NO
- Import alias : NO

3. Go inside the project folder and now, we can run our app using npm run dev 

4. Install JS-JSX extension and use rfc for react module skelton

import React from 'react'

export default function check() {
  return (
    <div>check</div>
  )
}


5. There are three folders created : pages, public and styles 

6. Only leave _app.js and index.js in pages folder. Clear everything in index.js. Add default component webpage in this index.js. This file if deleted give error (default page not found).

7. Install hardhat : npm i hardhat and @nomicfoundation/hardhat-toolbox (npm install -D)

8. Initialise hardhat : npx hardhat init

9. Install ethers and web3modal packages : npm i ethers web3modal
(web3modal library provides a unified interface to connect to various wallets)

10. Install tailwindCSS using : npm install -D tailwindcss postcss autoprefixer. 
It may be required to uninstall/ install certain package versions. And then re try installing tailwind packages

11. Initialise tailwindCSS using : npx tailwindcss init -p

12. Put following standard code in tailwind.config.css : 

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
    './app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      backgroundImage: {
        'gradient-radial': 'radial-gradient(var(--tw-gradient-stops))',
        'gradient-conic':
          'conic-gradient(from 180deg at 50% 50%, var(--tw-gradient-stops))',
      },
    },
  },
  plugins: [],
}

13. Goto styles folder and delete Home_modules.css. Now, goto global.css, clear everything and  add following code to be able to add custom classes for our CSS : 
@tailwind base;
@tailwind components;
@tailwind utilities;

14. Now, we can write our contracts in contracts folder

15. We can change the deploy script, hardhat.config.js to deploy our smart contract as per our need :

**hardhat.config.js goes as** : 

require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

const NETWORK_URL = process.env.NETWORK_URL;
const PRIVATE_KEY = process.env.PRIVATE_KEY;
module.exports = {
  solidity: "0.8.18",
  networks: {
    testnet: {
      url: NETWORK_URL,
      accounts: [PRIVATE_KEY],
    },
  },
};

### Obviously we need to install dotenv package and write NETWORK_URL,PRIVATE_KEY and API_KEY in it (taken from Infura/Alchemy Web3 provider)

**deploy.js goes as** :

const hre = require("hardhat");

async function main() {
  const mycontract = await hre.ethers.getContractFactory("mycontract");
  // other constructor variables if needed
  
  const contract = await mycontract.deploy(other constructor variables if needed); //instance of contract
  await contract.deployed();
  console.log("Address of contract:", contract.address);
}
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});



16. Now, we need to create front end react components. For this create a Components folder in root 

17. Also, we create a folder for Context, wherein we will handle all our data from smart contract and manage our connection 

18. Create various components in Component folder using jsx notation after initialising every component using rafce snippet

19. Now goto _app.js file inside pages folder and delete everything and use rafce to get default component : 

import '@/styles/globals.css' //mandatory to include in _app.js
import React from 'react'
import Footer from '../Components/Footer'

const _app = () => {
  return (
    <>
     <Footer/>
     </>
  )
}
export default _app



20. Now, for the case of a single page application, I will have different components of webpage. These will be created separately inside the components folder as different jsx files 

We know the default structure of any component is : 

import statements

const component_name = () => {

  Here the JS functions and contract interactions are handled.

  return (
    <>
     HTML to be rendered by that components inclusive of CSS and JS modules. However the JS functions and objects are written within {..}. For ex :  <form onSubmit={function_name}>
     Inline CSS is written within double {{..}}, however not used much
     </>
  )
}
export default _app


21. So, we will be interacting in the _app.js with the contract and then passing props to the components. 


22. Add following code in _app.js : 

import abi from "./contract/chai.json";
import addresss from "./contract/address.json";
import { useState, useEffect } from "react";
import { ethers } from "ethers";
import Component1 from "./components/Component1";
import Component2 from "./components/Component2";


const _app = () => {

  const [state, setState] = useState({
    provider: null,
    signer: null,
    contract: null,
  });

  const [account, setAccount] = useState("None");

  useEffect(() => {
    const connectWallet = async () => {
      const contractAddress = "address.address";
      const contractABI = abi.abi;
      try {
        const { ethereum } = window;

        if (ethereum) {
          const account = await ethereum.request({
            method: "eth_requestAccounts",
          });

          window.ethereum.on("chainChanged", () => {
            window.location.reload();
          });

          window.ethereum.on("accountsChanged", () => {
            window.location.reload();
          });

          const provider = new ethers.providers.Web3Provider(ethereum);
          const signer = provider.getSigner();
          const contract = new ethers.Contract(
            contractAddress,
            contractABI,
            signer
          );
          setAccount(account);
          setState({ provider, signer, contract });
        } else {
          alert("Please install metamask");
        }
      } catch (error) {
        console.log(error);
      }
    };
    connectWallet();
  }, []);



  return (
    <>
     <Footer state={state}/>
     </>
  )
}
export default _app



23. Notice the <Footer state={state}/>. It is to be passed in every component as a prop


24. Now, in Footer (or other components) add following : 

import { ethers } from "ethers";
import React from 'react'

const Footer = (**{ state }**) => {

 const function_for_HTML_events = async (event) => {
    event.preventDefault();
    const { contract } = state; //we destructure the contract instance from the state
    
    // Handle HTML elements 
    const name = document.querySelector("#name").value;
    const message = document.querySelector("#message").value;
    
    // Execute function of smart contract
    const transaction = await contract.function_of_smart_contract(name, message);
    await transaction.wait();

    // Above syntax is for writing on blockchain. To read from blockchain, simply : 
    // const value = await contract.function_of_smart_contract(arguments if any);
    
  };



  return (
    <>
     HTML elements to execute function on events 
     </>
  )
}
export default Footer




25. This is it. This way we can handle smart contracts with nextJS and make a full stack dapp.