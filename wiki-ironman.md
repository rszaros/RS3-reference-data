# Ironman Mode: what matters for Slayer Helper

Collected 2026-10-22 via the MediaWiki API (`action=parse&prop=wikitext`).
Quotes in "..." are verbatim. "Not verified" = our reading or not on the page.
Licence: RuneScape Wiki text, CC BY-NC-SA 3.0.

Sources:
- https://runescape.wiki/w/Ironman_Mode
- https://runescape.wiki/w/Group_Ironman_Mode

## Modes

- "Ironman Mode has two difficulties: Ironman and Hardcore Ironman. Hardcore
  players have the added challenge of only starting with one "life". As soon as
  their last life runs out, their account is switched to normal Ironman Mode."
- Group Ironman Mode (28 October 2024): "a mode allowing up to 5 people to group
  together, using modified ironman rulesets". Regular or competitive groups:
  "Group Ironman Mode players may freely trade within the group and have access
  to a shared group storage."
- Mode can be switched off with the jar of divine light / book of diplomacy
  (Mr Ex). So the mode can change on an account: read it, don't store it.

## Restrictions that matter for Slayer advice

### Trading / Grand Exchange (GP focus)
- The mode disables "trading with other players, the assist system, the Grand
  Exchange and loot from PvP".
- Grand Exchange usage: "No Except purchasing cosmetics and bonds only".
- "Examining a tradeable item while in Ironman Mode will display the high
  alchemy price instead of its Grand Exchange value. The price checker will also
  function this way, however loot beams are still based on Grand Exchange value."
- Consequence for the plugin (our reading): for an Ironman, "GP" focus cannot
  mean GE value. Useful options: high alchemy value, or "items you need"
  (supplies, quest/achievement items, collection log). Not decided.

### Legendary pets
- "Legendary pet features cannot be used: life saver, slayer finisher, repair and
  fertiliser." So `pet:slayer_finisher` must stay off for Ironmen (already noted
  in wiki-legendary-pet.md and data/afk_traits.lua).

### Slayer features
- "Co-op Slayer is disabled." (table: "Social Slayer: No").
- Group Ironman: Social Slayer IS available within the group (Group Ironman page,
  "Other content": "Social Slayer").
- "Features in other players' player-owned houses and personal slayer dungeons
  are disabled." Since late 2024 "non-ironman accounts can no longer enter an
  ironman's player-owned Slayer dungeon" (Sunken Pyramid).
- Kill XP: "Any NPCs killed will award experience depending on how much damage
  the player has done to it, not the full experience set on the monster."
- No Double XP, no event bonus XP; "Ironmen no longer benefit from the Grand
  Party (20th Anniversary Event's) increased Slayer XP buff".
- Update history items: Ironmen get Slayer drops/progress with siege cannons vs
  the Nodon; Slayer XP, KC and loot from abandoned siege engines; "Ironmen can
  now complete slayer tasks within the Dragonkin Laboratory"; "Slayer XP rewarded
  from completing Reaper tasks as an Ironman is no longer halved."
- Ironman black mask: obtainable from sea horrors (Shadow Reef) or cave /
  unspeakable horrors on Mos Le'Harmless (58 Slayer, Cabin Fever); see
  wiki-slayer-helmet.md.

### Microtransactions
- Premier reward token items Ironmen can use: Lightning staff, Bloodpouncer
  (a legendary pet), "This includes non-cosmetic items (such as silverhawk
  boots) which were sometimes obtainable outside Treasure Hunter".
- Whether Ironmen can use Slayer masks (now Shattered Worlds Reward Shop, see
  wiki-slayer-masks.md): not stated on the page. Not verified.

## Game vars for the account mode (pan-VarPlayer.txt candidates)

Base var `4818 IRONMAN INTEGER` holds the mode bits:

| id | name | type | base | mask |
|---|---|---|---|---|
| -20807 | IRONMAN_ENABLED | INTEGER | 4818 | 0x1 |
| -20808 | HARDCORE_ENABLED | INTEGER | 4818 | 0x2 |
| -21788 | IRONMAN_EARLYACCESS | INTEGER | 4818 | 0x4 |
| -25403 | HARDCORE_LIVESUSED | INTEGER | 4818 | 0x38 |
| -25404 | HARDCORE_LIVESUNLOCKED | INTEGER | 4818 | 0x1c0 |
| -28631 | IRONMAN_NEVER_DISABLE | INTEGER | 4818 | 0x1000 |
| -56612 | ACCOUNT_CREATED_POST_GROUP_IRONMAN_RELEASE | INTEGER | 4818 | 0x40000 |
| -56613 | GROUP_IRONMAN_ENABLED | INTEGER | 4818 | 0x80000 |
| -56614 | GROUP_HARDCORE_ENABLED | INTEGER | 4818 | 0x100000 |
| -56615 | GROUP_IRONMAN_CACHE_RULESET | INTEGER | 4818 | 0xe00000 |
| -56617 | GROUP_IRONMAN_HISCORE_INELIGIBLE | INTEGER | 4818 | 0x2000000 |

Also: `4819 IRONMAN_TEMP` (selection screen temps), `-56589
GROUP_IRONMAN_CACHE_GROUP_SIZE` (11938, 0xf), `-56574 GROUP_IRONMAN_MEMBER`
(11927, 0x2). Meaning of the ruleset values (regular vs competitive): not
verified.

## In-game test (Beta dev world)

1. Add to the watch list (main.lua, `adapter.watch`): IRONMAN_ENABLED,
   HARDCORE_ENABLED, GROUP_IRONMAN_ENABLED, GROUP_HARDCORE_ENABLED,
   GROUP_IRONMAN_CACHE_RULESET, HARDCORE_LIVESUSED, HARDCORE_LIVESUNLOCKED.
2. Reload; start values should be 0 on the (normal) test account.
3. Run `!setironman 1`, wait, then `!sethardcore 1`, then `!setgroupironman 1`;
   undo each with `0`. The log should show the matching var going 0 -> 1 -> 0.
   (Cheats are logged by Jagex; confirm the cheats work at all first.)

Not verified: whether these varbits are transmitted to the client at all (only
vars the server sends are visible), and what the cheats change.
