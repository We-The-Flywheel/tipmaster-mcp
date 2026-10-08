# TipMaster expert picks MCP server

Every Friday: how the players with the best long-term record in a football prediction game
running since 1997 picked the round's 25 matches. MCP server and JSON feed.

TipMaster Classic has run every week since 1997. Each round, hundreds of players pick home
win, draw or away win on the same 25 real matches, and every match a player has played is on
record. Of the players in the current round, everyone with at least 100 career matches is
ranked by career points per match, and the top quarter forms the expert cohort.

At the Friday 18:00 Europe/Berlin deadline, when picks lock, the feed publishes how the expert
cohort split on each of the 25 matches and its majority pick, with the whole crowd's split
beside it. Before the deadline only the crowd is shown. Read-only, no key, aggregates of at
least 20 players. No odds, no bookmaker data, no single player's pick.

Docs and rules of use: **https://tipmaster.net/agents/**

## Connect

Remote MCP server (Streamable HTTP, stateless, no authentication):

```
https://tipmaster.net/api/agent/mcp
```

Claude: add a custom connector with that URL. Any MCP client:

```json
{
  "mcpServers": {
    "tipmaster-consensus": { "url": "https://tipmaster.net/api/agent/mcp" }
  }
}
```

Tools: `get_expert_picks` (start here), `get_consensus`, `list_matches`, `get_crowd_record`. All read-only.

## REST

The same data as plain JSON:

```
curl -s "https://tipmaster.net/api/agent/v1/experts?game=btm" | jq '.rounds[0].matches[0]'
```

OpenAPI 3.1: https://tipmaster.net/api/agent/v1/openapi.json

## Rules of use

60 requests per minute per IP, responses cacheable for 60 seconds. Please link to
https://tipmaster.net/agents/ when you show or cite the numbers. The feed is
informational and is not betting advice.

## This repository

Holds the registry manifest (`server.json`) for the official MCP Registry. The server itself
runs inside the TipMaster site; there is no code to install here.

Terms: https://tipmaster.net/terms/ · Privacy: https://tipmaster.net/privacy/
