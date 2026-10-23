# Slayer variables (Beta, 2026-10-20)

Source: `pan-VarPlayer.txt` (names) + the plugin's var sniffer log
(`D:\Downloads\slayer-helper-log.txt`). The plugin reads vars **by name**
(`var.VarPlayer["NAME"]`); ids are listed only for reference.

Status: **confirmed** = seen changing in game as expected;
**candidate** = name fits, not verified yet.

## Needed

| What | Name | Id / bits | Status |
|---|---|---|---|
| Kills left | `SLAYER_COUNT` | varp 183 | **confirmed**: became 265 on a 265 Dark beasts task |
| Current task | `SLAYER_TARGET` | varp 185 | **confirmed**: 66 on the Dark beasts task (46 on the task just before) |
| Slayer points | `SMKI_SLAYER_POINTS` | varbit -9072 = varp 2092 & 0x1ffff | **confirmed**: 2844 = game |
| Slayer master | `SLAYER_MASTER` | varbit -9073 = varp 2092 & 0x7e0000 | **confirmed**: 8 while on a Laniakea task; full id map below (`SLAYER_MASTER_ENUM`) |
| Task streak | `SMKI_MISSION_COUNT` | varp 10077 | **confirmed**: the only var of ~76k holding 1531 (= game). Not `BSLAY_TASK_STREAK` (838, boss slayer). |

Task completion (seen 2026-10-20): `SLAYER_COUNT` 1 -> 0, `SMKI_MISSION_COUNT`
1531 -> 1532, `SMKI_2` +22 (points live in its low 17 bits), and
`SLAYER_TARGET` does NOT change (keeps 66). So: kills left 0 = no task.
Varbits (points, master, block/prefer slots) get no VarTransmit of their
own: only their base var is sent (`SMKI_2`, `SMKI_3`, `SMKI_4`, `SMKI_5`,
`SMKI_6`, `SS2`). Re-read the varbits after any var change.

Slayer VIP ticket (seen 2026-10-20): the player picks between 2 tasks (a
third with an extra ticket). `SLAYER_TARGET`/`SLAYER_COUNT` change once per
offered task within seconds (171 Dinosaurs x85, then 30 Black demons x275),
with no points change. The last one is the task; not a cancel.

## Nice to have

| What | Name | Notes |
|---|---|---|
| Slayer Codex | `SLAYER_CODEX_1` … `SLAYER_CODEX_7` | varps 7020–7025, 12309; probably one bit per creature |
| Fort guardhouse | `PLAYER_FORT_BUILDING_GUARDHOUSE_SLAYER_UPGRADE_1..3`, `PLAYER_FORT_BUILDING_GUARDHOUSE_SLAYER_MASTER` | varbits on varp 10762 |
| Slayer challenges | `SLAYC_BASE`, `SLAYC_BASE2`, `SLAYC_BASE3`, `SLAYC_TASKS`, `SLAYC_TASKS_2` | packed; `SLAYC_BASE` changed 10 -> 138 when the task was assigned |
| Normal tasks done (challenge counter?) | `SLAYC_NORMAL_TASKS_DONE` | varbit on 190 & 0xf (0–15 only, so not the streak) |
| Wilderness tasks | `SLAYER_WILDERNESS_VAR`, `SLAYER_WILDERNESS_COUNT`, `SLAYER_WILDERNESS_REAPER_POINTS_TO_AWARD` | |
| Raptor | `FORT_SLAYER_RAPTOR_TASK_LENGTH`, `SLAYC_RAPTOR_CHALLENGE_COUNT/LENGTH` | |
| Kill counter setting | `SLAYER_TOGGLE_SLAYER_COUNTER`, `SLAYER_COUNTER_DISPLAY_MODE` | |

| Block list | `SMKI_IGNORE_FLAG_1` … `_8` | **confirmed**: 8 slots, task id each (0 = empty); 49/52/25 = Dust devils/Nechryael/Blue dragons as in game |
| Prefer list | `SMKI_PREFER_FLAG_1` … `_8` | **confirmed**: 8 slots, task id each (0 = empty); all 7 match the game |

Not found yet: toggled tasks (Muspah, Nihil …), Slayer reward unlocks,
Wilderness PvP state.

## Slayer Codex / ushabti (internal name: SLAYER_POD)

| What | Name | Status |
|---|---|---|
| Ushabti (empty) | obj `SLAYER_POD_SOUL_CATCHER_EMPTY` | **confirmed** in backpack (`Inventory.Find(config.Inv.INV)`, `GetSlots`) |
| Cursed ushabti (empty) | obj `SLAYER_POD_SOUL_CATCHER_EMPTY_BLESSED` | **confirmed**: "blessed" = cursed internally |
| Worn equipment | `config.Inv.WORN` | **confirmed** works (showed Mask of Gloom) |
| Codex progress | `SLAYER_CODEX_1` … `_7` | **confirmed** bit fields, one bit per collected creature: 175 bits on = "Monsters collected: 175/173" in game. Bit order is NOT the order of `SLAYER_POD_NPC_LIST` (that predicted Hydrix dragon missing, but it is collected). Cannot be worked out on a complete Codex; needs an account with gaps. List saved as `codex.txt` |
| Codex per creature | structs `SLAYER_POD_<CREATURE>` (e.g. `SLAYER_POD_DARK_BEAST`), enum `SLAYER_POD_MONSTER_STRUCT` (NPC -> struct), `SLAYER_POD_NPC_TO_MOB_ENUM`, `SLAYER_POD_NPC_LIST` | being checked |
| Fort guardhouse | `PLAYER_FORT_BUILDING_GUARDHOUSE_SLAYER_UPGRADE_1..3` | all 2 on the user's account, whose guardhouse is fully upgraded: 2 = max per upgrade. Which upgrade gives the Codex bonus ("tier 2+") cannot be told on a maxed account; assumption for now: bonus when the upgrades are at max |
| Slayer helmet stand (Anachronia) | `DINO_BASE_CAMP_SLAYER_STAND_STATE` (varbit, 2 bits) | candidate. Wiki (Slayer helmet stand): a corrupted helm ON THE STAND also gives the ushabti bonus, so worn OR on the stand counts |
| Corrupted slayer helmet | obj `SLAYER_HELMET_ALLCOMBATS_TIER4` + 49 variants | **confirmed** worn (`config.Inv.WORN`); only counts when worn. All 50 versions (colours, fused, charged/uncharged, bought) match `[BOUGHT_]SLAYER_HELMET_ALLCOMBATS..._TIER4` in `pan-Obj.txt`; TIER1-3 are lower helmets |

## Requirements (checked 2026-10-20 on an account that meets all)

| Requirement | Source | Value here |
|---|---|---|
| Access to Morytania | quest `PRIEST_IN_PERIL` finished | true (copy `PRIESTPERIL` reads false) |
| Partial Mourning's End II | quest `MOURNINGS_END_PART_2` started | true |
| Partial Icthlarin's Little Helper | quest `ICS_LITTLE_HELPER` started | true (copy `ICTHLARINS_LITTLE_HELPER` false) |
| GWD knight | `GODWARS_PALLADIN1`, `GODWARS_PALLADIN2` | 1, 1 (candidate) |
| Fire cape | `ATJUN_ELITE_FIRECAPE`, `TZKILN_SACRIFICED_FIRE_CAPE` | 1, 1 (candidate); `TZHAAR_FIGHTCAVE_STATE` = 0 |
| World Wakes extra rewards | `TSD_QUEST_LOCKED_REWARDS`, `TSD_SLAYER_LAMP` | 1, 1 (candidate); `MAH_ALI_WORLD_WAKES` = 0 is not it |
| Hard Karamja rewards | `ATJUN_HARD_REWARD` (`ATJUN_HARD_DONE`) | 1 (2) (candidate); `ATJUN_HARD_LAMP_RECIEVED` = 0 is not it |
| Barbarian Training | `BRUT_LOG_1..25` (varp 608), `BRUT_LOG_OVERRIDE` | all 1 / 33554431; pyre ship index unknown |

## Player profile (Player API + config.Quest)

Confirmed 2026-10-20 on the user's account: Slayer 120, combat 152,
quest points 473 (= the current maximum; user has all quests), Smoking
Kills done. Quest points = sum of `questPoints` over quests with
`hasFinishedQuest`; quests that exist twice have one copy with 0 points.
Caveat: on a maxed account every quest is done, so a mistake in the
"done" check would not show here; recheck on an account with fewer quests.
Quest name -> config name mapping: `quests.txt` (533 quests) and the
plugin's `data/quests.lua`.

## Master task entries (structs)

`SLAYER_MASTER_ENUM` (confirmed): master id (`SLAYER_MASTER`) -> the master's
task enum: 1 Turael, 2 Mazchna, 3 Vannaka, 4 Chaeldar, 5 Duradel, 6 Kuradal,
7 Morvran, 8 Laniakea, 9 Raptor, 45 Sumona, 46 Mandrith, 47 Jacquelyn.
Laniakea's enum has 55 entries (structs `SLAYER_LANIAKEA_LIST_ENTRY_n`).

Each entry struct (read with `struct.params` + `struct:GetParamValue(p)`;
`paramValues` from the docs example is nil in the Beta) holds:

| Param | Example | Meaning |
|---|---|---|
| `SLAYER_TYPE` | 66 | task id (same as `SLAYER_TARGET`) |
| `SLAYER_NAME` | dark beasts | task name (client language, lower case) |
| `SLAYER_SL_REQ` | 90 | Slayer level needed |
| `SLAYER_CL_REQ` | 10 | combat level needed (only some entries) |
| `SLAYER_EXAMPLE_NPC` | MOURNING_DARK_BEAST | example NPC |
| `SLAYER_DESCRIPTION` | text | description |

Not in the structs: task weight, kill amount, quest requirements -> keep
those from the wiki data.

All 12 lists are saved in `master-tasks.txt` (421 entries, 2026-10-20):
Turael 7, Mazchna 37, Vannaka 26, Chaeldar 35, Duradel 41, Kuradal 62,
Morvran 51, Laniakea 55, Raptor 30, Sumona 46, Mandrith 19, Jacquelyn 12.

**Resolved (2026-10-20):** the earlier "wiki lists more Turael tasks" was
based on the old wiki summary page, not the real data source. The real
wiki source is a Lua data module per master, `Module:Slayer
assignments/<Master>` (NOT the "Slayer assignment/<Master>" page itself,
which only invokes a template) with `min`, `max`, `weight`, `reqs` per
task, fetched by `tools/fetch_wiki_data.py` into
`wiki/assignment_<Master>.lua`. Matched against the game's `SLAYER_NAME`
(case-insensitive) this gives an **exact task-count match for 9 of 12
masters**. The other three are short by exactly 2 each: Kuradal 62/64,
Morvran 51/53, Laniakea 55/57 (Laniakea's 2 confirmed as "Ravenous
strigoi" and "Sanguine werewolves", OPEN_POINTS #6) -> these are toggle
tasks the player must switch on (OPEN_POINTS #10c), not missing data.

**Name matching** (game `SLAYER_NAME` -> wiki task key) needs a small
build-time alias table (12 entries, mostly singular/plural or a rename,
e.g. game "kalphites" = wiki "Kalphite", game "cres's automatons" = wiki
"Cres's creations"); with it, **all 421 game tasks match (100%)**. See
the generator for the full table.

**Monster facts** (lifepoints, Slayer XP, combat level, weakness) join by
game NPC id, not by name: `SLAYER_EXAMPLE_NPC` (struct) -> `config.NPC`
id -> wiki bucket `infobox_monster.id` (that field can hold a comma list
of ids for one infobox row, e.g. all Chicken colour variants share one
row). This joins for **395/421 tasks (93.8%)**. The rest are tasks with
no single representative monster (e.g. "Birds", "Tzhaar", "Cres's
automatons": `SLAYER_EXAMPLE_NPC` is literally `UNKNOWN`/absent in the
game) or a "dummy" category NPC without its own wiki infobox (Corrupted
creatures, Shadow creatures, Creatures of the lost grove) plus one real
gap (Vyrewatch's chosen example NPC, id 4837, is not in the wiki bucket
at all). For these, no per-kill facts exist; fall back to the wiki
"Assignment summary" text (already shipped) or show no monster facts.
Seen in the sniffer log: task 46 (205 kills) was gargoyles.

## Task ids and task lists (game config, `pan-Enum.txt`)

`SLAYER_TARGET` holds the game's task id. The mapping comes from the
game's own config, not by hand. Candidates (being checked in game):

| Enum | Types | Probably |
|---|---|---|
| `SMKI_CRITTER_NAMES` | INTEGER -> STRING | **confirmed**: task id -> task name, 181 tasks (66 = Dark beasts, 1 = Monkeys, 2 = Goblins) |
| `SLAYER_MASTER_ENUM` | INTEGER -> ENUM | master id (`SLAYER_MASTER`) -> that master's task list |
| `SLAYER_MASTER_<NAME>_ENUM` (Turael, Jacquelyn, Mazchna, Raptor, Vannaka, Chaeldar, Duradel, Sumona, Kuradal, Morvran, Mandrith, Laniakea) | INTEGER -> STRUCT | per-master task list; struct per task (weight? requirements?) |
| `..._ENUM_ALPHABETICAL` | INTEGER -> STRUCT | same, sorted by name |
| `QUICKCHAT_LIST_SLAYERMASTERS` | INTEGER -> STRING | master names |

Seen so far: 66 = Dark beasts (confirmed on screen).

## Items, tool belt, pet, rewards (measured 2026-10-22, maxed account)

- Tool belt: `TOOLBELT_ROCKHAMMER`, `_SALT_BAG`, `_ICE_COOLER`, `_FUNGICIDE`,
  `_SLAYER_BELL`, `_FISHING_EXPLOSIVE` all read 1 (all on the belt); base var
  `TOOLBELT_SLAYER_TOOLS` = 4194175.
- Item config names seen in the backpack: `DEAL_SLAYER_GLOVES` (slayer gloves),
  `MOLANISK_BELL` (slayer bell), `OMGE_SKILL_HUBS_SLAYER_SPIKED_GAUNTLET`,
  `SLAYER_ICY_WATER` (ice cooler), `SLAYER_BUGLAN_OFF`, `SLAYER_SPRAY_PUMP_10`,
  plus the other shop items under their expected names. Some items report
  configName `UNKNOWN` (one in the backpack, one worn): which is not known.
- Legendary pet: `MTX_PET_ABILITY_1/2/3` (varbits of `MTX_FAMILIAR_OVERRIDE`,
  varp 5020) = ability per slot, 0 = empty, numbers in list order (first
  three abilities gave 1, 2, 3). **Slayer Finisher = 5** (swapped out:
  5 -> 0 -> 8); 6 = Item Repair, 7 = Beast of Burden (confirmed by the user).
- Summoned pet: `FOLLOWER_OBJ` (varp 1831, OBJ) = item of the current follower,
  -1 = none (seen -1 while switching pets); `MTX_PETS_CURRENT_ACTIVE_PET` (varp
  3472) = obj id of the active legendary pet. Seen: Dragon Wolf =
  `MTX_PET_DRAGONWOLF_ADULT` (27214), Prime colossus = `TWITCH_APR17_PET_ADULT`
  (39918), Fire Drake = `MTX_PET_DRAKE_ADULT` (34783). Ability slots stayed
  5/6/7 when switching pets. Dismissed: `FOLLOWER_OBJ` -> -1 (shown as
  UNKNOWN) while `MTX_PETS_CURRENT_ACTIVE_PET` keeps the chosen pet. So "pet
  out" = the two ids are equal (used in adapter.read_pet_finisher, tested
  live 2026-10-22: summon -> true, dismiss -> false).
- Items with configName `UNKNOWN` are empty slots.
- Warriors' Guild tokens (currency pouch, not items): `WARGUILD_TOKENS_BALANCE`,
  `_STRENGTH`, `_COMBAT`, `_ATTACK`, `_DEFENCE` match the game's token screen
  (51/307/380/0/56). `WARGUILD_TOKEN_TYPE` = chosen type (4 = combat: the combat
  counter dropped 380 -> 360 in the cyclops room). `WARGUILD_CYCLOPES_ENTRY_APPROVED`
  is 1 only briefly while entering. Entry rule (wiki): 200 of one type or 30 of
  each. Used for Mazchna's cyclopes requirement (adapter.read_cyclops_entry).
- Slayer masks (Treasure Hunter; can force their task once per day or few
  days, user). The 23 config names, seen in the backpack 2026-10-22:
  - `TRH9_SLAYER_MASK_`: ABERRANT_SPECTRE, BLOODVELD, DARK_BEAST,
    DESERT_STRYKEWYRM, ICE_STRYKEWYRM, JUNGLE_STRYKEWYRM
  - `WOF35_SLAYER_MASK_`: ABYSSAL, BASILISK, COCKATRICE, HANDS, KURASK
  - `WOF50_SLAYER_MASK_`: BANSHEE, DUSTDEVIL, GARGOYLE, JADINKO, JELLY
  - `TRH64_SLAYER_MASK_`: AIRUT, AQUANITE, AUTOMATON, DAGANNOTH, DEMON,
    GANODERMIC, TROLL
  A forced task changes SLAYER_TARGET/SLAYER_COUNT without a VarTransmit. Whether "pet summoned" is in a var: not known yet.
- Slayer Rewards (values on the test account): `SMKI_AUTOSMASH_GARGOYLE` 1
  (probably quicker killing blows), `BSLAY_UNLOCKED_GLACORS` 1,
  `BSLAY_UNLOCKED_TDEMONS` 0, `SLAYER_KURADEL_MUSPAH` 1, `SLAYER_KURADEL_NIHIL` 0,
  `SMKI_KURADAL_AQUANITE` 0, `FOTG2_NIGHTMARE_TASK_UNLOCKED` 1,
  `SMKI_ICE_STRYKEWYRM_NOFIRE` 0, `SMKI_HEAD/RING/MISSILE_MAKE` 1,
  `NJSLAY_BOUGHT_UPGRADE1..4` 1, `NJSLAY_BOUGHT_FUSED` 1. Toggle meaning still
  to confirm with the user.

## How to verify a candidate

In the Beta console: `!getvar SMKI_SLAYER_POINTS` (should print 2844),
`!getvar BSLAY_TASK_STREAK` (should print 1531), `!getvar SLAYER_MASTER`.

## XP at 200m (Beta 2026-10-23)

- At 200m Slayer XP no SkillTransmit for Slayer arrives (kills still change SLAYER_COUNT).
- VarClient is readable: `var.VarClient[name].value` works (TELEMETRY_READY = true).
- c:XPDISPLAY_SLAYER = 200000000 and did not change over 3 gargoyle kills; XPDISPLAY_TOTAL,
  DOUBLEXP_DROPLETAMOUNT, XP_POPUP_*_BUBBLE_LAST_SKILL_USED = -1; TELEMETRY_VARC = 0, unchanged.
- Conclusion: the RuneMetrics XP drops past 200m are not readable through vars.
