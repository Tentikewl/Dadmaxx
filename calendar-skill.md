# Calendar Skill — Google Calendar Integration

This skill governs how Claude reads and updates Google Calendar for Dad Max sessions.

## MCP tools available

Use the `mcp__c683d015-7a1f-4837-a1ab-b4e4ee21fe80__*` tools for all calendar operations:

- `list_calendars` — list available calendars, identify the right one (likely "Dad Max" or Ryan's primary)
- `list_events` — read events for a date range
- `get_event` — fetch a specific event's details
- `create_event` — add a new event
- `update_event` — modify an existing event (time, title, description, reminders)
- `delete_event` — remove an event
- `respond_to_event` — accept/decline invites
- `suggest_time` — find free slots

## Standard event format

When creating activity events:

```
title: [Activity name] — Harry
location: [Full address]
duration: as per activity schedule
reminders: 30 minutes before (default)
description: [cost, booking notes, anything useful]
```

## Term 2 activity schedule (ends July 1)

| Day       | Activity                          | Time         | Location                              | Notes          |
|-----------|-----------------------------------|--------------|---------------------------------------|----------------|
| Monday    | Glenaeon Steiner Playgroup        | 9:30–11:30am | 118 Sydney St, Willoughby             | $35, needs booking |
| Tuesday   | Playgroup Willoughby              | 12pm         | 56–58 Laurel St, Willoughby (Scouts Hall) | Free       |
| Wednesday | Baby Time Chatswood Library       | 11am         | Chatswood Library                     | Free           |
| Thursday  | Supported Playgroup Artarmon      | 10–11:30am   | 18 Broughton Rd, Artarmon (Kids Cottage) | Free       |
| Friday    | Flex / outdoor                    | —            | TBD                                   | Plan around naps |

## Wake window rule

Never schedule an outing that starts within 30 minutes of a nap window.
Current nap windows: 11:00am and 3:00pm.
Ideal outing start: 8:30–10:00am or 12:30–2:00pm.

## Term dates

- Term 2 end: July 1, 2026
- Flag to Ryan in the last week of June: "Term 2 ends this week — use /plan-week to set up Term 3 activities"
- Term 3 start: approximately July 20, 2026 (confirm with Ryan)

## /plan-week workflow

1. Call `list_events` for the coming week
2. Read `harrison-state.md` for current routine and goals
3. Read last 2 entries in `harrison-log.md` for what's been working
4. Propose the week: which activities to attend, what to try food-wise, any routine adjustments
5. Show the proposed calendar diff to Ryan
6. On confirmation, call `create_event` / `update_event` / `delete_event` as needed
7. Append plan to `harrison-log.md`
