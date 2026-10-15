---
tags:
  - dm-screen
  - foraging
  - crafting
  - city-and-wild
source: "City and Wild v4.1, pp. 70–71 and 130–131"
rules: "House rule — Fast Foraging"
---
# Quick Foraging — City and Wild

> [!info] At-the-table reference
> **Notos asks to forage → Nature check → d100 → ingredient + quantity → move on.**
> This page adapts the **published plant discovery tables** in *City and Wild v4.1*, Appendix C, pp. 130–131. The **streamlined check and quantities below are campaign house rules**, not the supplement's full harvesting procedure. The original supplement remains the authority for ingredient descriptions and alchemical properties.

> [!info] More gathering tools
> **Creature harvesting, exotic ores, crystals, and wood:** [[Gathering and Harvesting - City and Wild|🎲 Gathering & Harvesting Roller]] (Chapter 7).

## Click-to-Roll Foraging (Obsidian)

> [!tip] One-click rolling
> Choose the terrain and click **Roll Foraging**. The result automatically rolls **d100** against the terrain's table and **1d4** for quantity. Roll Notos's Nature check normally first, or use the optional check controls below. **Requires the installed Dataview plugin with JavaScript queries enabled** (Settings → Dataview → Enable JavaScript Queries). This block reads the tables farther down this same note; no duplicate ingredient list is required.

```dataviewjs
// Quick Foraging — City and Wild | Reads the Markdown tables in this note.
const source = await dv.io.load(dv.current().file.path);
if (!source) {
  dv.paragraph("Cannot load this note's foraging tables.");
} else {
  const terrains = ["Aquatic", "Arctic & Cold", "Caves", "Desert & Arid",
    "Forests & Woodlands", "Mountains", "Plains", "Swamps"];
  const tableData = {};
  for (let i = 0; i < terrains.length; i++) {
    const heading = "## " + terrains[i];
    const begin = source.indexOf(heading);
    if (begin === -1) continue;
    const next = source.indexOf("\n## ", begin + heading.length);
    const section = source.slice(begin + heading.length, next < 0 ? undefined : next);
    const rows = [];
    for (const line of section.split("\n")) {
      const m = line.match(/^\|\s*(\d+)(?:\s*-\s*(\d+))?\s*\|\s*([^|]+?)\s*\|\s*(Common|Uncommon|Rare)\s*\|\s*$/);
      if (m) rows.push({min: Number(m[1]), max: Number(m[2] || m[1]),
        ingredient: m[3].trim(), rarity: m[4]});
    }
    tableData[terrains[i]] = rows;
  }

  const root = dv.container.createDiv({cls: "quick-foraging-roller"});
  root.style.cssText = "border:1px solid var(--background-modifier-border);border-radius:12px;padding:16px;margin:8px 0;";
  const controlRow = root.createDiv();
  controlRow.style.cssText = "display:flex;gap:10px;flex-wrap:wrap;align-items:center;margin-bottom:12px;";
  const label = controlRow.createEl("label", {text:"Terrain: "});
  const terrainSelect = label.createEl("select");
  terrainSelect.style.cssText = "padding:6px;border-radius:6px;";
  terrains.forEach(t => terrainSelect.createEl("option", {text:t, value:t}));

  const checkLabel = controlRow.createEl("label", {text:"Nature modifier: "});
  const mod = checkLabel.createEl("input", {type:"number", value:"0"});
  mod.style.cssText = "width:65px;padding:5px;border-radius:6px;";
  const dcLabel = controlRow.createEl("label", {text:"DC: "});
  const dc = dcLabel.createEl("select");
  [10,15,20].forEach((n,i) => dc.createEl("option", {text:n+" ("+["abundant","limited","scarce"][i]+")",value:String(n)}));
  dc.value = "15";
  const adjustmentLabel = controlRow.createEl("label", {text:"DC modifier (+/-): "});
  const dcAdjust = adjustmentLabel.createEl("input", {type:"number", value:"0"});
  dcAdjust.style.cssText = "width:65px;padding:5px;border-radius:6px;";
  const rollButton = controlRow.createEl("button", {text:"🎲 Roll Foraging"});
  rollButton.addClass("mod-cta");
  const rawButton = controlRow.createEl("button", {text:"🎲 Roll ingredient only"});

  const result = root.createDiv();
  result.style.cssText = "padding:12px;border-radius:8px;background:var(--background-secondary);min-height:64px;";
  result.setText("Choose terrain. Roll Foraging makes the Nature check and discovery together; or roll ingredient only after a successful check at the table.");

  const d = sides => Math.floor(Math.random() * sides) + 1;
  function display(rollCheck) {
    const terrain = terrainSelect.value;
    const entries = tableData[terrain] || [];
    if (!entries.length) {
      result.setText("No table found for " + terrain + ". Check that its Markdown table is present.");
      return;
    }
    result.empty();
    if (rollCheck) {
      const natural = d(20);
      const bonus = Number(mod.value) || 0;
      const total = natural + bonus;
      const effectiveDC = Number(dc.value) + (Number(dcAdjust.value) || 0);
      const passed = total >= effectiveDC;
      result.createEl("div", {text:"Nature: " + natural + " + (" + bonus + ") = " + total +
        " vs DC " + dc.value + " + (" + (Number(dcAdjust.value) || 0) + ") = " + effectiveDC + " — " + (passed ? "SUCCESS" : "NO FIND")});
      if (!passed) {
        result.createEl("div", {text:"No useful ingredient found in this search."});
        return;
      }
    }
    const d100 = d(100), units = d(4);
    const entry = entries.find(e => d100 >= e.min && d100 <= e.max);
    if (!entry) { result.setText("No entry matches d100 = " + d100); return; }
    result.createEl("div", {text:"d100: " + d100 + " · " + terrain});
    const found = result.createEl("strong", {text:entry.ingredient});
    found.style.cssText = "display:block;font-size:1.15em;margin:4px 0;";
    result.createEl("div", {text:entry.rarity + " · 1d4 = " + units + " unit" + (units===1?"":"s")});
    const record = result.createEl("code", {text:entry.ingredient + " — " + entry.rarity + " — " + units + " unit" + (units===1?"":"s")});
    record.style.cssText = "display:block;margin-top:8px;white-space:normal;";
    const copy = result.createEl("button", {text:"Copy result"});
    copy.style.marginTop = "8px";
    copy.onclick = () => navigator.clipboard.writeText(record.textContent || "");
  }
  rollButton.onclick = () => display(true);
  rawButton.onclick = () => display(false);
}
```

---

## Fast Foraging: 30-Second Procedure

1. **Choose terrain** based on the party's current surroundings: Aquatic, Arctic & Cold, Caves, Desert & Arid, Forests & Woodlands, Mountains, Plains, or Swamps.
2. **One check per meaningful travel/exploration segment** (or when the party deliberately spends time foraging). Roll **Intelligence (Nature)**. The character can choose to spend **30 minutes** actively searching, matching the book's baseline search time. Passive foraging while walking is an optional DM allowance.
3. **Set the DC** by how much plant life is realistically accessible: **10 abundant / 15 limited / 20 very scarce**. *City and Wild* additionally suggests **+2 rare, +5 very rare, +10 legendary** when deliberately searching for a material of that rarity. For a **random** find using the d100 tables, don't add rarity modifiers after the roll: the table already weights rarities.
4. **DC adjustment:** Enter an optional positive or negative **DC modifier** for scarcity or depletion (e.g. abundant DC 10 + 2 = 12). The adjusted DC applies to the Nature check; the terrain discovery table is unchanged.
5. **On success:** roll **1d100** on the selected table. Award **1d4 units** of the named material (campaign shortcut; adjust to 1 unit for scarce regions if desired). **On failure:** no useful material found.
6. **Log only:** `Ingredient — rarity — units` in Notos's inventory. Save recipe questions, pricing, and crafting for downtime.

> [!tip] Fastest possible live call
> "Cesar, Nature DC 15. Success? Roll d100. You found **[table result]**, **1d4 units**. Note it down. Back to the scene."

### Limits to prevent repeating rolls

- Default **one search attempt per distinct travel segment or scene**, not unlimited repeats in the same patch of terrain.
- If Notos wants to spend additional hours deliberately collecting, use the **full source rules** rather than chaining rapid random rolls.
- Never call for a roll when the environment offers no harvestable growth (e.g., barren worked stone, open deck without plants). Let good scouting or a clever harvesting approach matter.
- **No automatic recipe unlock.** Discovery creates an ingredient; teaching the Philosopher's Jar still uses its established learning cost and Alchemical Mastery check.

## Source Rules vs. House Rules

| Topic | City and Wild v4.1 | Fast table variant |
|---|---|---|
| Searching | Intelligence (Nature), 30 minutes; DC 10 / 15 / 20 by abundance | Same DCs; allow passive discovery during an exploration segment at DM discretion |
| What is found | Choose or roll a plant from Appendix C for that terrain | Always d100 after success |
| Harvesting / extracting | Additional procedures and varying quantities for different material sources | One **1d4-unit award**; no separate harvesting roll |
| Targeting rare finds | Rarity DC modifiers apply when seeking known rare materials | Let rarity come from weighted d100 results; modifiers apply only when **targeting** a specific scarce material |
| Crafting | Separate alchemy and crafting rules | Not resolved during travel |

**Full rules:** *City and Wild* v4.1, Ch. 7 "Collecting Materials" (pp. 70–71), Appendix C "Plants by Areas" (pp. 130–131), and Ch. 8 "Alchemy" (pp. 88 onward).

---

# Terrain Discovery Tables

These are the **d100 tables from Appendix C**, with original range weighting and rarity, transcribed as a lookup aid. Ingredient effects, prices, and preparation rules remain in the PDF.

## Aquatic

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-6 | Banshee’s lament | Common |
| 7-12 | Blackleaf rose | Common |
| 13-18 | Chromatic mud | Common |
| 19-24 | Drojos ivy | Common |
| 25-30 | Frenn moss | Common |
| 31-36 | Goblin mud | Common |
| 37-42 | Golden coneflower | Common |
| 43-48 | Kreet paste | Common |
| 49-54 | Mermaid braid | Common |
| 55-60 | Sugar hibiscus berries | Common |
| 61-66 | Tempest flower | Common |
| 67-72 | Twilight wormwood | Common |
| 73-78 | White poppy | Common |
| 79-84 | Winter turtlehead | Common |
| 85-87 | Blue seaweed | Uncommon |
| 88-90 | Ecire laurel | Uncommon |
| 91-93 | Healer’s boon | Uncommon |
| 94-96 | Quicksilver fern | Uncommon |
| 97-100 | Slime thimbleberry | Rare |

## Arctic & Cold

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-6 | Angel flower | Common |
| 7-12 | Aniseed sap | Common |
| 13-18 | Chromatic mud | Common |
| 19-24 | Dusk itchweed | Common |
| 25-30 | Ellond shrub | Common |
| 31-36 | Ghostly snowdrop | Common |
| 37-42 | Kreet paste | Common |
| 43-48 | Mandrake root | Common |
| 49-54 | Mermaid braid | Common |
| 55-60 | Storm daisy | Common |
| 61-66 | Thunderleaf | Common |
| 67-72 | White poppy | Common |
| 73-78 | Winter turtlehead | Common |
| 79-84 | Wolfhair moss | Common |
| 85-87 | Celestial bloom | Uncommon |
| 88-90 | Frostbloom lily | Uncommon |
| 91-93 | Glowing duscle | Uncommon |
| 94-96 | Quicksilver fern | Uncommon |
| 97-99 | Yeti’s parsley | Uncommon |
| 100 | Spineflower berries | Rare |

## Caves

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-6 | Abyss flower | Common |
| 7-12 | Angel flower | Common |
| 13-18 | Banshee’s lament | Common |
| 19-24 | Crimson brittlebush | Common |
| 25-30 | Dragontongue petals | Common |
| 31-36 | Dried ephedra | Common |
| 37-42 | Ebrium fungus | Common |
| 43-48 | Golden hibiscus | Common |
| 49-54 | Mandrake root | Common |
| 55-60 | Nightshade | Common |
| 61-66 | Twilight wormwood | Common |
| 67-72 | Viper thistle | Common |
| 73-78 | White poppy | Common |
| 79-84 | Wizard’s clover | Common |
| 85-87 | Blue cress | Uncommon |
| 88-90 | Glowing duscle | Uncommon |
| 91-93 | Lunar nectar | Uncommon |
| 94-96 | Raiflower | Uncommon |
| 97-99 | Somnivine | Uncommon |
| 100 | Umbra orchid | Rare |

## Desert & Arid

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-5 | Blackleaf rose | Common |
| 6-10 | Crimson brittlebush | Common |
| 11-15 | Dragontongue petals | Common |
| 16-20 | Dried ephedra | Common |
| 21-25 | Ebrium fungus | Common |
| 26-30 | Ellond shrub | Common |
| 31-35 | Golden hibiscus | Common |
| 36-40 | Gray gilliflower | Common |
| 41-45 | Iron thistle | Common |
| 46-50 | Raven silkweed | Common |
| 51-55 | Tempest flower | Common |
| 56-60 | Twilight wormwood | Common |
| 61-65 | Viper thistle | Common |
| 66-70 | Wizard’s clover | Common |
| 71-75 | Ash chives | Uncommon |
| 76-80 | Bone garlic | Uncommon |
| 81-85 | Carmine starthistle | Uncommon |
| 86-90 | Emberroot | Uncommon |
| 91-95 | Kasuni juice | Uncommon |
| 96-100 | Ucre bramble | Uncommon |

## Forests & Woodlands

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-6 | Aniseed sap | Common |
| 7-12 | Blood herb | Common |
| 13-18 | Drojos ivy | Common |
| 19-24 | Dusk itchweed | Common |
| 25-30 | Frenn moss | Common |
| 31-36 | Golden coneflower | Common |
| 37-42 | Iron thistle | Common |
| 43-48 | Olina petals | Common |
| 49-54 | Raven silkweed | Common |
| 55-60 | Thunderleaf | Common |
| 61-66 | Viper thistle | Common |
| 67-72 | Winter turtlehead | Common |
| 73-78 | Wisp stems | Common |
| 79-82 | Ash chives | Uncommon |
| 83-86 | Astralshade moss | Uncommon |
| 87-90 | Blue cress | Uncommon |
| 91-94 | Kasuni juice | Uncommon |
| 95-98 | Yeti’s parsley | Uncommon |
| 99-100 | Phoenix featherfern | Rare |

## Mountains

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-5 | Abyss flower | Common |
| 6-10 | Angel flower | Common |
| 11-15 | Crimson brittlebush | Common |
| 16-20 | Dried ephedra | Common |
| 21-25 | Ebrium fungus | Common |
| 26-30 | Ellond shrub | Common |
| 31-35 | Golden hibiscus | Common |
| 36-40 | Gray gilliflower | Common |
| 41-45 | Iron thistle | Common |
| 46-50 | Nightshade | Common |
| 51-55 | Storm daisy | Common |
| 56-60 | Sugar hibiscus berries | Common |
| 61-65 | Tempest flower | Common |
| 66-70 | Wizard’s clover | Common |
| 71-75 | Wolfhair moss | Common |
| 76-80 | Celestial bloom | Uncommon |
| 81-85 | Emberroot | Uncommon |
| 86-90 | Lunar nectar | Uncommon |
| 91-95 | Raiflower | Uncommon |
| 96-100 | Serpentleaf herb | Uncommon |

## Plains

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-5 | Aniseed sap | Common |
| 6-10 | Banshee’s lament | Common |
| 11-15 | Blood herb | Common |
| 16-20 | Dragontongue petals | Common |
| 21-25 | Dusk itchweed | Common |
| 26-30 | Ghostly snowdrop | Common |
| 31-35 | Goblin mud | Common |
| 36-40 | Golden coneflower | Common |
| 41-45 | Gray gilliflower | Common |
| 46-50 | Mandrake root | Common |
| 51-55 | Olina petals | Common |
| 56-60 | Raven silkweed | Common |
| 61-65 | Storm daisy | Common |
| 66-70 | Sugar hibiscus berries | Common |
| 71-75 | Thunderleaf | Common |
| 76-80 | Wisp stems | Common |
| 81-85 | Carmine starthistle | Uncommon |
| 86-90 | Frostbloom lily | Uncommon |
| 91-95 | Healer’s boon | Uncommon |
| 96-100 | Ucre bramble | Uncommon |

## Swamps

| d100 | Ingredient | Rarity |
|---|---|---|
| 1-5 | Abyss flower | Common |
| 6-10 | Blackleaf rose | Common |
| 11-15 | Blood herb | Common |
| 16-20 | Chromatic mud | Common |
| 21-25 | Drojos ivy | Common |
| 26-30 | Frenn moss | Common |
| 31-35 | Ghostly snowdrop | Common |
| 36-40 | Goblin mud | Common |
| 41-45 | Kreet paste | Common |
| 46-50 | Mermaid braid | Common |
| 51-55 | Nightshade | Common |
| 56-60 | Olina petals | Common |
| 61-65 | Wisp stems | Common |
| 66-70 | Wolfhair moss | Common |
| 71-75 | Ecire laurel | Uncommon |
| 76-80 | Astralshade moss | Uncommon |
| 81-85 | Blue seaweed | Uncommon |
| 86-90 | Bone garlic | Uncommon |
| 91-95 | Serpentleaf herb | Uncommon |
| 96-100 | Somnivine | Uncommon |

---

## Notos — Quick Inventory Log

| Session / Location | Material | Rarity | Units | Used / Notes |
|---|---|---|---:|---|
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

> [!warning] Rulings
> This document addresses **plant and herb discovery**. Mining, salvaging, and harvesting creature parts use different rules in *City and Wild* and are **not** interchangeable with these tables. The Philosopher's Jar's daily replication and recipe-learning features also remain separate.
