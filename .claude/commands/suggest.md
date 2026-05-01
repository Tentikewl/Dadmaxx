# /suggest — Weekly Suggestions

Provide three targeted suggestions based on current state and log history.

## Inputs to read first

1. `harrison-state.md` — current age, routine, goals
2. `food-tracker.md` — what's been tried, what's next, allergen status
3. `activity-tracker.md` — what's worked, what's been missed
4. `harrison-log.md` — last 3 entries for recent pattern

## Output format

Respond with exactly three suggestions, brief and practical:

---
**Food this week:** [one food + why + how to serve it]

**Activity idea:** [one specific activity for an unscheduled slot + best time window given naps]

**Developmental focus:** [one thing to lean into this week given Harrison's current age/stage + one concrete way to do it]

---

## Rules

- Food: prioritise next item from food-tracker.md to-try list, or an allergen not yet introduced
- Activity: match to a real gap in the week (usually Friday or a cancelled session slot)
- Development: age-appropriate, based on 8-month milestones — gets more specific as log fills up
- Keep it doable for one person with an infant. Nothing elaborate.

## As the log grows

Early sessions: suggestions based on baseline state.
After 2+ weeks: use log patterns — e.g. if nap 1 is consistently short, suggest adjusting the morning outing timing.
