---
title: Developer API
description: "Change a dimension's Sable air pressure curve from your own mod."
---

# Developer API

Verified against Sable 2.0.5 on Minecraft 1.21.1 (NeoForge 21.1.236). Package: `com.radaeli.createaeronauticseasypressurecurve`.

## How it works

Sable evaluates air pressure on every call (`DimensionPhysicsData.getAirPressure`, which is `basePressure × pressureFunction(y)`) and caches nothing. The mod:

1. keeps a copy of the datapack's dimension physics (the baseline);
2. rebuilds Sable's map as baseline plus the saved overrides whenever a curve changes, and sends it to every player;
3. after a datapack reload, captures the new baseline and reapplies the overrides before Sable's own sync (`OnDatapackSyncEvent` at `HIGHEST` priority), so the packet Sable sends already carries them.

An override replaces only `pressure_function` and sets `base_pressure` to `1.0`, so a point's `value` is the real pressure. Overrides are saved in a `SavedData` named `create_aeronautics_easy_pressure_curve`, in the overworld's data storage.

## `PressureCurveService`

| Method | Side | Description |
| --- | --- | --- |
| `Optional<PressureCurve> getOverride(MinecraftServer, ResourceKey<Level>)` | server | The saved override, if any. |
| `PressureCurve getEffective(Level)` | both | The curve in force, with `base_pressure` folded into the values. On the client it reads what Sable synced. |
| `PressureCurve getDatapackCurve(ServerLevel)` | server | The datapack (or Sable default) curve, ignoring any override. |
| `double sample(Level, double altitude)` | both | Pressure at an altitude, as Sable computes it. |
| `void set(MinecraftServer, ResourceKey<Level>, PressureCurve)` | server | Saves the override, rebuilds Sable's map and sends it to all players. |
| `void reset(MinecraftServer, ResourceKey<Level>)` | server | Removes the override and goes back to the datapack. |

`set` and `reset` can be called from any thread; off the server thread the work is queued onto it.

```java
import com.radaeli.createaeronauticseasypressurecurve.PressureCurveService;
import com.radaeli.createaeronauticseasypressurecurve.curve.PressureCurve;
import com.radaeli.createaeronauticseasypressurecurve.curve.PressureCurvePoint;
import java.util.List;
import net.minecraft.server.MinecraftServer;
import net.minecraft.world.level.Level;

void thinAir(MinecraftServer server) {
    PressureCurve curve = new PressureCurve(List.of(
            new PressureCurvePoint(0, 1.0, 0.0),
            new PressureCurvePoint(300, 0.1, 0.0)));
    PressureCurveService.set(server, Level.OVERWORLD, curve);
}
```

This example was checked against the API, not compiled as a separate project.

## `PressureCurve`

A record of `List<PressureCurvePoint(altitude, value, slope)>`. It is always valid: 1 to 64 points, finite numbers, `value >= 0` and strictly increasing altitudes (points are sorted; two on the same altitude are rejected). The constructor throws `IllegalArgumentException` otherwise; `PressureCurve.tryCreate(List)` returns a `DataResult` instead.

It has a JSON `CODEC` (an array with the same fields as a Sable `pressure_function`) and a `STREAM_CODEC`. `withPoint`, `withoutPoint(index)` and `scaled(factor)` return new curves, and `toSable()` / `fromSable(...)` convert to and from Sable's `BezierResourceFunction`.

## `SetPressureCurvePayload`

A client-to-server payload (`create_aeronautics_easy_pressure_curve:set_pressure_curve`) with a dimension and an optional curve; an empty curve means reset. The server ignores it unless the sender has permission level 2. Build one with `SetPressureCurvePayload.set(dimension, curve)` or `SetPressureCurvePayload.reset(dimension)`.

## Limits

- Only the public API above is a contract. `SablePressureBridge` is internal.
- The server needs the mod. On the client it is optional: the payload is registered as optional, so clients without the mod can join, and the editor tells players when the server lacks the mod.
