# Calendar Skill — Google Calendar Integration

This skill governs how Claude reads and updates Google Calendar for Dad Max sessions.

## MCP tools available

Use the `mcp__c683d015-7a1f-4837-a1ab-b4e4ee21fe80__*` tools for all calendar operations:

- `list_calendars` — list available calendars. **Use `18rgavo@gmail.com` for all Dad Max events** (confirmed primary personal calendar)
- `list_events` — read events for a date range
- `get_event` — fetch a specific event's details
- `create_event` — add a new event
- `update_event` — modify an existing event (time, title, description, reminders)
- `delete_event` — remove an event
- `respond_to_event` — accept/decline invites
- `suggest_time` — find free slots

## Graceful degradation

If any MCP calendar tool returns an error or is unavailable:

1. Do not fail silently or retry in a loop
2. Do not apologise repeatedly
3. Output a plain text copyable schedule:

```
--- COPY TO CALENDAR ---
[Day, Date]: [Activity], [Time], [Location]
...
--- END ---
```

4. Say: "Calendar tools aren't connected right now — here's the schedule to copy in manually."
5. Still write the session log entry to `logs/sessions.md` as normal

This applies to all calendar-related commands, including `/plan-week`.

## Standard event format

When creating activity events:

```
title: [Activity name] — Harry
location: [Full address]
duration: as per activity schedule
reminders: 30 minutes before (default)
description: [cost, booking notes, contact, anything useful]
```

## Term 2 activity schedule (ends July 1)

| Day       | Activity                            | Time         | Location                                      | Cost | Notes                                        |
|-----------|-------------------------------------|--------------|-----------------------------------------------|------|----------------------------------------------|
| Monday    | —                                   | —            | —                                             | —    | Open slot                                    |
| Tuesday   | Willoughby Playgroup (Gymboree)     | 12pm         | 56–58 Laurel St, Willoughby (Scouts Hall)     | Free | Park on Hollywood Cres or Laurel St          |
| Wednesday | Baby Time                           | 11am         | Chatswood Library                             | Free | Booking: libraries.willoughby.nsw.gov.au/… |
| Thursday  | Supported Playgroup Artarmon        | 10–11:30am   | 18 Broughton Rd, Artarmon (Kids Cottage)      | Free | Contact: 9410 0174 / spns@integricare.org.au |
| Friday    | —                                   | —            | —                                             | —    | Open slot                                    |

Note: Glenaeon Steiner Playgroup has been removed (too expensive at $35/session).

## Wake window rule

Never schedule an outing that starts within 30 minutes of a nap window.
Current nap windows: 11:00am and 3:00pm.
Ideal outing start: 8:30–10:00am or 12:30–2:00pm.

Wednesday Baby Time at 11am is the exception — it is the published class time and is an established activity.

## Term dates

- Term 2 end: **July 1, 2026**
- **June 8**: Public holiday — no Monday session
- **June 22**: Flag to Ryan — "Term 2 ends in 9 days — time to research Term 3 options"
- Term 3 start: approximately July 20, 2026 (confirm with Ryan)
- Flag in last week of June: "Term 2 ends this week — use /plan-week to set up Term 3 activities"

## /plan-week workflow

1. Call `list_events` for the coming week
2. Read `state-index.md` for current routine and flags
3. Read `activity-tracker.md` for active schedule and to-try list
4. Read last 3 entries from `logs/sessions.md` if it exists
5. Propose the week as one line per day
6. Show proposed plan to Ryan and ask once: "Update calendar?"
7. On confirmation, call `create_event` / `update_event` / `delete_event` in one shot
8. Write one line to `logs/sessions.md`
