## Why interoperatibility is needed in blockchains ?

It is because none of the blockchains have all the features as per the need of the user. 

## Example ? 

If you have a ERC20 token and you want to convert it to an Solana token, you would typically need to go through a token bridge.

This is a valid argument as ERC20 token on Ethereum Blockchain is nothing but a representation of some real investment (ether, USDT). Similar is the case of Solana token. 

So, converting means the base investment should be shifted to other network, obviously with a small amount of fees. 


## How is it achieved ?

1. First let us assume we select a **token bridge contract** on ethereum 

    This contract handles the token locking and initiate the cross-chain transfer process. This smart contract is responsible for accepting token deposits, verifying transactions, and coordinating with the Solana network.

    So, suppose I need to transfer 100 ERC20 tokens. So, these 100 tokens are locked in the token bridge contract (TBC).

2. Bridge validators or oracles, monitor the events happening on the Ethereum network. They observe token deposits made to the Ethereum smart contract and verify their legitimacy.

3. In the Solana network, a corresponding program listens for events received through the bridge validators, to trigger the token minting process on Solana.

4. The Solana program creates an equivalent amount of tokens on the Solana network which are minted in the user's Solana wallet address.