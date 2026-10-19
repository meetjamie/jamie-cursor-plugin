---
name: jamie-meeting-context
description: Ground coding work in what was said in meetings recorded by Jamie. Use when the user refers to a meeting, call, standup, sync, demo, or customer conversation ("as discussed", "what did we agree on", "per the call with Acme"), or asks to implement, scope, or review something that was decided out loud rather than written in a ticket.
---

# Meeting context from Jamie

Before writing code based on a meeting, use the Jamie MCP tools to find out what was actually said.

## Workflow

1. **Find the meeting.**
   - You know the topic but not the meeting: call `search_meetings` with the topic as the query. It searches meeting titles and summaries from the last 6 months. Pass `startDate` for anything older.
   - You know the time ("this morning's standup", "last Tuesday's planning"): call `list_meetings` with `startDate` and `endDate`, then pick the meeting by title.
   - You know a participant: call `search_people` with their email. It returns their most recent meeting IDs.
   - The meeting is still going on: call `get_live_meeting_transcript`. Pass `lookbackMinutes` for just the latest part.
2. **Read it.** Call `get_meeting` for the summary, tasks, participants, and transcript. If `transcriptInfo` shows the transcript was cut off and you need the detail, call `get_meeting_transcript` repeatedly, passing each `nextCursor`, until `isFinal` is true.
3. **Pull out what the code needs:** decisions, requirements, constraints, edge cases, rejected alternatives, open questions, and who owns each part.
4. **Confirm before editing.** Before you change any file, give the user a short list of these requirements with the meeting title and date. Flag anything that is ambiguous or that a later meeting changed.

## Rules

- Quote or closely paraphrase the meeting. Never present something as decided unless the summary or transcript shows it.
- If several meetings cover the topic, go with the most recent one, and say so when it overturned an earlier decision.
- Give the meeting title and date for every requirement you take from a meeting.
- If the transcript is empty and `transcriptInfo.note` says access is restricted, work from the summary and tell the user.
- Never copy full transcripts into code, commits, or pull requests, because meeting content can be confidential. Summarize only what the change needs.
