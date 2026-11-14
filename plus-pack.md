# Howson Plus: the mod pack

Written by `tools/sync.py`; do not edit by hand. Game build 517554.

One pack built round [Satisfactory Plus](satisfactory-plus.html), in three forms cut from one list so they cannot drift apart. It is the pack for the solo world, and the pack the shared server moves to when it is restarted. Until then the server keeps the base-recipe pack in the [mod list](mod-list.md), and the Rocky Desert Works applies to that pack only.

| File | For | Mods |
| --- | --- | --- |
| [`packs/HowsonPlus.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonPlus.smmprofile) | Solo play | 106 |
| [`packs/HowsonPlusServer.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonPlusServer.smmprofile) | The dedicated server | 94 |
| [`packs/HowsonPlusClient.smmprofile`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/HowsonPlusClient.smmprofile) | A PC joining that server | 102 |

## Read this first

- **A new world.** Satisfactory Plus must never be added to a world that was started without it. Solo or server, the pack starts with a fresh save.
- **The server is a trial.** Satisfactory Plus's own page: 'The current public build does not officially support multiplayer or dedicated servers. Multiplayer is experimental until the next major release.' Every part of it has a Linux server build, so the pack installs; whether it plays correctly there is untested.
- **Everything has been checked on paper, nothing in the game.** Every mod is marked as working for this game build, every dependency version fits, every mod on the server has a Linux server build, and nothing in the pack is on the list that Satisfactory Plus refuses to start beside. That is not the same as having played it: the first launch and the checks below are what prove it.

## Installing

1. Close the game. In Satisfactory Mod Manager, make sure the install dropdown shows the right place: your game for the solo or client file, the `sftp://` server for the server file.
2. Import the file next to the Profile dropdown and wait for it to finish.
3. Server: do this with the server stopped, then switch the install dropdown back to your game before touching the Profile dropdown again.
4. Start a new world. The [Satisfactory Plus page](satisfactory-plus.html) is the guide for it.
5. For the server and for anyone joining it there is more than the profile: our own builds of FicsIt-Networks and two fixed mods, the Satisfactory Plus fixes and four settings files come as one overlay zip each. The steps are in [Howson Plus on the server](plus-server.md).

## Settings to make once

- **Shorter Hard Drive Research: 300 seconds.** It is set per save, in the game under Mod Savegame Settings; its own default is 3 seconds. For the server, a save's mod settings can only be chosen when the world is created: make the save in single player with the client pack, set it there, then upload the save.
- **Faster Manual Crafting: step 0.175, at most 8 times normal speed.** The file is [`packs/configs/FasterManualCraftingRedux.cfg`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/configs/FasterManualCraftingRedux.cfg). Copy it into `FactoryGame/Configs` on the server and on every PC, replacing the one there.
- **Universal Swatch Slots:** players joining the server need the same palette file as the server (its page).
- **Smart!: panel position Y 0.35.** At its default the Smart! panel sits under Location and Rotation's readout while you place something. In the game: Mods, Smart!, HUD. Each player sets it on their own PC.

## Satisfactory Plus fixes to copy once

Ten mods in the pack do not fit Satisfactory Plus by themselves (nine have no official patch, and the one for Storage On Belt misses its unlock): Covered Conveyor Belts, four of the five woods of Wood Walls, two Road Maker fence walls and Storage On Belt can never be unlocked, and Architecture + 01, SciFi 01, 2m Walls, Throughput Counter and Limiter, Lights + and Foundations + cost parts that Satisfactory Plus only makes later. The fixes are ten small folders of text files in [`packs/dataforge/`](https://github.com/scotthowson/SatisfactoryHowson/tree/main/packs/dataforge).

1. Close the game (stop the server).
2. In the game folder go to `FactoryGame/Mods` and make a folder named `DataForge`.
3. Copy the ten folders from `packs/dataforge/` into it and start the game.

The server and every PC need the same folders. The Mod Manager leaves them alone. What each one changes, how to check it loaded and how to take it out again is in [`packs/dataforge/README.md`](https://github.com/scotthowson/SatisfactoryHowson/blob/main/packs/dataforge/README.md). Loaded and checked on Scott's PC on 14 Nov 2026; not yet tried on the server.

## Check these in the first hours

These are the places where two mods meet and only the game can say what happens. Tell Claude what you see and the pack gets corrected.

1. The game reaches the main menu with no mod loader error, solo first, then the server's console.
2. In the HUB, every milestone is one of Satisfactory Plus's: no second "Logistics" or "Coal Power" left over from the base game.
3. With the fixes above copied in: Covered Conveyor Mk.1 is a tier 1 milestone and Mk.2 can be unlocked after Logistics Mk. 2; the Wood Walls pieces are all there after Base Building. The wall pipe supports appear in the AWESOME Shop once the game's own Pipeline Wall Attachments are bought there.
4. Snap On: put a Splitter straight onto a Constructor, not onto a Crusher or Sorter (see the warnings).
5. Critical Path (F10) lists Satisfactory Plus's milestone, not a base-game one.
6. A hard drive in the MAM takes five minutes.
7. On the server: your friend can join, place a sign, a Blueprint Designer+ piece and a Modern Railing piece, and see yours.

## Warnings that the mods' own pages give

- **SnapOn:** Snap On, Scott's pick. Its author warns that Splitters and Mergers attached straight to buildings 'could have negative consequences such as random crashes, item duplication, or item loss', more so on buildings with several outputs, which Satisfactory Plus is full of (Crusher, Sorter, Modular Miner). Use it on single-output machines. Its author also says snapped-on Splitters and Mergers will break with the next game patch.
- **Pipe Tuner:** changes how fluids behave; its settings name only Mk.1 and Mk.2 pipes and Satisfactory Plus has three tiers
- **Shorter Hard Drive Research:** only shortens the base game's hard drive scanner; whether Satisfactory Plus still uses that scanner for its alternates is not verified. Set per save in Mod Savegame Settings (300 seconds for Scott's five minutes); the default is 3 seconds.
- **Containers with Screen:** adds four buildables costed in base-game parts; no Satisfactory Plus patch
- **Covered Conveyor Belts:** no patch: Mk.2 to Mk.6 hang on base-game milestones that Satisfactory Plus replaced and may never unlock; check in game
- **Wall Pipe Supports:** no patch: its page ties the unlock to the base game's Coal Generator milestone; check in game
- **Wood Walls (and Roofs):** no patch: some entries hang on a base-game milestone; check in game
- **Road Maker:** solo only; fence walls are tied to milestones by base-game name; check in game
- **Power Checker:** own unlock, cost not patched
- **Faster Manual Crafting Redux:** hand-crafting speed; Scott's own cap is step 0.175, maximum 8
- **Taj's Graphical Overhaul:** last built for an older game; ficsit.app: 'Allegedly works. Author has not tested it.'
- **Snappy Build Menu:** client only
- **Storm Lights:** solo only; not tested in multiplayer by its author
- **Atlas: Buildings on the map:** building and machine settings from the map work in single player and for the host only
- **Megaprojects: Power Domain:** kept on Scott's choice, wireless power links included; a late goal (patched milestone at Tier 4, needs Space Elevator parts)
- **Critical Path:** F10 report of what blocks the current milestone. Its page says modded content is measured, not assumed, but it is untested beside Satisfactory Plus's replaced milestones and custom machines: try it solo first
- **Depot Sorting:** sorts the Dimensional Depot by the base game's tiers; Satisfactory Plus parts will probably fall outside its order
- **Hover Pack Fuse Reminder:** display only
- **Indicator Colors:** display only
- **KModelerExporter:** after the chat command /modeler-generate the game crashed a few minutes later, both times on 14 Nov: save, export, then restart the game

## Not on the server, and why

- **Location and Rotation:** only changes your own screen, so the server does not need it.
- **Outline Loot:** only changes your own screen, so the server does not need it.
- **No Z Fighting:** only changes your own screen, so the server does not need it.
- **Glass Cleaner:** only changes your own screen, so the server does not need it.
- **Snappy Build Menu:** only changes your own screen, so the server does not need it.
- **No Splash / Intro Screens:** only changes your own screen, so the server does not need it.
- **Taj's Graphical Overhaul:** only changes your own screen, so the server does not need it.
- **More Sign Spots:** only changes your own screen, so the server does not need it.
- **Road Maker:** no server build.
- **Storm Lights:** no server build.
- **Custom Hud:** its author marks it untested in multiplayer and likely host only, and a dedicated server has no host.
- **Bottleneck:** its author marks it untested in multiplayer and likely host only, and a dedicated server has no host.

The profile for this PC when it joins the Plus server: the server pack plus the mods that only change this PC's own screen. Each is client-optional: its plugin file says RequiredOnRemote false, or, where it is not installed here to read, its page says so (client_only_says). Road Maker and Storm Lights would be needed on the server but have no Linux server build, and Custom Hud and Bottleneck are host-only by their author's word, so those four stay off while joining.

## Held back for later

Left out on purpose so the start stays calm. Each comes in by adding it in the Mod Manager on the server and on every PC at the same time.

- **Industrial Evolution:** Industrial Evolution, held back on Scott's choice until Satisfactory Plus Tier 6 is running: Mk2 and Mk3 machines (3 and 5 times throughput) and an 18-node research tree that its patch opens from the first hour. Add it together with MkPlusSFPlus.
- **Industrial Evolution SF Plus:** the Satisfactory Plus patch and Mk2/Mk3 Satisfactory Plus machines for Industrial Evolution; comes in with MkPlus
- **Pneumatic Fracking Machine:** same authors as Satisfactory Plus, has a patch: three oil extractors and a new fluid. Offer at Tier 5 (Oil Processing)
- **Locomotives B-Units:** has a patch: one stronger locomotive; its page says multiplayer is untested. Offer when trains arrive (Tier 5)
- **Server Join Race Fix:** a runtime patch for crashes when joining a heavily modded server; new, so only if joining actually crashes

## Built by us, not from ficsit.app

Mods in the pack that the Mod Manager cannot install, because the working version is one we built ourselves with the modding kit in Scott's PC on 14 Nov 2026. They travel in the overlay zips made by tools/make_bundles.py (manifest with checksums: packs/custom/MANIFEST.md), never in a profile. Do not add the released versions of these in the Mod Manager as well.

- **FicsIt-Networks:** 1.3.0, built from the author's development branch (d1a1bf2) with twelve local fixes; the released 1.2.0 is marked 'Broken by the update to Unreal Engine 5.6.1'. Server and every player need this same build. When the author releases 1.3.0, remove this build everywhere first, then add the release to groups.
- **MAM Enhancer:** MAM Enhancer 1.9.2, built from the unmerged pull request Nogg-aholic/MAMTips #11; the released 1.9.1 is marked Broken since game 1.2.4.0. Client side only, optional for each player.
- **Megaprojects Library:** the released 1.2.4 with two library files rebuilt to fix the client crash on join (MegaprojectsLib issue 2). Client side; re-applying a profile in the Mod Manager puts the released files back.
- **Satisfactory Plus fixes:** ten Satisfactory Plus fixes as text packs (packs/dataforge): they unlock 157 recipes that were stuck (Covered Conveyor, Wood Walls, Road Maker fence walls, Storage On Belt) and re-cost six misplaced mods. Server and every player.

How to put them on the server and on a joining PC: [Howson Plus on the server](plus-server.html).

## Every mod

### Overhaul (1)

| Mod | What it does | Where |
| --- | --- | --- |
| [SatisfactoryPlus (SF+/SFP)](https://ficsit.app/mod/SatisfactoryPlus) | Content overhaul and recipe rebalancing for Satisfactory. | Everywhere |

### Build tools (14)

| Mod | What it does | Where |
| --- | --- | --- |
| [Smart!](https://ficsit.app/mod/SmartFoundations) | The Factory Builder's Multitool! Scale up your factory with a number of tools for fast, vanilla-friendly building! | Everywhere |
| [Smart! Camera](https://ficsit.app/mod/SmartCamera) | Companion mod for Smart! Foundations. Picture-in-Picture hologram preview for precise building from multiple angles. | Everywhere |
| [Infinite Zoop](https://ficsit.app/mod/InfiniteZoop) | Upgrade your max Zoop count and Zoop in two dimensions! | Everywhere |
| [Infinite Nudge](https://ficsit.app/mod/InfiniteNudge) | Nudge in smaller increments, scale, and rotate on any axis. Also nudge extractors! | Everywhere |
| [Curve Builder](https://ficsit.app/mod/CurveBuilder) | Now you're zooping with curves! | Everywhere |
| [Blueprint Designer+](https://ficsit.app/mod/KBlueprintDesignPlus) | Extended blueprint designer tools for Satisfactory. | Everywhere |
| [Persistent Paintables](https://ficsit.app/mod/PersistentPaintables) | Customization eyedropper support and optional automatic pipe painting | Everywhere |
| [Longer Beams](https://ficsit.app/mod/LongerBeams) | Build longer beams! | Everywhere |
| [Move Tool](https://ficsit.app/mod/MoveTool) | A tool that allows for moving structures instead of dismantling and rebuilding them | Everywhere |
| [Progressive Blueprinters](https://ficsit.app/mod/ProgressiveBlueprinter) | A set of tiered blueprinting machines that grow with your progress. | Everywhere |
| [Construction Preferences](https://ficsit.app/mod/ConstructionPreferences) | Set a variety of preferences related to construction | Everywhere |
| [Pole Position](https://ficsit.app/mod/StackableDistance) | Snaps the next stackable pole to max belt/pipe/tube reach from the last one and shows that range as a ring. | Everywhere |
| [Road Maker](https://ficsit.app/mod/RoadMaker) | Curved roads with lane lines and markings, intersections, road tools, fences, fence walls and a sign gantry, plus smart snapping | Solo only |
| [SnapOn](https://ficsit.app/mod/DirectToSplitter) | SNAPON, apply directly to the factory. (Attach Splitters, Mergers, and Pipe Junctions directly to factory inputs/outputs) | Everywhere |

### Information (8)

| Mod | What it does | Where |
| --- | --- | --- |
| [Power Checker](https://ficsit.app/mod/PowerChecker) | Check if your fuses can blow! | Everywhere |
| [Throughput Counter and Limiter](https://ficsit.app/mod/CounterLimiter) | Belt attachment that displays the actual item throughput per minute. Can optionally limit the IPM. | Everywhere |
| [MiniMap](https://ficsit.app/mod/MiniMap) | Shows a minimap on your hud | Everywhere |
| [Mod Update Notifier](https://ficsit.app/mod/ModUpdateNotifier) | Get notified in-game when one of your mods has an update available. | Everywhere |
| [Cable Highlighter](https://ficsit.app/mod/Cable_Highlighter) | Use F8 to toggle highlighting of nearby power cables through walls. | Everywhere |
| [KModelerExporter](https://ficsit.app/mod/KModelerExporter) | Exports your modpack production data for the KMods Production Modeler. | Everywhere |
| [Containers with Screen](https://ficsit.app/mod/ContainerWithScreen) | A light version of "Container Screens and more" mod to work on Dedicated Servers. | Everywhere |
| [Critical Path](https://ficsit.app/mod/CriticalPath) | Your factory, explained. What's holding up your objective, which lines are keeping up, and what to build next - in order. | Everywhere |

### HUD and looks of the game (26)

| Mod | What it does | Where |
| --- | --- | --- |
| [Custom Hud](https://ficsit.app/mod/CustomizableHUD) | Hide and show parts of your HUD | Solo only |
| [Speedometer](https://ficsit.app/mod/Velocimeter) | Shows the speed/coords and altitude of your character and have an Odometer. | Everywhere |
| [GameTime](https://ficsit.app/mod/GameTime) | Have the game time, system time and session time clock always on your screen. | Everywhere |
| [Location and Rotation](https://ficsit.app/mod/HologramLocation) | Adds a widget which shows you the location and rotation info for the currently highlighted buildable | Solo and client |
| [Bottleneck](https://ficsit.app/mod/Bottleneck) | A tool to easily see what the machine is doing and how well it is working. | Solo only |
| [Production Stats](https://ficsit.app/mod/Stats) | See production and consumption statistics. | Everywhere |
| [Atlas: Buildings on the map](https://ficsit.app/mod/FactoryAtlas) | See your buildings on the map, and control them! | Everywhere |
| [Miner Status on MAP](https://ficsit.app/mod/StatusMapMarker) | If the extractor/miner is stuck, will show on map as a marker. | Everywhere |
| [All Poles with Indicator Light](https://ficsit.app/mod/AllPolesHaveLights) | Every pole will have an indicator light: White: Ok Red: No Power Yellow: Fuse Triggered. | Everywhere |
| [Auto Signs](https://ficsit.app/mod/AutoSigns) | Automatically sets the text and icon according to the building the sign was placed on | Everywhere |
| [Auto - Sort Inventory](https://ficsit.app/mod/AutoSort) | Auto Sort your inventory when you open it! | Everywhere |
| [Object Scanner Highlighting](https://ficsit.app/mod/HighlightScannedObject) | Highlight the currently scanned object | Everywhere |
| [Show Enemy Health](https://ficsit.app/mod/ShowEnemiesHealth) | The mod show enemies health bar and data. | Everywhere |
| [Flashlight Settings](https://ficsit.app/mod/FlashlightSettings) | Adds a widget that lets you change some settings on your character's flashlight | Everywhere |
| [Outline Loot](https://ficsit.app/mod/OutlineLoot) | Gives loot an outline to make it easier to spot | Solo and client |
| [No Z Fighting](https://ficsit.app/mod/NoZFighting) | Adds miniscule offsets to various architectural pieces to prevent "Z Fighting" | Solo and client |
| [Glass Cleaner](https://ficsit.app/mod/GlassCleaner) | Cleans up glass windows, foundations, and roofs | Solo and client |
| [No Grass Under Buildings](https://ficsit.app/mod/NoGrassUnderBuildings) | Hides grass beneath buildings, stairs, and foundations. Restores it after dismantling. | Everywhere |
| [Snappy Build Menu](https://ficsit.app/mod/SnappyBuildMenu) | Performance improvements for the build menu. Instant search, no stutter, fewer clicks. | Solo and client |
| [No Splash / Intro Screens](https://ficsit.app/mod/NoSplash) | Removes all splash screens from game startup | Solo and client |
| [Taj's Graphical Overhaul](https://ficsit.app/mod/TajsGraph) | Crank up those graphics and make efficiency look sexy! | Solo and client |
| [Storm Lights](https://ficsit.app/mod/StormLights) | Your night only lights come on during storms, heavy rain and fog, and flicker when lightning strikes. | Solo only |
| [More Sign Spots](https://ficsit.app/mod/MoreSignSpots) | Adds more Sign attachment points to vanilla buildings | Solo and client |
| [Indicator Colors](https://ficsit.app/mod/IndicatorColors) | Change the colors of production indicators | Everywhere |
| [Hover Pack Fuse Reminder](https://ficsit.app/mod/HoverpackFuseReminder) | Warns you in the Fuse Box UI when you have a Hover Pack equipped. | Everywhere |
| [Depot Sorting](https://ficsit.app/mod/DepotSorter) | Sort Dimensional Depot entries | Everywhere |

### Walls, floors and structure (18)

| Mod | What it does | Where |
| --- | --- | --- |
| [Structural Solutions](https://ficsit.app/mod/SS_Mod) | Structural Solutions adds 300+ new buildable objects to Satisfactory. | Everywhere |
| [Architecture +](https://ficsit.app/mod/Architecture) | Additional architectural elements | Everywhere |
| [Architecture + 02](https://ficsit.app/mod/Architecture02) | Additional architectural elements - Walls & Windows 4x1 - 4x4 | Everywhere |
| [Architecture + 03](https://ficsit.app/mod/Architecture03) | Additional architectural elements - Oeil-de-Boeuf | Everywhere |
| [Architecture + 04 - Doors](https://ficsit.app/mod/Architecture04) | Additional architectural elements - Doors | Everywhere |
| [Architecture + 05 - Roofs](https://ficsit.app/mod/Architecture05) | Additional architectural elements - Roofs | Everywhere |
| [SciFi 01](https://ficsit.app/mod/SciFi01) | Architectural elements for a futuristic base | Everywhere |
| [Gateways Extension](https://ficsit.app/mod/GatewaysExtension) | Adds gateways types - Catwalks - Walkways | Everywhere |
| [Spiral Stairs](https://ficsit.app/mod/SpiralStairs) | Always climb higher! | Everywhere |
| [More Walls](https://ficsit.app/mod/MoreWalls) | This Mod adds 2 new Wallsets | Everywhere |
| [2m Walls](https://ficsit.app/mod/TwoMeterWalls) | 2m high walls for the extra efficient builder. | Everywhere |
| [Foundations +](https://ficsit.app/mod/FoundationMaterialsPlus) | 15 new colourable foundation styles in three materials over three sizes for you to decorate your factories and more! | Everywhere |
| [Modern Railing Extension](https://ficsit.app/mod/ModernRailingExtension) | Modern railing variants for Satisfactory foundations. | Everywhere |
| [Safe-T-Walkways](https://ficsit.app/mod/SafeTWalkways) | Adds a new version of the T walkway with no railing gap. | Everywhere |
| [Catwalk Ladders](https://ficsit.app/mod/CatwalkLadders) | Adds Catwalk variants with climbable ladders cut through them. | Everywhere |
| [Wood Walls (and Roofs)](https://ficsit.app/mod/WoodWalls) | Adds Wood Walls (and Roofs) in several styles! | Everywhere |
| [Small Roll-Up Gate](https://ficsit.app/mod/SGSmallGarageDoor) | Roll-Up Gate, but smaller! (8x4 m) | Everywhere |
| [Catwalk T Rotation Fix](https://ficsit.app/mod/CatwalkTRotation) | Switches rotation direction of Catwalk T Junctions snapped to catwalks, making it consistent with the rest of the game | Everywhere |

### Decoration, lights and signs (14)

| Mod | What it does | Where |
| --- | --- | --- |
| [Factory Props](https://ficsit.app/mod/Factory_Prop_Mod) | Your Ultimate Decorating Toolkit! | Everywhere |
| [Decor +](https://ficsit.app/mod/DecorPlus) | Ficsit approved furniture and decorations galore | Everywhere |
| [Lights +](https://ficsit.app/mod/LightsPlus) | New lights of all kinds to light up your worlds! Mostly emissives (all colourable), some "fire"! | Everywhere |
| [3D Text](https://ficsit.app/mod/Letters) | All letters and numbers paintable in 3D to put in your factory. Ficsit and Satisfactory logo included. | Everywhere |
| [RSS2 - Really Simple Signs 2](https://ficsit.app/mod/RSS) | Really Simple Signs dynamic sign buildables. | Everywhere |
| [Cable Choices Plus](https://ficsit.app/mod/AB_CableMod) | Add some industrial style or something a little more crazy with these alternate power cables/poles. Alt Ficsmas recipe included! | Everywhere |
| [Universal Swatch Slots](https://ficsit.app/mod/UniversalSwatchSlots) | Create your own palette of swatches or modify existing ones. Share your palettes between different session or even with others. | Everywhere |
| [Painted Metal Roof Material](https://ficsit.app/mod/SGPaintedMetalRoof) | Same shape as vanilla Metal Roof but can be painted like FICSIT Roof | Everywhere |
| [Rough Concrete Wall Material](https://ficsit.app/mod/SGRoughConcreteWallMaterial) | Adds a new wall material that mimics the side texture of a concrete foundation. | Everywhere |
| [Industrial Storage and Props +](https://ficsit.app/mod/IndustrialPropsPlus) | 200+ New Industrial Storage Options & Props galore! 3 & 4 Port Fluid Buffers, 4 New Mk1 & 2 Storage Containers & SO Much More! | Everywhere |
| [Copy Sampled Sign](https://ficsit.app/mod/CopySampledSign) | Copies sign data when sampling a sign and applies it to new signs | Everywhere |
| [This Sign Up](https://ficsit.app/mod/ThisSignUp) | Adds arrows to indicate which way is up when building a sign | Everywhere |
| [Elevator Icon Pack](https://ficsit.app/mod/SGIconPackElevator) | A set of monochrome icons with numbered floors and basements. | Everywhere |
| [Road Sign Icons](https://ficsit.app/mod/RoadSignIcons) | Adds 44 New Icons for Signs! | Everywhere |

### Belts, pipes and lifts (11)

| Mod | What it does | Where |
| --- | --- | --- |
| [Modular Load Balancers](https://ficsit.app/mod/LoadBalancers) | Modular buildable that can be snapped together to form load balancers of any size | Everywhere |
| [Floor Hole Ceiling Logistics](https://ficsit.app/mod/FloorHole) | Pass Conveyors, Pipes, Power and Hypertubes through Foundations and Ceilings. | Everywhere |
| [Conveyor Wall Hole](https://ficsit.app/mod/WallHoleConveyor) | Put a hole in the wall for conveyors wherever you want. | Everywhere |
| [Wall Conveyor Supports](https://ficsit.app/mod/WallConveyorSupports) | Additional variants of the wall conveyor support | Everywhere |
| [Wall Pipe Supports](https://ficsit.app/mod/WallPipeSupports) | Additional variants of the wall pipe support | Everywhere |
| [Covered Conveyor Belts](https://ficsit.app/mod/CoveredConveyor) | A variety of Covered Conveyor Belts Mk1-6! (+ coloured-belt standard conveyors Mk 1-6!) | Everywhere |
| [Glass Fluid Buffer](https://ficsit.app/mod/GlassFluidTank) | Four fluid buffers that you can see the fluids inside. | Everywhere |
| [Linear Motion](https://ficsit.app/mod/LinearMotion) | Elevators and More! | Everywhere |
| [Storage On Belt](https://ficsit.app/mod/StorageOnBelt) | A small storage container that can be snapped to belts | Everywhere |
| [Simple Conveyor Logistics](https://ficsit.app/mod/ConveyorLogistics) | Adds Conveyor Junctions and Weighted Splitters to minimize early-game load balancing infrastructure | Everywhere |
| [Pipe Tuner](https://ficsit.app/mod/PipeTuner) | Tune hidden Pipeline variables to improve fluid dynamics. | Everywhere |

### More to research and build (9)

| Mod | What it does | Where |
| --- | --- | --- |
| [Refined Power](https://ficsit.app/mod/RefinedPower) | A Satisfactory Mod that adds 30+ hand made buildings to produce power! | Everywhere |
| [Ficsit Farming](https://ficsit.app/mod/FicsitFarming) | Get your Fingers Dirty with the ficsit farming mod! | Everywhere |
| [Fluid Extras](https://ficsit.app/mod/AB_FluidExtras) | Several new pipe junctions, alternate Mini Water Extractor, and new A.I. Packing machine. | Everywhere |
| [Megaprojects: Power Domain](https://ficsit.app/mod/Megaprojects_PowerDomain) | A Megaproject resulting in a colossal Power Storage capable of storing up to 1.000.000MW of power (and more) | Everywhere |
| [Lithium - Expansion Mod](https://ficsit.app/mod/Lithium) | Adds a new raw resource - Lithium together with new items, buildings and Space Elevator Parts | Everywhere |
| [Pipe Priorities](https://ficsit.app/mod/PriorityPipes) | Adds priority pipe splitters and mergers | Everywhere |
| [Signal Bridge](https://ficsit.app/mod/TrainSignalBridge) | Alternative for the Path and Block Signals | Everywhere |
| [Modular Stations](https://ficsit.app/mod/ModularStations) | Provides modular pieces for building train stations | Everywhere |
| [Modular Stations SF Plus](https://ficsit.app/mod/ModularStationsSFPlus) | Compatibility patch for Modular Stations and Satisfactory Plus | Everywhere |

### Small comforts (5)

| Mod | What it does | Where |
| --- | --- | --- |
| [Faster Manual Crafting Redux](https://ficsit.app/mod/FasterManualCraftingRedux) | Are you tired of the early game crafting grind? Speed up your manual crafting! | Everywhere |
| [Manta Raise](https://ficsit.app/mod/MantaRaise) | Adjusts Flying Manta heights to keep them from flying through your buildings | Everywhere |
| [Doggo Transportation](https://ficsit.app/mod/DoggoTransportation) | Pick up and place Doggos | Everywhere |
| [BoomBox Plus](https://ficsit.app/mod/BoomBoxPlus) | The Boom Box plays your music: local files, YouTube, SoundCloud, Spotify playlists and internet radio, synced in multiplayer. | Everywhere |
| [Shorter Hard Drive Research](https://ficsit.app/mod/ShortenHardDriveResearch) | Configure how long it takes to research Hard Drives for alternates! Make it instant, longer, or in the middle. | Everywhere |

## Dropped or not added, with the reason

- `BetterGrass`: removed 2026-11-12 when Taj's Graphical Overhaul went in: Taj's sets grass density itself
- `SFPFactoryPlanner`: removed 2026-11-12: the KBFL library that Satisfactory Plus runs on refuses to start beside it (fatal 'Could not loaded SFPContentDescriptor' at boot; the library names SFPFactoryPlanner and ModelerModRecipes next to that message). Never add either to a Satisfactory Plus pack.
- `SimpleCodex`: removed 2026-11-12: its menu re-reads the recipe list every frame; with this pack the game fell to about 19 frames a second while it was open (ten 'FGRecipe::GetRecipeName: class was nullpeter' warnings per frame in the log). No settings file, 1.0.9 was the latest. The game's own Codex covers it.
- `Megaprojects_WaterDam`: removed 2026-11-14 on Scott's choice: its page calls it 'a source of unconditionally free power' (up to 50,000 MW) and Satisfactory Plus has its own Hydroelectric Power milestone and limits free power on purpose
- `Cartograph`: removed 2026-11-14: marked Damaged on ficsit.app (texture blurring from video memory use) and Atlas does the same job
- `Decoration`: removed 2026-11-14: the Factory Props page lists it as a known incompatibility (duplicate foliage, buildings that cannot be dismantled)
- `ExtraFinishes`: removed 2026-11-14: its page names Universal Swatch Slots as incompatible, ficsit.app warns of a multiplayer crash, and removing it later can stop a save loading
- `EfficiencyCheckerMod`: removed 2026-11-14: its page says it ignores Refined Power and other custom machines, which is most of a Satisfactory Plus factory
- `FicsitWiremod`: removed 2026-11-14: Scott has no use for circuitry
- `SmallTrainStation`: removed 2026-11-14, one mod per job: Modular Stations is the station mod
- `DoorsAnywhere`: removed 2026-11-14, one mod per job: Architecture+ 04 is doors and has a Satisfactory Plus patch
- `DI_MoreGlassAndWalls`: removed 2026-11-14, one mod per job: Architecture+ 02 is windows and has a patch; this one has a known missing wall preview
- `DI_More_Lights`: removed 2026-11-14, one mod per job: Lights+ stays
- `BigWalls`: removed 2026-11-14: the game no longer lists its 30 large foundations
- `CBuildings`: removed 2026-11-14, one mod per job: Foundations+ is the foundation-texture pack
- `MoreBeams`: removed 2026-11-14, one mod per job: Longer Beams and Structural Solutions stay
- `UpsideDownFoundations`: removed 2026-11-14, one mod per job: Foundations+ stays; only CBuildings and More Beams needed it
- `PropsAndDeco`: removed 2026-11-14, no overlaps: second general prop pack beside Factory Props, and its Satisfactory Plus patch no longer finds its milestone (Props and Deco 0.11.0 is newer than the patch)
- `RoadSplineTool`: removed 2026-11-14, no overlaps: second road mod beside Road Maker, and four of its pieces are named ERROR by its author
- `ContainerScreen`: not added 2026-11-14: its page says 'NOT working on Dedicated Servers or Multiplayer'; Containers with Screen (ContainerWithScreen) is its author's server-ready version and is in the pack
- `LightSettings`: removed 2026-11-14: with Taj's Graphical Overhaul it cut the game to about 8 frames a second, in the menu too. Its code (mklierman/SatisfactoryMods, LightSettings.cpp) hooks the game's light-pool update and, on every call, loops over every pooled light and resets six properties; Taj's raises the pool to 500 lights ('pool.light.count = 500'), so each update pass became hundreds of thousands of light changes on the game thread. Found by test profiles (smooth without it, slow with it) and the log (the slowdown starts on the frame Taj's applies its settings). Do not combine the two.
