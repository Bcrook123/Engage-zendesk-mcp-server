# Engage Knowledge Web MCP Server

A Model Context Protocol (MCP) server that provides access to the District Engage Knowledge Base with always up-to-date information directly from Zendesk.

## Features

- Fetch live content from District Knowledge Base articles
- Search within knowledge base content using Zendesk API
- List all available categories and sections
- Always up-to-date information (no stale cache)
- Optimized for Zendesk Help Center
- Clean text extraction from HTML

## What This Does

This MCP server allows Claude (or any MCP client) to access the District Knowledge Base at [https://knowledge.district.au/hc/en-au](https://knowledge.district.au/hc/en-au) in real-time using the Zendesk API. Instead of having stale documentation, it fetches the latest content directly from Zendesk whenever you ask questions about District Engage.

## Team Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Bcrook123/Engage-zendesk-mcp-server.git
cd Engage-zendesk-mcp-server
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Build the Server

```bash
npm run build
```

### 4. Configure Claude Desktop

Add this to your Claude Desktop config file:

**MacOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "engage-knowledge-web": {
      "command": "node",
      "args": ["/ABSOLUTE/PATH/TO/Engage-zendesk-mcp-server/build/index.js"],
      "env": {
        "ZENDESK_EMAIL": "your-zendesk-email@district.au",
        "ZENDESK_API_TOKEN": "your-zendesk-api-token"
      }
    }
  }
}
```

**Important:**
- Replace `/ABSOLUTE/PATH/TO/` with the actual path where you cloned the repository
- Example MacOS: `/Users/yourname/Engage-zendesk-mcp-server/build/index.js`
- Example Windows: `C:/Users/yourname/Engage-zendesk-mcp-server/build/index.js`
- **Replace the email and API token** with the credentials shared with you privately by the team lead

### 5. Restart Claude Desktop

After adding the configuration, restart Claude Desktop completely.

## Verifying Installation

Once configured, you can test it by asking Claude:

- "What categories are available in Engage Knowledge Web?"
- "Search for District Engage features"
- "Fetch article 9063642309135 from the knowledge base"

## Available Tools

### list_categories

Lists all available categories and sections in Engage Knowledge Web.

**Parameters:** None

**Example:**
```
What categories are available in Engage Knowledge Web?
```

### fetch_article

Fetches the latest content from a specific knowledge base article by ID.

**Parameters:**
- `article_id` (required): The Zendesk article ID

**Example:**
```
Fetch article 9063642309135 from the knowledge base
```

### search_content

Searches for articles within Engage Knowledge Web using the Zendesk search API.

**Parameters:**
- `query` (required): Search term or topic

**Example:**
```
Search for "publishing workflows" in the knowledge base
```

## Security Notes

**IMPORTANT:**
- This is a **private repository** - only authorized District team members should have access
- Zendesk credentials are required
- API tokens should be treated as passwords - keep them secure!


## License

MIT
