# Slayer masks (RS3 wiki reference)

Source: https://runescape.wiki/w/Slayer_mask (read 2026-10-22 through a page
reader: a summary, only the quoted sentence is verbatim; first 100,000 of
158,737 characters read). Licence: RuneScape Wiki text, CC BY-NC-SA 3.0.

## What they do
- Force a Slayer task for the mask's creature when asking a master that assigns
  it; cooldown 1 or 3 days per mask (the three strykewyrm masks share one).
  A forced task changes SLAYER_TARGET/SLAYER_COUNT without a VarTransmit (Beta).
- Two free daily teleports to the creature's locations.
- On an assignment for its creature, until the helm is unlocked: +12.5% damage
  and accuracy (overrides the helmet-stand bonus).
- Bonus Slayer XP per kill equal to the creature's Slayer level, on or off task,
  until upgraded to the helm. Every 10th kill: double drops (until upgraded).
- "Both masks and helms provide the same benefits as the spiny helmet, earmuffs,
  face mask, and nose peg." (verbatim). Mask of Stone / helm of Petrification
  and mask of Reflection / helm of Little Kings also replace the mirror shield
  (Basilisk page).
- After N kills the mask becomes its helm (keeps forcing, teleports,
  protection; loses bonus XP, damage boost, double drops). "Check Kills" shows
  kills and the 3-day cooldown. Masks warn before forcing a blocked task; no
  forcing in a co-op group.
- Bought in the Shattered Worlds Reward Shop (removed from Treasure Hunter
  27 Sep 2021).

## Masks (creature, Slayer level, kills to helm, cooldown days) and config names
| Mask / helm | Creature | Slayer | Kills | Cooldown | Config (mask / helm) |
|---|---|---|---|---|---|
| Troll / Troll | Trolls | 1 | 100 | 1 | TRH64_SLAYER_MASK_TROLL / _HELM_ |
| Broken Fingers / Dead Hand | Crawling hands | 5 | 100 | 1 | WOF35_SLAYER_MASK_HANDS |
| Mourning / Keening | Banshees | 15 | 200 | 1 | WOF50_SLAYER_MASK_BANSHEE |
| Stone / Petrification | Cockatrice | 25 | 300 | 1 | WOF35_SLAYER_MASK_COCKATRICE |
| Reflection / Little Kings | Basilisks | 40 | 500 | 1 | WOF35_SLAYER_MASK_BASILISK |
| Crimson / Blood | Bloodveld | 50 | 600 | 1 | TRH9_SLAYER_MASK_BLOODVELD |
| Gelatin / Jellyhead | Jellies | 52 | 600 | 1 | WOF50_SLAYER_MASK_JELLY |
| Stench / Foulness | Aberrant spectres | 60 | 700 | 1 | TRH9_SLAYER_MASK_ABERRANT_SPECTRE |
| Dust / Devilry | Dust devils | 65 | 700 | 1 | WOF50_SLAYER_MASK_DUSTDEVIL |
| Kura / Kuraski | Kurask | 70 | 800 | 1 | WOF35_SLAYER_MASK_KURASK |
| Green Wyrm / Verdant Wyrm | Jungle strykewyrms | 73 | 800 | 3 (shared) | TRH9_SLAYER_MASK_JUNGLE_STRYKEWYRM |
| Granite / Grotesquery | Gargoyles | 75 | 800 | 1 | WOF50_SLAYER_MASK_GARGOYLE |
| Dagannoth / Dagannoth | Dagannoth | 1 | 1,000 | 3 | TRH64_SLAYER_MASK_DAGANNOTH |
| Yellow Wyrm / Parched Wyrm | Desert strykewyrms | 77 | 800 | 3 (shared) | TRH9_SLAYER_MASK_DESERT_STRYKEWYRM |
| Vines / Mutation | Mutated jadinkos | 80 | 900 | 1 | WOF50_SLAYER_MASK_JADINKO |
| Abyss / Warping | Abyssal creatures | 85 | 900 | 1 | WOF35_SLAYER_MASK_ABYSSAL |
| Black Demon / Black Demon | Black demons | 1 | 1,000 | 3 | TRH64_SLAYER_MASK_DEMON |
| Automatons / Automatons | Automatons | 67 | 1,000 | 3 | TRH64_SLAYER_MASK_AUTOMATON |
| Aquanites / Aquanites | Aquanites | 78 | 1,000 | 3 | TRH64_SLAYER_MASK_AQUANITE |
| Gloom / Darkness | Dark beasts | 90 | 1,000 | 1 | TRH9_SLAYER_MASK_DARK_BEAST |
| Airut / Airut | Airut | 92 | 1,000 | 3 | TRH64_SLAYER_MASK_AIRUT |
| White Wyrm / Frozen Wyrm | Ice strykewyrms | 93 | 1,000 | 3 (shared) | TRH9_SLAYER_MASK_ICE_STRYKEWYRM |
| Ganodermic / Ganodermic | Ganodermic creatures | 95 | 1,000 | 3 | TRH64_SLAYER_MASK_GANODERMIC |

Helm config names: same with `_SLAYER_HELM_` instead of `_SLAYER_MASK_` (pan-Obj).
The mask-to-config mapping is by creature name (not verified in game per mask).

## Update history (summary)
27 Jan 2025 mask task options shown together with VIP ticket options; 27 Sep 2021
removed from Treasure Hunter, Shattered Worlds only; 15 Jul 2019 correct tasks
from Laniakea; 3 Jul 2017 can produce blocked tasks; 13 Mar 2017 Check kills shows
3-day cooldown; 23 Nov 2015 hybrid class; 2 Apr 2013 choice when asking the wrong
master. Not read: the last 58,737 characters of the page.
