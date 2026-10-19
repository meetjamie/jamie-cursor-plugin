---
name: jamie-action-items
description: Work through meeting action items stored in Jamie. Use when the user asks about their open action items, follow-ups, or to-dos from meetings, wants to turn meeting tasks into a coding plan, issues, or a PR checklist, or wants to record new action items on a Jamie meeting.
---

# Action items from Jamie

## Reading action items

1. Call `list_tasks` with `completed: false` and a `startDate` for the period the user means, or the last two weeks if they don't say. To get the tasks from a single meeting, pass `meetingId`.
2. Keep the tasks that matter for the codebase, such as bugs, features, refactors, and investigations. Mention the others only briefly.
3. For each task you keep, call `get_meeting` with the task's meeting ID. This gets you the discussion behind the task: what was asked for, why, and any constraints.
4. Present the tasks grouped by meeting. Give each one its assignee, due date, and priority, plus a one-line summary of the context from the meeting.

## Turning action items into work

- Turn each task into a concrete step that names the files or components involved. If the meeting did not say enough, ask the user rather than guessing.
- When drafting issues or PR descriptions, link back to the meeting by title and date. Do not paste the transcript.

## Recording new action items

`create_tasks` writes to the user's Jamie account, so:

1. Draft the list first: text, assignee, due date (`YYYY-MM-DD`), and priority (`low`, `medium`, or `high`). Show it to the user and wait for confirmation.
2. Find the meeting with `get_meeting`. Tasks can only be added to meetings the user owns, one meeting per call.
3. For assignees, use `speakerId` or `email` from the meeting's `participants` whenever possible, and `name` only when neither is available. Report every assignee returned with status `unlinked`.
