---
cover: .gitbook/assets/MakeX Background.jpeg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Getting Started

## What is MakeX?

MakeX is a suite of web3 applications built exclusively for [Make.com](https://www.make.com), the leading no-code automation platform. MakeX brings the power of the [MultiversX](https://multiversx.com) blockchain to no-code developers, businesses, and institutions, enabling them to automate web3 operations without writing a single line of code.

With MakeX, you can build automated workflows (called "scenarios" on Make.com) that interact with the MultiversX blockchain — send tokens, manage digital assets, run NFT snapshots, execute token swaps, and much more.

## MakeX Apps

| App | Description |
|---|---|
| **Snapshot & Draw** | Take snapshots of NFT, SFT, and ESDT token holders. Run random draws. Get unique owner statistics. |
| **MultiversX Transfers** | Send EGLD, ESDT tokens, NFTs, SFTs, and Meta-ESDTs. Airdrop tokens. Mint NFTs via smart contracts. |
| **MultiversX Assets** | Issue and manage ESDT, NFT, and SFT collections. Set roles, mint/burn supply, manage properties. |
| **Warps** | Execute MultiversX Warps — reusable blockchain action blueprints — directly from Make.com workflows. |
| **MultiversX Swap** | Swap tokens on MultiversX DEXs (xExchange, OneDex, AshSwap). Get quotes and token prices. *(Coming Soon)* |

---

## Step 1: Install MakeX Apps

Each MakeX app needs to be installed individually into your Make.com environment using the links below. Installation is **free**.

| App | Installation Link |
|---|---|
| Snapshot & Draw | [Install](https://www.make.com/en/hq/app-invitation/682839e9c23f1ba1aeb9925e16551466) |
| MultiversX Transfers | [Install](https://www.make.com/en/hq/app-invitation/db68efb5e85d04d711a632a3b2017b7d) |
| MultiversX Assets | [Install](https://www.make.com/en/hq/app-invitation/4663d084cfa02a4cfc8824724f4bfa6a) |
| Warps | [Install](https://www.make.com/en/hq/app-invitation/113f288efa442e5a2529b09e3dbe4339) |
| MultiversX Swap | *Coming Soon — not published yet* |

Click each link and follow the on-screen instructions to add the app to your Make.com account.

---

## Step 2: Create a MultiversX Wallet

You need a MultiversX wallet to interact with the blockchain.

**Create your wallet here:** [https://wallet.multiversx.com](https://wallet.multiversx.com)

During wallet creation you will receive a **seed phrase** (24 words). Write it down and store it safely — you will need it in the next step.

> **Important:** We strongly recommend creating a **new, dedicated wallet** for automations. Beginners may make mistakes, and poorly designed workflows or scheduling errors could result in unintended transactions. Keep your main funds in a separate wallet.

---

## Step 3: Generate a PEM File

To connect your wallet with MakeX apps, you need to derive a **PEM file** from your wallet's seed phrase. The PEM file is used to sign transactions from your automation wallet.

**Use our secure PEM Generator:** [https://subtle-crepe-8124c7.netlify.app](https://subtle-crepe-8124c7.netlify.app)

Enter your seed phrase, download the generated PEM file, and keep it safe. This file grants full access to your wallet — never share it with anyone.

---

## Step 4: Create a Connection in Make.com

Once you have your PEM file, you can create a wallet connection that all MakeX apps will share. You only need to do this **once per wallet**.

1. Open **Make.com** and create a new scenario (or open an existing one).
2. Drop any MakeX app onto the canvas — for example, search for **"Snapshot & Draw"**.
3. Click on the app node (bubble) to open the configuration popup.
4. Look for the **Connection** field. On the right side, click the **"Add"** button.
5. Give your connection a recognizable name. We suggest including the last 3 digits of your wallet address for easy identification (e.g., *"My Automation Wallet - 3dg"*).
6. Under the **"PEM Content"** field, click the **"Extract"** button.
7. In the extract form, click **"Choose File"** and select the PEM file you downloaded.
8. Click **"Save"** to load the PEM content, then click **"Save"** again to create the connection.

That's it! The connection is now stored under the **Credentials** section on Make.com and is available to use with any MakeX app. To add more wallet connections, simply repeat this process.

---

## Fees & Pricing

### Usage Fee

Each MakeX module call requires a small usage fee paid in **REWARD-cf6eac** tokens. The fee is **$0.03 per module call**, dynamically calculated based on the current REWARD token price.

Make sure your automation wallet holds enough **REWARD-cf6eac** tokens to cover usage fees.

### Gas Fees

Apps that perform on-chain transactions (transfers, swaps, asset management) also require **EGLD** in your wallet to cover blockchain gas fees.

### Make.com Credits

Make.com charges its own credits for each module call. For new users, Make offers **1,000 free credits per month** to test the platform.

### Free Trial

MakeX offers a **free 30-day trial** with no usage fee charges. Sign up on the official MakeX website: [https://mvx-websocket-dapp.netlify.app](https://mvx-websocket-dapp.netlify.app)

---

## You're Ready!

With your apps installed, wallet created, PEM file generated, and connection set up, you are ready to automate web3 operations on MultiversX.

Explore the documentation for each app to learn about available modules, their input fields, and how to use them in your workflows:

- [Snapshot & Draw](snapshot-and-draw.md)
- [MultiversX Transfers](multiversx-transfers.md)
- [MultiversX Assets](multiversx-assets.md)
- [Warps](warps.md)
- [MultiversX Swap](multiversx-swap.md)
