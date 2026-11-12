# Installing Vayancy TravelOS (for AI Agents)

Vayancy TravelOS is a hosted remote MCP server over Server-Sent Events (SSE). There is nothing to clone, build or run locally; do not install local packages.

## 1. Remote Connection Details

* **Server Name:** `vayancy`
* **Transport:** `sse`
* **Production URL:** `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse`
* **Custom Domain:** `https://api.vayancy.gr/mcp/hospitality/sse`
* **Authentication:** None required for public traveler search and inventory holds (optional `X-Tenant-Key` for private agency portfolios).

---

## 2. Client Configurations

### Claude Desktop
Add to `claude_desktop_config.json`:
* **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
* **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "vayancy": {
      "type": "sse",
      "url": "https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse"
    }
  }
}
```

### Claude Code
Run in your terminal:
```bash
claude mcp add vayancy --transport sse https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse
```
Or install via plugin marketplace:
```bash
/plugin marketplace add nikoskalyvas/vayancy-mcp
/plugin install vayancy@vayancy
```

### Cursor & Windsurf
Add to `.cursor/mcp.json` or project MCP settings:
```json
{
  "mcpServers": {
    "vayancy": {
      "type": "sse",
      "url": "https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse"
    }
  }
}
```

### Gemini CLI
Run in your terminal:
```bash
gemini extensions install https://github.com/nikoskalyvas/vayancy-mcp
```

### Cline & Roo Code
Add to `cline_mcp_settings.json`:
```json
{
  "mcpServers": {
    "vayancy": {
      "type": "sse",
      "url": "https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse"
    }
  }
}
```

---

## 3. Verify Connection
Ask your AI assistant:
> *"Find me a 5-bedroom luxury villa in Lefkada for 10 guests with a private infinity pool and sea view for July 10-17 under €700/night."*

The assistant will invoke `search_properties` and return real-time direct-booking villas with live PMS availability.
