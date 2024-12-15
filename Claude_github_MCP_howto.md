# Setting up Claude GitHub MCP on Windows

This guide covers setting up the GitHub Model Context Protocol (MCP) server on Windows devices. While most Claude MCP documentation focuses on MacOS, this guide provides Windows-specific instructions.

Reference: 
- [MCP Quickstart Guide](https://modelcontextprotocol.io/quickstart)
- [MCP Servers Repository](https://github.com/modelcontextprotocol/servers)

## Requirements

- Claude Desktop App
- Node.js installed on your Windows device
- A GitHub Personal Access Token ([how to get one](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens))
- Admin access to your Windows device
- Winget package manager (pre-installed on Windows 11; for Windows 10 or if missing, see [Microsoft's installation guide](https://learn.microsoft.com/en-us/windows/package-manager/winget/))

## Installation Steps

### 1. Install Claude Desktop App
From CMD as admin:
```cmd
winget install Anthropic.Claude
```
Or download manually from [claude.ai/download](https://claude.ai/download)

### 2. Install Node.js
From CMD as admin:
```cmd
winget install OpenJS.NodeJS
```

### 3. Install GitHub MCP Server
From CMD as admin, using the npm package manager installed with Node.js:
```cmd
npm install -g @modelcontextprotocol/server-github
```

### 4. Configure Claude Desktop

1. Open Claude and go to File -> Settings (ctrl+comma)
2. Navigate to the Developer Tab
3. Click "Edit Config" 
4. Add the following to your config file:
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```
5. Replace `<YOUR_TOKEN>` with your GitHub Personal Access Token
   - When creating the token, you only need to select "full control of private repositories" under permissions
   - Make sure to save your token as it won't be shown again

## Notes
- Multiple MCPs can be added under the `mcpServers` section - only add new server entries, not the entire JSON structure again
- Make sure to maintain proper JSON formatting when editing the config file

That's it! Claude should now be able to interact with your GitHub repositories.