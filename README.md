# TipMaster Soccer Expert Predictions (MCP server)

Football (soccer) predictions from the players of TipMaster, a free prediction game that has
run every week since 1997. For almost 30 years its players have predicted real matches and
every prediction is on record, so TipMaster knows who has called matches right for years.

For each match: the most likely final score, the home/draw/away split of the Top 20%, Top 25%
and All players (ranked by their own record), and the result once played. Plus how often each
group was right (home/draw/away and exact score) and the five best players' records.

- National: exact-score predictions on the Bundesliga, Premier League, LaLiga, Serie A,
  Ligue 1 and other top leagues in 15 countries.
- Classic: home/draw/away on 25 matches a week since 1997.

Free, read-only, no account or key. Aggregates of at least 20 players, no odds, no bookmaker
data, no single player's prediction. Published shares are final.

Docs and rules of use: **https://tipmaster.net/agents/**

## Connect

Remote MCP server (Streamable HTTP, stateless, no authentication):

```
https://tipmaster.net/api/agent/mcp
```

Claude: Settings, Connectors, Add custom connector with that URL. ChatGPT: Developer mode,
create a connector with that URL and no authentication. Any MCP client:

```json
{
  "mcpServers": {
    "tipmaster": { "url": "https://tipmaster.net/api/agent/mcp" }
  }
}
```

Tools (all read-only): `get_match_prediction` (one match by team names), `find_matches`,
`get_accuracy`, `get_expert_picks` (this week's Classic round), `get_consensus`, `list_matches`.

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

Holds the registry manifest (`server.json`) for the official MCP Registry. The server itself
runs inside the TipMaster site; there is no code to install here.

Terms: https://tipmaster.net/agents/terms/ · Privacy: https://tipmaster.net/privacy/
