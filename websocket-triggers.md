# WebSocket Triggers for Make Scenarios

**Trigger your Make.com scenarios from MultiversX blockchain transactions — for free.**

MakeX provides a **free WebSocket subscription service** that lets you create real-time triggers for your Make scenarios. When a transaction occurs on MultiversX that matches your filters, the service sends the event data to your webhook URL, and Make.com instantly runs your scenario.

No polling. No usage fees. Just instant, event-driven automation.

---

## How It Works

1. **Create a Webhook** in Make.com — Add a Webhooks module as the first trigger in your scenario and copy the webhook URL.
2. **Configure the subscription** — Go to the [MakeX WebSocket app](https://mvx-websocket-dapp.netlify.app), enter your webhook URL, and set your filters (address, token, sender, receiver, etc.).
3. **Subscribe** — The service connects to the MultiversX WebSocket API and listens for matching transactions.
4. **Automate** — When a matching transaction occurs, the event is sent to your webhook and your Make scenario runs automatically.

---

## Webhook Setup in Make.com

Setting up the webhook is straightforward:

1. Create a new scenario in Make.com.
2. Add the **Webhooks** module as the **first** trigger (Instant Trigger).
3. Choose **Create a webhook**.
4. Copy the webhook URL that Make.com generates (e.g., `https://hook.make.com/your-unique-id`).
5. Paste this URL into the MakeX WebSocket app when configuring your subscription.

That’s it. Your scenario will now be triggered whenever a matching MultiversX transaction occurs.

---

## Custom Transfers (Filtered) Subscription

The service uses the **Custom Transfers (Filtered)** subscription type. It subscribes to the complete stream of actions associated with a specific address or token, including:

- **Transactions** — Standard on-chain transfers.
- **Smart Contract Results (SCRs)** — Results from smart contract calls.
- **Rewards** — Staking rewards.
- **Other blockchain operations** — All relevant activity for your filters.

This is the preferred mode for tracking the full real-time activity of an account or the global movement of a specific token.

### Subscribe Event

`subscribeCustomTransfers`

### Subscription Filters (Payload)

You can filter which transactions trigger your webhook using these optional filters:

| Field | Type | Required | Description |
|---|---|---|---|
| **address** | string | No* | **Universal filter:** Matches if the address is the Sender OR Receiver OR Relayer. Use this to track all activity for a specific wallet. |
| **sender** | string | No* | Filter by sender address (bech32 format, e.g., `erd1...`). |
| **receiver** | string | No* | Filter by receiver address (bech32 format). |
| **relayer** | string | No* | Filter by the relayer address (for meta-transactions). |
| **function** | string | No* | Filter by smart contract function name. |
| **token** | string | No* | Filter by Token Identifier (e.g., `USDC-c76f1f` or `EGLD` for native EGLD). |

*At least one filter is typically required to narrow down results.

---

## Example Use Cases

- **Track incoming payments** — When someone sends EGLD or a token to your wallet, trigger a scenario to send a thank-you message or update a spreadsheet.
- **Monitor NFT sales** — When an NFT from your collection is sold, trigger a notification or update your analytics.
- **Token movement alerts** — When a specific token (e.g., `REWARD-cf6eac`) is transferred, run a follow-up action.
- **Smart contract events** — When a specific smart contract function is called, trigger a workflow.

---

## MakeX WebSocket App

**URL:** [https://mvx-websocket-dapp.netlify.app](https://mvx-websocket-dapp.netlify.app)

The service is **free** and requires no registration. Just enter your webhook URL, configure your filters, and start subscribing.

---

## Technical Reference

The MakeX WebSocket service connects to the MultiversX WebSocket API and uses the `subscribeCustomTransfers` event. When a matching transaction occurs, the event payload is forwarded to your webhook URL as an HTTP POST request. Make.com’s Webhooks module receives this payload and triggers your scenario, making the event data available in subsequent modules.

For more details on the MultiversX WebSocket API, see the [MultiversX API documentation](https://docs.multiversx.com/sdk-and-tools/rest-api/multiversx-api).
