---
AssociatedGroup: The Myriad
Gender: Any
Race: Humanoid (any)
Age: Adult
Class: Skirmisher
Alignment: Neutral Evil
Character-Role: Enforcer
Location: Stillben
NoteIcon: npc
tags:
  - monster
  - homebrew
  - myriad
  - session-15
---

# Myriad Foot Soldier

> [!infobox]
> # Myriad Foot Soldier
> ![[z_Assets/Misc/ImagePlaceholder.png|cover hsmall]]
> ###### Basic Information
> Type | Stat
> ---|---
> Home | Stillben
> Group | The Myriad
> Role | Street-level enforcer
> ###### Rules Info
> Type | Stat
> ---|---
> Challenge | 1 (200 XP)
> Creature | Medium humanoid
> Alignment | Neutral evil (typical)

## Profile

A Myriad foot soldier is a paid enforcer, lookout, or courier assigned to intimidate witnesses, guard safehouses, and support more influential operatives. Their loyalty is often to the pay, not the cause. Their equipment is practical and unremarkable, allowing them to pass as an ordinary traveler or dockworker when not wearing gang colors.

**Use in Session 15:** These are possible guards or escorts if the party investigates the disappearance of Hurk and Heijla or confronts Myriad operatives in Stillben. Their presence is **not** a mandatory combat encounter.

> [!info] Custom Statblock — Obsidian 5e Statblocks
> The YAML code block below is intended for the installed 5e Statblocks plugin. It uses explicit attributes instead of pulling a stock monster by name.

```statblock
layout: Basic 5e Layout
name: Myriad Foot Soldier
size: Medium
type: humanoid (any)
alignment: neutral evil
ac: 14
hp: 27
hit_dice: 5d8 + 5
speed: 30 ft.
stats: [12, 14, 12, 10, 11, 10]
skillsaves:
  - deception: 2
  - perception: 2
  - stealth: 4
senses: passive Perception 12
languages: Common, one other language
cr: 1
traits:
  - name: Cunning Escape
    desc: "The foot soldier can take the Disengage action as a bonus action."
  - name: Pack Tactics
    desc: "The foot soldier has advantage on an attack roll against a creature if at least one of the foot soldier's allies is within 5 feet of the creature and the ally isn't incapacitated."
actions:
  - name: Shortsword
    desc: "Melee Weapon Attack: +4 to hit, reach 5 ft., one target. Hit: 5 (1d6 + 2) piercing damage."
  - name: Light Crossbow
    desc: "Ranged Weapon Attack: +4 to hit, range 80/320 ft., one target. Hit: 6 (1d8 + 2) piercing damage."
reactions:
  - name: Dirty Defense (Recharge 5–6)
    desc: "When a creature the foot soldier can see hits it with a melee attack, the foot soldier adds 2 to its AC against that attack, potentially causing it to miss. The foot soldier must be wielding a melee weapon."
```

## Encounter Test

> [!warning] Plugin integration test
> The embedded `statblock` defines the creature for **5e Statblocks**. The separate `encounter-table` plugin may require the custom monster to be registered in its own bestiary/source data before it resolves the name. Test rendering independently; if the encounter entry is unresolved, it does not mean the statblock failed.

```encounter-table
name: Myriad Foot Soldier — Test
creatures:
 - 1: Myriad Foot Soldier
```

### Suggested Difficulty for Level 6 Characters

A single CR 1 foot soldier is a **low-threat test creature**, not a balanced stand-alone encounter against a level 6 party. Use one initially to test Obsidian rendering and custom encounter lookup. Multiple soldiers, a commanding operative, terrain, objectives, and the party's actual size can be considered later when building a real encounter.

### Tactics

- Works with allies to take advantage of **Pack Tactics**.
- Uses **Cunning Escape** to reposition instead of fighting to the death.
- Prefers intimidation, stalling, and withdrawing to protect the Myriad's identities.
- May surrender, bargain, or flee if isolated or badly wounded.

### DM Notes

- **Not every Myriad foot soldier knows the truth about Hurk and Heijla.** A guard knows only what their assignment would reasonably reveal.
- A captured foot soldier might identify a meeting place, courier route, or superior, but should not automatically reveal the whole operation.
- For this test, the creature has **CR 1 (200 XP)** and is intended as one supporting enemy among level 6 adventurers.
- The `Dirty Defense` recharge on a reaction is a homebrew mechanic; if its tracking proves inconvenient, remove the recharge and limit the reaction to one use per round.

## Links

- [[Shadows Over Stillben]]
