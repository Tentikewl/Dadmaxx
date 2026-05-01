# /suggest — Weekly Suggestions

No preamble. No "here are my suggestions." Just the three items.

---

## Step 1 — Load context

Read these files in order:
1. `state-index.md` — Harrison's current age and routine
2. `food-tracker.md` — foods introduced, to-try list, allergen table
3. `activity-tracker.md` — to-try list, active/dropped activities
4. `logs/milestones.md` — ALL previous suggestions (every entry, every line)

---

## Step 2 — Generate 3 suggestions (no repeats, ever)

Before generating anything, scan every line of `logs/milestones.md`. A suggestion is disqualified if it matches anything already recorded there — food name, activity name, or the gist of a dev focus. If milestones.md has 30 entries, suggestion 31 must still be fresh.

### 1. Food this week

- Take the first item from the `food-tracker.md` **to-try list** that has not already been suggested in `logs/milestones.md`.
- If the to-try list is exhausted, move to the **allergen table** and suggest the next allergen that has not yet been introduced (in order: Peanut → Tree nuts → Dairy (full) → Wheat (full) → Soy → Sesame → Fish → Shellfish).
- Add one practical sentence on how to serve it — no elaborate prep, no multiple steps.

### 2. Activity idea

- Take the first item from the `activity-tracker.md` **To Try** table that has not already been suggested in `logs/milestones.md`.
- If the To Try table is empty or all entries are already in milestones.md, suggest something specific for Monday or Friday (the open slots) that fits within the nap window schedule (nap 1 ≈ 11am, nap 2 ≈ 3pm — outings should not cut into either window).
- Must not have been suggested before (check milestones.md).
- Add one sentence: best time of day given the nap windows.

### 3. Developmental focus

- A single, concrete, in-the-moment play action tied to Harrison's current age.
- Format: what to do + what it develops. Example: "When Harry drops a toy, pick it up slowly in front of him and watch his reaction — you're testing object permanence."
- Must be specific and actionable — not vague theory.
  - GOOD: "Hold a toy just out of reach to his left side — watch him rotate his trunk to grab it, that's core strength and midline crossing."
  - BAD: "Harrison is developing object permanence this month."
- Must not repeat the gist of anything already in `logs/milestones.md`.
- Use Claude's general knowledge of 8-month developmental milestones — no static reference file needed.

---

## Step 3 — Write to milestones.md immediately

After generating the three suggestions, append this line to `logs/milestones.md`:

```
[YYYY-MM-DD]: Food suggested: [food name]. Activity suggested: [activity name]. Dev focus: [one-line summary of the play action].
```

Write this **before** outputting the response. This is the memory that prevents repeats in future sessions.

---

## Step 4 — Output format

Respond with exactly this, nothing more:

---
**Food this week:** [food] — [how to serve, one sentence]

**Activity idea:** [activity] — [where/when, one sentence]

**Developmental focus:** [the specific play action + what it develops]

---
