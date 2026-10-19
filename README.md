# Jamie for Cursor

This Cursor plugin connects agents to [Jamie](https://www.meetjamie.ai), the AI meeting assistant, through Jamie's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

With it, agents can search your meeting notes, read summaries and full transcripts, follow a meeting while it is live, and work through your action items. Coding work can then start from what was actually decided in the meeting, not from memory.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Jamie**.
3. Click **Install**, then complete the Jamie sign-in prompt.

You can also run `/add-plugin jamie` in chat.

## MCP

```json
{
  "mcpServers": {
    "jamie": {
      "type": "http",
      "url": "https://mcp.meetjamie.ai/mcp"
    }
  }
}
```

Jamie signs you in with OAuth. When the plugin connects, Cursor opens a browser window where you log in to Jamie. You don't need an API key, client ID, or client secret, because the client registers itself through Dynamic Client Registration.

## Before you connect

- MCP access requires a Jamie **Pro**, **Team**, or **Enterprise** plan.
- Tool calls run as the Jamie user who signs in, and can only reach the meetings that user can see.
- Workspace admins can restrict transcript access. When they do, transcripts come back empty and agents work from the summaries.

## What agents can do

| Category | Tools |
| --- | --- |
| Meetings | `list_meetings`, `search_meetings`, `get_meeting` |
| Transcripts | `get_meeting_transcript` (full transcript, paginated), `get_live_meeting_transcript` (the meeting in progress) |
| People | `search_people` (look up contacts by email, with role, company, and recent meetings) |
| Action items | `list_tasks`, `create_tasks` |
| Summary templates | `list_templates`, `upsert_template` |
| Tags | `list_tags`, `create_tag`, `update_tag`, `delete_tag`, `set_tag_sharing`, `add_tag_to_meetings`, `remove_tag_from_meetings` |

The hosted server is the source of truth for tool names and schemas. For example prompts for each tool, see the [Jamie MCP docs](https://docs.meetjamie.ai/integrations/mcp#available-tools).

## Skills

| Skill | Use it for |
| --- | --- |
| `jamie-meeting-context` | Starting a coding task from a meeting: the agent finds the meeting, pulls out the decisions and requirements, and confirms them with you before it edits any files. |
| `jamie-action-items` | Reviewing your open action items from meetings, turning them into a coding plan or issues, and recording new action items on a meeting after you confirm them. |

## Example prompts

- *Implement the export changes we agreed on in yesterday's product sync.*
- *What are my open action items from this week's meetings that touch this repo?*
- *Summarize what the customer said about the webhook retries in the call with Acme, then check our retry logic against it.*
- *Follow the live meeting and list every bug report as it comes up.*

## Docs

- Jamie MCP docs: https://docs.meetjamie.ai/integrations/mcp
- Server URL: https://mcp.meetjamie.ai/mcp
- Support: support@meetjamie.ai

## License

MIT
