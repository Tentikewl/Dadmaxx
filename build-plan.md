# Dad Max — Build Plan
Generated from grill session 2026-05-01. All decisions final.

## What we're building
A Claude Code paternity leave assistant for Ryan. Primary product is calendar management.
Logging is optional enrichment, never mandatory. System must function without Ryan logging anything.

---

## Architecture decisions

### File loading (session startup)
- Load `state-index.md` ONLY at session start — tiny, ~20 lines, always current
- All other files loaded lazily, only when relevant to what Ryan says
- File routing is invisible to Ryan — no "loading X file" narration
- Greet Ryan with one line: date + today's activity + any flag from last session

### File structure (final)
```
state-index.md              ← always loaded, tiny snapshot
harrison-state.md           ← loaded when routine/rules/goals discussed
food-tracker.md             ← loaded when food discussed
activity-tracker.md         ← loaded when activities/planning discussed
calendar-skill.md           ← reference for calendar MCP usage
logs/
  sessions.md              ← one-liner per session (date + summary)
  feeds.md                 ← formula amounts, solids sessions, reactions over time
  sleep.md                 ← nap times, settling notes, patterns over time
  activities.md            ← activity sessions log, how they went
  milestones.md            ← developmental suggestions given + observations
```

### Mid-session writes
- Claude writes to files whenever alignment is reached on something
- NOT on every response — only when something is decided or recorded
- Never batch writes to end of session (session may close without warning)

### Routine updates
- Claude updates `harrison-state.md` based on conversation naturally
- No special trigger phrase needed — if Ryan describes a pattern, Claude updates
- If a nap pattern looks like it's shifting, Claude flags it: "looks like nap 1 is shortening — want me to update the routine?"

---

## Activity tracker decisions

### Status system
Every activity has one of these statuses:
- `active` — on the current schedule
- `dropped` — tried, didn't work, not returning
- `on-hold` — paused temporarily
- `to-try` — candidate, not yet scheduled

### Drop/replace workflow
1. Ryan mentions an activity was bad (conversationally, no special command)
2. Claude marks it `dropped` with a note
3. Claude opens a brainstorm — pulls from to-try list, suggests options
4. Ryan picks one or they work it out together
5. Claude updates activity-tracker + fires calendar update
6. All days equal — no special logic for Monday vs Friday

### To-try list
Lives in `activity-tracker.md`. Claude populates it from `/suggest` outputs and anything Ryan mentions. `/plan-week` pulls from here when a slot is open.

### Term 2 calendar flags
- June 8: public holiday — no Monday session (Monday has 9 sessions total, Tue/Wed have 10)
- June 22: proactive flag — "Term 2 ends in 9 days — time to research Term 3 options"
- July 1: Term 2 ends — all recurring activities stop

---

## Current activity schedule (Term 2, post-grill)

| Day       | Activity                        | Time         | Location                              | Cost | Notes |
|-----------|---------------------------------|--------------|---------------------------------------|------|-------|
| Monday    | —                               | —            | —                                     | —    | Open slot |
| Tuesday   | Willoughby Playgroup (Gymboree) | 12pm         | 56–58 Laurel St, Willoughby (Scouts Hall) | Free | Park on Hollywood Cres or Laurel St. Arrive 5 min early |
| Wednesday | Baby Time                       | 11am         | Chatswood Library                     | Free | Booking: libraries.willoughby.nsw.gov.au/Eventbrite/Baby-Time-292937432747 |
| Thursday  | Supported Playgroup Artarmon    | 10–11:30am   | 18 Broughton Rd, Artarmon (Kids Cottage) | Free | Contact: 9410 0174 / spns@integricare.org.au |
| Friday    | —                               | —            | —                                     | —    | Open slot |

Steiner Playgroup: REMOVED (too expensive at $35/session).

---

## Slash command decisions

### /log
- Completely optional — system works without it
- Ryan describes day conversationally, Claude extracts everything
- Writes to relevant logs/ files immediately (not at session end)
- No confirmation needed — Claude just does it

### /debrief
- Fast, 2 minutes max
- 3 questions max, warm tone
- Writes immediately after Ryan responds

### /plan-week
- Reads state-index + activity-tracker + last 3 sessions.md entries
- Shows one-line-per-day plan to Ryan
- One confirmation: "Update calendar?"
- Then executes all calendar changes in one shot
- Graceful degradation: if calendar MCP not connected, outputs plain text plan
- Checks nap windows before placing any activity
- Pulls from to-try list for open slots

### /suggest
- Outputs exactly 3 things: one food, one activity, one developmental focus
- Reads milestones.md — NEVER repeats a previous suggestion
- Developmental focus: concrete in-the-moment play action, not theory
  - Good: "When Harry drops a toy, pick it up slowly in front of him and watch his reaction"
  - Bad: "Harrison is developing object permanence this month"
- Food: next item from food-tracker to-try list, or next allergen to introduce
- Activity: pulls from to-try list or suggests something for an open slot

### /grill-me
- Already installed (coderocketai skill)
- No changes needed

---

## Developmental suggestions
- Claude's general knowledge is sufficient — no static reference file needed
- All suggestions tracked in `logs/milestones.md`
- Future: `/research` command for periodic web scan of age-appropriate activities (not in this build)

---

## End of paternity leave
- No handover doc for Jessie
- In August, Claude proactively prompts: "Paternity leave is wrapping up — worth thinking about childcare and back-to-work arrangements"
- No special command needed — Claude flags it based on the date

---

## state-index.md format (target)
```markdown
# State Index
Last updated: [date]

Today: [day] — [activity name] at [time] or "no activity scheduled"
Last session: [date]
Flags: [one line from last session, or "none"]

Routine snapshot:
- Wake: 8:00am | Nap 1: 11am | Nap 2: 3pm | Bed: 8pm
- Formula target: 600–800ml/day
- Max wake window: 2.5hr

Harrison: 8 months, 9kg
```

---

## Build slices (vertical — each touches all layers)

### Slice 1: Session foundation
**Goal:** Ryan opens a session, gets a one-line useful greeting, right files load.
**Touches:** `state-index.md` (create), `CLAUDE.md` (update startup logic), `activity-tracker.md` (read today's activity)
**Done when:** Session startup reads state-index only, greeting includes today's activity and any flag.

### Slice 2: /plan-week + calendar
**Goal:** Ryan runs /plan-week and calendar gets updated.
**Touches:** `activity-tracker.md` (add status column + to-try section), `.claude/commands/plan-week.md` (rewrite), `calendar-skill.md` (update with degradation logic)
**Done when:** /plan-week shows one-line-per-day plan, one confirmation, executes calendar changes.

### Slice 3: Activity drop/replace workflow
**Goal:** Ryan says an activity was bad, system handles end-to-end.
**Touches:** `CLAUDE.md` (add drop workflow instructions), `activity-tracker.md` (status transitions), `.claude/commands/plan-week.md` (to-try list integration)
**Done when:** Ryan can say "that playgroup was terrible" and Claude marks dropped, brainstorms, updates files + calendar.

### Slice 4: Optional logging
**Goal:** Ryan describes his day, everything updates.
**Touches:** `logs/` directory (create all 5 files), `.claude/commands/log.md` (rewrite), `.claude/commands/debrief.md` (rewrite), `CLAUDE.md` (logging is optional, mid-session writes)
**Done when:** /log and /debrief write to topic files immediately; system still functions if never used.

### Slice 5: /suggest with memory
**Goal:** Ryan asks for a suggestion and never hears the same one twice.
**Touches:** `logs/milestones.md` (create), `.claude/commands/suggest.md` (rewrite with no-repeat logic + concrete dev actions)
**Done when:** /suggest outputs food + activity + concrete play action, all tracked in milestones.md.

---

## Build order
1 → 2 → 3 → 4 → 5. Each agent reads this file + current repo state. Commits after each slice.
