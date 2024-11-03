
# Web3 Women Hackathon - Preserving Lands Through NFTs on Vottun and Arbitrum

This project issues NFTs as symbolic digital assets representing preservation certificates for landowners who commit to protecting their properties. Each NFT is unique and reflects the specific characteristics of the protected land, promoting land preservation through a digital record on the blockchain. The project also uses tokens that allow for direct investments in the preserved lands, encouraging the development of sustainable infrastructure.

## Overview

- **Project Name**: Nossa Terra Firme (Our Solid Ground)
- **Token Symbol**: NTF
- **Network**: Arbitrum 

This document provides a step-by-step guide to setting up, uploading metadata, and minting NFTs on the Vottun and Arbitrum networks.

## Project Concept
### NFTs:
The project issues NFTs to voluntary reserve owners. These are landowners who either purchased land to protect it or decided to protect land they already own. After verification, landowners joining our network receive an NFT that certifies the preservation of their land, including its specific characteristics. This certificate also grants access to the **Protectors of the Forest DAO**.

### Tokens:
Tokens enable investment in the lands—each property will have its own business model. For example, in the case of Marcela's land, which is the first in the network, investments will fund fencing the area and constructing a lodging center for artistic immersion experiences.

### Real Business Model:
While tokens may be symbolic and gain liquidity over time, the primary strategy is to form partnerships with DeFi companies or DAOs. These entities can issue specific tokens to sell to their clients or create other types of partnerships that generate revenue for these preservation areas.



## NFT creation on Vottun

### 1. ERC721 Token Configuration

The token configuration defines basic details such as the token’s name, symbol, network, and gas limits. This configuration initializes the NFT contract on the Arbitrum network.

``` 
POST https://api.vottun.tech/erc/v1/erc721/deploy
```
#### JSON Configuration:

```json
{
    "name": "Nossa Terra Firme",
    "symbol": "NTF",
    "network": 421614,
    "gasLimit": 6000000,
    "alias": "My first 721 contract"
}
```
After deployment, a response is returned with the contract address and transaction hash for verification.

```json
{
    "contractAddress": "0x2204D8fA82D58e8DeB4226f74928951188C32d0C",
    "txHash": "0xcf2dda94bb337c774928bd3c68bfca9350f6eb17fbfb1d141af72df6a5ee86d4"
}
```

### 2. Uploading the NFT File to IPFS
Each NFT requires a unique image or digital file, representing the preserved land, which is uploaded to IPFS (InterPlanetary File System) to ensure decentralized storage and access.

``` 
POST https://ipfsapi-v2.vottun.tech/ipfs/v2/file/upload
```

#### IPFS File Response:
```json
{
    "contractAddress": "0x2204D8fA82D58e8DeB4226f74928951188C32d0C",
    "txHash": "0xcf2dda94bb337c774928bd3c68bfca9350f6eb17fbfb1d141af72df6a5ee86d4"
}
```
This hash URL will serve as the image link in the metadata.

### 3. Metadata Definition for the NFT
The metadata associated with the NFT contains descriptive and specific information about the land, such as its registration number, area size, and conservation status. This data is essential for both the symbolic and practical aspects of the asset.

``` 
POST https://ipfsapi-v2.vottun.tech/ipfs/v2/file/metadata
```

```json
{
  "name": "Rural Property - Environmental Rural Registry",
  "description": "NFT representing the registration of rural property in the Environmental Rural Registry (CAR).",
  "image": "https://ipfsgw.vottun.tech/ipfs/bafybeiclzqqccehf26jovlfp47owymoi6yinzezg4yyhjs66rgofurkkly",
  "attributes": [
    {
      "trait_type": "CAR Registration",
      "value": "PA-1504802-8D08.EA62.51B1.4EBF.BB2B.9F12.3CEF.319A"
    },
    {
      "trait_type": "Registration Date",
      "value": "21/11/2015 10:26:04"
    },
    {
      "trait_type": "Total Property Area",
      "value": "10.9635 ha"
    },
    {
      "trait_type": "Consolidated Area",
      "value": "10.8969 ha"
    },
    {
      "trait_type": "Legal Reserve Area",
      "value": "0.0000 ha"
    },
    {
      "trait_type": "Permanent Preservation Area",
      "value": "0.0000 ha"
    },
    {
      "trait_type": "Restricted Use Area",
      "value": "0.0000 ha"
    }
  ]
}

```
#### IPFS Metadata Response:

```json
{
    "IpfsHash": "https://ipfsgw.vottun.tech/ipfs/bafkreiem2molv5iaj5sxggkdfpyqncfioax5nrzzdoebamm2nuhzs44rce",
    "PinSize": 727,
    "Timestamp": "2024-10-31 22:08:11.804948374 +0000 UTC m=+1430954.629927949"
}
```
### 4. Minting the NFT
The minting process finalizes the creation of the NFT on the blockchain. It involves specifying the recipient's wallet address, token ID, IPFS URI, network, contract address, royalty percentage, and gas limit. The royalty percentage rewards the NFT creator for secondary sales, encouraging continued support for land preservation.

``` 
POST https://api.vottun.tech/erc/v1/erc721/mint
```

```json
{
    "recipientAddress": "0xF2F657e6F9da95DDDef50f9f130359973080F149",
    "tokenId": 1,
    "ipfsUri": "https://ipfsgw.vottun.tech/ipfs/bafybeiclzqqccehf26jovlfp47owymoi6yinzezg4yyhjs66rgofurkkly",
    "ipfsHash": "bafkreiem2molv5iaj5sxggkdfpyqncfioax5nrzzdoebamm2nuhzs44rce",
    "network": 421614,
    "contractAddress": "0x2204D8fA82D58e8DeB4226f74928951188C32d0C",
    "royaltyPercentage": 10,
    "gasLimit": 3000000
}
```
#### Minting Response:
```json
{
    "txHash": "0xca00d5d8cba084eb224bd35f859893e8105f94433ec8f9ff5e8159d5a33d400a",
    "nonce": 1
}

```







