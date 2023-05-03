## We are going to use NextJS for front, hardhat for smart contract and ethers.js for web3 library

1. Install next app : npm create next-app ./

2. It will ask for some questions and our structure will be ready. Select No for tailwind CSS as we will install it separately 

3. We can run our app using npm run dev (check in package.json)

4. Install react emmet extension in VS code (to be able to use rafce emmet)

5. In the pages folder created by nextJS, only keep app.js and index.js

6. Make things clean in index.js

7. Install hardhat : npm i hardhat 

8. Initialise hardhat : npx hardhat init. It will ask us to install @nomicfoundation/hardhat-toolbox 

9. Install ethers and web3modal packages : npm i ethers and npm i web3modal

10. Install tailwindCSS using : npm install -D tailwindcss postcss autoprefixer

11. Initialise tailwindCSS using : npx tailwindcss init -p

12. Put following code in tailwind.config.css : 

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

13. Goto global.css and add following commands to be able to add custom classes for our CSS : 
@tailwind base;
@tailwind components;
@tailwind utilities;

14. Now, we can write our contracts in contracts folder

15. We can change the deploy script, hardhat.config.js to deploy our smart contract as per our need 

16. Now, we need to create front end react components. For this create a Components folder in root 

17. Also, we create a folder for Context, wherein we will handle all our data from smart contract and manage our connection 

18. Create various components in Component folder using jsx notation and initialise every component usinf rafce

19. Create index.js inside Components to cumulatively import all components and export them so that we can use them anywhere in the app 

20. Inside index.js, import all other components. Suppose I created two components - Navbar and Footer then inside index.js : 

import Footer from './Footer';
import Navbar from './Navbar';

export {Footer, Navbar}


21. Now goto app.js file inside pages folder : 

import '@/styles/globals.css'

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}

22. Here import the two components exported by index.js of Components and then wrap it inside main app :

import '@/styles/globals.css'

//Internal Import 
import {Navbar,Footer} from '../Components';

export default function App({ Component, pageProps }) {
  return (
    <>
    <Navbar/>
    <Component {...pageProps} />
    <Footer/>
    </>
  );  
}






