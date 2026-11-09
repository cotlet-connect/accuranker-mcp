# How to connect AccuRanker to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your AccuRanker account.** AccuRanker has its own ChatGPT app and documents a custom MCP connector for Claude. Cotlet.dev connects your own signed-in AccuRanker account to any AI agent, so you can ask in plain words and the AI adds keywords and lists your ranks for you.

## What you can ask

> Add these 20 keywords to my acmeplumbing.com domain and track them in Google US on desktop and mobile.

> List all keywords for bluebottlebakery.com with their current rank and the change over the last 7 days.

> Which of my keywords dropped more than 5 positions since Monday? Show the page that ranks for each.

> Add "emergency plumber denver", "water heater repair denver" and "drain cleaning denver" and tag them "Denver services".

> Show my 10 keywords with the highest search volume that rank between position 11 and 20.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its AccuRanker tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"accuranker":{"command":"uvx","args":["accuranker-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t accuranker-mcp .
docker run -i --rm -e COTLET_API_KEY accuranker-mcp
```

Tools: `accuranker_guide`, `accuranker_status`, `accuranker_open`, `accuranker_read`, `accuranker_click`, `accuranker_type`, `accuranker_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install accuranker-mcp        # or run it once: uvx accuranker-mcp connect
accuranker-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 accuranker_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 accuranker_agent.py status    # is AccuRanker ready in your Cotlet.dev account
python3 accuranker_agent.py guide     # AccuRanker screens and sign-in link
python3 accuranker_agent.py read      # open AccuRanker, read the page, close the browser
python3 accuranker_agent.py tools     # list Cotlet.dev tools
python3 accuranker_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from AccuRanker users

**Does AccuRanker have an API?**

AccuRanker has an official API and an official MCP server (checked 23 Oct 2026). The Read API and Write API (both v4) come with API access at no additional cost, but need a developer and an API token. Cotlet.dev works in your own signed-in AccuRanker account, so your AI agent can add keywords and check your rankings with no API key and no code.

**How do I connect AccuRanker to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to AccuRanker once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no AccuRanker API key.

**Is there a way to use Claude with AccuRanker?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own AccuRanker account.

**Is there an AccuRanker MCP server?**

Yes, AccuRanker documents its own MCP connector for Claude. Cotlet.dev is also a hosted MCP server that works in your AccuRanker account for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

**What is AccuRanker Search Intelligence?**

AccuRanker Search Intelligence is AccuRanker's official app in the ChatGPT Plugin directory. Cotlet.dev is another way in: one connector, `https://cotlet.dev/mcp/v1`, that works in your own AccuRanker account from ChatGPT, Claude and any other AI agent.

## Find it on

- [AccuRanker on Cotlet.dev](https://cotlet.dev/integrations/accuranker-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=accuranker&utm_content=find)
- [PyPI package accuranker-mcp](https://pypi.org/project/accuranker-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-accuranker-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/accuranker-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=accuranker

Start free: https://cotlet.dev/signup?app=accuranker&utm_source=github&utm_medium=readme&utm_campaign=accuranker
