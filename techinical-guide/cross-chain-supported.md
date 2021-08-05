# Cross-Chain Supported

## SpacePanda NFT Chain

[SpacePanda NFT chain](https://github.com/Space-Pandas/space-panda-nft-chain) \(spNFT\) chain is built on top of [Substrate](https://substrate.dev/). Substrate is powered by best-in-class cryptographic research and comes with peer-to-peer networking, consensus mechanisms, and much more.

The architecture diagram of spNFT chain is:

![spNFT Architecture Design](../.gitbook/assets/image%20%281%29.png)

There are three layers of spNFT chain platform:

### NFT Chain Layer

It is built on top of Substrate, and leverage all the core functionalities provided, such as consensus, Wasm runtime, Storage, etc. At the same time, three core runtime modules was implemented.

* The NFT module will store all the NFT assets that were cross-chain transferred from other blockchain networks, and allow users to add additional information specific to spNFT chain.
* The SPT native token module will support the core functionalities of SPT token.  Users can stake or participate governance using SPT. And they can pay cross-chain transaction fees with SPT.
* Cross-chain NFT module will store all the cross-chain verifications and transaction records on chain.

## spNFT Chain Runtime

## spNFT Bridge

## SpacePanda Ecosystem

