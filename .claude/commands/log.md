# /log — Daily Log Entry

Completely optional. The system functions without it. If Ryan uses it, great — extract what you can.

Ryan describes his day conversationally. As much or as little as he wants. Do not prompt him for more detail — work with what you get.

## What to extract (from whatever Ryan says)

- **Food / formula** → `logs/feeds.md`
- **Naps / sleep** → `logs/sleep.md`
- **Activities** → `logs/activities.md`
- **Development observations** → `logs/milestones.md`

Also:
- `food-tracker.md` — if a new food was tried or a reaction noted
- `activity-tracker.md` — if an activity was attended (increment attendance count, add brief note)

Write to each relevant file immediately. Do not wait. Do not batch.

## Entry format (per log file)

Each entry is a single dated line, or a short list under a date heading if there's more to record. Keep it tight.

Example for `logs/feeds.md`:
```
2026-05-03: Avocado fingers — ate most of it, big fan. Formula ~650ml.
```

Example for `logs/sleep.md`:
```
2026-05-03: Nap 1 45min (short), Nap 2 1hr 20min. Settled well both times.
```

Example for `logs/activities.md`:
```
2026-05-03: Baby Time (Chatswood Library) — loved the singing, very engaged.
```

## Session line

Always write one line to `logs/sessions.md` (newest first):
```
2026-05-03: /log — solids, naps, Baby Time.
```

## Response format

After writing:
- One sentence confirming what was logged (skip if nothing to log)
- One optional flag for tomorrow if something stood out
- That's it — no summaries, no lists, no paragraphs

## Handling minimal input

If Ryan says "good" or "fine" — log what you can (date, "uneventful day") and move on. Do not interrogate.

If Ryan says nothing useful — write nothing to the topic files. Just write the session line.
