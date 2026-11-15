# Howson Plus on the server

How to put the whole Howson Plus pack on the dedicated server and on a PC that joins it. It takes two things each time: a Mod Manager profile, and an overlay zip with everything the Mod Manager cannot install.

Scott's server has run Howson Plus since 14 Nov 2026, with a new world. The older base-recipe pack and its steps are in [server install](install-server.md).

## Why a profile is not enough

A Mod Manager profile can only name mods released on ficsit.app. Howson Plus also uses:

| What | Why it is not in the profile | Needed on |
| --- | --- | --- |
| FicsIt-Networks 1.3.0, our own build | The released 1.2.0 does not load in this game version; 1.3.0 is not released yet. Built from the author's development branch with our fixes | Server and every player, the same build |
| Megaprojects Library with the join-crash fix | The author has not released the fix. Two patched library files replace the released ones | Every joining player |
| MAM Enhancer 1.9.2 | The released 1.9.1 cannot start research; the fix is an unmerged pull request | Optional, each player's own PC |
| Ten Satisfactory Plus fixes | Text files read by Satisfactory Plus's own library, not mods ([what they fix](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/dataforge/README.md)) | Server and every player |
| Four settings files | Faster Manual Crafting, Move Tool, Smart! and Infinite Zoop must be set the same everywhere | Server and every player |
| Howson Map Link 2.5.0 | Our own mod for the [World map](world-map.html); it is not released anywhere | Optional, each player's own PC (in the client overlay) |
| Slug egg text | One more text file for Satisfactory Plus's library: the twelve slug eggs show `UNKNOWN_KEY(...)` where their hatching values should be, and this puts one plain sentence there | Optional, each player's own PC (in the client overlay) |

## The files

| For | Profile | Overlay |
| --- | --- | --- |
| The dedicated server (Linux) | [`packs/HowsonPlusServer.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonPlusServer.smmprofile) | `HowsonPlus-server-overlay.zip` |
| A PC that joins (Windows) | [`packs/HowsonPlusClient.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonPlusClient.smmprofile) | `HowsonPlus-client-overlay.zip` |

The overlays are compiled files, so they are not in the repository itself. Scott builds them on his PC with `python3 tools/make_bundles.py`, which writes both zips to the repository's `dist/` folder and an unpacked copy of the server one, with the server profile beside it, to `dist/server-upload/`. If they have been attached to this repository's [releases](https://github.com/scotthowson/SatisfactoryHowson/releases) they can be downloaded there; otherwise ask Scott for the client one. The script also lays out `dist/send-to-friend/`: the client profile, the client overlay and a `READ ME FIRST.txt` with the steps below, numbered in the order they are used. That folder is all a joining player needs. What is inside each, from which build and with which checksum, is in [`packs/custom/MANIFEST.md`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/custom/MANIFEST.md).

Each overlay holds one folder, `FactoryGame`, laid out like the game's own. Installing it means merging that folder over the real one.

## The server

1. Stop the server.
2. In Satisfactory Mod Manager, pick the server in the install dropdown and import `HowsonPlusServer.smmprofile`. Wait until it has finished, then switch the install dropdown back to your own game.
3. Unzip `HowsonPlus-server-overlay.zip` on your PC. Over SFTP, upload the contents of its `FactoryGame` folder into the server's `FactoryGame` folder, merging and replacing. This adds `Mods/GameFeatures/FicsItNetworks`, `Mods/DataForge` and four files in `Configs`.
4. Start the server with a new world: Satisfactory Plus must never be added to an existing one.

Always the profile first, then the overlay. Importing or changing a profile later leaves `FicsItNetworks` and `DataForge` alone (the Mod Manager only removes folders it made itself), but repeat step 3 if in doubt; it does no harm.

## A PC that joins

1. Close the game.
2. In Satisfactory Mod Manager, with your own game in the install dropdown, import `HowsonPlusClient.smmprofile` and wait until it has finished.
3. Unzip `HowsonPlus-client-overlay.zip`. Copy its `FactoryGame` folder over the game's `FactoryGame` folder (Steam: right-click Satisfactory, Manage, Browse local files) and say yes to merging and replacing files.
4. Do not add FicsIt-Networks or MAM Enhancer in the Mod Manager as well: the released versions would overwrite these builds.
5. Start the game and join.

Repeat step 3 after every profile import or change: the Mod Manager puts the released Megaprojects Library files back, and the join crash with them.

Three parts of the overlay are optional and only change your own screen. Delete the folder after step 3 if you would rather not have one; nothing else depends on them:

| Part | Folder to delete |
| --- | --- |
| MAM Enhancer | `FactoryGame/Mods/MAMTips` |
| Howson Map Link (the live map) | `FactoryGame/Mods/HowsonMapLink` |
| Slug egg text | `FactoryGame/Mods/DataForge/SlugEggTooltips` |

**Playing without mods** (another server, an unmodded game): click Mods off at the top left of the Mod Manager first. That has not been tried with the overlay's folders in place. If the game then complains about a missing plugin, move `GameFeatures/FicsItNetworks`, `MAMTips` and `HowsonMapLink` out of `FactoryGame/Mods` while you play unmodded, and repeat step 3 afterwards.

## Scott's PC

Already has all of it, put there piece by piece on 14 and 15 Nov 2026: FicsIt-Networks, MAM Enhancer, the patched Megaprojects Library files, the ten fixes, the settings, Howson Map Link and the slug egg text. The client overlay is built from exactly those files: on 15 Nov 2026 all 100 files in it were compared with Scott's game folder and are the same, the profile file names the same 102 mods as the profile his Mod Manager uses, and every one of the 122 mods that installs (with the libraries they pull in) was at its newest release on ficsit.app, so an import that day gives the same versions.

## The live map (optional)

Howson Map Link is our own read-only mod for the [World map](world-map.html). It is not in any profile and nobody needs it to join.

- **On a PC that plays:** with it, the map on that PC shows where you are in real time, what you have built and what is collected. It answers on that PC only, at `127.0.0.1:8765`. Scott's PC has it, and it is in the client overlay.
- **On the server:** with it, the map gets the exact picture for both players: every collectible, power, and every machine with its state. It listens on TCP port 8765 on the server, so that port has to be given to the server in the panel, and should not be forwarded to the internet. It has not run on the server yet.
- The files, laid out ready to copy with their own steps, are written to `dist/map-link/` on Scott's PC (`server/` for the server, `client/` for a PC).

## Check it worked

- **Server console or log:** `FicsItNetworks: 1.3.0` in the list of loaded mods, and a line `KDataForge: … pack(s), … document(s) applied` with no error naming a file from `Mods/DataForge`. On the server expect 33 packs and 171 documents (one fewer of each than on Scott's PC, because Road Maker is not on the server).
- **Player:** `FicsItNetworks: 1.3.0` in `%LOCALAPPDATA%\FactoryGame\Saved\Logs\FactoryGame.log`, and `KDataForge: 34 pack(s), 172 document(s) applied` (the slug egg text is one pack; 33 without it), plus `MAMTips: 1.9.2` and `HowsonMapLink: 2.5.0` if you kept them. The nine errors that line counts are Satisfactory Plus's own and were there before any of ours.
- **In the game:** under tier 1 in the HUB there is a "Covered Conveyor Belt Mk.1" milestone.

## When something changes

- **A new pack list:** new profile files appear here; import them on the server first, then on each PC, then repeat the overlay step.
- **A new overlay:** a new release appears here; replace the folders on the server and on every PC together.
- **FicsIt-Networks 1.3.0 is released by its author:** delete `Mods/GameFeatures/FicsItNetworks` on the server and on every PC together, then add the released mod to the pack. Our build and the release must never be mixed between server and players.

## Status

- The profiles are checked against ficsit.app for this game build; every mod in the server profile has a Linux server build.
- Scott plays on the dedicated server with the client profile and the client overlay. Seen in his game on 15 Nov 2026 while joined to it: FicsIt-Networks 1.3.0, MAM Enhancer 1.9.2, Howson Map Link 2.5.0 and 34 data packs loaded, three and a half hours into the world.
- **No second PC has joined yet.** What is installed on the server itself was put there by Scott and cannot be checked from this repository. Satisfactory Plus's own page calls multiplayer experimental.
- Built but left out on purpose: a Linux server build of Road Maker (Road Maker stays solo-only), and rebuilt copies of SML, ContentLib and More Sign Spots that are only for faults we have not seen. They are listed in the manifest.
