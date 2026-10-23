# DataSocial MCP: query TikTok data from Claude, Cursor or any MCP client

A hosted MCP server over a ClickHouse warehouse of TikTok data: **4.1B creators, 5.5B videos, 604M sounds and 113.7B
follow edges** (124.6B rows). Ask your AI assistant a question; it writes the SQL and runs it. Free.

- **Endpoint:** `https://api.datasocial.ai/mcp` (Streamable HTTP, stateless)
- **Key:** free. Sign in at [datasocial.ai](https://datasocial.ai), open the **MCP** tab, and copy the command with your key
  already in it.
- **Limits:** 100 rows per query, 10 s per query, read-only.

## Connect

**Claude Code**

```bash
claude mcp add --transport http datasocial https://api.datasocial.ai/mcp \
  --header "Authorization: Bearer $DATASOCIAL_KEY"
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "datasocial": {
      "url": "https://api.datasocial.ai/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

**Claude Desktop** (`claude_desktop_config.json`, via `mcp-remote`)

```json
{
  "mcpServers": {
    "datasocial": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://api.datasocial.ai/mcp", "--header", "Authorization:${AUTH}"],
      "env": { "AUTH": "Bearer YOUR_KEY" }
    }
  }
}
```

## Tools

| Tool | What it does |
|---|---|
| `list_tables` | The tables, their row counts and what one row is |
| `describe_table` | One table's columns, types and sort key |
| `examples` | Worked questions with SQL that runs, plus SQL tips |
| `run_sql` | Runs one read-only `SELECT` (up to 100 rows) |

## Things to ask

- "Which US creators with over 1M followers grew fastest this week?"
- "Which sounds are being used in the most new videos today?"
- "Who does @&lt;username&gt; follow?"
- "What's the average view count of videos by creators in Brazil with 100K–500K followers?"

Daily creator and video history started on 2026-09-26; sound history has 106 days since January 2026.

## Also

- Plain SQL or plain-English search in the browser, no account: [datasocial.ai](https://datasocial.ai)
- How the data is collected: [Scraping TikTok's mobile API at billions of records a day](https://datasocial.ai/writing/scraping-mobile-api)
- The full database without the 100-row limit, or the scraper code: [datasocial.ai/buy](https://datasocial.ai/buy)

This repo holds documentation only; the server is hosted.
