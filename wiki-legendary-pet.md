# Legendary pets and Slayer Finisher (RS3 wiki research, 2026-10-22)

Facts copied from the RuneScape Wiki via the MediaWiki API (wikitext). Anything unclear is
marked "not verified". Wiki text is CC BY-NC-SA 3.0.

Related files (not repeated here):
- `wiki-slayer-equipment.md`: finisher items (rock hammer, bag of salt / salt shaker, ice cooler /
  ice shaker, fungicide spray / shaker) and the "deliver killing blows quicker" unlock text.
- `wiki-slayer-rewards.md`: the quicker killing blows unlock (400 points, 75 Slayer) in the shop.

---

## 1. What a legendary pet is

Source: https://runescape.wiki/w/Legendary_pet

> "Legendary pets are interface pets that differ from companion and follower pets for their
> abilities that can help the player in many different ways."

> "Most legendary pets could be obtained by purchasing them from Solomon's General Store or the
> Marketplace for RuneCoins, while some are available through other methods."

Sources in the wiki list: Solomon's General Store and Marketplace (RuneCoins), Premier Token Store
(Bloodpouncer, Prime colossus), several "Currently not available". Individual pets not covered here.

### Growth

> "All legendary pets have three stages of growth - baby, adolescent, and adult. 900 pet points
> are required for a legendary pet to reach the adolescent state, and a further 1500 points for it
> to reach the adult stage. A pet will take approximately 15 hours to reach the adolescent stage and
> an additional 25 hours to reach the adult stage."

Tasty treat +50% growth rate, jelly treat +100%, Growth Surge advances one stage instantly.

### Number of abilities

Source: https://runescape.wiki/w/Template:Legendary_pet_abilities (shown on the Legendary pet page)

> "Pets in the baby stage can have one active ability, adolescent pets can have two, and adult pets
> can have three. Abilities can be switched out at any time unless that ability is on cooldown.
> Active abilities are switched via the pet interface by clicking on the "Abilities" button at the
> bottom right corner."

> "Life Saver, Slayer Finisher, Item Repair, and Fertiliser are not available for Ironman Mode
> accounts."

Which pet can have which ability: the wiki gives no per-pet restriction; the ability list is shared
by all legendary pets. That every pet can pick every ability is **not verified** (only implied).

---

## 2. List of abilities

Source: https://runescape.wiki/w/Template:Legendary_pet_abilities (descriptions verbatim)

| Ability | Type | Description |
|---|---|---|
| Forage | Active | Finds items for you as you explore. |
| Banking | Active (10 minutes cooldown) | Takes one item to the bank for you. |
| Scavenge | Passive | Collects the most expensive item from monsters that you defeat. |
| Life Saver | Passive (2 hours cooldown) | If your health drops below 10%, your legendary pet will drag you to safety. This does not work in PvP areas. |
| Slayer Finisher | Passive | Finish off any slayer monsters that require an item to be killed. |
| Item Repair | Active (1 hour cooldown) | Use weapons and armours on your pet to have them repaired (normal costs still apply). |
| Beast of Burden | Passive | Use a beast of burden pouch on your pet to gain the ability to store items in your pet. This does not work in PvP areas. |
| High Level Alchemy | Active (10 minutes cooldown) | Use items on your pet to cast High Level Alchemy on items transforming them into gold. |
| Fertiliser | Active (1 hour cooldown) | Use the natural abilities of your pet to create super compost. |

Notes (verbatim, shortened to the relevant part):
- Scavenge: "The pet will only pick up one item from a slain enemy ... There is a chance that the
  item picked up by the pet be sent directly to the bank rather than the backpack. This ability has
  a 10-second cooldown."
- Life Saver: "The pet will save the players from death, as per a ring of life."
- High Level Alchemy: "This requires 55 Magic, but does not consume runes or grant any experience."

---

## 3. Slayer Finisher

Source: https://runescape.wiki/w/Slayer_Finisher (full page text)

> "Slayer Finisher is a passive ability of legendary pets.
>
> The pet will automatically finish off Slayer monsters that usually require an item, saving the
> players a right-click action and/or a backpack space.
>
> This ability is not available for Ironman Mode accounts."

- Requirements: a legendary pet with Slayer Finisher as one of its active ability slots; not for
  Ironman accounts. No Slayer level or points requirement is mentioned.
- Item still needed? The page says it saves "a right-click action and/or a backpack space", which
  implies the item is not needed. **Not verified** for each monster (see table).
- Update history: the section on the page is commented out with no date. Release date **not
  verified**.

### Which monsters (from the monster pages)

| Monster / task | Finisher item | Slayer Finisher works? | Source |
|---|---|---|---|
| Gargoyles | rock hammer (or upgraded Darklight) | Yes | https://runescape.wiki/w/Gargoyle |
| Corrupted scarab (corrupted creatures) | feather of Ma'at | **No** | https://runescape.wiki/w/Corrupted_scarab |
| Rockslugs | bag of salt / salt shaker | No (user, 2026-10-22: gargoyles only) | https://runescape.wiki/w/Rockslug (redirect) |
| Desert lizards | ice cooler / ice shaker | No (user, 2026-10-22: gargoyles only) | https://runescape.wiki/w/Desert_lizard |
| Mutated zygomites | fungicide spray / shaker | No (user, 2026-10-22: gargoyles only) | https://runescape.wiki/w/Mutated_zygomite |
| Soul devourers (akh) | feather of Ma'at | No (user, 2026-10-22: gargoyles only) | https://runescape.wiki/w/Soul_devourer |

Gargoyle (verbatim): "A rock hammer (or Darklight, if it has been upgraded after Dimension of
Disaster) is required to finish them off, when their health drops below 1,050 (2,000 in Wilderness)
life points. This is done by right-clicking the gargoyle and selecting "Smash", or automatically if
the finishing blows ability has been purchased with 400 Slayer reward points. The rock hammer may
also be added to the toolbelt to free inventory space for drops. Alternatively, players may use the
rock hammer or Darklight in their inventory on the Gargoyle, or be accompanied by a legendary pet
that has activated the passive ability Slayer Finisher, in which the pet will deal the final blow to
the Gargoyle when its health reaches 0."

Corrupted scarab (verbatim): "requires level 91 Slayer to damage and a feather of Ma'at to complete
each kill (the legendary pet ability 'Slayer Finisher' does not work)".

### Compared with the "deliver killing blows quicker" unlock

| | Quicker killing blows (Slayer Rewards) | Slayer Finisher (legendary pet) |
|---|---|---|
| Cost | 400 Slayer points, 75 Slayer | a legendary pet (RuneCoins / Premier token) with the ability selected |
| Item needed | yes, "must still be in the backpack or tool belt" (see wiki-slayer-equipment.md) | implied no ("saving ... a backpack space"), not verified per monster |
| Ironman | allowed (not verified) | not available |
| Feather of Ma'at monsters | not covered | does NOT work on corrupted scarab |

### Relevance for the plugin

- `data/afk_traits.lua`: `gargoyles` has `finisher = "rock hammer"`, `finisher_unlock =
  "unlock:finishing_blows"`; `soul_devourers` has `finisher = "feather of Ma'at"` with no unlock.
  Slayer Finisher is a second way to remove the finisher need (at least for gargoyles). It is a
  pet setting, not a Slayer reward, so it could be its own manual id (e.g. `pet:slayer_finisher`).
  Not for Ironman accounts.

---

## 4. Var candidates (pan-VarPlayer.txt, NOT tested in game)

| Var | id | Base varp / mask | Guess |
|---|---|---|---|
| `MTX_PET_ABILITY_1` | -27735 | 5020 / 0xf000 | ability in slot 1 (4 bits: an ability id) |
| `MTX_PET_ABILITY_2` | -27736 | 5020 / 0xf0000 | ability in slot 2 |
| `MTX_PET_ABILITY_3` | -27737 | 5020 / 0xf00000 | ability in slot 3 |
| `MTX_PET_ABILITY_LOGIN_CHECK` | -27738 | 5020 / 0x40000000 | unknown |
| `MTX_PET_ABILITY_COOLDOWN`, `_COOLDOWN_2` | 5257, 5258 | varps | ability cooldowns |
| `MTX_PET_ALCH_ABILITY` | -27744 | 5257 / 0x10000000 | High Level Alchemy related |
| `MTX_PET_BOB_ABILITY` | -27748 | 4053 / 0x4000 | Beast of Burden related |

Not found: a var for "a legendary pet is summoned now" or "which pet is summoned". Which number
in `MTX_PET_ABILITY_n` means Slayer Finisher is **not verified** (test: select the ability in slot 1
and read the var).

---

## Not verified

- Whether Slayer Finisher works on rockslugs, desert lizards, mutated zygomites, soul devourers
  (wiki pages don't say; only gargoyles yes, corrupted scarab no).
- Whether the finisher item may be left out entirely with Slayer Finisher (only implied).
- Whether the pet must be summoned / nearby (implied: "be accompanied by a legendary pet").
- Release date / update history of Slayer Finisher.
- Ability id numbers in `MTX_PET_ABILITY_1..3`, and a var for a summoned legendary pet.
- Whether every legendary pet can have every ability.
