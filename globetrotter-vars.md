# Globetrotter outfit vars (not part of Slayer Helper)

## Globetrotter outfit (Treasure Trails), confirmed Beta 2026-10-23

Worn objs: TRAIL17_TORSO/LEGS/GLOVES/BOOTS/CAPE_TIER3 (cape = Globetrotter backpack).

- TRAIL_OUTFIT_*_OWNED (TORSO/LEGS/GLOVES/BOOTS/CAPE) = 1 each, TRAIL_OUTFIT_FULL_OWNED = 31 (bitmask of the 5).
- TRAIL_OUTFIT_TORSO_CHARGES = 3, CAPE_CHARGES = 4, BOOTS_CHARGES = 4; *_CHARGE_PROGRESS = 0.
  Meaning still to confirm (torso = direct teleport? cape = swap clue? boots = ?).
- Arm guard teleport scrolls: TRAIL17_TELEPORT_CHARGE_<DEST>, 10 bits (max 1023).
  All 10 matched the in-game menu exactly: GRAND_EXCHANGE 105, BANDIT_CAMP 18, CLOCKTOWER 66,
  GUTANOTH 70, LIGHTHOUSE 18, FORT_FORINTHRY 133, MISCELLANIA 115, PHOENIX_LAIR 118,
  POLLNIVNEACH 177, TAI_BWO_WANNAI 129.
