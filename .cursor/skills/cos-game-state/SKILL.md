---
name: cos-game-state
description: Tracks the live state of the Curse of Strahd Reloaded campaign — real player names, character names, classes/levels, current module/session pointer, items in hand, room layouts, NPC fates, and post-session reflections. Use whenever the user asks about who's playing, what character a player runs, where the party is in the campaign or in a building (rooms, floors, layouts), what session is next, who has which item, where an item or NPC is, what's in a specific room, what happened last session, or asks to update/prep/recap a session.
---

# Curse of Strahd Reloaded — Game State Tracker

This skill keeps a single source of truth for the live state of the campaign: who is at the table, what they play, where the party is in the story, and what the DM needs for the next session.

## The dictionary-lookup contract

The repo is the brain. Chat is the I/O. **Never** rely on context memory for player names, character names, classes, levels, item carriers, plot beats, NPC fates, room contents, layouts, or session pointers. If a fact isn't in `state.md` (or a file `state.md` links to), treat it as unknown and ask. When something changes during a conversation, write it back to the appropriate file immediately so the next read is fresh.

**Always trust files over your own memory.** If you've read a fact in this chat already but ten messages have passed, re-read the file before answering. Never paraphrase from memory when the file is one tool call away.

## Companion skills (the full pipeline)

| Phase | Skill | What it does |
|---|---|---|
| Pre-session | `cos-session-prep` | Reads state, generates the printable briefer + opening narrations + absent-player handwaves + numbered run-of-show |
| **During session** | **`cos-live-dm`** | **Rapid-fire mid-session help: "row 3 is done, what's next", "what's in this room", "DC for X", "the rogue rolled 17"** |
| During session (manual) | (DM drops bullets into `Campaign/Course/module_<N>/session_<M>/live_log.md`) | |
| Post-session | `cos-session-recap` | Ingests the live log + dictation, atomically updates state, writes recap.md, appends session log |
| Anytime lookup | **this skill** | Answers any roster/pointer/items/threads question by reading `state.md` first |

## The canonical state file

**`Campaign/Course/state.md`** is the only authoritative tracker for live game state. Read it first whenever the user asks about:

- Real player names or character names
- Class / level / HP / AC for any PC
- Which module and session the party is on (the "pointer")
- Where the party physically is in the world right now
- Who's carrying which item (amber shard, key, locket, disc, etc.)
- What happened last session and what's planned for next session
- **What's in a specific room, floor, or location** (state.md links to layout files like `death_house_layout.md`)

Other files (`party.md`, `module_1/session_*/recap.md`, layout files, etc.) are deep references; `state.md` is the at-a-glance dashboard that links into them. **Always traverse the link** — never answer geography or layout questions from memory.

## When to read

Read `Campaign/Course/state.md` at the start of any task that involves:

- Pre-session prep ("get me ready for tonight", "what do I need to print", "what's next")
- Post-session updates ("we just finished — update the tracker", "Mike's PC died", "Ben gave the shard to Jake")
- Roster questions ("who plays the rogue", "what's Scott's character name")
- Plot continuity ("where did we leave off", "did they meet Ireena yet", "is Doru resolved")
- **Geography / layout questions** ("what's in the storage room", "how do they get to the basement", "where's the music box", "which room has the toy chest"). After reading state.md, **follow the link to the relevant layout file** (e.g. `Campaign/Course/module_1/session_1/death_house_layout.md` for any Death House room question).

## When to update

Update `Campaign/Course/state.md` whenever any of these change:

- A real-life session completes — bump `Last session played` and `Next session` rows
- A character name, class, level, HP, or AC is confirmed or changes
- A key item changes hands or is acquired/lost
- The party moves to a new narrative beat (Floor 3 → basement → village of Barovia → Vallaki, etc.)
- A PC dies or returns
- A major NPC fate is decided (Doru destroyed/cured, Ireena's status, etc.)

When updating, also append a one-line entry to the `Session log` table at the bottom so history is preserved.

## What `state.md` must always contain

The state file MUST keep these sections, in this order, so any agent (or the DM at 5 minutes before kickoff) can scan it fast:

1. **Pointer** — module, narrative session folder, last RL session date, next RL session date, current narrative beat
2. **Roster** — one row per player: real name, character name, race, class, subclass, level, HP/AC/PP, status (Active / Down / Dead / Spirit)
3. **Items in play** — who carries the amber shard, iron key, Walter's disc, Klara's locket, Gustav's letter, plus any new artifacts
4. **Open threads / decisions pending** — checkbox list (Doru, Tarokka draws, etc.)
5. **Last session post-mortem** — what worked, what was rough, what to fix next time
6. **Next session prep checklist** — short, scannable, with file links
7. **Session log** — append-only table: date, RL session #, narrative beat, level at end, notable outcome

## Editing rules

- **Never** delete history from the `Session log` — only append.
- When a value is unknown, write `?` or `(confirm at table)` rather than guessing. The DM would rather see a hole than a fabrication.
- Cross-link to deep files instead of duplicating their content. E.g. for full ability lists, link to `Campaign/Course/party.md`; for amber shard mechanics, link to `Campaign/Items/quest_items/elisabeth_amber_shard.md`.
- Keep the file under ~200 lines. If it grows, push detail into linked files.

## Quick lookups

- Full ability/spell breakdowns per PC → `Campaign/Course/party.md`
- Per-session character item tracker (Death House) → `Campaign/Course/module_1/session_1/characters.md`
- **Death House every-room reference (geography, what's in each room, by floor)** → `Campaign/Course/module_1/session_1/death_house_layout.md`
- Module 1 navigation (which folder has what) → `Campaign/Course/module_1/README.md`
- Campaign overview / 4-month schedule → `Campaign/Course/README.md`
- Death & resurrection rules → `Campaign/Course/rules/death_and_resurrection.md`
- D&D 5e DM rules quick reference (DCs, conditions, action economy) → `Campaign/Course/rules/dm_quickref.md`

**Layout files pattern:** as the campaign moves to new locations (Village of Barovia, Vallaki, Castle Ravenloft, Amber Temple), create one `*_layout.md` per major location and link it from `state.md`. This is the dictionary-lookup contract for geography.
