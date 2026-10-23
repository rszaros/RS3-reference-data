# RS Wiki "Slayer training": notes for Slayer Helper

Source: https://runescape.wiki/w/Slayer_training, revision 37207430
(2026-10-14), CC BY-NC-SA 3.0. Raw wikitext: `slayer_training.wikitext`
(same folder). Parsed assignment summary: `assignment_summary.tsv`
(generator: plugin `tools/read_slayer_training.py`).
Read 2026-10-20. Skipped on purpose: equipment lists (gear is not used for
advice), abilities, prayers, familiars (advice on these is prohibited).

## Masters (table "Slayer masters")

| Master | Req | Points task / 10th / 50th |
|---|---|---|
| Turael / Spria | none | 0 / 0 / 0 (and changing a task there resets the streak) |
| Jacquelyn | none | 1 / 5 / 15 |
| Vannaka | 30 combat | 2 / 10 / 30 |
| The Raptor | 35 combat, Unwelcome Guests | scales with level, up to 21 / 105 / 315 |
| Mazchna | 50 combat | 4 / 20 / 60 |
| Chaeldar | 75 combat, Lost City | 10 / 50 / 150 |
| Sumona | 90 combat, 35 Slayer, Smoking Kills | 12 / 60 / 180 |
| Duradel / Lapalok | 100 combat, 50 Slayer, Shilo Village | 15 / 75 (80 after Elite Karamja) / 225 |
| Kuradal | 110 combat, 75 Slayer, Barbarian Firemaking (NPC Contact bypasses) | 18 / 90 / 270 |
| Morvran | 120 combat, 85 Slayer, Plague's End | 20 / 100 / 300 |
| Laniakea | 120 combat, 90 Slayer | 22 / 110 / 330 |
| Mandrith | 120 combat, 95 Slayer, tasks in the Wilderness | 22 / 110 / 330 (+ Wilderness chest, Reaper point) |

Spria and Lapalok replace Turael and Duradel after While Guthix Sleeps.
10th task = 5x, 50th = 15x the master's normal points.
Without Smoking Kills: half points.

## Strategy facts (usable as advice)

- Highest master = most points, not necessarily the best XP/hour.
- **Master switching**: do tasks 1-9 with a lower/faster master, take the
  10th (and 50th) from the highest master for the bigger bonus.
  -> Fits our "Streak bonus" line: "next task is a 10th: take it from <best
  master you can use>".
- Around 90 combat: The Raptor (else Sumona) until Kuradal; not The Raptor
  at very low levels (poor points). Kuradal at 110 combat / 75 Slayer
  (ferocious ring drops in his dungeon).
- 1 block/prefer slot per 50 quest points, max 8.
- **Spending order for XP**: 1. blocks, 2. Slayer helmet unlock and
  upgrades, 3. prefer / extend, 4. extra unlocks (ring of slaying),
  5. enabling specific monsters.
- Cancel = 30 points; use it as often as the points stay stable. Low on
  points: do tasks you would normally cancel.
- An unwanted toggleable task that is on: toggle it off (a free block).
- Extend only tasks you normally do.
- Temporary boosts do not unlock higher assignments.

## Notable rewards (table)

| Reward | Cost | Why |
|---|---|---|
| Ring of slaying crafting | 300 | teleports, less downtime |
| Quicker killing blows (finisher unlock) | 400 | gargoyles etc. no manual finish |
| Slayer helmet crafting | 400 | "most important piece of equipment" |
| Fuse rings to full slayer helmet | 500 | ferocious ring + helmet |
| Full slayer helmet upgrades | 2,100 | 4 upgrades |
| Move souls in personal slayer dungeon | 1,000 | Sunken Pyramid |
| Ushabti | 20 | Codex / Sunken Pyramid |

Slayer helmet: +7.5-9.5% damage, +12.5-14.5% accuracy on task; includes
all slayer headgear effects. On the Anachronia stand it still gives the
boost (ring effects do not work there).

## Access to assignments (quest requirements)

Mithril dragons: Barbarian Firemaking. Chaos giants: Birthright of the
Dwarves. Jungle/Cave horrors: Cabin Fever (cave horrors 58 Slayer).
Nightmare creatures: Children of Mah (80). Killerwatts: Ernest the Chicken
(37). Nihil, Muspah: Fate of the Gods (Muspah 76). Dagannoth: Horror from
the Deep. Suqahs: partial Lunar Diplomacy. Mogres: Mogre lore activity
(32). Celestial dragons: One of a Kind. Warped tortoises/terrorbirds: The
Path of Glouphrie (56). Glacors: Ritual of the Mahjarrat. Fever spiders:
partial Rum Deal (42). Tormented demons: While Guthix Sleeps. Cres's
creations: full The World Wakes (67). Stalker creatures: Dishonour among
Thieves (71). Crystal shapeshifters: The Light Within (75). Gemstone
dragons: Shilo Village + hard Karamja achievements (95). Corrupted
creatures: partial Icthlarin's Little Helper (88). Soul devourers: partial
Icthlarin's Little Helper (105). Rune dragons: Fate of the Gods + Ritual of
the Mahjarrat. Vyrewatch: The Branches of Darkmeyer. Terror dogs: Haunted
Mine (40). Skeletal wyverns: Elemental Workshop I (72).

## Quest unlocks with a Slayer benefit

Smoking Kills (full points, slayer helmet), Ritual of the Mahjarrat (bane
ammo, Glacor Cave), Lair of Tarn Razorlor (salve amulet (e)), Necromancy!,
Animal Magnetism (Ava's devices), Do No Evil partial (Ava's alerter), Dwarf
Cannon, Desert Treasure (Ancient Magicks), King's Ransom + Knight Waves
(Piety etc.), Fairy Tale I (fairy rings), Legacy of Seergaze, The Jack of
Spades (Slayer Codex and Sunken Pyramid at 99 Slayer), Hunt for Surok,
Fur 'n Seek, Back to my Roots, In Pyre Need.

## Items that change assignments

Headhunter's sacrifice / thrill, Trophy-taker's perk, Slayer Introspection
relic (choose min or max amount), Slayer trophy (Raptor: short/long tasks),
Slayer VIP ticket (choose between 2 tasks).

## Slayer Codex

99 Slayer, The Jack of Spades. **+1% Slayer XP per 20 souls collected, max
+5% at 100 souls** (with a slayer helmet). The plugin can count collected
souls (number of bits set in `SLAYER_CODEX_1..7`) even without knowing the
bit order -> advice "N more souls for the next +1%" is possible.
Sunken Pyramid suggestions: Muspah 5, Ripper demon 1, Crystal
shapeshifters 5, Shadow creatures 5, Hydrix dragon 1.

## Assignment summary (per task, endgame)

41 tasks, high level only. "Purely based on maximal xp/hr", with
recommended equipment; real rates vary. Columns: Task, Slayer XP/hr, Use,
Slayer lvl, Notes, Pros, Cons, Priority (Prefer / Do / Skip / Block / Skip).
- Prefer: Gemstone dragons, Ripper demons, Soul devourers, Shadow
  creatures, Nightmare creatures, Lost Grove, Acheron mammoths, Corrupted
  creatures, Crystal shapeshifters, Greater demons.
- Do: Airut, Nodon dragonkin, Abyssal demons, Camel warriors, Stalker
  creatures, Edimmu, Ganodermic creatures, Chaos giants, Dark beasts, Cres's
  creations, Ice strykewyrms, Dinosaurs, Dragons, Vile blooms.
- Skip: Vyrewatch, Celestial dragons, Muspah, Rune dragons, Black dragons,
  Gargoyles, Waterfiends, Kalphite, Ascension members, Adamant dragons,
  Dagannoth, Aviansies.
- Block / Skip: Grotworms, Glacors, Tormented demons, Nihil, Aquanites.
Use as "Wiki suggests" next to PvME (endgame view), not as the ranking.
Notes/Pros/Cons are prose: do not show verbatim at length.
