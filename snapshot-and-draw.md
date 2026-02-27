# Snapshot & Draw

The **Snapshot & Draw** app allows you to take real-time snapshots of NFT, SFT, and ESDT token holders on the MultiversX blockchain. You can run random winner draws, export holder data as CSV, and generate unique owner statistics — all without writing any code.

**Install:** [Snapshot & Draw](https://www.make.com/en/hq/app-invitation/682839e9c23f1ba1aeb9925e16551466)

---

## Modules

- [NFT Snapshot & Draw](#nft-snapshot--draw)
- [NFT Snapshot CSV](#nft-snapshot-csv)
- [NFT Unique Owners Stats](#nft-unique-owners-stats)
- [SFT Snapshot & Draw](#sft-snapshot--draw)
- [ESDT Snapshot & Draw](#esdt-snapshot--draw)
- [Staked NFTs Snapshot & Draw](#staked-nfts-snapshot--draw)
- [Staked ESDTs Snapshot & Draw](#staked-esdts-snapshot--draw)

---

## NFT Snapshot & Draw

Takes a snapshot of all NFT holders in a given collection and randomly selects a specified number of winners. Supports filtering by NFT traits and metadata file names.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **collectionTicker** | Text | Yes | The NFT collection ticker (e.g., `MYNFT-a1b2c3`). |
| **numberOfWinners** | Number | Yes | How many random winners to select from the snapshot. |
| **includeSmartContracts** | Boolean | No | Whether to include smart contract addresses in the snapshot. Default: `false`. |
| **traitType** | Text | No | Filter NFTs by a specific trait type (e.g., `Background`, `Rarity`). Only NFTs that have this trait will be included. |
| **traitValue** | Text | No | Used together with `traitType` to filter by a specific trait value (e.g., `Blue`, `Legendary`). |
| **fileNamesList** | Array | No | A list of metadata file names to filter the snapshot to specific NFTs. |

### Response

Returns a list of randomly selected winners, each including the owner address, NFT identifier, and metadata attributes. Also returns collection statistics and metadata issue reports.

---

## NFT Snapshot CSV

Takes a snapshot of all NFT holders in a collection and returns the data as a CSV string. Useful for exporting holder data to spreadsheets or other tools. Supports the same trait and metadata filtering as the draw module.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **collectionTicker** | Text | Yes | The NFT collection ticker (e.g., `MYNFT-a1b2c3`). |
| **includeSmartContracts** | Boolean | No | Whether to include smart contract addresses. Default: `false`. |
| **traitType** | Text | No | Filter by a specific trait type. |
| **traitValue** | Text | No | Filter by a specific trait value (used with `traitType`). |
| **fileNamesList** | Array | No | Filter to specific NFTs by metadata file names. |

### Response

Returns a CSV-formatted string containing all NFT holders (address, identifier, metadata file name, and attributes). Also returns total counts and metadata issue reports.

---

## NFT Unique Owners Stats

Takes a snapshot of an NFT collection and generates statistics about unique owners — how many NFTs each wallet holds. This data is useful for airdrops and reward distribution.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **collectionTicker** | Text | Yes | The NFT collection ticker (e.g., `MYNFT-a1b2c3`). |
| **includeSmartContracts** | Boolean | No | Whether to include smart contract addresses. Default: `false`. |
| **traitType** | Text | No | Filter by a specific trait type. |
| **traitValue** | Text | No | Filter by a specific trait value (used with `traitType`). |
| **fileNamesList** | Array | No | Filter to specific NFTs by metadata file names. |

### Response

Returns an array of `uniqueOwnerStats`, where each entry contains:
- **owner** — the wallet address
- **tokensCount** — how many NFTs this wallet holds in the collection

> **Compatibility note:** The `uniqueOwnerStats` output from this module can be directly mapped to the **ESDT Airdrop** module of the **MultiversX Transfers** app. This allows you to take a snapshot and then airdrop rewards to holders based on how many NFTs they own — all in a single scenario.

---

## SFT Snapshot & Draw

Takes a snapshot of all SFT (Semi-Fungible Token) holders across specified editions and randomly selects winners.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **collectionTicker** | Text | Yes | The SFT collection ticker (e.g., `MYSFT-d4e5f6`). |
| **editions** | Text | Yes | Comma-separated list of edition hex nonces to include (e.g., `01,02,03`). |
| **numberOfWinners** | Number | Yes | How many random winners to select. |
| **includeSmartContracts** | Boolean | No | Whether to include smart contract addresses. Default: `false`. |

### Response

Returns the list of winners (address and balance), unique owner statistics, total owner count, and a CSV string of all holders.

---

## ESDT Snapshot & Draw

Takes a snapshot of all holders of a specific ESDT (fungible) token and randomly selects winners. Balances are properly formatted using the token's decimal precision.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **token** | Text | Yes | The ESDT token identifier (e.g., `REWARD-cf6eac`). |
| **numberOfWinners** | Number | Yes | How many random winners to select. |
| **includeSmartContracts** | Boolean | No | Whether to include smart contract addresses. Default: `false`. |

### Response

Returns the list of winners (with properly formatted balances), unique owner statistics, total owner count, token decimals, and a CSV string of all holders.

---

## Staked NFTs Snapshot & Draw

Takes a snapshot of NFTs staked in supported staking contracts and randomly selects winners from the stakers.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **collectionTicker** | Text | Yes | The NFT collection ticker (e.g., `MYNFT-a1b2c3`). |
| **contractLabel** | Text | Yes | The label of the staking contract. Supported values: `oneDexStakedNfts`, `xoxnoStakedNfts`, `artCpaStakedNfts`, `middleStakingNfts`, `hodlFounderNfts`, `ooxStakedNfts`. |
| **numberOfWinners** | Number | Yes | How many random winners to select. |

### Response

Returns the list of winners, unique owner statistics, total staked count, contract address, and a CSV string of all stakers.

---

## Staked ESDTs Snapshot & Draw

Takes a snapshot of ESDT tokens staked in a specific staking contract and randomly selects winners.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **token** | Text | Yes | The ESDT token identifier (e.g., `REWARD-cf6eac`). |
| **stakingContractAddress** | Text | Yes | The bech32 address of the staking smart contract (e.g., `erd1qqq...`). |
| **numberOfWinners** | Number | Yes | How many random winners to select. |

### Response

Returns the list of winners (with properly formatted balances), unique owner statistics, total staker count, and a CSV string of all stakers.
