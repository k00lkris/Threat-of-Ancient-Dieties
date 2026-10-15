---
tags: [dm-screen, harvesting, crafting, city-and-wild]
source: "City and Wild v4.1, Chapter 7 pp. 70–86; Appendix B pp. 121–129"
---
# Gathering & Harvesting — City and Wild

> [!tip] DM shortcuts
> **Herbs:** [[Quick Foraging - City and Wild|🎲 Open the foraging roller]].
> **Slain creature:** Choose its type, CR and size below; the calculator rolls harvesting checks, while you select the part from Appendix B.
> **Ore, crystal, wood or other exotic material:** Use the second roller below.
>
> **These are separate workflows in the book.** Do not treat Appendix B as a random drop list: it specifies *possible parts and estimated totals* for each creature, not guaranteed loot.

## Appendix B creature parts

> [!important] Creature-specific loot list
> Open [[Appendix B - Parts by Creature]] to search the creature name and see **each harvestable part, estimated maximum units, and source page**. The Appendix B lookup is supplied as a separate Obsidian Markdown file for import into this DM Screen folder.

## Slain Creature — Interactive Harvesting

```dataviewjs
const root=dv.container.createDiv();
root.style.cssText="border:1px solid var(--background-modifier-border);border-radius:12px;padding:14px;";
const control=root.createDiv();
control.style.cssText="display:flex;gap:9px;flex-wrap:wrap;align-items:end;";
function select(label,choices) {
 const wrap=control.createDiv();
 wrap.createEl("div",{text:label});
 const e=wrap.createEl("select");
 choices.forEach(([v,t])=>e.createEl("option",{value:v,text:t}));
 return e;
}
function numeric(label,value,step="1") {
 const wrap=control.createDiv();wrap.createEl("div",{text:label});
 const e=wrap.createEl("input",{type:"number",value:String(value)});
 e.step=step;e.style.width="78px";return e;
}
const creature=select("Creature type",[
 ["arcana","Aberration"],["arcana","Construct"],["arcana","Dragon"],["arcana","Elemental"],["arcana","Fey"],["arcana","Ooze"],
 ["nature","Beast"],["nature","Giant"],["nature","Humanoid"],["nature","Monstrosity"],["nature","Plant"],
 ["religion","Celestial"],["religion","Fiend"],["religion","Undead"]]);
const skillNames=["Arcana","Arcana","Arcana","Arcana","Arcana","Arcana","Nature","Nature","Nature","Nature","Nature","Religion","Religion","Religion"];
const cr=numeric("Creature CR",3,"0.125");
const size=select("Creature size",[["Tiny","Tiny"],["Small","Small"],["Medium","Medium"],["Large","Large"],["Huge","Huge"],["Gargantuan","Gargantuan"]]);size.value="Medium";
const bonus=numeric("Harvester's skill bonus",4);
const attempts=numeric("Checks this corpse",1);
const specs={Tiny:[1,0.25],Small:[2,0.5],Medium:[2,1],Large:[3,2],Huge:[4,3],Gargantuan:[5,4]};
const info=root.createDiv();info.style.margin="10px 0";
const result=root.createDiv();result.style.cssText="padding:12px;background:var(--background-secondary);border-radius:8px;margin-top:8px;";
const roll=root.createEl("button",{text:"🎲 Roll harvesting"});
roll.addClass("mod-cta");
function update(){
 const [maximum,per]=specs[size.value];
 const dc=12+Math.max(0,Number(cr.value)<2?0:Number(cr.value)/2);
 info.setText("Use "+skillNames[creature.selectedIndex]+" · DC "+dc+" (12 + ½ CR; CR below 2 contributes 0) · "+maximum+" suggested maximum checks · up to "+per+" unit(s) per successful check · 10 minutes/check.");
 return {maximum,per,dc};
}
for(const e of [creature,cr,size])e.onchange=update;
update();
result.setText("Choose a creature. Use Appendix B to determine which parts exist; one part or organ may have a smaller harvest limit than the size-based maximum.");
roll.onclick=()=>{
 const {maximum,per,dc}=update();
 const n=Math.min(maximum,Math.max(1,Math.floor(Number(attempts.value)||1)));
 const modifier=Number(bonus.value)||0;
 result.empty();
 let wins=0;
 for(let i=0;i<n;i++){
  const d20=Math.floor(Math.random()*20)+1;
  const total=d20+modifier;
  if(total>=dc)wins++;
  result.createEl("div",{text:"Check "+(i+1)+": "+d20+" + ("+modifier+") = "+total+" vs DC "+dc+" — "+(total>=dc?"SUCCESS":"FAILURE — attempted part destroyed")});
 }
 result.createEl("strong",{text:"Successful checks: "+wins+" / "+n+" · maximum potential yield: "+(wins*per)+" unit(s), subject to specific part limits."});
 result.createEl("p",{text:"DM: Name the selected part using Appendix B; for unique organs, apply its own limit (often 1). Parts may require chilling to avoid decomposition."});
};
```

### Creature harvesting reference (source rules, pp. 70–72)

| Creature type | Skill |
|---|---|
| Aberration, Construct, Dragon, Elemental, Fey, Ooze | Intelligence (Arcana) |
| Beast, Giant, Humanoid, Monstrosity, Plant | Intelligence (Nature) |
| Celestial, Fiend, Undead | Intelligence (Religion) |

**DC:** 12 + ½ CR. Creatures below CR 2 add nothing. The source does not specify rounding for half-CR; calculator retains the fraction. **10 minutes per check.** Failed checks destroy the part attempted.

| Size | Suggested maximum checks | Maximum units per successful check |
|---|---:|---:|
| Tiny | 1 | ¼ |
| Small | 2 | ½ |
| Medium | 2 | 1 |
| Large | 3 | 2 |
| Huge | 4 | 3 |
| Gargantuan | 5 | 4 |

These are **suggested ceilings**, not a guarantee that each named part can be harvested that often. A dragon's heart, for example, could permit only one check. **Appendix B (pp. 121–129)** supplies named creature parts and estimated quantities. It excludes ordinary meat, bones, blood and organs. The supplement says a creature has **one unit of type essence**, extractable with the *Essence Extraction Device* (pp. 11 and 72); that is a **separate magic-item process**, not an automatic bonus on a successful harvesting roll.

## Exotic Materials — Interactive Gathering

Use this for material deposits or identifiable herbs **after** locating them, rather than the foraging discovery shortcut. Source: Chapter 7 pp. 70–71.

```dataviewjs
const root=dv.container.createDiv();
root.style.cssText="border:1px solid var(--background-modifier-border);border-radius:12px;padding:14px;";
const row=root.createDiv();row.style.cssText="display:flex;gap:9px;flex-wrap:wrap;align-items:end;";
function choice(label,opts){
 const w=row.createDiv();w.createEl("div",{text:label});const e=w.createEl("select");
 opts.forEach(([v,t])=>e.createEl("option",{value:String(v),text:t}));return e;
}
function number(label,value){
 const w=row.createDiv();w.createEl("div",{text:label});const e=w.createEl("input",{type:"number",value:String(value)});e.style.width="75px";return e;
}
const group=choice("Material",[["Ores","Ores (Strength)"],["Crystals and stones","Crystals & stones (Str/Dex)"],["Wood","Wood (Str/Dex)"],["Plants and herbs","Plants & herbs (Dex/Int)"],["Other materials","Other (DM choice)"]]);
const dc=choice("Abundance / DC",[[10,"Abundant — 10"],[15,"Limited — 15"],[20,"Scarce — 20"]]);
const search=choice("Find a deposit?",[["no","Already found"],["yes","Roll Nature search"]]);
const nature=number("Nature search bonus",4);
const bonus=number("Gathering check bonus",4);
const ability=number("Relevant ability modifier",2);
const output=root.createDiv();output.style.cssText="padding:12px;background:var(--background-secondary);border-radius:8px;margin-top:12px;";
output.setText("Search (optional), then gather. Each gathering check takes 1 hour and yield depends on how far you beat the DC.");
const button=root.createEl("button",{text:"🎲 Roll gathering"});button.addClass("mod-cta");button.style.marginTop="10px";
const d=s=>Math.floor(Math.random()*s)+1;
button.onclick=()=>{
 output.empty();const target=Number(dc.value);let passed=true;
 if(search.value==="yes"){
 const die=d(20),total=die+(Number(nature.value)||0);
 passed=total>=target;
 output.createEl("div",{text:"Find material: "+die+" + "+(Number(nature.value)||0)+" = "+total+" vs DC "+target+" — "+(passed?"FOUND":"NOT FOUND")});
 }
 if(!passed)return;
 const die=d(20),total=die+(Number(bonus.value)||0),margin=total-target;
 output.createEl("div",{text:group.value+" gathering: "+die+" + "+(Number(bonus.value)||0)+" = "+total+" vs DC "+target});
 if(margin<0){output.createEl("strong",{text:"Failed to gather units."});return;}
 const sides=margin<=4?4:margin<=9?6:8;
 const raw=d(sides)+(Number(ability.value)||0);
 const units=Math.max(0,raw);
 output.createEl("strong",{text:"Success by "+margin+" · 1d"+sides+" + ability modifier = "+raw+" unit(s)"+(units!==raw?" (minimum 0 used)":"")});
 output.createEl("div",{text:"1 hour spent. DM may increase DC by 2 for later extractions of the same material in the same area."});
};
```

### Exotic collection reference

| Material group | Suggested tool / spell | Suggested ability |
|---|---|---|
| Ores | *Mold earth* | Strength |
| Crystals and stones | Mason's tools | Strength or Dexterity |
| Wood | Carpenter's tools | Strength or Dexterity |
| Plants and herbs | Herbalism kit | Dexterity or Intelligence |
| Other materials | Varies | Varies |

**Search:** 30 minutes and Intelligence (Nature) DC 10 (abundant), 15 (limited), or 20 (very scarce). Increase DC by 2/5/10 when specifically locating a **rare / very rare / legendary** material. Once identified, gathering uses Strength, Dexterity or Intelligence as relevant, with applicable proficiency. **Each gathering check: 1 hour.** Maximum attempts equal the higher of Intelligence or Constitution modifier (minimum one). On success by 0–4: **1d4 + ability modifier** units; success by 5–9: **1d6 + ability modifier**; success by 10+: **1d8 + ability modifier**. DM may increase subsequent DC by 2 as the deposit is depleted.

> [!note] Reference index — Chapter 7
> - **p. 70:** Material sources, material search, creature checks and skills.
> - **p. 71:** Size/yield guidelines, preservation, exotic extraction.
> - **p. 72:** Creature essence, part tags, and creature-part applications.
> - **p. 73:** Material costs, unit weights, and rarities, including ore/crystal/wood/other categories.
> - **pp. 74–86:** Properties and uses for the book's exotic materials and plants.
> - **Appendix B, pp. 121–129:** Creature-specific parts and quantities.
> - **Appendix C, pp. 130–131:** Terrain-based plant discoveries (in the linked foraging roller).
>
> Not every creature in your campaign is in Appendix B. For homebrewed monsters, the DM should specify available parts and limits; don't generate impossible organs solely from creature type.

## Suggested harvest log

| Creature / deposit | Part or material | Units | Skill roll | Notes |
|---|---|---:|---|---|
| | | | | |
