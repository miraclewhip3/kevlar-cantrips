![Kevlar & Cantrips](logo.svg)

# Kevlar & Cantrips

A co-op dice tactics game for 1 to 3 friends (solo runs all 3 operatives). Each player is one wizard operative with 2 class dice, built up with items as the squad climbs. The squad breaches a cursed corporate tower in the near-future city of Halcyon, one floor per round, for 10 floors. The tone follows Tactical Breach Wizards: wizards in tactical gear, police jargon applied to magic, and dry humor. Keywords follow Slice & Dice. All names and characters are original.

**Play:** https://miraclewhip3.github.io/kevlar-cantrips/ (public copy). Source of truth: `cheezy-games/kevlar-cantrips/`.

**Visual guide:** https://miraclewhip3.github.io/kevlar-cantrips/guide.html — every class, die, keyword, item and enemy drawn with the game's own art. Best place to review content. Rebuild it after changes with `python -X utf8 tests/build-guide.py`.

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
1. **Squad up.** Play solo and pick all 3 operatives, or one player hosts and shares a 4-letter code (2 or 3 players; with 2, the Field Intern AI takes the third seat). Each operative is a different class. **Details** on the class screen shows its dice.
2. **Each turn**, every enemy shows its **intent**: an icon, a number and a target (with keyword symbols such as ↔ spread or ☠ poison).
3. **Roll in the middle.** All the dice you control roll in the middle of the screen. Tap a die to lock it: it moves to its slot beside its hero on the left. Reroll rolls whatever is still in the middle (2 rerolls). Tap a locked die to send it back. Once every die is locked, or rerolls run out, you start using them. **Undo** goes back while you have rerolls. Cantrip faces fire as soon as they land.
4. **Use dice in real time.** Click a die beside a hero, then its target; it happens right away. ✦ dice charge on click (charge maxes at **4**). Abilities are on each hero's card and fire once per turn each.
   - Your health bar shows what's coming before your next turn: red stripes for attacks left after your ward, green for poison, and the HP you'll end on (`6/8 → 2`).
   - Enemy health bars stripe the poison due this turn. Pick a die and hover an enemy: its health bar shows the chunk it would lose (striped yellow, like your own bar shows incoming damage), including Scatter and Chain splash and a ✺ if it would be stunned. A tick marks where it enrages or changes phase.
   - Dice show their number as it stands right now, so Charged, Plated, Patient and the like change the pips, which turn gold.
   - Click an enemy's intent die to see every side it can roll (each boss phase separately).
5. **End turn.** It asks first if dice are left. Solo, one press ends the turn for all 3. When the whole squad is done, every enemy that isn't stunned acts. Ward lasts until then; poison ticks at the end of the turn. If a fight reaches turn 11, the building locks down: enemy attacks get +1 every turn, so no fight can stall forever.
6. **Down, not out.** At 0 HP you're down and back next floor at 50% HP. The run ends when the whole squad is down.
7. **Between floors** everyone heals half their missing HP and picks an item, or upgrades a die on floors 2, 5 and 8 (which also gives +2 max HP). After floor 5 each operative also picks 1 of 3 upgrades for their class ability. An arrow shows the die turning into either upgrade, and you can change your mind until you press Ready. Then everyone presses **Ready**; the next floor starts when the whole squad is ready.
8. **Win** by clearing floor 10, the CEO.

## Dice and faces
- Every face is one **primary** plus, on starting dice, at most one **keyword**. The primaries are ⚔ damage, 🛡 ward, ✚ heal and ✦ charge (plus ✕ blank).
- **Face strength by position** (a guideline): left strongest, then middle; top, right and bottom about equal; rightmost weakest. Items that say "the left face" follow this layout.
- **Power baseline:** about ⚔3 ⚔2 🛡1 🛡1 🛡1 ✕ (8 pips). Starting dice sit near it, with 1 or 2 keywords each.
- **Pips:** numbers are shown as pips in the bottom-right corner: a tick is 1, a tall bar is 5. Hover (or tap on a phone) for the exact number.
- **Built-in pairings** have their own icon (⚔ + Scatter = three spread rounds, ⚔ + Pierce = an armor-piercing slug). Keywords added by items show as small purple symbols.

## Keywords

Keywords come from Slice & Dice, with our own twist. **"The last die" means the last die anyone in the party used this turn**, so Pair, Trio, Inspired, Focus, Echo and Copycat all work across the squad. Cantrips don't count. A small marker in the middle of the screen shows the last die.

| Symbol | Keyword | Effect |
| --- | --- | --- |
| ♨ | Bloodlust | +1 for each damaged enemy. |
| ⇈ | Boost | The target also gets +N to all its faces this turn. |
| ! | Cantrip | Fires on a random target the moment it lands while rolling. You can still use the die afterward. |
| ⌁ | Chain | Also deals 1 to each enemy next to the target. |
| ϟ | Charged | +1 for each ✦ charge you have. |
| ❋ | Cleanse | Removes poison and curses from the target. |
| ⌬ | Comms | +1 for each teammate who has used a die this turn. |
| ⧉ | Copycat | Also gets the keywords of the last face anyone in the party used this turn. |
| ⛨ | Cover | The target also takes half from the next attack that hits it. |
| ✂ | Cruel | Double if the target is at half HP or less. |
| ✝ | Deathwish | Double if you are at 3 HP or less. |
| ② | Double Use | You can use this face twice in a turn. |
| ≈ | Echo | Its number becomes the number of the last die anyone in the party used this turn. |
| ⊕ | Engage | Double if the target is at full HP. |
| ⌛ | Era | +1 for each turn that has passed this floor. |
| ⇯ | Exert | +2, but this die is blank next turn. |
| ☗ | Flesh | +1 for each HP you have. |
| ◎ | Focus | Double if the last die anyone in the party used this turn had the same target. |
| ⏭ | Future | Lands at the start of your next turn, with +1. |
| ↑ | Growth | This face gets +1 every time it is used, for the rest of the floor. |
| ⛰ | Heavy | Must target the enemy with the most HP. |
| ⤴ | Inspired | Double if the last die anyone in the party used this turn had a higher number. |
| ✴ | Overcast | Spends all your ✦ for +2 each. |
| ✶ | Pain | You take 1 damage when you use it. |
| ⚁ | Pair | Double if its number matches the last die anyone in the party used this turn. |
| ⧗ | Patient | Double if this die was not used last turn (never on turn 1 of a floor). |
| ⟂ | Pierce | Ignores the target's ward. |
| ▣ | Plated | +1 for each point of ward you have. |
| ☠ | Poison | Adds poison equal to its number. A poisoned target takes damage equal to its poison at the end of every turn this floor; more poison stacks on top. Works on stunned enemies too. |
| ✧ | Pristine | Double if you are at full HP. |
| ↻ | Rampage | If it kills, this die rerolls and can be used again (once a turn). |
| ⌖ | Ranged | Can target enemies in the back row. |
| ✿ | Regen | The target heals 1 at the start of each turn this floor (stacks). |
| ⟲ | Reload | Also brings back this die's spent Single-use faces. |
| ⚇ | Return Fire | Double against an enemy that is targeting you. |
| ↯ | Ricochet | Also hits a random other enemy for half. |
| ↔ | Scatter | Also hits the enemies on both sides of the target with the whole face: Pierce, Poison and Stun apply to each one too. |
| ♥ | Self-heal | Also heals you by its number. |
| ◈ | Self-shield | Also gives you ward equal to its number. |
| ⇄ | Share | The ward or heal also goes to the lowest-HP teammate. |
| ∅ | Silenced | Doesn't set off Reactive enemies. |
| ① | Single-use | After you use it, this face is blank for the rest of the floor. |
| ⚓ | Sticky | Once rolled, this face can't be rerolled. |
| ✺ | Stun | Cancels every intent of the target this turn. |
| ⤓ | Suppress | The target's attacks also get -N this turn. |
| ➶ | Tracer | The target also takes +N from each hit for the rest of this turn. |
| ⚂ | Trio | Triple if its number matches the last two dice anyone in the party used this turn. |
| ✟ | Vigil | +2 for each downed teammate. |
| ❤ | Vitality | The target also gets +N empty max HP this floor. |
| ⟳ | Wind-up | Use it to wind up: the die locks on this face and sits out next turn. The turn after, it comes back with triple its number. Sitting out also sets off Patient. |

**Enemy attack keywords:** Spread (also hits the operatives next to the target), Poison, Growth, Charged, Heavy (targets the most HP), Eliminate (targets the least HP), Weaken (faces -1 next turn), Jam (turns one face blank for the floor), Backlash (dice deal 1 Pain next turn), Curse (highest face is blank next turn), Empower (an ally's attacks +1 for the floor).

**Enemy traits:** Back row, Kevlar (-1 per hit), Reactive (hits back), Brittle (a 4+ hit kills it), Volatile (explodes on nearby enemies), Contractor (leaves if alone), Courier (flees after a turn; kill it for a 5-item pick), Leader (all enemies +1), Splits, Enrages, Shatters.

## Classes and dice

Faces are listed **Left · Middle · Top · Right · Bottom · Rightmost**. Each class has 2 dice, and each die has 2 upgrades.

### Breach Mage

HP 6 · Piercing burst. Door-kicker in ceramic plate. Hex rounds that punch straight through enemy wards.

**Ability: Door Kick (1✦).** 1 Pierce damage to every enemy.

| Die | Faces |
| --- | --- |
| Scattershot | ⚔2 Scatter · ⚔1 Scatter · ⚔1 · 🛡1 · ⚔1 · ✕ |
| → Scattershot+ | ⚔3 Scatter · ⚔2 Scatter · ⚔2 · 🛡1 · ⚔2 · ⚔1 |
| → Slug Choke | ⚔4 Pierce · ⚔3 Pierce · ⚔2 · 🛡1 · ⚔2 · ✕ |
| Breaching Charge | ⚔3 Engage · ⚔2 Pierce · ⚔1 · ✦1 · ⚔1 · ✕ |
| → Breaching Charge+ | ⚔4 Engage · ⚔3 Pierce · ⚔2 · ✦1 · ⚔2 · ⚔1 |
| → Thermite Charge | ⚔2 Poison · ⚔2 Poison · ⚔1 Pierce · ✦1 · ⚔1 Pierce · ⚔1 |

### Storm Witch

HP 5 · Chain damage. Ex-Navy weather witch. Lightning that jumps from target to target.

**Ability: Thunderhead (3✦).** 2 damage to every enemy, +1 for each ✦ you still have after paying.

| Die | Faces |
| --- | --- |
| Arc Lash | ⚔2 Chain · ⚔2 Chain · ⚔1 · ✦1 · ⚔1 · ✕ |
| → Arc Lash+ | ⚔3 Chain · ⚔2 Chain · ⚔2 Chain · ✦1 · ⚔2 Chain · ⚔1 |
| → Overcharge | ⚔3 Charged · ⚔2 Charged · ⚔1 · ✦2 · ⚔1 · ✦1 |
| Squall | ✦2 Cantrip · ✦2 · 🛡1 · ✦1 · 🛡1 · ✕ |
| → Squall+ | ✦3 Cantrip · ✦2 Cantrip · 🛡2 · ✦1 · 🛡2 · ✦1 |
| → Static Build-up | ⚔2 Charged · ✦2 Cantrip · ✦1 · ⚔1 Charged · ✦1 · ⚔1 |

### Precog

HP 5 · Combo and setup. Sees the next five seconds. Sets up hits for next turn and copies what just worked.

**Ability: Told You So (3✦).** Stun the enemy with the biggest intent.

| Die | Faces |
| --- | --- |
| Foresight | ⚔3 Future · 🛡2 Future · ⚔1 Copycat · ✦1 · ⚔1 Copycat · ✕ |
| → Foresight+ | ⚔4 Future · 🛡3 Future · ⚔2 Copycat · ✦1 · ⚔2 Copycat · ⚔1 |
| → Precognition | ⚔2 Copycat · ⚔2 Future · 🛡2 Future · ✦1 Cantrip · 🛡2 Future · ⚔1 |
| Sidearm | ⚔3 Patient · ⚔2 Wind-up · ⚔1 Echo · 🛡1 · ⚔1 Echo · ✕ |
| → Sidearm+ | ⚔4 Patient · ⚔3 Wind-up · ⚔2 Echo · 🛡1 · ⚔2 Echo · ⚔1 |
| → Called Shot | ⚔3 Focus · ⚔3 Patient Wind-up · ⚔2 Focus · 🛡1 · ⚔2 Focus · ⚔1 Echo |

### Riot Cleric

HP 7 · Wards, heals, taunt. Shield-first riot chaplain. Wards the squad, patches wounds and pulls enemy fire onto herself.

**Ability: Riot Line (2✦).** 🛡3 on you, and every enemy attack this turn hits you instead.

| Die | Faces |
| --- | --- |
| Riot Ward | 🛡3 · 🛡2 Share · 🛡1 · ✚1 · 🛡1 · ✕ |
| → Riot Ward+ | 🛡4 · 🛡2 Share · 🛡2 Share · ✚1 · 🛡2 Share · 🛡1 |
| → Bastion | 🛡2 Share · 🛡2 Share · ⚔2 Plated · ✚1 Regen · ⚔2 Plated · 🛡1 |
| Censure | ⚔2 Plated · ✚2 · ⚔1 · ✦1 · ⚔1 · ✕ |
| → Censure+ | ⚔3 Plated · ✚3 · ⚔2 · ✦1 · ⚔2 · ✚1 |
| → Absolution | ✚3 Share · ✚2 Regen · ✚2 · ✦1 · ✚2 · ⚔1 Plated |

### Combat Medic

HP 6 · Heals and revives. Field medic with a hex-charged trauma kit. Keeps everyone standing, then gets them back up.

**Ability: Medevac (3✦).** Bring back a downed operative at 3 HP. If no one is down, heal the most hurt operative 3. Deplete: costs +1 ✦ each time you cast it this floor.

| Die | Faces |
| --- | --- |
| Trauma Kit | ✚3 Vitality · ✚2 · ✚1 Regen · ✦1 · ✚1 Regen · ✕ |
| → Trauma Kit+ | ✚4 Vitality · ✚3 · ✚2 Regen · ✦1 · ✚2 Regen · ✚1 |
| → Field Surgery | ✚2 Share · ✚2 Cleanse · ✚2 Vitality · ✦1 · ✚2 Vitality · ✚1 |
| Stim Pistol | ⚔2 Self-heal · ✚1 Boost · ⚔1 · ✦1 · ⚔1 · ✕ |
| → Stim Pistol+ | ⚔3 Self-heal · ✚2 Boost · ⚔2 · ✦1 · ⚔2 · ⚔1 |
| → Combat Stims | ✚1 Boost · ✚1 Boost · ⚔2 Self-heal · ✦1 · ⚔2 Self-heal · ✚1 |

### Hex Assassin

HP 5 · Poison and finishers. Corporate wetwork, now freelance. Poisons the big ones, finishes the weak ones and is gone before the alarm.

**Ability: Time Bomb (2✦).** Future: at the start of next turn, 4 damage to the enemy with the most HP.

| Die | Faces |
| --- | --- |
| Silenced Pistol | ⚔2 Cruel · ⚔1 Ranged · ⚔1 Poison · 🛡1 Cover · ⚔1 Poison · ✕ |
| → Silenced Pistol+ | ⚔3 Cruel · ⚔2 Ranged · ⚔2 Poison · 🛡1 Cover · ⚔2 Poison · ⚔1 |
| → Wetwork | ⚔3 Ranged Cruel · ⚔2 Silenced · ⚔1 Tracer · 🛡1 Cover · ⚔1 Tracer · ✕ |
| Smoke Hex | 🛡2 Cover · ✦2 · ⚔1 Poison · ✦1 · ⚔1 Poison · ✕ |
| → Smoke Hex+ | 🛡3 Cover · ✦2 · ⚔2 Poison · ✦1 · ⚔2 Poison · ✦1 |
| → Black Bag | ⚔2 Ricochet · ⚔2 Poison · ✦1 · 🛡1 Cover · ✦1 · ⚔1 |

### Dice Runner

HP 6 · Big swings. Runs numbers for the hex underground. One huge face and a lot of nothing, unless the squad sets it up.

**Ability: Double Down (1✦).** Reroll your unused dice. Deplete: costs +1 ✦ each time you cast it this floor.

| Die | Faces |
| --- | --- |
| Hot Hand | ⚔5 · ⚔1 Pair · ⚔1 Pair · ✕ · ⚔1 Pair · ✕ |
| → Hot Hand+ | ⚔7 · ⚔2 Pair · ⚔2 Pair · ✕ · ⚔2 Pair · ⚔1 |
| → Loaded Dice | ⚔4 Double Use · ⚔2 Pair · ⚔2 Trio · ✕ · ⚔2 Trio · ✕ |
| Side Bet | ⚔2 Pair · 🛡2 Pair · ✦1 · ✦1 · ✦1 · ✕ |
| → Side Bet+ | ⚔3 Pair · 🛡3 Pair · ✦2 · ✦1 · ✦2 · ⚔1 |
| → House Money | ⚔2 Trio · ⚔1 Overcast · ✦2 · ✦1 · ✦2 · 🛡2 |

### Field Commander

HP 7 · Buffs the squad. Runs the op over comms with a hex-tapped radio. Hits harder when the squad moves together.

**Ability: Rally (3✦).** Every operative gets +1 to all faces this turn.

| Die | Faces |
| --- | --- |
| Comms Array | 🛡2 Boost · ✚1 Boost · ⚔1 Comms · ✦1 · ⚔1 Comms · ✕ |
| → Comms Array+ | 🛡3 Boost · ✚2 Boost · ⚔2 Comms · ✦1 · ⚔2 Comms · 🛡1 |
| → Battle Net | 🛡1 Boost · 🛡1 Boost · ⚔1 Comms Inspired · ✦2 · ⚔1 Comms Inspired · 🛡1 |
| Service Pistol | ⚔2 Comms · ⚔2 Inspired · 🛡1 · ✦1 · 🛡1 · ✕ |
| → Service Pistol+ | ⚔3 Comms · ⚔3 Inspired · 🛡2 · ✦1 · 🛡2 · ⚔1 |
| → Last Order | ⚔2 Vigil · ⚔3 Heavy · ⚔1 Suppress · ✦1 · ⚔1 Suppress · ⚔1 |

### Field Intern

HP 6 · AI teammate (2-player games). Unpaid, over-caffeinated and somehow still alive. Does exactly what the manual says.

**Ability: Coffee Run (2✦).** Heal every operative 1.

| Die | Faces |
| --- | --- |
| Stapler | ⚔2 · ⚔1 · ⚔1 · 🛡1 · ⚔1 · ✕ |
| → Stapler+ | ⚔3 · ⚔2 · ⚔2 · 🛡1 · ⚔2 · ⚔1 |
| → Nail Gun | ⚔3 Pierce · ⚔2 Pierce · ⚔1 · 🛡1 · ⚔1 · ⚔1 |
| Coffee Cart | ✦2 · ✚2 · ✚1 · 🛡1 · ✚1 · ✕ |
| → Coffee Cart+ | ✦2 · ✚3 · ✚2 · 🛡2 · ✚2 · ✚1 |
| → Double Shot | ✦2 · ✦2 · ✚2 · ✚1 Boost · ✚2 · ⚔1 |

## Ability upgrades

Each player picks 1 of 3 upgrades for their ability after floor 5, and a second one after floor 8 (a field promotion, which also gives +2 max HP).

| Class | Ability | Upgrades |
| --- | --- | --- |
| Breach Mage | Door Kick | **Battering Ram:** 2 Pierce to every enemy instead of 1.<br>**Cleared Room:** Also strips all ward from every enemy.<br>**Follow Through:** Your next ⚔ this turn gains Pierce and +2. |
| Storm Witch | Thunderhead | **Supercell:** Costs 2✦.<br>**Conduit:** Your ⚔ faces gain Chain this turn.<br>**Eye of the Storm:** Also 🛡2 on every operative. |
| Precog | Told You So | **Saw It Coming:** Costs 2✦.<br>**Called It:** Also deals damage equal to the stunned enemy's biggest attack.<br>**Déjà Vu:** Also lets you use your last used die again this turn. |
| Riot Cleric | Riot Line | **Shield Wall:** Also 🛡1 on every teammate.<br>**Retribution:** Each attack that hits you this turn deals 1 back.<br>**Hold the Line:** 🛡5 instead of 🛡3. |
| Combat Medic | Medevac | **Stretcher Team:** Back up at 5 HP, or heal 5.<br>**Surge Capacity:** No longer costs more each cast.<br>**Trauma Bay:** The target also gets 2 Vitality. |
| Hex Assassin | Time Bomb | **Bigger Charge:** 6 damage instead of 4.<br>**Cluster Charge:** Also 1 damage to every other enemy.<br>**Short Fuse:** Goes off right away. |
| Dice Runner | Double Down | **Stacked Deck:** No longer costs more each cast.<br>**High Roller:** You also get +1 to all faces this turn.<br>**Insurance:** Also 🛡2 on you. |
| Field Commander | Rally | **Standing Orders:** Costs 2✦.<br>**Hold Fast:** Also 🛡1 on every operative.<br>**Second Wind:** Also heals every operative 1. |
| Field Intern | Coffee Run | **Espresso:** Heal 2 instead of 1.<br>**Donuts:** Also 🛡1 on every operative.<br>**Crunch Time:** Also 1 damage to every enemy. |

## Between floors

Everyone heals half their missing HP, and downed operatives come back at 50%.

| After floor | You get |
| --- | --- |
| 2 | Die upgrade on a random die: pick 1 of its 2 versions, +2 max HP |
| 5 | Die upgrade on your other die, +2 max HP, and an ability upgrade |
| 8 | Field promotion: a second ability upgrade, +2 max HP |
| 1, 3, 4, 6, 7, 9 | Pick 1 of 3 items for a die (5 items if your squad killed a Courier) |

Move and reorder items freely between floors. Items apply top to bottom. Then everyone presses **Ready**.

## Items by floor

**Rule (2026/11/03): no item says "all faces".** Every item names positions or a condition, so where it goes is the decision. There are 80 items. Class items only appear for their class. The [guide](guide.html) draws which faces each one changes.

### After floor 1 · Reception (21 items)

*Replace a face, small hp, drawbacks, swaps.*

| | Item | Effect |
| --- | --- | --- |
| 🩹 | Duct Tape | The rightmost blank becomes 🛡1. |
| 🔋 | Spare Battery | The rightmost blank becomes ✦1. |
| 💉 | Field Dressing | The bottom face becomes ✚2. |
| 🧷 | Kevlar Patch | The lowest 🛡 face +1. |
| 🔫 | Pistol Grip | The right face +1. |
| 🔴 | Laser Sight | The left face +1, the bottom face -1. |
| 🧤 | Grip Tape | The middle face +1, the top face -1. |
| 🦺 | Vest Insert | +1 max HP. |
| 🛢️ | Surplus Plate | +3 max HP. The middle face becomes blank. |
| 📱 | Burner Phone | Swaps the left and rightmost faces. |
| 🪙 | Coin Flip | Swaps the left and middle faces. |
| 🔄 | Rotary Mag | Rotates the top, left, bottom and right faces clockwise. |
| 🌰 | Hex Seed Round | The left face becomes ⚔2 Growth. |
| 🧯 | Riot Foam | The left face becomes 🛡3. |
| 👝 | First-Aid Pouch | The middle face becomes ✚3. |
| 🎒 | Surplus Kit | The top face becomes ⚔2 and the bottom face becomes 🛡2. |
| 🔪 | Box Cutter | Blanks become ⚔1 Cantrip Pain. |
| 🧂 | Smelling Salts | Blanks become ✚1. |
| 📎 | Office Nailer | The middle row (left, middle, right, rightmost) becomes ⚔1. |
| 💊 | Caffeine Pill | The left face gains Single-use and +2. |
| 🔭 | Glass Scope | The left face becomes ⚔3. -2 max HP. |

### After floor 3 · Open-Plan Office (16 items)

*One keyword on a weaker face, cheap abilities, class items.*

| | Item | Effect |
| --- | --- | --- |
| 🪚 | Serrated Edge | The top face gains Cruel. |
| 🎺 | Opening Salvo | The top face gains Engage. |
| 📌 | Stapler Rounds | The middle ⚔ face gains Pierce. |
| 🧪 | Toxin Vial | The right ⚔ face gains Poison. |
| 🪞 | Mirror Polish | The top face gains Pristine. |
| 🧴 | Med-Gel Cartridge | The top and bottom ✚ faces +1. |
| ⚙️ | Overclock Chip | The left and middle faces +1 and gain Exert. |
| 🔢 | Tally Counter | The right face gains Pair. |
| 🎼 | Metronome | The top face gains Inspired. |
| 🌫️ | Tear Gas Canister | The right ⚔ face gains Suppress. |
| 🎇 | Tracer Rounds | The right ⚔ face gains Tracer. |
| 💳 | Spark Spellcard | Grants Zap (3✦): 2 damage to the lowest-HP enemy. |
| 🩺 | Triage Sigil | Grants Triage (3✦): heal the most hurt operative 3. |
| 🧨 | Door Charge | Breach Mage only. The middle ⚔ face gains Pierce and +1. |
| 🌀 | Déjà Vu Lens | Precog only. The top face gains Echo. |
| 🛡️ | Tactical Shield | Riot Cleric only. The middle face becomes 🛡4. |

### After floor 4 · Server Farm (13 items)

*One keyword on a good face, +3 hp.*

| | Item | Effect |
| --- | --- | --- |
| 🪱 | Leech Coil | The left face gains Self-heal. |
| ⏳ | Hourglass | The left face gains Patient. |
| 🕰️ | Mainspring | The left face gains Wind-up. |
| 🔌 | Capacitor | The left face gains Charged. |
| 🥋 | Kevlar Vest | +3 max HP. |
| 🧱 | Ceramic Plate | The middle column (top, middle, bottom) 🛡 faces +1. |
| 🧥 | Kevlar Lining | The top and bottom ⚔ faces gain Self-shield. |
| 🎆 | Flare Rune | Grants Flare (3✦): 3 damage to the enemy with the most HP. |
| 🧲 | Grounding Coil | Storm Witch only. Chain faces on this die hit 2 enemies on each side. |
| 🚑 | Crash Cart | Combat Medic only. The middle ✚ face gains Share and +1. |
| ➰ | Hex Garrote | Hex Assassin only. The left ⚔ face gains Ranged and Silenced. |
| 🃏 | Marked Card | Dice Runner only. The rightmost blank becomes ⚔5 Single-use. |
| 🎧 | Tactical Headset | Field Commander only. The left face gains Comms and +1. |

### After floor 6 · Executive Gym (11 items)

*A keyword on two faces, passives.*

| | Item | Effect |
| --- | --- | --- |
| 🎚️ | Tuning Fork | The left and middle ⚔ faces +1. |
| 🌱 | Bonsai Chip | The left face gains Growth. |
| 🔁 | Echo Chamber | Blanks become ⚔2 Echo. |
| 🔷 | Mirror Shard | The rightmost face becomes a copy of the middle face. |
| 🐗 | Rampage Rounds | The left ⚔ face gains Rampage. |
| 🔑 | Lucky Keychain | The top face gains Cantrip. |
| 🩸 | Bloodlust Sigil | The left ⚔ face gains Bloodlust. |
| 🔍 | Focus Lens | The left and middle ⚔ faces gain Focus. |
| 🕸️ | Regen Weave | The left 🛡 face gains Regen. |
| 🎖️ | Duelist's Badge | The top and bottom ⚔ faces gain Return Fire. |
| 🪖 | Auto-Plating | At the start of each turn, 🛡1 on you. |

### After floor 7 · R&D Ritual Lab (10 items)

*A keyword on a row or column, strong conditions.*

| | Item | Effect |
| --- | --- | --- |
| 🔮 | Glass Rune | The left ⚔ face doubles and gains Pain. |
| 🧶 | Spellwire | The left face gains Cantrip. |
| 🔗 | Share Link | The left and middle 🛡 and ✚ faces gain Share. |
| 🎱 | Ricochet Rounds | The left and middle ⚔ faces gain Ricochet. |
| 🎯 | Bullseye | The middle column (top, middle, bottom) gains Engage. |
| ⚖️ | Even Odds | Faces with exactly 2 pips get +2. |
| ⏰ | Overtime | The middle face gains Era. |
| 📦 | Three-Round Mag | The top and bottom faces gain Trio. |
| 🔆 | Backup Generator | At the start of each turn, gain 1 ✦. |
| 🪂 | Golden Parachute | +6 max HP. |

### After floor 9 · Glass Atrium (9 items)

*Build-arounds for the final fight.*

| | Item | Effect |
| --- | --- | --- |
| 📍 | Flashbang Pin | The middle ⚔ face gains Stun. |
| ⚡ | Neural Taser | Grants Stun Burst (4✦): stun a random enemy. |
| 🪃 | Twin-Barrel Mod | The left face gains Copycat and +2. |
| 🔥 | Phoenix Sigil | The left face gains Deathwish and +3. |
| 🕳️ | Singularity Core | The left face becomes ⚔8 Single-use. |
| 📡 | Arcane Amplifier | The middle row (left, middle, right, rightmost) +2. The top and bottom faces become blank. |
| 🕯️ | Memorial Patch | The middle row (left, middle, right, rightmost) gains Vigil. |
| 🌶️ | Hot Streak | The left face gains Double Use. |
| 🧬 | Bloodline Serum | The left face gains Flesh. |

## Enemies and floors

Enemies have less HP and hit harder than before, so each fight is about who to kill and who to protect.

**Threat score.** Every enemy has a hidden Threat: √(HP × Offense), where Offense is the average worth of its 6 faces, then multiplied for traits. Scores add up, so a floor's difficulty is just the sum.

**Floor shapes.** Each floor has a Threat budget and picks a shape, never the same one twice in a row: Swarm, Security detail, Heavy hitters, Chain of command, Ambush, Onboarding or Bounty. The name shows in the floor banner. Enemies join the pool on the floor shown and stay in it. Newer enemies are three times as likely.

| Floor | 1 | 2 | 3 | 4 | 6 | 7 | 8 | 9 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Threat budget | 9 | 11 | 14 | 16 | 21 | 24 | 28 | 31 |

### From floor 1 · Reception

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Hexsec Guard | std | 4 | ⚔2, ⚔1 |  |
| Lobby Drone | tiny | 3 | 🛡2, ⚔1 |  |
| Temp Worker | tiny | 2 | ⚔2, ⚔1 |  |
| Night Receptionist | tiny | 3 | ✚2, ⚔1 |  |

### From floor 2 · Mailroom

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Mailroom Golem | big | 7 | ⚔2 Growth |  |
| Paper Imp | tiny | 2 | ⚔2, ⚔1 Poison |  |
| Bike Courier | tiny | 4 | ⚔1, ✕ | Courier |
| Suspicious Package | tiny | 3 | ✕ | Volatile |

### From floor 3 · Open-Plan Office

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Middle Manager | std | 5 | ⚔3, ⚔2, 📈1 |  |
| Cubicle Ghoul | std | 4 | ⚔2 Spread, ⚔2, ⚔1 |  |
| HR Rep | tiny | 3 | ⚔2, ⚔1 Weaken |  |
| Contractor | std | 5 | ⚔3, ⚔2 | Contractor |

### From floor 4 · Server Farm

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Server Wraith | std | 5 | ⚔2 Charged, ⚔1 Charged |  |
| Firewall Drone | std | 6 | 🛡3 All, ⚔2 |  |
| Cable Snake | tiny | 3 | ⚔2 Poison, ⚔1 Poison |  |
| Sysadmin | std | 4 | ⚔3, ⚔2 Jam, ⚔2 | Back row |

### From floor 6 · Executive Gym

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Gym Golem | big | 9 | ⚔4, ⚔3 | Enrages |
| Riot Necro | std | 6 | ✚3, ⚔3 |  |
| Personal Trainer | std | 7 | ⚔3, ⚔2 | Leader |
| Protein Slime | big | 9 | ⚔3 Spread, ⚔2 | Splits |

### From floor 7 · R&D Ritual Lab

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Ritual Acolyte | std | 6 | ⚔4, ⚔3, ⛓ |  |
| Hex Construct | big | 11 | ⚔3 Spread Growth, ⚔2 Spread Growth |  |
| Onboarding Specialist | std | 6 | ⚔3, 📎 | Summons |
| Hex Turret | tiny | 4 | ⚔4, ⚔3 | Back row |

### From floor 8 · Legal Department

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Paralegal Specter | std | 6 | ⚔2 Poison, ⛓ |  |
| Litigation Golem | big | 13 | ⚔5, ⚔4 | +🛡2 each turn |
| Process Server | std | 7 | ⚔4, ⚔3 Backlash, ⚔3 | Reactive |
| Compliance Officer | std | 6 | ⚔6 Heavy, ⚔4 Backlash, ⚔4 | Back row |

### From floor 9 · Glass Atrium

| Enemy | Size | HP | Attacks and actions | Traits |
| --- | --- | ---: | --- | --- |
| Sniper Seer | tiny | 4 | ⚔6, ⚔5, ✕ | Back row, Hits lowest HP |
| Glass Elemental | big | 8 | ⚔4 Spread, ⚔3 Spread | Shatters |
| Mirror Shade | std | 7 | ⚔5 Eliminate, ⚔4 | Reactive, Brittle |
| Executive Protection | big | 12 | ⚔6 Heavy, ⚔5 | Kevlar |

### Summoned only

| Enemy | HP | Attacks |
| --- | ---: | --- |
| Intern Familiar | 2 | ⚔2, ⚔1 |
| Protein Blob | 3 | ⚔2, ⚔1 |

### Bosses

| Boss | Floor | HP |
| --- | ---: | ---: |
| Regional Manager Vex | 5 | 33 |
| Auditor General | 5 | 30 |
| Head of People | 5 | 28 |
| Halcyon Grieve, CEO | 10 | 60 |

## Squad scaling and balance

Every run is 3 operatives. If players leave a multiplayer run, enemy HP scales to 75% or 50%. Enemy HP grows 3% per floor, and floors get harder mainly through their Threat budgets.

**Bot results (300 runs each, 2026/11/03, `tests/bots.js`):**

| Bot | Wins | Most run-ends |
| --- | ---: | --- |
| No plan (takes the first item) | 28% | Floors 7 to 9 |
| Sensible build | 46% | Floor 9 |
| Sees the whole item pool | 23% | Floors 7 and 8 |

Floors 1 to 3 almost never end a run, which matches the goal. **The third bot doesn't show pillar 3 yet:** it should thrash, but it wins less than the sensible bot. It picks items by a simple power score and doesn't play combos, so this measures the bot more than the game. Judge broken builds by playing.

The bots also underplay Pair, Future, Echo and Copycat, so classes built on them (Precog, Dice Runner, Hex Assassin) look weaker in these numbers than they may be.

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
- **Battle layout** (after Slice & Dice, updated 2026/11/03): heroes as slim bars on the left with slots for their locked dice, rolling dice in the middle, enemies as slim bars on the right with their intent dice on the side closest to the squad, buttons along the bottom.
- In multiplayer, your operative is always the top hero, with teammates below. Solo keeps the same order so nothing jumps.
- **Squad of 3:** every run has exactly 3 operatives with 2 dice each. Solo: you run all three, and all 6 dice roll together. Multiplayer is 2 or 3 people; with 2, the **Field Intern** fills the third seat.
- **Field Intern** (AI only, 2-player games): HP 6, plain dice (Stapler, Coffee Cart), and it picks its own items for now.
- Health bar numbers sit in a small dark label so they read over the stripes.

## Saving, audio, dev tools
- Solo runs **autosave**. Export/Import uses a `KC1:` text string. Saves from before the first-draft update can't be loaded.
- Procedural WebAudio: a distinct sound per event and a low synth loop, with 🎵 and 🔊 toggles. `?mute` silences everything.
- **Animations:** events replay in order (hits shake, heals and wards glow, kills pop, enemies lunge), and banners announce each floor.
- `?dev` adds **Clear floor**, **+5 ✦**, **Heal** and **Auto-play**. `window.KC` exposes `act`, `botNext`, `newRun`, `addPlayer`, `ITEMS` and `ENEMIES`.

## Design decisions
- **Revision (2026/11/03, from the user):** roll in the middle and lock to the left; 2 dice per hero with 3 slots each; no "all faces" items; 80 items with 3× at the lowest level; more classes and enemies; lower HP and harder hits; hidden Threat budgets; party-wide last die; rename only keywords that clash. Why it's built this way: [research/revision-proposal.md](research/revision-proposal.md).
- **First draft (2026/11/01, from the user):** primaries are charge, damage, ward and heal; Pierce, Chain and Stun are keywords; Stun is rare; Foresight is cut; per-floor item pools of 7; 3 items per die; no player equipment; much weaker starting operatives; more keywords and enemies; enemy keywords; random die upgrades with a + and a role change; no caps on Poison or Charged; Patient never on turn 1; phone layout; reconnecting after focus loss.
- **Earlier:** co-op 1-4 with 3 dice (now 1-3 with 2 dice), real-time dice, no floor modifiers, Tactical Breach Wizards tone, hand-drawn SVG art.

## Assumptions and to review
- The 4 new classes, new items, new enemies and their names are first drafts for your review.
- Cleave became **Scatter**, Duel became **Return Fire** and Steel became **Plated**. Other name ideas are in [research/revision-proposal.md](research/revision-proposal.md).
- After floor 8, with only 2 dice to upgrade, you get a second ability upgrade and +2 max HP.
- With 6 slots and 6 item floors, nobody has to replace an item. To be judged in a playtest.
- Real multiplayer with the party-wide last die hasn't been tested over a network.

## Planned
- **Tutorial:** add a short first-run tutorial that teaches rolling, locking, rerolling and using dice.
- **Remove the rolling hint** ("Tap a die to lock it: it moves to its hero on the left. Reroll rolls whatever is still in the middle.") once the tutorial covers it.
- **Fierce and Guilt keywords:** add these two Slice & Dice keywords later. They need definitions first: neither is on the wiki, which covers version 2.0.

## Ideas
Not planned, just worth remembering.
- **More mechanics from the research:** Overwatch, Incendiary, Explosive, Blood Magic, Counterspell, Sigil, Hexbolt, Hack and Deploy were proposed but not built. See the [revision proposal](research/revision-proposal.md).
- **Weapon dice and spell dice:** every die is one or the other, and items stay generic. A blank on a weapon die gives your next weapon die +1 (Reload), and a blank on a spell die gives 1 ✦ (Fizzle). Kevlar enemies take 1 less damage per hit from weapon dice, and Warded enemies take 1 less from spell dice and abilities. Considered for the 2026/11/03 revision and not taken forward. The full draft is in the [revision proposal](research/revision-proposal.md#idea-weapon-dice-and-spell-dice-not-going-forward).
