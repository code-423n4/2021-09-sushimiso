# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos: 
- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted. (We'll set that one up later.) 

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest is over and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

## ⭐️ Sponsor: Provide contest details

Under "SPONSORS ADD INFO HERE" heading below, include the following:

- [ ] Name of each contract and:
  - [ ] lines of code in each
  - [ ] external contracts called in each
  - [ ] libraries used in each
- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [ ] Describe anything else that adds any special logic that makes your approach unique
- [ ] Identify any areas of specific concern in reviewing the code
- [ ] Add all of the code to this repo that you want reviewed
- [ ] Create a PR to this repo with the above changes.

---

# ⭐️ Sponsor: Provide marketing details

- [ ] Your logo (URL or add file to this repo - SVG or other vector format preferred)
- [ ] Your primary Twitter handle
- [ ] Any other Twitter handles we can/should tag in (e.g. organizers' personal accounts, etc.)
- [ ] Your Discord URI
- [ ] Your website
- [ ] Optional: Do you have any quirks, recurring themes, iconic tweets, community "secret handshake" stuff we could work in? How do your people recognize each other, for example? 
- [ ] Optional: your logo in Discord emoji format

---

# Contest prep

## 🐺 C4: Contest prep
- [x] Rename this repo to reflect contest date (if applicable)
- [x] Rename contest H1 below
- [x] Add link to report form in contest details below
- [x] Update pot sizes
- [x] Fill in start and end times in contest bullets below.
- [ ] Move any relevant information in "contest scope information" above to the bottom of this readme.
- [x] Add matching info to the [code423n4.com public contest data here](https://github.com/code-423n4/code423n4.com/blob/main/_data/contests/contests.csv))
- [ ] Delete this checklist.

## ⭐️ Sponsor: Contest prep
- [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2021-06-gro/blob/main/README.md))
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 8 hours prior to contest start time.**
- [ ] Ensure that you have access to the _findings_ repo where issues will be submitted.
- [ ] Promote the contest on Twitter (optional: tag in relevant protocols, etc.)
- [ ] Share it with your own communities (blog, Discord, Telegram, email newsletters, etc.)
- [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] Designate someone (or a team of people) to monitor DMs & questions in the C4 Discord (**#questions** channel) daily (Note: please *don't* discuss issues submitted by wardens in an open channel, as this could give hints to other wardens.)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Sushi MISO contest details:
- ~$200,000 (16,000 Sushi) award pot
- Join [C4 Discord](https://discord.gg/EY5dvm3evD) to register
- Submit findings [using the C4 form](https://code423n4.com/2021-09-sushi-miso-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts September 9, 2021 at 00:00 UTC
- Ends TBD September 22, 2021 at 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

# Contest Scope
This contest is open for one week. Representatives from Sushi will be available in the Code Arena Discord to answer any questions during the contest period. The focus for the contest is to try to find any errors in the logic of the code that would create undesireable or unexexpected behaviors, or would enable an attacker to drain funds from any of the contracts in a way that is advantageous for an attacker at the expense of users. The focus is set broadly in order to allow the wardens to expect the unexpected, and think outside the box. Wardens should assume that governance variables are set sensibly. However, if the wardens are able to find a way to change the value of a governance variable such that the users' funds could become susceptible to an attack as a result, this of course would be included in the scope of the contest. Lastly, we are not including social engineering approaches in this contest.

# Codebase
The full codebase may be found in this repository: https://github.com/sushiswap/miso

##Protocol Overview

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


## Post-Auction Launcher
https://github.com/sushiswap/miso/blob/master/contracts/Liquidity/PostAuctionLauncher.sol

Below is a non-technical description of the Post-Auction Launcher, which is a smart contract that can be found by following the link above.

The Post-Auction Launcher as name indicates, is a contract for creation and migration of liquidity pools to Sushiswap exchange. To launch the Liquidity Pool we deposit the auction token and payment token and call finalize function.

## Access Controls
https://github.com/sushiswap/miso/tree/master/contracts/Access

Below is a non-technical description of MISO's Access Controls, which consist of smart contracts that can be found by following the link above.

When utilizing MISO to launch a project, there will be a need for admin controls for each project so that founders can initiate the auctions and make decisions about the way the auction unfolds. MISO's access controls give the founder the ability to do so, while maintaining all the security that cryptography has to offer.

##Pointlist
https://github.com/sushiswap/miso/blob/master/contracts/Access/PointList.sol

Below is a non-technical description of PointList, which is an access control smart contract that can be found by following the link above.

The Pointlist contract gives the admin the ability to set parameters for the participants of the auction such that each paticipant falls under a specific threshold that is unique to the auction type, and thus the needs of the founder.

## Auctions
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
