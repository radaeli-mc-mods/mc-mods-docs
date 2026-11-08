---
title: "Create: Aeronautics Easy Pressure Curve"
description: "Change the Sable air pressure curve live, per dimension, without a reboot."
---

# Create: Aeronautics Easy Pressure Curve

[![CurseForge](https://cf.way2muchnoise.eu/title/1792363.svg)](https://www.curseforge.com/minecraft/mc-mods/create-aeronautics-easy-pressure-curve)

Balloons, propellers and burners in Create Aeronautics depend on how thin the air gets with altitude. Sable defines that **air pressure curve** in a datapack. Create: Aeronautics Easy Pressure Curve lets you change it **while the world is running**: the new curve applies at once on the server and to every connected player, without a reboot, a world reload or a full `/reload`. No blocks, items or recipes are added.

**Documentation reflects Create: Aeronautics Easy Pressure Curve 0.1.0.**

| Minecraft | Loader | Requires | Optional |
| --- | --- | --- | --- |
| 1.21.1 | NeoForge 21.1.236 | Sable 2.0.5 or newer; R-Ui Lib 0.10.0 or newer on the client | Create Aeronautics 1.3 or newer |

Install the mod on the server (required). It is optional on the client: players without it connect normally and the curve still applies to them; players who install it (with R-Ui Lib) also get the editor screen.

## For players

- [Install and use](player/): edit the curve on a graph or with `/pressurecurve`, check it, edit single points and reset it.
- [Configuration](player/configuration): the editor key, and the fact that the mod has no configuration files.

## For developers

- [Developer API](technical/api): `PressureCurveService`, `PressureCurve` and the client-to-server payload.

## Changelog

[View release notes](changelog)
