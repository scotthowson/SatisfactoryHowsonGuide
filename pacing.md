# Keeping the pace

The aim is a game that takes as long as it is meant to. Mods should make building nicer, not make the game shorter.

What sets the length of the game is the parts each milestone and each Space Elevator phase asks for. No mod in the pack changes those numbers. These are the mods that can shorten the road to them.

| Mod | What it speeds up | Risk to the pace | What to do |
| --- | --- | --- | --- |
| Faster Manual Crafting | Hand crafting speeds up with every item, to 25 times normal by default | High in the first hours | Capped: `MaxSpeedMultiplier` 4 and `SpeedMultiplier` 0.1. The file is in the repository under `packs/configs`. Hand crafting stays a chore worth automating |
| Industrial Evolution | Upgraded machines with a production multiplier, researched in the MAM. A bigger multiplier costs more to build | High from the mid game | Leave its MAM tree alone until phase 2 is delivered. Never use its `/ie UnlockAll` chat command |
| Refined Power | Wind, water and solar power that burns nothing | Medium | Build the coal station first. Treat wind and solar as a phase 3 reward |
| Megaprojects: Water Dam | Free power, 250 MW from each unfinished dam | Low for us | None of its three sites is near the Rocky Desert |
| Progressive Blueprinters | Small blueprint designers before Tier 4 | Low | They are 1 to 3 foundations across: decorations and small repeats, not factories |
| Smart!, Infinite Zoop, Move Tool, Curve Builder | Faster building. Everything placed costs the normal parts | None on progress | Keep. Infinite Zoop's `CheatMode` stays `false`, as it is now |
| Lithium | Cheaper alternate recipes from Tier 7 | Low | Its extra Space Elevator parts are off by default. Turn them on for a longer end game |

## House rules

1. The world is created with the game's normal settings. Advanced Game Settings stay off on the server.
2. One extra branch at a time, in the order of the [game plan](game-plan.md).
3. Mod settings are the same on the server and on both PCs. Change them on a PC first, then copy the file to the server.
4. No chat commands that unlock things.

## What this rests on

Each mod's own page on ficsit.app and its settings file as installed on the host's PC. Nothing here is measured: nobody has timed a playthrough with this pack.

The hand-crafting cap is set on Scott's PC (13 Nov 2026). It still has to be copied to the server and to every other PC: the install guides say where. At 4 times, hand crafting is still clearly faster than the base game but stops well short of replacing a Constructor.

The base plan relies on hand crafting in one place only: the 50 Rotors for the first Space Elevator phase.

## Blueprints

- The base game unlocks the Blueprint Designer at Tier 4, with the FICSIT Blueprints milestone. Downloaded blueprints wait for that, and for the belts inside them.
- Progressive Blueprinters adds designers 1, 2 and 3 foundations across earlier. Its page says the first asks you to gather a full stack of every basic material, and that saved blueprints will not load back into those three small designers: you build them inside instead.
- Blueprints cost their normal parts each time you place one, so they save clicks, not materials.
- The repository holds 194. Fifteen are picked for the early game. The 179 from ImKibitz's packs were made in the Tier 6 and Tier 9 designers; 87 of them have no belts (roads, platforms, walls, walkways, pipe runs) and most of the rest use Mk.5 or Mk.6 belts.
- See [the blueprints folder](https://github.com/scotthowson/SatisfactoryHowson/tree/main/blueprints) for what is collected and what each needs.
