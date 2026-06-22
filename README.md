# LLMemory — Cursor Plugin

Connect [Cursor](https://cursor.com) to your [LLMemory](https://llmemory.xyz) vault. Search and pull context from your ChatGPT, Claude, Codex, and Claude Code conversations without copy-pasting — directly from your editor.

## What's included

- **MCP Server** — Connects to LLMemory's remote MCP server (`https://mcp.llmemory.xyz/mcp`) with OAuth authentication. No API keys required.
- **Rules** — Contextual guidelines that help the Cursor agent use LLMemory tools effectively and avoid bloating context with vault dumps.

## What it does

LLMemory reads your local-first chat vault live from your own Google Drive (the `LLMemory/` folder, manifest + per-conversation JSON). The server is read-only and zero-storage — it brokers OAuth, streams the result, then forgets everything. Your chats never leave your Drive on a server.

Five tools:

| Tool | Purpose |
|---|---|
| `list_sources` | See which AI providers have data in your vault and counts |
| `list_recent` | Recently updated conversations (id, title, source, message count). Filter by `source` |
| `search_chats` | Full-text search across all imported conversations. Returns snippets + conversation IDs |
| `get_conversation` | Fetch one full transcript by ID (Markdown or JSON) |
| `get_context_pack` | Agent-ready briefing (goal, recent state, files, open tasks) for one conversation or a whole folder |

## Installation

Install from the Cursor plugin marketplace, or add manually:

1. Clone this repository into your Cursor plugins directory
2. Restart Cursor
3. On first use, a browser window opens — authorize LLMemory with your Google account and grant Drive access

## Authentication

OAuth 2.1 with Dynamic Client Registration. No API keys to manage. On first tool call, Cursor opens a browser flow where you sign in with Google and approve Drive access. LLMemory only ever sees your `LLMemory/` Drive folder.

## Examples

Ask the agent things like:

- *"What did I figure out about the OAuth worker last week?"* → searches your vault
- *"Pull my most recent Codex session"* → `list_recent` filtered to `codex`, then `get_conversation`
- *"Give me a context pack for the Claude Code session where we built the MCP connector"* → `get_context_pack`
- *"Show me which chats have data imported"* → `list_sources`

## Privacy

- **Zero server-side storage.** The MCP worker brokers Google OAuth and reads your Drive live; it stores no chat content and no per-user database.
- **Your Drive is the storage.** Chats live in your own Google Drive `LLMemory/` folder (written by the LLMemory browser extension / CLI).
- **Read-only.** The connector never writes to your vault.

See [STORE_PRIVACY.md](https://github.com/intrepid37/LLMemory/blob/main/STORE_PRIVACY.md) for the full privacy posture.

## Links

- [LLMemory](https://llmemory.xyz)
- [LLMemory MCP connector docs](https://github.com/intrepid37/LLMemory/blob/main/MCP_CONNECTOR.md)
- [Cursor plugin docs](https://cursor.com/docs/reference/plugins)

## License

MIT
