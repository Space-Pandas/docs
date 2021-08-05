# Cross-Chain Supported

## SpacePanda NFT Chain

[SpacePanda NFT chain](https://github.com/Space-Pandas/space-panda-nft-chain) \(spNFT\) chain is built on top of [Substrate](https://substrate.dev/). Substrate is powered by best-in-class cryptographic research and comes with peer-to-peer networking, consensus mechanisms, and much more.

The architecture diagram of spNFT chain is:

![spNFT Architecture Design](../.gitbook/assets/image%20%281%29.png)

There are three layers of spNFT chain platform:

### spNFT Chain Runtime Layer

It is built on top of Substrate, and leverage all the core functionalities provided, such as consensus, Wasm runtime, Storage, etc. At the same time, three core runtime modules was implemented.

* The NFT module will store all the NFT assets that were cross-chain transferred from other blockchain networks, and allow users to add additional information specific to spNFT chain.
* The SPT native token module will support the core functionalities of SPT token.  Users can stake or participate governance using SPT. And they can pay cross-chain transaction fees with SPT.
* Cross-chain NFT module will store all the cross-chain verifications and transaction records on chain.

## spNFT Bridge Layer

spNFT bridge \(built on top of [ChainBridge](https://chainbridge.chainsafe.io/)\) is responsible for all the cross-chain requests, proposal votings and executions. There are four core components in spNFT bridge:

* Bridge contract. It is used to manage all the cross-chain requests and executions.
* Whitelist contract. It is used to store all the whitelist NFT assets that can be allowed to perform a cross-chain transfer. This contract can be governed by community.
* NFT handler contract. It is used to burn or send NFT assets.
* Proposal voting contract. It is used to perform the voting strategy and finish the cross-chain transaction.

It relies on trusted relayers to perform the proposal voting and execution. In order to make the bridge trust-less and fully decentralization, the multisig contract was introduced to hold the private key of the bridge contract. Approved community users and trusted partners will hold the key share of multisig contract.

## SpacePanda Ecosystem Layer

Built on top of spNFT chain and bridge. There will be a lot of applications in SpacePanda ecosystem. For example:

* Gameplay. Users can raise, feed, battle with their SpacePanda.
* BlindBox & Auction. Users can get their unique blockchain pets through blindbox or auction.
* Play/Stake to Earn. Users can earn SPT through skilled gameplay or staking.
* User Generated Content \(UGC\). Users can generate customized NFTs and trade them.
* NFT dApps. There will be lending, staking, social dApps, etc.
* Developer Program. Developers can build application on top of spNFT platform.



