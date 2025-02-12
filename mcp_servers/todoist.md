# todoist MCP server

Created by: <https://github.com/lotarcc/todoist-mcp-server>
From a fork of: <https://github.com/abhiz123/todoist-mcp-server>

## Quick reference

### Commands

Install:
``` bash
npm install -g todoist-mcp-enhanced-server
```
### .json config

Create a todoist API token from <https://app.todoist.com/app/settings/integrations/developer>

Copy and paste into claude.desktop.config.json
``` json
{
  "mcpServers": {
    "todoist": {
      "command": "npx",
      "args": ["todoist-mcp-enhanced-server"],
      "env": {
        "TODOIST_API_TOKEN": "your_api_token_here"
      }
    }
  }
}
```
