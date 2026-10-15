---
AssociatedGroup: The Myriad
Gender: Any
Race: Humanoid (any)
Age: Adult
Class: Field Commander
Alignment: Neutral Evil
Character-Role: Field Commander
Location: Stillben
NoteIcon: npc
tags:
  - monster
  - homebrew
  - myriad
  - session-15
---
# Myriad Lieutenant

> [!infobox]
> # Myriad Lieutenant
> ![[z_Assets/Misc/ImagePlaceholder.png|cover hsmall]]
> ###### Basic Information
> Type | Stat
> ---|---
> Group | The Myriad
> Role | Field Commander
> Location | Stillben
> ###### Rules Information
> Type | Stat
> ---|---
> Challenge | 4 (1,100 XP)
> Creature | Medium humanoid

## Profile

A hardened field officer directing local Myriad guards, collecting payments, and overseeing discreet intimidation. A lieutenant is a serious threat but does not have to be a cruel fanatic; leverage or capture may change their behavior.

> [!info] Custom Statblock — 5e Statblocks
> This YAML uses the format tested successfully with [[Myriad Foot Soldier]]. The challenge rating is a **homebrew design target**, not a playtested guarantee.

```statblock
layout: Basic 5e Layout
name: Myriad Lieutenant
size: Medium
type: humanoid (any)
alignment: neutral evil
ac: 16
hp: 76
hit_dice: 9d8 + 36
speed: 30 ft.
stats: [16, 14, 18, 12, 12, 14]
skillsaves:
  - deception: 5
  - perception: 4
  - stealth: 4
senses: passive Perception 14
languages: Common, one other language
cr: 4
traits:
  - name: Hold the Line
    desc: "Allied Myriad creatures within 10 feet of the lieutenant have advantage on saving throws against being frightened while they can see or hear the lieutenant."
actions:
  - name: Multiattack
    desc: "The lieutenant makes two longsword attacks."
  - name: Longsword
    desc: "Melee Weapon Attack: +5 to hit, reach 5 ft., one target. Hit: 7 (1d8 + 3) slashing damage."
  - name: Heavy Crossbow
    desc: "Ranged Weapon Attack: +4 to hit, range 100/400 ft., one target. Hit: 7 (1d10 + 2) piercing damage."
  - name: Command (Recharge 5–6)
    desc: "One allied creature within 30 feet that can hear the lieutenant may immediately use its reaction to move up to half its speed without provoking opportunity attacks."
reactions:
  - name: Parry
    desc: "The lieutenant adds 2 to its AC against one melee attack that would hit it. It must see the attacker and be wielding a melee weapon."
```

## Tactics

- Directs foot soldiers toward choke points instead of charging blindly.
- Uses Command to help an ally escape with sensitive evidence.
- Offers a deal when the situation turns against the Myriad; knows only the local chain of command.

## Encounter Guidance

**Party level:** 6. This is a supporting enemy or situational antagonist. Evaluate the **actual number of PCs**, encounter objectives, terrain, and additional combatants before deciding an encounter is balanced.

Open this note and use the **+** control on the rendered statblock to add the monster to Initiative Tracker.

## DM Notes

A low- or mid-ranking operative knows their orders, relevant contacts, and immediate assignment—not necessarily who masterminded Hurk and Heijla's disappearance. This enemy is optional; using the creature does not require the party to enter combat.

## Links

- [[Myriad Foot Soldier]]
- [[Act 2 - The Myriad's Warning]]
