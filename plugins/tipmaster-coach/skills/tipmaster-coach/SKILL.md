---
name: tipmaster-coach
description: Use when the user wants to play their TipMaster soccer prediction game, review open matches and deadlines, save chosen scores, or follow their results, standings and cups.
---

# TipMaster Coach

Use the connected account's MCP at `https://tipmaster.net/api/coach/mcp`.
Discover tool names and current schemas in the host. If disconnected, use the
host's OAuth connection flow and https://tipmaster.net/agents/connect/; never
ask the user to paste a password or token into chat.

Start a game overview with `get_my_overview`. Available modes follow the returned
account state. Classic, National, World Tour and Fanclub are untranslated names.
Do not enroll the user or enable a mode through another service.

| Request | Tools |
| --- | --- |
| Open matches and deadlines | `get_open_tips`; `get_upcoming_matches` for the wider schedule |
| Saved predictions | `get_my_tips` |
| Live or completed results | `get_live_results`, `get_completed_matches` |
| League, cup or season history | `get_my_standings`, `get_my_cups`, `get_my_seasons` |
| Save chosen scores | `save_tips` after the workflow below |

For score entry, read fresh `get_open_tips` results. Show each match, score,
deadline and destination mode/competition. One fixture can have several target
IDs; use only the destinations the coach confirms. Ask for missing exact scores
or target choices. An explicit instruction confirming exact scores and targets
is sufficient; avoid repeated confirmation. General interest in predictions is
not a score submission.

Save only confirmed, currently open targets. Read eligibility immediately before
saving after any intervening delay; if the
deadline has passed, report that result without substituting another mode.
Classic uses a complete 1/X/2 round form and stays unavailable for writes unless
the live server explicitly enables it. Do not translate a score into that form
or route around a refusal.

Read saved predictions back, matching the exact target and score, and report
verified saves separately from failures or unverified writes. After a timeout,
reconcile with an authoritative read before retrying an unchanged, still-open
target. If that read fails or remains inconclusive, keep the outcome unknown
and do not retry blindly. An unknown write outcome is not success. Report
terms, scope, deadline and availability errors without bypassing them.

Show football scores, permitted predictions and plain-language outcomes. Hide
opponents' predictions before lock and never display internal duel-comparison
totals. Real league standings points remain visible. Times come from the server
in UTC; name the timezone when converting. Put the current season first.

The plugin has no payments or account-management tools. Public expert statistics
belong to the separate TipMaster Expert Soccer Predictions connection; do not
invent forecasts when the user asks only to manage their game.
