---
name: algorover-research-setup
description: Set up AlgoRover Research after installation or on an explicit setup request by connecting to the hosted service and showing the strategy catalog.
---

# AlgoRover Research setup

When Research tools are available, call `search_strategies` with `{}` to open the inline strategy catalog before replying. Point to the card's search and strategy controls. Mention that browsing is public and starting a personal backtest requires OAuth.

If tools are missing or the host requires authorization, follow [Connection recovery](../algorover-research/SKILL.md#connection-recovery), then resume setup after the host confirms the connection.

If the remote service cannot be reached, report that connection failure. Do not install or start a local Runtime as a substitute.
