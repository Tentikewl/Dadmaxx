# /log — Daily Log Entry

Ryan will describe his day conversationally. Extract and record everything automatically.

## What to extract

From Ryan's description, identify:

1. **Foods** — what was offered, what was eaten, how much, any reactions or faces made
2. **Formula** — total ml across the day if mentioned
3. **Naps** — actual times vs planned, how long, how easy to settle
4. **Activities** — what was done, how Harrison responded, energy level
5. **Mood / development** — anything notable (new skill, fussy period, teething signs, etc.)
6. **Deviations from routine** — anything that shifted the usual schedule
7. **What worked / what didn't** — Ryan's own read on the day

## What to do with it

1. Append a dated entry to `harrison-log.md` with a clean summary of the above
2. Update `food-tracker.md` if any new foods were tried or reactions noted
3. Update `activity-tracker.md` if activities happened (mark attended weeks, add notes)
4. Update `harrison-state.md` if anything has structurally changed (new routine, weight, goals)

## Response format

After logging, reply with:
- One sentence confirming what was logged
- One observation or encouragement (keep it brief)
- Any flag worth noting for tomorrow (e.g. "Harry seemed off solids — worth watching tomorrow")

Do not ask Ryan to confirm the log. Just do it.

## Example

Ryan: "Pretty good day. He smashed the avocado fingers — ate basically all of it. Nap 1 was only 45 min, bit of a disaster. Went to the library Baby Time, he loved the singing."

Claude extracts:
- Food: avocado fingers, eaten enthusiastically (first time)
- Nap 1: 45 min (short), settled okay
- Activity: Baby Time at Chatswood Library, positive response to singing
Then logs, updates food-tracker (avocado: positive), updates activity-tracker (Wednesday library: attended).
