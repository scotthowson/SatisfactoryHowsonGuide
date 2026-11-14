# Server install

The server is a normal Satisfactory dedicated server with the 80-mod server pack put on it by Satisfactory Mod Manager over SFTP. Ours runs on a Pelican panel; the mod steps (5 to 8) are the same on any host that gives you SFTP.

Never copy a client's Mods folder to the server: client builds of mods do not run there. The Mod Manager fetches the server builds itself.

## What you need

- [`server/egg-satisfactory-modded.json`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/server/egg-satisfactory-modded.json), the Pelican egg.
- [`packs/HowsonServer.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonServer.smmprofile), the server pack.
- Satisfactory Mod Manager 3.0.0 or newer on a PC.

## Set up, in order

1. **Import the egg.** Panel, admin area: Eggs, Import, choose `egg-satisfactory-modded.json`. It appears as "Satisfactory (Modded)" and does not overwrite the stock egg.
2. **Create the server** from that egg. Primary allocation: port 7788. Additional allocation: port 8889. Memory 12288 MiB, disk 15 GB or more.
3. **Open the firewall** on the host and the router: 7788 TCP and UDP, 8889 TCP, same numbers inside and out.
4. **Start it once** and wait for the console to say it is running. It prints `Mods installed: 0`. Stop it. The server must be stopped whenever mods are installed or changed.
5. **Add the server to the Mod Manager.** Left panel, under Other: Manage Servers. Choose SFTP and enter the host, port and user name from the server's SFTP details in the panel. Type the password yourself. The address has the form `sftp://user:password@host:port/path/`.
6. **Install the pack.** Pick that server in the game installation dropdown, Import `HowsonServer.smmprofile`, and wait for it to finish. Then switch the installation dropdown back to your own game before touching the Profile dropdown again: choosing a profile installs it on whichever installation is showing, so choosing your own pack with the server still showing changes the server's mods.
7. **Start the server.** The console prints the number of mods installed (the 80, their libraries and the mod loader) and should show no mod loader errors.
8. **Claim it.** In the game, with the client pack on: Server Manager, Add Server, the address and port 7788. Claim the server and set its admin password there.

## What the egg changes from the stock Pelican egg

| | Stock egg | This egg |
| --- | --- | --- |
| Game updates on start | On | Off, so a game update cannot arrive before the mods are ready and stop the mod loader |
| Reliable messaging port | 8888 | 8889, so it can sit beside an unmodded server on the same machine |
| Rotating autosaves | 3 | 5 |
| Console on start | Nothing | Prints how many mods are installed |
| Missing game files | Fixed by the update on every start | Downloads the game itself when the server binary is missing |

## Starting the world

- Mod settings that belong to a save can only be chosen when the world is created, and the in-game server manager cannot set them. With every mod at its defaults, create the world on the server as usual. To change one (for example Lithium's extra Space Elevator parts, which are off by default), create the save in single player with the client pack, then upload it to the server.
- Mods that have a settings file must be set the same on the server and on each player's PC. Change them on a PC first, then copy the file to the server's `FactoryGame/Configs` folder.

## Updating later

1. Game update: set Automatic Game Updates to 1 in the panel, start once, set it back to 0, stop.
2. Mods: in the Mod Manager, update the server first, then each PC, from the new profile files in this repo.
3. Start the server.

## Status

The egg's download-on-start change was tested with stand-in files, not yet on the panel. The 80-mod pack has not been run on the server.

## Mod settings

- Copy [`packs/configs/FasterManualCraftingRedux.cfg`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/configs/FasterManualCraftingRedux.cfg) into the server's `FactoryGame/Configs` folder over SFTP, replacing the one there, and restart the server. It caps hand crafting at 8 times normal speed.
- Every player needs the same file: see the client guide. This step has not been done on the server yet.

