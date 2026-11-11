---
name: algorover-research
description: Open the AlgoRover Research inline card when the user starts using Research. Discover published strategies, preview and run historical backtests, check or cancel jobs, read reports, and manage research data.
---

# AlgoRover Research

Use this plugin's remote MCP tools. Computation runs in the hosted Research service. Users do not install Python, Docker, the main AlgoRover application, or a local Runtime.

Research uses public market data and supports historical analysis only. It does not connect exchange accounts or place orders. Search and preparation are public. Running backtests and reading personal results require the host's OAuth connection; never request passwords, tokens or exchange credentials in chat. Personal research belongs to the signed-in user, rather than to a conversation.

## Show the Research card first

When the user opens or starts using AlgoRover Research without specifying a strategy or task, call `search_strategies` with `{}` before replying. Use their query when they provide one. Show the inline strategy catalog so they can make their first choice on the card.

For a specific strategy, preview, job list, job status, cancellation or report request, call the corresponding card-enabled Research tool before replying. If the selected strategy still needs a preset, venue or window, open its `get_strategy` card so the user can choose. Keep replies brief and direct the user to the inline card's controls.

If the current conversation has no Research tools, ask the user to open a new Codex conversation and select `@AlgoRover Research`. If the host only renders text, use the actual tool result and its returned links. Describe the outcome without claiming that a card opened. A task's `web_url` opens its Research web page.

## Discover and prepare

1. Use `search_strategies` with the user's query and supported filters. Preserve returned cursors for pagination and describe any unsupported constraints or lack of a good match.
2. Use `get_strategy` to read the selected version, its package license and the current preparation state. If the user requests a backtest or a preview and the state is `not_requested`, call `prepare_strategy` with the exact strategy reference. While queued or running, wait at least 3 seconds between read-only `get_strategy` checks. If preparation fails, show `unavailable_reason`; an explicit retry uses `prepare_strategy` with `retry=true`. Use the preset and market combinations returned in `runnable_presets`.
3. Use `prepare_backtest` with the exact strategy reference, preset, venue and a supported 90- or 365-day window. Show the preview card and wait for the user to confirm the displayed inputs or click Start backtest. Preserve the returned package hash and signed preparation unchanged.
4. Use `get_strategy_download` only when the user requests the published strategy package. Return its download link; do not execute the downloaded package on the user's computer.

## Run and inspect

- After confirmation in chat, call `start_backtest` with the returned `prepared_input`, `preparation_ticket`, and `request_key` as `idempotency_key` to open the task card. If the user started the backtest from the card, use the created task. Reuse the key if the same start request must be retried after an uncertain response. Do not invent identifiers or silently change parameters.
- If authorization is required, let the host complete OAuth and then resume the requested operation.
- Use `get_backtest` to show the requested task's status card and `list_backtests` to show the signed-in user's task list.
- Follow the task's returned `allowed_actions` for cancellation, viewing results, and deletion. Refresh the task before acting on an older status.
- For results or a report download, use `get_backtest_result` to show the result card. Point to its Download full report button. In a text-only host, use `get_backtest_report_download` to obtain the requested link. Explain metrics, assumptions, warnings and provenance when asked. Historical results do not establish future returns.
- Use `list_backtest_trades` for requested trade details. Preserve returned pagination cursors and download URLs.
- On failure, show the service's error message and request ID when available. Do not invent results or substitute a local engine.

## Cancellation and data

- On a cancellation request, call `cancel_backtest` with the actual task ID. `cancel_requested=true` means cancellation is pending; report completion only after status becomes `cancelled`. Already completed jobs keep their completed result.
- Use `get_research_usage` to show queued and running backtests. Research has no daily backtest count quota.
- Call `delete_backtest_result` only for the result the user asked to delete.
- Call `delete_research_data` only when the user explicitly requests deletion of all their Research data, passing the required `delete-my-research-data` confirmation. This does not mean deleting their external identity account.

Respond in the user's language and use supported locale values from the tool schema.
