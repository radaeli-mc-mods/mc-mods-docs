---
title: Configuration
description: "How to control Create: Aeronautics Easy Pressure Curve."
---

# Configuration

Version 0.1.0 does not add editable configuration files for players or server administrators. The curve is controlled in game with the [curve editor](./#edit-the-curve-on-a-graph) and the [`/pressurecurve` command](./#commands), both of which need operator permission (level 2) to change anything.

## Key binding

| Control | Default | Where to change it |
| --- | --- | --- |
| Open pressure curve editor | `F9` | Options → Controls → Key Binds → Aeronautics Easy Pressure Curve (client). |

The key only works in game with no screen open, and only for operators (level 2).

The curves you set are saved in the world, in `data/create_aeronautics_easy_pressure_curve.dat`. This is game state, not a configuration file: change curves with the command instead of editing it.

The datapack that supplies the starting curve is Sable's `data/sable/dimension_physics/*.json`. Each file's `pressure_function` is the format `/pressurecurve set` accepts. See [Install and use](./) for the full guide.
