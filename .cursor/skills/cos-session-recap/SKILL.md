---
name: cos-session-recap
description: Closes a Curse of Strahd Reloaded session — ingests live bullets (live_log.md, the user's after-session dictation, or whatever notes exist) and atomically updates the canonical state, writes a clean recap.md, and appends a row to the session log. Use when the user says "recap last night", "we just finished — update the tracker", "process my bullets", "Mike's PC died, update everything", "the rough session never got recapped, here's what happened", or any post-session ingest request.
---

# Curse of Strahd Reloaded — Session Recap

Post-session pipeline. Treats every recap as a transaction: read existing state, ingest new events, write the diff to every file that needs it, never lose history.

## Input contract

Always read these before writing anything:

1. **`Campaign/Course/state.md`** — current canonical state
2. **`Campaign/Course/module_<N>/session_<M>/live_log.md`** — bullets captured during play (if it exists)
3. The user's post-session message — anything they dictated that isn't in the live log
4. **`Campaign/Course/module_<N>/session_<M>/recap.md`** — existing recap stub (template to fill, or previous recap to extend)

If the live log is empty AND the user has nothing to dictate, ask what happened in 5–10 bullets before generating anything.

## Output contract

Every recap MUST update **all four** of these in one pass. Never write one without the others.

| File | Update |
|---|---|
| `Campaign/Course/state.md` — Pointer | New beat, last RL session date/#, next session date if known, in-game date if advanced, long-rest status |
| `Campaign/Course/state.md` — Roster | Levels, **current HP** (not just max), status (Active / Down / Dead / Spirit), any new conditions or curses, **once-per-session abilities used** (e.g. Mike's bonus action divine smite — track if spent and not yet recharged) |
| `Campaign/Course/state.md` — Items in play | Carrier changes, new items, lost items, items used up |
| `Campaign/Course/state.md` — Open threads | Tick boxes that resolved; add new threads opened; preserve unresolved ones |
| `Campaign/Course/state.md` — Last session post-mortem | Replace with this session's reflections; preserve format |
| `Campaign/Course/state.md` — Session log | **Append** one row. Never delete. |
| Recap file (see naming below) | Fill the template sections (What Happened, Key Decisions, Character Moments, Plot Threads, Where We Left Off, XP/Milestone, Continuity Notes, DM Reflections) |

## Recap file naming — handle multi-RL-session narrative folders

A "narrative session folder" (e.g. `module_1/session_1/`) does **not** equal one real-life session. Death House routinely takes 2–3 RL sessions to complete inside `module_1/session_1/`. Use this naming so each RL session has its own recap file:

| RL session | File path |
|---|---|
| First RL session in a narrative folder | `module_<N>/session_<M>/recap.md` |
| Second RL session in same narrative folder | `module_<N>/session_<M>/rl_session_<K>_recap.md` |
| Third RL session in same narrative folder | `module_<N>/session_<M>/rl_session_<K>_recap.md` |

Where `<K>` is the global RL session counter (counts across all narrative folders since RL #1). Example: if RL session 2 happened in `module_1/session_1/`, the file is `module_1/session_1/rl_session_2_recap.md`. The legacy `recap.md` is reserved for RL #1 only and should not be overwritten.

When a new narrative folder begins (e.g. party reaches Barovia, transitioning to `module_1/session_2/`), the first RL session in that folder gets `recap.md` again.

## Tracking categories — make sure each recap captures these

Every recap and state.md update MUST address each of the following if it changed during the session:

- **Current HP** for every PC at session end — not just max
- **Long-rest status** of the current location — blocked? available? partial?
- **Once-per-session / once-per-rest abilities used** — Paladin's bonus action divine smite (if houseruled), Sorcery Points, Action Surge, etc. Note explicitly which are spent and when they recharge.
- **Lay on Hands pool remaining** for any Paladin
- **Spell slots used** if the DM tracks them between sessions (some don't — confirm with DM)
- **Hit Dice spent** during short rests
- **Items collected, dropped, traded, or used up** — every transaction
- **NPC fates resolved** (destroyed, cured, allied, hostile)
- **Plot threads opened or closed**
- **Player attendance** — who was at the table; who their PC is narratively positioned as if absent
- **DM houserules invoked** — record so consistency is maintained next session

## Workflow

```
Recap Workflow:
- [ ] Step 1: Read state.md, live_log.md, existing recap.md
- [ ] Step 2: Confirm session metadata (date, RL session #, players present, level at end)
- [ ] Step 3: Diff — what changed in roster, items, pointer, threads?
- [ ] Step 4: Write recap.md (clean prose from bullets)
- [ ] Step 5: Update state.md (all six sections listed above)
- [ ] Step 6: Append session log row
- [ ] Step 7: Show DM the diff and ask for confirmation before writing
- [ ] Step 8: Clear or archive live_log.md ready for next session
```

## Recap.md template adherence

Use the section headers already present in the repo's recap files. If a stub exists, fill it; do not rename headers. Required sections:

- What Happened (Summary) — 4–8 sentences, prose
- Key Decisions Made — bullets, each tied to a downstream consequence
- Character Moments — one bullet per PC present, preserving spotlight balance
- Plot Threads Opened
- Plot Threads Resolved
- Where We Left Off — physical location + party condition + immediate next decision facing them
- XP / Milestone — what level the party is at session end; whether a milestone triggered
- Continuity Notes — anything that affects future sessions (NPC fates, items lost/gained, curses, debts)
- DM Reflections — what worked, what was rough, fixes for next session

## Session log row format

Append to the table at the bottom of `state.md`:

```
| <RL #> | <YYYY-MM-DD> | <narrative folder> | <one-line beat covered> | <level at end> | <one notable outcome> |
```

## Backfilling a missed session

If the user says "we never recapped session X", run the same workflow but:

- Do not advance the pointer past where the most-recent session actually ended
- Insert the missed row in correct chronological order in the session log (don't append out of order)
- If the missed session has no live log, ask 5–10 questions before writing — never invent

## Diff confirmation

Before writing to `state.md` and `recap.md`, show the DM a short summary of the diff:

```
About to update:
  state.md → Pointer beat: "<old>" → "<new>"
  state.md → Roster: Mike level 2→3, Jason curse cleared
  state.md → Items: Iron Key → Ben (was unknown)
  state.md → Threads: Doru (resolved: destroyed) — added Continuity row
  recap.md → Filling Session 3 stub (8 sections)
  Session log → +1 row: 2026-04-24 | Floor 3 → basement | L3 | Flesh Mound defeated

Proceed? (Y/n)
```

If the DM declines or amends, do not write. Iterate.

## Anti-patterns

- **Never** silently overwrite the previous post-mortem before logging this session's reflections — if the previous one was unaddressed, surface it ("last week's rough-session post-mortem still has open items: <list>").
- **Never** delete or rewrite past `Session log` rows.
- **Never** advance the in-game calendar arbitrarily. Tie every advance to an explicit player action.
- **Never** invent NPC dialogue, item descriptions, or game outcomes that weren't in the bullets. Ask if unsure.
