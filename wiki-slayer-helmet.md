# Slayer helmet and its parts (RS3 Wiki research)

Fetched 2026-10-22 via the MediaWiki API (action=parse, prop=wikitext). Quotes are copied
verbatim from the wiki. Wiki content is CC BY-NC-SA 3.0. Object config names/ids come from
`pan-Obj.txt` in this folder. Anything marked "not verified" was not confirmed.

## Overview: what is made from what

```
Spiny helmet + Face mask + Earmuffs + Nose peg + Black mask (uncharged)
  -> Slayer helmet            (55 Crafting, Smoking Kills, 400 Slayer points unlock)
Slayer helmet + Hexcrest + Focus sight
  -> Full slayer helmet       (tier 25, 20 Defence)
  -> Reinforced slayer helmet (tier 45, 30 Def, 100 pts, re-upgrade 10)   = "tier 1 upgraded"
  -> Strong slayer helmet     (tier 65, 50 Def, 400 pts, re-upgrade 40)   = "tier 2 upgraded"
  -> Mighty slayer helmet     (tier 85, 70 Def, 600 pts, re-upgrade 60)   = "tier 3 upgraded"
  -> Corrupted slayer helmet  (tier 85, 70 Def, 1000 pts + Corrupted gem, re-upgrade 100) = "tier 4 upgraded"
Optional: Ensouled spectral lens on any full slayer helmet variant (Necromancy boost, permanent)
Optional: fuse rings (500 pts, 50 after first purchase; 60 Crafting, Smoking Kills)
```

Masked earmuffs (face mask + earmuffs) can NOT be used to make the helmet; they must be
taken apart first.

## Slayer helmet

Source: https://runescape.wiki/w/Slayer_helmet

- Obtain: "It may be assembled after a player spends 400 Slayer points to learn how to craft
  one. In addition, it requires level 55 Crafting and level 35 Slayer, which is also needed to
  complete the pre-requisite quest Smoking Kills." Black mask "must be uncharged".
- Requirement to wear: 10 Defence. Members. Untradeable. Wiki id 13263.
- Passive ("Slayer Spirit", from the black mask): "Melee attacks against the monsters of active
  Slayer assignments have 12.5% increased accuracy and deal 7.5% increased damage."
  - "The boost does not work on Shattered Worlds' monsters."
  - "The damage boost does not apply to bleeds and burns."
- Combined protections (kept in all higher tiers, same text on Full and Corrupted pages):
  - "Like a spiny helmet, it protects players from wall beasts when traversing the Lumbridge Swamp Caves."
  - "Like earmuffs, it deafens the screams of banshees."
  - "Like a face mask, it protects players from the dust in the Smoke Dungeon and from stat-draining attacks by dust devils."
  - "Like a nose peg, it blocks stat-draining attacks by aberrant spectres."
- Helmet stand: see "Slayer helmet stand" below.
- Points needed per master to reach 400 (one master only, incl. 4 no-point tasks):
  Vannaka 254 / 132 after Smoking Kills; Mazchna/Achtryn 132 / 70; Chaeldar 50 / 32;
  Sumona 50 / 30; Duradel/Lapalok 44 / 23; Kuradal 37 / 20; Morvran 32 / 20; Laniakea 30 / 19.
- Ironman black mask: sea horrors in the Shadow Reef, or cave horrors / unspeakable horrors on
  Mos Le'Harmless (58 Slayer, Cabin Fever).
- Config names: `SMKI_INV_FULL_SLAYER_HELMET` (13263). Also `SLAYER_HELMET_UNCHARGED` (14636),
  `SLAYER_HELMET_CHARGED` (14637): which helmet these are is not verified.

Update history (Slayer helmet):
- 25 Nov 2024: Given a 100 life points bonus.
- 23 Oct 2023: Corrected a typo when combining the items required to create a Slayer Helmet.
- 18 Sep 2023: Reworked damage buffs: "Slayer helm (Rebalanced from 12.5% random damage to 7.5% total at the lowest tier, 9.5% at the highest tier)."
- 13 Jan 2020: Equipping Slayer helmet from the bank now has wear in the options.
- 4 Nov 2019: Original slayer helmet now correctly give any accuracy bonus to melee.
- 14 Oct 2019: Fixed an issue causing the Slayer helmet stand to not work as a helmet slot.
- 28 Aug 2018: Non usable 'enchanted slayer helmet' can be converted to regular slayer helmet.
- 26 Jun 2017: Slayer helmets now correctly equip from the Bank menu.
- 5 Jan 2015: Rellekka Slayer Caves teleport renamed "Fremennik Slayer Dungeon".
- 13 Oct 2014: No longer possible to teleport to Morvran without unlocking it first.
- 6 Oct 2014: A fused slayer helmet tells how many charges remain after teleporting.
- 23 Jun 2014: Asked how many items to recharge; fused slayer helmets benefit from the ferocious ring damage boost.
- 10 Mar 2014: Upgrading costs significantly less if upgraded before.
- 17 Feb 2014: Reinforced, strong and mighty helmets return summoning scrolls correctly after being infused.
- 4 Feb 2014: Tiered slayer helmets show the correct colour on chatheads.
- 13 Jan 2014: Summoning scrolls in re-coloured/enchanted helms trigger familiar special moves.
- 2 Oct 2013: Fixed helmets converting bacon scrolls to bones.
- 28 Nov 2012: All slayer helm variants brought up to their appropriate stats, regardless of colour.
- 11 Apr 2012: Pikkupstix no longer tries to wipe paint off unpainted helmets.
- 6 Mar 2012: Graphically updated.
- 5 Jun 2008 (Smoking Kills): Added to game.

## Spiny helmet

Source: https://runescape.wiki/w/Spiny_helmet

- "a helmet designed to protect the player from the attacks of a wall beast, located in the
  Lumbridge Swamp Caves. It requires level 5 Defence to equip ... It can be bought from any
  Slayer Master for 650 coins."
- Task: Wall beasts (Lumbridge Swamp Caves). Function kept in the slayer helmet and all tiers.
- Config: `WALLBEAST_SPIKE_HELMET` (4551), noted `CERT_WALLBEAST_SPIKE_HELMET` (4552).
- History: 16 Mar 2026 life points 50 -> 100 (crafted armour no longer offset);
  25 Nov 2024 given 50 life points; 14 Mar 2005 added (Lumbridge Swamp Caves).

## Face mask

Source: https://runescape.wiki/w/Face_mask

- "requiring level 10 Slayer to wear. The face mask can be bought from any Slayer Master for 200 coins."
- "It is worn when entering the Smoke Dungeon ... inhaling the dust and smoke will cause heavy
  damage to players at a rate of 200 life points every 12 seconds. It must also be worn when
  fighting dust devils otherwise they will dramatically decrease players' stats."
- Substitutes: masked earmuffs (after Smoking Kills), or a gas mask (no Slayer level, protects
  against the smoke only, not against dust devils).
- Also recommended on Freneskae during Fate of the Gods (50 damage every 15 seconds without it).
- Tasks: Dust devils; Smoke Dungeon (Smoking Kills area). Kept in slayer helmet and all tiers.
- Config: `SLAYER_FACEMASK` (4164), `CERT_SLAYER_FACEMASK` (4165).
- History: 16 May 2011 Soul Wars cape head stretch fix; 10 Feb 2009 graphical fix with
  Barrelchest anchor; 26 Jan 2005 added (Slayer Skill).

## Earmuffs

Source: https://runescape.wiki/w/Earmuffs

- "used to protect against banshees' screams. They require 15 Slayer to wear, and may be
  purchased from any Slayer Master."
- Task: Banshees (incl. mighty banshees). Kept in slayer helmet and all tiers.
- Config: `SLAYER_EARMUFFS` (4166), `CERT_SLAYER_EARMUFFS` (4167). (`XMAS24_EARMUFFS_*` are
  cosmetic Christmas items, not Slayer gear.)
- History: 8 Apr 2009 female hairstyles fix; 26 Jan 2005 added (Slayer Skill).

## Nose peg

Source: https://runescape.wiki/w/Nose_peg

- "requiring level 60 Slayer to wear. When worn, the peg protects the player from the special
  attack of the aberrant spectre which, if not equipped, will cause a rapid and significant
  reduction in the player's stats and life points. The nose peg can be bought from any Slayer Master."
- Task: Aberrant spectres. Kept in slayer helmet and all tiers.
- Config: `SLAYER_NOSEPEG` (4168), `CERT_SLAYER_NOSEPEG` (4169).
- History: 26 Jan 2005 added (Slayer Skill).

## Masked earmuffs

Source: https://runescape.wiki/w/Masked_earmuffs

- Face mask + earmuffs, 25 Crafting, partial completion of Smoking Kills. "help protect players
  against both banshees and the smoke effects of the Smoke Dungeon ... can also offer protection
  from dust devils". No requirement to wear.
- Cannot be used to make the slayer helmet (must be disassembled first).
- Config: `SMKI_EARMUFF_MASK` (13277).
- History: 4 Mar 2013 renders correctly on male characters; 5 Jun 2008 added (Smoking Kills).

## Black mask

Source: https://runescape.wiki/w/Black_mask

- "requires 10 Defence, 20 Strength, and 40 Combat to wear ... when worn it gives the player a
  7.5% Melee damage increase and 12.5% Melee accuracy bonus against their current Slayer assignment.
  Black masks are dropped by cave horrors and unspeakable horrors (level 58 Slayer required),
  found in the Mos Le'Harmless Caves." Also on the Grand Exchange with 0 or 10 charges.
- Charges (10): reduce opponent's Defence by 3-10 at random; "currently black mask charges may
  be bugged and will not be used". Must be uncharged ("remove-charges") to make the helmet.
- Function in helmet: the Slayer Spirit melee boost; higher tiers extend it to ranged/magic.
- Config: `HARMLESS_BLACK_MASK` (8921, uncharged), `HARMLESS_BLACK_MASK_1` .. `_10`
  (8919 .. 8901, odd ids), each with a `CERT_` noted id one higher.
- History: 16 Mar 2026 life points 200 -> 100; 25 Nov 2024 given 200 life points;
  31 Oct 2022 accepted as 'evil' item in Shadow of the Storm; 25 Feb 2009 clipping reduced;
  4 Jul 2006 added (Trouble Brewing).

## Hexcrest

Source: https://runescape.wiki/w/Hexcrest

- "dropped by jungle strykewyrms. It requires 20 Magic and 20 Defence to equip. When worn while
  slaying, it boosts the player's Magic damage by 7.5% and Magic accuracy by 12.5%."
  Jungle strykewyrms need 73 Slayer (Slayer helmet page).
- Function in full helmet: magic part of Slayer Spirit.
- Config: `SLAYER_MAGE_MASK` (15488), `CERT_SLAYER_MAGE_MASK` (15489).
- History: 25 Nov 2024 given 200 life points; 4 Apr 2016 skill guide defence requirement
  corrected; 13 Mar 2012 no more bald patch; 8 Feb 2010 added (Strykewyrms).

## Focus sight

Source: https://runescape.wiki/w/Focus_sight

- "a headband dropped by desert strykewyrms. It requires 20 Ranged and 20 Defence to equip.
  When worn, the player's Ranged damage is increased by 7.5% and their Ranged accuracy by 12.5%
  against their current Slayer task." Desert strykewyrms need 77 Slayer (Slayer helmet page).
- Function in full helmet: ranged part of Slayer Spirit.
- Config: `SLAYER_RANGE_MASK` (15490), `CERT_SLAYER_RANGE_MASK` (15491).
- History: 25 Nov 2024 given 200 life points; 4 Apr 2016 skill guide defence requirement
  corrected; 5 Oct 2015 stretching fix; 13 Mar 2012 no more bald patch; 8 Feb 2010 added.

## Spectral lens / Ensouled spectral lens

Sources: https://runescape.wiki/w/Spectral_lens, https://runescape.wiki/w/Ensouled_spectral_lens

- Spectral lens: "dropped by Profane Scabarites. It requires level 20 Necromancy, 20 Defence,
  and completion of Necromancy! quest to equip. When worn, it boosts the player's necromancy
  damage by 7.5% and necromancy accuracy by 12.5% against their current Slayer assignment."
- Ensouled spectral lens: made with the "ensoul spectral lens" ritual (Ritual site tier 2).
  "can be attached to the full slayer helmet ... This is a permanent upgrade that applies to all
  variants of full slayer helmet the player owns, including any crafted afterwards."
  Necromancy level for the ritual: not verified.
- Config: `SLAYER_NECROMANCY_MASK` (57871), `CERT_SLAYER_NECROMANCY_MASK` (57872),
  `SLAYER_NECROMANCY_MASK_ENSOULED` (57873). How the game stores "lens attached" (helmet config
  name does not change; probably a var): not verified.
- History: 25 Nov 2024 given 200 life points; 4 Nov 2024 added (New Slayer Mobs & Premier Refresh).

## Full slayer helmet

Source: https://runescape.wiki/w/Full_slayer_helmet

- "a tier 25 slayer helmet requiring level 20 Defence to equip. It is made by combining a focus
  sight, hexcrest, and slayer helmet". 55 Crafting, Smoking Kills, the 400-point unlock.
- Passive: "Melee, ranged, and magic attacks against the monsters of active Slayer assignments
  have 12.5% increased accuracy and deal 7.5% increased damage." Stacks with the salve amulet.
- "Every 20 souls added to the Slayer Codex add a 1% boost to Slayer experience gained while
  wearing the helmet, up to 5% for adding 100 souls."
- Also has the functions of an enchanted gem (kills left, contact master), Co-op Slayer.
- Config: `SLAYER_HELMET_ALLCOMBATS` (15492), `_UNCHARGED` (15496), `_CHARGED` (15497), colours
  `_RED/_BLUE/_GREEN/_YELLOW` (22528-22551), fused `_FUSED*` (30641-30655), and `BOUGHT_` copies.
  The base name `SLAYER_HELMET_ALLCOMBATS` = full slayer helmet is inferred from "all-class"; not
  verified against the wiki id.
- History: 18 Sep 2023 damage rework (see above); 9 Aug 2021 "Wear" and "Activate" fixed;
  13 Jan 2020 wear from bank; 9 Apr 2018 Morvran teleports mentioned when checking charges;
  26 Jun 2017 equip from bank; 5 Jan 2015 Fremennik Slayer Dungeon rename; 13 Oct 2014 Morvran
  teleport needs unlock; 4 Feb 2014 chathead colours; 21 Jan 2014 disconnection fix;
  13 May 2013 coloured helms same stats; 13 Mar 2012 recoloured/charged helms drop hexcrest and
  focus sight in PvP; 6 Mar 2012 graphical update; 6 Oct 2010 banner stretching fix;
  8 Feb 2010 added (Strykewyrms).

### Boss slayer table (Full and Corrupted helmet pages)

Bosses that count for a Slayer assignment; the helmet boost applies to them on task.

| Boss | Slayer assignment | Slayer req | Slayer XP |
|---|---|---|---|
| Arch-Glacor (no helmet effect in Hard Mode) | Glacors | 1 | 4810 |
| Astellarn | Celestial dragons, Dragons | 1 | 27400 |
| The Barrows Brothers, Rise of the Six | Ghosts, Undead | 1 | Varies |
| Black stone dragon | Gemstone dragons, Dragons | 1 | 37600 |
| Dagannoth Prime / Supreme / Rex | Dagannoth | 1 | 1068 |
| Exiled Kalphite Queen | Kalphite | 1 | 2055 |
| K'ril Tsutsaroth | Greater demons, Demons | 1 | 2151.5/3912.4 |
| Kalphite King | Kalphite | 1 | 3963 |
| Kalphite Queen | Kalphite | 1 | 1309.4 |
| Kerapac, the bound | Nodon dragonkin | 1 | 16700 |
| King Black Dragon | Black dragons, Dragons | 1 | 1050.6 |
| Kree'arra | Aviansies | 1 | 2934/3912 |
| Legiones | Ascension members | 95 | 1829.2 |
| The Magister (no helmet effect) | Soul devourers | 115 | 8000 |
| Orikalka / Rathis / Pthentraken / Osseous (Undead only Osseous) | Dinosaurs, Undead | 1 | 4545 |
| Queen Black Dragon | Black dragons, Dragons | 1 | 1693.5 |
| Taraket the Necromancer | Undead | 1 | Unknown |
| Verak Lith | Black dragons, Dragons | 1 | 27438 |
| Vorkath | Blue dragons, Dragons, Undead | 1 | 31340.5 |

## Reinforced / Strong / Mighty slayer helmet

Sources: https://runescape.wiki/w/Reinforced_slayer_helmet,
https://runescape.wiki/w/Strong_slayer_helmet, https://runescape.wiki/w/Mighty_slayer_helmet

| Helmet | Tier | Defence | Slayer points (re-upgrade) | Accuracy | Damage | Config names |
|---|---|---|---|---|---|---|
| Reinforced | 45 | 30 | 100 (10) | 13% | 8% | `SLAYER_HELMET_ALLCOMBATS*_TIER1` (30656-30685) |
| Strong | 65 | 50 | 400 (40) | 13.5% | 8.5% | `..._TIER2` (30686-30715) |
| Mighty | 85 | 70 | 600 (60) | 14% | 9% | `..._TIER3` (30716-30745) |

- "Players must be wearing the full slayer helmet in order to upgrade it" (same for each step).
- All three keep every protection and function of the full slayer helmet; the Ensouled spectral
  lens works on all of them.
- History (identical on all three): 18 Sep 2023 damage rework; 13 Jan 2020 wear from bank;
  9 Apr 2018 Morvran teleports on check; 26 Jun 2017 equip from bank; 5 Jan 2015 Fremennik
  Slayer Dungeon rename; 13 Oct 2014 Morvran teleport needs unlock; 4 Feb 2014 chathead colours;
  21 Jan 2014 disconnection fix; 21 Jan 2014 added (Slayer Helmet and Social Slayer Update).
  Mighty also: 13 Jan 2014 summoning scrolls trigger familiar special moves.

## Corrupted slayer helmet

Source: https://runescape.wiki/w/Corrupted_slayer_helmet

- "a tier 85 slayer helmet requiring level 70 Defence to equip. It is made by upgrading a mighty
  slayer helmet for 1,000 Slayer points and a corrupted gem at any Slayer Master, although
  subsequent upgrades will only cost 100 Slayer points. The mighty slayer helmet must be worn and
  the corrupted gem must be in the backpack".
- Trivia: "players who do not have level 80 Defence cannot buy it from the Slayer reward shop.
  It is unclear if this was intended or a bug."
- Passive: "Melee, ranged, and magic attacks against your active Slayer assignments have 14.5%
  increased accuracy and deal 9.5% increased damage."
- Extra over mighty:
  - "It increases the chance of capturing a soul in an ushabti by 5% when killing an assigned
    monster or with 120 Slayer."
  - "It can be used to view the Slayer codex while worn." (Equipped option "Slayer codex".)
- Keeps all protections (spiny, earmuffs, face mask, nose peg), the Codex XP boost (1% per 20
  souls, max 5%), enchanted gem functions, fuse rings. Cannot be stored in the keepsake box.
- Corrupted gem: "may be dropped when killing creatures in the Sophanem Slayer Dungeon whilst on
  an applicable slayer task." Config `MENAPHOS_SLAYER_CORRUPTED_GEM` (40334), noted 40335.
- Config names (50 total): `SLAYER_HELMET_ALLCOMBATS[_UNCHARGED|_CHARGED][_RED|_BLUE|_GREEN|_YELLOW][_FUSED...]_TIER4`
  (40377-40406, 30 names) and `BOUGHT_SLAYER_HELMET_ALLCOMBATS..._TIER4` (57850-57869, 20 names).
  All end in `_TIER4` and contain `SLAYER_HELMET_ALLCOMBATS`.
- History: 18 Sep 2023 damage rework; 13 Jan 2020 wear from bank; 4 Jun 2018 "The corrupt slayer
  helmet will now provide a 5% bonus chance to catching souls and has the option to view the
  slayer codex."; 26 Jun 2017 equip from bank; 12 Jun 2017 ring of slaying / ferocious ring can
  be added; 4 Feb 2014 chathead colours; 21 Jan 2014 disconnection fix; 5 Jun 2017 added
  (Menaphos - The Gates are Open).

## Ushabti formula (helmet part)

Source: https://runescape.wiki/w/Ushabti

- "If the player has a corrupted slayer helmet equipped or has it placed in the tier 3 slayer
  lodge on Anachronia, multiply target by 1.05."
- "For clarity, the corrupted helm is active if the player is 120 Slayer but not on-task."
- Separate factor: "If the player has built a tier 2+ guardhouse in Fort Forinthry, multiply
  target by 1.05."

## Slayer helmet stand

Source: https://runescape.wiki/w/Slayer_helmet_stand

- Tier 3 Slayer Lodge, Anachronia base camp. 90 Slayer to build, 20 Defence to place a helmet.
- Gives without wearing: the damage/accuracy bonus of the helmet on it (incl. Necromancy if the
  ensouled lens was used), the spiny helmet / earmuffs / nose peg / face mask effects, the ushabti
  increase with a corrupted helmet, and the 1%-5% Codex XP boost.
- Not given: "the armour, PvP damage reduction, ferocious ring effects or teleports, ring of
  slaying teleports or access to the Slayer Codex". "The effects may not be available in some
  quest areas, like Freneskae during the quest Fate of the Gods."
- History: 8 Jul 2019 added (Land Out of Time).

## Not verified

- Which helmet `SLAYER_HELMET_UNCHARGED`/`_CHARGED` (14636/14637) are.
- That `SLAYER_HELMET_ALLCOMBATS` without TIER is the full slayer helmet (name-based inference).
- How the game stores "ensouled lens attached" and the Necromancy level of the ritual.
- Whether stand state 2 (`DINO_BASE_CAMP_SLAYER_STAND_STATE`) tells which helmet tier is on it.
