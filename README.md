![Kevlar & Cantrips](logo.svg)

# Kevlar & Cantrips

A co-op dice tactics game for 1 to 4 friends. Each player is one wizard operative with 3 class dice, built up with items as the squad climbs. The squad breaches a cursed corporate tower in the near-future city of Halcyon, one floor per round, for 10 floors. The tone follows Tactical Breach Wizards: wizards in tactical gear, police jargon applied to magic, and dry humor. Keywords follow Slice & Dice. All names and characters are original.

**Play:** https://miraclewhip3.github.io/kevlar-cantrips/ (public copy). Source of truth: `cheezy-games/kevlar-cantrips/`.

## Vision
*Pillars from the user's words (2026/11/01). The full design is in the [design document](DESIGN.md).*

1. **Build options come first.** The game must have good options for builds and a lot of flexibility. Everything else serves this.
2. **Start basic, get really powerful.** You choose a character who starts out basic and ends up really powerful.
3. **A good build barely wins; a broken build thrashes.** A good build can just barely beat the game. Sometimes synergistic equipment makes a really powerful, broken build that thrashes enemies. Both are fun.
4. **A real challenge worth talking about.** The game is hard enough that squads strategize together: what could we have done differently, and what equipment is good for what?

- **Core loop (the user's words):** "The core gameplay loop revolves around modifying and upgrading dice as you go up the tower. Putting equipment on the dice is really key."
- **Fantasy:** a squad of wizard cops kicking in doors, one floor at a time.
- **Non-goals:** PvP and long games. Positional tactics and per-floor rule modifiers are also out for now.

## Contents
- [How to play](#how-to-play)
- [Dice and faces](#dice-and-faces)
- [Keywords](#keywords)
- [Classes and dice](#classes-and-dice)
- [Ability upgrades](#ability-upgrades)
- [Between floors](#between-floors)
- [Items by floor](#items-by-floor)
- [Enemies and floors](#enemies-and-floors)
- [Squad scaling and balance](#squad-scaling-and-balance)
- [Multiplayer and reconnecting](#multiplayer-and-reconnecting)
- [Phones](#phones)
- [Saving, audio, dev tools](#saving-audio-dev-tools)
- [Design decisions](#design-decisions)
- [Assumptions and to review](#assumptions-and-to-review)

## How to play
1. **Squad up.** Play solo, or one player hosts and shares a 4-letter code (up to 4 players). Each player picks a different class. The class screen shows a portrait, a short description and the charge ability; **Details** shows the starting dice.
2. **Each turn**, every enemy shows its **intent**: an icon, a number and a target (with keyword symbols such as ↔ spread or ☠ poison).
3. **Everyone rolls at once.** Tap dice to 🔒 lock them (a padlock badge and gold frame show it; unlocked dice have a dashed outline), then Reroll rolls only the unlocked ones (2 rerolls). Locking all three moves on automatically; **Undo** goes back while you have rerolls. Cantrip faces fire as soon as they land.
4. **Use dice in real time.** Click a die, then its target; it happens right away. ✦ dice charge on click (charge maxes at **4**). Abilities fire once per turn each.
   - Your health bar shows what's coming before your next turn: red stripes for attacks left after your ward, green for poison, and the HP you'll end on (`6/8 → 2`).
   - Enemy health bars stripe the poison due this turn. Pick a die and hover an enemy: its health bar shows the chunk it would lose (striped yellow, like your own bar shows incoming damage), including Cleave and Chain splash and a ✺ if it would be stunned. A tick marks where it enrages or changes phase.
   - Dice show their number as it stands right now, so Charged, Steel, Patient and the like change the pips, which turn gold.
   - Click an enemy's intent die to see every side it can roll (each boss phase separately).
5. **End turn.** It asks first if dice are left. When the whole squad is done, every enemy that isn't stunned acts. Ward lasts until then; poison ticks at the end of the turn.
6. **Down, not out.** At 0 HP you're down and back next floor at 50% HP. The run ends when the whole squad is down.
7. **Between floors** everyone heals half their missing HP and picks an item, or upgrades a die on floors 2, 5 and 8 (which also gives +2 max HP). After floor 5 each operative also picks 1 of 3 upgrades for their class ability. An arrow shows the die turning into either upgrade, and you can change your mind until you press Ready. Then everyone presses **Ready**; the next floor starts when the whole squad is ready.
8. **Win** by clearing floor 10, the CEO.

## Dice and faces
- Every face is one **primary** plus, on starting dice, at most one **keyword**. The primaries are ⚔ damage, 🛡 ward, ✚ heal and ✦ charge (plus ✕ blank).
- **Face strength by position** (a guideline): left strongest, then middle; top, right and bottom about equal; rightmost weakest. Items that say "the left face" follow this layout.
- **Power baseline:** about ⚔3 ⚔2 🛡1 🛡1 🛡1 ✕ (8 pips). Starting dice sit near it, with 1 or 2 keywords each.
- **Pips:** numbers are shown as pips in the bottom-right corner: a tick is 1, a tall bar is 5. Hover (or tap on a phone) for the exact number.
- **Built-in pairings** have their own icon (⚔ + Cleave = three spread rounds, ⚔ + Pierce = an armor-piercing slug). Keywords added by items show as small purple symbols.

## Keywords
| Symbol | Keyword | Effect |
|---|---|---|
| ⟂ | Pierce | Ignores the target's ward |
| ⌁ | Chain | Also deals 1 to each enemy next to the target |
| ↔ | Cleave | Also hits the enemies on both sides with the whole face: Pierce, Poison and Stun apply to each, and Engage, Cruel and Duel are checked per target |
| ☠ | Poison | Adds poison equal to its number; the target takes its poison as damage at the end of every turn this floor (stacks, no cap, works on stunned enemies) |
| ✺ | Stun | Cancels every intent of the target this turn (rare: 2 floor-9 items and the Precog signature) |
| ⊕ | Engage | Double vs a target at full HP |
| ✂ | Cruel | Double vs a target at half HP or less |
| ✧ | Pristine | Double if you're at full HP |
| ✝ | Deathwish | Double if you're at 3 HP or less |
| ♨ | Bloodlust | +1 per damaged enemy |
| ↻ | Rampage | If it kills, the die rerolls and can be used again (once a turn) |
| ✶ | Pain | You take 1 when you use it |
| ▣ | Steel | +1 per point of ward you have |
| ϟ | Charged | +1 per ✦ you have (charge itself maxes at 4) |
| ↑ | Growth | This face gets +1 each use, for the floor |
| ≈ | Echo | Takes the number of the last die you used this turn |
| ⧉ | Copycat | Also gets the keywords of the last face you used this turn |
| ⚇ | Duel | Double vs an enemy targeting you |
| ◎ | Focus | +2 if your last die hit the same enemy |
| ⧗ | Patient | Double if the die wasn't used last turn (never on turn 1 of a floor) |
| ⟳ | Wind-up | Use it to wind up: the die locks on this face and sits out next turn. The turn after, it comes back with triple its number. Sitting out also sets off Patient, for six times the number |
| ⇯ | Exert | +2, but the die is blank next turn |
| ① | Single-use | Blank for the rest of the floor after you use it |
| ⚓ | Sticky | Can't be rerolled once rolled |
| ⏭ | Future | Lands at the start of your next turn, with +1 |
| ! | Cantrip | Fires on a random target the moment it lands while rolling |
| ◈ | Self-shield | Also wards you for its number |
| ♥ | Self-heal | Also heals you for half its number (at least 1) |
| ⇄ | Share | The ward or heal also goes to the lowest-HP teammate |
| ❋ | Cleanse | Removes poison and curses from the target |
| ✿ | Regen | Target heals 1 at the start of each turn this floor (stacks) |

**Enemy keywords:** Spread (also hits the operatives next to the target), Poison (1 damage per turn this floor), Curse (your highest face is blank next turn), Growth (+1 each use), Charged (+1 per turn alive), Enrage (+2 below half HP), Empower (an ally's attacks +1 for the floor), Shatter (damages everyone when killed).

## Classes and dice
Faces are listed **left · middle · top · right · bottom · rightmost**. Each die has two upgrades: the **+** version (same idea, better) and a **role change** (same theme, new job).

| Class | HP | Signature | Dice (base) |
|---|---|---|---|
| Breach Mage | 9 | Door Kick (1✦): 1 Pierce to every enemy | Scattershot ⚔2 Cleave · ⚔2 · ⚔1 · ⚔1 · 🛡1 · ✕ / Breaching Charge ⚔3 Engage · ⚔2 Pierce · ⚔1 · ⚔1 · ✦1 · ✕ / Kevlar Ward 🛡3 · ⚔2 Steel · 🛡1 · 🛡1 · ✦1 · ✕ |
| Storm Witch | 8 | Thunderhead (3✦): 2 to every enemy, +1 for each ✦ left after paying | Arc Lash ⚔2 Chain · ⚔2 Chain · ⚔1 · ⚔1 · ✦1 · ✕ / Downdraft 🛡2 Share · 🛡2 · 🛡1 · ✦1 · 🛡1 · ✕ / Squall ✦2 Cantrip · ✦2 · ⚔1 · ✦1 · ⚔1 · ✕ |
| Precog | 8 | Told You So (3✦): stun the biggest intent | Foresight ⚔3 Future · 🛡2 Future · ⚔1 · 🛡1 · ✦1 · ✕ / Second Guess ⚔2 Copycat · ✦2 · 🛡1 · ⚔1 · ✦1 · ✕ / Sidearm ⚔3 Patient · ⚔2 Wind-up · ⚔1 Echo · ⚔1 · 🛡1 · ✕ |
| Riot Cleric | 10 | Riot Line (2✦): 🛡3 on you; enemies target you this turn | Riot Ward 🛡3 · 🛡2 Share · 🛡1 · 🛡1 · ✚1 · ✕ / Flashbang ⚔2 Cleave · ⚔2 · 🛡1 · ⚔1 · ✦1 · ✕ / Censure ⚔3 Steel · ✚2 · ✚1 · ⚔1 · ✦1 · ✕ |

Role changes: Slug Choke, Thermite Charge, Reactive Plating (Breach); Overcharge, Eye of the Storm, Static Build-up (Storm); Precognition, Double Take, Called Shot (Precog); Bastion, Tear Gas, Absolution (Riot). Full faces are in the design document and in the game's Details and upgrade screens.

## Ability upgrades
After floor 5, on top of the die upgrade, each operative picks 1 of 3 upgrades for their class ability. It lasts the rest of the run.

| Ability | Upgrades |
|---|---|
| Door Kick | Battering Ram: 2 Pierce to every enemy. Cleared Room: also strips all ward from every enemy. Follow Through: your next ⚔ this turn gains Pierce and +2. |
| Riot Line | Shield Wall: also 🛡1 on every teammate. Retribution: each attack that hits you this turn deals 1 back. Hold the Line: 🛡5 instead of 🛡3. |
| Told You So | Saw It Coming: costs 2✦. Called It: also deals damage equal to the stunned enemy's biggest attack. Déjà Vu: also lets you use your last used die again this turn. |
| Thunderhead | Supercell: costs 2✦. Conduit: your ⚔ faces gain Chain this turn. Eye of the Storm: also 🛡2 on every operative. |

**Saving a teammate:** if a teammate's health bar says they'd go down, and your die or ability takes that away, sparks fly off their bar with a three-note chime, and the combat log records it.

## Between floors
- **After floors 2, 5 and 8:** a random die that isn't upgraded yet is picked; you choose its + version or its role change.
- **After floors 1, 3, 4, 6, 7 and 9:** pick 1 of 3 items from that floor's own pool of 7 (items that change at least one of your faces are offered first).
- Each die holds up to **3 items**; installing on a full die asks which to replace. There is no player equipment.
- Item text links its keywords: hover or tap a keyword name to read what it does. Items no longer show as badges on your dice; open a die (tap its name) to see them.
- **Rearranging:** on the between-floors screen, move items to another die (Move → Move here), swap them between full dice (Swap here), or reorder them (↑). Items apply **top to bottom**, so order matters: Tuning Fork above Glass Rune adds 1 before doubling.

## Items by floor
| After floor | Items (tier) |
|---|---|
| 1 Reception | Duct Tape (rightmost blank → 🛡1), Spare Battery (rightmost blank → ✦1), Laser Sight (left +1), Grip Tape (middle +1), Field Dressing (bottom → ✚1), Kevlar Patch (lowest 🛡 +1), Lucky Keychain (top gains Cantrip) |
| 3 Open-Plan Office | Serrated Edge (left Cruel), Opening Salvo (left Engage), Stapler Rounds (middle ⚔ Pierce), Toxin Vial (middle ⚔ Poison), Mirror Polish (left Pristine), Med-Gel Cartridge (✚ +1), Spark Spellcard (Zap 3✦: 2 to the lowest-HP enemy) |
| 4 Server Farm | Tuning Fork (⚔ +1), Broadhead Rounds (left and middle ⚔ Cleave), Capacitor (left Charged), Grounding Coil (Chain hits 2 each side), Leech Coil (left Self-heal), Mainspring (left Wind-up), Hourglass (left Patient), Flare Rune (Flare 3✦: 3 to the highest-HP enemy) |
| 6 Executive Gym | Ceramic Plate (🛡 +1), Echo Chamber (blanks → ⚔2 Echo), Mirror Shard (rightmost copies the middle), Kevlar Lining (⚔ Self-shield), Bonsai Chip (left and middle Growth), Rampage Rounds (left ⚔ Rampage), Triage Sigil (Triage 3✦: heal 3) |
| 7 R&D Ritual Lab | Glass Rune (⚔ doubles; 6+ gain Pain), Overclock Chip (all +1, Exert), Spellwire (left Cantrip), Bloodlust Sigil (⚔ Bloodlust), Duelist's Badge (⚔ Duel), Focus Lens (⚔ Focus), Regen Weave (🛡 Regen) |
| 9 Glass Atrium | Flashbang Pin (middle ⚔ Stun), Neural Taser (Stun Burst 5✦), Twin-Barrel Mod (left Copycat +2), Phoenix Sigil (left Deathwish +1), Singularity Core (left → ⚔8 Single-use), Arcane Amplifier (all +1), Share Link (🛡 and ✚ Share) |

## Enemies and floors
Two new enemies arrive on each regular floor and mix with earlier ones (new ones are twice as likely). HP below is solo, before floor growth (+10% per floor) and squad scaling.

| Floor | New enemies |
|---|---|
| 1 Reception | Hexsec Guard (4 HP, ⚔1-2), Lobby Drone (3, 🛡2 an ally or ⚔1) |
| 2 Mailroom | Mailroom Golem (6, ⚔2 Growth), Paper Imp (2, ⚔1 Poison) |
| 3 Open-Plan Office | Middle Manager (5, ⚔2 or Empower an ally), Cubicle Ghoul (4, ⚔1 Spread) |
| 4 Server Farm | Server Wraith (5, ⚔2 Charged), Firewall Drone (6, 🛡3 all allies or ⚔1) |
| 5 | **Regional Manager Vex** (13 per operative): ⚔3, 🛡3, summons Interns; below half: Enrage, ⚔2 Spread |
| 6 Executive Gym | Gym Golem (8, ⚔3, Enrage), Riot Necro (6, ✚3 an ally or ⚔2) |
| 7 R&D Ritual Lab | Ritual Acolyte (5, Curse or ⚔2), Hex Construct (9, ⚔2 Spread Growth) |
| 8 Legal Department | Paralegal Specter (6, ⚔1 Poison or Curse), Litigation Golem (12, ⚔4, +🛡2 each turn) |
| 9 Glass Atrium | Sniper Seer (6, ⚔5 at the lowest HP), Glass Elemental (7, ⚔3 Spread, shatters for 2) |
| 10 | **Halcyon Grieve, CEO** (24 per operative): ⚔4, 🛡4; below 2/3 curses everyone; below 1/3 2 damage to all and Growth |

## Squad scaling and balance
| Operatives | Enemies per floor | Enemy HP | Boss actions |
|---|---|---|---|
| 1 | 2 | ×0.9 | 1 |
| 2 | 3 (4 on floors 7-9) | ×1.5 | 2 |
| 3 | 4 (5 on floors 7-9) | ×2.4 | 2 |
| 4 | 5 (6 on floors 7-9) | ×3.2 | 3 |

Each extra operative adds one boss escort. Enemy HP also grows 11% per floor, and enemy attacks get +1 on floors 8-10. Measured with 150 bot runs per setup (2026/11/01, `tests/bots.js`). Wins for squads of 1, 2, 3 and 4: no plan 38/27/33/39%, a sensible build 41/33/46/51%, a lucky stacked build 51/62/68/71%. These bots don't really exploit combos, so human broken builds should do better. Floor 8 is now the biggest run-ender. Solo Precog and Riot still lose too often on floor 2 (21% and 14% of runs).

## Multiplayer and reconnecting
- **Names:** every player starts with a random callsign from a list of 25 (🎲 next to the name box picks another). Names show on every card. The host keeps names unique by adding a number (Static, Static 2).
- **WebRTC peer-to-peer via PeerJS 1.5.4.** Room ids are `cheezy-kc-<CODE>`. The host runs the rules; guests send actions and draw the state.
- **Phones losing focus no longer kick you out.** Each browser tab keeps a token. If a guest's connection drops (switching apps, locking the screen), the host marks them **away**: their turns are skipped and floor rewards are auto-picked, but their operative stays. The guest's page keeps retrying for about 2 minutes and reconnects automatically when it comes back to the front; they reclaim their seat and can still use that turn's dice.
- **Leave** (the button) still removes you for good. If the host's tab closes, the run ends; a host that briefly loses the broker reconnects by itself.
- Strict networks may block direct connections (no TURN relay).

**Deploy:** `./deploy-itch.sh` rebuilds `dist/kevlar-cantrips-itch.zip` and pushes it to `miraclewhip3/kevlar-and-cantrips:html` with butler. The 630×500 cover is `dist/cover-630x500.png`.

## Phones
- One column, bigger dice and buttons, the combat log collapsed by default (tap "Combat log" to open), and a compact top bar.
- Tap any face, badge or label to read its tooltip (there's no hover on phones). Tap a die's name to inspect all six sides.
- Hover a hero (tap on a phone) to light up the enemies attacking them and their intent dice. An enemy's target is also in its intent die's tooltip.
- Animations: hits flash a slash and shake the target, the attacker lunges, wards pop a shield, kills and downed operatives show a skull and fade to grey. When a floor ends, the battle stays on screen about 2.5 seconds under the banner before moving on.
- A compact layout after Slice & Dice is mocked up in [mockups-compact-layout.html](mockups-compact-layout.html): heroes as slim bars on the left, enemies on the right, your dice in the middle tray, buttons along the bottom.
- On a phone, your operative is always the top card in the squad, with teammates below. A sideways (landscape) layout is mocked up in [mockups-mobile-landscape.html](mockups-mobile-landscape.html): squad on the left, enemies on the right.

## Saving, audio, dev tools
- Solo runs **autosave**. Export/Import uses a `KC1:` text string. Saves from before the first-draft update can't be loaded.
- Procedural WebAudio: a distinct sound per event and a low synth loop, with 🎵 and 🔊 toggles. `?mute` silences everything.
- **Animations:** events replay in order (hits shake, heals and wards glow, kills pop, enemies lunge), and banners announce each floor.
- `?dev` adds **Clear floor**, **+5 ✦**, **Heal** and **Auto-play**. `window.KC` exposes `act`, `botNext`, `newRun`, `addPlayer`, `ITEMS` and `ENEMIES`.

## Design decisions
- **First draft (2026/11/01, from the user):** primaries are charge, damage, ward and heal; Pierce, Chain and Stun are keywords; Stun is rare; Foresight is cut; per-floor item pools of 7; 3 items per die; no player equipment; much weaker starting operatives; more keywords and enemies; enemy keywords; random die upgrades with a + and a role change; no caps on Poison or Charged; Patient never on turn 1; phone layout; reconnecting after focus loss.
- **Earlier:** co-op 1-4, one operative with 3 dice, real-time dice, no floor modifiers, Tactical Breach Wizards tone, hand-drawn SVG art.

## Assumptions and to review
- All dice, items, enemies and numbers come from the draft design document and still need the user's review.
- Boss numbers were lowered from the draft (Vex 20 → 13, Grieve 36 → 24 per operative, fewer boss actions in big squads) so runs don't stall on floor 5.
- Storm Witch and Precog are weaker than the other two classes in solo bot play; the bot underplays Future, Copycat and Echo.
- Floor 7 (Ritual Acolyte curses and Hex Construct spread) is the biggest difficulty spike.
