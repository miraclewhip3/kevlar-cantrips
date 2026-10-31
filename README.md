![Kevlar & Cantrips](logo.svg)

# Kevlar & Cantrips

A co-op dice tactics game for 1 to 4 friends. Each player is one wizard operative with 3 class dice. The squad breaches a cursed corporate tower in the near-future city of Halcyon, one floor per round, for 10 floors. The tone follows Tactical Breach Wizards: wizards in tactical gear, police jargon applied to magic, and dry humor. Keywords follow Slice & Dice. All names and characters are original.

**Play:** https://miraclewhip3.github.io/kevlar-cantrips/

## Vision
*Assembled from the 2026/10/31 design rounds. It hasn't been confirmed as a written statement.*

- **Fantasy:** you and your friends are a squad of wizard cops kicking in doors, one floor at a time.
- **Feeling:** planning a turn together and watching it land. "You ward me, I stun the sniper."
- **Pillars**
  1. **Co-op planning.** Everyone rolls at once, every die lands in real time where the squad can see it, and the squad readies up together.
  2. **One character, grown die by die.** You keep 3 dice all run, improved by die+ upgrades and die equipment.
  3. **Readable at a glance.** Dice show an icon, a number and short keyword tags. Enemy intents show before you act.
  4. **Zero setup.** Room codes, no accounts, no server.
- **Non-goals:** positional tactics, per-floor rule modifiers (cut for now), PvP, long campaigns.
- **When in doubt:** pick what makes the squad talk to each other.

## Contents
- [How to play](#how-to-play)
- [Faces](#faces)
- [Keywords](#keywords)
- [Classes and dice](#classes-and-dice)
- [Between floors](#between-floors)
- [Die equipment](#die-equipment)
- [Player equipment](#player-equipment)
- [Enemies and floors](#enemies-and-floors)
- [Squad scaling](#squad-scaling)
- [Multiplayer](#multiplayer)
- [Saving, audio, dev tools](#saving-audio-dev-tools)
- [Design decisions](#design-decisions)
- [Assumptions made in this prototype](#assumptions-made-in-this-prototype)
- [To review later](#to-review-later)
- [Roadmap to alpha](#roadmap-to-alpha)

## How to play
1. **Squad up.** Play solo, or one player hosts and shares a 4-letter code (up to 4 players). Each player picks a different class (4 classes).
2. **Each turn**, every enemy shows its **intent**: an icon, a number and a target.
3. **Everyone rolls at once.** Click dice to keep them, then reroll the rest (2 rerolls). Keeping all three moves on automatically; **Undo** goes back to rolling while you have rerolls and haven't used anything. Your Reroll, Done rolling, Undo and End turn buttons sit in your own operative card, next to your dice. **Cantrip** faces fire on a random target the moment they land.
4. **Use dice in real time.** Click a die, then its target. It happens right away, and everyone sees HP and ward change. ✦ dice charge as soon as you click them. Abilities (your signature, plus any your gear grants) also fire right away, once per turn each.
5. **End turn.** Unused dice are lost. If you still have unused dice or a usable ability, End turn asks you to confirm first. When the whole squad is ready, turrets fire, then every enemy that's still standing and not stunned acts. Ward lasts until then. Poison ticks at the end of the turn.
6. **Down, not out.** At 0 HP you're down. A Necromedic can revive you; otherwise you're back next floor at 50% HP. The run ends when the whole squad is down.
7. **Between floors** everyone heals half their missing HP and picks an upgrade (see below).
8. **Win** by clearing floor 10, the CEO.

## Faces
| Face | Effect |
|---|---|
| ⚔ Damage N | N damage to one enemy |
| ➹ Pierce N | N damage to one enemy, ignoring its ward |
| ⚡ Arc N | N damage to one enemy, and 1 to each enemy next to it |
| 🛡 Ward N | N ward on any operative until enemies act |
| ✚ Patch N | Heal any standing operative N |
| ◉ Stun | Cancel every intent of one enemy this turn |
| 👁 Foresight | Reroll one enemy's intent |
| ✦ Charge N | N charge for abilities (lasts the floor) |
| ✕ Blank | Nothing |

## Keywords
These come from the Slice & Dice wiki (slice-and-dice.fandom.com, Category:Keywords), adapted to co-op. Built-in pairings on class dice have their own icon (see below), so a die reads at a glance. Keywords added by gear show as small purple symbols at the bottom of a side; they never move the main icon. Hovering lists each keyword on its own line.

| Symbol | Keyword | Effect |
|---|---|---|
| ↔ | Cleave | Also hits the enemies on both sides of the target for the same amount |
| ⊕ | Engage | Double if the target is at full HP |
| ✂ | Cruel | Double if the target is at half HP or less |
| ! | Cantrip | Fires on a random target the moment it lands while rolling; the die can still be used |
| ✧ | Pristine | Double if you're at full HP |
| ▣ | Steel | +1 per point of ward you have |
| ϟ | Charged | +1 per ✦ you have |
| ≈ | Echo | Takes the number of the last die you used this turn |
| ⧗ | Patient | Double if this die wasn't used last turn |
| ↑ | Growth | This face gets +1 each time it's used, for the rest of the floor |
| ◈ | Self-shield | Also gives you that much ward |
| ♥ | Self-heal | Also heals you that much |
| ☠ | Poison | The target takes 1 more damage at the end of every turn this floor (stacks) |
| ✶ | Pain | You take 1 damage when you use it |

### Built-in pairings
| Icon | Name | Face + keyword |
|---|---|---|
| 🪓 | Cleaving Strike | ⚔ + Cleave |
| 💢 | Opening Strike | ⚔ + Engage |
| 🔪 | Cruel Strike | ⚔ + Cruel |
| 🔨 | Steel Strike | ⚔ + Steel |
| 🎯 | Aimed Shot | ⚔ + Patient |
| 🔁 | Echo Shot | ⚔ + Echo |
| 🏹 | Breaching Shot | ➹ + Engage |
| 🔱 | Piercing Spread | ➹ + Cleave |
| 🌩️ | Charged Arc | ⚡ + Charged |
| 💫 | Static Arc | ⚡ + Cantrip |
| ⛓️ | Chain Lightning | ⚡ + Cleave |
| 🪖 | Self Ward | 🛡 + Self-shield |
| 🏰 | Steel Ward | 🛡 + Steel |
| 💠 | Pristine Ward | 🛡 + Pristine |
| 🔆 | Snap Stun | ◉ + Cantrip |
| 🔮 | Flash Vision | 👁 + Cantrip |
| 🌟 | Spark Charge | ✦ + Cantrip |

## Classes and dice
| Class | HP | Dice (base) | Signature |
|---|---|---|---|
| 💥 Breach Mage | 14 | Scattershot ⚔2 CLV, ⚔2, ⚔3, ➹1, ➹2 ENG, ✕ · Breaching Charge ⚔4 ENG, ➹3, ➹2, ⚔1, ✕, ✕ · Kevlar Ward 🛡2, 🛡2, 🛡3, 🛡1, ✦1, ✕ | Door Kick (3✦): 2 piercing to every enemy |
| ⚡ Storm Witch | 11 | Arc Lash ⚡2, ⚡2, ⚡3 CHG, ⚡1 CAN, ✦1, ✕ · Downdraft 🛡2, 🛡1, ⚡1, ◉, ✕, ✕ · Squall ✦2, ✦1 CAN, ⚡2, ⚔2 CRU, 🛡1, ✕ | Thunderhead (4✦): 2 to every enemy |
| 👁 Precog | 10 | Foresight ◉, ◉, 👁, 👁 CAN, ✦1, ✕ · Second Guess 👁, 🛡2, 🛡1, ✦2, ✦1, ✕ · Sidearm ⚔2 PAT, ⚔2, ⚔3, ⚔1, ⚔1 ECH, ✕ | Told You So (3✦): stun the 2 biggest intents |
| 🛡️ Riot Cleric | 16 | Riot Ward 🛡3, 🛡2, 🛡2, 🛡1, ✦1, ✕ · Flashbang ◉, ◉ CAN, ⚔1, ⚔1, 🛡1, ✕ · Censure ⚔3 STL, ⚔2 STL, ⚔2, ✚1, ✦1, ✕ | Riot Line (3✦): 🛡2 on everyone; enemy attacks hit you this turn |

Four classes for now (Necromedic and Drone Hexer were cut). Every die has **two + versions**: one mostly raises numbers, the other leans on keywords (for example Scattershot+ Heavy Load or Wide Spread). Hover any die's name for a quick preview of all six sides; click it to open the full unfolded die and hover each side (click outside to close). Equipped gear is listed only if there is any.

## Between floors
- **After floors 2, 5 and 8:** a die upgrade. A random die that isn't upgraded yet is picked for you, and you choose which of its two + versions it becomes. By floor 9 all three dice are +.
- **After floors 1, 3, 4, 6, 7 and 9:** pick 1 of 3 offers. Two are die equipment and one is player equipment.
- Die equipment: **2 per die**. Installing on a full die asks which piece to replace.
- Player equipment: **2 per operative**. Taking a third asks which to replace.

## Die equipment
24 pieces, three times the old 7. They change faces, add pips, add keywords, or grant a ✦ ability.

| Gear | Kind | Effect on that die |
|---|---|---|
| 🔴 Laser Sight | Pips | ⚔ +1 |
| 🧤 Breaching Gauntlet | Pips | ➹ +1 |
| 🎚️ Tuning Fork | Pips | ⚡ +1 |
| 💉 Med-Gel Cartridge | Pips | ✚ +1 |
| 🧱 Ceramic Plate | Face change | Blanks become 🛡2 |
| 🔋 Battery Pack | Face change | Blanks become ✦1 |
| 🔁 Echo Chamber | Face change | Blanks become ⚔1 Echo |
| 🫧 Riot Foam | Face change | ⚔ becomes 🛡 of the same number +1 |
| ♻️ Conversion Rig | Face change | ✚ becomes ⚔ of the same number, with Cruel |
| 🪚 Serrated Edge | Keyword | ⚔ gains Cruel |
| 🎺 Opening Salvo | Keyword | Number faces gain Engage |
| 🪓 Broadhead Rounds | Keyword | ⚔ and ➹ gain Cleave |
| 🧵 Spellwire | Keyword | Every face gains Cantrip |
| 🪞 Mirror Polish | Keyword | Number faces gain Pristine |
| 🔌 Capacitor | Keyword | Number faces gain Charged |
| 🦺 Kevlar Lining | Keyword | ⚔ and ➹ gain Self-shield |
| 🩸 Leech Coil | Keyword | ⚔ and ⚡ gain Self-heal |
| ⏳ Hourglass | Keyword | Number faces gain Patient |
| 🌱 Bonsai Chip | Keyword | Number faces gain Growth |
| 🧪 Toxin Vial | Keyword | ⚔, ➹ and ⚡ gain Poison |
| 🔮 Glass Rune | Pips + keyword | Doubles every number; faces gain Pain |
| 💳 Taser Spellcard | Ability | Zap (2✦): stun a random enemy |
| 🎇 Flare Rune | Ability | Flare (3✦): 3 to the enemy with the most HP |
| ⚕️ Triage Sigil | Ability | Triage (2✦): heal the most hurt operative 3 |

Order of effects: face changes first, then pips and keywords, then Glass Rune doubling, then Growth.

## Player equipment
Formerly "relics". These belong to the operative, never a die. You can carry 2.

| Equipment | Effect |
|---|---|
| ☕ Thermos of Dark Roast | +1 reroll every turn |
| 🧉 Hip Flask of Ether | Start every floor with 2 ✦ |
| 🪪 Union Card | +5 max HP |
| 🦺 Spare Vest | Start every turn with 🛡1 |
| 📎 Expired Warrant | +1 damage against bosses |
| 💼 Overtime Pay | Each enemy you kill gives you 1 ✦ |
| 📻 Squad Radio | Your 🛡 and ✚ give +1 when used on a teammate |
| 💉 Adrenaline Shot | Once per floor, survive a hit that would down you, at 1 HP |
| 📹 Body Cam | Your signature costs 1 less |
| 🎒 Hex Ammo Pouch | The first damage die you use each turn gets +1 |

## Enemies and floors
Floors no longer have rule modifiers. Each floor has a name and an enemy pool.

| Enemy | HP (base) | Intents |
|---|---|---|
| 👮 Hexsec Guard | 6 | ⚔1–3 on an operative |
| 🛰️ Ward Drone | 4 | 🛡2–3 on an enemy, sometimes ⚔1 |
| 🧟 Riot Necro | 7 | ✚2–3 on the most hurt enemy, or ⚔1–2 |
| 🎯 Sniper Seer | 5 | ⚔3–5 on the lowest-HP operative |
| 🦾 Mag-Boot Heavy | 12 | ⚔2–4, +🛡2 on itself every turn |
| 🐀 Intern Familiar | 2 | ⚔1–2 (summoned) |
| 🧛 Regional Manager Vex (floor 5) | 24 per operative | ⚔3–5, 🛡4, 📎 summon; 1 action per operative |
| 💀 Halcyon Grieve, CEO (floor 10) | 40 per operative | ⚔4–6, 🛡5, 📎, 💥3 to all; +1 action below 50% HP |

Enemy numbers get +1 from floor 4 and +2 from floor 8.

## Squad scaling
| Operatives | Enemies per floor | Enemy HP | Enemy numbers | Boss actions |
|---|---|---|---|---|
| 1 | 2 | ×1.0 | +0 | 1 |
| 2 | 3 (4 on floors 7–9) | ×1.6 | +0 | 2 |
| 3 | 4 (5 on floors 7–9) | ×2.4 | +1 | 3 |
| 4 | 5 (6 on floors 7–9) | ×3.4 | +1 | 4 |

Normal enemy HP also grows 10% per floor, and each extra operative adds one escort on boss floors. Tuned with bot runs: with the 4 classes, a simple bot won 11–24% of runs and reached floor 8–9 on average at every squad size (80 runs each). Real players should do better.

## Multiplayer
- **WebRTC peer-to-peer via PeerJS 1.5.4** (from unpkg). Room ids are `cheezy-kc-<CODE>`.
- **The host is authoritative.** The host runs `act(state, player, action)` for everyone and applies dice in the order they arrive. Guests send actions and draw the state they receive; the RNG seed is stripped first.
- Up to 4 players can join in the lobby. If a guest leaves mid-run, their operative leaves and the rest carry on. If the host leaves, the run ends.
- Strict networks may block direct connections (no TURN relay).

**itch.io:** zip `index.html` on its own, set the project kind to HTML, tick "played in the browser", and use a viewport of about 1150 × 900 or fullscreen.

## Saving, audio, dev tools
- Solo runs **autosave**. Export/Import uses a `KC1:` text string. Saves from before this update (version 1) can't be loaded.
- Procedural WebAudio sound effects and a low synth loop, with 🎵 and 🔊 toggles.
- `?dev` adds these top-bar buttons: **Clear floor**, **+5 ✦**, **Heal** and **Auto-play**. `window.KC` exposes `act`, `botNext`, `newRun` and `addPlayer`.

## Design decisions
- **The user's choices (2026/10/31, round 8):**
  - Up to 2 die equipment per die, and 2 player equipment per operative.
  - Relics were renamed to player equipment.
  - About triple the die equipment, built around Slice & Dice keywords.
  - Whole-die upgrades after floors 2, 5 and 8.
  - No floor modifiers.
  - Dice apply in real time instead of showing "incoming" previews.
- **Co-op rules (round 7):** one operative per player, 3 dice, unique classes, simultaneous rolling, own offers, revive at 50% next floor.
- **Round 9 (user's choices):** dice sit in one row; click a die name to inspect every side; keyword symbols replace the purple counts; tooltips put each keyword on its own line; "Reroll" instead of "Reroll unkept"; two + versions per die with the die picked at random; End turn confirms when dice or abilities are left; 4 classes.
- **Round 10 (user's choices):** auto-continue when all dice are kept, plus Undo; controls inside your own card; phase and hint moved above the combat log; no "kept" label and no Cancel button; unique icons for built-in pairings, with indicators only for gear-added keywords; inspector closes on click-outside and previews on hover.
- **Real-time dice:** there's no resolve step for the squad; the enemy turn happens when everyone is ready. This removed the incoming badges and the resolve order (pillar 3).
- **Cantrip** fires on landing even if you reroll later; it doesn't use up the die (as in Slice & Dice).

## Assumptions made in this prototype
I filled these in; change any of them freely.
- All keyword choices and the 14 adapted keywords. I left out Copycat, Exert, Heavy, Petrify, Sticky, Single-use, Death and Future to keep the first pass readable.
- Both + versions of every die, all 24 die equipment and 10 player equipment, and every number.
- Die sides in the unfolded view have a green frame (my reading of "the sides should be green").
- There's no undo once a die is used.
- Gear offers are random, so a class may be offered gear that doesn't match its faces.
- Abilities can each be cast once per turn.

## To review later
- With 4 players the screen is busy (up to 6 enemies plus 4 operative cards).
- Spellwire (every face gains Cantrip) and Glass Rune may be too strong with some dice.
- Offers could be biased toward gear that fits your faces.
- The old mockup page doesn't show this update.

## Roadmap to alpha
- More keywords (Copycat, Exert, Single-use, Sticky), elites, and a branching floor map.
- Banter lines between operatives at the start of each floor.
- Turn timer, reconnect for dropped guests, spectators.
- An in-game wiki.
