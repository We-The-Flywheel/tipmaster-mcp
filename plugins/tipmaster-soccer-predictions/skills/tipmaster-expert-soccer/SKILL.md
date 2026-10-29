---
name: tipmaster-expert-soccer
description: Use when the user asks for TipMaster football or soccer predictions, differences between expert player groups, recorded accuracy, or the model benchmark.
---

# TipMaster Expert Soccer Predictions

Use the public TipMaster MCP connection at `https://tipmaster.net/api/agent/mcp`.
It needs no account or API key. Discover the host's tool names and current input
schemas; do not assume a provider-specific namespace. If unavailable, direct the
user to https://tipmaster.net/agents/connect/#public-predictions.

| Request | Tools |
| --- | --- |
| A named fixture | `find_matches`, then `get_match_prediction` for the matching fixture |
| A league or date range | `find_matches` or `list_matches` |
| Full published records | `get_consensus` |
| This week's Classic round | `get_expert_picks` |
| Historical performance | `get_accuracy` with the relevant competition/mode |
| Model versus players | `get_model_comparison` |

Resolve ambiguous teams or dates before choosing a fixture. Include the teams,
competition, kickoff and source link when returned. Separate All, Top 25% and
Top 20%; report each available sample size. National can return exact scores;
Classic predicts home/draw/away only.

Unavailable groups and rates are meaningful results. Public splits require at
least 20 players, expert groups wait until the deadline, and accuracy rates
require at least 50 published matches. Preserve the returned reason; do not
reconstruct suppressed rates or individual player predictions.

Prediction shares measure agreement, not calibrated win probabilities. TipMaster
has operated since 1997; that history does not prove high-confidence forecasts.
For model comparisons, retain the evaluation date/window, baseline, matched
sample and limitations. Compare models and groups on the same fixtures; All is
not an expert group. The retrospective benchmark is not a live match forecast.

Answer from the returned data, with concise qualifications where they change the
interpretation. These tools provide free-game statistics, not guaranteed outcomes,
bookmaker odds or instructions for wagers. They cannot enter a player's scores;
that is the separate TipMaster Coach connection.
