# sBTC FAQ

sBTC is a trustless two-way Bitcoin peg mechanism through which users can peg BTC from Bitcoin L1 to Bitcoin layers and then back. More specifically, sBTC is enabled by the unique properties of the [Stacks Bitcoin layer](https://stacks.co/stacks.pdf) and proposed as an upgrade to Stacks layer (see [SIP-021](https://github.com/stacksgov/sips/blob/56b73eada5ef1b72376f4a230949297b3edcc562/sips/sip-021/sip-021-trustless-two-way-peg-for-bitcoin.md)). 

Two resources for sBTC information:

- The [sBTC whitepaper](https://stacks.co/sbtc.pdf).
- sBTC [website + slides](https://stacks.co/sbtc).

### Q: Is sBTC really 'trustless'? 

A: sBTC is not BTC on Bitcoin L1. It is a pegged asset where BTC gets locked at Bitcoin L1 and sBTC is minted by the Stacks layer consensus. A decentralized group of signers are economically incentivized to sign the peg-out requests. This is an open-membership group (anyone can join), the group is dynamic (signers can come and go), and the signers have economic incentives to follow protocol rules (they lock STX capital in consensus and get BTC rewards for doing the work of signing). Some people may prefer to call this 'trust-minimized peg' or 'decentralized peg' vs a 'trustless peg'. The reason to call the peg trustless is that (a) there is no custodian or centralized company in the middle, (b) there is no fixed/known federation in the middle, (c) the system is open with open-source code and on-chain data where anyone can verify the state of the peg and locked BTC backing sBTC, and (d) the system follows the censorship properties of Bitcoin mining and finality properties of Bitcoin L1. If you consider Bitcoin design (with incentives for miners) to be trustless then you might consider sBTC peg design (with incentives for signers) to be trustless. The confusion might be that the sBTC authors are **not implying** that sBTC is as secure as BTC on Bitcoin L1. If you are pegging BTC from Bitcoin L1 to any Bitcoin layer (Lightning, Stacks, RSK, Liquid) you are taking on some additional risk and complexity than Bitcoin L1. Lightning arguably has the least amount of additional risk out of the existing Bitcoin layers. However, the sBTC peg mechanism is 'trustless' (or trust-minimized if you prefer that term) because there is no central party or federation that you are trusting in the middle.

### Q: What if someone attacks the Bitcoin on-chain oracle? 

A: sBTC uses a unique oracle from the Bitcoin L1 where there is a native Bitcoin L1 feed of the STX/BTC price pair. This information is used to determine the upper limit on sBTC that can be pegged into the Stacks layer. What if someone attacks the oracle by bidding higher than the real STX/BTC pair? (Note that bidding low is not a practical attack given other STX miners will naturally bid higher and win the bids, so the price feed will not change.) The first thing to understand is that the oracle takes a moving average of 90 days while limiting any single-day price jump to max double of the previous day price. This implies that after a day of such an attack, where the attacker is losing money, only a small percent change on the oracle feed can be made (1/90th of the input can change). Which gives ample time (days and weeks) for the community to notice the attack attempt. More importantly, sBTC can only be minted if BTC on Bitcoin L1 was locked (sBTC cannot be minted out of thin air). So even if the oracle now "widens the door" or allows a higher bandwidth of peg-ins to happen, users will still need to lock BTC on Bitcoin L1 to actually mint sBTC. Wallets (like Xverse or Hiro wallet) can easily check multiple oracles (including Chainlink or other oracles, even centralized ones) for the STX/BTC price pair and warn the user that the Bitcoin on-chain oracle seems to be reporting an incorrect price. In summary, (a) attacks on the oracle have no other implication than a small delta increase in bandwidth for peg-ins per day (no one can create sBTC out of thin air), and (b) the issue can be easily handled at the wallet UX level (which has access to feeds from multiple oracles and not just the Bitcoin on-chain oracle).