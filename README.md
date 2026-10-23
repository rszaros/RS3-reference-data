# RS3 reference data for Slayer Helper

Reference material collected while building the Slayer Helper plugin
(`C:\ProgramData\Jagex\RuneScape-BETA\dev_plugins\slayer-helper\`). Nothing in
this folder is shipped with the plugin. It holds three kinds of files:

1. **Game exports**: name lists and dumps taken from the RS3 Beta client.
2. **Wiki data**: raw RuneScape Wiki data and notes (CC BY-NC-SA 3.0).
3. **Notes**: what was found, tested or decided, written for later reference.

Open questions and the to-do list are kept in the plugin's own
`OPEN_POINTS.md`, not here.

## 1. Game exports (Beta client, 2026-10-20)

Made with the console command `pan <Type>` (Alt+` opens the console; the list
is copied to the clipboard and then saved here). Each line is `id NAME`,
sometimes with extra columns.

| File | Source | Format and use |
|---|---|---|
| `pan-VarPlayer.txt` | `pan VarPlayer` | `id NAME TYPE [base-var mask]`. A negative id is a varbit: bits `mask` of VarPlayer `base-var`. Read in a plugin with `var.VarPlayer[NAME].value`. |
| `pan-VarClient.txt` | `pan VarClient` | `id NAME TYPE`. Client-side vars, read with `var.VarClient[NAME].value`. |
| `pan-Quest.txt` | `pan Quest` | `id CONFIG_NAME`. Use with `config.Quest[name].hasFinishedQuest`. |
| `pan-NPC.txt` | `pan NPC` | `id CONFIG_NAME`. Use with `config.NPC[name]`, e.g. to draw a monster model. |
| `pan-Obj.txt` | `pan Obj` | `id CONFIG_NAME`. Item config names, e.g. for item icons. |
| `pan-Enum.txt` | `pan Enum` | `id NAME INPUT_TYPE OUTPUT_TYPE`. Read with `config.Enum[name].values`. |
| `pan-Struct.txt` | `pan Struct` | `id NAME`. Read with `config.Struct[name]`. |
| `pan-DBTable.txt` | `pan DBTable` | `id NAME`. |
| `pan-DBRow.txt` | `pan DBRow` | `id NAME`. Read with `config.DBRow[name]`. |
| `pan-Sprite.txt` | sprite list | `id NAME`. Game sprites, e.g. skill icons `SKILL_SLAYER` via `id.Sprite[...]`. |
| `pan-Interface.txt` | `pan Interface` | `id NAME`. Game interfaces. |
| `pan-Component.txt` | `pan Component` | `id INTERFACE__COMPONENT`. Parts of game interfaces. |
| `clip-*.txt` | raw clipboard saves | The same lists before they were renamed (`clip-191359` = sprites, `clip-193520` = objs, `clip-195437` = interfaces, `clip-195454` = components). Use the `pan-*` files instead. |

Dumps made by the plugin itself:

| File | Contents |
|---|---|
| `master-tasks.txt` | Every task of the 12 Slayer masters as the game holds it: `master_id`, master enum, entry, `task_id`, Slayer and combat requirement, `example_npc` (the game's example monster per task), name. |
| `game-inventory.txt` | Full dump of the task structs (`S|` lines) and their example NPCs with params (`N|` lines). |
| `game-inventory-summary.txt` | Which params the task structs and NPCs have, with counts and examples. |
| `codex.txt` | The Slayer Codex creature list: `index`, NPC, Codex struct, name. |
| `quests.txt` | All quests: `id`, config name, display name, quest points. |

## 2. Wiki data (`wiki/`)

Fetched with the plugin's tools (`tools/fetch_wiki_data.py`,
`tools/fetch_locations.py`). Source: https://runescape.wiki, CC BY-NC-SA 3.0.

| File | Contents |
|---|---|
| `wiki/monsters.tsv` | Every monster with a Slayer category (wiki Bucket `infobox_monster`): page, level, Slayer level and XP, category, and more. |
| `wiki/assignment_<Master>.lua` | Raw wiki module per Slayer master: task weights, amounts and requirements. |
| `wiki/assignment_summary.tsv` | Parsed table of the "Slayer training" guide's assignment summary. |
| `wiki/slayer_training.wikitext` | Raw text of the "Slayer training" guide. |
| `wiki/slayer-training-notes.md` | Digest of that guide: masters and points, spending order, rewards, quest requirements, Codex bonus. Read this instead of the raw page. |
| `wiki/pages/*.wiki` | Cached wikitext of 697 monster pages (for the Locations tables). |
| `wiki/fetch_log.txt` | What was fetched, with revision ids and problems. |

## 3. Generated data (`generated/`)

Made by the plugin's tools from the files above. Staged here for review;
only reviewed data is copied into the plugin's `data/` folder.

| File | Contents |
|---|---|
| `generated/<master>.lua` | Task tables per Slayer master (weights, amounts, requirements), made by `tools/gen_master_tasks.py`. |
| `generated/gen_log.txt` | Log of that generator. |
| `generated/locations_review.md` / `.tsv` | All wiki Locations rows (964) for the tasks that had no locations yet: per monster the location, spawns, level and members flag. Leagues fields are left out on purpose. |
| `generated/locations_grouped.md` | Filter proposal: per task the same location merged over its monsters, top 5 by spawns, plus a "Special" list of rows with 0 spawns (special requirements, bosses, events). |

## 4. Notes

| File | Contents |
|---|---|
| `slayer-vars.md` | All Slayer-related game vars found and tested in the Beta (task, kills left, master, points, streak, unlocks, tool belt, pets, tokens, XP at 200m). The main reference for the plugin's game hookup. |
| `api-feasibility.md` | What the plugin API can and cannot do (from the developer docs), per topic. |
| `guidelines-data-storage.md` | Jagex guidelines on storing data per player (data protection cases). |
| `wiki-slayer-helmet.md` | Slayer helmet and its parts. |
| `wiki-slayer-equipment.md` | Slayer equipment, with config names. |
| `wiki-slayer-rewards.md` | Slayer reward shop: unlocks, extensions, buys. |
| `wiki-legendary-pet.md` | Legendary pets and the Slayer Finisher ability. |
| `wiki-slayer-masks.md` | Slayer masks (Treasure Hunter) and what they do. |
| `wiki-slayer-collection-log.md` | The Slayer collection log: areas, items, game enums. |
| `wiki-ironman.md` | Ironman modes and their game vars. |
| `wiki-slayer-challenges.md` | Slayer challenges. |
| `globetrotter-vars.md` | Globetrotter outfit vars (Treasure Trails). Not part of the plugin; kept for reference. |

## Adding a new export

Run `pan <Type>` in the Beta console (for example `pan Seq` for animations),
save the clipboard here as `pan-<Type>.txt`, and add a row to the table above.
