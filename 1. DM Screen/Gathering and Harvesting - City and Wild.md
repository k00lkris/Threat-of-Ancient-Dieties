---
tags: [dm-screen, harvesting, crafting, city-and-wild]
source: "City and Wild v4.1, Chapter 7 pp. 70–86; Appendix B pp. 121–129"
---
# Gathering & Harvesting — City and Wild

> [!tip] DM shortcuts
> **Herbs:** [[Quick Foraging - City and Wild|🎲 Open the foraging roller]].
> **Slain creature:** Search Appendix B by any part of a monster name (suggestions appear as you type), choose its part, then select type, CR and size for the harvesting roll.
> **Ore, crystal, wood or other exotic material:** Use the second roller below.
>
> **These are separate workflows in the book.** Do not treat Appendix B as a random drop list: it specifies *possible parts and estimated totals* for each creature, not guaranteed loot.

## Appendix B creature parts

> [!important] Creature-specific loot list
> The roller searches **[[Appendix B - Parts by Creature]]** directly. **First setup:** download that note and save it in the same `1. DM Screen` folder. The name search then suggests matching creatures as you type. **Creature type is still needed** for the correct harvesting skill (Arcana/Nature/Religion), since Appendix B lists parts but not complete stat blocks.

## Slain Creature — Interactive Harvesting

```dataviewjs
const root=dv.container.createDiv();
root.style.cssText="border:1px solid var(--background-modifier-border);border-radius:12px;padding:14px;";
const dataPath=dv.current().file.folder+"/Appendix B - Parts by Creature.md";
const dataText=await dv.io.load(dataPath);
const entries={};
if(dataText){
 const start=dataText.indexOf("<!-- APPENDIX_B_START -->");
 const end=dataText.indexOf("<!-- APPENDIX_B_END -->");
 if(start>=0&&end>start){
  for(const line of dataText.slice(start,end).split("\n")){
   const m=line.match(/^\| ([^|]+) \| ([^|]+) \| ([^|]+) \| (\d+) \|$/);
   if(!m)continue;
   (entries[m[1].trim()]??=[]).push({part:m[2].trim(),max:m[3].trim(),page:m[4]});
  }
 }
}
const names=Object.keys(entries).sort((a,b)=>a.localeCompare(b));
const searchRow=root.createDiv();
searchRow.style.cssText="display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-bottom:10px;";
searchRow.createEl("strong",{text:"Appendix B creature:"});
const search=searchRow.createEl("input",{attr:{type:"search",placeholder:"Search monster..." }});
search.style.cssText="min-width:150px;padding:6px;";
const hints=searchRow.createEl("datalist");
const hintId="harvest-creatures-"+Math.random().toString(36).slice(2);
hints.id=hintId;
search.setAttribute("list",hintId);
const monster=searchRow.createEl("select");
monster.style.maxWidth="330px";
monster.setAttribute("aria-label","Matching creatures");
const partList=root.createDiv();
const chosenLabel=root.createDiv();
chosenLabel.style.cssText="margin:10px 0;";
const chosenPart=chosenLabel.createEl("select");
const control=root.createDiv();
control.style.cssText="display:flex;gap:9px;flex-wrap:wrap;align-items:end;";
function select(label,choices){
 const wrap=control.createDiv();wrap.createEl("div",{text:label});
 const el=wrap.createEl("select");
 choices.forEach(([v,t])=>el.createEl("option",{value:v,text:t}));
 return el;
}
function numeric(label,value,step="1"){
 const wrap=control.createDiv();wrap.createEl("div",{text:label});
 const el=wrap.createEl("input",{type:"number",value:String(value)});
 el.step=step;el.style.width="78px";return el;
}
const creature=select("Creature type",[
 ["arcana","Aberration"],["arcana","Construct"],["arcana","Dragon"],["arcana","Elemental"],["arcana","Fey"],["arcana","Ooze"],
 ["nature","Beast"],["nature","Giant"],["nature","Humanoid"],["nature","Monstrosity"],["nature","Plant"],
 ["religion","Celestial"],["religion","Fiend"],["religion","Undead"]]);
const skillNames=["Arcana","Arcana","Arcana","Arcana","Arcana","Arcana","Nature","Nature","Nature","Nature","Nature","Religion","Religion","Religion"];
const cr=numeric("Creature CR",3,"0.125");
const size=select("Creature size",[["Tiny","Tiny"],["Small","Small"],["Medium","Medium"],["Large","Large"],["Huge","Huge"],["Gargantuan","Gargantuan"]]);size.value="Medium";
const bonus=numeric("Skill bonus",4);
const attempts=numeric("Checks",1);
const specs={Tiny:[1,0.25],Small:[2,0.5],Medium:[2,1],Large:[3,2],Huge:[4,3],Gargantuan:[5,4]};
const info=root.createDiv();info.style.margin="10px 0";
const roll=root.createEl("button",{text:"🎲 Roll selected part harvest"});roll.addClass("mod-cta");
const result=root.createDiv();
result.style.cssText="padding:12px;background:var(--background-secondary);border-radius:8px;margin-top:10px;";
function showParts(){
 partList.empty();chosenPart.empty();
 const found=entries[monster.value]||[];
 if(!found.length){
  partList.setText(names.length?"No matching creature. Try part of its name, or use the matching-creatures dropdown.":"Appendix B lookup unavailable. Save the downloaded Appendix B - Parts by Creature.md in the same 1. DM Screen folder as this note, then reopen the note.");
  chosenLabel.style.display="none";
  return;
 }
 chosenLabel.style.display="";
 chosenLabel.prependText("Harvest target: ");
 const table=partList.createEl("table");
 const hdr=table.createEl("tr");
 ["Part","Estimated total available","PDF page"].forEach(h=>hdr.createEl("th",{text:h}));
 found.forEach((e,i)=>{
  const tr=table.createEl("tr");
  [e.part,e.max,e.page].forEach(v=>tr.createEl("td",{text:v}));
  chosenPart.createEl("option",{text:e.part,value:String(i)});
 });
}
function options(){
 const q=search.value.toLowerCase().trim();
 monster.empty();
 hints.empty();
 const matches=names.filter(n=>n.toLowerCase().includes(q));
 matches.forEach(n=>monster.createEl("option",{value:n,text:n}));
 matches.slice(0,40).forEach(n=>hints.createEl("option",{value:n}));
 if(names.includes(search.value))monster.value=search.value;
 showParts();
}
search.oninput=options;
search.onchange=options;
monster.onchange=()=>{search.value=monster.value;showParts();};
options();
function update(){
 const [maximum,per]=specs[size.value];
 const dc=12+Math.max(0,Number(cr.value)<2?0:Number(cr.value)/2);
 info.setText("Use "+skillNames[creature.selectedIndex]+" · DC "+dc+" · max "+maximum+" checks · up to "+per+" unit(s) per successful check · 10 min/check.");
 return {maximum,per,dc};
}
[creature,cr,size].forEach(e=>e.onchange=update);update();
result.setText("Select the monster and part, then roll. Creature type, CR and size remain editable because Appendix B does not supply full stat blocks.");
roll.onclick=()=>{
 const {maximum,per,dc}=update();
 const n=Math.min(maximum,Math.max(1,Math.floor(Number(attempts.value)||1)));
 const mod=Number(bonus.value)||0;
 const list=entries[monster.value]||[];
 const part=list[Number(chosenPart.value)];
 result.empty();
 if(!part){result.setText("Choose a creature and part from the Appendix B lookup first.");return;}
 result.createEl("strong",{text:monster.value+" → "+part.part+" (Appendix B maximum: "+part.max+"; p. "+part.page+")"});
 let wins=0;
 for(let i=0;i<n;i++){
  const die=Math.floor(Math.random()*20)+1,total=die+mod,pass=total>=dc;
  if(pass)wins++;
  result.createEl("div",{text:"Check "+(i+1)+": "+die+" + ("+mod+") = "+total+" vs DC "+dc+" — "+(pass?"SUCCESS":"FAIL — attempted part destroyed")});
 }
 result.createEl("div",{text:"Successful checks: "+wins+"/"+n+". Size-based potential: up to "+(wins*per)+" units. Apply the part's Appendix B limit ("+part.max+") and any special creature rules."});
 const note=monster.value+" — "+part.part+" — "+wins+" successful checks; ≤"+(wins*per)+" size-based units; Appendix B limit "+part.max;
 const copy=result.createEl("button",{text:"Copy harvest result"});copy.style.marginTop="8px";
 copy.onclick=()=>navigator.clipboard.writeText(note);
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
