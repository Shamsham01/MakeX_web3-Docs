# MultiversX Transfers

The **MultiversX Transfers** app lets you send EGLD, ESDT tokens, NFTs, SFTs, and Meta-ESDTs directly from Make.com workflows. It also supports bulk NFT transfers, free NFT mint airdrops via smart contracts, and ESDT reward distribution to NFT holders.

**Install:** [MultiversX Transfers](https://www.make.com/en/hq/app-invitation/db68efb5e85d04d711a632a3b2017b7d)

***

## Modules

* [EGLD Transfer](multiversx-transfers.md#egld-transfer)
* [ESDT Transfer](multiversx-transfers.md#esdt-transfer)
* [NFT Transfer](multiversx-transfers.md#nft-transfer)
* [Multi NFT Transfer](multiversx-transfers.md#multi-nft-transfer)
* [SFT Transfer](multiversx-transfers.md#sft-transfer)
* [Meta-ESDT Transfer](multiversx-transfers.md#meta-esdt-transfer)
* [Free NFT Mint Airdrop](multiversx-transfers.md#free-nft-mint-airdrop)
* [ESDT Airdrop (Distribute Rewards to NFT Owners)](multiversx-transfers.md#esdt-airdrop)

***

## EGLD Transfer

Sends EGLD (the native MultiversX token) from your automation wallet to a recipient address.

### Input Fields

| Field         | Type   | Required | Description                                                                          |
| ------------- | ------ | -------- | ------------------------------------------------------------------------------------ |
| **recipient** | Text   | Yes      | The recipient's wallet address in bech32 format (e.g., `erd1...`).                   |
| **amount**    | Number | Yes      | The amount of EGLD to send (in human-readable format, e.g., `0.5` for half an EGLD). |

### Response

Returns the transaction hash and status (`success` or `fail`), plus the usage fee transaction hash.

***

## ESDT Transfer

Sends an ESDT (fungible token) from your automation wallet to a recipient. The module automatically handles decimal conversion based on the token's configuration.

### Input Fields

| Field           | Type   | Required | Description                                                                             |
| --------------- | ------ | -------- | --------------------------------------------------------------------------------------- |
| **recipient**   | Text   | Yes      | The recipient's wallet address (e.g., `erd1...`).                                       |
| **amount**      | Number | Yes      | The amount of tokens to send in human-readable format (e.g., `100` to send 100 tokens). |
| **tokenTicker** | Text   | Yes      | The ESDT token identifier (e.g., `REWARD-cf6eac`, `USDC-c76f1f`).                       |

### Response

Returns the wallet address, transaction result (hash and status), and usage fee hash.

***

## NFT Transfer

Sends a single NFT from your automation wallet to a recipient.

### Input Fields

| Field               | Type | Required | Description                                                                                                                                          |
| ------------------- | ---- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **recipient**       | Text | Yes      | The recipient's wallet address (e.g., `erd1...`).                                                                                                    |
| **tokenIdentifier** | Text | Yes      | The full NFT identifier including the hex nonce, in the format `COLLECTION-HEX-NONCE` (e.g., `EMP-897b49-1006`). The nonce is in hexadecimal format. |

### Response

Returns the transaction hash and status, plus the usage fee hash.

***

## Multi NFT Transfer

Sends up to **50 NFTs** in a single transaction from your automation wallet to a recipient. This is more efficient and cost-effective than sending NFTs one by one.

### Input Fields

| Field                | Type  | Required | Description                                                                                                                                                                         |
| -------------------- | ----- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **recipient**        | Text  | Yes      | The recipient's wallet address (e.g., `erd1...`).                                                                                                                                   |
| **tokenIdentifiers** | Array | Yes      | An array of full NFT identifiers to send (e.g., `["EMP-897b49-0112", "EMP-897b49-014d"]`). Each identifier uses the format `COLLECTION-HEX-NONCE`. Maximum 50 NFTs per transaction. |

### Response

Returns the transaction hash, status, number of NFTs sent, and usage fee hash.

***

## SFT Transfer

Sends a specified quantity of an SFT (Semi-Fungible Token) from your automation wallet to a recipient.

### Input Fields

| Field               | Type   | Required | Description                                                                                                               |
| ------------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------- |
| **recipient**       | Text   | Yes      | The recipient's wallet address (e.g., `erd1...`).                                                                         |
| **amount**          | Number | Yes      | The number of SFT units to send (e.g., `5`).                                                                              |
| **tokenIdentifier** | Text   | Yes      | The full SFT identifier in the format `COLLECTION-HEX-NONCE` (e.g., `SRB-0f1b1d-22`). The nonce is in hexadecimal format. |

### Response

Returns the transaction hash and status, plus the usage fee hash.

***

## Free NFT Mint Airdrop

Calls a smart contract's minting endpoint to mint and airdrop free NFTs to a specified receiver. This is useful for projects that have a minting smart contract with a giveaway function.

### Input Fields

| Field              | Type   | Required | Description                                                                                          |
| ------------------ | ------ | -------- | ---------------------------------------------------------------------------------------------------- |
| **scAddress**      | Text   | Yes      | The smart contract address that handles minting (e.g., `erd1qqq...`).                                |
| **endpoint**       | Text   | Yes      | The smart contract function name to call (e.g., `giveaway`).                                         |
| **receiver**       | Text   | Yes      | The wallet address that will receive the minted NFTs (e.g., `erd1...`).                              |
| **qty**            | Number | Yes      | The number of NFTs to mint and send. Must be greater than 0.                                         |
| **actionType**     | Text   | No       | Set to `giveaway_extended` if the smart contract requires collection name and stage name parameters. |
| **collectionName** | Text   | No       | Required when `actionType` is `giveaway_extended`. The name of the NFT collection.                   |
| **stageName**      | Text   | No       | Required when `actionType` is `giveaway_extended`. The minting stage name.                           |

### Response

Returns the transaction hash and status, plus the usage fee hash.

***

## ESDT Airdrop

Distributes ESDT token rewards to a list of NFT owners. You provide a list of wallet addresses with their token counts, a base reward amount, and optionally enable a multiplier so holders with more NFTs receive proportionally more tokens.

### Input Fields

| Field                | Type   | Required | Description                                                                                                                                                                                              |
| -------------------- | ------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **uniqueOwnerStats** | Array  | Yes      | An array of objects, each containing `owner` (wallet address) and `tokensCount` (number of tokens held). This can be directly mapped from the **Unique Owners Stats** output of the Snapshot & Draw app. |
| **tokenTicker**      | Text   | Yes      | The ESDT token to distribute (e.g., `REWARD-cf6eac`).                                                                                                                                                    |
| **baseAmount**       | Number | Yes      | The base reward amount per address (in human-readable format).                                                                                                                                           |
| **multiply**         | Text   | No       | Set to `"yes"` to multiply the base amount by each owner's `tokensCount`. When enabled, holders with more NFTs receive proportionally more tokens. Default: no multiplication.                           |

### Response

Returns a summary of the distribution including individual transaction hashes and statuses for each recipient, submission logs, and the usage fee hash.

> **Compatibility note:** This module works seamlessly with the **NFT Unique Owners Stats** module from the Snapshot & Draw app. Take a snapshot to get `uniqueOwnerStats`, then map it directly into this module to airdrop rewards proportionally to NFT holders.
