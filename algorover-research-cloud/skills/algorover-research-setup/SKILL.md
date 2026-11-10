---
name: algorover-research-setup
description: Set up AlgoRover Research after installation or on an explicit setup request by connecting to the hosted service and showing the strategy catalog.
---

# AlgoRover Research setup

Follow the first-time setup flow in [AlgoRover Research](../algorover-research/SKILL.md).

Call `search_strategies` using the user's stated interest, or an empty query when none was provided. Show the returned catalog and explain the next available action. Search is public; starting a personal backtest requires the host's OAuth connection. Nothing needs installing on the user's computer.

If the remote service cannot be reached, report that connection failure. Do not install or start a local Runtime as a substitute.
