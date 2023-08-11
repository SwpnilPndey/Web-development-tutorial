## What are tokens? 

They are are similar to real world currencies but have intrinsic value in the decentralised ecosystem only. They can serve as assets to certain products and services. 

But, unlike real world currencies, they are decentralised.

They are signified by owner versus balance mapping and allowance nested mapping which can be populated and modified with token contract’s methods like transfer, approve, transferFrom. Total tokens can be increased by minting and decreased by burning

1 token in solidity is by default represented as 1 with 18 zeros.

Decimal function is only to show in human readable format. It means if I have one token, solidity understands it as : 1000000000000000000. If I give decimal value as 18, then after importing the token in metamask, the balance shown would be 1 (although in smart contract it is still 1000000000000000000)



## What is the use of tokens in DeFi?

Tokens are like shares. 

Following is the general procedure of the fundraising using tokens : 

- A company creates token (anybody can create and mint tokens to its address)

- It does publicity of its token : 
    - Own publicity 
    - Hire a launchpad which has a community 
    - Ask a CEX to do publicity of tokens on your behalf
    - Ask a DEX to do publicity of tokens on your behalf

- It does a presale event (mostly its own website). Owners set a token price and a time of TGE. Investors pay ETH and get their tokens booked. Those tokens would be paid out to them based on a vesting schedule after the TGE

- Now owner can distribute tokens by various methods. 
    - Directly from website (very less used)
    - ICO from a website or launchpad. Here the tokens are open for public. Also called public sale 
    - IEO from CEX
    - IDO from DEX or a launchpad 

- After the target token are sold, the token owners can **list their token on CEX or DEX** to be able to be traded by common public. Now after this, the price becomes market driven and volatile


### For centralised exchanges, token owners need to transfer tokens to a certain address on the ethereum belonging to Binance (examples). Then people can buy tokens from CEXs and trade  

### For decentralised exchanges, people can buy tokens from DEX as soon as I create a liquidity pool in it. Creating a LP is different from listing on the DEX. Listing involves scrutiny by DEX as listing equals prestige for DEX. Simply swapping is possible by searching the token address in swap window in Uniswap app (example)



## When does staking fit in the cycle ? 

 Staking can be done at any stage - before TGE or after TGE 

 Purpose is same. Hold tokens and get rewards. 

 In presale, people are generally required to stake their tokens (keep them locked) for certain duration and the tokens are available as per vesting schedule (This is generally done so that investors donot sell all their tokens immediately after ICO and hurt other investors and destabilize the market caused by inflation.)



## How does staking and staking reward work ?

Owner will set the reward amount and the locking period (duration for which the token needs to be staked/ locked)

Lets, say a user stakes 200 tokens for one week

So, simply if total staked tokens are lets say 2000, and 1000 tokens are given for every week of staking, then  the rewards that he user will get : 

Reward tokens = 200/2000 * (1000 per week)* (no. of weeks he staked)

So, if he staked for one week, he will earn 100 extra tokens as rewards 

### In terms of tokenomics, owner stes the reward, sends it to the staking contract, users lock their tokens in the staking contract and based on the period of staking, staking contract transfers the reward tokens to the user

We can calculate the rewards earned by user from time i=k to i=n seconds as :  

![Staking rewards formula](/images/staking_rewards.png)


However above formula uses a lot of gas, so in solidity the formula is reduced as : 

(Considering S as constant (staked tokens)), 


![Staking rewards in solidity](/images/staking_rewards_2.png)

**The first term is reward per token and the other is reward per token paid**


So, the staking algorithm goes as : 

1. Calculate rewards per token

r+= R/totalSupply * (Current timestamp-lastupDateTime), where R is Rewards/second


2. Calculate rewards earned by user : 

rewards[user]+=balanceOf[user]*(r-userRewardperTokenPaid[user])


3. Update user reward per token paid : 

userRewardperTokenPaid[user]= current value of r


4. Update last update time : 

lastupDateTime=current time


5. Update staked amount and total supply : 

balanceOf[user] +/- = amount, based on staking or withdrawing 
totalSupply +/- = amount, based on staking or withdrawing 



**Everytime, some user stakes, this above logic is executed.**




## What is a DEX and how does it work ?

Each of these words we hear, DEX, Liquidity pool exchange or swap exchange are basically same thing.

### How a CEX works in real world ?

If we talk about CEX first, they work on the concept of CLOB (Centralised Limit Order Book). The CEX maintains a ledger where on one side there are sell orders (price offers) and on other side there are buy orders (price bids). For example, there is one seller who wants to sell at Rs. 105 per share and there is one buyer who wants to buy at Rs. 95 per share. Then order is not complete and the record keeps on building this way. 

If there comes two entries of same price, it is on FTFS basis, this is called Price Time Priority. Which means that for buy order : highest price is highest priority, for sell, it is for lowest sell price. For same price, time is the criteria. 


### How do Crypto CEX work?

They work similar to stock exchanges but they are fast, reliable and deal in cryptos.The CEX provide a different crypto address to every user which is different from our own personal wallet address. (Similar to wallets in stock exchanges)

There are two types of transactions on CEX : deposit/ withdraw and buy/sell

The deposit and withdrawl means we transfer cryptos between our personal address & CEX provided address. This transaction is recorded on blockchain. 

However the buy and sell of cryptos is not recorded on blockchain and is maintained internally by CEX. 


### What are types of DEX ?

On DEXs, their is no concept of using fiat currency for cryptos. We can buy one token for another token only. 


There are primarly three types of DEX : 

- AMM based : smart contract based relative prices, there is no CLOB . Eg : Uniswap

- Hydrid model : off chain CLOB is there, on chain record of trades

- On chain CLOB : completely on blockchain. Eg : Serum on solana

- Aggregators based : DEX of DEXes to get best deal. Eg : 1 inch


### What is Automated Market Maker (AMM) in a DEX?

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



### What are AMM type DEXs ?

In a AMM type DEX (most common), 

- User can create a LP (add two tokens in a ratio he wants and this ratio doesnot change)

- User can add liquidity to the LP (by adding the two tokens in the same ratio as the current ratio of tokens)

- Users can swap their tokens based on the AMM rates

**Arbitrageurs can make use of lower prices on DEXes and sell them on CEXes, hence maintaining the overall market price.**


Now, how do we get tokens on a DEX, lets understand : 

- First goto a CEX and buy 100 DAI tokens for 50 USD (fiat)

- Then based on the token I want, lets say I want DOGECOIN, so, I will check for the DEX which has the the pair of DAO and DOGECOIN.

- Then I will swap my DAO tokens with the DOGECOIN tokens 


### Then questions comes, what are the benefits to become a liquidity provider?

Well based on the % of liquidity pool that I have created, who so ever uses my pool to swap their tokens, uniswap will pay some transaction fees to me. 



### What is Yield farming and how is it different from staking ?

Yield farming refers to the practice of earning additional crypto rewards by providing liquidity to decentralized exchanges or lending platforms.

Staking typically involves supporting a blockchain network, whereas yield farming involves providing liquidity to DeFi platforms.

Intention behind both is same : lock crypto and earn interests but the underlying mechanism is different.



## What is Uniswap V1, V2, V3?

Unlike most exchanges, which match buyers and sellers to determine prices and execute trades, Uniswap uses AMM and pools of tokens and ETH to do the same job


Uniswap V1 provided users to swap their tokens with ethereum only. It means there were many pools but each one had ETH as one token mandatory. So, to swap token A to token B, user needed to swap twice. Another feature Uniswap v1 introduced was LP tokens, proportional to the percentage of total liquidity they added. Every trade on Uniswap incurred a 0.30% trading fee, which went to the LP providers (Uniswap is free and doesnot charge anything)


Uniswap V2 solved this problem as now LP providers could create LPs of different pairs as well. Hence, reduced fees and slippages. ETH bridging was no longer needed. However users could still use custom path (Router contracts) for the swap (this feature is called Multi-Hop).

### Multi-Swap (multi-hop trade) and routers 

It is useful sometimes as a trade off between low fees versus more liquidity, arbitrage opportunities etc. It is used when there is not enough liquidity or depth in a single trading pair to facilitate the trade directly.

Routing algorithms analyze the available liquidity pools and trading pairs on the DEx platform to determine the optimal sequence of swaps needed to convert one token to another



### Uniswap V2 also used Oracles to get transparent prices. 


### Uniswap V3 introduced several new features : 

- **Concentrated liquidity** : The liquidity I provided in V2 is distributed all across from price 0 to infinity. But, in V3, there are markers (ticks) and I can define that my LP will be used only when the price range is between specific tick (V3 creates individualised price curves for each of the liquidity providers) 

Example : I give liquidity in a LP with 1 ETH to 100 DAI and specify that my LP should be used when 1 ETH is between 80 DAI to 120 DAI only.

So, I earn trading fees for my percent of liqudity in the price range I choose (better fees but risk is also more).

- **Active liquidity** : Risk is more since V3 uses a concept called active liquidity. It means that if the price ratio falls below the range I specified, I will not get any fees obviously and all my LP will be converted to one of the assets. I can rearrange my range or wait till price comes in the range or I can sell my assets also based on the current price. 

- **Range Limit Orders** : This allows LPs to provide a single token as liquidity in a custom price range above or below the current market price. When the market price enters into the specified range, one asset is sold for another along a smooth curve — all while still earning swap fees in the process.

- **Non-Fungible Liquidity** : As each LP can basically create its own price curve, the liquidity positions are no longer fungible and provided liquidity is tracked by non-fungible ERC721 tokens.

- Time-weighted average prices of Oracles is introduced in V3


### What is the use of Oracles in Uniswap DEX ? 

One question which comes to our mind is the wha is the use of Oracles to fetch live prices. DEX works on AMM and the prices are handled by it. 

But, in real scenario, Oracle prices fetch prices from various CEXes, DEXes and give a realisitc price for the swap. This aggregated price helps stabilize the overall price within the decentralized exchange (DEX) and prevents significant price discrepancies or surges.

Arbitrageurs play a crucial role in utilizing these oracle prices to maintain price equilibrium and reduce price discrepancies across different trading venues. When a price discrepancy occurs between the DEX and other platforms, arbitrageurs can take advantage of the price difference by buying from the lower-priced platform and selling on the higher-priced one.


### But how will the oracle fetch the price of my own created token ?

To get the price of our token, lets say HAWKS, we would need to integrate our token and its corresponding trading pair (HAWKS/USDT) into a reliable price oracle service. Once the integration is set up, we would provide the necessary information about our HAWKS token, such as its contract address, symbol, and decimals, to the oracle provider. We would also specify the trading pair HAWKS/USDT


### Various peripheral contracts can be created along with the main contracts. For example : 
trading fees are no longer automatically reinvested back into the liquidity pool on LPs’ behalf. Peripheral contracts can be created to offer such functionality.


## What is impermanent loss in crypto ?

It is the loss which the liquidity provider (investor) has to bear when he provides adds his assets (like ETH) to a liquidity pool and the price of an asset he provided changes such that if he withdraws his investment now, he will be at loss. 

Its impermanent because if he doesnot withdraw his investment, his loss might correct itself. 

### Investors suffer impermanent loss when price of the asset they provided liquidty of, changes w.r.t the stable coin they hold. But, still investors bear this loss and cover it from the transaction fees of the LPs.

So, to avoid IL : 

- Invest in stable pairs and avoid volatile
- Provide liquidity in bear market (as when the market goes up, although there is IR, the interest fees is higher to cover the losses)
- Look for extra incentives platforms 