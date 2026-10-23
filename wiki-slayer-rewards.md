# Slayer Rewards shop (RS3 wiki reference)

Collected 2026-10-22 via the MediaWiki API (wikitext, copied verbatim where quoted).
Wiki text is CC BY-NC-SA 3.0.

Sources:
- https://runescape.wiki/w/Slayer_Rewards
- https://runescape.wiki/w/Template:Slayer_Rewards_stock (the Buy / Learn / Assignment tables)
- https://runescape.wiki/w/Template:Slayer_Rewards_stock/Co-op

Related files (not repeated here):
- `wiki-slayer-helmet.md`: helmet parts, tiers, corrupted helmet bonuses, ensouled spectral lens.
- `wiki-slayer-equipment.md`: finisher items (rock hammer, bag of salt, ice cooler, fungicide and
  the shakers) and section 2 "Finishing blows", which already quotes the quicker killing blows unlock.

Var candidates come from `pan-VarPlayer.txt` (name, id, base var, mask). They are **candidates
only**: none of them has been checked in game.

## 1. The shop

Source: https://runescape.wiki/w/Slayer_Rewards

> '''Slayer Rewards''' is a shop run by [[Slayer Masters]] where [[Slayer points]] can be spent in
> exchange for learning how to craft Slayer equipment, gaining various Slayer-related abilities,
> modifying Slayer assignments and more.

> Having unlocked all abilities to craft Slayer items and the ability to deliver killing blows
> quicker is a requirement needed to get a [[Completionist cape (t)|trimmed completionist cape]].

> Once the helm upgrades have been purchased, any subsequent purchases of the upgrades are reduced
> to 10% of the original cost.

- Run by: Jacquelyn, Vannaka, Mazchna/Achtryn, Chaeldar, The Raptor, Sumona, Duradel/Lapalok,
  Kuradal, Morvran, Laniakea, Mandrith (all versions list the same stock). Turael/Spria are not in
  the list.
- Released 5 June 2008 (Smoking Kills). Members: yes.
- Interface tabs (gallery): Buy, Learn, Assignment, Co-op.

## 2. Assignment tab (cancel, block, extend, prefer)

Source: https://runescape.wiki/w/Template:Slayer_Rewards_stock (section "Assignment")

> Block/prefer lists are shared among all Slayer masters, even when one does not assign the task
> block/preferred from another master.

| Reward | Cost (points) | Wiki notes (verbatim) |
|---|---|---|
| Cancel task | 30 | Skips the player's current assignment without penalties. The next assignment will gain the player normal task progression and Slayer points. However, if a current task is cancelled by accepting a new task from [[Turael]] or [[Spria]], task streak will reset and the player will need to complete four assignments before they can start earning points again. This is only worth buying if tasks are from [[Chaeldar]], [[Sumona]], [[Duradel]], [[Kuradal]], [[Morvran]] or [[Laniakea]], unless you are near a 10th or 50th task. It would take a minimum of two tasks from Laniakea, Duradel or Kuradal and three from Chaeldar or Sumona to regain the points used in buying this service. |
| Block task | 100 | Skips the player's current assignment without penalties and permanently removes the assignment from the player's task list - the player will not be assigned that monster again, unless getting a task from [[Mandrith]], who ignores the player's prefer/block list. There is a current maximum limit of 8 types of assignments that can be cancelled - one for every 50 [[quest points]], up to a maximum of 400 quest points. Cancelling the removal of monsters allows the monster to be assigned again, but does not refund points spent removing the monster. Blocking a cluster task from Laniakea does not prevent the individual subset task from being rolled, for example blocking [[Creatures of Daemonheim]] can still roll [[Kal'gerion demon]] or [[Stalker creature]] tasks. |
| Extend task | 30 | Extends the player's number of monsters to kill on that task by 20% (e.g., 180 Nihil would be 216 instead). While this can be used at any point during the task, the 20% is still based on the initial number of monsters. It does not provide extra slayer points, compared to [[Soul Reaper\|boss slayer]]. You cannot extend a task that is the same as your previous task, if the previous task was extended. |
| Prefer task | 100 | Extends the player's current assignment automatically and approximately doubles the chance for the assignment to appear as a task in the future. There is a current maximum limit of 8 types of assignments that can be preferred - one for every 50 [[quest points]], up to a maximum of 400 quest points. Cancelling a preferred task does not refund points spent preferring the monster. |

Prefer mechanism, quoted by the wiki from Mod Rowley (Twitter, 26 September 2014):

> Preferred Slayer tasks = a silent, second random roll. If either task is on your prefer list,
> that's what you get (bias towards first roll)... Once normal and prefer roll is decided, [if] you
> have a VIP ticket, you get the choice between that roll and a third roll.

Var candidates:
- Block slots: `SMKI_IGNORE_FLAG_1..8`, prefer slots: `SMKI_PREFER_FLAG_1..8` (already confirmed and
  used in game/adapter.lua).
- Extend: `ELFCITY_SLAYER_TASK_EXTENDED` (-25048, varp 4772, 0x100). Candidate only; "ELFCITY" is
  Prifddinas, so this may be something else (not verified).

## 3. Learn tab

Source: https://runescape.wiki/w/Template:Slayer_Rewards_stock (section "Learn")

> After buying the option to be assigned this monster, players can always go back to any slayer
> master to toggle this task off through the rewards interface, free of charge. Turning the task
> back on will require re-payment.

### 3a. Task toggles (unlock a task)

| Reward | Cost | Description (verbatim) | Notes (verbatim) | Var candidate |
|---|---|---|---|---|
| Persuade Kuradal and Morvran to assign aquanites | 50 | Ask [[Kuradal]], [[Morvran]] or [[Laniakea]] to add Aquanites to their assignment list (with 78 Slayer). | The player must have the required Slayer level, boosts will not work. [[Sumona]] and [[Duradel]] (or [[Lapalok]]) can still assign aquanites even with this toggled off. | `SMKI_KURADAL_AQUANITE` (-9084, varp 2094, 0x80000000) |
| Persuade Slayer masters to assign muspah | 50 | Ask [[Kuradal]], [[Morvran]] or [[Laniakea]] to add Muspah to their assignment list (with 76 Slayer. Requires [[Fate of the Gods]]). | The player must have the required Slayer level, boosts will not work. | `SLAYER_KURADEL_MUSPAH` (-22466, varp 4469, 0x1) |
| Persuade Slayer masters to assign nihil | 50 | Ask [[Kuradal]], [[Morvran]] or [[Laniakea]] to add Nihil to their assignment list (with 76 Slayer. Requires [[Fate of the Gods]]). | The player must have the required Slayer level, boosts will not work. | `SLAYER_KURADEL_NIHIL` (-22467, varp 4469, 0x2) |
| Persuade Slayer masters to assign glacors | 50 | Ask [[Kuradal]], [[Morvran]] or [[Laniakea]] to add Glacor to their assignment list (requires [[Ritual of the Mahjarrat]]). | (none) | `BSLAY_UNLOCKED_GLACORS` (-23278, varp 4061, 0x80000) |
| Persuade Slayer masters to assign tormented demons | 50 | Ask [[Kuradal]], [[Morvran]] or [[Laniakea]] to add Tormented Demons to their assignment list (requires [[While Guthix Sleeps]]). | (none) | `BSLAY_UNLOCKED_TDEMONS` (-23279, varp 4061, 0x100000) |
| Persuade Slayer masters to assign nightmare creatures | 50 | Ask [[Kuradal]], [[Morvran]] or [[Laniakea]] to add Nightmare creatures to their assignment list (requires [[Children of Mah]]). | (none) | `FOTG2_NIGHTMARE_TASK_UNLOCKED` (-34408, varp 6640, 0x80000000); weak candidate, the other FOTG2_ vars in that varp are quest state |

### 3b. Task requirement replaced

| Reward | Cost | Description (verbatim) | Notes (verbatim) | Var candidate |
|---|---|---|---|---|
| Learn new technique to attack ice strykewyrms | 2,000 | Learn an ancient technique to attack [[ice strykewyrm]]s without a fiery item (with 93 Slayer). | This ability can replace a [[fire cape]] as a requirement to be assigned [[Ice strykewyrms (Slayer assignment)\|ice strykewyrms]] assignment. The player must have the required Slayer level, boosts will not work. | `SMKI_ICE_STRYKEWYRM_NOFIRE` (-9085, varp 2091, 0x80000000), strong candidate by name |

### 3c. Finishers

| Reward | Cost | Description (verbatim) | Var candidate |
|---|---|---|---|
| Learn how to deliver killing blows quicker | 400 | Learn how to deliver killing blows quicker (with 75 Slayer). | `SMKI_AUTOSMASH_GARGOYLE` (-9086, varp 2093, 0x80000000), candidate by name |

Notes (verbatim):

> Monsters which require a finishing blow to kill, such as [[rock slug]]s, [[desert lizard]]s,
> [[zygomite]]s, and [[gargoyle]]s will die when they reach zero life points like normal monsters,
> as long as the item required to kill them is in the backpack or tool belt. This ability functions
> with ranged and magic attacks; the player does not need to be positioned adjacent to the monster
> to activate the finishing blow effect.
>
> This ability does not work when using experimental fungicide during [[Chaeldar]]'s challenge.
>
> The item may still be used to kill a monster slightly above zero life points as before.
>
> It is stated in-game that 75 [[Slayer]] is required for this ability, but neither purchasing it
> nor using it actually requires the stated level.

Related items: rock hammer, bag of salt / salt shaker, ice cooler / ice shaker, fungicide spray /
fungicide shaker (see `wiki-slayer-equipment.md`). Patch 11 January 2016: "Familiars no longer block
the 'deliver finishing blows quicker' slayer ability."

### 3d. Crafting

| Reward | Cost | Description (verbatim) | Notes (verbatim) | Var candidate |
|---|---|---|---|---|
| Learn how to fletch broad arrows/bolts | 300 | Learn how to fletch [[broad arrows]] (with 52 [[Fletching]]) and [[broad-tipped bolts\|bolts]] (with 55 Fletching). | (none) | `SMKI_MISSILE_MAKE` (-9066, varp 2091, 0x40000) |
| Learn how to craft rings of slaying | 300 | Learn how to craft [[Ring of slaying\|rings of slaying]] (with 75 [[Crafting]]). | The [[Assist System]] can be used. | `SMKI_RING_MAKE` (-9067, varp 2091, 0x80000) |
| Learn how to craft Slayer helmets | 400 | Learn how to combine the [[nose peg\|nosepeg]], [[earmuffs]], [[spiny helmet\|spiny helm]], [[face mask\|facemask]] and uncharged [[black mask]] (with 55 [[Crafting]]) | [[Smoking Kills]] is required to craft [[slayer helmet]]s. | `SMKI_HEAD_MAKE` (-9068, varp 2091, 0x100000) |
| Learn how to fuse rings to full Slayer helmets | 500 | Learn how to fuse [[Ring of slaying\|Rings of Slaying]] and [[Ferocious ring\|Ferocious Ring]]s to your Full Slayer Helmet (with 60 Crafting). | See below. | `NJSLAY_BOUGHT_FUSED` (-21388, varp 4061, 0x1) |

Fuse notes (verbatim):

> [[Smoking Kills]] is required to craft [[Full slayer helmet (f)|fused full slayer helmet]]s and
> their variants.
>
> Players who purchase this ability can add up to five fully charged rings of slaying (40 teleports)
> and up to six fully charged ferocious rings (30 teleports) to any full slayer helmet variant to
> gain access to their teleports. The number of rings a player can fuse to it depends on the tier of
> the helmet.
>
> Players can recharge the teleports by fusing more rings, or by paying 5 [[co-op Slayer points]].
> The helm does not gain the [[ring of life]] property of the ferocious ring, and already has the
> non-teleport properties of a ring of slaying. Fused slayer helmets benefit from the ferocious ring
> damage boost.

### 3e. Tool belt

| Reward | Cost | Description (verbatim) | Notes (verbatim) | Var candidate |
|---|---|---|---|---|
| Learn how to attach the bonecrusher to your tool belt | 500 | Learn how to attach the [[bonecrusher]] to your [[tool belt]]. | Requires the bonecrusher from the shops. | `TOOLBELT_BONECRUSHER_BOUGHT` (-28233, varp 5699, 0x4000) |
| Learn how to attach herbicide to your tool belt | 500 | Learn how to attach [[herbicide]] to your [[tool belt]]. | Requires the herbicide from the shops. | `TOOLBELT_HERBICIDE_BOUGHT` (-28234, varp 5699, 0x8000) |
| Learn how to attach seedicide to your tool belt | 500 | Learn how to attach [[seedicide]] to your [[tool belt]]. | Requires the seedicide from the shops. | `TOOLBELT_SEEDICIDE_BOUGHT` (-28235, varp 5699, 0x10000) |
| Learn how to attach the charming imp on your tool belt | 500 | Learn how to attach the [[charming imp]] to your [[tool belt]]. | Requires the charming imp from the shops. | `TOOLBELT_CHARMING_IMP_BOUGHT` (-28236, varp 5699, 0x20000) |
| Attach the gold accumulator on your tool belt | 500 | Learn how to attach the [[advanced gold accumulator]] to your tool belt. | Requires the advanced gold accumulator from the shops. | `TOOLBELT_GOLD_ACC_BOUGHT` (-38662, varp 5699, 0x100000) |

Related "enabled" bits (candidates): `TOOLBELT_BONECRUSHER_ENABLED` (-28232), `TOOLBELT_GOLD_ACC_ENABLED` (-38663).

### 3f. Sunken Pyramid (personal Slayer dungeon)

| Reward | Cost | Description (verbatim) | Notes (verbatim) | Var candidate |
|---|---|---|---|---|
| Learn to move the souls in your personal slayer dungeon | 1,000 | Learn how to control the souls in your slayer dungeon to move them between chambers. | Allows the use of the [[Slayer master's Ouija board]] in the [[Sunken Pyramid]]. | `SLAYER_POD_MANAGEMENT_PURCHASED` (-48272, varp 7014, 0x80000000) |

## 4. Buy tab

Source: https://runescape.wiki/w/Template:Slayer_Rewards_stock (section "Buy")

| Item | Cost (points) | Requirement / description (verbatim) | Var candidate |
|---|---|---|---|
| Broad arrows x50/100/150/200/250 | 35 | Amount by Slayer level: 1 / 5 / 15 / 25 / 35 Slayer. "50 broad arrows." etc. | |
| Broad bolts x50/100/150/200/250 | 35 | Same Slayer level steps. | |
| Runes for Slayer Dart | 35 | 50 death + 150 air runes at 1 Slayer, up to 250 death + 750 air runes at 35 Slayer. | |
| Ring of Slaying | 75 | A ring which enables teleports to Slayer locations (8 charges). | |
| Full Slayer Helmet Upgrade (1) | 100 (re-upgrade 10) | Upgrade the stats of one Full Slayer Helmet (tier 1). Upgraded helmet requires 30 Defence to wear. Chosen helmet must be worn to be eligible for upgrade. | `NJSLAY_BOUGHT_UPGRADE1` (-21750, varp 4061, 0x80) |
| Full Slayer Helmet Upgrade (2) | 400 (re-upgrade 40) | ... (tier 2). Upgraded helmet requires 50 Defence to wear. ... must have the tier 1 upgrade. | `NJSLAY_BOUGHT_UPGRADE2` (-21751, 0x100) |
| Full Slayer Helmet Upgrade (3) | 600 (re-upgrade 60) | ... (tier 3). Upgraded helmet requires 70 Defence to wear. ... must have the tier 2 upgrade. | `NJSLAY_BOUGHT_UPGRADE3` (-21752, 0x200) |
| Full Slayer Helmet Upgrade (4) | 1,000 (re-upgrade 100) | Upgrade the effectiveness of one Full Slayer Helmet (tier 4). Upgraded helmet requires 70 Defence to wear. Chosen helmet must be worn to be eligible for upgrade, and must have the tier 3 upgrade and a corrupted gem. | `NJSLAY_BOUGHT_UPGRADE4` (-36285, varp 4061, 0x200000) |
| Ferocious ring upgrade (for use in Morvran's dungeon) | 100 | Enable use of ferocious rings in Morvran's dungeon (with 90 Slayer). | none found |
| Slayer XP | 400 | 10000 Slayer XP. Footnote: "The player receives 250 Slayer experience at Slayer level 1, scaling up to 10,000 at level 35 or higher." | |
| Ushabti | 20 | A figurine that has the ability to hold the soul of a Slayer monster. | |
| Fourth Room in Sunken Pyramid | 3,000 | Access to the fourth room in the [[Sunken Pyramid]]. Available after completing the quest '[[Eclipse of the Heart]]'. Requires 99 Slayer and access to the chambers within the Sunken Pyramid | `SLAYER_POD_FOURTH_ROOM_PURCHASED` (-58314, varp 7015, 0x40000000) |

Helmet tiers themselves (stats, corrupted bonuses): see `wiki-slayer-helmet.md`. Other helmet var
seen: `SLAYER_HELMET_NECROMANCY_ATTACHMENT_UNLOCKED` (-56741), probably the ensouled spectral lens
(not verified, see helmet file).

### Slayer XP reward breakdown (verbatim table, Slayer level -> XP for the 400-point reward)

| Level | XP | Level | XP |
|---|---|---|---|
| 1 | 250 | 19 | 1,773 |
| 2 | 250 | 20 | 1,995 |
| 3 | 250 | 21 | 2,239 |
| 4 | 250 | 22 | 2,510 |
| 5 | 250 | 23 | 2,807 |
| 6 | 250 | 24 | 3,136 |
| 7 | 290 | 25 | 3,499 |
| 8 | 357 | 26 | 3,900 |
| 9 | 432 | 27 | 4,342 |
| 10 | 515 | 28 | 4,830 |
| 11 | 606 | 29 | 5,369 |
| 12 | 706 | 30 | 5,964 |
| 13 | 818 | 31 | 6,620 |
| 14 | 940 | 32 | 7,344 |
| 15 | 1,076 | 33 | 8,143 |
| 16 | 1,225 | 34 | 9,026 |
| 17 | 1,390 | 35 | 10,000 |
| 18 | 1,572 | | |

## 5. Co-op tab (Co-op Slayer points, not normal Slayer points)

Source: https://runescape.wiki/w/Template:Slayer_Rewards_stock/Co-op

| Reward | Cost (co-op points) | Description (verbatim, shortened to the first sentence where long) | Var candidate |
|---|---|---|---|
| Recharge a fused Full Slayer Helmet | 5 | Recharge the teleport charges on your Fused Slayer Helmet. | |
| Recharge Rings of Slaying and Ferocious Rings | 10 | Recharge all Rings of Slaying and Ferocious Rings you are currently carrying. | |
| Ability to use food on your partner | 25 | Learn how to use food to heal your co-op Slayer partner in designated Slayer areas | |
| You share your partner's protective equipment | 30 | Learn how to share your co-op partner's protective slayer equipment. Equipment shared: facemask, earmuffs, insulated boots, mirror shield, spiny helmet, witchwood icon, Slayer gloves and nose peg. Partner must be nearby and within a designated Slayer area. | `NJSLAY_BOUGHT_EQUIPSHARE` (-21394, 0x40) |
| Your partner gains half your portent of restoration effects | 35 | Learn how to share your portent healing effects with your co-op partner. | `NJSLAY_BOUGHT_DIVINE` (-21389, 0x2)? |
| Squidge (pet) | 50 | Buy Squidge, the baby aquanite. | |
| Share your Slayer teleports with your partner | 60 | Learn how to share your Slayer teleports (Ring of Slaying, Ferocious Ring, or Fused Slayer Helmets) with your co-op partner. | `NJSLAY_BOUGHT_TELEPORTS` (-21390, 0x4) |
| Your partner gains half your potion effects | 75 | Learn how to share half the effect of potions you drink with your nearby co-op Slayer partner, within designated Slayer areas. | |
| Freezy (pet) | 100 | Buy Freezy, the baby ice strykewyrm. | |
| Freezy's jungle / wilderness / desert skin | 125 each | Unlock the ... skin for your Freezy pet. Requires Freezy (pet). | `NJSLAY_JUNGLE_SKIN` / `NJSLAY_WILDY_SKIN` / `NJSLAY_DESERT_SKIN` (-21392 / -21393 / -21391) |
| Runtstable (pet) | 200 | Buy Runtstable, the baby ganodermic runt. | |

The co-op protective-equipment share is the only co-op reward that touches task requirements
(items from `wiki-slayer-equipment.md` and `wiki-slayer-helmet.md`).

## 6. Update history (verbatim)

Source: https://runescape.wiki/w/Slayer_Rewards

- 28 July 2025 (update, Eclipse of the Heart): Added purchasing Fourth Room in Sunken Pyramid.
- 29 July 2025 (coldfix): Making the 4th Slayer Helmet upgrade visible in the store again.
- 26 October 2020 (ninja): Slayer Masters will now teach the ability to use the Slayer Master's
  Ouija Board for 1,000 Slayer Points. Using the Slayer Master's Ouija Board within the Sunken
  Pyramid will allow you to customise the placement of creatures in your Personal Slayer Dungeon.
- 4 May 2020 (patch): A new Slayer point icon has been created so that it can be displayed in the
  Reward interface.
- 24 February 2020 (patch): RuneScape Mobile: Improved the visibility of messages generated for
  users when interacting with the Slayer Rewards shop on mobile.
- 16 September 2019 (patch): Right-clicking on the prefer list within the slayer rewards interface
  will now show 'Remove preferences' rather than 'Allow this task'.
- 19 August 2019 (patch): Corrected the full slayer helmet tier 4 Defence requirement in the Slayer
  Rewards shop to match its level.
- 20 August 2018 (ninja): Blocking/Preferring tasks now immediately adds them to the list on the
  interface.
- 13 November 2017 (ninja): The Slayer Rewards shop has been graphically updated to be more in line
  with current interface standards.
- 10 July 2017 (patch): The 'prefer task' option on the Slayer Rewards interface will now appear
  disabled when the player does not have enough points.
- 11 January 2016 (patch): Familiars no longer block the 'deliver finishing blows quicker' slayer
  ability.
- 4 March 2013 (patch): The Slayer Rewards interface no longer has the tooltips sticking in place.
- 24 July 2012 (patch): It is now possible to once again purchase the "Enable Aquanites" reward
  from the Slayer rewards interface with less than 100 points.
- 7 February 2012 (patch): Bank PIN protection has been added to the Slayer Rewards interface.
- 6 December 2011 (patch): The tooltip on the Slayer rewards interface for "Never assign X again"
  has been shortened.
- 3 March 2010 (patch, Shattered Heart): The ability to deal killing blows faster to specific Slayer
  creatures can now be purchased. The ability to be assigned ice strykewyrms and aquanites from
  Kuradal can now be purchased. A 5th task can now be blocked if the player has more than 250 quest
  points.
- 8 July 2009 (patch): Corrected some pre-purchase advice for Slayer items.
- 5 June 2008 (update, Smoking Kills): Added to game.

Achievements linked from the page: Special Slayer Delivery, Get Tooled Up, Finished unpacking!
(not looked up).

## 7. Compared with the plugin data (2026-10-22)

Matches:
- Costs in `core/points.lua` (`M.COST = { cancel = 30, extend = 30, block = 100, prefer = 100 }`)
  and slots (1 per 50 quest points, max 8) match the wiki.
- Turael/Spria resetting the streak, Mandrith ignoring the lists: match `data/masters.lua`.
- Toggle tasks at Kuradal, Morvran, Laniakea (aquanites, muspah, nihil, glacors, tormented demons,
  nightmare creatures, all `toggle = true`, cost 50 in laniakea.lua comment): match.
- Aquanites at Sumona and Duradel without a toggle: matches (no `toggle` in sumona.lua / duradel.lua).
- Quicker killing blows: matches `finisher_unlock = "unlock:finishing_blows"` in afk_traits.lua
  (now a manual setting).

Differences / to check:
1. **Muspah and nihil: wiki says "with 76 Slayer"**, our task data (laniakea, kuradal, morvran)
   only has `quest("Fate of the Gods")`, no Slayer 76. Check against the game structs
   (SLAYER_SL_REQ) or the assignment pages.
2. **Glacors at Mandrith** (`tasks/mandrith.lua`) has `toggle = true`; the wiki Learn text only
   names Kuradal, Morvran and Laniakea. Not verified whether Mandrith needs the toggle.
3. **Ice strykewyrm technique** (2,000 points) is only in the requirement label; the check reads
   the fire cape vars only. `SMKI_ICE_STRYKEWYRM_NOFIRE` could make it readable.
4. **Prefer is a second roll**, not exactly x2 (CLAUDE.md formula "prefer x2"). The wiki itself says
   "approximately doubles"; the Mod Rowley quote gives the real mechanism.
5. **Prefer also extends the current task** ("Extends the player's current assignment
   automatically"); the plugin does not mention this.
6. **Blocking a Laniakea cluster task does not block its subset tasks** (e.g. Creatures of
   Daemonheim vs Kal'gerion demons / Stalker creatures). Check that the advice does not treat a
   blocked cluster as blocking its parts.
7. **Extend**: +20% of the initial amount, no extra points, not twice in a row on the same task.
8. Nihil XP differs inside our own data: laniakea.lua 423.2, kuradal.lua/morvran.lua 705.4
   (outside this page, noticed while comparing).

## 8. Not verified

- Every var candidate above (none checked in game). Strongest by name: `SMKI_KURADAL_AQUANITE`,
  `SLAYER_KURADEL_MUSPAH`/`_NIHIL`, `BSLAY_UNLOCKED_GLACORS`/`_TDEMONS`,
  `SMKI_ICE_STRYKEWYRM_NOFIRE`, `SMKI_HEAD_MAKE`/`SMKI_RING_MAKE`/`SMKI_MISSILE_MAKE`,
  `NJSLAY_BOUGHT_*`, `TOOLBELT_*_BOUGHT`, `SLAYER_POD_*_PURCHASED`. Weak: `SMKI_AUTOSMASH_GARGOYLE`
  (quicker killing blows?), `FOTG2_NIGHTMARE_TASK_UNLOCKED`, `ELFCITY_SLAYER_TASK_EXTENDED`.
- No var found for the ferocious ring upgrade (Morvran's dungeon) or a "task extended" flag.
- Whether a toggled-off reward (free to switch off, paid to switch on) clears the same bit.
- Ferocious ring, Sunken Pyramid and co-op pages were not read beyond this shop page.
