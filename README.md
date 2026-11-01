# OutlierKit MCP server

OutlierKit gives your AI assistant YouTube research data: outlier videos, channels, transcripts, comments and keyword volumes. It is a hosted, read-only MCP server, so there is nothing to install or run.

- **Server URL:** `https://outlierkit.com/mcp`
- **Transport:** streamable HTTP
- **Auth:** OAuth 2.1, sign in with Google. No API key.
- **Docs:** https://outlierkit.com/mcp/docs

This repository holds the setup guide and client configuration. The server itself runs on OutlierKit's infrastructure, and its source is not published here.

## Requirements

An OutlierKit account with MCP access, on a plan or a free trial. Use the Google account tied to your OutlierKit login. The [docs](https://outlierkit.com/mcp/docs) list current access and credit costs.

## Setup

### Claude Code

```bash
claude mcp add outlierkit --transport http https://outlierkit.com/mcp
```

Run `/mcp` inside Claude Code, pick `outlierkit`, and sign in with Google.

### Claude (claude.ai)

Open Settings, then Connectors, then Add custom connector. Paste `https://outlierkit.com/mcp` and leave the auth fields blank.

### Cursor and other clients

Add a remote MCP server with the same URL, or use the config in [`.mcp.json`](./.mcp.json):

```json
{
  "mcpServers": {
    "outlierkit": {
      "type": "http",
      "url": "https://outlierkit.com/mcp"
    }
  }
}
```

The client opens a sign-in window on first connect. Clients that only support local stdio servers cannot connect.

## Tools

All ten tools are read-only. Each call draws from your OutlierKit credit balance.

| Tool | What it does |
|---|---|
| `outliers_search` | Find outlier videos on a topic, ranked by outlier score |
| `outliers_refresh` | Run a deeper on-demand outlier search when `outliers_search` returns too few results |
| `channels_search` | Find outlier channels on a topic with their top outlier videos |
| `channels_similar` | Find channels similar to a given channel |
| `channels_get` | Look up a channel's stats, classification, keywords and recent uploads |
| `channels_videos` | List a channel's recent uploads |
| `videos_get` | Look up a video's details, outlier metrics and channel context |
| `videos_transcript` | Get a video's transcript |
| `videos_comments` | Get a video's comments, sorted by top or newest |
| `keywords_research` | Expand seed keywords into related terms with monthly search volumes |

## Example prompts

- "Find outlier videos about tax planning for consultants from the last year."
- "Which channels are similar to this one and close to its size?"
- "Pull the transcript of this video and summarise its hook."
- "Give me keywords related to 'youtube for coaches' with at least 500 monthly searches."

## Privacy

The connector reads only your email address, to match your OutlierKit account and apply your credits. It does not access your YouTube channel, your Google account or any private Google data. See the [privacy policy](https://outlierkit.com/privacy).

## Support

Email hello@outlierkit.com.

## License

The documentation and configuration in this repository are under the [MIT License](./LICENSE). The OutlierKit service has its own terms.
