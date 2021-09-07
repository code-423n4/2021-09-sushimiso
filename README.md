# Sushi MISO contest details
- 7,600 Sushi (~$95,000) main award pot
- 400 Sushi (~$5,000) gas optimization award pot
- Join [C4 Discord](https://discord.gg/EY5dvm3evD) to register
- Submit findings [using the C4 form](https://code423n4.com/2021-09-sushi-miso-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts September 9, 2021 at 00:00 UTC
- Ends September 15, 2021 at 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

# Contest Scope
This contest is open for one week. Representatives from Sushi will be available in the Code Arena Discord to answer any questions during the contest period. The focus for the contest is to try to find any errors in the logic of the code that would create undesireable or unexexpected behaviors, or would enable an attacker to drain funds from any of the contracts in a way that is advantageous for an attacker at the expense of users. The focus is set broadly in order to allow the wardens to expect the unexpected, and think outside the box. Wardens should assume that governance variables are set sensibly. However, if the wardens are able to find a way to change the value of a governance variable such that the users' funds could become susceptible to an attack as a result, this of course would be included in the scope of the contest. Lastly, we are not including social engineering approaches in this contest.

# Codebase
The full codebase may be found in this repository: https://github.com/sushiswap/miso

# Protocol Overview

MISO (short for Minimal Initial Swap Offering) is a suite of open-source smart contracts created to ease the process of launching a new project on the SushiSwap exchange. MISO aims to drive new capital and trade to the exchange by increasing the attractiveness of SushiSwap as a place for token creators and communities to launch new project tokens. MISO aims to create a launchpad for both technical and non-technical project founders, that will allow communities and projects access to all the options they need for a secure and successful deployment to the SushiSwap exchange.

# Documentation 

A general documentation explaining the backgrounds of MISO may be found here:

https://instantmiso.gitbook.io/miso/dev/token-factory-smart-contract/sushi-token-smart-contract, and all of the contracts in the MISO repository are in scope. 

While all of the contracts are in scope, specific focus should be paid to the elements listed below:

| Focus for the Contest | Description |
|-------------------------------|------------------------------------------------------|
| Post-Auction Launcher | Allows to launch liquidity to SushiSwap after a successful sale. |
| Access Controls | Utilizes OpenZeppelin Access Control to granularly control admin controls for auctions and factories. |
| Pointlist | Allows for the WhiteListing of Participants by setting commitment amounts per account. |
| Dutch Auction | Implementation of a dutch auction with a linearly falling price, with commitments being able to be made in tokens or ETH. |
| Hyperbolic Auction | Implementation of an auction with a price following a price curve, with commitments being able to be made in tokens or ETH. |
| Batch Auction | Collects funds for a specified period of time and then redistributes the tokens percentually according to the size of the commitments. |
| Crowdsale | The Miso crowdsale allows the sale of tokens at a fixed price in ETH or tokens. |


# Post-Auction Launcher
https://github.com/sushiswap/miso/blob/master/contracts/Liquidity/PostAuctionLauncher.sol

Below is a non-technical description of the Post-Auction Launcher, which is a smart contract that can be found by following the link above.

The Post-Auction Launcher as name indicates, is a contract for creation and migration of liquidity pools to Sushiswap exchange. To launch the Liquidity Pool we deposit the auction token and payment token and call finalize function.

# Access Controls
https://github.com/sushiswap/miso/tree/master/contracts/Access

Below is a non-technical description of MISO's Access Controls, which consist of smart contracts that can be found by following the link above.

When utilizing MISO to launch a project, there will be a need for admin controls for each project so that founders can initiate the auctions and make decisions about the way the auction unfolds. MISO's access controls give the founder the ability to do so, while maintaining all the security that cryptography has to offer.

## Pointlist
https://github.com/sushiswap/miso/blob/master/contracts/Access/PointList.sol

Below is a non-technical description of PointList, which is an access control smart contract that can be found by following the link above.

The Pointlist contract gives the admin the ability to set parameters for the participants of the auction such that each paticipant falls under a specific threshold that is unique to the auction type, and thus the needs of the founder.

# Auctions
https://github.com/sushiswap/miso/tree/master/contracts/Auctions

Below are the extended descriptions of each of the auction types in non-technical terms. Each of these auction types consists of a smart contract, which can be found by following the link above.

## Dutch Auction

In MISO's Dutch auctions, the price is set at a higher value per token than expected and descends over time, with the eventual price being settled on once all tokens have been sold. Practically, this means participants individually decide at which point they're happy with a token price and commit their funds--yet the auction continues until everyone is happy with the token price. This can be an active decision by a project, as often it leads to a lower total amount raised (and thus less liquidity and funding); however, everyone buying will be getting the cheapest possible token--not a bad position to be in when MISO automatically provides liquidity to SushiSwap and price speculation begins.

## Hyperbolic Auction

Hyperbolic acutions are similar to the Dutch Auction, but set along a hyperbolic curve, rather than a straight line. This method allows a more direct progression towards a target price, while still allowing price discovery in the areas above that price. Hyperbolic auctions effectively start at infinity, then rapidly drop - slowing as the auction approaches zero or the Auction minimum.

## Batch Auction

The Batch Auction is a market method whereby a set amount of tokens are divided amongst all the contributors to the market event, weighted according to their contribution to the pool. Whatever your percentage of the total raise, that's the portion of the total tokens on offer you will receive. Straightforward. Simple. Effective. Batch Auctions will be useful for projects who would like to ensure that everyone taking part is rewarded, no matter their net worth.

## Crowdsale

A fixed price and a fixed set of tokens, then it's first in best dressed. Crowdsales are great when the token price is already known or has been decided on previously. They allow a token to be distributed and provide a strong base for a tokens future listing on the SushiSwap exchange. MISO crowdsales allow any project to create an auction and go on to be exchanged in the open Sushi market.
