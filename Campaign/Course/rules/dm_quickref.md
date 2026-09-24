# DM Quick Reference — D&D 5e Basics

> One-page reference for the DM mid-session. Skill checks, saves, common rulings, and the short-form "what does X mean" lookups.

---

## DC — Difficulty Class

The target number on `d20 + modifier` to succeed at a check or save. Player **meets or beats** the DC = success.

| DC | Difficulty | Use for |
|---|---|---|
| 5 | Very easy | Trivial — usually skip the roll |
| 10 | Easy | A trained person succeeds most of the time |
| **13** | **Moderate** *(default)* | Most checks; basic traps, common locks |
| 14–15 | Hard | Skilled professional succeeds about half the time |
| 17 | Very hard | Specialist territory |
| 20 | Nearly impossible | Hero moment |
| 25+ | Legendary | Reserve for cinematic stakes |

**Calling a check at the table:**
1. Player describes action.
2. DM decides if outcome is uncertain. If not — just say yes/no.
3. DM picks ability + difficulty. Default DC 13.
4. *"Make a [skill] check."* Player rolls. DM rules.

---

## Ability mapping (which ability for what)

| Ability | Use it for |
|---|---|
| **STR** | Force a door, lift, grapple, shove, swim against current |
| **DEX** | Stealth, sleight of hand, acrobatics, dodge a falling thing, pick a lock (sometimes) |
| **CON** | Hold breath, resist poison/disease, endurance |
| **INT** | Investigation, Arcana, History, recall lore |
| **WIS** | Perception, Insight, Survival, Medicine, Animal Handling |
| **CHA** | Persuasion, Deception, Intimidation, Performance |

> Common new-DM trip: **Religion is INT, not WIS.** Recall facts about gods = INT (you're remembering). Sense the holiness of a place = WIS.

---

## Action economy (what a creature can do on its turn)

Per turn, a creature gets:
- **1 Action** — attack, cast a spell, dash, dodge, disengage, help, hide, ready, search, use an object
- **1 Bonus Action** — only if a feature/spell explicitly grants one (Cunning Action, Healing Word, Flurry of Blows, etc.)
- **1 Reaction** — only when triggered (opportunity attack, Shield spell, etc.). Resets at start of turn.
- **Movement** — up to your speed (default 30 ft.), can be split before/after action
- **Free interactions** — draw a weapon, open a door, speak a few words. One per turn unless the DM allows more.

---

## Common saves and their DCs in this campaign

| Save | What it resists |
|---|---|
| **STR** | Being shoved, knocked prone, restrained by force |
| **DEX** | Area effects (fireball, dart traps, falling) |
| **CON** | Poison, disease, exhaustion, maintaining concentration on spells |
| **INT** | Mental intrusion, illusions, psychic attacks (rare) |
| **WIS** | Charm, frighten, possession, mental domination |
| **CHA** | Banishment, soul attacks (rare) |

---

## Healing math (level 3 reminders)

| Source | Effect |
|---|---|
| **Lay on Hands (Paladin)** | Pool = 5 × Paladin level (15 at L3). Touch, restore HP up to remaining pool. Or 5 from pool to cure 1 disease/poison. |
| **Cure Wounds (L1 slot)** | 1d8 + spellcasting mod. Touch only. |
| **Healing Word (L1 slot)** | 1d4 + spellcasting mod. **Bonus action**. Range 60 ft. |
| **Goodberry (L1 slot)** | 10 berries, 1 HP each, last 24 hr. Massive value when long-resting is blocked. |
| **Short rest (1 hr)** | Spend Hit Dice (1 die per level). Roll + CON mod = HP regained per die. |
| **Long rest (8 hr)** | Full HP. Half Hit Dice back. All spell slots restored. *Currently BLOCKED in Death House.* |

---

## Conditions cheat sheet (the ones that hit our table)

| Condition | What it does |
|---|---|
| **Paralyzed** | Can't move/speak. Auto-fail STR/DEX saves. Attacks have advantage; melee hits = crit. |
| **Frightened** | Disadv on attacks/checks while source is in sight. Can't willingly move toward source. |
| **Poisoned** | Disadv on attack rolls and ability checks. |
| **Prone** | Melee attacks on you have advantage; ranged have disadv. Half movement to stand up. |
| **Grappled** | Speed = 0. Ends if grappler is incapacitated or you escape (contested STR or use Escape). |
| **Restrained** | Speed = 0. Disadv on attacks. Attacks against you have advantage. Disadv on DEX saves. |
| **Cursed (this campaign)** | Custom — Druid: disadv on WIS saves until lifted. Define new curses explicitly. |

---

## Initiative and combat order

1. Everyone rolls d20 + DEX mod when combat starts. Highest goes first.
2. **Surprise:** if a side ambushed the other, the surprised side can't move/act on round 1.
3. **Reaction in combat:** Opportunity attack triggers when an enemy moves out of your reach without disengaging.

---

## "What if a player asks…"

| They ask | Answer |
|---|---|
| *"Can I cast a cantrip and attack?"* | No — cantrips are an Action. One Action per turn. (Quickened spell via Sorcery Points is the only exception.) |
| *"I want to roll a Charisma check"* | Make them describe what they're trying to do. Then YOU pick the skill (Persuasion / Deception / Intimidation / Performance). |
| *"Can I take 10?"* | No, that's a 3.5e rule. Make them roll. Or say "you succeed automatically" if it's trivial. |
| *"I want to use Divine Smite"* | Paladin: on a melee weapon hit, declare smite, expend a spell slot, add 2d8 radiant damage (3d8 vs undead/fiends). At Level 2+. *Houserule at this table: Mike has 1 bonus-action smite per session — track it in `state.md`.* |
| *"Can I help my ally attack?"* | Yes — Help action. They get advantage on their next attack against an adjacent enemy (must be within 5 ft. of it). |

---

## What words mean

| Term | Meaning |
|---|---|
| **DC** | Difficulty Class — target number to meet or beat |
| **AC** | Armor Class — target number an attacker must meet or beat to hit you |
| **HP** | Hit Points — your damage buffer |
| **PP** | Passive Perception — 10 + Perception mod; what you notice without rolling |
| **Modifier** | The +X you add to a d20 roll. Comes from your ability score (10–11 = +0, 12–13 = +1, 14–15 = +2, 16–17 = +3, 18–19 = +4, 20 = +5). Negative for low scores. |
| **Proficiency bonus** | +2 at L1–4, +3 at L5–8, +4 at L9–12. Add when proficient with a skill, weapon, save, or tool. |
| **Advantage** | Roll 2d20, take the higher. |
| **Disadvantage** | Roll 2d20, take the lower. |
| **Cantrip** | A spell castable at-will without using a slot. |
| **Spell slot** | A consumable resource for casting leveled spells. Restored on long rest. |
| **Critical hit** | Natural 20 on attack roll. Roll damage dice twice (not the modifier). |
| **Critical fail** | Natural 1 on attack roll = automatic miss. (5e RAW: no auto-fails on skill checks or saves — that's a popular houserule.) |

---

## When to **not** ask for a roll

- The action is trivial → just narrate the success.
- The action is impossible → just narrate the failure.
- The information is already known → just give it.
- You haven't decided what failure looks like → don't ask for the roll yet. Decide first.

> *Rule of thumb:* don't roll unless **failure is interesting**. Otherwise the dice are noise.
