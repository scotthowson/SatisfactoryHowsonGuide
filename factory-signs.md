# Live factory signs

Written by `tools/fin_page.py` from `packs/fin/`; do not edit by hand. Part of the [Howson Plus pack](plus-pack.html); the map they can read from is the [World map](world-map.html)'s own mod.

Ready-made programs for the in-game computers of FicsIt-Networks (the pack's own 1.3.0 build). Each is one file. You paste it into a computer, press the power button, and a screen or a sign starts showing live numbers from the factory.

**Not yet run in the game.** Every call in these programs was read in the source of the build the pack uses, and the programs pass 78 checks against a stand-in for the game written from that source (`test/`). What only a game run can show is listed at the end.

**Nothing extra to join.** A program lives inside the computer it was pasted into, which is part of the world. It runs on the server (or on the host). A friend who joins sees the screens and signs like any other building and needs no file.

## The programs

| File | What it shows | Where | You can build it from |
| --- | --- | --- | --- |
| `first-steps.lua` | Run once on a new computer: does three small tasks the mod's research tree asks for, then lists everything the computer can see on its network | the computer's log | Satisfactory Plus tier 5 |
| `sign-line.lua` | One live line on the game's own signs: power, a hall's machines, the emptiest container, or one item per minute | ordinary signs | tier 5 |
| `hall-board.lua` | Every machine on the network: recipe, state (running, waiting, output full, no power, paused), productivity, and a total per minute for each item | a Large Screen | tier 7 |
| `stock-board.lua` | Every storage container on the network: item, amount, fill bar; red when nearly empty, amber when nearly full | a Large Screen | tier 7 |
| `power-board.lua` | One power grid: used, produced, capacity, what it would draw with every machine running, batteries, a curve of the last minutes, and **FUSE BLOWN** in red | a Large Screen | tier 7 |
| `maplink-board.lua` | The whole factory from Howson Map Link's own numbers: power, open alerts, made and used per minute for the top items. No cables to machines | a Large Screen | tier 9 |

The tiers are where Satisfactory Plus first makes the parts the research costs (details under "What it costs").

## Putting a program into a computer

1. Build a **Computer Case** and give it power like any machine.
2. With the build gun, place a **Lua CPU** and a **Memory T1** into the open window on the front of the case. For a board, also place a **Graphical Processing Unit T1** there.
3. Craft a **Text EEPROM** at the craft bench. Open the computer, go to the EEPROM tab and drag the chip into the thin slot.
4. On this PC, open the program's file in a text editor, select everything and copy it.
5. In the computer's first tab, click into the code box, select everything and paste.
6. If you want, change the few settings in the block marked `CHANGE ONLY THIS BLOCK` near the top. Change nothing below it.
7. Press the power button. The log under the code says `... running`, or says in plain words what is missing.

To change a setting later: switch the computer off, edit the line, switch it on.

Network Cable: with the cable in the build gun, click the computer's plug, then the thing to connect. On a machine the cable clicks onto its power plug. Things can be chained one to the next. A cable also goes onto the plain and Industrial Storage Container, the game's free-standing signs, power poles, switches and Power Storages.

Nicknames: with the **Network Manager** in hand, look at a connected thing, click, and type into the nickname field. A nickname can be several words; a program that asks for a word matches any of them.

## first-steps.lua

1. Build a computer as above (no graphics card needed) and paste the file.
2. Press the power button and read the log.
3. In the MAM, the nodes after "Hello World!" are now open, and the tasks of "Network Pole" and "Network Card" are done.

Run it again whenever you want to see what a computer is connected to.

## sign-line.lua

1. Build a computer (no graphics card) and paste the file.
2. Build one or more of the game's signs. In each sign's own window pick a layout with a text field and type a single `#` into the field the line should go to.
3. Run Network Cable from the computer to each sign and to what the signs report on: the machines, the containers, and one power pole or machine of the grid.
4. With the Network Manager, give each sign a nickname:

| Nickname | The sign shows |
| --- | --- |
| `line power` | `POWER 320 / 450 MW  71 %`, or `FUSE BLOWN` |
| `line hall` | `10 of 12 running  92 %` for every machine on the network |
| `line hall smelt` | the same, only machines whose nickname contains `smelt` |
| `line stock` | the emptiest container: `Iron Plate 12 %` |
| `line stock ore` | the same, only containers whose nickname contains `ore` |
| `line item Iron Plate` | `Iron Plate 118 / min`, made on this network |

5. Press the power button. Lines refresh every 10 seconds; a line that has not changed is not written again.

If a sign stays as it was, the log says so: it found no field holding `#`.

## hall-board.lua

1. Build a computer with a Graphical Processing Unit T1 and paste the file.
2. Build a **Large Screen** and run Network Cable from the computer to it.
3. Run Network Cable to each machine of the hall, chaining from one to the next.
4. Press the power button.

Settings: `TITLE`; `GROUP` (a word: only machines whose nickname contains it, so one network can feed several boards); `COLUMNS` and `ROWS` (how many characters fit; larger numbers mean smaller text); `REFRESH`.

What the states mean: **RUNNING** its progress moved since the last look; **OUTPUT FULL** not moving and an output stack is full; **WAITING** not moving, so most likely short of input; **NO POWER**; **PAUSED** switched to standby; **NO RECIPE**. The first look after start shows `...` because one look cannot tell movement.

More machines than lines: the board turns pages by itself.

## stock-board.lua

1. Build a computer with a Graphical Processing Unit T1 and paste the file.
2. Build a Large Screen and cable it to the computer.
3. Cable each Storage Container to the network.
4. Press the power button.

A container holding one kind of item shows its exact fill. A mixed container is measured by the first item found in it, so its percentage is rough. Give a container a nickname to show that name. `LOW` and `HIGH` set where a line turns red or amber.

## power-board.lua

1. Build a computer with a Graphical Processing Unit T1 and paste the file.
2. Build a Large Screen and cable it to the computer.
3. Cable **one** thing on the grid to the network: a power pole, a Power Storage, a switch or any machine.
4. Press the power button.

`BEEP = true` makes the computer beep while the fuse is blown. If the network also carries things on another grid, nickname the one to read from and put that word in `SOURCE`.

## maplink-board.lua

Works only where Howson Map Link runs in the same program as the computer: on the dedicated server when you play there, or in your own game when you host or play alone. The per-minute list needs Map Link 2.7.0 or newer; an older one still gives power and alerts.

1. Build a computer with a Graphical Processing Unit T1 **and an Internet Card**, and paste the file.
2. Build a Large Screen and cable it to the computer.
3. Press the power button.

If Map Link listens somewhere else than `http://127.0.0.1:8765`, change `URL`.

## Trying a board before you have a Large Screen

Place a **Screen Driver** into the Computer Case and start the board with no Large Screen on the network. The picture then shows inside the computer's own window. Doing this once also completes the research task "What GPU?", which the Large Screen node waits for.

The boards do not draw on the game's own signs. In this build, pointing a graphics card at a sign only blanks the sign, so the boards refuse to. Signs get their text from `sign-line.lua`.

## What it costs

Read from the list of recipes and research the game wrote out on 14 Nov 2026 with the pack loaded (export `ingame-ba08246d`).

Research in the MAM, tree "Networking", in the order the tree demands:

| Node | Cost | Gives |
| --- | --- | --- |
| Getting Started | 1 Circuit Board, 1 Computer | Computer Case, CPU T1 (Lua), RAM T1, Text EEPROM |
| Hello World! | a task: `first-steps.lua` does it | |
| Network Cable | 10 Quickwire | Network Cable |
| Network Manager | 10 Quickwire, 2 Object Scanner | Network Manager (for nicknames) |
| Simple Graphics | 10 Crystal Oscillator, 50 Quartz Crystal, 5 Circuit Board | Graphical Processing Unit T1, Screen Driver |
| What GPU? | a task: any board drawing once does it | |
| Large Screen | 100 Quartz Crystal, 10 Circuit Board | Large Screen |

Only for `maplink-board.lua`, after Network Cable: Network Pole (10 Quickwire, 2 Object Scanner; its task is done by any of these programs), Network Card (10 Quickwire, 2 Object Scanner; its task is done by `first-steps.lua`), Wireless (10 Heavy Modular Frame, 10 Crystal Oscillator), Routing (10 High-Speed Connector, 10 Modular Frame), then Internet (20 Crystal Oscillator, 2 Computer, 200 Quickwire, 10 SAM Fluctuator), which gives the Internet Card.

When Satisfactory Plus first makes those parts by milestone: Circuit Board and Computer at tier 5 ("Industrial Manufacturing"), Quartz Crystal at tier 4, Crystal Oscillator at tier 7 ("Control System Development"), SAM Fluctuator at tier 9 ("Matter Conversion"). The MAM has nodes for Crystal Oscillator and SAM Fluctuator too; when those open was not read.

Building, each piece:

| Piece | Cost |
| --- | --- |
| Computer Case | 3 Modular Frame, 3 Reinforced Iron Plate, 4 Copper Sheet, 50 Screws |
| CPU T1 (Lua) | 1 Iron Plate, 2 Copper Sheet, 3 Quickwire |
| RAM T1 | 2 Silica, 2 Wire, 2 Quickwire |
| Text EEPROM (bench) | 1 Quickwire, 2 Iron Plate, 5 Silica |
| Network Cable | 2 Quickwire each |
| Network Manager (bench) | 2 Reinforced Iron Plate, 3 Quickwire, 3 Wire, 20 Screws |
| Graphical Processing Unit T1 | 1 Circuit Board, 3 Quickwire, 2 Copper Sheet |
| Screen Driver | 2 Iron Plate, 3 Quickwire, 2 Copper Sheet |
| Large Screen | 2 Reinforced Iron Plate, 2 Copper Sheet |
| Internet Card | 5 Quickwire, 5 Wire, 5 Copper Sheet |

One board with its screen comes to 3 Modular Frame, 5 Reinforced Iron Plate, 10 Copper Sheet, 50 Screws, 3 Iron Plate, 9 Quickwire, 7 Silica, 2 Wire and 1 Circuit Board, plus 2 Quickwire a cable. One Memory T1 is enough: this build does not count a program's memory against the modules.

## What a game run still has to show

- That the game answers each call the way its source reads. Nothing here has run in the game.
- **Productivity's scale.** The source does not say whether the game reports 0 to 1 or 0 to 100. The programs accept both.
- **Liquids.** Amounts of liquids and gases are divided by 1,000 to show cubic metres. That is how the game is known to count them, not something read in this source.
- **Speed.** Each machine costs about ten questions to the game per refresh. A hall of fifty machines may refresh slower than `REFRESH` says. Split big halls with `GROUP`, one computer each.
- **How the text looks on a Large Screen** at 80 by 28 characters, and which `COLUMNS` and `ROWS` read best from across a hall.
- **Sign fields.** `sign-line.lua` finds the text field by the `#` you typed. That the game lists a field only once it holds text is my reading; if a sign with `#` in it stays untouched, the log says so.
- **Which containers take a cable.** The plain and the Industrial Storage Container are on the mod's list. Containers that Satisfactory Plus or other mods add may not be.
- **The Internet Card and 127.0.0.1.** The mod passes the address straight to the game's own web client and blocks nothing. Whether the game's client has an allow-list of its own was not readable.
- **`/rates`.** Written against the contract for Map Link 2.7.0, which is not built yet. `/state` is as built in 2.6.0.

## For whoever changes these files

`test/run.lua` runs every program against `test/mock.lua`, a stand-in for the mod's Lua environment that has no `os`, `io` or `require`, exactly like the mod. From `test/`: `lua5.4 run.lua` (add `-v` to see every screen). The source lines behind every call are listed in the pack notes (`ficsit-networks.md`, section "Live factory signs").

## The programs, to copy

Open a box, select everything in it and copy. Step 4 above then needs no file.

<details markdown="1"><summary><code>first-steps.lua</code> (37 lines)</summary>

{% raw %}
```lua
-- FIRST STEPS (FicsIt-Networks 1.3.0, Lua)
--
-- Run this once on a new computer. It does three small things the mod's research
-- tree asks for before it lets you go on, and then lists everything the computer
-- can see on its network, so you know the cables are right.
--
--   "Hello World!"             opens the nodes after Getting Started
--   "Proxy a Network Component" asked for by the Network Pole node
--   "Proxy a computer"          asked for by the Network Card node
--
-- BUILD
--   1. A Computer Case with one Lua CPU and one Memory T1 placed into it.
--   2. Paste this whole file into the Text EEPROM of the computer and press the
--      power button. Read the result in the computer's log.
--
-- NOTHING NEEDS EDITING

print("Hello World!")

-- every computer case on the network, this one included
local caseClass = classes.ComputerCase
local cases = caseClass and component.proxy(component.findComponent(caseClass)) or {}
print("Computer cases on this network: " .. #cases)

-- everything on the network: an empty nickname matches all of it
local ids = component.findComponent("")
print("Things on this network: " .. #ids)
for i, id in ipairs(ids) do
  local obj = component.proxy(id)
  if obj then
    local nick = obj.nick
    if nick == nil or nick == "" then nick = "(no nickname)" end
    local kind = tostring(obj.internalName or "?"):gsub("^Build_", ""):gsub("_C_%d+$", "")
    print(string.format("%3d  %-28s %s", i, kind, nick))
  end
end
print("Done. This computer can be switched off.")
```
{% endraw %}

</details>

<details markdown="1"><summary><code>hall-board.lua</code> (369 lines)</summary>

{% raw %}
```lua
-- HALL BOARD (FicsIt-Networks 1.3.0, Lua)
--
-- Shows every machine on this computer's network: its recipe, whether it is
-- running, and how productive it is, with a total per minute for each item.
--
-- BUILD
--   1. A Computer Case with one Lua CPU, one Memory T1 and one Graphical
--      Processing Unit T1 placed into it.
--   2. A Large Screen to draw on. To try the program before you have one, place
--      a Screen Driver into the Computer Case: the picture then shows inside
--      the computer's own window.
--   3. Network Cable from the Computer Case to the Large Screen and to each
--      machine of the hall. A cable clicks onto a machine's power plug. Machines
--      can be daisy-chained: computer - machine - machine - ...
--   4. Paste this whole file into the Text EEPROM of the computer and press the
--      power button.
--   Only when several Large Screens hang on the same network: look at the one
--   you want with the Network Manager in hand, click, type a nickname (for
--   example board1) and put the same word in SCREEN below.
--
-- CHANGE ONLY THIS BLOCK
local TITLE   = "HALL 1"   -- heading on the board
local SCREEN  = ""         -- "" = the first Large Screen found on the network;
                           -- or the nickname you gave the one to draw on
local GROUP   = ""         -- "" = every machine on the network; a word = only
                           -- machines whose nickname contains that word
local COLUMNS = 80         -- characters across (at most 300)
local ROWS    = 28         -- lines down (at most 100)
local REFRESH = 5          -- seconds between redraws
local RESCAN  = 60         -- seconds between looking for added or removed machines
local TOTALS  = 6          -- how many items the totals list shows at most
-- NOTHING BELOW NEEDS EDITING

local WHITE, GREY   = {1, 1, 1}, {0.45, 0.45, 0.45}
local GREEN, AMBER  = {0.2, 1, 0.3}, {1, 0.75, 0.1}
local RED, BLUE     = {1, 0.2, 0.15}, {0.4, 0.75, 1}

---------------------------------------------------------------- display
local gpu

local function firstProxy(query)
  local ids = component.findComponent(query)
  if ids and ids[1] then return component.proxy(ids[1]) end
  return nil
end

local function findScreen()
  if SCREEN ~= "" then
    local s = firstProxy(SCREEN)
    if s then return s end
  end
  local class = classes.Screen
  if class then
    local s = firstProxy(class)
    if s then return s end
  end
  local driver = classes.FINComputerScreen
  if driver then return computer.getPCIDevices(driver)[1] end
  return nil
end

-- This build cannot draw on the game's own signs: binding one only blanks it.
local function refuseSign(screen, who)
  local signClass = classes.WidgetSign
  if not signClass then return end
  local ok, isSign = pcall(function() return screen:isA(signClass) end)
  if ok and isSign then
    computer.panic(who .. ": '" .. SCREEN .. "' is one of the game's own signs. Use a Large Screen (sign-line.lua writes to signs).")
  end
end

local function openDisplay()
  local class = classes.GPUT1
  gpu = class and computer.getPCIDevices(class)[1]
  if not gpu then computer.panic("Hall board: no Graphical Processing Unit T1 in this computer.") end
  local screen = findScreen()
  if not screen then computer.panic("Hall board: no Large Screen on this network and no Screen Driver in this computer (SCREEN = '" .. SCREEN .. "').") end
  refuseSign(screen, "Hall board")
  gpu:bindScreen(screen)
  gpu:setSize(COLUMNS, ROWS)
end

local function cut(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n <= width then return text .. string.rep(" ", width - n) end
  local stop = utf8.offset(text, width + 1)
  return stop and text:sub(1, stop - 1) or text:sub(1, width)
end

local function right(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n >= width then return cut(text, width) end
  return string.rep(" ", width - n) .. text
end

local function put(x, y, text, colour)
  if y < 0 or y >= ROWS or x >= COLUMNS then return end
  colour = colour or WHITE
  gpu:setForeground(colour[1], colour[2], colour[3], 1)
  gpu:setText(x, y, cut(text, math.min(utf8.len(tostring(text)) or #tostring(text), COLUMNS - x)))
end

local function clear()
  gpu:setBackground(0, 0, 0, 1)
  gpu:setForeground(1, 1, 1, 1)
  gpu:fill(0, 0, COLUMNS, ROWS, " ")
end

local function num(value)
  if value >= 1000 then return string.format("%.0f", value) end
  if value >= 100 then return string.format("%.0f", value) end
  return string.format("%.1f", value)
end

---------------------------------------------------------------- machines
local machines = {}      -- { obj, label, lastProgress, powerInfo }
local recipes = {}       -- recipe internal name -> { name, products = { {name, amount} } }
local lastScan = nil

local function shortName(obj)
  local nick = obj.nick
  if nick and nick ~= "" then
    if GROUP ~= "" then
      local words = {}
      for word in nick:gmatch("%S+") do
        if word ~= GROUP then words[#words + 1] = word end
      end
      if #words > 0 then return table.concat(words, " ") end
    else
      return nick
    end
  end
  local name = tostring(obj.internalName or "machine")
  name = name:gsub("^Build_", ""):gsub("_C_%d+$", ""):gsub("_C$", "")
  return name
end

local function scan()
  local class = classes.Manufacturer
  local ids
  if GROUP ~= "" then ids = component.findComponent(GROUP) else ids = component.findComponent(class) end
  local found = {}
  for _, id in ipairs(ids or {}) do
    local obj = component.proxy(id)
    if obj then
      local ok, isMachine = pcall(function() return obj:isA(class) end)
      if ok and isMachine then
        found[#found + 1] = { obj = obj, id = id, label = shortName(obj) }
      end
    end
  end
  table.sort(found, function(a, b) return a.label < b.label end)
  -- keep what was already known about a machine (its last progress)
  local old = {}
  for _, entry in ipairs(machines) do old[entry.id] = entry end
  for _, entry in ipairs(found) do
    local before = old[entry.id]
    if before then
      entry.lastProgress = before.lastProgress
      entry.powerInfo = before.powerInfo
    end
  end
  machines = found
end

local function recipeInfo(recipe)
  local key = recipe.internalName
  local info = recipes[key]
  if info then return info end
  info = { name = recipe.name, products = {} }
  for _, product in ipairs(recipe:getProducts() or {}) do
    local itemType = product.type
    local amount = product.amount or 0
    local name = "?"
    if itemType then
      name = itemType.name
      -- liquids and gases are counted in thousandths of a cubic metre
      if itemType.form == 2 or itemType.form == 3 then amount = amount / 1000 end
    end
    info.products[#info.products + 1] = { name = name, amount = amount }
  end
  recipes[key] = info
  return info
end

local function hasPower(entry)
  if entry.powerInfo == nil then
    entry.powerInfo = false
    local connectors = entry.obj:getPowerConnectors()
    local connector = connectors and connectors[1]
    if connector then entry.powerInfo = connector:getPower() or false end
  end
  if entry.powerInfo == false then return nil end
  return entry.powerInfo.hasPower
end

local function outputFull(machine)
  local inventory = machine:getOutputInv()
  if not inventory then return false end
  for slot = 0, inventory.size - 1 do
    local stack = inventory:getStack(slot)
    local itemType = stack and stack.item and stack.item.type
    if itemType then
      local limit = itemType.max or 0
      if limit > 0 and stack.count >= limit then return true end
    end
  end
  return false
end

-- one machine -> { label, recipe, state, colour, pct, rates = { {name, now, full} } }
local function read(entry)
  local machine = entry.obj
  local row = { label = entry.label, recipe = "", rates = {} }
  local recipe = machine:getRecipe()
  if not recipe then
    row.state, row.colour = "NO RECIPE", GREY
    return row
  end
  local info = recipeInfo(recipe)
  row.recipe = info.name

  local productivity = machine.productivity or 0
  if productivity > 1.5 then productivity = productivity / 100 end   -- accept 0..1 or 0..100
  row.pct = productivity

  local cycle = machine.cycleTime or 0
  local boost = machine.currentProductionBoost or 1
  if boost <= 0 then boost = 1 end
  if cycle > 0 then
    for _, product in ipairs(info.products) do
      local full = product.amount * boost * 60 / cycle
      row.rates[#row.rates + 1] = { name = product.name, now = full * productivity, full = full }
    end
  end

  local progress = machine.progress or 0
  local first = entry.lastProgress == nil
  local moving = (not first) and math.abs(progress - entry.lastProgress) > 0.0001
  entry.lastProgress = progress

  if machine.standby then
    row.state, row.colour = "PAUSED", GREY
  elseif hasPower(entry) == false then
    row.state, row.colour = "NO POWER", RED
  elseif moving then
    row.state, row.colour = "RUNNING", GREEN
  elseif first then
    row.state, row.colour = "...", GREY
  elseif outputFull(machine) then
    row.state, row.colour = "OUTPUT FULL", AMBER
  else
    row.state, row.colour = "WAITING", AMBER
  end
  return row
end

---------------------------------------------------------------- drawing
local page = 0

local function draw(rows)
  clear()

  local running, pctSum, pctCount = 0, 0, 0
  local totals, order = {}, {}
  for _, row in ipairs(rows) do
    if row.state == "RUNNING" then running = running + 1 end
    if row.pct then pctSum, pctCount = pctSum + row.pct, pctCount + 1 end
    for _, rate in ipairs(row.rates) do
      local total = totals[rate.name]
      if not total then
        total = { name = rate.name, now = 0, full = 0 }
        totals[rate.name] = total
        order[#order + 1] = total
      end
      total.now, total.full = total.now + rate.now, total.full + rate.full
    end
  end
  table.sort(order, function(a, b) return a.full > b.full end)

  local average = pctCount > 0 and (pctSum / pctCount * 100) or 0
  local summary = string.format("%d machines  %d running  %.0f %%", #rows, running, average)
  put(0, 0, TITLE, BLUE)
  put(math.max(#TITLE + 2, COLUMNS - #summary), 0, summary, WHITE)
  put(0, 1, string.rep("-", COLUMNS), GREY)

  -- the totals never take more than a third of the board
  local totalLines = math.min(#order, TOTALS, math.max(0, (ROWS - 4) // 3))
  local bottom = totalLines > 0 and (totalLines + 2) or 0
  local listTop = 3
  local listLines = math.max(1, ROWS - listTop - bottom)

  local nameW = math.max(8, math.floor(COLUMNS * 0.24))
  local stateW, pctW, rateW = 12, 6, 16
  if COLUMNS < 64 then rateW = 0 end   -- a narrow board drops the per-minute column
  local recipeW = math.max(6, COLUMNS - nameW - stateW - pctW - rateW - (rateW > 0 and 4 or 3))
  local x1, x2, x3, x4 = nameW + 1, nameW + recipeW + 2, nameW + recipeW + stateW + 3, nameW + recipeW + stateW + pctW + 4
  put(0, 2, cut("MACHINE", nameW), GREY)
  put(x1, 2, cut("RECIPE", recipeW), GREY)
  put(x2, 2, cut("STATE", stateW), GREY)
  put(x3, 2, right("PROD", pctW), GREY)
  if rateW > 0 then put(x4, 2, right("PER MIN", rateW), GREY) end

  local pages = math.max(1, math.ceil(#rows / listLines))
  if page >= pages then page = 0 end
  local from = page * listLines
  for line = 1, listLines do
    local row = rows[from + line]
    if not row then break end
    local y = listTop + line - 1
    put(0, y, cut(row.label, nameW), WHITE)
    put(x1, y, cut(row.recipe, recipeW), WHITE)
    put(x2, y, cut(row.state, stateW), row.colour)
    if row.pct then put(x3, y, right(string.format("%.0f %%", row.pct * 100), pctW), WHITE) end
    local first = row.rates[1]
    if first and rateW > 0 then put(x4, y, right(num(first.now) .. " / " .. num(first.full), rateW), WHITE) end
  end
  if pages > 1 then
    local note = string.format(" page %d of %d", page + 1, pages)
    put(COLUMNS - #note, 1, note, GREY)
    page = page + 1
  end

  if totalLines > 0 then
    local y = ROWS - bottom
    put(0, y, string.rep("-", COLUMNS), GREY)
    put(0, y + 1, "MADE PER MINUTE (now / at 100 %)", GREY)
    for i = 1, totalLines do
      local total = order[i]
      local colour = GREEN
      if total.full > 0 and total.now < total.full * 0.5 then colour = AMBER end
      put(0, y + 1 + i, cut(total.name, math.max(8, COLUMNS - 22)), WHITE)
      put(COLUMNS - 20, y + 1 + i, right(num(total.now) .. " / " .. num(total.full), 20), colour)
    end
  end

  gpu:flush()
end

---------------------------------------------------------------- main
openDisplay()
print("Hall board running: " .. TITLE)

while true do
  local now = computer.millis()
  if lastScan == nil or now - lastScan >= RESCAN * 1000 then
    local ok, err = pcall(scan)
    if not ok then print("Hall board: scan failed: " .. tostring(err)) end
    lastScan = now
  end

  local rows = {}
  for _, entry in ipairs(machines) do
    local ok, row = pcall(read, entry)
    if ok then
      rows[#rows + 1] = row
    else
      rows[#rows + 1] = { label = entry.label, recipe = "", state = "GONE?", colour = GREY, rates = {} }
      lastScan = nil   -- look again on the next round
    end
  end

  local ok, err = pcall(draw, rows)
  if not ok then print("Hall board: drawing failed: " .. tostring(err)) end

  event.pull(REFRESH)
end
```
{% endraw %}

</details>

<details markdown="1"><summary><code>maplink-board.lua</code> (374 lines)</summary>

{% raw %}
```lua
-- MAP LINK BOARD (FicsIt-Networks 1.3.0, Lua)
--
-- A factory-wide board fed by Howson Map Link's own numbers: what the whole
-- factory makes and uses per minute, the power grid, and the open alerts.
-- It needs no cables to machines: it asks Map Link over the Internet Card.
--
-- It only works where Howson Map Link is running in the SAME program as this
-- computer: on the dedicated server when you play there, or in your own game
-- when you host or play alone. 127.0.0.1 always means "this machine".
-- The per-minute list needs Map Link 2.7.0 or newer (/rates); with an older
-- Map Link the board shows power and alerts only.
--
-- BUILD
--   1. A Computer Case with one Lua CPU, one Memory T1, one Graphical Processing
--      Unit T1 and one Internet Card placed into it.
--   2. A Large Screen to draw on, joined to the Computer Case with a Network
--      Cable. (To try it first: a Screen Driver placed into the Computer Case
--      shows the picture inside the computer's own window.)
--   3. Paste this whole file into the Text EEPROM of the computer and press the
--      power button.
--
-- CHANGE ONLY THIS BLOCK
local TITLE   = "FACTORY"                 -- heading on the board
local SCREEN  = ""                        -- "" = the first Large Screen found; or its nickname
local URL     = "http://127.0.0.1:8765"   -- where Map Link listens
local COLUMNS = 80                        -- characters across (at most 300)
local ROWS    = 28                        -- lines down (at most 100)
local REFRESH = 15                        -- seconds between redraws
local ITEMS   = 14                        -- how many items the list shows at most
local ALERTS  = 5                         -- how many alerts the list shows at most
-- NOTHING BELOW NEEDS EDITING

local WHITE, GREY   = {1, 1, 1}, {0.45, 0.45, 0.45}
local GREEN, AMBER  = {0.2, 1, 0.3}, {1, 0.75, 0.1}
local RED, BLUE     = {1, 0.2, 0.15}, {0.4, 0.75, 1}

---------------------------------------------------------------- display
local gpu

local function firstProxy(query)
  local ids = component.findComponent(query)
  if ids and ids[1] then return component.proxy(ids[1]) end
  return nil
end

local function findScreen()
  if SCREEN ~= "" then
    local s = firstProxy(SCREEN)
    if s then return s end
  end
  local class = classes.Screen
  if class then
    local s = firstProxy(class)
    if s then return s end
  end
  local driver = classes.FINComputerScreen
  if driver then return computer.getPCIDevices(driver)[1] end
  return nil
end

-- This build cannot draw on the game's own signs: binding one only blanks it.
local function refuseSign(screen, who)
  local signClass = classes.WidgetSign
  if not signClass then return end
  local ok, isSign = pcall(function() return screen:isA(signClass) end)
  if ok and isSign then
    computer.panic(who .. ": '" .. SCREEN .. "' is one of the game's own signs. Use a Large Screen (sign-line.lua writes to signs).")
  end
end

local function openDisplay()
  local class = classes.GPUT1
  gpu = class and computer.getPCIDevices(class)[1]
  if not gpu then computer.panic("Map Link board: no Graphical Processing Unit T1 in this computer.") end
  local screen = findScreen()
  if not screen then computer.panic("Map Link board: no Large Screen on this network and no Screen Driver in this computer (SCREEN = '" .. SCREEN .. "').") end
  refuseSign(screen, "Map Link board")
  gpu:bindScreen(screen)
  gpu:setSize(COLUMNS, ROWS)
end

local function cut(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n <= width then return text .. string.rep(" ", width - n) end
  local stop = utf8.offset(text, width + 1)
  return stop and text:sub(1, stop - 1) or text:sub(1, width)
end

local function right(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n >= width then return cut(text, width) end
  return string.rep(" ", width - n) .. text
end

local function put(x, y, text, colour)
  if y < 0 or y >= ROWS or x >= COLUMNS then return end
  colour = colour or WHITE
  gpu:setForeground(colour[1], colour[2], colour[3], 1)
  gpu:setText(x, y, cut(text, math.min(utf8.len(tostring(text)) or #tostring(text), COLUMNS - x)))
end

local function clear()
  gpu:setBackground(0, 0, 0, 1)
  gpu:setForeground(1, 1, 1, 1)
  gpu:fill(0, 0, COLUMNS, ROWS, " ")
end

local function num(value)
  if value >= 100 then return string.format("%.0f", value) end
  return string.format("%.1f", value)
end

---------------------------------------------------------------- JSON
-- A small reader. pick(text, {"items", "power"}) walks the outermost object and
-- decodes only the named keys; everything else is stepped over without building
-- tables, so a large answer does not use the computer's memory.
local function skipSpace(s, i)
  local _, stop = s:find("^[ \n\r\t]*", i)
  return stop + 1
end

local function readString(s, i)   -- s:sub(i,i) is the opening quote
  local out, j = {}, i + 1
  while true do
    local a, b = s:find('["\\]', j)
    if not a then error("JSON: unfinished text") end
    out[#out + 1] = s:sub(j, a - 1)
    if s:sub(a, a) == '"' then return table.concat(out), a + 1 end
    local c = s:sub(a + 1, a + 1)
    if c == "u" then
      local code = tonumber(s:sub(a + 2, a + 5), 16) or 63
      if code >= 0xD800 and code <= 0xDBFF and s:sub(a + 6, a + 7) == "\\u" then
        local low = tonumber(s:sub(a + 8, a + 11), 16) or 0
        code = 0x10000 + ((code - 0xD800) << 10) + (low - 0xDC00)
        a = a + 6
      end
      out[#out + 1] = utf8.char(code)
      j = a + 6
    else
      local map = { b = "\b", f = "\f", n = "\n", r = "\r", t = "\t" }
      out[#out + 1] = map[c] or c
      j = a + 2
    end
  end
end

local function skipString(s, i)
  local j = i + 1
  while true do
    local a = s:find('["\\]', j)
    if not a then error("JSON: unfinished text") end
    if s:sub(a, a) == '"' then return a + 1 end
    j = a + 2
  end
end

local decode   -- declared first: values contain values

local function decodeArray(s, i)
  local list, n = {}, 0
  i = skipSpace(s, i + 1)
  if s:sub(i, i) == "]" then return list, i + 1 end
  while true do
    local value
    value, i = decode(s, i)
    n = n + 1
    list[n] = value
    i = skipSpace(s, i)
    local c = s:sub(i, i)
    if c == "]" then return list, i + 1 end
    if c ~= "," then error("JSON: expected , or ] at " .. i) end
    i = skipSpace(s, i + 1)
  end
end

local function decodeObject(s, i)
  local object = {}
  i = skipSpace(s, i + 1)
  if s:sub(i, i) == "}" then return object, i + 1 end
  while true do
    if s:sub(i, i) ~= '"' then error("JSON: expected a name at " .. i) end
    local key
    key, i = readString(s, i)
    i = skipSpace(s, i)
    if s:sub(i, i) ~= ":" then error("JSON: expected : at " .. i) end
    local value
    value, i = decode(s, skipSpace(s, i + 1))
    object[key] = value
    i = skipSpace(s, i)
    local c = s:sub(i, i)
    if c == "}" then return object, i + 1 end
    if c ~= "," then error("JSON: expected , or } at " .. i) end
    i = skipSpace(s, i + 1)
  end
end

decode = function(s, i)
  i = skipSpace(s, i)
  local c = s:sub(i, i)
  if c == "{" then return decodeObject(s, i) end
  if c == "[" then return decodeArray(s, i) end
  if c == '"' then return readString(s, i) end
  if s:sub(i, i + 3) == "true" then return true, i + 4 end
  if s:sub(i, i + 4) == "false" then return false, i + 5 end
  if s:sub(i, i + 3) == "null" then return nil, i + 4 end
  local a, b = s:find("^-?%d+%.?%d*[eE]?[+-]?%d*", i)
  if not a then error("JSON: unexpected character at " .. i) end
  return tonumber(s:sub(a, b)), b + 1
end

local function skipValue(s, i)
  i = skipSpace(s, i)
  local c = s:sub(i, i)
  if c == '"' then return skipString(s, i) end
  if c == "{" or c == "[" then
    local depth = 0
    while true do
      local a = s:find('["{}%[%]]', i)
      if not a then error("JSON: unfinished value") end
      local d = s:sub(a, a)
      if d == '"' then
        i = skipString(s, a)
      else
        if d == "{" or d == "[" then depth = depth + 1 else depth = depth - 1 end
        i = a + 1
        if depth == 0 then return i end
      end
    end
  end
  local _, stop = s:find("^[^,}%]]*", i)
  return stop + 1
end

local function pick(s, wanted)
  local want = {}
  for _, key in ipairs(wanted) do want[key] = true end
  local result = {}
  local i = skipSpace(s, 1)
  if s:sub(i, i) ~= "{" then error("JSON: the answer is not an object") end
  i = skipSpace(s, i + 1)
  if s:sub(i, i) == "}" then return result end
  while true do
    if s:sub(i, i) ~= '"' then error("JSON: expected a name at " .. i) end
    local key
    key, i = readString(s, i)
    i = skipSpace(s, i)
    if s:sub(i, i) ~= ":" then error("JSON: expected : at " .. i) end
    i = skipSpace(s, i + 1)
    if want[key] then
      result[key], i = decode(s, i)
    else
      i = skipValue(s, i)
    end
    i = skipSpace(s, i)
    local c = s:sub(i, i)
    if c == "}" then return result end
    if c ~= "," then error("JSON: expected , or } at " .. i) end
    i = skipSpace(s, i + 1)
  end
end

---------------------------------------------------------------- asking Map Link
local card

local function ask(path, wanted)
  local request = card:request(URL .. path, "GET", "")
  local code, body = request:await()
  if code == nil then return nil, "no answer" end
  if code ~= 200 then return nil, "answer " .. tostring(code) end
  local ok, result = pcall(pick, body or "", wanted)
  if not ok then return nil, tostring(result) end
  return result, nil
end

---------------------------------------------------------------- drawing
local function draw(state, stateError, rates, ratesError)
  clear()
  put(0, 0, TITLE, BLUE)
  local y = 2
  put(0, 1, string.rep("-", COLUMNS), GREY)

  if not state then
    put(0, y, "Map Link does not answer at " .. URL, RED)
    put(0, y + 1, "(" .. tostring(stateError) .. ") Is it running in this game or on this server?", GREY)
    gpu:flush()
    return
  end

  -- power
  local power = state.power
  if type(power) == "table" then
    local used, capacity = tonumber(power.consumed) or 0, tonumber(power.capacity) or 0
    local produced = tonumber(power.produced) or 0
    if power.fuse then
      put(0, y, "POWER   FUSE BLOWN - THE POWER IS OFF", RED)
    else
      local share = capacity > 0 and (used / capacity * 100) or 0
      local colour = share >= 90 and AMBER or GREEN
      put(0, y, string.format("POWER   %.0f used  %.0f produced  %.0f capacity MW  %.0f %%", used, produced, capacity, share), colour)
    end
    if power.source == "client" then put(0, y + 1, "(this game is a client: only the fuse is known here)", GREY) end
    y = y + 2
  end

  -- alerts
  local alerts = state.alerts
  if type(alerts) == "table" and type(alerts.list) == "table" then
    local total = tonumber(alerts.total) or #alerts.list
    put(0, y, total == 0 and "ALERTS  none" or ("ALERTS  " .. total .. " open"), total == 0 and GREEN or AMBER)
    y = y + 1
    for i = 1, math.min(#alerts.list, ALERTS) do
      local alert = alerts.list[i]
      local colour = AMBER
      if (tonumber(alert.sev) or 0) >= 3 then colour = RED end
      local text = tostring(alert.text or alert.kind or "?")
      if alert.n then text = tostring(alert.n) .. ": " .. text end
      put(2, y, text, colour)
      y = y + 1
    end
    y = y + 1
  end

  -- per minute
  if not rates then
    put(0, y, "PER MINUTE  not available (" .. tostring(ratesError) .. "): needs Map Link 2.7.0", GREY)
    gpu:flush()
    return
  end
  local items = rates.items
  if type(items) ~= "table" then items = {} end
  table.sort(items, function(a, b) return (tonumber(a.made) or 0) > (tonumber(b.made) or 0) end)
  local nameW = math.max(10, COLUMNS - 36)
  put(0, y, cut("PER MINUTE", nameW), GREY)
  put(nameW, y, right("MADE", 9) .. right("AT 100 %", 10) .. right("USED", 9) .. right("LEFT", 8), GREY)
  y = y + 1
  for i = 1, math.min(#items, ITEMS, math.max(0, ROWS - y)) do
    local item = items[i]
    local made, used, cap = tonumber(item.made) or 0, tonumber(item.used) or 0, tonumber(item.cap) or 0
    local left = made - used
    local colour = GREEN
    if cap > 0 and made < cap * 0.5 then colour = AMBER end
    if left < 0 then colour = RED end
    put(0, y, cut(tostring(item.n or "?"), nameW), WHITE)
    put(nameW, y, right(num(made), 9) .. right(num(cap), 10) .. right(num(used), 9), WHITE)
    put(nameW + 28, y, right(num(left), 8), colour)
    y = y + 1
  end
  gpu:flush()
end

---------------------------------------------------------------- main
openDisplay()
do
  local class = classes.FINInternetCard
  card = class and computer.getPCIDevices(class)[1]
  if not card then computer.panic("Map Link board: no Internet Card in this computer.") end
end
print("Map Link board running: " .. TITLE)

while true do
  local okState, state, stateError = pcall(ask, "/state", {"power", "alerts"})
  if not okState then state, stateError = nil, tostring(state) end
  local rates, ratesError = nil, "not asked"
  if state then
    local okRates
    okRates, rates, ratesError = pcall(ask, "/rates", {"items"})
    if not okRates then rates, ratesError = nil, tostring(rates) end
  end
  local ok, err = pcall(draw, state, stateError, rates, ratesError)
  if not ok then print("Map Link board: drawing failed: " .. tostring(err)) end
  event.pull(REFRESH)
end
```
{% endraw %}

</details>

<details markdown="1"><summary><code>power-board.lua</code> (281 lines)</summary>

{% raw %}
```lua
-- POWER BOARD (FicsIt-Networks 1.3.0, Lua)
--
-- Shows one power grid: produced, used, capacity, what it would draw with every
-- machine running, the batteries, and a red line the moment the fuse blows.
--
-- BUILD
--   1. A Computer Case with one Lua CPU, one Memory T1 and one Graphical
--      Processing Unit T1 placed into it.
--   2. A Large Screen to draw on. To try the program before you have one, place
--      a Screen Driver into the Computer Case: the picture then shows inside
--      the computer's own window.
--   3. Network Cable from the Computer Case to the Large Screen and to ONE
--      thing that is plugged into the grid you want to watch: a power pole, a
--      Power Storage, a power switch or any machine. The cable clicks onto its
--      power plug.
--   4. Paste this whole file into the Text EEPROM of the computer and press the
--      power button.
--   Only when the network also carries things on another grid: give the one to
--   read from a nickname with the Network Manager and put it in SOURCE below.
--
-- CHANGE ONLY THIS BLOCK
local TITLE   = "POWER"    -- heading on the board
local SCREEN  = ""         -- "" = the first Large Screen found on the network;
                           -- or the nickname you gave the one to draw on
local SOURCE  = ""         -- "" = the first pole, switch, storage or machine found;
                           -- or the nickname of the thing to read the grid from
local COLUMNS = 56         -- characters across (at most 300)
local ROWS    = 16         -- lines down (at most 100)
local REFRESH = 2          -- seconds between redraws
local BEEP    = false      -- true = the computer beeps while the fuse is blown
-- NOTHING BELOW NEEDS EDITING

local WHITE, GREY   = {1, 1, 1}, {0.45, 0.45, 0.45}
local GREEN, AMBER  = {0.2, 1, 0.3}, {1, 0.75, 0.1}
local RED, BLUE     = {1, 0.2, 0.15}, {0.4, 0.75, 1}

---------------------------------------------------------------- display
local gpu

local function firstProxy(query)
  local ids = component.findComponent(query)
  if ids and ids[1] then return component.proxy(ids[1]) end
  return nil
end

local function findScreen()
  if SCREEN ~= "" then
    local s = firstProxy(SCREEN)
    if s then return s end
  end
  local class = classes.Screen
  if class then
    local s = firstProxy(class)
    if s then return s end
  end
  local driver = classes.FINComputerScreen
  if driver then return computer.getPCIDevices(driver)[1] end
  return nil
end

-- This build cannot draw on the game's own signs: binding one only blanks it.
local function refuseSign(screen, who)
  local signClass = classes.WidgetSign
  if not signClass then return end
  local ok, isSign = pcall(function() return screen:isA(signClass) end)
  if ok and isSign then
    computer.panic(who .. ": '" .. SCREEN .. "' is one of the game's own signs. Use a Large Screen (sign-line.lua writes to signs).")
  end
end

local function openDisplay()
  local class = classes.GPUT1
  gpu = class and computer.getPCIDevices(class)[1]
  if not gpu then computer.panic("Power board: no Graphical Processing Unit T1 in this computer.") end
  local screen = findScreen()
  if not screen then computer.panic("Power board: no Large Screen on this network and no Screen Driver in this computer (SCREEN = '" .. SCREEN .. "').") end
  refuseSign(screen, "Power board")
  gpu:bindScreen(screen)
  gpu:setSize(COLUMNS, ROWS)
end

local function cut(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n <= width then return text .. string.rep(" ", width - n) end
  local stop = utf8.offset(text, width + 1)
  return stop and text:sub(1, stop - 1) or text:sub(1, width)
end

local function right(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n >= width then return cut(text, width) end
  return string.rep(" ", width - n) .. text
end

local function put(x, y, text, colour)
  if y < 0 or y >= ROWS or x >= COLUMNS then return end
  colour = colour or WHITE
  gpu:setForeground(colour[1], colour[2], colour[3], 1)
  gpu:setText(x, y, cut(text, math.min(utf8.len(tostring(text)) or #tostring(text), COLUMNS - x)))
end

local function clear()
  gpu:setBackground(0, 0, 0, 1)
  gpu:setForeground(1, 1, 1, 1)
  gpu:fill(0, 0, COLUMNS, ROWS, " ")
end

---------------------------------------------------------------- the grid
local connector = nil

-- anything on the network with a power plug that is wired to something
local function findConnector()
  local candidates = {}
  if SOURCE ~= "" then
    for _, id in ipairs(component.findComponent(SOURCE) or {}) do candidates[#candidates + 1] = id end
  else
    for _, name in ipairs({"FGBuildablePowerPole", "PowerStorage", "CircuitSwitch", "Factory"}) do
      local class = classes[name]
      if class then
        for _, id in ipairs(component.findComponent(class) or {}) do candidates[#candidates + 1] = id end
      end
    end
  end
  for _, id in ipairs(candidates) do
    local obj = component.proxy(id)
    if obj then
      local ok, list = pcall(function() return obj:getPowerConnectors() end)
      if ok and list then
        for _, plug in ipairs(list) do
          local okCircuit, circuit = pcall(function() return plug:getCircuit() end)
          if okCircuit and circuit then return plug end
        end
      end
    end
  end
  return nil
end

local function read()
  if not connector then connector = findConnector() end
  if not connector then return nil end
  local circuit = connector:getCircuit()
  if not circuit then
    connector = nil
    return nil
  end
  local grid = {
    produced = circuit.production or 0,
    used     = circuit.consumption or 0,
    capacity = circuit.capacity or 0,
    maxDraw  = circuit.maxPowerConsumption or 0,
    fuse     = circuit.isFuesed and true or false,   -- the game's own spelling
    battery  = circuit.hasBatteries and true or false,
  }
  if grid.battery then
    grid.stored   = circuit.batteryStore or 0
    grid.room     = circuit.batteryCapacity or 0
    grid.charging = circuit.batteryIn or 0
    grid.draining = circuit.batteryOut or 0
    grid.toEmpty  = circuit.batteryTimeUntilEmpty or 0
    grid.toFull   = circuit.batteryTimeUntilFull or 0
  end
  return grid
end

---------------------------------------------------------------- drawing
local history = {}       -- used / capacity, newest last
local blink = false

local function bar(part, whole, width)
  local filled = 0
  if whole > 0 then filled = math.floor(math.min(1, part / whole) * width + 0.5) end
  return "[" .. string.rep("#", filled) .. string.rep("-", width - filled) .. "]"
end

local function duration(seconds)
  if seconds <= 0 then return nil end
  if seconds >= 3600 then return string.format("%.1f h", seconds / 3600) end
  if seconds >= 60 then return string.format("%.0f min", seconds / 60) end
  return string.format("%.0f s", seconds)
end

local function mw(value) return string.format("%.1f MW", value) end

local function draw(grid)
  clear()
  put(0, 0, TITLE, BLUE)
  put(0, 1, string.rep("-", COLUMNS), GREY)
  if not grid then
    put(0, 3, "No power grid found on this network.", AMBER)
    put(0, 4, "Run a Network Cable to a power pole or a machine.", GREY)
    gpu:flush()
    return
  end

  local share = grid.capacity > 0 and (grid.used / grid.capacity) or 0
  local colour = GREEN
  if share >= 0.9 then colour = AMBER end
  if grid.fuse then colour = RED end
  local barW = math.max(6, COLUMNS - 32)

  put(0, 3, "Used", GREY)
  put(11, 3, right(mw(grid.used), 12), WHITE)
  put(25, 3, bar(grid.used, grid.capacity, barW), colour)
  put(COLUMNS - 5, 3, right(string.format("%.0f %%", share * 100), 5), colour)
  put(0, 4, "Produced", GREY)
  put(11, 4, right(mw(grid.produced), 12), WHITE)
  put(0, 5, "Capacity", GREY)
  put(11, 5, right(mw(grid.capacity), 12), WHITE)
  put(0, 6, "Max draw", GREY)
  put(11, 6, right(mw(grid.maxDraw), 12), WHITE)
  if grid.maxDraw > grid.capacity and not grid.battery then
    put(25, 6, "trips if every machine runs", AMBER)
  else
    put(25, 6, "with every machine running", GREY)
  end

  if grid.battery then
    local filled = grid.room > 0 and (grid.stored / grid.room) or 0
    put(0, 8, "Batteries", GREY)
    put(11, 8, right(string.format("%.0f / %.0f MWh", grid.stored, grid.room), 20), WHITE)
    put(33, 8, right(string.format("%.0f %%", filled * 100), 5), WHITE)
    local note
    if grid.draining > 0.05 and duration(grid.toEmpty) then
      note, colour = "empty in " .. duration(grid.toEmpty), AMBER
    elseif grid.charging > 0.05 and duration(grid.toFull) then
      note, colour = "full in " .. duration(grid.toFull), GREEN
    end
    if note then put(11, 9, note, colour) end
  else
    put(0, 8, "Batteries", GREY)
    put(11, 8, "none on this grid", GREY)
  end

  -- the last minutes of use, one character a reading
  history[#history + 1] = share
  while #history > COLUMNS do table.remove(history, 1) end
  local marks = " .:-=+*#"
  local line = {}
  for i = 1, #history do
    local step = math.floor(math.min(1, history[i]) * (#marks - 1) + 0.5) + 1
    line[i] = marks:sub(step, step)
  end
  put(0, ROWS - 3, "USE OVER TIME (newest on the right)", GREY)
  put(0, ROWS - 2, table.concat(line), WHITE)

  if grid.fuse then
    blink = not blink
    local text = "FUSE BLOWN - THE POWER IS OFF"
    local x = math.max(0, math.floor((COLUMNS - #text) / 2))
    if blink then
      gpu:setBackground(1, 0.1, 0.1, 1)
      put(0, ROWS - 5, string.rep(" ", COLUMNS), WHITE)
      put(x, ROWS - 5, text, WHITE)
      gpu:setBackground(0, 0, 0, 1)
    else
      put(x, ROWS - 5, text, RED)
    end
    if BEEP then computer.beep(1.0) end
  end

  gpu:flush()
end

---------------------------------------------------------------- main
openDisplay()
print("Power board running: " .. TITLE)

while true do
  local ok, grid = pcall(read)
  if not ok then
    print("Power board: reading failed: " .. tostring(grid))
    connector = nil
    grid = nil
  end
  local okDraw, err = pcall(draw, grid)
  if not okDraw then print("Power board: drawing failed: " .. tostring(err)) end
  event.pull(REFRESH)
end
```
{% endraw %}

</details>

<details markdown="1"><summary><code>sign-line.lua</code> (276 lines)</summary>

{% raw %}
```lua
-- SIGN LINE (FicsIt-Networks 1.3.0, Lua)
--
-- Writes one live line of text onto ordinary in-game signs. Needs no graphics
-- card and no screen, so it is the cheapest of the set.
--
-- What a sign shows is decided by its nickname:
--   line power            POWER 320 / 450 MW  71 %      (or FUSE BLOWN)
--   line hall             10 of 12 running  92 %
--   line hall smelt       the same, only machines whose nickname contains smelt
--   line stock            the emptiest container: Iron Plate 12 %
--   line stock ore        the same, only containers whose nickname contains ore
--   line item Iron Plate  Iron Plate 118 / min          (made on this network)
--
-- BUILD
--   1. A Computer Case with one Lua CPU and one Memory T1 placed into it.
--   2. Any of the game's signs. In the sign's own window pick a layout that has a
--      text field and type a single # into the field the line should go to.
--   3. Network Cable from the Computer Case to each sign, and to what the signs
--      report on: the machines, the Storage Containers, and one power pole (or
--      any machine) of the grid.
--   4. With the Network Manager in hand, click each sign and give it one of the
--      nicknames above.
--   5. Paste this whole file into the Text EEPROM of the computer and press the
--      power button.
--
-- CHANGE ONLY THIS BLOCK
local WORD    = "line"     -- signs whose nickname starts with this word are written
local MARKER  = "#"        -- the text you typed into the field to be replaced
local ELEMENT = ""         -- "" = find the field by MARKER; or the field's exact name
local REFRESH = 10         -- seconds between updates
local RESCAN  = 60         -- seconds between looking for added or removed things
-- NOTHING BELOW NEEDS EDITING

---------------------------------------------------------------- finding things
local function proxies(query, class)
  local list = {}
  for _, id in ipairs(component.findComponent(query) or {}) do
    local obj = component.proxy(id)
    if obj then
      local keep = true
      if class then
        local ok, answer = pcall(function() return obj:isA(class) end)
        keep = ok and answer
      end
      if keep then list[#list + 1] = obj end
    end
  end
  return list
end

local function words(text)
  local list = {}
  for word in tostring(text or ""):gmatch("%S+") do list[#list + 1] = word end
  return list
end

---------------------------------------------------------------- power
local function powerLine()
  local plug = nil
  for _, name in ipairs({"FGBuildablePowerPole", "PowerStorage", "CircuitSwitch", "Factory"}) do
    local class = classes[name]
    if class then
      for _, obj in ipairs(proxies(class)) do
        local ok, list = pcall(function() return obj:getPowerConnectors() end)
        if ok and list then
          for _, candidate in ipairs(list) do
            local okCircuit, circuit = pcall(function() return candidate:getCircuit() end)
            if okCircuit and circuit then plug = candidate break end
          end
        end
        if plug then break end
      end
    end
    if plug then break end
  end
  if not plug then return "POWER: nothing to read" end
  local circuit = plug:getCircuit()
  if not circuit then return "POWER: nothing to read" end
  if circuit.isFuesed then return "FUSE BLOWN" end   -- the game's own spelling
  local used, capacity = circuit.consumption or 0, circuit.capacity or 0
  local share = capacity > 0 and (used / capacity * 100) or 0
  return string.format("POWER %.0f / %.0f MW  %.0f %%", used, capacity, share)
end

---------------------------------------------------------------- machines
local progressSeen = {}   -- machine id -> last progress

local function machines(group)
  local class = classes.Manufacturer
  if group and group ~= "" then return proxies(group, class) end
  return proxies(class)
end

local function hallLine(group)
  local total, running, pctSum, pctCount = 0, 0, 0, 0
  for _, machine in ipairs(machines(group)) do
    local ok = pcall(function()
      total = total + 1
      local id = machine.id
      local progress = machine.progress or 0
      local before = progressSeen[id]
      progressSeen[id] = progress
      if before ~= nil and math.abs(progress - before) > 0.0001 and not machine.standby then
        running = running + 1
      end
      local productivity = machine.productivity or 0
      if productivity > 1.5 then productivity = productivity / 100 end   -- accept 0..1 or 0..100
      pctSum, pctCount = pctSum + productivity, pctCount + 1
    end)
    if not ok then total = total - 1 end
  end
  if total <= 0 then return "no machines" end
  local average = pctCount > 0 and (pctSum / pctCount * 100) or 0
  return string.format("%d of %d running  %.0f %%", running, total, average)
end

local function itemLine(itemName)
  local now, full, found = 0, 0, false
  local wanted = itemName:lower()
  for _, machine in ipairs(machines(nil)) do
    pcall(function()
      local recipe = machine:getRecipe()
      if not recipe then return end
      local cycle = machine.cycleTime or 0
      if cycle <= 0 then return end
      local productivity = machine.productivity or 0
      if productivity > 1.5 then productivity = productivity / 100 end
      local boost = machine.currentProductionBoost or 1
      if boost <= 0 then boost = 1 end
      for _, product in ipairs(recipe:getProducts() or {}) do
        local itemType = product.type
        if itemType and tostring(itemType.name):lower() == wanted then
          local amount = product.amount or 0
          if itemType.form == 2 or itemType.form == 3 then amount = amount / 1000 end
          local rate = amount * boost * 60 / cycle
          now, full, found = now + rate * productivity, full + rate, true
        end
      end
    end)
  end
  if not found then return itemName .. ": not made here" end
  return string.format("%s %.0f / min", itemName, now)
end

---------------------------------------------------------------- storage
local function stockLine(group)
  local class = classes.FGBuildableStorage
  local list
  if group and group ~= "" then
    list = proxies(group, class)
  elseif class then
    list = proxies(class)
  else
    list = {}
  end
  local worstName, worstPct = nil, nil
  for _, container in ipairs(list) do
    pcall(function()
      local inventory, slots = nil, 0
      for _, candidate in ipairs(container:getInventories() or {}) do
        local size = candidate.size or 0
        if size > slots then inventory, slots = candidate, size end
      end
      if not inventory then return end
      local count = inventory.itemCount or 0
      local name, stackSize = nil, 0
      for slot = 0, slots - 1 do
        local stack = inventory:getStack(slot)
        local itemType = stack and stack.item and stack.item.type
        if itemType and stack.count > 0 then
          name, stackSize = itemType.name, itemType.max or 0
          break
        end
      end
      local nick = container.nick
      if nick and nick ~= "" and group and group ~= "" then
        local rest = {}
        for _, word in ipairs(words(nick)) do
          if word ~= group then rest[#rest + 1] = word end
        end
        nick = table.concat(rest, " ")
      end
      if nick and nick ~= "" then name = nick end
      local pct = 0
      if stackSize > 0 then pct = math.min(100, count / (slots * stackSize) * 100) end
      if worstPct == nil or pct < worstPct then worstName, worstPct = name or "(empty)", pct end
    end)
  end
  if worstPct == nil then return "no containers" end
  return string.format("%s %.0f %%", worstName, worstPct)
end

---------------------------------------------------------------- signs
local signs = {}          -- { obj, id, nick, element, last }
local lastScan = nil

local function scanSigns()
  local class = classes.WidgetSign
  local old = {}
  for _, entry in ipairs(signs) do old[entry.id] = entry end
  local found = {}
  for _, obj in ipairs(proxies(WORD, class)) do
    local id = obj.id
    local entry = old[id] or { obj = obj, id = id }
    entry.nick = obj.nick or ""
    found[#found + 1] = entry
  end
  signs = found
end

local function textFor(nick)
  local parts = words(nick)
  local kind = parts[2] or ""
  local rest = table.concat(parts, " ", 3)
  if kind == "power" then return powerLine() end
  if kind == "hall" then return hallLine(rest) end
  if kind == "stock" then return stockLine(rest) end
  if kind == "item" and rest ~= "" then return itemLine(rest) end
  return "nickname: " .. WORD .. " power | hall | stock | item NAME"
end

-- which text field of this sign gets the line
local function pickElement(entry, names, values)
  if ELEMENT ~= "" then return ELEMENT end
  if entry.element then
    for _, name in ipairs(names) do
      if name == entry.element then return name end
    end
  end
  for i, name in ipairs(names) do
    if values[i] == MARKER or (entry.last and values[i] == entry.last) then return name end
  end
  if #names == 1 then return names[1] end
  return nil
end

local function write(entry, text)
  if entry.last == text and entry.element then return end
  local sign = entry.obj
  local data = sign:getPrefabSignData()
  local names, values = data:getTextElements()
  names, values = names or {}, values or {}
  local element = pickElement(entry, names, values)
  if not element then
    if not entry.warned then
      print("Sign line: sign '" .. entry.nick .. "' has no field holding " .. MARKER .. ". Type " .. MARKER .. " into the field to use.")
      entry.warned = true
    end
    return
  end
  data:setTextElement(element, text)
  sign:setPrefabSignData(data)
  entry.element, entry.last, entry.warned = element, text, nil
end

---------------------------------------------------------------- main
print("Sign line running")

while true do
  local now = computer.millis()
  if lastScan == nil or now - lastScan >= RESCAN * 1000 then
    local ok, err = pcall(scanSigns)
    if not ok then print("Sign line: scan failed: " .. tostring(err)) end
    lastScan = now
  end

  for _, entry in ipairs(signs) do
    local ok, err = pcall(function() write(entry, textFor(entry.nick)) end)
    if not ok then
      print("Sign line: '" .. tostring(entry.nick) .. "': " .. tostring(err))
      lastScan = nil
    end
  end

  event.pull(REFRESH)
end
```
{% endraw %}

</details>

<details markdown="1"><summary><code>stock-board.lua</code> (296 lines)</summary>

{% raw %}
```lua
-- STOCK BOARD (FicsIt-Networks 1.3.0, Lua)
--
-- Shows every storage container on this computer's network: what is in it and
-- how full it is, red when nearly empty and amber when nearly full.
--
-- BUILD
--   1. A Computer Case with one Lua CPU, one Memory T1 and one Graphical
--      Processing Unit T1 placed into it.
--   2. A Large Screen to draw on. To try the program before you have one, place
--      a Screen Driver into the Computer Case: the picture then shows inside
--      the computer's own window.
--   3. Network Cable from the Computer Case to the Large Screen and to each
--      Storage Container (the plain and the Industrial one take a cable; a small
--      plug appears on the container). Containers can be daisy-chained.
--   4. Paste this whole file into the Text EEPROM of the computer and press the
--      power button.
--   Optional: with the Network Manager in hand, click a container and give it a
--   nickname. The board shows that name in place of the item's name.
--
-- CHANGE ONLY THIS BLOCK
local TITLE   = "STOCK"    -- heading on the board
local SCREEN  = ""         -- "" = the first Large Screen found on the network;
                           -- or the nickname you gave the one to draw on
local GROUP   = ""         -- "" = every storage container on the network; a word =
                           -- only containers whose nickname contains that word
local LOW     = 10         -- per cent: at or below this the line is red
local HIGH    = 95         -- per cent: at or above this the line is amber
local COLUMNS = 70         -- characters across (at most 300)
local ROWS    = 24         -- lines down (at most 100)
local REFRESH = 10         -- seconds between redraws
local RESCAN  = 60         -- seconds between looking for added or removed containers
-- NOTHING BELOW NEEDS EDITING

local WHITE, GREY   = {1, 1, 1}, {0.45, 0.45, 0.45}
local GREEN, AMBER  = {0.2, 1, 0.3}, {1, 0.75, 0.1}
local RED, BLUE     = {1, 0.2, 0.15}, {0.4, 0.75, 1}

---------------------------------------------------------------- display
local gpu

local function firstProxy(query)
  local ids = component.findComponent(query)
  if ids and ids[1] then return component.proxy(ids[1]) end
  return nil
end

local function findScreen()
  if SCREEN ~= "" then
    local s = firstProxy(SCREEN)
    if s then return s end
  end
  local class = classes.Screen
  if class then
    local s = firstProxy(class)
    if s then return s end
  end
  local driver = classes.FINComputerScreen
  if driver then return computer.getPCIDevices(driver)[1] end
  return nil
end

-- This build cannot draw on the game's own signs: binding one only blanks it.
local function refuseSign(screen, who)
  local signClass = classes.WidgetSign
  if not signClass then return end
  local ok, isSign = pcall(function() return screen:isA(signClass) end)
  if ok and isSign then
    computer.panic(who .. ": '" .. SCREEN .. "' is one of the game's own signs. Use a Large Screen (sign-line.lua writes to signs).")
  end
end

local function openDisplay()
  local class = classes.GPUT1
  gpu = class and computer.getPCIDevices(class)[1]
  if not gpu then computer.panic("Stock board: no Graphical Processing Unit T1 in this computer.") end
  local screen = findScreen()
  if not screen then computer.panic("Stock board: no Large Screen on this network and no Screen Driver in this computer (SCREEN = '" .. SCREEN .. "').") end
  refuseSign(screen, "Stock board")
  gpu:bindScreen(screen)
  gpu:setSize(COLUMNS, ROWS)
end

local function cut(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n <= width then return text .. string.rep(" ", width - n) end
  local stop = utf8.offset(text, width + 1)
  return stop and text:sub(1, stop - 1) or text:sub(1, width)
end

local function right(text, width)
  text = tostring(text)
  local n = utf8.len(text) or #text
  if n >= width then return cut(text, width) end
  return string.rep(" ", width - n) .. text
end

local function put(x, y, text, colour)
  if y < 0 or y >= ROWS or x >= COLUMNS then return end
  colour = colour or WHITE
  gpu:setForeground(colour[1], colour[2], colour[3], 1)
  gpu:setText(x, y, cut(text, math.min(utf8.len(tostring(text)) or #tostring(text), COLUMNS - x)))
end

local function clear()
  gpu:setBackground(0, 0, 0, 1)
  gpu:setForeground(1, 1, 1, 1)
  gpu:fill(0, 0, COLUMNS, ROWS, " ")
end

---------------------------------------------------------------- containers
local containers = {}    -- { obj, id, nick, inventory, itemName, stackSize }
local lastScan = nil

local function label(nick)
  if not nick or nick == "" then return nil end
  if GROUP == "" then return nick end
  local words = {}
  for word in nick:gmatch("%S+") do
    if word ~= GROUP then words[#words + 1] = word end
  end
  if #words == 0 then return nil end
  return table.concat(words, " ")
end

-- the inventory with the most slots is the storage itself
local function storageInventory(obj)
  local best, bestSize = nil, 0
  for _, inventory in ipairs(obj:getInventories() or {}) do
    local size = inventory.size or 0
    if size > bestSize then best, bestSize = inventory, size end
  end
  return best
end

local function scan()
  local class = classes.FGBuildableStorage
  local ids
  if GROUP ~= "" then
    ids = component.findComponent(GROUP)
  elseif class then
    ids = component.findComponent(class)
  else
    ids = {}
  end
  local old = {}
  for _, entry in ipairs(containers) do old[entry.id] = entry end
  local found = {}
  for _, id in ipairs(ids or {}) do
    local obj = component.proxy(id)
    if obj then
      local isStorage = true
      if class then
        local ok, answer = pcall(function() return obj:isA(class) end)
        isStorage = ok and answer
      end
      if isStorage then
        local entry = old[id] or { obj = obj, id = id }
        entry.nick = label(obj.nick)
        if not entry.inventory then
          local ok, inventory = pcall(storageInventory, obj)
          entry.inventory = ok and inventory or nil
        end
        if entry.inventory then found[#found + 1] = entry end
      end
    end
  end
  containers = found
end

-- look through the slots until one holds something; that item names the container
local function learnItem(entry)
  local inventory = entry.inventory
  for slot = 0, inventory.size - 1 do
    local stack = inventory:getStack(slot)
    local itemType = stack and stack.item and stack.item.type
    if itemType and stack.count > 0 then
      entry.itemName = itemType.name
      entry.stackSize = itemType.max or 0
      entry.fluid = (itemType.form == 2 or itemType.form == 3)
      return
    end
  end
end

-- one container -> { name, item, count, capacity, pct }
local function read(entry)
  local inventory = entry.inventory
  local count = inventory.itemCount or 0
  if count > 0 and (not entry.itemName or entry.wasEmpty) then learnItem(entry) end
  entry.wasEmpty = (count == 0)
  local row = { name = entry.nick or entry.itemName or "(empty)", item = entry.itemName or "", count = count }
  local capacity = (inventory.size or 0) * (entry.stackSize or 0)
  if capacity > 0 then
    row.capacity = capacity
    row.pct = math.min(100, count / capacity * 100)
  elseif count == 0 then
    row.pct = 0
  end
  if entry.fluid then
    row.count = count / 1000
    if row.capacity then row.capacity = row.capacity / 1000 end
  end
  return row
end

---------------------------------------------------------------- drawing
local page = 0

local function bar(pct, width)
  local filled = math.floor(pct / 100 * width + 0.5)
  if filled > width then filled = width end
  return "[" .. string.rep("#", filled) .. string.rep("-", width - filled) .. "]"
end

local function draw(rows)
  clear()
  local low, high = 0, 0
  for _, row in ipairs(rows) do
    if row.pct and row.pct <= LOW then low = low + 1 end
    if row.pct and row.pct >= HIGH then high = high + 1 end
  end
  local summary = string.format("%d containers  %d low  %d full", #rows, low, high)
  put(0, 0, TITLE, BLUE)
  put(math.max(#TITLE + 2, COLUMNS - #summary), 0, summary, WHITE)
  put(0, 1, string.rep("-", COLUMNS), GREY)

  local barW = math.max(6, math.min(20, math.floor(COLUMNS * 0.22)))
  local pctW, countW = 6, 17
  local nameW = math.max(8, COLUMNS - barW - 2 - pctW - countW - 3)
  local x1, x2, x3 = nameW + 1, nameW + countW + 2, nameW + countW + barW + 5
  put(0, 2, cut("CONTAINER", nameW), GREY)
  put(x1, 2, right("HOLDS / ROOM", countW), GREY)
  put(x3, 2, right("FILL", pctW), GREY)

  local listTop = 3
  local listLines = math.max(1, ROWS - listTop)
  local pages = math.max(1, math.ceil(#rows / listLines))
  if page >= pages then page = 0 end
  local from = page * listLines
  for line = 1, listLines do
    local row = rows[from + line]
    if not row then break end
    local y = listTop + line - 1
    local colour = GREEN
    if row.pct == nil then colour = GREY
    elseif row.pct <= LOW then colour = RED
    elseif row.pct >= HIGH then colour = AMBER end
    local name = row.name
    if row.item ~= "" and row.item ~= row.name then name = row.name .. " (" .. row.item .. ")" end
    put(0, y, cut(name, nameW), WHITE)
    local amount = string.format("%.0f", row.count)
    if row.capacity then amount = amount .. " / " .. string.format("%.0f", row.capacity) end
    put(x1, y, right(amount, countW), WHITE)
    if row.pct then
      put(x2, y, bar(row.pct, barW), colour)
      put(x3, y, right(string.format("%.0f %%", row.pct), pctW), colour)
    end
  end
  if pages > 1 then
    local note = string.format("page %d of %d", page + 1, pages)
    put(math.max(0, x2), 2, cut(note, barW + 2), GREY)
    page = page + 1
  end
  gpu:flush()
end

---------------------------------------------------------------- main
openDisplay()
print("Stock board running: " .. TITLE)

while true do
  local now = computer.millis()
  if lastScan == nil or now - lastScan >= RESCAN * 1000 then
    local ok, err = pcall(scan)
    if not ok then print("Stock board: scan failed: " .. tostring(err)) end
    lastScan = now
  end

  local rows = {}
  for _, entry in ipairs(containers) do
    local ok, row = pcall(read, entry)
    if ok then
      rows[#rows + 1] = row
    else
      entry.inventory = nil
      lastScan = nil   -- look again on the next round
    end
  end
  table.sort(rows, function(a, b) return a.name < b.name end)

  local ok, err = pcall(draw, rows)
  if not ok then print("Stock board: drawing failed: " .. tostring(err)) end

  event.pull(REFRESH)
end
```
{% endraw %}

</details>
