# Client install: joining the server

About fifteen minutes, most of it download time. Works the same on Windows and Linux.

## What you need

- Satisfactory on Steam or Epic, on the normal branch (not Experimental), at build 517554 (patch 1.2.5.0).
- The file [`packs/HowsonServerClient.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonServerClient.smmprofile) from this repo.
- The server address from Scott. The port is 7788.

## Steps

1. **Install Satisfactory Mod Manager.** Get it from <https://smm.ficsit.app>. On Windows, if the browser says the file is not commonly downloaded, choose Keep. On Linux it is an AppImage: mark it executable and run it.
2. **Open it.** It finds your game by itself. If you have more than one install, pick the right one in the install dropdown. If you have also added the server there (Scott has), make sure the dropdown shows your game and not the `sftp://` address: a profile is installed on whichever install is showing.
3. **Import the pack.** Next to the Profile dropdown, choose Import, pick `HowsonServerClient.smmprofile`, give it a name if the name box is empty, and confirm.
4. **Wait.** It downloads 87 mods plus the libraries they need. Do not start the game until it has finished.
5. **Check the profile.** The Profile dropdown should show the imported profile, and the switch at the top left should say mods are on.
6. **Start the game**, from the Mod Manager, Steam or Epic; the mods load either way. The main menu shows the mod loader under the game version, and a Mods entry.
7. **Join.** Main menu, Server Manager, Add Server, then the address and port 7788.

## Rules that keep it working

- **Do not update mods yourself.** Everyone must have the same versions as the server. When the pack changes you will get a new profile file: import it again.
- **Game updates.** If Steam updates the game and the server has not been updated yet, you cannot join until it has. Tell Scott.
- **Playing without mods.** Click Mods off at the top left of the Mod Manager before joining any unmodded game or server, and turn them back on for this one.

## If something is wrong

| What you see | Do this |
| --- | --- |
| Import stops with "installing Snappy Build Menu ... is forbidden, version solving failed" | The install dropdown is showing the server. Seven mods in this pack exist for players only, so the pack cannot go on a server. Pick your game in the install dropdown, then choose the profile again |
| The join fails or you are kicked straight away | Your mods differ from the server's. Import the newest profile file from this repo again |
| The game will not start after a game update | The mod loader has not caught up with the new game build. Wait for a new pack |
| Low frame rate | Pause Taj's Graphical Overhaul in the Mod Manager (the play button on its row). It only changes your own picture, so the server does not care |
| A mod looks wrong or missing in the build menu | Say which piece. Do not remove the mod yourself: that breaks the match with the server |

The seven mods you may pause freely are listed at the bottom of the [mod list](mod-list.md). All others must stay on.

## Mod settings that must match the server

One mod has a setting we have changed, and it has to be the same on the server and on every PC.

- **Faster Manual Crafting** is capped at 8 times normal speed, building up slowly (Scott's setting of 14 Nov 2026), so that hand crafting never replaces a factory. The file is [`packs/configs/FasterManualCraftingRedux.cfg`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/configs/FasterManualCraftingRedux.cfg).
- Close the game, then copy that file into the game's `FactoryGame/Configs` folder, replacing the one there. On Steam that folder is inside `steamapps/common/Satisfactory`.
- Why, and what else to leave alone, is in [Keeping the pace](pacing.md).

