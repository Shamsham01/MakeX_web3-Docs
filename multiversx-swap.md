# MultiversX Swap

The **MultiversX Swap** app lets you swap tokens on MultiversX decentralized exchanges directly from Make.com workflows. It supports three major DEXs: **xExchange**, **OneDex**, and **AshSwap**. You can also get token prices and available trading pairs.

> **Status:** This app is currently in development and has not been published yet. It will be available for installation soon.

---

## Modules

- [xExchange Swap](#xexchange-swap)
- [OneDex Aggregator Swap](#onedex-aggregator-swap)
- [AshSwap Aggregator](#ashswap-aggregator)
- [AshSwap Quote](#ashswap-quote)
- [Get Available Pairs](#get-available-pairs)
- [Get Token Price](#get-token-price)

---

## xExchange Swap

Swaps tokens on [xExchange](https://xexchange.com), the main decentralized exchange on MultiversX. Supports both EGLD-to-token and token-to-token swaps via direct pair contracts.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **fromToken** | Text | Yes | The token you want to sell. Use `EGLD` for native EGLD, or a token identifier like `USDC-c76f1f`. |
| **toToken** | Text | Yes | The token you want to buy (e.g., `REWARD-cf6eac`). |
| **amount** | Number | Yes | The amount to swap in human-readable format (e.g., `1.5` for 1.5 EGLD). |
| **slippagePercentage** | Number | No | Maximum allowed slippage in percent. Default: `1` (1%). Higher values reduce the chance of failed transactions but may result in a worse price. |

### Response

| Field | Description |
|---|---|
| **swapDetails.fromQuantity** | Amount of tokens sent. |
| **swapDetails.fromToken** | Token sold. |
| **swapDetails.toQuantity** | Amount of tokens received. |
| **swapDetails.toToken** | Token bought. |
| **expectedAmountOut** | The expected output amount before slippage. |
| **minAmountOut** | The minimum acceptable output after slippage. |
| **transactionHash** | The swap transaction hash. |
| **transactionStatus** | `success` or `fail`. |
| **explorerUrl** | Link to view the transaction on the MultiversX Explorer. |

---

## OneDex Aggregator Swap

Swaps tokens using the [OneDex](https://onedex.app) aggregator, which finds the best route across multiple liquidity pools. Supports both EGLD and ESDT inputs. The module can automatically find the optimal route or accept custom route steps.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **fromToken** | Text | No | The token to sell. Default: `EGLD`. Use a token identifier for ESDT tokens. |
| **toToken** | Text | Yes* | The destination token identifier. Required when auto-routing (no `routeSteps` provided). |
| **amount** | Number | Yes | The amount to swap in human-readable format. |
| **routeSteps** | Array | No | Custom route steps. Each step contains `token` (identifier) and `minAmountOut` (minimum output). If not provided, the module automatically finds the best route. |
| **slippagePercentage** | Number | No | Maximum allowed slippage in percent. Default: `1`. |
| **gasLimit** | Number | No | Custom gas limit. Default: `77000000`. |

### Response

Returns swap details including the route taken, amounts, transaction hash, status, and explorer link. When auto-routing is used, the module also returns the expected output amount.

---

## AshSwap Aggregator

Swaps tokens using the [AshSwap](https://ashswap.io) aggregator v2. This aggregator finds optimal routes across multiple liquidity pools on the AshSwap protocol. Supports EGLD, ESDT-to-ESDT, ESDT-to-EGLD, and EGLD-to-ESDT swaps.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **fromToken** | Text | Yes | The token to sell. Use `EGLD` for native EGLD or a token identifier. |
| **toToken** | Text | Yes | The token to buy. Use `EGLD` for native EGLD or a token identifier. |
| **amount** | Number | Yes | The amount to swap in human-readable format. |
| **slippagePercentage** | Number | No | Maximum allowed slippage in percent. Default: `1`. |
| **gasLimit** | Number | No | Custom gas limit. Default: `77000000`. |

### Response

Returns swap details including output tokens received, route information (swaps and pools used), expected and minimum amounts, transaction hash, status, and explorer link.

---

## AshSwap Quote

Gets a price quote from AshSwap without executing a swap. Useful for previewing the expected output, checking routes, and comparing prices before committing to a trade.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **fromToken** | Text | Yes | The token to sell. Use `EGLD` or a token identifier. |
| **toToken** | Text | Yes | The token to buy. Use `EGLD` or a token identifier. |
| **amount** | Number | Yes | The amount to quote in human-readable format. |
| **slippagePercentage** | Number | No | Slippage to apply to the minimum output calculation. Default: `1`. |

### Response

| Field | Description |
|---|---|
| **quoteDetails.expectedAmountOutRaw** | Expected output amount (raw, with decimals). |
| **quoteDetails.minAmountOutRaw** | Minimum output after slippage. |
| **quoteDetails.slippagePercentage** | Applied slippage. |
| **route** | Detailed route information including pools, swap steps, and token addresses. |
| **compatibleSwapRequest** | A ready-to-use request object that can be passed directly to the AshSwap Aggregator module. |

---

## Get Available Pairs

Returns all available trading pairs for a specific token on the MultiversX DEX ecosystem.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The token identifier to look up pairs for (e.g., `WEGLD-bd4d79`). |

### Response

Returns an array of available trading pairs with their details (base token, quote token, liquidity, etc.).

---

## Get Token Price

Retrieves the current price and information for a specific token on MultiversX.

### Input Fields

| Field | Type | Required | Description |
|---|---|---|---|
| **tokenIdentifier** | Text | Yes | The token identifier to look up (e.g., `WEGLD-bd4d79`, `USDC-c76f1f`). |

### Response

Returns detailed token information including current price, market cap, supply, and decimals. If a direct price is not available, the module attempts to estimate it via WEGLD pair pricing.
