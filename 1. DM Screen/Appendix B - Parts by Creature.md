---
tags: [dm-screen, crafting, harvesting, city-and-wild]
source: "City and Wild v4.1, Appendix B pp. 121-129"
---
# Appendix B — Parts by Creature

> [!info] Source and interpretation
> Searchable transcription of the creature-specific part lists in *City and Wild v4.1*, Appendix B (pp. 121–129). Values are **estimated total material available**, **not automatic drops**. Roll the harvesting checks in [[Gathering and Harvesting - City and Wild]]. The source explicitly excludes ordinary bone, meat, blood, and common organs. Creature-type essence (1 unit per creature, when applicable) requires an Essence Extraction Device.

## Creature lookup

```dataviewjs
const text = await dv.io.load(dv.current().file.path);
const start=text.lastIndexOf('<!-- APPENDIX_B_START -->');
const end=text.lastIndexOf('<!-- APPENDIX_B_END -->');
const data=(start>=0&&end>start)?text.slice(start,end):'';
const creatures={};
for(const line of data.split('\n')){
 const m=line.match(/^\| ([^|]+) \| ([^|]+) \| ([^|]+) \| (\d+) \|$/);
 if(!m)continue;
 const name=m[1].trim();
 (creatures[name]??=[]).push({part:m[2].trim(),max:m[3].trim(),page:m[4]});
}
const wrap=dv.container.createDiv();
const bar=wrap.createDiv();bar.style.cssText='display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin:12px 0';
bar.createEl('span',{text:'Creature:'});
const search=bar.createEl('input',{attr:{type:'search',placeholder:'Search creature...'}});
search.style.cssText='padding:7px;min-width:160px';
const select=bar.createEl('select');select.style.maxWidth='320px';
const names=Object.keys(creatures).sort((a,b)=>a.localeCompare(b));
const shown=wrap.createDiv();
function options(){const q=search.value.toLowerCase();select.empty();for(const name of names.filter(n=>n.toLowerCase().includes(q)))select.createEl('option',{text:name,value:name});render()}
function render(){shown.empty();const name=select.value;const entries=creatures[name];if(!entries){shown.setText('No matching creature');return;}
 shown.createEl('h4',{text:name});
 const tab=shown.createEl('table');const tr=tab.createEl('tr');for(const h of ['Part','Estimated maximum','PDF page'])tr.createEl('th',{text:h});
 for(const e of entries){const tr=tab.createEl('tr');for(const value of [e.part,e.max,e.page])tr.createEl('td',{text:value});}
 shown.createEl('p',{text:'Actual yield requires the harvesting skill check and is subject to the creature-size limits and each specific part maximum.'});
}
search.oninput=options;select.onchange=render;options();
```

## Appendix B's special cases

- **Dragon variants (p. 123):** Adult/ancient dracoliches use the corresponding base dragon parts but change scale yields (adult: 1d6; ancient: 1d8). Shadow dragons have a shadow-specific essential organ and renamed scales/claws/horns/teeth/wings, plus one unit of shadow dragon dust. Other dragon kinds use the dragon age/size baseline, identified by dragon kind.
- **Faerie dragons (p. 123):** Their scale color identifies young versus older color groups; the tabulated parts are shared.
- **Giants, hags, and mephits (pp. 124–125):** Base part entries apply across their respective types, with type/race differences at the DM's discretion.
- **Slaad control gems (p. 126):** A slaad has a control gem only if born at the Spawning Stone in Limbo or an equivalent location. Listed gems are conditional.
- **Dice quantities:** Entries such as **4d4** are estimated available totals rolled once per creature, *not* guaranteed quantities per harvesting success.
- **Unlisted monsters:** The source offers no exact parts list for every possible or homebrew monster. Use creature anatomy and Chapter 7 guidance rather than inventing an official Appendix B entry.

## Source table (used by the lookup)

<!-- APPENDIX_B_START -->

| Creature | Part | Estimated total | PDF page |
|---|---|---|---|
| Aarakockra | aarakockra feathers | 1 | 121 |
| Aboleth | aboleth brain | 1 | 121 |
| Aboleth | aboleth hide | 4 | 121 |
| Aboleth | aboleth mucous | 1 | 121 |
| Aboleth | aboleth tail | 1 | 121 |
| Aboleth | aboleth teeth | 1d4 | 121 |
| Aboleth | aboleth tentacles | 3 | 121 |
| Air Elemental | elemental dust | 1 | 123 |
| Angel, Deva | deva feathers | 1 | 121 |
| Angel, Planetar | planetar feathers | 4 | 121 |
| Angel, Solar | solar feathers | 4 | 121 |
| Ankheg | ankheg acid | 1 | 121 |
| Ankheg | ankheg carapace | 4 | 121 |
| Ankheg | ankheg claws | 2 | 121 |
| Ankheg | ankheg mandibles | 1 | 121 |
| Ape | ape hide | 1 | 127 |
| Awakened Shrub | awakened shrub twigs | 1/2 | 127 |
| Awakened Tree | wood | 3 | 127 |
| Axe Beak | axe beak feathers | 2 | 127 |
| Azer | azer heart | 1 | 121 |
| Baboon | baboon hide | 1/2 | 127 |
| Badger | badger pelt | 1/4 | 127 |
| Banshee | banshee ectoplasm | 1 | 121 |
| Banshee | banshee dust | 1 | 121 |
| Basilisk | basilisk eyes | 2 | 121 |
| Basilisk | basilisk hide | 2 | 121 |
| Basilisk | basilisk teeth | 1d4 | 121 |
| Bat | bat wings | 1/4 | 127 |
| Behir | behir claws | 4d4 | 121 |
| Behir | behir essential organ | 1 | 121 |
| Behir | behir hide | 9 | 121 |
| Beholder | central beholder eye | 1 | 121 |
| Beholder | small beholder eyes | 2 | 121 |
| Beholder, Death Tyrant | death tyrant ectoplasm | 3 | 121 |
| Beholder, Spectator | central spectator eye | 1 | 121 |
| Beholder, Spectator | small spectator eyes | 1 | 121 |
| Black Bear | black bear hide | 1 | 127 |
| Blight, Needle Blight | needle blight roots | 1 | 121 |
| Blight, Twig Blight | twig blight roots | 1 | 121 |
| Blight, Vine Blight | vine blight roots | 1 | 121 |
| Blink Dog | blink dog hide | 1 | 127 |
| Blood Hawk | blood hawk feathers | 1/2 | 127 |
| Boar | boar hide | 1 | 127 |
| Boar | boar tusks | 1 | 127 |
| Brown Bear | brown bear hide | 2 | 127 |
| Bulette | bulette claws | 2 | 121 |
| Bulette | bulette scales | 2 | 121 |
| Cambion | cambion wings | 1 | 121 |
| Cambion | fiend heart | 1 | 121 |
| Camel | camel hide | 2 | 127 |
| Carrion Crawler | carrion crawler tentacles | 2 | 121 |
| Carrion Crawler | carrion crawler mucus | 1 | 121 |
| Cat | cat pelt | 1/4 | 127 |
| Chimera | chimera claws | 2 | 121 |
| Chimera | young red dragon essential organ | 1 | 121 |
| Chimera | young red dragon scales | 1 | 121 |
| Chimera | young red dragon wings | 4 | 121 |
| Chuul | chuul carapace | 2 | 121 |
| Chuul | chuul tentacles | 1 | 121 |
| Chuul | chuul pincers | 2 | 121 |
| Cloaker | cloaker eyes | 1 | 121 |
| Cloaker | cloaker hide | 2 | 121 |
| Cockatrice | cockatrice hide | 1 | 121 |
| Constrictor Snake | constrictor snake skin | 2 | 127 |
| Couatl | couatl feathers | 1 | 122 |
| Couatl | couatl hide | 1 | 122 |
| Couatl | couatl venom sac | 1 | 122 |
| Crab | crab carapace | 1/4 | 127 |
| Crocodile | crocodile hide | 2 | 127 |
| Crocodile | crocodile teeth | 2 | 127 |
| Cyclops | cyclops eye | 1 | 122 |
| Cyclops | cyclops toes | 2d4 | 122 |
| Darkmantle | darkmantle hide | 1 | 122 |
| Darkmantle | darkmantle tentacles | 1 | 122 |
| Death Dog | death dog pelt | 1 | 127 |
| Death Knight | death knight heart | 1 | 122 |
| Deer | deer hide | 1 | 127 |
| Demilich | demilich ectoplasm | 1/4 | 122 |
| Demon, Barlgura | barlgura hide | 2 | 122 |
| Demon, Chasme | chasme carapace | 2 | 122 |
| Demon, Chasme | chasme wings | 2 | 122 |
| Demon, Dretch | dretch fetid cloud sac | 1 | 122 |
| Demon, Glabrezu | glabrezu carapace | 2 | 122 |
| Demon, Glabrezu | glabrezu claws | 2 | 122 |
| Demon, Goristro | goristro hide | 6 | 122 |
| Demon, Goristro | goristro horns | 2 | 122 |
| Demon, Hezrou | hezrou claws | 2 | 122 |
| Demon, Hezrou | hezrou essential organ (stench) | 1 | 122 |
| Demon, Marilith | marilith snake tail | 2 | 122 |
| Demon, Nalfeshnee | nalfeshnee tusks | 2 | 122 |
| Demon, Nalfeshnee | nalfeshnee wings | 2 | 122 |
| Demon, Shadow Demon | shadow demon dust | 1 | 122 |
| Demon, Vrock | vrock hide | 4 | 122 |
| Demon, Vrock | vrock spores | 1 | 122 |
| Demon, Vrock | vrock wings | 2 | 122 |
| Demon, Yochlol | yochlol eye | 1 | 122 |
| Demon, Yochlol | yochlol slime | 1 | 122 |
| Devil, Barbed Devil | barbed devil hide | 1 | 122 |
| Devil, Bearded Devil | bearded devil beard | 1 | 122 |
| Devil, Bone Devil | bone devil poison | 1 | 122 |
| Devil, Erinyes | erinyes feathers | 2 | 122 |
| Devil, Horned Devil | horned devil horns | 2 | 122 |
| Devil, Horned Devil | horned devil wings | 2 | 122 |
| Devil, Ice Devil | ice devil carapace | 4 | 122 |
| Devil, Ice Devil | ice devil mandibles | 1 | 122 |
| Devil, Imp | imp wings | 1/4 | 122 |
| Devil, Pit Fiend | pit fiend hide | 4 | 122 |
| Devil, Pit Fiend | pit fiend horns | 2 | 122 |
| Devil, Pit Fiend | pit fiend wings | 2 | 122 |
| Devil, Spined Devil | spined devil hide | 1 | 122 |
| Devil, Spined Devil | spined devil wings | 2 | 122 |
| Dinosaur, Allosaurus | allosaurus claws | 2 | 122 |
| Dinosaur, Allosaurus | allosaurus hide | 4 | 122 |
| Dinosaur, Ankylosaurus | ankylosaurus hide | 6 | 122 |
| Dinosaur, Plesiosaurus | plesiosaurus hide | 4 | 122 |
| Dinosaur, Pteranodon | pteranodon wings | 2 | 122 |
| Dinosaur, Triceratops | triceratops hide | 6 | 122 |
| Dinosaur, Triceratops | triceratops horns | 3 | 122 |
| Dinosaur, Tyrannosaurus Rex | tyrannosaurus rex hide | 6 | 122 |
| Dinosaur, Tyrannosaurus Rex | tyrannosaurus rex teeth | 4d4 | 122 |
| Dire Wolf | dire wolf pelt | 2 | 128 |
| Displacer Beast | displacer beast hide | 4 | 122 |
| Displacer Beast | displacer beast tentacles | 2 | 122 |
| Doppelganger | doppelganger brain | 1 | 123 |
| Doppelganger | doppelganger flesh | 2 | 123 |
| Draft Horse | draft horse hooves | 1 | 128 |
| Dragon Turtle | dragon turtle claws | 6d6 | 123 |
| Dragon Turtle | dragon turtle hide | 12 | 123 |
| Dragon Turtle | dragon turtle shell fragments | 12 | 123 |
| Dragon, Adult | adult dragon claws | 4d4 | 123 |
| Dragon, Adult | adult dragon essential organ | 1 | 123 |
| Dragon, Adult | adult dragon horns | 2 | 123 |
| Dragon, Adult | adult dragon scales | 6 | 123 |
| Dragon, Adult | adult dragon teeth | 4d4 | 123 |
| Dragon, Adult | adult dragon wings | 6 | 123 |
| Dragon, Ancient | ancient dragon claws | 4d4 | 123 |
| Dragon, Ancient | ancient dragon essential organ | 1 | 123 |
| Dragon, Ancient | ancient dragon horns | 2 | 123 |
| Dragon, Ancient | ancient dragon scales | 8 | 123 |
| Dragon, Ancient | ancient dragon teeth | 4d4 | 123 |
| Dragon, Ancient | ancient dragon wings | 8 | 123 |
| Dragon, Shadow | shadow dragon dust | 1 | 123 |
| Dragon, Wyrmling | dragon wyrmling claws | 2 | 123 |
| Dragon, Wyrmling | dragon wyrmling essential organ | 1 | 123 |
| Dragon, Wyrmling | dragon wyrmling horns | 2 | 123 |
| Dragon, Wyrmling | dragon wyrmling scales | 2 | 123 |
| Dragon, Wyrmling | dragon wyrmling teeth | 1d4 | 123 |
| Dragon, Wyrmling | dragon wyrmling wings | 2 | 123 |
| Dragon, Young | young dragon claws | 1d4 | 123 |
| Dragon, Young | young dragon essential organ | 1 | 123 |
| Dragon, Young | young dragon horns | 2 | 123 |
| Dragon, Young | young dragon scales | 4 | 123 |
| Dragon, Young | young dragon teeth | 2d4 | 123 |
| Dragon, Young | young dragon wings | 4 | 123 |
| Drider | drider web sac | 1 | 123 |
| Dryad | dryad heart | 1 | 123 |
| Eagle | eagle feathers | 1/2 | 128 |
| Earth Elemental | elemental rock shards | 1 | 123 |
| Elephant | elephant hide | 6 | 128 |
| Elephant | elephant tusks | 2 | 128 |
| Elk | elk antlers | 1 | 128 |
| Elk | elk hide | 2 | 128 |
| Empyrean | empyrean heart | 1 | 123 |
| Ettercap | ettercap claws | 1 | 123 |
| Ettercap | ettercap poison | 1 | 123 |
| Ettercap | ettercap silk gland | 1 | 123 |
| Ettin | ettin tusk | 2 | 123 |
| Ettin | ettin toes | 2d4 | 123 |
| Faerie Dragon | faerie dragon essential organ | 1/4 | 123 |
| Faerie Dragon | faerie dragon scales | 1/4 | 123 |
| Fire Elemental | elemental molten core | 1 | 123 |
| Flumph | flumph foul-smelling liquid | 1 | 124 |
| Flumph | flumph tendrils | 1 | 124 |
| Flying Snake | flying snake feathers | 1/4 | 128 |
| Flying Snake | flying snake hide | 1/4 | 128 |
| Fomorian | fomorian evil eye | 1 | 124 |
| Fomorian | fomorian fingers | 2d4 | 124 |
| Fungi, Gas Spore | gas spore poisonous gas | 2 | 124 |
| Fungi, Violet Fungus | violet fungus stalks | 1 | 124 |
| Galeb Duhr | galeb duhr rocky skin | 1 | 124 |
| Gargoyle | gargoyle rocky skin | 1 | 124 |
| Ghast | ghast claws | 1 | 124 |
| Ghast | ghast stench | 1 | 124 |
| Ghost | ghost ectoplasm | 1 | 124 |
| Ghoul | ghoul claws | 1 | 124 |
| Giant | giant heart | 1 | 124 |
| Giant | giant toes | 2d4 | 124 |
| Giant Ape | giant ape hide | 3 | 128 |
| Giant Badger | giant badger hide | 1 | 128 |
| Giant Bat | giant bat hide | 2 | 128 |
| Giant Bat | giant bat wings | 2 | 128 |
| Giant Boar | giant boar hide | 2 | 128 |
| Giant Boar | giant boar tusks | 2 | 128 |
| Giant Centipede | giant centipede poison | 1/2 | 128 |
| Giant Constrictor Snake | giant constrictor snake skin | 4 | 128 |
| Giant Crab | giant crab carapace | 1 | 128 |
| Giant Crocodile | giant crocodile hide | 4 | 128 |
| Giant Crocodile | giant crocodile teeth | 3 | 128 |
| Giant Eagle | giant eagle feathers | 2 | 128 |
| Giant Elk | giant elk antlers | 1 | 128 |
| Giant Elk | giant elk hide | 4 | 128 |
| Giant Fire Beetle | giant fire beetle carapace | 1 | 128 |
| Giant Fire Beetle | giant fire beetle glowing glands | 1 | 128 |
| Giant Frog | giant frog skin | 1 | 128 |
| Giant Frog | giant frog tongue | 1 | 128 |
| Giant Goat | giant goat pelt | 2 | 128 |
| Giant Goat | giant goat horns | 1 | 128 |
| Giant Hyena | giant hyena pelt | 2 | 128 |
| Giant Lizard | giant lizard scales | 2 | 128 |
| Giant Octopus | giant octopus tentacles | 3 | 128 |
| Giant Octopus | giant octopus ink sac | 1 | 128 |
| Giant Owl | giant owl feathers | 2 | 128 |
| Giant Poisonous Snake | giant poisonous snake skin | 1 | 128 |
| Giant Poisonous Snake | giant poisonous snake poison | 1 | 128 |
| Giant Rat | giant rat hide | 1/2 | 128 |
| Giant Scorpion | giant scorpion carapace | 2 | 128 |
| Giant Scorpion | giant scorpion claws | 2 | 128 |
| Giant Scorpion | giant scorpion sting | 1 | 128 |
| Giant Scorpion | giant scorpion venom sac | 1 | 128 |
| Giant Sea Horse | giant sea horse hide | 2 | 128 |
| Giant Shark | giant shark skin | 4 | 128 |
| Giant Spider | giant spider venom | 1 | 128 |
| Giant Spider | giant spider web sac | 1 | 128 |
| Giant Toad | giant toad tongue | 1 | 128 |
| Giant Toad | giant toad skin | 2 | 128 |
| Giant Vulture | giant vulture feathers | 2 | 128 |
| Giant Wasp | giant wasp stinger | 1 | 128 |
| Giant Weasel | giant weasel hide | 1 | 128 |
| Giant Wolf Spider | giant wolf spider venom | 1 | 129 |
| Giant Wolf Spider | giant wolf spider web sac | 1 | 129 |
| Gibbering Mouther | gibbering mouther eyes | 1 | 124 |
| Gibbering Mouther | gibbering mouther spittle gland | 1 | 124 |
| Goat | goat pelt | 1 | 129 |
| Gorgon | gorgon hide | 2 | 124 |
| Gorgon | gorgon horns | 2 | 124 |
| Gorgon | gorgon petrifying gas sac | 1 | 124 |
| Grell | grell beak | 1 | 124 |
| Grell | grell tentacles | 1d4 | 124 |
| Grick | grick beak | 1 | 124 |
| Grick | grick hide | 1 | 124 |
| Grick | grick tentacles | 1d4 | 124 |
| Grick Alpha | grick alpha beak | 1 | 124 |
| Grick Alpha | grick alpha hide | 2 | 124 |
| Grick Alpha | grick alpha tentacles | 1d4 | 124 |
| Griffon | griffon claws | 2 | 124 |
| Griffon | griffon feathers | 2 | 124 |
| Hag | hag claws | 1 | 124 |
| Hag | hag heart | 1 | 124 |
| Half-Ogre | half ogre toes | 1d4 | 125 |
| Harpy | harpy feathers | 1 | 124 |
| Hawk | hawk feathers | 1/4 | 129 |
| Hell Hound | hell hound essential organ | 1 | 124 |
| Hell Hound | hell hound hide | 1 | 124 |
| Hell Hound | hell hound teeth | 1 | 124 |
| Hippogriff | hippogriff claws | 2 | 124 |
| Hippogriff | hippogriff feathers | 2 | 124 |
| Hook Horror | hook horror carapace | 2 | 124 |
| Hook Horror | hook horror hooks | 2 | 124 |
| Hunter Shark | hunter shark skin | 2 | 129 |
| Hydra | hydra scales | 9 | 124 |
| Hydra | hydra teeth | 4d4 | 124 |
| Hyena | hyena pelt | 1 | 129 |
| Intellect Devourer | intellect devourer brain matter | 1 | 124 |
| Intellect Devourer | intellect devourer claws | 1 | 124 |
| Jackal | jackal pelt | 1 | 129 |
| Kenku | kenku feathers | 1 | 124 |
| Killer Whale | killer whale skin | 4 | 129 |
| Kraken | kraken hide | 15 | 124 |
| Kraken | kraken ink sac | 4 | 124 |
| Kraken | kraken scales | 15 | 124 |
| Kraken | kraken teeth | 6d4 | 124 |
| Kraken | kraken tentacles | 2d4 | 124 |
| Lamia | lamia claws | 2 | 124 |
| Lamia | lamia heart | 1 | 124 |
| Lich | lich ectoplasm | 1 | 125 |
| Lion | lion hide | 2 | 129 |
| Lizard | lizard scales | 1/4 | 129 |
| Magmin | magmin molten skin | 1 | 125 |
| Mammoth | mammoth hide | 4 | 129 |
| Mammoth | mammoth tusks | 2 | 129 |
| Manticore | maticore tail spike | 1 | 125 |
| Manticore | manticore teeth | 2 | 125 |
| Manticore | manticore wings | 2 | 125 |
| Mastiff | mastiff hide | 1 | 129 |
| Medusa | medusa head | 1 | 125 |
| Mephit | mephit core | 1 | 125 |
| Merfolk | merfolk hide | 1 | 125 |
| Merrow | merrow hide | 2 | 125 |
| Mind Flayer | mind flayer brain | 1 | 125 |
| Mind Flayer | mind flayer tentacles | 1 | 125 |
| Minotaur | minotaur horns | 2 | 125 |
| Mule | mule hide | 1 | 129 |
| Mummy | mummy heart | 1 | 125 |
| Mummy | mummy wrappings | 2 | 125 |
| Mummy Lord | mummy lord dust | 2 | 125 |
| Mummy Lord | mummy lord wrappings | 2 | 125 |
| Myconid Adult | myconid adult spores | 1 | 125 |
| Myconid Sovereign | myconid sovereign spores | 2 | 125 |
| Myconid Sprout | myconid sprout spores | 1 | 125 |
| Naga, Bone | bone naga fangs | 2d4 | 125 |
| Naga, Guardian | guardian naga fangs | 2d4 | 125 |
| Naga, Guardian | guardian naga scales | 2 | 125 |
| Naga, Guardian | guardian naga poison gland | 1 | 125 |
| Naga, Spirit | spirit naga fangs | 2d4 | 125 |
| Naga, Spirit | spirit naga scales | 2 | 125 |
| Nightmare | nightmare hooves | 1 | 125 |
| Nothic | nothic claws | 1 | 125 |
| Nothic | nothic eye | 1 | 125 |
| Octopus | octopus tentacles | 1 | 129 |
| Octopus | octopus ink sac | 1/2 | 129 |
| Ogre | ogre toes | 2d4 | 125 |
| Oni | oni claws | 1 | 125 |
| Oni | oni ivory horns | 1 | 125 |
| Oni | oni toes | 2d4 | 125 |
| Ooze, Black Pudding | black pudding goo | 2 | 125 |
| Ooze, Gelatinous Cube | gelatinous cube gel | 2 | 125 |
| Ooze, Gray | gray ooze slime | 1 | 125 |
| Ooze, Ochre Jelly | ochre jelly slime | 2 | 125 |
| Otyugh | otyugh teeth | 2 | 125 |
| Otyugh | otyugh tentacles | 2 | 125 |
| Owl | owl feathers | 1/4 | 129 |
| Owlbear | owlbear claws | 1 | 125 |
| Owlbear | owlbear feathers | 2 | 125 |
| Owlbear | owlbear hide | 1 | 125 |
| Panther | panther hide | 1 | 129 |
| Pegasus | pegasus feathers | 2 | 125 |
| Pegasus | pegasus hooves | 1 | 125 |
| Peryton | peryton antlers | 1 | 125 |
| Peryton | peryton feathers | 1 | 125 |
| Peryton | peryton talons | 1 | 125 |
| Phase Spider | phase spider venom | 1 | 129 |
| Phase Spider | phase spider web sac | 1 | 129 |
| Piercer | piercer hide | 1 | 125 |
| Pixie | pixie dust | 1/4 | 126 |
| Poisonous Snake | poisonous snake skin | 1/4 | 129 |
| Poisonous Snake | poisonous snake poison | 1/4 | 129 |
| Polar Bear | polar bear hide | 2 | 129 |
| Pony | pony hooves | 1 | 129 |
| Pseudodragon | pseudodragon scales | 1/4 | 126 |
| Pseudodragon | pseudodragon venom | 1/4 | 126 |
| Purple Worm | purple worm hide | 8 | 126 |
| Purple Worm | purple worm teeth | 4d4 | 126 |
| Purple Worm | purple worm venom | 2d4 | 126 |
| Quaggoth | quaggoth claws | 1 | 126 |
| Quaggoth | quaggoth hide | 1 | 126 |
| Rat | rat pelt | 1/4 | 129 |
| Raven | raven feathers | 1/4 | 129 |
| Reef Shark | reef shark skin | 1 | 129 |
| Remorhaz | remorhaz carapace | 4 | 126 |
| Remorhaz | remorhaz heat organ | 1 | 126 |
| Remorhaz | remorhaz legs | 3d4 | 126 |
| Remorhaz, Young | young remorhaz carapace | 2 | 126 |
| Remorhaz, Young | young remorhaz heat organ | 1 | 126 |
| Remorhaz, Young | young remorhaz legs | 2d4 | 126 |
| Rhinoceros | rhinoceros hide | 2 | 129 |
| Rhinoceros | rhinoceros horns | 2 | 129 |
| Riding Horse | riding horse hooves | 1 | 129 |
| Roc | roc feathers | 8 | 126 |
| Roc | roc talons | 2d4 | 126 |
| Roper | roper hide | 2 | 126 |
| Roper | roper tendrils | 1d6 | 126 |
| Roper | roper teeth | 1d4 | 126 |
| Rust Monster | rust monster antennae | 1 | 126 |
| Rust Monster | rust monster carapace | 1 | 126 |
| Saber-Toothed Tiger | saber-toothed tiger hide | 2 | 129 |
| Saber-Toothed Tiger | saber-toothed tiger fangs | 1 | 129 |
| Salamander | salamander scales | 2 | 126 |
| Salamander, Fire Snake | fire snake scales | 1 | 126 |
| Scorpion | scorpion venom | 1/4 | 129 |
| Shadow | shadow ectoplasm | 1 | 126 |
| Shadow | shadow dust | 1 | 126 |
| Shambling Mound | shambling mound root-stem | 1 | 126 |
| Shambling Mound | shambling mound vines | 2 | 126 |
| Slaad, Blue | blue slaad claws | 1 | 126 |
| Slaad, Blue | blue slaad control gem | 1 | 126 |
| Slaad, Blue | blue slaad hide | 2 | 126 |
| Slaad, Death | death slaad claws | 1 | 126 |
| Slaad, Death | death slaad control gem | 1 | 126 |
| Slaad, Death | death slaad hide | 1 | 126 |
| Slaad, Gray | gray slaad claws | 1 | 126 |
| Slaad, Gray | gray slaad control gem | 1 | 126 |
| Slaad, Gray | gray slaad hide | 1 | 126 |
| Slaad, Green | green slaad claws | 1 | 126 |
| Slaad, Green | green slaad control gem | 1 | 126 |
| Slaad, Green | green slaad hide | 2 | 126 |
| Slaad, Red | red slaad claws | 1 | 126 |
| Slaad, Red | red slaad control gem | 1 | 126 |
| Slaad, Red | slaad eggs | 1d4 | 126 |
| Slaad, Red | red slaad hide | 1 | 126 |
| Specter | specter ectoplasm | 1 | 126 |
| Specter | specter dust | 1 | 126 |
| Sphinx, Androsphinx | androsphinx feathers | 2 | 126 |
| Sphinx, Androsphinx | androsphinx hide | 2 | 126 |
| Sphinx, Gynosphinx | gynosphinx feathers | 2 | 126 |
| Sphinx, Gynosphinx | gynosphinx hide | 2 | 126 |
| Spider | spider venom | 1/4 | 129 |
| Sprite | sprite dust | 1/4 | 126 |
| Succubus & Incubus | succubus/incubus claws | 1 | 126 |
| Succubus & Incubus | succubus/incubus wings | 1 | 126 |
| Tarrasque | tarrasque carapace | 15 | 126 |
| Tarrasque | tarrasque hide | 15 | 126 |
| Tarrasque | tarrasque teeth | 6d4 | 126 |
| Tarrasque | tarrasque horns | 6d4 | 126 |
| Thri-Kreen | thri-kreen carapace | 1 | 126 |
| Thri-Kreen | thri-kreen venom | 1 | 126 |
| Tiger | tiger hide | 2 | 129 |
| Treant | treant bark | 6 | 126 |
| Treant | treant branches | 4d4 | 126 |
| Treant | treant roots | 4d4 | 126 |
| Umber Hulk | umber hulk carapace | 3 | 127 |
| Umber Hulk | umber hulk mandibles | 2 | 127 |
| Unicorn | unicorn hooves | 1 | 127 |
| Unicorn | unicorn horn | 1 | 127 |
| Vampire | vampire dust | 1 | 127 |
| Vampire | vampire fangs | 1 | 127 |
| Vampire | vampire heart | 1 | 127 |
| Vampire Spawn | vampire spawn dust | 1 | 127 |
| Vampire Spawn | vampire spawn fangs | 1 | 127 |
| Vampire Spawn | vampire spawn heart | 1 | 127 |
| Vulture | vulture feathers | 1 | 129 |
| Warhorse | warhorse hooves | 1 | 129 |
| Water Elemental | elemental water | 1 | 123 |
| Weasel | weasel pelt | 1/4 | 129 |
| Will-o’-Whisp | will-o’-whisp dust | 1/4 | 127 |
| Will-o’-Whisp | will-o’-whisp ectoplasm | 1/4 | 127 |
| Winter Wolf | winter wolf hide | 2 | 129 |
| Wolf | wolf hide | 1 | 129 |
| Worg | worg hide | 2 | 129 |
| Wraith | wraith dust | 1 | 127 |
| Wraith | wraith ectoplasm | 1 | 127 |
| Wyvern | wyvern scales | 2 | 127 |
| Wyvern | wyvern stinger | 1 | 127 |
| Wyvern | wyvern teeth | 1 | 127 |
| Wyvern | wyvern venom | 2 | 127 |
| Wyvern | wyvern wings | 2 | 127 |
| Xorn | xorn rocky hide | 1 | 127 |
| Xorn | xorn teeth | 1d4 | 127 |
| Yeti | yeti hide | 2 | 127 |
| Yeti | yeti horns | 2 | 127 |
| Yeti | yeti eyes | 2 | 127 |
| Yeti, Abominable | yeti hide | 3 | 127 |
| Yeti, Abominable | yeti horns | 2 | 127 |
| Yeti, Abominable | yeti eyes | 2 | 127 |
| Yuan-Ti Abomination | yuan-ti abomination scales | 2 | 127 |
| Yuan-Ti Abomination | yuan-ti abomination fangs | 1 | 127 |
| Yuan-Ti Abomination | yuan-ti abomination venom | 1 | 127 |
| Yuan-Ti Malison | yuan-ti malison scales | 1 | 127 |
| Yuan-Ti Malison | yuan-ti malison venom | 1 | 127 |

<!-- APPENDIX_B_END -->
