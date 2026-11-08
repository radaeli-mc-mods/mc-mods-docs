---
title: Install and use
description: "Install Create: Aeronautics Easy Pressure Curve and change the air pressure curve with /pressurecurve."
---

# Install and use

## Requirements

- Minecraft **1.21.1** with NeoForge **21.1.236** or newer.
- **Sable** 2.0.5 or newer (required).
- **R-Ui Lib** 0.10.0 or newer on clients that install the mod (for the editor screen).
- **Create Aeronautics** 1.3 or newer (optional: it is one of the mods that reads the curve).
- Install the mod on the server (required). On the client it is optional and only adds the editor; then the client needs R-Ui Lib and the server does not.

## How the curve works

Sable computes air pressure as a function of altitude (world Y), defined by points: each has an `altitude`, a pressure `value` and a `slope`. Create Aeronautics reads that pressure for balloons, propellers, burner and steam vent tooltips and the Altitude Sensor, so changing the curve changes how they behave.

A curve you set with this mod:

- applies at once on the server and to all players, including those who join later;
- is saved with the world and kept after reopening the world, restarting the server and `/reload`;
- wins over the datapack for that dimension until you reset it;
- replaces only the pressure; gravity, drag and the rest still come from the datapack.

The `value` of each point is the **real pressure**: the curve you set replaces the datapack's `base_pressure`. For reference, the usual Overworld curve is 1.0 at Y=63.

## Edit the curve on a graph

Press **F9** in game to open the curve editor (change the key in **Options → Controls → Key Binds → Aeronautics Easy Pressure Curve**). It opens on the dimension you are in, and a dropdown at the top lets you pick any other dimension. It opens already filled with the curve in force and its points. Sable's built-in curve is drawn behind it for comparison.

- **Drag a point** to move it and **drag its handles** to change the slope there.
- **Double-click** the graph to add a point, and **right-click** a point (or press Delete) to remove it. Arrow keys nudge the selected point.
- **Max Y** and **Max pressure** choose how much of the graph you see and where points can go.
- **Apply** sends the curve to the server, which saves it and applies it for every player. **Revert** drops your unsaved edits. **Reset to datapack** removes the mod's curve for the dimension. **Close** leaves the screen.

Only operators (level 2) can open the editor; for other players the key does nothing and stays free for other bindings. Altitudes snap to whole blocks and pressures to hundredths.

## Set a curve with commands

You need operator permission (level 2). Run the commands in the dimension you want to change, or add the dimension at the end.

1. Look at the current curve: `/pressurecurve show`. It lists each point with its index and says whether the curve comes from the mod or the datapack.
2. Set a new one with `/pressurecurve set <dimension> <json>`:

   ```text
   /pressurecurve set minecraft:overworld [{"altitude":0,"value":2.0,"slope":0.0},{"altitude":1000,"value":0.2,"slope":0.0}]
   ```

3. Check the result with `/pressurecurve sample 500`. With the curve above it reports `1.10000`.

## Commands

| Command | What it does |
| --- | --- |
| `/pressurecurve show [dimension]` | Lists the points and whether the curve is the mod's or the datapack's. |
| `/pressurecurve sample <altitude> [dimension]` | Pressure at that altitude, as the game computes it. |
| `/pressurecurve set <dimension> <json>` | Replaces the curve with the given array of points. |
| `/pressurecurve point add <altitude> <value> <slope> [dimension]` | Adds a point to the current curve. |
| `/pressurecurve point remove <index> [dimension]` | Removes a point; the first point is `0`. |
| `/pressurecurve copy-datapack [dimension]` | Makes the datapack's curve an editable curve of the mod. |
| `/pressurecurve reset [dimension]` | Removes your curve; the dimension goes back to the datapack. |

The dimension defaults to the one of whoever runs the command (the Overworld from the console). `point add` and `point remove` start from the curve currently in force, whether it is yours or the datapack's.

## Curve rules

- 1 to 64 points.
- Every `altitude` is different (points can be given in any order; they are sorted).
- `altitude`, `value` and `slope` are finite numbers, and `value` is not negative.

A command that breaks a rule or has invalid JSON is rejected with a message and changes nothing.

## Scenario: thin the air for a high-altitude ship

1. `/pressurecurve copy-datapack` turns the current curve into an editable one.
2. `/pressurecurve point add 400 0.05 0` adds a very thin layer at Y=400.
3. `/pressurecurve sample 400` reports the new pressure, which everything that reads Sable's air pressure uses right away.
4. `/pressurecurve reset` brings the datapack curve back.

## Troubleshooting

- **The command does not exist or is denied:** it needs operator level 2, and the mod must be installed with Sable.
- **Players still see the old numbers:** run `/pressurecurve show` and `/pressurecurve sample` on the server first; the mod only has to be on the server, since clients get the curve through Sable. Reconnecting is not needed.
- **My `base_pressure` seems ignored:** that is intended for dimensions with a curve from this mod; put the final value in each point.

See [Configuration](configuration) for what controls the mod.
