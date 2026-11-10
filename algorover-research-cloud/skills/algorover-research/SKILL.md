---
name: algorover-research
description: Discover published strategies, prepare and run historical backtests, inspect results and reports, cancel tasks, and manage the user's research data through the hosted AlgoRover Research service.
---

# AlgoRover Research

Use this plugin's remote MCP tools. Computation runs in the hosted Research service. Users do not install Python, Docker, the main AlgoRover application, or a local Runtime.

Research uses public market data and supports historical analysis only. It does not connect exchange accounts or place orders. Search and preparation are public. Running backtests and reading personal results require the host's OAuth connection; never request passwords, tokens or exchange credentials in chat. Personal research belongs to the signed-in user, rather than to a conversation.

## Discover and prepare

1. Use `search_strategies` with the user's query and supported filters. Preserve returned cursors for pagination and describe any unsupported constraints or lack of a good match.
2. Use `get_strategy` to read the selected version, its package license and the current preparation state. If the user requests a backtest or a preview and the state is `not_requested`, call `prepare_strategy` with the exact strategy reference. While queued or running, wait at least 3 seconds between read-only `get_strategy` checks. If preparation fails, show `unavailable_reason`; an explicit retry uses `prepare_strategy` with `retry=true`. Use the preset and market combinations returned in `runnable_presets`.
3. Use `prepare_backtest` with the exact strategy reference, preset, venue and a supported 90- or 365-day window. Preserve the returned package hash and signed preparation unchanged. Explain the selected configuration before starting if the user has not already requested that run.
4. Use `get_strategy_download` only when the user requests the published strategy package. Return its download link; do not execute the downloaded package on the user's computer.

## Run and inspect

- Call `start_backtest` with the returned `prepared_input`, `preparation_ticket`, and `request_key` as `idempotency_key`. Reuse that key if the same start request must be retried after an uncertain response. Do not invent identifiers or silently change parameters.
- If authorization is required, let the host complete OAuth and then resume the requested operation.
- Use `get_backtest` to inspect progress. Respect `next_poll_after_ms`; do not continuously poll without a delay. Use `list_backtests` to find the signed-in user's existing tasks.
- Follow the task's returned `allowed_actions` for cancellation, viewing results, and deletion. Refresh the task before acting on an older status.
- On success, use `get_backtest_result`. Explain the actual metrics, assumptions, warnings and provenance. Historical results do not establish future returns.
- Use `list_backtest_trades` for requested trade details and `get_backtest_report_download` for the requested report. Preserve returned pagination cursors and download URLs.
- On failure, show the service's error message and request ID when available. Do not invent results or substitute a local engine.

## Cancellation and data

- On a cancellation request, call `cancel_backtest` with the actual task ID. `cancel_requested=true` means cancellation is pending; report completion only after status becomes `cancelled`. Already completed jobs keep their completed result.
- Use `get_research_usage` to show queued and running backtests. Research has no daily backtest count quota.
- Call `delete_backtest_result` only for the result the user asked to delete.
- Call `delete_research_data` only when the user explicitly requests deletion of all their Research data, passing the required `delete-my-research-data` confirmation. This does not mean deleting their external identity account.

Respond in the user's language and use supported locale values from the tool schema. Display the host's Research card when available; use returned structured results when the host does not display cards. Do not fabricate UI links. A task's `web_url` opens its Research web page.

For first-time setup, start a strategy search using the user's stated interest. If none was provided, retrieve the public catalog and briefly explain that login is needed to run a personal backtest.
