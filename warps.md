# Warps

The **Warps** app lets you execute MultiversX [Warps](https://warps.multiversx.com) directly from Make.com workflows. Warps are reusable blockchain action blueprints — predefined smart contract calls, token transfers, data queries, and data collection operations that anyone can create and share.

With this app, you can integrate any Warp into your automation scenarios, pass dynamic inputs from your workflows, and receive structured results back.

**Install:** [Warps](https://www.make.com/en/hq/app-invitation/113f288efa442e5a2529b09e3dbe4339)

---

## Modules

- [Execute Warp](#execute-warp)
- [Get Warp Info](#get-warp-info)
- [Check Transaction Status](#check-transaction-status)

---

## Execute Warp

Executes a Warp by its ID or URL. The module resolves the Warp, processes its inputs, signs and sends the resulting transactions (for contract/transfer types), and returns the results.

Supported Warp action types:

- **contract** — Executes a smart contract interaction on the MultiversX blockchain.
- **transfer** — Performs a token transfer.
- **query** — Reads data from the blockchain without creating a transaction (read-only).
- **collect** — Collects and stores data.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **warpId** | Text | Yes | The Warp identifier. This can be a Warp hash, a Warp URL, or any identifier that the Warp registry can resolve. |
| **inputs** | Object | No | A key-value object of input values required by the Warp. The available input fields depend on the specific Warp you are executing. Use the **Get Warp Info** module first to discover what inputs are available. |
| **chain** | Text | No | The network environment. Default: `mainnet`. |
| **simulate** | Boolean | No | If `true`, simulates the transaction without actually sending it. Useful for testing. |
| **verbose** | Boolean | No | If `true`, includes detailed debug information in the response (action details, input processing, transaction status checks). |
| **fields** | Array | No | An array of specific response field names to return. Use this to reduce response size by only getting the fields you need. |

### How to Use

1. **Find a Warp** — Browse the Warp registry or get a Warp ID from a project.
2. **Discover inputs** — Use the **Get Warp Info** module (or the RPC endpoint) to see what input fields the Warp expects.
3. **Execute** — Pass the Warp ID and any required inputs. The module handles transaction signing, sending, and status polling automatically.

### Response

| Field | Description |
|---|---|
| **warpId** | The Warp identifier that was executed. |
| **warpHash** | The resolved Warp's hash. |
| **finalTxHash** | The transaction hash (for contract/transfer actions). `null` for queries. |
| **finalStatus** | The final status: `success`, `fail`, or `pending`. |
| **results** | Array of result data returned by the Warp execution. |
| **messages** | Array of messages from the execution. |
| **next** | Next action or Warp to execute (if chained). |
| **usageFeeHash** | The usage fee transaction hash. |

If the transaction is still pending after the maximum wait time, the module returns a `pending` status with the transaction hash. You can check the status later using the **Check Transaction Status** module.

---

## Get Warp Info

Retrieves the full structure and input field definitions of a Warp without executing it. Use this to discover what inputs a Warp requires before calling **Execute Warp**.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **warpId** | Text | Yes | The Warp identifier (hash, URL, or registry name). |

### Response

Returns an array of input field definitions, each containing:

| Field | Description |
|---|---|
| **name** | The input field name (use this as the key in the `inputs` object when executing). |
| **type** | The expected data type (`text`, `number`, `date`). |
| **label** | A display label for the input. |
| **required** | Whether this input is required. |
| **min** / **max** | Minimum and maximum value constraints (if defined). |
| **pattern** | A regex pattern the value must match (if defined). |
| **patternDescription** | A description of the pattern format. |

---

## Check Transaction Status

Checks the current status of a MultiversX transaction by its hash. Useful for following up on transactions that returned a `pending` status.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **txHash** | Text | Yes | The transaction hash to check (e.g., from a previous Warp execution). |

### Response

| Field | Description |
|---|---|
| **txHash** | The transaction hash that was checked. |
| **status** | Current status: `success`, `fail`, or `pending`. |
| **details** | Additional details or error messages (if the transaction failed). |
