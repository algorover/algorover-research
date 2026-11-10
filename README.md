# AlgoRover Research

English | [简体中文](README.zh-CN.md)

AlgoRover Research helps you find published trading strategies, run historical backtests on public market data, and inspect trades and research reports through conversation. Backtests run in the hosted AlgoRover Research service.

This repository distributes version 0.1.2 of the Codex plugin and its installation package. The plugin connects to `https://research.algorover.ai/mcp`. You do not need to install Python, Docker, the main AlgoRover application, or a local Runtime.

[Download the plugin ZIP](algorover-research-cloud-0.1.2.zip)

## Features

- Search strategies and inspect published versions, package licenses, and runnable presets.
- Prepare a backtest using a supported market and preset, choose a 90-day or 365-day historical window, and review the configuration before starting.
- Run backtests, check progress, and cancel unfinished tasks.
- View your backtest metrics, trade details, and task history, and download research reports. Request download links for published strategy packages when needed.
- Delete a selected backtest result or all your Research data on request. Deletion requires separate authorization.

Available strategies, markets, and presets depend on what the service returns. Strategies that need preset preparation go through that step first. If preparation fails, the plugin displays the reason returned by the service.

## Installation and sign-in

Use a Codex client that supports plugins. To install from a terminal, run these commands in order:

```bash
codex plugin marketplace add algorover/algorover-research
codex plugin add algorover-research-cloud@algorover-research-github
codex mcp login algorover-research --oauth-client-registration dcr --scopes research:read,research:run
```

The last command opens the authorization page in your browser. Sign in with your AlgoRover account, review the requested permissions, and allow access. Once the terminal confirms authorization, start a new conversation in Codex.

Strategy search and backtest configuration previews are publicly accessible. Starting backtests, viewing personal tasks, and downloading personal reports require sign-in. The command above requests these permissions:

| Permission | Purpose |
| --- | --- |
| `research:read` | Read research tasks, results, and reports belonging to the signed-in account. |
| `research:run` | Start and cancel backtest tasks belonging to the signed-in account. |

Deleting data requires the additional `research:delete` permission, which the command above does not request. To use deletion tools, authorize again through your client with that permission, or manage your data on the [Research website](https://research.algorover.ai/).

Sign-in and authorization take place in your browser. Do not share passwords, access tokens, or exchange API keys in the conversation.

## Example prompts

- "Use AlgoRover Research to find EMA pullback strategies and show their runnable presets."
- "Choose an available ETH preset and prepare a backtest for the last 90 days. Show me the configuration first."
- "Start the backtest with that configuration and check its progress."
- "Show the metrics and trades from my latest successful backtest, and give me the report download link."
- "Cancel the backtest I just started."

## Data and permissions

The plugin sends the strategy reference, market, preset, and historical window needed for your task to the AlgoRover Research service. Tasks and results belong to the signed-in account and can be retrieved across conversations. Access to personal data follows account permissions.

You can request deletion of a selected backtest result or explicitly request deletion of all your Research data. Deleting all Research data is separate from deleting the identity account used to sign in. See the [privacy policy](https://www.algorover.ai/privacy/) for data collection, use, and retention rules.

AlgoRover Research supports historical research only. It does not connect exchange accounts or execute trading orders. Historical backtest results do not establish future returns.

## Connection issues

If you see `OAuth authorization required`, run the sign-in command above again, complete authorization in your browser, and start a new conversation.

If the service cannot be reached, check your network and the client's MCP connection status. When contacting support, include the error message and request ID. Leave out passwords and tokens.

## Publisher and support

Published by Rivendell Holdings Investment Limited.

- [AlgoRover website](https://www.algorover.ai/)
- [Help and support](https://www.algorover.ai/en/help/)
- [Privacy policy](https://www.algorover.ai/privacy/)
- [Terms of service](https://www.algorover.ai/terms/)
