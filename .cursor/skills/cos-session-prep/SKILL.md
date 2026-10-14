---
name: cos-session-prep
description: Generates pre-session prep for the Curse of Strahd Reloaded campaign — reads the live state file, produces the printable briefer (current pointer, roster snapshot, items in play, open threads), and drafts opening narrations ("Previously on", cold open, any handoff/handwave scenes for absent players). Use when the user says "prep tonight", "get me ready", "session is in X minutes", "write the cold open", "who's missing tonight, write the workaround", or any pre-kickoff prep request.
---

# Curse of Strahd Reloaded — Session Prep

Pre-session pipeline. Reads the canonical state, produces a one-page DM briefer plus opening narrations.

## Input contract

Always run these reads BEFORE generating anything. Do not rely on context memory.

1. **`Campaign/Course/state.md`** — the pointer, roster, items in play, open threads, last post-mortem
2. **`Campaign/Course/module_<N>/session_<M>/plan.md`** — beat-level prep for the current narrative folder (use the `Module` and `Narrative session folder` from the state pointer)
3. **`Campaign/Course/module_<N>/session_<M>/plot.md`** — DM script for the upcoming scenes (only the section the pointer says they're entering)
4. The most recent **`recap.md`** in the relevant session folder — for "Previously on" continuity
5. The most recent **`live_log.md`** in the relevant session folder, if any — for any unrecapped session bullets

## What to ask the DM (1 question, max)

Before generating, if any of these are unknown, ask in **one** consolidated question:

- Who's at the table tonight? (real names — confirms the roster delta vs. `state.md`)
- Is the pointer current? (i.e. did anything change since `state.md` was last written?)

If the live log shows a session that wasn't recapped, also ask: "I see uncaptured bullets in `live_log.md` for session X — should I recap that first, or write tonight's prep on top of it?"

## Output — produce in this order

### 1. The briefer (printable, one page)

```markdown
# Tonight — <date> — Module <N>, Session <M> attempt <K>

## Pointer
- Beat: <where they are right now, in 1 line>
- Level start: <N>
- In-game date: <date>

## At the table
| Real | Character | Class | Level | HP / AC | Status flags |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

**Absent:** <list, with their PCs' fates handwaved — link to narration section>

## Items the party has on them
- ...

## Open decisions to resolve at the table (60 seconds)
- ...

## Encounter risks tonight
- ...   *(pull from level_scaling.md and the upcoming plot.md beats)*

## DM checklist (load in order)
- [ ] ...
```

### 2. Opening narrations

Write three sub-pieces, each marked clearly:

- **"Previously on"** — paraphrasable, ~60 seconds, focused on the 4–6 things that matter for tonight's beats. Cite item carriers and active conditions (curses, wounds, bonds).
- **Cold open** — read aloud, present-tense, sensory, ends on a beat the players can react to.
- **Absent-player handwaves** — for each missing player, a 2–3 sentence narrative excuse that:
  - Keeps the PC alive unless the DM has already approved a death
  - Hands off any critical items the absent PC was carrying to a present PC, with a one-line in-fiction reason
  - Says explicitly "the PC is unreachable, not gone" so the absent player can return next session without ceremony

### 3. Numbered run-of-show (the spine of the night)

Produce a flat numbered list of every step the DM will walk through, in narrative order. Each row has:

- A **bold short title** describing the premise of the step (e.g. "The Trunk Opens", "Klara at the Threshold")
- A one-to-two sentence description of what happens

Rules for the run-of-show:
- **Highlight any prop / handout / read-aloud step as its own called-out row** with a divider above and below, the prop's text in a blockquote, and a short "why this matters" note. Examples: a letter from Strahd, a Tarokka draw, a death-note from an NPC, anything the DM hands to the players.
- **Include the actual canonical text** for read-alouds, derived from `plot.md` or source files. Do not paraphrase.
- **End with a "where to cliffhang" suggestion** if the night might run long — pick 2–3 natural stop points by step number.
- Save the run-of-show as `Campaign/Course/module_<N>/session_<currentNarrativeFolder>/rl_session_<K>_run_of_show.md` and link it from `state.md` as the night's primary reference.

### 4. Mood / pacing reminders

3–6 short bullets. Pull from the upcoming scenes' tone notes in `plot.md`. Flag:
- Any save risks where active conditions stack (e.g. cursed PC + WIS save scene)
- Any moment where a previously injured PC is at lethal risk if not healed
- Any music/audio cues that close earlier loops

## Where to save the output

Save the narrations to a dedicated file so they survive the chat:

`Campaign/Course/module_<N>/session_<M>/session_<K>_cold_open.md`

(Example pattern already in repo: `module_1/session_1/session_2_gm_flow.md`, `module_1/session_1/session_3_cold_open.md`.)

Update `state.md`'s "Next session prep checklist" so the new file is the first link.

## Anti-patterns

- **Never** invent character names, races, levels, or item carriers. If unknown, write `?` and surface to the DM.
- **Never** kill an absent player's PC for narrative convenience.
- **Never** advance the pointer in `state.md` before the session actually plays. Prep predicts; recap commits.
- **Never** copy long passages of `plot.md` into the briefer. Link to it.
