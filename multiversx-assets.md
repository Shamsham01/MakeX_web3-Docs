# MultiversX Assets

The **MultiversX Assets** app provides full lifecycle management for digital assets on MultiversX. Issue new ESDT, NFT, and SFT collections, set roles, mint and burn supply, manage properties, and more — all from Make.com workflows.

**Install:** [MultiversX Assets](https://www.make.com/en/hq/app-invitation/4663d084cfa02a4cfc8824724f4bfa6a)

---

## Modules

### ESDT Management
- [Issue ESDT](#issue-esdt)
- [Set Special Role ESDT](#set-special-role-esdt)
- [Manage ESDT Supply (Mint/Burn)](#manage-esdt-supply)
- [Pause/Unpause ESDT](#pauseunpause-esdt)
- [Freeze/Unfreeze ESDT](#freezeunfreeze-esdt)
- [Wipe ESDT](#wipe-esdt)
- [Transfer ESDT Ownership](#transfer-esdt-ownership)

### NFT Management
- [Issue NFT Collection](#issue-nft-collection)
- [Set Special Role NFT](#set-special-role-nft)
- [Create NFT](#create-nft)
- [Change NFT Attributes](#change-nft-attributes)
- [Add URI Assets to NFT](#add-uri-assets-to-nft)
- [Change NFT Properties](#change-nft-properties)
- [Transfer NFT Creation Role](#transfer-nft-creation-role)
- [Transfer NFT Ownership](#transfer-nft-ownership)

### SFT Management
- [Issue SFT Collection](#issue-sft-collection)
- [Set Special Role SFT](#set-special-role-sft)
- [Create SFT](#create-sft)
- [Transfer SFT Creation Role](#transfer-sft-creation-role)
- [Stop SFT Creation](#stop-sft-creation)
- [Transfer SFT Ownership](#transfer-sft-ownership)
- [Change SFT Properties](#change-sft-properties)
- [Freeze/Unfreeze SFT](#freezeunfreeze-sft)

### Utility
- [Set Herotag](#set-herotag)
- [Check Herotag](#check-herotag)

---

## Issue ESDT

Issues (creates) a new ESDT fungible token on MultiversX. This registers the token on-chain and sets its initial properties.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenName** | Text | Yes | Display name of the token (e.g., `MyToken`). 3-20 alphanumeric characters. |
| **tokenTicker** | Text | Yes | Short ticker symbol (e.g., `MTK`). 3-10 uppercase alphanumeric characters. |
| **initialSupply** | Number | Yes | The initial number of tokens to mint. |
| **decimals** | Number | Yes | Number of decimal places (e.g., `18` for standard tokens). |
| **canFreeze** | Boolean | No | Allow freezing tokens in specific accounts. |
| **canWipe** | Boolean | No | Allow wiping frozen tokens from accounts. |
| **canPause** | Boolean | No | Allow pausing all token transactions. |
| **canMint** | Boolean | No | Allow minting additional supply after issuance. |
| **canBurn** | Boolean | No | Allow burning (reducing) supply. |
| **canChangeOwner** | Boolean | No | Allow transferring token ownership. |
| **canUpgrade** | Boolean | No | Allow upgrading token properties. |
| **canAddSpecialRoles** | Boolean | No | Allow assigning special roles to addresses. |

### Response

Returns the transaction hash, status, token identifier (assigned by the blockchain), and explorer link.

---

## Set Special Role ESDT

Assigns or removes special roles (like minting or burning permissions) for an ESDT token to a specific address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The ESDT token identifier (e.g., `MTK-a1b2c3`). |
| **action** | Text | Yes | `set` to assign the role, or `unset` to remove it. |
| **targetAddress** | Text | Yes | The wallet address to assign the role to (e.g., `erd1...`). |
| **role** | Text | Yes | The role to assign. Options: `ESDTRoleLocalMint`, `ESDTRoleLocalBurn`, `ESDTTransferRole`. |

### Response

Returns the transaction hash and status.

---

## Manage ESDT Supply

Mints new tokens or burns existing tokens from an ESDT supply.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The ESDT token identifier (e.g., `MTK-a1b2c3`). |
| **action** | Text | Yes | `mint` to create new tokens, or `burn` to destroy tokens. |
| **amount** | Number | Yes | The amount of tokens to mint or burn (in human-readable format). |

### Response

Returns the transaction hash, status, and details of the supply change.

---

## Pause/Unpause ESDT

Pauses or unpauses all transactions for an ESDT token. When paused, no transfers of this token can occur.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The ESDT token identifier (e.g., `MTK-a1b2c3`). |
| **action** | Text | Yes | `pause` to halt all transfers, or `unpause` to resume. |

### Response

Returns the transaction hash and status.

---

## Freeze/Unfreeze ESDT

Freezes or unfreezes ESDT tokens in specific wallet addresses. Supports batch operations on multiple addresses at once.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The ESDT token identifier (e.g., `MTK-a1b2c3`). |
| **action** | Text | Yes | `freeze` or `unfreeze`. |
| **targetAddress** | Text | No | A single wallet address to freeze/unfreeze. |
| **targetAddresses** | Array | No | An array of wallet addresses for batch freeze/unfreeze operations. |

### Response

Returns transaction results for each address processed.

---

## Wipe ESDT

Wipes (permanently removes) ESDT tokens from specific frozen wallet addresses. The address must be frozen before wiping. Supports batch operations.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The ESDT token identifier (e.g., `MTK-a1b2c3`). |
| **targetAddress** | Text | No | A single wallet address to wipe. |
| **targetAddresses** | Array | No | An array of wallet addresses for batch wipe operations. |

### Response

Returns transaction results for each address processed.

---

## Transfer ESDT Ownership

Transfers the management ownership of an ESDT token to a new address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The ESDT token identifier (e.g., `MTK-a1b2c3`). |
| **newOwnerAddress** | Text | Yes | The wallet address of the new owner (e.g., `erd1...`). |

### Response

Returns the transaction hash and status.

---

## Issue NFT Collection

Issues (creates) a new NFT collection on MultiversX. This registers the collection on-chain so you can mint individual NFTs under it.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenName** | Text | Yes | Display name of the collection (e.g., `My NFT Collection`). 3-20 alphanumeric characters. |
| **tokenTicker** | Text | Yes | Short ticker symbol (e.g., `MYNFT`). 3-10 uppercase alphanumeric characters. |
| **canFreeze** | Boolean | No | Allow freezing NFTs in specific accounts. |
| **canWipe** | Boolean | No | Allow wiping frozen NFTs from accounts. |
| **canPause** | Boolean | No | Allow pausing all transfers of this collection. |
| **canTransferNFTCreateRole** | Boolean | No | Allow transferring the NFT creation role to another address. |
| **canChangeOwner** | Boolean | No | Allow transferring collection ownership. |
| **canUpgrade** | Boolean | No | Allow upgrading collection properties. |
| **canAddSpecialRoles** | Boolean | No | Allow assigning special roles to addresses. |

### Response

Returns the transaction hash, status, collection identifier, and explorer link.

---

## Set Special Role NFT

Assigns or removes special roles for an NFT collection to a specific address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT collection identifier (e.g., `MYNFT-a1b2c3`). |
| **action** | Text | Yes | `set` to assign or `unset` to remove the role. |
| **targetAddress** | Text | Yes | The wallet address to assign the role to. |
| **role** | Text | Yes | The role to assign. Options: `ESDTRoleNFTCreate`, `ESDTRoleNFTBurn`, `ESDTRoleNFTUpdateAttributes`, `ESDTRoleNFTAddURI`, `ESDTTransferRole`. |

### Response

Returns the transaction hash and status.

---

## Create NFT

Mints a new NFT within an existing collection. You must have the `ESDTRoleNFTCreate` role assigned to your wallet.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT collection identifier (e.g., `MYNFT-a1b2c3`). |
| **name** | Text | Yes | The name of this specific NFT (e.g., `My NFT #1`). |
| **quantity** | Number | No | Number of units to create (default: `1` for NFTs). |
| **royalties** | Number | No | Royalty percentage for secondary sales (0-10000, where 10000 = 100%). |
| **hash** | Text | No | A hash string for the NFT content. |
| **attributes** | Text | No | Metadata attributes as a string (e.g., `tags:art,nature;description:A beautiful piece`). |
| **uris** | Array | No | An array of URI strings pointing to the NFT media and metadata (e.g., IPFS links). |

### Response

Returns the transaction hash, status, and the newly minted NFT's nonce.

---

## Change NFT Attributes

Updates the metadata attributes of an existing NFT. Your wallet must have the `ESDTRoleNFTUpdateAttributes` role.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT identifier (e.g., `MYNFT-a1b2c3-01`). If the nonce is included, the `nonce` field is optional. |
| **nonce** | Number | No | The NFT nonce. Optional if the full identifier includes the nonce. |
| **attributes** | Text | Yes | The new attributes string to set on the NFT. |

### Response

Returns the transaction hash and status.

---

## Add URI Assets to NFT

Adds new URIs (links to media or metadata files) to an existing NFT. Your wallet must have the `ESDTRoleNFTAddURI` role.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT identifier (e.g., `MYNFT-a1b2c3-01`). |
| **nonce** | Number | No | The NFT nonce. Optional if included in the identifier. |
| **uris** | Array | Yes | An array of URI strings to add to the NFT. |

### Response

Returns the transaction hash and status.

---

## Change NFT Properties

Updates the properties of an NFT collection (such as whether special roles can be added).

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT collection identifier (e.g., `MYNFT-a1b2c3`). |
| **canAddSpecialRoles** | Boolean | No | Allow adding special roles to addresses. |
| **canTransferNFTCreateRole** | Boolean | No | Allow transferring the NFT creation role. |
| **canFreeze** | Boolean | No | Allow freezing NFTs. |
| **canWipe** | Boolean | No | Allow wiping frozen NFTs. |
| **canPause** | Boolean | No | Allow pausing transfers. |
| **canUpgrade** | Boolean | No | Allow upgrading properties. |
| **canChangeOwner** | Boolean | No | Allow transferring ownership. |

### Response

Returns the transaction hash and status.

---

## Transfer NFT Creation Role

Transfers the `ESDTRoleNFTCreate` role from one address to another within an NFT collection.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT collection identifier (e.g., `MYNFT-a1b2c3`). |
| **currentAddress** | Text | Yes | The current address that has the creation role. |
| **newAddress** | Text | Yes | The address to transfer the creation role to. |

### Response

Returns the transaction hash and status.

---

## Transfer NFT Ownership

Transfers the management ownership of an NFT collection to a new address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The NFT collection identifier (e.g., `MYNFT-a1b2c3`). |
| **newOwnerAddress** | Text | Yes | The wallet address of the new owner. |

### Response

Returns the transaction hash and status.

---

## Issue SFT Collection

Issues a new SFT (Semi-Fungible Token) collection on MultiversX.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenName** | Text | Yes | Display name of the SFT collection. 3-20 alphanumeric characters. |
| **tokenTicker** | Text | Yes | Short ticker symbol. 3-10 uppercase alphanumeric characters. |
| **canFreeze** | Boolean | No | Allow freezing SFTs in specific accounts. |
| **canWipe** | Boolean | No | Allow wiping frozen SFTs. |
| **canPause** | Boolean | No | Allow pausing all transfers. |
| **canTransferNFTCreateRole** | Boolean | No | Allow transferring the SFT creation role. |
| **canChangeOwner** | Boolean | No | Allow transferring collection ownership. |
| **canUpgrade** | Boolean | No | Allow upgrading collection properties. |
| **canAddSpecialRoles** | Boolean | No | Allow assigning special roles. |

### Response

Returns the transaction hash, status, collection identifier, and explorer link.

---

## Set Special Role SFT

Assigns or removes special roles for an SFT collection to a specific address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |
| **targetAddress** | Text | Yes | The wallet address to assign the role to. |
| **action** | Text | Yes | `set` to assign or `unset` to remove the role. |
| **role** | Text | Yes | The role to assign. Options: `ESDTRoleNFTCreate`, `ESDTRoleNFTBurn`, `ESDTRoleNFTAddQuantity`, `ESDTTransferRole`. |

### Response

Returns the transaction hash and status.

---

## Create SFT

Mints a new SFT within an existing collection with a specified initial quantity.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |
| **name** | Text | Yes | The name of this SFT edition. |
| **quantity** | Number | Yes | The initial supply quantity. |
| **royalties** | Number | No | Royalty percentage (0-10000, where 10000 = 100%). |
| **hash** | Text | No | A hash string for the SFT content. |
| **attributes** | Text | No | Metadata attributes string. |
| **uris** | Array | No | Array of URI strings for media and metadata. |

### Response

Returns the transaction hash, status, and the newly minted SFT's nonce.

---

## Transfer SFT Creation Role

Transfers the SFT creation role from one address to another.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |
| **currentAddress** | Text | Yes | The address currently holding the creation role. |
| **newAddress** | Text | Yes | The address to receive the creation role. |

### Response

Returns the transaction hash and status.

---

## Stop SFT Creation

Permanently stops the ability to create new SFTs within a collection. This action is irreversible.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |

### Response

Returns the transaction hash and status.

---

## Transfer SFT Ownership

Transfers the management ownership of an SFT collection to a new address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |
| **newOwnerAddress** | Text | Yes | The wallet address of the new owner. |

### Response

Returns the transaction hash and status.

---

## Change SFT Properties

Updates the properties of an SFT collection.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |
| **canAddSpecialRoles** | Boolean | No | Allow adding special roles. |
| **canTransferNFTCreateRole** | Boolean | No | Allow transferring the creation role. |
| **canFreeze** | Boolean | No | Allow freezing SFTs. |
| **canWipe** | Boolean | No | Allow wiping frozen SFTs. |
| **canPause** | Boolean | No | Allow pausing transfers. |
| **canUpgrade** | Boolean | No | Allow upgrading properties. |
| **canChangeOwner** | Boolean | No | Allow transferring ownership. |

### Response

Returns the transaction hash and status.

---

## Freeze/Unfreeze SFT

Freezes or unfreezes SFT tokens in specific wallet addresses. Supports batch operations.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The SFT collection identifier (e.g., `MYSFT-d4e5f6`). |
| **action** | Text | Yes | `freeze` or `unfreeze`. |
| **targetAddress** | Text | No | A single wallet address. |
| **targetAddresses** | Array | No | An array of wallet addresses for batch operations. |

### Response

Returns transaction results for each address processed.

---

## Set Herotag

Registers a herotag (human-readable name) for your MultiversX wallet address. Once set, others can send tokens to your herotag instead of your full address.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **herotag** | Text | Yes | The desired herotag name (e.g., `myname`). Will be registered as `myname.elrond` on the DNS system. Lowercase alphanumeric characters only. |

### Response

Returns the transaction hash and status.

---

## Check Herotag

Checks if a herotag is available or already registered.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **herotag** | Text | Yes | The herotag name to check (e.g., `myname`). |

### Response

Returns availability status and, if registered, the associated wallet address.
