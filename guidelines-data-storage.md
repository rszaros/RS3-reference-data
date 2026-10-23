# Storing data per player: what the official rules say

Read 2026-10-23 through a page reader (WebFetch). Short quotes are verbatim; the
rest is a summary. "Not documented" = the pages read do not say it.
Pages read: submission/guidelines.html, submission/example.html,
submission/process.html, submission/adequacy.html, core/persistentdb.html.
Not read: core/plugin.html, managing.html, structure.html.

## 1. Personal data: what counts
Sources: https://developer.runescape.com/rs/submission/example.html ,
https://developer.runescape.com/rs/submission/process.html
- No definition of personal data in the pages read: **not documented**.
- The example's placeholders for "information used" are: character name, in-game
  chat, hashed identifier, game events. Those are the kinds of data Jagex expects
  developers to list.
- "Your plugin is required to explicitly state what it will do with all
  information that it gathers." (process.html)
- Measurements (kills/h, XP/h) or collection log progress are not named; they are
  "game events / game information" derived data: classification **not documented**.

## 2. The data protection cases
Sources: example.html, process.html, adequacy.html
- Only one case is described in a submission: "Only one is required for your
  submission, for the data protection case that your plugin uses."
- **Case 1, no external transmission**: "Any information collected does not leave
  the local plugin." Template: "This information is not transmitted outside of the
  plugin under any circumstances." Game information is not kept between sessions;
  plugin settings are ("plugin setting are stored between sessions"). The contact
  e-mail may be hidden: "this email address is not required to be public".
- **Case 2**: sent to an endpoint in the UK/EU/EEA or a country with UK adequacy:
  name the endpoint, its security measures, who has access, a privacy notice URL.
- **Case 3**: sent to a country without adequacy (the USA counts as not adequate
  for plugins): as Case 2, plus private contact details, name and address to Jagex,
  a data protection contact e-mail, and a password-protected form.
- All cases: list the data used and the security measures. A privacy notice is
  expected ("You should also have a privacy notice in place that meets legal
  requirements."). A contact e-mail is required, e.g. "to have their data deleted".

## 3. PersistentDB
Source: https://developer.runescape.com/rs/core/persistentdb.html
- Per plugin, isolated: plugins cannot read each other's data.
- Shared by every character on the device: "Records are shared by all game clients
  of the same type on the device". For per-character data the page advises putting a
  character name or tracking ID in the key. So hashing the display name into the key
  (what the plugin does now) matches the advice; whether a hash still counts as a
  "hashed identifier" to declare: the example lists it as such, so declare it.
- Beta and live are separate: "Records are not shared between beta and live game
  clients."
- Types: BOOL, INT, FLOAT, STRING, STRUCTURED_DATA (Lua tables).
- Functions: Get/Set (typed variants), CheckExists, IterateEntries, Delete, Clear
  ("You may want to prompt the user before deleting data in this manner.").
- Where on disk: **not documented** (seen in the Beta: plugins/PluginData.db).
- Size or entry limits: **not documented** (seen in the Beta: writes failed after
  about 700 small entries; one table per character works).
- Retention, deletion on uninstall: **not documented**.

## 4. Sending data off the PC, sharing between players
Sources: guidelines.html, process.html
- HTTP needs the `httpAccess` permission and base URLs in the manifest; any plugin
  requesting a permission is "Subject to review". Then Case 2 or 3 applies.
- "Obtaining any information about other players" is subject to review.
- Prohibited: "Plugins cannot export any information about other players (we are
  hoping to revise this rule in the future)."
- Sharing own data between players: **not documented** beyond the above.

## 5. What Slayer Helper has to declare (Case 1)
From SUBMISSION.md (current draft): Case 1; "Game information is not stored between
sessions, but plugin settings are." with a TODO to confirm the "own measurements".
- Settings per character (focus, checkboxes, toggles, window place): fits "plugin
  settings are stored between sessions". Declare the hashed character key as a
  "hashed identifier".
- Kills/h and XP/h per task saved between sessions: this is game information kept
  between sessions. The Case 1 template says game information is NOT stored, so
  either ask Jagex whether derived measurements count as settings, or adapt the
  text to say what is stored locally (never transmitted). **Not documented.**
- Collection-log-derived info: the plugin can read it from the game each time, so
  nothing needs storing. If cached: same question as the measurements.

## Questions for Jagex
1. Do locally stored derived measurements (kills/h, XP/h per task) still fit Case 1
   if the text says they are stored locally and never transmitted?
2. Is a hashed display name as storage key fine, and must it be declared as a
   "hashed identifier"?
3. Any PersistentDB size/entry limit, and is data removed on uninstall?
4. Is a privacy notice required for a Case 1 plugin?
