# Hacker News MCP Server

A Model Context Protocol (MCP) server that provides tools for fetching stories from Hacker News. This server parses the HTML content from news.ycombinator.com and provides structured data for different types of stories (top, new, ask, show, jobs).

## Features

- Fetch different types of stories (top, new, ask, show, jobs)
- Get structured data including titles, URLs, points, authors, timestamps, and comment counts
- Configurable limit on number of stories returned
- Clean error handling and validation

## Installation

1. Clone the repository:
```bash
git clone [your-repo-url]
cd hn-server
```

2. Install dependencies:
```bash
npm install
```

3. Build the server:
```bash
npm run build
```

4. Add to your MCP settings configuration file (location depends on your system):

For VSCode Claude extension:
```json
{
  "mcpServers": {
    "hacker-news": {
      "command": "node",
      "args": ["/path/to/hn-server/build/index.js"]
    }
  }
}
```

## Usage

The server provides a tool called `get_stories` that can be used to fetch stories from Hacker News.

### Tool: get_stories

Parameters:
- `type` (string): Type of stories to fetch
  - Options: 'top', 'new', 'ask', 'show', 'jobs'
  - Default: 'top'
- `limit` (number): Number of stories to return
  - Range: 1-30
  - Default: 10

Example usage:
```typescript
use_mcp_tool with:
server_name: "hacker-news"
tool_name: "get_stories"
arguments: {
  "type": "top",
  "limit": 5
}
```

Sample output:
```json
[
  {
    "title": "Example Story Title",
    "url": "https://example.com/story",
    "points": 100,
    "author": "username",
    "time": "2024-12-28T00:03:05",
    "commentCount": 50,
    "rank": 1
  },
  // ... more stories
]
```

### Story Object Structure

Each story object contains:
- `title` (string): The story title
- `url` (string, optional): URL of the story (may be internal HN URL for text posts)
- `points` (number): Number of upvotes
- `author` (string): Username of the poster
- `time` (string): Timestamp of when the story was posted
- `commentCount` (number): Number of comments
- `rank` (number): Position in the list

## Development

The server is built using:
- TypeScript
- Model Context Protocol SDK
- Axios for HTTP requests
- Cheerio for HTML parsing

To modify the server:

1. Make changes to `src/index.ts`
2. Rebuild:
```bash
npm run build
```

## Error Handling

The server includes robust error handling for:
- Invalid story types
- Network failures
- HTML parsing errors
- Invalid parameter values

Errors are returned with appropriate error codes and descriptive messages.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT License - feel free to use this in your own projects.