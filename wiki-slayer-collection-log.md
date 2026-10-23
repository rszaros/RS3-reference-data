# Slayer collection log (RS3 wiki + game data reference)

Collected 2026-10-23. Wiki text via the MediaWiki API (`action=parse`) and the wiki drop
database (`action=bucket`, bucket `dropsline`). Licence: RuneScape Wiki, CC BY-NC-SA 3.0.
Quotes in "..." are verbatim; everything else is a summary. Not verified = our reading.

## The log

Source: https://runescape.wiki/w/Slayer_collection_log

- "The Slayer collection log is a collection log and book that keeps track of assorted drops received from Slayer monsters. It can be obtained from any Slayer Master's shop for free. The interface can also be accessed by right-clicking the Slayer kill counter and choosing the Collection Log option and via the Adventures interface".
- "Completing the collection in each area listed in the log will grant a title. Completing every collection will unlock the achievement The Ultimate Slayer". No title for General drops.
- "obtaining the item as a drop from any monster counts for the log. Items are counted at the time of the creatures death" (also with Scrimshaw of sacrifice, and drops not picked up). Not counted: metamorphic geodes, Motherlode Maw and "certain other non-combat methods".
- "The slayer log will not count past 65500 copies of a single item."
- Rarity column on the wiki: "This is the highest drop rate, see item page for drop rates per monster."

Update history: 4 Nov 2024 Spectral lens added (Kharidian Desert); 11 Apr 2023 Bone fragments (General) and Greater Sonic Wave Ability Codex (Wilderness) added; 25 Jul 2022 ectoplasmator fix; 30 May 2022 Jaws of the Abyss link fix; 27 Sep 2021 Senntisten wrongly complete fixed; 6 Apr 2021 logs stay open in combat, update live; 6 Apr 2020 open via Slayer counter fixed; 9 Dec 2019 favourite button; 23 Sep 2019 added.

## How the game stores it (pan lists, not verified in game)

- Per item a counter varbit `ITEMLOG_ITEM_<OBJ CONFIG NAME>` (1,083 such vars, all collection logs), e.g. `ITEMLOG_ITEM_GRANITE_SHIELD` (-45009, varp 8913 mask 0xffff), `ITEMLOG_ITEM_GRANITE_MAUL` (-45008, varp 8912 mask 0xffff0000), `ITEMLOG_ITEM_ABYSSAL_WHIP` (-22442). Masks are 16 bits, matching "will not count past 65500": the value is probably the number logged (0 = not yet). Some are 8 bits (e.g. `ITEMLOG_ITEM_ABYSSAL_SLAYER_WHIP` 0xff00).
- Per area an item list enum (INTEGER -> OBJ): `ITEMLOG_SLAYER_ASGARNIA_MISTHALIN_ITEM_LIST`, `_DAEMONHEIM_`, `_DESERT_`, `_FELDIP_`, `_FREMENNIK_`, `_KANDARIN_`, `_KARAMJA_`, `_KELDAGRIM_`, `_LOST_LANDS_`, `_MORYTANIA_`, `_OFF_WORLD_`, `_WILDERNESS_`, `_GENERAL_` (`..._ITEM_LIST`). No enum by that name for Havenhythe and Senntisten; they have structs `ITEMLOG_SLAYER_HAVENHYTHE` / `_SENNTISTEN` (the list may be a struct param: not verified).
- `ITEMLOG_SLAYER_ALL_LOGS_META` (INTEGER -> STRUCT) and structs `ITEMLOG_SLAYER_<AREA>` (15023-15034, 45440, 52981): probably area metadata (name, list, title).
- Title vars (2 bits each): `ITEMLOG_SLAYER_<AREA>_TITLE` for all 14 areas plus `ITEMLOG_SLAYER_ALL_LOGS_TITLE`; `ITEMLOG_SLAYER_LOG_RECEIVED` (book received).
- DBTable `COLLECTION_LOG`, DBRow `COLLECTION_LOG_SLAYER` (2634).
- How a plugin could read "have I logged this drop": walk the area enum (`config.Enum[...].values`, outputs are ObjTypes), and read `ITEMLOG_ITEM_` .. obj.configName (> 0 = logged). The var name = `ITEMLOG_ITEM_` + the item's config name is a pattern seen in the list, not verified for every item.

In-game test to confirm: read `ITEMLOG_ITEM_<X>` for an item the player has logged (expect its count) and one not logged (expect 0), and dump one area enum (dump_enum) to compare with the wiki list.

## Areas and items

Per item: wiki rarity (best rate), then Slayer drop sources from the wiki drop database, best rate first (max 4; `*` = not marked as a Slayer drop).

### Asgarnia & Misthalin (25 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Goblin mail | 10/128 | Goblin (10/128), Lumpnose (10/128), Brokeface (10/128), Hollowtoof (10/128), +9 more |
| Goblin book | 2/128 | Goblin (2/128), Goblin guard (Observatory) (2/128), Lumpnose (2/128), Brokeface (2/128), +6 more |
| Cornucopia | 5/128 | Oomlie bird (5/128), Chicken (1/128), Rooster (1/128), Seagull#Sarim 5 feathers (Very rare), +4 more |
| Off-hand rubber chicken | Always | Chicken (Always), Rooster (Always) |
| Crunchy claw token | 6/150 | Mogre (6/150) |
| Mudskipper hat | 4/128 | Mogre (4/128) |
| Flippers | 2/128 | Mogre (2/128) |
| Granite legs | 1/496 | Skeletal Wyvern (1/512) |
| Royal cape | 3/100 | Young grotworm (3/100), Grotworm (2/100), Mature grotworm (1/2,048) |
| Right skull half | 15/100 | Minotaur (3/100) |
| Left skull half | 15/80 | Ankou (elite) (3/80), Ankou (3/128) |
| Top of sceptre | 15/100 | Catablepon (3/100) |
| Bottom of sceptre | 15/100 | Flesh Crawler (3/100) |
| Shade robe top | 1/16 | Shade (1/16) |
| Shade robe bottom | 1/16 | Shade (1/16) |
| Bronze defender | 2/100 | Cyclops (2/100) |
| Iron defender | 2/100 | Cyclops (2/100) |
| Steel defender | 2/100 | Cyclops (2/100) |
| Black defender | 2/100 | Cyclops (2/100) |
| Mithril defender | 2/100 | Cyclops (2/100) |
| Adamant defender | 2/100 | Cyclops (2/100) |
| Rune defender | 1/4 | Cyclossus (1/4), Cyclops (2/100) |
| Dragon defender | 1/4 | Cyclossus (1/4), Cyclops (2/100) |
| Raptor key part 1 | 3 × 1/253 | Wyvern (elite) (1/256), Wyvern (1/256) |
| Wyvern crossbow | 3 × 1/1,940 | Wyvern (elite) (1/10,000), Wyvern (1/10,000), Raptor's chest of slaying (1/50) * |

### Daemonheim (14 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Adrenaline urn | 1/396 | Kal'gerion demon (1/1,024), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,024), Yor'Ger the Deceiver#Normal mode (1/400) *, Corrupted energy (medium) (Always) * |
| Demon slayer circlet | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/210), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Demon slayer torso | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/210), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Demon slayer skirt | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/210), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Demon slayer boots | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/210), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Demon slayer gloves | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/210), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Demon slayer crossbow | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/210), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Off-hand demon slayer crossbow | 1/175 | Demon boss#Wilderness (1/175), Demon boss#Non-Wilderness (1/256), Kal'gerion demon (1/896), Kal'gerion demon (The Shadow Reef)#Normal mode (1/1,400), +1 more |
| Kal'gerion battle commendation | 1/512 | Kal'gerion demon (1/512), Wythien (1/642) *, Motherlode Maw (1/1,292) *, Treasure chest (player-owned port) (1/1,927) * |
| Seeker's charm | 10/128 | Seeker (10/128), Flesh-hatcher Mhekarnahz (Rare) |
| Hexhunter bow | Always | Soulgazer (elite) (1/1,500), Flesh-hatcher Mhekarnahz (1/1,000,000), Soulgazer (1/1,500,000), Veil-ripper Ozharakha (Always) |
| Baby Soulgazer | 1/750 | not found in the drop database |
| Blood necklace shard | 1/126 | Edimmu (elite) (1/128), Edimmu (1/512) |
| Edimmu | 1/496 | not found in the drop database |

### Feldip Hills (3 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Hexcrest | 1/253 | Jungle strykewyrm (1/512) |
| Ascension Keystone | 1/50 | Scutarius (1/50), Legio Primus (1/64), Gladius (1/64), Legio Secundus (1/64), +6 more |
| Ascension grips | 1/1,994 | Legio Primus (1/2,056), Scutarius (1/2,056), Legio Secundus (1/2,056), Legio Tertius (1/2,056), +6 more |

### Fremennik Province (23 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Light mystic hat | 1/496 | Wall beast (1/512), Basilisk (1/512) |
| Light mystic robe top | 1/496 | Kurask (1/512) |
| Light mystic robe bottom | 1/496 | Turoth (1/512) |
| Light mystic gloves | 1/496 | Desert lizard (1/512), Small lizard (1/512), Lizard (1/512), Rock slug (1/512) |
| Light mystic boots | 1/496 | Cockatrice (1/512) |
| Basilisk boots | 1/360 | Basilisk (1/512) |
| Kurask boots | 1/360 | Kurask (1/512) |
| Turoth boots | 1/360 | Turoth (1/512) |
| Amulet of ranging | 3 × 1/248 | Aquanite (elite) (1/256), Aquanite (1/512) |
| Leaf-bladed sword | 1/1,012 | Kurask (1/1,024), Turoth (1/2,048) |
| Off-hand leaf-bladed sword | 1/1,012 | Kurask (1/1,024), Turoth (1/2,048) |
| Brine sabre | 1/496 | Brine rat (1/512) |
| Circular hide | 2/128 | Dagannoth#Ranged (2/128) |
| Flattened hide | 2/128 | Dagannoth#Ranged (2/128) |
| Stretched hide | 2/128 | Dagannoth#Ranged (2/128) |
| Spined boots | 2/128 | Dagannoth#Ranged (2/128), Rhazien#Manor Farm (Common) * |
| Spined gloves | 2/128 | Dagannoth#Ranged (2/128), Rhazien#Manor Farm (Common) * |
| Kurask head | 1/1,500 | Kurask (1/3,000) |
| Cockatrice head | 1/500 | Cockatrice (1/1,000) |
| Basilisk head | 1/1,000 | Basilisk (1/2,000) |
| Staff of light | 1/496 | Ice strykewyrm (1/2,000) |
| Raptor key part 4 | 1/253 | Acheron mammoth (1/256) |
| Mammoth tusk | Always | Acheron mammoth (Always) |

### Havenhythe (9 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Vampyrism gloves | 1/200 | Sanguine crawler (1/1,000), Sanguine creeper (Very rare) |
| Tainted seed | Very rare | Sanguine crawler (1/2,500), Sanguine creeper (Very rare) |
| Forgotten painting piece (1) | 1/128 | Sanguine werewolf (1/128), Sanguine Alpha (1/128), Ravenous strigoi (1/512), Sanguine Omega (Rare), +34 more |
| Forgotten painting piece (2) | 1/128 | Sanguine werewolf (1/128), Sanguine Alpha (1/128), Ravenous strigoi (1/512), Sanguine Omega (Rare), +34 more |
| Forgotten painting piece (3) | 1/128 | Sanguine werewolf (1/128), Sanguine Alpha (1/128), Ravenous strigoi (1/512), Sanguine Omega (Rare), +34 more |
| Forgotten painting piece (4) | 1/128 | Sanguine werewolf (1/128), Sanguine Alpha (1/128), Ravenous strigoi (1/512), Sanguine Omega (Rare), +34 more |
| Forgotten painting piece (5) | 1/128 | Sanguine werewolf (1/128), Sanguine Alpha (1/128), Ravenous strigoi (1/512), Sanguine Omega (Rare), +34 more |
| Crimson ichor | Always | Ravenous strigoi (6/128), Sanguine werewolf (3/128), Sanguine Alpha (3/128), Sanguine bear (Rare), +3 more |
| Nightblood ring | Very rare | Ravenous strigoi (Very rare) |

### Kandarin (16 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Tortoise shell | 10/128 | Warped tortoise (10/128), Tortoise#No riders (10/128) *, Tortoise#With riders (8/128) *, Spirit impling jar (1/130) *, +4 more |
| Perfect shell | 2/128 | Warped tortoise (2/128), Tortoise#With riders (2/128) * |
| Dragon full helm | 1/1,000 | Adamant dragon (1/5,000), Mithril dragon (1/32,512), Chewed bones (1/256) *, Metamorphic geode (1/336) *, +4 more |
| Chewed bones | Always | Mithril dragon (4/127), Holy scarab scroll (Bone Conjure) (293/33,611) * |
| Cresbot (unpoked) | 1/1,012 | Automaton Guardian (1/1,024), Automaton Generator (1/1,024), Automaton Tracer (1/1,024) |
| Static gloves | 1/1,012 | Automaton Guardian (1/1,024) |
| Pneumatic gloves | 1/1,012 | Automaton Tracer (1/1,024) |
| Tracking gloves | 1/1,012 | Automaton Generator (1/1,024) |
| Dark bow | 3 × 1/475 | Dark beast (elite) (1/480), Dark beast (1/1,024) |
| Razorback gauntlets | 1/554 | Airut (1/2,056), Beastmaster Durzag (1/554) * |
| Kaigi's journal pages | 1/10 | Airut (1/10) |
| Tuska mask upper tusks | 1/250 | Airut (1/250), Airut Brawler (1/250) * |
| Tuska mask lower tusks | 1/250 | Airut (1/250), Airut Brawler (1/250) * |
| Tuska mask headpiece | 1/250 | Airut (1/250), Airut Brawler (1/250) * |
| Tuska mask plate | 1/250 | Airut (1/250), Airut Brawler (1/250) * |
| Tuska mask top | 1/250 | Airut (1/250), Airut Brawler (1/250) * |

### Karamja (16 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Dragon platelegs | 5/256 | Elite rune dragon (5/256), The Magister (2/128), Rune dragon (1/256), Adamant dragon (1/512), +8 more |
| Dragon plateskirt | 5/256 | Elite rune dragon (5/256), The Magister (2/128), Rune dragon (1/256), Adamant dragon (1/512), +8 more |
| Whip vine | 1/496 | Mutated jadinko male (1/512), Mutated jadinko guard (1/2,048) |
| Toktz-mej-tal | 1/50 | TokHaar-Mej (Fight Cauldron) (1/50), TzHaar-Mej (6/129,280) |
| Toktz-xil-ul | 1/50 | TokHaar-Xil (Fight Cauldron) (1/50), TzHaar-Xil (360/142,080) * |
| Toktz-xil-ak | 1/50 | TokHaar-Xil (Fight Cauldron) (1/50), TzHaar-Xil (90/142,080) * |
| Toktz-xil-ek | 1/50 | TokHaar-Xil (Fight Cauldron) (1/50), TzHaar-Xil (9/142,080) * |
| TzHaar-Ket-Om | 1/50 | TokHaar-Ket Champion (1/50), TzHaar-Ket (36/12,928) |
| Toktz-ket-xil | 1/50 | TokHaar-Ket (Fight Cauldron) (1/50), TzHaar-Ket (36/12,928) |
| Obsidian cape | 1/150 | TokHaar-Hur (Fight Cauldron) (1/150), TzHaar-Ket (45/12,928), TzHaar-Mej (60/129,280), TzHaar-Xil (360/142,080) * |
| Ring of stone | 1/4,850 | TzHaar-Ket (1/5,000), TzHaar-Mej (1/5,000), TzHaar-Hur (1/5,000), TzHaar-Xil (1/5,000) * |
| Gemstone hauberk | 1/1,000 | Hydrix dragon (1/2,500) |
| Gemstone boots | 1/2,000 | Dragonstone dragon (1/5,000) |
| Gemstone gauntlets | 1/2,000 | Dragonstone dragon (1/5,000) |
| Gemstone helm | 1/2,000 | Onyx dragon (1/5,000) |
| Gemstone greaves | 1/2,000 | Onyx dragon (1/5,000) |

### Keldagrim (6 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Granite shield | 1/128 | Troll general (1/128), Pee Hat (1/128), Kraka (1/128), Ice troll grunt#Variant 2 (1/128), +7 more |
| Hand cannon | 1/132 | Chaos dwarf hand cannoneer (1/132) |
| Hand cannon shot | 3/132 | Chaos dwarf hand cannoneer (3/132) |
| Dragon throwing axe | 4/128 | Chaos Giant (4/128), Motherlode Maw (1/9,612) *, Wythien (1/14,388) *, Treasure chest (player-owned port) (1/43,164) * |
| Off-hand dragon throwing axe | 4/128 | Chaos Giant (4/128), Motherlode Maw (1/9,612) *, Wythien (1/14,388) *, Treasure chest (player-owned port) (1/43,164) * |
| Dragon pickaxe | 1/970 | Chaos Giant (1/1,000), Chaos dwarf hand cannoneer (1/3,000), Chaos dwarf (Chaos Dwarf Battlefield) (1/3,000), Triskelion Treasures (3/1,814) *, +5 more |

### Kharidian Desert (13 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Focus sight | 1/253 | Desert strykewyrm (1/512) |
| Dragon chainbody | 1/126 | Kalphite Queen (1/128), Exiled Kalphite Queen (1/128), Dust devil (elite) (1/4,096), Dust devil (1/32,768), +5 more |
| Vital spark | Common | The Magister (4/128), Corrupted scorpion (Uncommon), Corrupted scarab (Uncommon), Corrupted worker (Uncommon), +25 more |
| Corrupted gem | 1/5,000 | Corrupted scorpion (1/5,000), Corrupted scarab (1/5,000), Corrupted worker (1/5,000), Corrupted lizard (1/5,000), +11 more |
| Khopesh of the Kharidian | 1/8,000 | Corrupted scorpion (1/15,000), Corrupted scarab (1/15,000), Corrupted worker (1/15,000), Corrupted lizard (1/15,000), +11 more |
| Key to the Crossing | Always | The Magister (1/128), Corrupted scorpion (1/400), Corrupted scarab (1/400), Corrupted worker (1/400), +25 more |
| Raptor key part 2 | 3 × 1/253 | Ripper Demon (1/256), Slasher Demon (1/256) |
| Raptor key part 3 | 1/248 | Camel Warrior (1/256) |
| Camel staff | 1/1,940 | Camel Warrior (1/10,000), Raptor's chest of slaying (1/50) * |
| Ripper claw | 3 × 1/1,980 | Ripper Demon (1/10,000), Slasher Demon (1/10,000), Raptor's chest of slaying (1/50) * |
| Off-hand ripper claw | 3 × 1/1,980 | Ripper Demon (1/10,000), Slasher Demon (1/10,000), Raptor's chest of slaying (1/50) * |
| Nipper demon | 3 × 1/990 | not found in the drop database |
| Spectral lens | 1/506 | Profane Scabarite (1/4,096), Elite Profane Scabarite (1/4,096) |

### Lost Lands and Dungeons (28 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Black mask (10) | 3 × 1/248 | Cave horror (elite) (1/256), Unspeakable horror (elite) (1/256), Cave horror (1/512), Unspeakable horror (1/512) |
| Scare Tactics | 3 × 1/255 | Unspeakable horror (1/256), Unspeakable horror (elite) (1/256) |
| Brackish blade | 1/200 | 'Rum'-pumped crab (1/200) |
| Dragon boots | 1/128 | Spiritual mage (1/128), Metamorphic geode (1/336) *, Motherlode Maw (1/9,612) *, Wythien (1/14,388) *, +1 more |
| Dragon gauntlets | 1/248 | Spiritual mage (1/256) |
| Dragon limbs | 1/253 | Tormented demon (1/256) |
| Ruined dragon armour lump | 1/1,044 | Tormented demon (1/1,056) |
| Ruined dragon armour slice | 1/1,044 | Tormented demon (1/1,056) |
| Ruined dragon armour shard | 1/1,044 | Tormented demon (1/1,056) |
| Dragon claw | 1/253 | Tormented demon (1/256), Metamorphic geode (1/336) *, Motherlode Maw (1/9,612) *, Wythien (1/14,388) *, +1 more |
| Off-hand dragon claw | 1/253 | Tormented demon (1/256), Metamorphic geode (1/336) *, Motherlode Maw (1/9,612) *, Wythien (1/14,388) *, +1 more |
| Steadfast boots | 1/1,260 | Glacor (1/1,280) |
| Glaiven boots | 1/1,260 | Glacor (1/1,280) |
| Ragefire boots | 1/1,260 | Glacor (1/1,280) |
| Shards of Armadyl | 10/96 | Glacor (10/96) |
| Penny | Varies | not found in the drop database |
| Seiryu's claw | 1/1,000 | Arhat (1/1,024), Elite Sakadagami#Normal mode (1/1,000) * |
| The Path of the Monk | 1/16 | Anagami (1/16) *, Sakadagami (1/32) *, Sotapanna (1/64) * |
| The Path of the Elemental | 1/32 | Anagami (1/32) *, Sakadagami (1/64) *, Sotapanna (1/128) * |
| The Path of the Dragon | 1/64 | Anagami (1/64) *, Sakadagami (1/128) *, Sotapanna (1/256) * |
| Cinderbane gloves | 1/1,000 | Vinecrawler (1/5,000), Bulbous crawler (1/5,000), Moss golem (1/5,000), Solak, Guardian of the Grove (1/1,000) * |
| Ancient elven ritual shard | 1/1,000 | Vinecrawler (1/5,000), Bulbous crawler (1/5,000), Moss golem (1/5,000), Solak, Guardian of the Grove (1/1,000) * |
| Blowpipe chitin | 1/18,000 | Ripper dinosaur (1/20,000), Venomous dinosaur (1/20,000), Feral Dinosaur (1/20,000), Brutish dinosaur (1/20,000) |
| Blowpipe feather | 1/18,000 | Ripper dinosaur (1/20,000), Venomous dinosaur (1/20,000), Feral Dinosaur (1/20,000), Brutish dinosaur (1/20,000) |
| Blowpipe fins | 1/18,000 | Ripper dinosaur (1/20,000), Venomous dinosaur (1/20,000), Feral Dinosaur (1/20,000), Brutish dinosaur (1/20,000) |
| Bone blowpipe | 1/18,000 | Ripper dinosaur (1/20,000), Venomous dinosaur (1/20,000), Feral Dinosaur (1/20,000), Brutish dinosaur (1/20,000) |
| Laceration boots | 1/2,000 | Ripper dinosaur (1/8,000), Venomous dinosaur (1/8,000), Feral Dinosaur (1/8,000), Brutish dinosaur (1/8,000) |
| Blast diffusion boots | 1/2,000 | Liverworts (1/8,000), Luminous snaggler (1/8,000), Devil's snare (1/10,000), Lampenflora (1/16,000) |

### Morytania (28 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Congealed blood | 8 × 75/1,000 | Bloodveld (1/2), Ghast#Temple Trekking (1/10), Mutated bloodveld (1/10), Nechryael (elite) (1/10), +69 more |
| Black boots | 12/128 | Mutated bloodveld (12/128), Bloodveld (1/128), Bloodveld (God Wars Dungeon) (1/128) |
| Dark mystic hat | 3 × 1/768 | Infernal Mage (1/512), Infernal Mage (elite) (1/768) |
| Dark mystic robe top | 1/496 | Gargoyle (1/512), Gargoyle sentinel (1/512), WildyWyrm (2011, historical) (Rare) * |
| Dark mystic robe bottom | 1/496 | Aberrant spectre (1/512), WildyWyrm (2011, historical) (Rare) * |
| Dark mystic gloves | 1/256 | Mighty banshee (1/256), Banshee (1/512), Skeletal hand (2/2,316), Zombie hand (2/2,316) |
| Dark mystic boots | 3 × 1/768 | Infernal Mage (1/512), Infernal Mage (elite) (1/768) |
| Lava battlestaff | 2/128 | Aberrant spectre (2/128), Kalphite Queen (1/128), Exiled Kalphite Queen (1/128), Infernal Mage (elite) (1/768), +1 more |
| Granite maul | 1/496 | Gargoyle (1/512), Gargoyle sentinel (1/512) |
| Granite helm | 1/248 | Terror dog (1/256) |
| Abyssal wand | 3 × 1/1,484 | Abyssal demon (elite) (1/1,500), Abyssal demon (1/6,104) |
| Abyssal orb | 3 × 1/1,484 | Abyssal demon (elite) (1/1,500), Abyssal demon (1/6,104) |
| Abyssal whip | 3 × 1/485 | Abyssal demon (elite) (1/500), Abyssal demon (1/1,024) |
| Crawling hand (item) | 1/243 | Crawling hand (1/500), Skeletal hand (1/500), Zombie hand (1/500) |
| Abyssal head | 1/2,910 | Abyssal demon (elite) (1/6,000), Abyssal demon (1/6,000) |
| Ganodermic gloves | 1/101 | Ganodermic beast (1/101), Ganodermic runt (1/200) |
| Ganodermic boots | 1/101 | Ganodermic beast (1/101), Ganodermic runt (1/200) |
| Polypore stick | 1/101 | Ganodermic beast (1/101) |
| Grifolic shield | 1/60 | Grifolapine (1/60) |
| Grifolic wand | 1/60 | Grifolapine (1/60) |
| Grifolic orb | 1/60 | Grifolaroo (1/60) |
| Grifolic gloves | 1/60 | Grifolaroo (1/60) |
| Celestial handwraps | 5/1,000 | Celestial dragon (Dragonkin Laboratory)#Normal mode (5/1,000), Celestial dragon (1/2,056) |
| Dragon Rider helm | 1/5,120 | Celestial dragon (1/5,120) |
| Dragon Rider body | 1/5,120 | Celestial dragon (1/5,120) |
| Dragon Rider chaps | 1/5,120 | Celestial dragon (1/5,120) |
| Dragon Rider cape | 1/5,120 | Celestial dragon (1/5,120) |
| Dragon Rider kit | 1/5,120 | Celestial dragon (1/5,120) |

### Other Worlds (18 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Dragon ward | 1/506 | Force muspah (1/512) |
| Dragon hasta | 3 × 1/64 | Nodon guard (6/128), Nodon engineer (1/64), Nodon enforcer (1/64), Bladed muspah (1/512), +1 more |
| Dragon knife | 1/506 | Throwing muspah (1/512) |
| Off-hand dragon knife | 1/506 | Throwing muspah (1/512) |
| Vampyre fangs | 1/6 | Blood nihil (1/6) |
| Icyene feather | 1/6 | Ice nihil (1/6) |
| Demon horn | 1/6 | Shadow nihil (1/6) |
| Aviansie talons | 1/6 | Smoke nihil (1/6) |
| Attuned crystal weapon seed | 1/100 | Edimmu (elite) (1/100), Crystal Shapeshifter (1/1,024), Cadarn magus (40/100,000), Cadarn ranger (40/100,000), +2 more |
| Attuned crystal armour seed | 1/100 | Edimmu (elite) (1/100), Crystal Shapeshifter (1/1,024), Cadarn magus (40/100,000), Cadarn ranger (40/100,000), +2 more |
| Ancient elven wedding ring | 1/10 | Crystal Shapeshifter (1/1,000) |
| Nightmare gauntlets | 1/2,000 | Nightmare (1/2,000) |
| Steadfast scale | 1/582 | Elite rune dragon (1/588), Rune dragon (1/768), Ol' Sawtooth#Normal mode (1/5,000), Elite Sotapanna#Normal mode (1/10,000), +26 more |
| Glaiven wing-tip | 1/582 | Elite rune dragon (1/588), Rune dragon (1/768), Verak Lith#Normal mode (1/833), Astellarn#Normal mode (1/833), +26 more |
| Ragefire gland | 1/267 | Taraket the Necromancer#Normal mode (1/267), Quetzathog#Normal mode (1/267), Masuta the Descended#Normal mode (1/267), Elite rune dragon (1/588), +30 more |
| Kethsi ring (5) | 1/512 | Elite rune dragon (1/512), Rune dragon (1/1,024), Wythien (1/482) *, Motherlode Maw (1/969) *, +1 more |
| Kethsi outfit scroll | 1/1 | Elite rune dragon (1/200), Wythien (1/2,409) *, Motherlode Maw (1/4,846) *, Treasure chest (player-owned port) (1/7,226) * |
| Tuska's Wrath ability codex | 1/400 | Airut (1/1,000), Beastmaster's hound (1/1,000) |

### Senntisten (8 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Dwarf multicannon upgrade kit | 1/12.4 | Nodon enforcer (1/12.4), Nodon engineer (1/609.5), Nodon hunter (1/2,133.3), Nodon artificer (1/2,133.3), +2 more |
| Kinetic cyclone upgrade kit | 1/12.4 | Nodon enforcer (1/12.4), Nodon engineer (1/609.5), Nodon hunter (1/2,133.3), Nodon artificer (1/2,133.3), +2 more |
| Oldak coil upgrade kit | 1/12.4 | Nodon enforcer (1/12.4), Nodon engineer (1/609.5), Nodon hunter (1/2,133.3), Nodon artificer (1/2,133.3), +2 more |
| Steadfast boots | 1/1,260 | Glacor (1/1,280) |
| Glaiven boots | 1/1,260 | Glacor (1/1,280) |
| Ragefire boots | 1/1,260 | Glacor (1/1,280) |
| Abyssal scourge | 1/1,980 | Abyssal lord (1/10,000) |
| Jaws of the Abyss | 1/990 | Abyssal beast (1/5,000) |

### Wilderness (40 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Dragon chainbody | 1/126 | Kalphite Queen (1/128), Exiled Kalphite Queen (1/128), Dust devil (elite) (1/4,096), Dust devil (1/32,768), +5 more |
| Corrupt dragon helm | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon chainbody | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +11 more |
| Corrupt dragon platelegs | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon plateskirt | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon battleaxe | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon dagger | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon longsword | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon mace | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon scimitar | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon spear | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Corrupt dragon sq shield | 2/5,454 | Revenant dragon (2/5,454), Revenant knight (2/6,000), Revenant dark beast (2/6,000), Revenant ork (2/6,666), +12 more |
| Statius's full helm | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Statius's platebody | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Statius's platelegs | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Statius's warhammer | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Vesta's chainbody | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Vesta's plateskirt | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Vesta's longsword | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Vesta's spear | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Zuriel's hood | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Zuriel's robe top | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Zuriel's robe bottom | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Zuriel's staff | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Morrigan's coif | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Morrigan's leather body | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Morrigan's leather chaps | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Morrigan's javelin | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Morrigan's throwing axe | 10/92,718 | Revenant dragon (10/92,718), Revenant knight (10/102,000), Revenant dark beast (10/102,000), Revenant ork (10/113,322), +11 more |
| Ancient warriors' equipment patch | Very rare | Revenant dragon (5/5,454), Revenant knight (5/6,000), Revenant dark beast (5/6,000), Revenant ork (5/6,666), +50 more |
| Ancient crystal | Unknown | Revenant vampyre (Unknown), Revenant knight (Unknown), Revenant dark beast (Unknown), Revenant ork (Unknown), +13 more |
| Fremennik equipment patch | 1/314 | Greater demon berserker (1/314), Greater demon ash lord (1/336), Soulgazer (elite) (1/370), Veil-ripper Ozharakha (1/370), +53 more |
| Revenant drop enhancer | Very rare | Greater demon berserker (1/1,572), Greater demon ash lord (1/1,678), Soulgazer (elite) (1/1,852), Veil-ripper Ozharakha (1/1,852), +48 more |
| Wilderness hilt | Very rare | Greater demon berserker (1/1,572), Greater demon ash lord (1/1,678), Soulgazer (elite) (1/1,852), Veil-ripper Ozharakha (1/1,852), +55 more |
| Adrenaline crystal | 1/786 | Greater demon berserker (1/786), Greater demon ash lord (1/839), Soulgazer (elite) (1/926), Veil-ripper Ozharakha (1/926), +54 more |
| Revenant Spirit | 1/297 | Revenant dragon (1/297), Revenant knight (1/315), Revenant dark beast (1/334), Revenant ork (1/382), +13 more |
| Wyrm spike | 1/6,105 | WildyWyrm (2015, historical) (1/1,536), Lava strykewyrm (1/12,288), Wyrm reward gland (1/1,500) * |
| Wyrm heart | 1/6,105 | WildyWyrm (2015, historical) (1/1,536), Lava strykewyrm (1/12,288), Wyrm reward gland (1/1,500) * |
| Wyrm scalp | 1/6,105 | WildyWyrm (2015, historical) (1/1,536), Lava strykewyrm (1/12,288), Wyrm reward gland (1/1,500) * |
| Greater Sonic Wave ability codex | 1/506 | Armoured phantom (1/1,536), Risen ghost (1/4,608) |

### General drops (19 items)

| Item | Rarity (best) | Dropped by |
|---|---|---|
| Tooth half of a key | 6/52 | K'ril Tsutsaroth (1/625.64), Black demon (1/712.58), Dagannoth Prime (1/862.77), Dagannoth Supreme (1/862.77), +192 more |
| Loop half of a key | 6/52 | K'ril Tsutsaroth (1/625.64), Black demon (1/712.58), Dagannoth Prime (1/862.77), Dagannoth Supreme (1/862.77), +191 more |
| Ghostly essence | Always | Taraket the Necromancer#Normal mode (Solo) (100/1,000), Taraket the Necromancer#Normal mode (Duo) (100/1,000), Taraket the Necromancer#Normal mode (Trio) (100/1,000), Risen ghost (6/100), +40 more |
| Crystal triskelion fragment 1 | 1/11 | Abyssal lord (6/100), Kerapac, the bound#Normal mode (1/100), Kerapac, the bound#Hard mode (1/100), Arch-Glacor#Normal mode (1/100), +87 more |
| Crystal triskelion fragment 2 | 1/11 | Abyssal lord (6/100), Kerapac, the bound#Normal mode (1/100), Kerapac, the bound#Hard mode (1/100), Arch-Glacor#Normal mode (1/100), +87 more |
| Crystal triskelion fragment 3 | 1/11 | Abyssal lord (6/100), Kerapac, the bound#Normal mode (1/100), Kerapac, the bound#Hard mode (1/100), Arch-Glacor#Normal mode (1/100), +87 more |
| Starved ancient effigy | 3 × 1/256 | K'ril Tsutsaroth#Normal mode (1/128), K'ril Tsutsaroth#Hard mode (1/128), Kree'arra#Normal (1/128), Kree'arra#Hard mode (1/128), +192 more |
| Ferocious ring (5) | 3 × 1/140 | Airut (1/80), Steel dragon (1/100), Iron dragon (1/120), Dark beast (1/140), +8 more |
| Sirenic scale | 3/44 | Legio Primus (441/11,041), Legio Secundus (441/11,041), Legio Tertius (441/11,041), Legio Quartus (441/11,041), +73 more |
| Cursed Amascut sand | 2/300 | Acheron mammoth (1/1,024), Camel Warrior (1/1,024), Wyvern (elite) (1/1,024), Ripper Demon (1/1,024), +14 more |
| Draconic visage | 1/109 | Queen Black Dragon (1/109), Verak Lith#Normal mode (1/455), Astellarn#Normal mode (1/455), Black stone dragon#Normal mode (1/455), +52 more |
| Red dragon egg | 1/200 | Red dragon (1/200) |
| Blue dragon egg | 1/200 | Blue dragon (1/200) |
| Green dragon egg | 1/200 | Green dragon (1/200) |
| Black dragon egg | 1/200 | Black dragon (1/200) |
| Ectoplasmator | 1/400 | Edimmu (elite) (1/400), Edimmu (1/400), Evil spirit (1/500), Aberrant spectre (1/500), +53 more |
| Cremation ability | 1/1,000 | not found in the drop database |
| Deployable herb burner | 1/512 | Ankou (1/1,024), Ghast (1/1,024), Tortured soul (Port Phasmatys) (1/1,024), Loar Shade (1/1,024), +53 more |
| Bone fragments | 115/150 | Abyssal lord (115/150), Armoured phantom (113/150), Hydrix dragon (101/150), Onyx dragon (98/150), +49 more |
