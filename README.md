# Redbubble API and MCP server for ChatGPT and Claude

Connect ChatGPT, Claude and other AI agents to your Redbubble account through Cotlet.dev. Review designs, analytics and earnings, and edit tags and design text in your signed-in Cloud Browser.

## What you can ask

> List the works in my Manage Portfolio.

> Read the title, description and tags of a selected work.

> Review the Artist Analytics Dashboard for a selected period.

> Read my Payment History.

> Update the tags of a selected work.

> Change the title and description of a selected work.

## Connect your AI agent

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings > Apps & Connectors > Create. Use `https://cotlet.dev/mcp/v1/connect` with OAuth.

### Claude

Settings > Connectors > Add custom connector. Use `https://cotlet.dev/mcp/v1/connect`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

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

This repository provides a local MCP bridge to the hosted Cotlet.dev service.
It lists seven browser tools without a key. Account calls require your Cotlet API key.
Run it directly from this repository with Python 3.10 or later:

```bash
python3 redbubble_agent.py serve
```

Or with Docker:

```bash
docker build -t redbubble-mcp .
docker run -i --rm -e COTLET_API_KEY redbubble-mcp
```

Tools: `redbubble_guide`, `redbubble_status`, `redbubble_open`, `redbubble_read`, `redbubble_click`, `redbubble_type`, `redbubble_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, using only the Python standard library:

```bash
export COTLET_API_KEY="your-key"
python3 redbubble_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 redbubble_agent.py status    # is Redbubble ready in your Cotlet.dev account
python3 redbubble_agent.py guide     # Redbubble screens and sign-in link
python3 redbubble_agent.py read      # open Redbubble, read the page, close the browser
python3 redbubble_agent.py tools     # list Cotlet.dev tools
python3 redbubble_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Redbubble users

**How does Cotlet.dev connect to Redbubble?**

Sign in to Redbubble in your Cotlet Cloud Browser and connect ChatGPT or Claude using the instructions in your console. Your agent works in your own account.

**Can it upload new designs to Redbubble?**

No. The Cotlet.dev page describes tools for works already in your portfolio. Upload new works yourself in Redbubble.

**Is Cotlet.dev affiliated with Redbubble?**

No. Cotlet.dev is independent and is not affiliated with Redbubble or Articore Group.

## Learn more

[Redbubble on Cotlet.dev](https://cotlet.dev/integrations/redbubble-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=redbubble)

---

More: https://cotlet.dev/integrations/redbubble-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=redbubble

Start free: https://cotlet.dev/signup?app=redbubble&utm_source=github&utm_medium=readme&utm_campaign=redbubble
