# Claude Model Context Protocol Servers on Windows Devices

It seems like most people using Claude MCP's are using Mac OS devices and information on how to get started on Windows was a bit harder to find than I'd like. So I figured I'd write a bit here on how I got Claude up and running. And since I've never worked with most of the tools or pre-reqs before, I'll make this guide a bit verbose for anyone starting a bit blank like myself.

<https://modelcontextprotocol.io/quickstart>

<https://github.com/modelcontextprotocol/servers>

## Some clarifications

Using MCP's with claude takes three components:

Claude Desktop App (most recent version)
A node.js or python driven "server" installed on your Windows Device (this confused me...)
Editing the Claude_desktop_config.json file that tells Claude which MCP's are installed and it can use
I've only tried getting the github MCP up and running, and since it's node.js based that's what I'll cover.

**To use the github MCP you also need a Classic github Personal Access Token [(how to get one)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)**

### 1. Install Claude Desktop App

Easy enough. From cmd as admin, run:

``` CMD
winget install Anthropic.Claude
```

Or download and install manually from here: <https://claude.ai/download>

### 2. Installing github MCP

Before we can install the github MCP we need node.js installed, since it's node.js based. I did this with winget (installs latest version):

``` CMD
winget install OpenJS.NodeJS
```

To install an MCP we'll need the name of the server. This is conveniently located in the json snippet you add to theclaude_Desktop_config.json later on. For the github MCP it can be found in the repo here: <https://github.com/modelcontextprotocol/servers/tree/main/src/github>

From the above link we can scroll down and find the json snippet and that has an arg: **@modelcontextprotocol/server-github.**

``` JSON
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

From the cmd termina as admin, run:

npm install -g @modelcontextprotocol/server-github
This will install the MCP server on your Windows device using the npm package manager.

### 3. Enable the MCP in Claude Desktop App

Open Claude, and navigate to File->Settings (ctrl+comma), go to the Developer Tab.

In the Developer tab, press Edit Config. It will open the explorer highlighitng the config file. 

Open that in your favorite text editor and paste in the MCP snippet from the Github MCP above.

Note the formatting of the .json file. For adding more than one MCP you only add the servers themselves, not the entire .json from the repo.

After you pasted the .json snippet into the claude_desktop_config.json file, you need to add your 

``` JSON
"env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
```

---

And that's about it. You should now be able to use the github MCP from Claude. 
