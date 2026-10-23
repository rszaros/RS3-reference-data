# RS3 plugin API: what is technically possible (feasibility check)

Read 2026-10-23 from the official docs at https://developer.runescape.com/rs/
(through a page reader; quotes are verbatim, everything else is a summary).
"Not documented" = the page says nothing about it; it may still exist.

## 1. Saving per-task measurements across sessions and characters
Source: https://developer.runescape.com/rs/core/persistentdb.html
- Possible. `PersistentDB` with `Get/Set` and typed variants (`SetInt`, `SetString`,
  `SetStructuredData`, ...), `IterateEntries`, `Delete`, `Clear`.
- "Records are isolated per plugin". "Records are shared by all game clients of
  the same type on the device, and therefore all characters that are played from
  the device." Per character: put the character in the key (we already hash the
  display name). "Records are not shared between beta and live game clients."
- Size / entry limits: not documented. Seen in the Beta: writes failed after
  ~700 small log entries, so store one structured table per character, not one
  entry per measurement.
- Guidelines: no rule on storing data on this page (data protection page not
  covered); our plan stays "Case 1" (nothing leaves the PC).

## 2. Grand Exchange prices and alch value
Sources: https://developer.runescape.com/rs/game/grandexchange.html ,
https://developer.runescape.com/rs/game/config/objtype.html
- No market price lookup. `GrandExchange.GetOffer(slot)` only gives the player's
  own offers; `GrandExchangeOffer.price` is "The gold price per individual item"
  of that offer.
- ObjType has `cost` ("The 64-bit numeric value of this object"), `isStockmarket`,
  `stockmarketBuyLimit`, `isTradeable`, `isMembers`, `params`. High alchemy: not
  documented (alch is commonly derived from the item value; not verified).
- So GE prices must be shipped with the plugin (or fetched with HTTP, see 10).

## 3. Player location / which Slayer area
Sources: https://developer.runescape.com/rs/game/entity/playerentity.html ,
https://developer.runescape.com/rs/game/coordgrid.html ,
https://developer.runescape.com/rs/game/world.html
- Possible: `Player.GetEntity()` -> PlayerEntity `coordGrid` (CoordGrid: `level`,
  `x`, `z`, `mapSquareX`, `mapSquareZ`, `localX`, `localZ`), `position`, `route`,
  `routeEnd`.
- No area/zone names and no distance function (distance = own maths on x/z).
  `World.IsRegion()`, `World.GetRegionSourceForCoordGrid(coord)` for instanced
  regions; events `RegionCreated`, `WorldCreated`.
- Knowing "you are in the Fremennik Slayer Dungeon" needs our own table of
  coordinate boxes per location (not in the game API).

## 4. Shortest path / route / markers
Sources: https://developer.runescape.com/rs/game/shapes.html ,
https://developer.runescape.com/rs/game/config/mapelementtype.html , guidelines
- No pathfinding API documented.
- Drawing: Shapes draw "simple 3D shapes within the game world" (`ShapeList.Draw`,
  `CreateInstance`, `CreateEntity`). Minimap / world map: not documented;
  MapElementType cannot be created by plugins ("you cannot create your own").
- Guidelines: "Navigation or guidance systems" are Subject to review; Prohibited:
  "Anything that automatically indicates where to stand, or not to stand." and
  "Automatically indicating where players should stand or move." Allowed:
  "Manually placed markers or notes."
- Conclusion: text routes (wiki "how to get there") are fine; an automatic drawn
  route is risky and would need review.

## 5. Teleport options
- No teleport/spellbook/lodestone API documented. Possible only through vars
  (quests via `config.Quest`, items via inventories). Lodestone unlock vars: not
  found by name in pan-VarPlayer (grep LODESTONE: only league/fort/tutorial
  vars); not verified. Spellbook var: not found by name.

## 6. Bank contents
Sources: https://developer.runescape.com/rs/game/inventory.html ,
https://developer.runescape.com/rs/game/config/invtype.html
- `Inventory.Find(config.Inv.BANK)` exists as a config (`config.Inv.BANK` is named).
  Whether the bank is readable when closed: not documented ("Inventories can be
  added or removed from the client by the server for a variety of reasons").
  Events `InventoryAdded/Updated/Removed` suggest the bank arrives when opened.
  Needs a Beta test.
- Guidelines: nothing specific on bank or best-in-slot; "interpreted or
  actionable gameplay recommendations may be subject to stricter review".

## 7. Achievements
Source: https://developer.runescape.com/rs/game/config/achievementtype.html
- Possible: `config.Achievement[name]` / `FromID`, `progress` ("Values above 0 are
  percentages out of 10000"), `prereqsComplete`, requirement tests with
  `isComplete`, `reward` (text), `requirements`.
- So "achievement done / not done" can be read; which items an achievement needs
  is not a field (requirements are tests, not item lists).

## 8. NPCs near the player
Source: https://developer.runescape.com/rs/game/list/npclist.html
- Possible: NPCList `All`, `ByName`, `ByDistance(coordGrid, range)`, `ByConfig`,
  `ByConfigID`, `Filter`; events `NPCEntityAdded/Removed`.
- E.g. count task monsters around you or see a Slayer master nearby. Health /
  combat level / target of NPCs: not documented on this page.
- Guidelines: Prohibited: "Indicates which player an NPC is focused on"; NPC
  highlighting beyond parity is not allowed; counting is not addressed.

## 9. Notifications outside our window
Sources: https://developer.runescape.com/rs/game/chat.html ,
https://developer.runescape.com/rs/audio/index.html , events, guidelines
- Chat: `Chat.AddMessage(message)`: "Plugin-created chat messages are visible only
  to the local Player Character, and are not transmitted." Needs the
  `chatAccess` permission.
- Sound: `audio.Play(resource, params?)` for built-in or custom sounds; no
  permission mentioned.
- Toast/pop-up: not documented (only our own UI components).
- Guidelines: Allowed: "Notifications based on visible or already-known
  non-combat events." Subject to review: "Containing custom resources like images
  or sounds." and any plugin that requests a permission.

## 10. HTTP at runtime
Source: https://developer.runescape.com/rs/core/http.html
- Possible: `HTTPRequest.new(baseURL, path)`, `:Get`, `:Post`, `:AddHeader`,
  `:Cancel`; permission `httpAccess`; every base URL must be declared under
  `urls` in plugin.json. "Specifying malformed URLs or URL shortener/redirect
  addresses will cause your plugin to be rejected." Rate limits: not documented.
- Guidelines: a requested permission makes the plugin "Subject to review"; data
  protection then is no longer "nothing leaves the PC" (our CLAUDE.md decision:
  no HTTP at runtime, ship data instead).
