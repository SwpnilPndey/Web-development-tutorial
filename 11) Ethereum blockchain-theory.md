## Web 3.0 : 

read, write and own the data on the internet. 


## Web2 issues : 

data we are reading is authentic or not (fake news)/ product we are buying is the same as we saw on website or not/ the photos we are sharing can someone misuse them


## Web3 solutions : 

the database is tamper proof and decentralized - so authentic and traceable/ we can track the whole cycle of a product/ we can control access to our data through the use of public keys and private keys which help us store our digital assets securely and transfer only when we want and to whom we want


## How is web 3.0 better : 

data security and data sovereignty would improve using blockchain


## Blockchain : 

method to store data more securely 


## How does blockchain provide more data security : 

- Append only (immutable) database (data in form of blocks), so traceability of data is there; 
- Decentralized, so resistant to manipulations because of consensus to add any data;
- Distributed, so tamper proof as everyone has the copy of blockchain;
- User identity is not username and password but cryptographic public key and private key pair;
- Decentralized so no downtime, lesser fees and faster systems


## Block : 

blocks are data structures stored as binary data in the node database. Block has block headers data ie. binary values of hash of previous block, merkle root, timestamp, version of blockchain and transactions data ie. binary values of encrypted transactions 


## Hash of a block : 

hash function of the block header binary data becomes the hash of the block and is stored in the header of next block


## Merkle tree : 

the transactions in a block are stored in a data structure called merkle tree in the form of a parent and two children. The hash of the topmost transaction becomes the merkle root. Change in any transaction = changed merkle root


## Peer to peer network : 

Any node is connected to a subset of nodes to avoid network congestion.  


## Transactions on ethereum : 

- transfer of ethers, 
- tokens from one EOA to another, 
- deploy smart contract, 
- self destroy smart contract, 
- calling a function of smart contract or transfer ethers to it (called message), 
- internal transaction (contract calls another contract, is part of parent transaction), - delegate call, 
- mining reward transaction (coinbase) etc. 

Transaction details like sender receiver address, bytecode, ethers, gas used etc are hashed to form the transaction hash. 


## Transaction verification : 

- user initiates a transaction, 
- transaction goes to mempool (separate data structure on each node) of all nodes, 
- each node validates the transaction (sufficient funds, smart contract rules), 
- miner mines the block based on consensus algorithm, 
- miner sends this block to its peer nodes who validate the block and chain continues.
- After sufficient nodes validate the block and add the block to their version of blockchain, the block is set to be verified and added to the blockchain forever. 
- New version of blockchain is then broadcast to all nodes. 


## Use of cryptography in blockchain : 

- transaction data is hashed to form transactions, 
- transactions are hashed to form merkle tree, 
- block header data is hashed to form block hash. 
- User exists in the form of externally owned accounts addresses and have a cryptographic public private key pair


## Smart contract : 

piece of code which can automatically check the authenticity of a transaction before it is executed like only the contract owner calling a function or sufficient funds being available in the sender's account or any other condition. 


## Smart contract compilation : 

compiler generates two files - bytecode which is deployed by the EVM on the blockchain as part of contract deployment transaction, and ABI which is used by third parties to interact with the smart contract 


## How does EVM execute code if the data is hashed : 

the transaction data is hashed and the hashed value is stored in binary format in blocks. The EVM is able to decode this hash and reach to the original piece of data


## Deployment on blockchain : 

it means that the transaction representing the contract deployment will also include the byte code of the contract which will be hashed and stored in the block forever


## How does the external world interact with the smart contract : 

- Suppose I have a smart contract deployed. 

- The transaction denoting this will store the address of sender, ether transferred along, contract bytecode or any other data like gas limit, gas price, additional input data such as constructor arguments. 

- Now, the miners will check the transaction and the contract bytecode will be stored on that block, along with the state variables initial values. 

- Now, when someone calls any function of this contract, the miners after verification of transaction, execute the function call of the smart contract using the current state (value of state variables) and then update the state variables and the new bytecode ( with new values of state variables) is recorded in the next block miner mines along with the transaction with called the function. 

- When a new user interacts with the blockchain, they will query the latest version of smart contract bytecode (having latest state variables value, called the state of blockchain). And the process is the same as before. 

- To read the bytecode, execute the bytecode and update the bytecode, miner nodes have any software installed on their machines which implements EVM which creates a virtual and separate runtime environment to interact with the blockchain (chain of binary data structures as told before).  


## Geth : 

it is a CLI to interact with the ethereum (means able to talk to the data stored in blocks of blockchain, which may be stored on your machine somewhere but unless you have the right tool, you can’t access it). Geth is a Ethereum client software which includes implementation of EVM in itself.


## Infura : 

there are nodes belonging to infura on the ethereum network. So, we as developers can interact with the ethereum blockchain without being a node. This we can do by interacting with the infura web services which provides developers a range of endpoints. As using the APIs, we are actually sending JSON-RPC requests to the actual ethereum nodes (belonging to infura) who will then upon approval of the API request execute a function of a smart contract and update the state of blockchain (state variables new data) on our behalf. So, infura is not using EVM directly, but the ethereum nodes (belonging to infura) are in actuality using EVM as they are nodes of the blockchain


## JSON -RPC API : 

client sends HTTP request to ethereum network nodes and receive a JSON file in return from the ethereum network 


## Addresses in ethereum : 

they are 20 byte strings. EOA addresses are created by wallets (using public key) while the contract addresses are calculated based on deployer address and the nonce of the transaction and then truncating last 20 bytes. 


## Where are the addresses stored : 

- First let us talk about smart contract addresses. They are stored as part of the transaction data which is used to deploy the contract. 

- Now, for the EOA, whenever a user does a transaction for the first time, the address is verified by cross checking the public key sent along with the transaction and the signed transaction (done by private key). After a transaction is verified, the miner adds the transaction data in the block which includes all data like addresses involved. These addresses are stored in state-trie format which basically means key -value data structure. This address is part of the transaction bytecode which is understood by EVM and extracted by it when the transaction demands it and the transaction has been approved by node. 


## Gas : 

fees in terms of ether which users have to pay to get their transaction validated by nodes


## Gas Price : 

it is the price which the user is ready to pay for each unit gas. This data is part of transaction data 


## Gas Limit : 

it is set by the user initiating a transaction. He approximates the gas consumption in his transaction and sets the gas limit some units higher. It prevents gas wastage 


## Metamask : 

- it is a browser extension which does various tasks :

- Act as digital wallet for cryptos and tokens 

- It has an inbuilt Light ethereum node to talk to ethereum (like getting balances, sending ethers etc.) 

- To interact with the smart contract, it does so via JSON-RPC requests to API services like Infura for mainnet/ testnet or directly to the ganache endpoint in case of ganache


## Ganache : 

it is a local blockchain setup which provides a URL. This URL acts as an endpoint from where we can interact with the ganache blockchain 


## Web3 injector/ Web3 provider : 

Metamask is a web3 injector as it injects a web3 provider in the browser. Now, let us understand what a web3 provider is. 

Web3 provider is that part of software, to which web3.js library in a dapp can talk to and get the data from blockchain using JSON-RPC APIs.

Geth is a local web3 provider since it allows the use of the JSON-RPC API of ethereum network. 

Metamask is a injected web3 provider or browser web3 provider since it allows to use JSON-RPC API of network

Infura is also a web3 provider since it allows to use JSON-RPC API of blockchain



## Advantages with ethereum : 

large community, more dapps, decentralization is valued, Ethereum 2.0 (move to PoS, increase block size)



## Challenges with ethereum : 

high fees, smaller block, smart contract vulnerabilities, no regulation (frauds), volatile prices, limited acceptance in real world, technical complexity



## What is ethereum trilemma : 

decentralization, security and scalability (only two at a time)


## Current solutions to scalability : 

sharding, layer-2 solutions like channels, plasma. roll ups, side chains

![How scalability works](/images/scalability.gif)



## Reentrancy attacks on contracts 

Hackers/hijackers can start a transaction with a smart contract which does some function and also transfers some ethers to some address. Before this transaction gets completed, the hijacker can call the function again and since the last transaction is not completed, a new transaction will be initiated. This way multiple calls can be done which will drain the smart contract. 	

So, to avoid this, one of the ways would be to avoid state changes after transfer, explained below : 

uint amount = shares[msg.sender];
shares[msg.sender] = 0; 
msg.sender.transfer(amount);


This is what we call the CEI withdrawal pattern(Check, Effects and Interaction)

Checks : the require statement

Effects : change in state variables (state of blockchain indirectly)

Interaction : transaction with outer world, like transfers, calls etc. 

How is reentrancy possible : It is interesting to note that if we break the pattern and have the Interaction before Effects, since hacker can run the transaction multiple times before the state change is even recorded (i.e before miners/ other nodes get to know)


