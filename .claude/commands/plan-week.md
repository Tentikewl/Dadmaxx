# /plan-week — Weekly Planning and Calendar Update

Read the current calendar, state files, and log. Propose the week. Execute calendar updates on confirmation.

## Step 1 — Gather context

1. Call `list_calendars` to identify the right calendar
2. Call `list_events` for the next 7 days
3. Read `harrison-state.md`
4. Read last 3 entries of `harrison-log.md`
5. Read `food-tracker.md` for what to introduce this week
6. Read `activity-tracker.md` for attendance gaps and patterns

## Step 2 — Build the week plan

Propose:

1. **Activities** — which Term 2 sessions to attend each day, whether to book (Monday needs booking)
2. **Food** — one new food to introduce this week and which day
3. **Flex day (Friday)** — specific outdoor or ad hoc activity suggestion
4. **Routine note** — anything to adjust based on recent log patterns

Check nap window rules before placing any outing:
- Nap 1: ~11:00am → outings should start by 9:30am or after 12:15pm
- Nap 2: ~3:00pm → outings should end by 2:30pm or start after 5:15pm

## Step 3 — Present the plan

Show Ryan a concise summary:

```
Week of [date]

Mon: Glenaeon Playgroup 9:30am (booking needed — confirm?)
Tue: Willoughby Playgroup 12pm
Wed: Baby Time Library 11am
Thu: Artarmon Supported Playgroup 10am
Fri: [specific suggestion]

New food: [food] on [day]
Focus: [one developmental note]
```

Ask: "Want me to update the calendar with this?"

## Step 4 — Execute on confirmation

On Ryan's go-ahead:
- `create_event` or `update_event` for each session not already in calendar
- Add 30-minute reminders to all activity events
- Delete any conflicting placeholders

## Step 5 — Log the plan

Append a brief "Week plan" entry to `harrison-log.md`.

## Term end flag

If current date is within 7 days of July 1: include a reminder — "Term 2 ends this week. These recurring activities won't continue. Run /plan-week after July 1 to set up Term 3."
