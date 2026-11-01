---
title: Configuration
---

# Configuration

This reference applies to Aeronautics: Fly by Instruments on Minecraft 1.21.1 / NeoForge.

## aeronautics_fly_by_instruments-server.toml

Format: TOML. The base file is generated in config/ in the instance or server directory. The world owner or server administrator edits it. A file with the same name in saves/&lt;world&gt;/serverconfig/ (singleplayer) or &lt;world&gt;/serverconfig/ (dedicated server) overrides the base configuration for that world. Server values apply to all connected players.

Close the world or stop the server before editing, then reopen/restart to apply the file. Keep values within the inclusive ranges below; NeoForge validates the configuration against this schema and corrects invalid entries during loading.

```toml
#Maximum cable and endpoint blocks visited while discovering one avionics network.
# Default: 4096
# Range: 1 ~ 1000000
maxAvionicsNetworkBlocks = 4096
#Ticks between server-side acquisition sensor scans.
# Default: 5
# Range: 1 ~ 1200
sensorScanIntervalTicks = 5
#Maximum Radar Altimeter range in blocks.
# Default: 128
# Range: 1 ~ 4096
radarAltimeterMaxRange = 128
#Maximum Terrain Scanner range in blocks.
# Default: 128
# Range: 1 ~ 4096
terrainScannerMaxRange = 128
#Block light emitted by a modular table with a fully lit lamp; 0 disables it.
# Default: 5
# Range: 0 ~ 15
lampLightLevel = 5
#Longest Avionics Wire span between two consecutive connectors/supports, in blocks.
# Default: 24
# Range: 2 ~ 64
wireMaxSpan = 24
#Most connectors and supports a single Avionics Wire may pass through, ends included.
# Default: 32
# Range: 2 ~ 128
wireMaxPoints = 32
#Blocks of wire made from one Avionics Wire item (costs round up).
# Default: 8
# Range: 1 ~ 64
wireBlocksPerItem = 8
```

| Key | Type | Default | Accepted values (inclusive) | Effect |
| --- | --- | --- | --- | --- |
| `maxAvionicsNetworkBlocks` | Integer | 4096 | 1–1000000 | Maximum visited nodes/devices in one network discovery. |
| `sensorScanIntervalTicks` | Integer | 5 | 1–1200 | Ticks between sensor scans (20 ticks = 1 second at 20 TPS). |
| `radarAltimeterMaxRange` | Integer | 128 | 1–4096 | Maximum altitude measurement distance, in blocks. |
| `terrainScannerMaxRange` | Integer | 128 | 1–4096 | Maximum scan distance for both terrain scanners, in blocks. |
| `lampLightLevel` | Integer | 5 | 0–15 | Maximum block light from a fully lit panel; 0 disables block light. |
| `wireMaxSpan` | Integer | 24 | 2–64 | Longest span between consecutive wire nodes, in blocks. |
| `wireMaxPoints` | Integer | 32 | 2–128 | Maximum points in a wire route, including both ends. |
| `wireBlocksPerItem` | Integer | 8 | 1–64 | Wire length per item, in blocks; item cost rounds up. |

All keys are top-level integers. There are no groups, lists, string identifiers or enum values in this file. No separate client/common configuration file is registered by the mod.

Per-device ranges, frequencies, aperture, sensitivity, panel indications and waypoints are saved with the devices, not in this file. Wiring View and Ponder keys are set in Minecraft Controls. See the [Ponder tutorials](ponder) and functional player guides.
