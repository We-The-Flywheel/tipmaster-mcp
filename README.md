# TipMaster consensus MCP server

What real football tippers predict, per match, as an MCP server and a JSON feed.

TipMaster is a free football prediction game that people have played since 1997. For every
match in the current round the feed publishes how the players split between home win, draw
and away win, the most common exact scores, and the same split for the highest-ranked
players. Read-only, no key, aggregates only. No odds, no bookmaker data, no single player's tip.

Docs and rules of use: **https://www.tipmaster.net/agents/**

## Connect

Remote MCP server (Streamable HTTP, stateless, no authentication):

```
https://www.tipmaster.net/api/agent/mcp
```

Claude: add a custom connector with that URL. Any MCP client:

```json
{
  "mcpServers": {
    "tipmaster-consensus": { "url": "https://www.tipmaster.net/api/agent/mcp" }
  }
}
```

Tools: `list_matches`, `get_consensus`, `get_crowd_record`. All read-only.

## REST

The same data as plain JSON:

```
curl -s "https://www.tipmaster.net/api/agent/v1/consensus?mode=classic" | jq '.matches[0]'
```

OpenAPI 3.1: https://www.tipmaster.net/api/agent/v1/openapi.json

## Rules of use

60 requests per minute per IP, responses cacheable for 60 seconds. Please link to
https://www.tipmaster.net/agents/ when you show or cite the numbers. The feed is
informational and is not betting advice.

## This repository

Holds the registry manifest (`server.json`) for the official MCP Registry. The server itself
runs inside the TipMaster site; there is no code to install here.

Terms: https://www.tipmaster.net/terms/ · Privacy: https://www.tipmaster.net/privacy/
