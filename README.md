# TipMaster plugins and MCP servers

Two integrations are available from this repository:

| Product | Connection | Included skill |
| --- | --- | --- |
| **TipMaster Expert Soccer Predictions** | Public, seven read-only tools; no account required | Find matches, compare published expert groups, review measured accuracy and the retrospective model benchmark |
| **TipMaster Coach** | OAuth to your own TipMaster account; nine reads and confirmed prediction saves | Review open matches and deadlines, save chosen scores, follow results and standings |

## Install the plugins

Claude Code:

```text
/plugin install tipmaster-soccer-predictions --marketplace We-The-Flywheel/tipmaster-mcp
/plugin install tipmaster-coach --marketplace We-The-Flywheel/tipmaster-mcp
```

For Codex, add this repository as a plugin marketplace and choose either product.
The catalog is at `.agents/plugins/marketplace.json`; Claude's catalog is at
`.claude-plugin/marketplace.json`. Each `plugins/` folder also contains the portable
OpenAI manifest and its skill. Repository availability is separate from approval
in the providers' public directories.

Coach connects to `https://tipmaster.net/api/coach/mcp`. It uses your account's
available game modes. Saves require your chosen scores and open targets; they can
replace existing predictions and become immutable at the deadline. Opponents'
predictions remain private until lock. No payments or account-management tools.

[Connection guide](https://tipmaster.net/agents/connect/) ·
[Coach plugin](plugins/tipmaster-coach/) ·
[Expert plugin](plugins/tipmaster-soccer-predictions/)

## TipMaster Expert Soccer Predictions (MCP server)

Football (soccer) predictions from the players of TipMaster, a free prediction game that has
run since 1997, with nearly 30 years of prediction-game experience. Expert groups are
selected from recorded player performance; available history differs by mode. Crowd
agreement is not a calibrated probability or a guarantee of accuracy.

For each match: the most likely final score, the home/draw/away split of the Top 20%, Top 25%
and All players (ranked by their own record), and the result once played. Plus how often each
group was right (home/draw/away and exact score). No individual player or name is ever shown.

- National: exact-score predictions on the Bundesliga, Premier League, LaLiga, Serie A,
  Ligue 1 and other top leagues in 15 countries.
- Classic: home/draw/away on 25 matches a week since 1997.

Free, read-only, no account or key. Aggregates of at least 20 players, no odds, no bookmaker
data, no single player's prediction. National shares and Classic expert groups appear
after the deadline; the Classic whole-crowd split is available while its round is open.

Docs and rules of use: **https://tipmaster.net/agents/**

## Connect

Remote MCP server (Streamable HTTP, stateless, no authentication):

```
https://tipmaster.net/api/agent/mcp
```

Claude: Customize, Connectors, Add custom connector with that URL. ChatGPT: Plugins,
Add custom MCP server with that URL and no authentication. Account/workspace restrictions
may apply; see the [setup guide](https://tipmaster.net/agents/connect/). Any MCP client:

```json
{
  "mcpServers": {
    "tipmaster": { "url": "https://tipmaster.net/api/agent/mcp" }
  }
}
```

Tools (all read-only): `get_match_prediction` (one match by team names), `find_matches`,
`get_accuracy`, `get_model_comparison`, `get_expert_picks` (this week's Classic round), `get_consensus`, `list_matches`.

`get_model_comparison` reports a dated, retrospective stored-result benchmark fitted
from imported Sportmonks fixtures. It compares published groups on the same matches,
withholds paired rates below 50 matches and makes no high-confidence or superiority
claim. Model training is offline; the public tool returns aggregate evaluation only.

## REST

The same data as plain JSON:

```
curl -s "https://tipmaster.net/api/agent/v1/consensus?mode=national" | jq '.matches[0] | {home, away, mostLikelyScore}'
```

OpenAPI 3.1: https://tipmaster.net/api/agent/v1/openapi.json

## Rules of use

60 requests per minute per IP, responses cacheable for 60 seconds. Please link to
https://tipmaster.net/agents/ when you show or cite the numbers. The service is
informational and is not betting advice.

## This repository

Holds the public registry manifest (`server.json`), Coach registry manifest
(`servers/coach.json`), plugin catalogs and integration skills. Both MCP servers
run inside TipMaster; the packages contain no game server or player data.

Terms: https://tipmaster.net/agents/terms/ · Privacy: https://tipmaster.net/privacy/
