---
AssociatedGroup: The Myriad
Gender: Any
Race: Humanoid (any)
Age: Adult
Class: Mobile Pursuer
Alignment: Neutral Evil
Character-Role: Mobile Pursuer
Location: Stillben
NoteIcon: npc
tags:
  - monster
  - homebrew
  - myriad
  - session-15
---
# Myriad Interceptor

> [!infobox]
> # Myriad Interceptor
> ![[z_Assets/Misc/ImagePlaceholder.png|cover hsmall]]
> ###### Basic Information
> Type | Stat
> ---|---
> Group | The Myriad
> Role | Mobile Pursuer
> Location | Stillben
> ###### Rules Information
> Type | Stat
> ---|---
> Challenge | 3 (700 XP)
> Creature | Medium humanoid

## Profile

An agile Myriad operative used to follow suspects, retrieve evidence, and intercept people fleeing through Stillben's alleys. Interceptors prefer arrests, intimidation, and quick retreats to heroic last stands.

> [!info] Custom Statblock — 5e Statblocks
> This YAML uses the format tested successfully with [[Myriad Foot Soldier]]. The challenge rating is a **homebrew design target**, not a playtested guarantee.

```statblock
layout: Basic 5e Layout
name: Myriad Interceptor
size: Medium
type: humanoid (any)
alignment: neutral evil
ac: 15
hp: 60
hit_dice: 11d8 + 11
speed: 30 ft.
stats: [11, 16, 12, 12, 12, 11]
skillsaves:
  - deception: 3
  - perception: 4
  - stealth: 6
senses: passive Perception 14
languages: Common, one other language
cr: 3
traits:
  - name: Cunning Escape
    desc: "The interceptor can take the Dash or Disengage action as a bonus action."
  - name: Street Ambusher
    desc: "Once per turn, the interceptor deals an extra 7 (2d6) damage when it hits a target with a weapon attack and has advantage on the attack roll."
actions:
  - name: Multiattack
    desc: "The interceptor makes two shortsword or hand crossbow attacks."
  - name: Shortsword
    desc: "Melee Weapon Attack: +5 to hit, reach 5 ft., one target. Hit: 6 (1d6 + 3) piercing damage."
  - name: Hand Crossbow
    desc: "Ranged Weapon Attack: +5 to hit, range 30/120 ft., one target. Hit: 6 (1d6 + 3) piercing damage."
reactions:
  - name: Evasive Step
    desc: "When the interceptor is hit by an opportunity attack, it can use its reaction to halve that attack's damage (round down)."
```

## Tactics

- Exploits cover, crowds, and escape lanes.
- May focus on grabbing a document or delaying the party rather than inflicting maximum damage.
- Withdraws when the assignment becomes untenable.

## Encounter Guidance

**Party level:** 6. This is a supporting enemy or situational antagonist. Evaluate the **actual number of PCs**, encounter objectives, terrain, and additional combatants before deciding an encounter is balanced.

Open this note and use the **+** control on the rendered statblock to add the monster to Initiative Tracker.

## DM Notes

A low- or mid-ranking operative knows their orders, relevant contacts, and immediate assignment—not necessarily who masterminded Hurk and Heijla's disappearance. This enemy is optional; using the creature does not require the party to enter combat.

## Links

- [[Myriad Foot Soldier]]
- [[Act 2 - The Myriad's Warning]]
