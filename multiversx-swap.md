# MultiversX Swap

The **MultiversX Swap** app lets you swap tokens on MultiversX decentralized exchanges directly from Make.com workflows. It aggregates and routes from three major DEXs: **xExchange**, **OneDex**, **JEX** and **AshSwap**. You can also get token prices and available trading pairs.

> **Status:** This app is currently in development and has not been published yet. It will be available for installation soon.

***

## Modules

* [xExchange Swap](multiversx-swap.md#xexchange-swap)
* [AshSwap Aggregator](multiversx-swap.md#ashswap-aggregator)
* [AshSwap Quote](multiversx-swap.md#ashswap-quote)

***

## xExchange Swap

Swaps tokens on [xExchange](https://xexchange.com), the main decentralized exchange on MultiversX. Supports both EGLD-to-token and token-to-token swaps via direct pair contracts.

### Input Fields

| Field                  | Type   | Required | Description                                                                                                                                     |
| ---------------------- | ------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **fromToken**          | Text   | Yes      | The token you want to sell. Use `EGLD` for native EGLD, or a token identifier like `USDC-c76f1f`.                                               |
| **toToken**            | Text   | Yes      | The token you want to buy (e.g., `REWARD-cf6eac`).                                                                                              |
| **amount**             | Number | Yes      | The amount to swap in human-readable format (e.g., `1.5` for 1.5 EGLD).                                                                         |
| **slippagePercentage** | Number | No       | Maximum allowed slippage in percent. Default: `1` (1%). Higher values reduce the chance of failed transactions but may result in a worse price. |

### Response

| Field                        | Description                                              |
| ---------------------------- | -------------------------------------------------------- |
| **swapDetails.fromQuantity** | Amount of tokens sent.                                   |
| **swapDetails.fromToken**    | Token sold.                                              |
| **swapDetails.toQuantity**   | Amount of tokens received.                               |
| **swapDetails.toToken**      | Token bought.                                            |
| **expectedAmountOut**        | The expected output amount before slippage.              |
| **minAmountOut**             | The minimum acceptable output after slippage.            |
| **transactionHash**          | The swap transaction hash.                               |
| **transactionStatus**        | `success` or `fail`.                                     |
| **explorerUrl**              | Link to view the transaction on the MultiversX Explorer. |

***

## AshSwap Aggregator

Swaps tokens using the [AshSwap](https://ashswap.io) aggregator v2. This aggregator finds optimal routes across multiple liquidity pools on the AshSwap protocol. Supports EGLD, ESDT-to-ESDT, ESDT-to-EGLD, and EGLD-to-ESDT swaps.

### Input Fields

| Field                  | Type   | Required | Description                                                          |
| ---------------------- | ------ | -------- | -------------------------------------------------------------------- |
| **fromToken**          | Text   | Yes      | The token to sell. Use `EGLD` for native EGLD or a token identifier. |
| **toToken**            | Text   | Yes      | The token to buy. Use `EGLD` for native EGLD or a token identifier.  |
| **amount**             | Number | Yes      | The amount to swap in human-readable format.                         |
| **slippagePercentage** | Number | No       | Maximum allowed slippage in percent. Default: `1`.                   |
| **gasLimit**           | Number | No       | Custom gas limit. Default: `77000000`.                               |

### Response

Returns swap details including output tokens received, route information (swaps and pools used), expected and minimum amounts, transaction hash, status, and explorer link.

***

## AshSwap Quote

Gets a price quote from AshSwap without executing a swap. Useful for previewing the expected output, checking routes, and comparing prices before committing to a trade.

### Input Fields

| Field                  | Type   | Required | Description                                                        |
| ---------------------- | ------ | -------- | ------------------------------------------------------------------ |
| **fromToken**          | Text   | Yes      | The token to sell. Use `EGLD` or a token identifier.               |
| **toToken**            | Text   | Yes      | The token to buy. Use `EGLD` or a token identifier.                |
| **amount**             | Number | Yes      | The amount to quote in human-readable format.                      |
| **slippagePercentage** | Number | No       | Slippage to apply to the minimum output calculation. Default: `1`. |

### Response

| Field                                 | Description                                                                                 |
| ------------------------------------- | ------------------------------------------------------------------------------------------- |
| **quoteDetails.expectedAmountOutRaw** | Expected output amount (raw, with decimals).                                                |
| **quoteDetails.minAmountOutRaw**      | Minimum output after slippage.                                                              |
| **quoteDetails.slippagePercentage**   | Applied slippage.                                                                           |
| **route**                             | Detailed route information including pools, swap steps, and token addresses.                |
| **compatibleSwapRequest**             | A ready-to-use request object that can be passed directly to the AshSwap Aggregator module. |
