# Quick Setup Guide for Engage Knowledge Web

## For You (Local Use)

1. The server is already built and ready to use at `/Users/bencrook/mcp-web-content`

2. Add this to your Claude Desktop config:
   - **MacOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows**: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "engage-knowledge-web": {
      "command": "node",
      "args": ["/Users/bencrook/mcp-web-content/dist/index.js"]
    }
  }
}
```

3. Restart Claude Desktop

4. Test it by asking: "What categories are available in Engage Knowledge Web?"

## For Public Distribution (npm)

To make this available for anyone to install:

### Step 1: Prepare for Publishing

1. Make sure you have an npm account: [https://www.npmjs.com/signup](https://www.npmjs.com/signup)

2. Login to npm:
```bash
npm login
```

### Step 2: Publish

```bash
cd /Users/bencrook/mcp-web-content
npm publish
```

### Step 3: Share Installation Instructions

Once published, anyone can install with:

```bash
npm install -g engage-knowledge-web
```

Then add to their Claude Desktop config:

```json
{
  "mcpServers": {
    "engage-knowledge-web": {
      "command": "engage-knowledge-web"
    }
  }
}
```

## Troubleshooting

### Server Not Showing Up in Claude

1. Check the config file path is correct
2. Ensure the JSON is valid (no trailing commas, proper quotes)
3. Restart Claude Desktop completely
4. Check Claude Desktop logs for errors

### Build Errors

If you make changes, rebuild with:
```bash
cd /Users/bencrook/mcp-web-content
npm run build
```

### Testing Without Claude Desktop

You can test the server directly:
```bash
node /Users/bencrook/mcp-web-content/dist/index.js
```

The server should start and show: "Engage Knowledge Web MCP Server running on stdio"
