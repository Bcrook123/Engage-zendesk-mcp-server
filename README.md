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
git clone <repository-url>
cd mcp-web-content
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Your Credentials

1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your Zendesk credentials:
   ```bash
   ZENDESK_EMAIL=your-email@district.au
   ZENDESK_API_TOKEN=your_api_token_here
   ```

3. **How to get your Zendesk API token:**
   - Log in to Zendesk Admin Center
   - Go to **Apps and integrations** > **APIs** > **Zendesk API**
   - Click **Add API token**
   - Copy the token and paste it into your `.env` file
   - **Important:** Save the token securely - you won't be able to see it again!

### 4. Build the Server

```bash
npm run build
```

### 5. Configure Claude Desktop

Add this to your Claude Desktop config file:

**MacOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "engage-knowledge-web": {
      "command": "node",
      "args": ["/ABSOLUTE/PATH/TO/mcp-web-content/build/index.js"],
      "env": {
        "ZENDESK_EMAIL": "your-email@district.au",
        "ZENDESK_API_TOKEN": "your_api_token_here"
      }
    }
  }
}
```

**Important:**
- Replace `/ABSOLUTE/PATH/TO/` with the actual path to your installation
- Replace the email and API token with your actual credentials
- Or, if you set up the `.env` file, the environment variables will be loaded automatically

### 6. Restart Claude Desktop

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
- Never commit your `.env` file or credentials to Git
- Each team member should use their own Zendesk API credentials
- The `.gitignore` file is configured to prevent accidental credential commits
- API tokens should be treated as passwords - keep them secure!

## Troubleshooting

### "Missing required environment variables" error

Make sure you've set `ZENDESK_EMAIL` and `ZENDESK_API_TOKEN` either:
- In your `.env` file, OR
- In the Claude Desktop config under the `env` section

### "404 Not Found" errors

- Verify your Zendesk subdomain is correct (default: `districtsd`)
- Check that your API token is valid and hasn't been revoked
- Ensure your Zendesk account has permission to access the Help Center API

### Server not showing up in Claude

- Make sure you've restarted Claude Desktop after changing the config
- Check that the path to `build/index.js` is correct and absolute
- Verify the build completed successfully with `npm run build`

## Development

To make changes to the server:

1. Edit files in `src/`
2. Run `npm run build` to compile
3. Restart Claude Desktop to test changes

## Contributing

This is a private repository for the District team. To suggest improvements:

1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## License

MIT
