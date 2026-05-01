# /plan-week — Weekly Planning and Calendar Update

Read state files and activity tracker. Propose the week as one line per day. Execute calendar updates on confirmation.

## Step 1 — Gather context

1. Read `state-index.md` — routine snapshot, current flags
2. Read `activity-tracker.md` — active schedule, dropped activities, to-try list
3. Read last 3 entries from `logs/sessions.md` if the file exists — skip gracefully if it doesn't

Do not narrate the file loading to Ryan.

## Step 2 — Build the week plan

For each day Mon–Fri:
- If a day has an `active` activity, slot it in at the listed time
- If a day is open (Monday / Friday), check the to-try list and suggest one candidate
- If the to-try list is empty, leave the day as "Open — no activity" (do not invent activities)
- Check for any activities marked `on-hold` — if a slot is open and Ryan hasn't mentioned returning to it, leave the slot open rather than auto-restoring it.

Before placing any activity, verify it clears nap windows:
- Nap 1: ~11:00am → activity must start by 9:30am OR start at 12pm or later
- Nap 2: ~3:00pm → activity must end by 2:30pm OR start after 4:30pm

Wednesday Baby Time (11am) starts exactly at Nap 1 — flag if this is a concern, but keep it in the plan (it is the established time).

## Step 3 — Show plan and ask once

Present the plan as one line per day, then ask exactly once:

```
Week of [Mon date] – [Fri date]

Mon: Open — no activity
Tue: Willoughby Playgroup (Gymboree), 12pm — 56–58 Laurel St
Wed: Baby Time, 11am — Chatswood Library
Thu: Supported Playgroup Artarmon, 10am — 18 Broughton Rd
Fri: Open — no activity

Update calendar?
```

Do not ask for further confirmation or elaboration. One question only.

## Step 4 — Execute on confirmation

If Ryan says yes (any affirmative):
- Calendar ID is always `18rgavo@gmail.com` — do NOT call `list_calendars`
- Call `list_events` for the week to check what's already there
- Daily routine events (Wake, Breakfast, Brush teeth, Nap 1, Milk, Nap 2, Dinner solids, Bath, Brush teeth evening, Bedtime milk) are already recurring — do NOT recreate them
- For each activity not already in calendar: call `create_event`
- For any conflicting or outdated event: call `update_event` or `delete_event`
- Add 30-minute reminders to all activity events (30 min = departure time from Artarmon, intentional)
- Standard event format:
  - title: `[Activity name] — Harry`
  - location: full address
  - description: cost, contact, booking notes + drive time + "Leave by [time]" (see drive times in `calendar-skill.md`)

Execute all changes in one shot — do not ask again before each event.

## Step 5 — Graceful degradation

If any MCP calendar tool returns an error or is unavailable:
- Do not fail or apologise repeatedly
- Output a plain text copyable schedule instead:

```
--- COPY TO CALENDAR ---
[Day, Date]: [Activity], [Time], [Location]
...
--- END ---
```

Then say: "Calendar tools aren't connected right now — here's the schedule to copy in manually."

## Step 6 — Write session log

After completing (whether calendar was updated or not), write one line to `logs/sessions.md`:

```
[YYYY-MM-DD]: /plan-week — week of [Mon date], [N] activities scheduled
```

If `logs/sessions.md` doesn't exist yet, create it with that line as the first entry.

## Term 2 flags

- **June 8**: No Monday session (public holiday) — note in the plan
- **June 22**: Add flag — "Term 2 ends in 9 days — time to research Term 3 options"
- **July 1**: Term 2 ends — remind Ryan that recurring activities stop and /plan-week will need fresh input for Term 3
