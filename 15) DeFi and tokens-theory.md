## What are tokens? 

They are are similar to real world currencies but have intrinsic value in the decentralised ecosystem only. They can serve as assets to certain products and services. 

But, unlike real world currencies, they are decentralised.

They are signified by owner versus balance mapping and allowance nested mapping which can be populated and modified with token contract’s methods like transfer, approve, transferFrom. Total tokens can be increased by minting and decreased by burning

1 token in solidity is by default represented as 1 with 18 zeros.

Decimal function is only to show in human readable format. It means if I have one token, solidity understands it as : 1000000000000000000. If I give decimal value as 18, then after importing the token in metamask, the balance shown would be 1 (although in smart contract it is still 1000000000000000000)



## What is the use of tokens in DeFi?


Companies create token, distribute them to investors and raise funds via ICO (similar to IPO) and instead of shares in company, the investors get tokens. 

Investors can benefit in a number of ways in the project ecosystem using those tokens like low cost of tokens if investors invest in presale (showing confidence in project) or subsidized access to company services and dapps or voting rights in significant decisions 

Investors can also stake their share of tokens and earn token staking reward (in terms of native tokens or some other tokens) and portion of transaction fees and this way appreciate the token value with time 

After the initial token distribution, the tokens can be traded on a variety of exchanges, including centralized exchanges like Binance or Coinbase, as well as decentralized exchanges like Uniswap or Sushiswap.

Very similar to shares, the value of tokens is volatile and driven by market forces and sentiments.

Other way people can earn company tokens is to become whitelisted user and get free tokens called AIRDROPS. Companies expand their user base in which the user needs to do some activities like liking and subscribing on social media, sending the airdrop links to others etc.




## What is presale vesting of tokens?

The presale events are those where investors get tokens at cheaper prices but they have to keep the tokens locked and withdraw only as per a vesting schedule. 

Investors use the lock function to lock their tokens in the vesting contract and after the lock period is over, they can withdraw the unlocked tokens (as per vesting schedule) if they want or keep them invested if they want to earn interests on it.

This is generally done so that investors donot sell all their tokens immediately after ICO and hurt other investors and destabilize the market caused by inflation.




## How does staking and staking reward work ?

Owner will set the reward amount and the locking period (duration for which the token needs to be staked/ locked)

Lets, say a user stakes 200 tokens for one week

So, simply if total staked tokens are lets say 2000, and 1000 tokens are given for every week of staking, then  the rewards that he user will get : 

Reward tokens = 200/2000 * (1000 per week)* (no. of weeks he staked)

So, if he staked for one week, he will earn 100 extra tokens as rewards 

### In terms of tokenomics, owner stes the reward, sends it to the staking contract, users lock their tokens in the staking contract and based on the period of staking, staking contract transfers the reward tokens to the user

We can calculate the rewards earned by user from time i=k to i=n seconds as :  

![Staking rewards formula](/images/staking_rewards.png)




## What is a DEX and how does it work ?











## How does Liquidity pool work?










## What is Automated Market Maker in a DEX?


An AMM is a part of decentralized exchange (DEX) that relies on a mathematical formula to determine the prices of assets being traded on the platform.

AMM uses a liquidity pool that contains two or more assets in a fixed ratio.

The mathematical formula used by AMMs is usually based on the constant product formula, also known as the x*y=k formula.

These values are taken at the time of creation of liquidity pool. 

Suppose I want to create a pool of 1:1 ratio between token A and token B, then this ratio will be maintained at all times. 

So, suppose initially I have 50,000 token A and 50,000 token B.

Now, Mr. X comes with 2,000 token A to take token B in return. After he adds 2,000 tokens, the number of token A becomes 52,000. 

Based on constant product formula. The total no. of products should be 50,000 * 50,000 = 2,500,000,000

So, in order to maintain this ratio, the number of token B in the pool should be : 2,500,000,000/52,000 = 48,076.92.

So, extra token B would be = 50,000-48076.92 = 1923.08 

This is the value of token B that Mr. X will get. 

This is how AMM works and the constant product ratio is maintained 