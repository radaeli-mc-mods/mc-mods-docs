# Configuration

RoadWeaver 2.4.1-1.21.1 — NeoForge 1.21.1.

## Main file

`config/roadweaver/roadweaver.json` is JSON. The mod creates it on first launch. On the server it controls generation; the client uses `client` settings for its loading display. Close the game/server before editing and restart to apply file edits. There is no command to reload this file. The settings screen saves edits through `ConfigService.markDirty`; generation edits affect future work and do not rebuild existing chunks.

The following defaults were serialized from `new ModConfig()` on a machine with 16 logical processors. `sharedWorkerThreads` is `max(1,min(4,CPUs−1))`; `initialGenerationThreads` is `max(1,min(128,CPUs))`; `maxConcurrentGenerations` is `max(1,min(2,sharedWorkerThreads))`. Other defaults are fixed.

```json
{
  "structurePrediction": {
    "enabled": true,
    "structureAvoidanceEnabled": true,
    "predictRadiusChunks": 1024,
    "biomePrefilter": true,
    "structureWhitelist": [
      "#minecraft:village"
    ],
    "structureBlacklist": [],
    "villageRoadOffset": 60,
    "otherStructureRoadOffset": 15
  },
  "planning": {
    "initialPlanRadiusChunks": 128,
    "dynamicPlanEnabled": true,
    "dynamicPlanRadiusChunks": 128,
    "dynamicPlanStrideChunks": 64,
    "planningAlgorithm": "RNG",
    "terrainSamplingMode": "COARSE_CORRIDOR",
    "debugRawPaths": false
  },
  "pathfindingCost": {
    "orthoStepCost": 1,
    "diagStepCost": 1.414,
    "elevationWeight": 80,
    "biomeWeight": 2,
    "stabilityWeight": 15,
    "waterDepthWeight": 80,
    "nearWaterCost": 80,
    "waterProximityCost": 20,
    "heuristicWeight": 15,
    "deviationWeight": 0.5,
    "aStarStep": 8,
    "aStarMaxSteps": 200000,
    "pathfindingAlgorithm": "GRADIENT_DESCENT"
  },
  "roadAppearance": {
    "roadsEnabled": true,
    "allowArtificial": true,
    "allowNatural": true,
    "placeWaypoints": false,
    "spawnCabinEnabled": true,
    "averagingRadius": 8,
    "roadWidth": 3,
    "roadSignsEnabled": true,
    "lampInterval": 32,
    "roadClearHeight": 4,
    "tunnelEnabled": false,
    "tunnelClearHeight": 5,
    "preventTreesOnRoad": true,
    "maxSlopeStepPerTwoSegments": 1,
    "slopeLimitEnabled": true
  },
  "bridge": {
    "enabled": true,
    "deckClearance": 2,
    "maxLengthBlocks": 100,
    "useBuoysInstead": false,
    "useBuoysWhenSkipped": false,
    "buoyIntervalBlocks": 32,
    "pierInterval": 6,
    "pierWidth": 1,
    "pierMaxHeight": 20,
    "keepLamps": true,
    "rampSegments": 4,
    "minWaterDepth": 1,
    "minLength": 5,
    "mergeGap": 8
  },
  "performance": {
    "sharedWorkerThreads": 4,
    "initialGenerationThreads": 16,
    "maxConcurrentGenerations": 2,
    "threadDutyCycle": 50,
    "idleGenerationEnabled": false,
    "idleMaxConcurrentGenerations": 1,
    "idleThreadDutyCycle": 20,
    "openclCoarseSamplingEnabled": true,
    "openclAccurateSamplingEnabled": true,
    "openclDevicePreference": "AUTO",
    "openclMinSamples": 1024,
    "openclValidateSamples": false
  },
  "roadsideStructure": {
    "enabled": true,
    "maxStructuresPerRoad": 3,
    "smallStructureOffset": 8,
    "mediumStructureOffset": 12,
    "largeStructureOffset": 16
  },
  "roadsideVillage": {
    "enabled": true,
    "maxVillagesPerRoad": 6,
    "minRoadSegments": 32,
    "windowSegments": 24,
    "targetNodeCountMin": 6,
    "targetNodeCountMax": 14,
    "maxHeightDiff": 4,
    "maxLocalSlope": 4,
    "minCurveAngle": 0,
    "maxCurveAngle": 70,
    "roadBufferBlocks": 6,
    "buildingGapInterval": 3,
    "maxStepHeight": 3,
    "maxDistanceFromCenter": 96,
    "spawnChance": 0.3
  },
  "client": {
    "loadingTipsEnabled": true,
    "loadingProgressEnabled": true,
    "loadingProgressDebugEnabled": false
  }
}
```

Ranges below include both endpoints. The validator clamps values to these ranges except for the special rules after the tables. Use exact enum names. Malformed JSON retains the loaded configuration or startup defaults; it is not automatically converted into a valid file.

### structurePrediction

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `structurePrediction.enabled` | boolean | `true` | true / false; Enables this subsystem |
| `structurePrediction.structureAvoidanceEnabled` | boolean | `true` | true / false; Avoid structures when laying roads |
| `structurePrediction.predictRadiusChunks` | integer | `1024` | [1, 2147483647]; Structure prediction radius, chunks |
| `structurePrediction.biomePrefilter` | boolean | `true` | true / false; Filter structure candidates by biome |
| `structurePrediction.structureWhitelist` | string[] | `["#minecraft:village"]` | Structure IDs, `#namespace:id` tags and wildcards; Structures to connect |
| `structurePrediction.structureBlacklist` | string[] | `[]` | Structure IDs, `#namespace:id` tags and wildcards; Structures to exclude |
| `structurePrediction.villageRoadOffset` | integer | `60` | [0, 2147483647]; Distance from village centers, blocks |
| `structurePrediction.otherStructureRoadOffset` | integer | `15` | [0, 2147483647]; Distance from other structures, blocks |

### planning

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `planning.initialPlanRadiusChunks` | integer | `128` | [1, 2048]; Initial planning radius, chunks |
| `planning.dynamicPlanEnabled` | boolean | `true` | true / false; Plan while players explore |
| `planning.dynamicPlanRadiusChunks` | integer | `128` | [1, 2048]; Exploration planning radius, chunks |
| `planning.dynamicPlanStrideChunks` | integer | `64` | [1, planning.dynamicPlanRadiusChunks]; Movement before replanning, chunks |
| `planning.planningAlgorithm` | string | `"RNG"` | KNN, DELAUNAY, RNG, MST, SNAP_BRANCH; Road network layout algorithm |
| `planning.terrainSamplingMode` | string | `"COARSE_CORRIDOR"` | LEGACY_DIRECT, COARSE_CORRIDOR, FULL_REGION; Terrain planning strategy |
| `planning.debugRawPaths` | boolean | `false` | true / false; Capture paths for debug overlay |

### pathfindingCost

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `pathfindingCost.orthoStepCost` | number | `1` | [0, finite number]; Straight step pathfinding cost |
| `pathfindingCost.diagStepCost` | number | `1.414` | [0, finite number]; Diagonal step pathfinding cost |
| `pathfindingCost.elevationWeight` | integer | `80` | [0, 2147483647]; Elevation penalty weight |
| `pathfindingCost.biomeWeight` | integer | `2` | [0, 2147483647]; Biome penalty weight |
| `pathfindingCost.stabilityWeight` | integer | `15` | [0, 2147483647]; Ground stability penalty weight |
| `pathfindingCost.waterDepthWeight` | integer | `80` | [0, 2147483647]; Water depth penalty weight |
| `pathfindingCost.nearWaterCost` | integer | `80` | [0, 2147483647]; Near-water pathfinding cost |
| `pathfindingCost.waterProximityCost` | integer | `20` | [0, 2147483647]; Stored cost setting; currently only contributes to path cache identity |
| `pathfindingCost.heuristicWeight` | number | `15` | [0, finite number]; Search heuristic weight |
| `pathfindingCost.deviationWeight` | number | `0.5` | [0, finite number]; Route deviation weight |
| `pathfindingCost.aStarStep` | integer | `8` | [4, 128]; Search spacing, blocks |
| `pathfindingCost.aStarMaxSteps` | integer | `200000` | [3000, 200000]; Maximum search iterations |
| `pathfindingCost.pathfindingAlgorithm` | string | `"GRADIENT_DESCENT"` | ASTAR_BASIC, ASTAR_BIDIRECTIONAL, GRADIENT_DESCENT, POTENTIAL_FIELD; Path search algorithm |

### roadAppearance

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `roadAppearance.roadsEnabled` | boolean | `true` | true / false; Enable physical road placement |
| `roadAppearance.allowArtificial` | boolean | `true` | true / false; Allow artificial material presets |
| `roadAppearance.allowNatural` | boolean | `true` | true / false; Allow natural material presets |
| `roadAppearance.placeWaypoints` | boolean | `false` | true / false; Place waypoints |
| `roadAppearance.spawnCabinEnabled` | boolean | `true` | true / false; Generate spawn cabin |
| `roadAppearance.averagingRadius` | integer | `8` | Integer; no clamp in the configuration validator; Height averaging radius, blocks |
| `roadAppearance.roadWidth` | integer | `3` | [0, 15]; Road width setting, blocks |
| `roadAppearance.roadSignsEnabled` | boolean | `true` | true / false; Place road signs |
| `roadAppearance.lampInterval` | integer | `32` | [1, 2048]; Lamp spacing, blocks |
| `roadAppearance.roadClearHeight` | integer | `4` | [1, 16]; Clearance above road, blocks |
| `roadAppearance.tunnelEnabled` | boolean | `false` | true / false; Enable tunnels |
| `roadAppearance.tunnelClearHeight` | integer | `5` | [2, 16]; Tunnel headroom, blocks |
| `roadAppearance.preventTreesOnRoad` | boolean | `true` | true / false; Keep trees out of road space |
| `roadAppearance.maxSlopeStepPerTwoSegments` | integer | `1` | [0, 8]; Allowed rise per two segments, blocks |
| `roadAppearance.slopeLimitEnabled` | boolean | `true` | true / false; Limit road slopes |

### bridge

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `bridge.enabled` | boolean | `true` | true / false; Enables this subsystem |
| `bridge.deckClearance` | integer | `2` | [1, 8]; Bridge clearance above sea level, blocks |
| `bridge.maxLengthBlocks` | integer | `100` | [0, 10000]; Maximum bridge length, blocks |
| `bridge.useBuoysInstead` | boolean | `false` | true / false; Use buoys instead of bridges |
| `bridge.useBuoysWhenSkipped` | boolean | `false` | true / false; Mark skipped bridge spans with buoys |
| `bridge.buoyIntervalBlocks` | integer | `32` | [4, 256]; Buoy spacing, blocks |
| `bridge.pierInterval` | integer | `6` | [3, 32]; Pier spacing, blocks |
| `bridge.pierWidth` | integer | `1` | [1, 3]; Pier width, blocks |
| `bridge.pierMaxHeight` | integer | `20` | [6, 64]; Maximum pier height, blocks |
| `bridge.keepLamps` | boolean | `true` | true / false; Keep lamps on bridges |
| `bridge.rampSegments` | integer | `4` | [0, 12]; Bridge ramp segments |
| `bridge.minWaterDepth` | integer | `1` | Integer; no clamp in the configuration validator; Water depth for bridge detection, blocks |
| `bridge.minLength` | integer | `5` | Integer; no clamp in the configuration validator; Minimum bridge span, segments |
| `bridge.mergeGap` | integer | `8` | Integer; no clamp in the configuration validator; Gap for merging bridge spans, segments |

### performance

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `performance.sharedWorkerThreads` | integer | `4` | [1, 128]; Background worker count |
| `performance.initialGenerationThreads` | integer | `16` | [1, 128]; Initial generation worker count |
| `performance.maxConcurrentGenerations` | integer | `2` | [1, 128]; Concurrent road jobs |
| `performance.threadDutyCycle` | integer | `50` | [1, 100]; Worker duty cycle, percent |
| `performance.idleGenerationEnabled` | boolean | `false` | true / false; Generate roads while idle |
| `performance.idleMaxConcurrentGenerations` | integer | `1` | [1, 8]; Concurrent idle jobs |
| `performance.idleThreadDutyCycle` | integer | `20` | [1, 100]; Idle duty cycle, percent |
| `performance.openclCoarseSamplingEnabled` | boolean | `true` | true / false; Enable OpenCL coarse heights |
| `performance.openclAccurateSamplingEnabled` | boolean | `true` | true / false; Enable OpenCL accurate heights |
| `performance.openclDevicePreference` | string | `"AUTO"` | AUTO, GPU, CPU; Preferred coarse OpenCL device |
| `performance.openclMinSamples` | integer | `1024` | [0, 1100000]; Minimum coarse GPU batch size, samples |
| `performance.openclValidateSamples` | boolean | `false` | true / false; Compare GPU batches with CPU |

### roadsideStructure

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `roadsideStructure.enabled` | boolean | `true` | true / false; Enables this subsystem |
| `roadsideStructure.maxStructuresPerRoad` | integer | `3` | [0, 20]; Maximum roadside structures per road |
| `roadsideStructure.smallStructureOffset` | integer | `8` | [1, 64]; Small structure offset, blocks |
| `roadsideStructure.mediumStructureOffset` | integer | `12` | [1, 64]; Medium structure offset, blocks |
| `roadsideStructure.largeStructureOffset` | integer | `16` | [1, 64]; Large structure offset, blocks |

### roadsideVillage

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `roadsideVillage.enabled` | boolean | `true` | true / false; Enables this subsystem |
| `roadsideVillage.maxVillagesPerRoad` | integer | `6` | [0, 8]; Maximum roadside villages |
| `roadsideVillage.minRoadSegments` | integer | `32` | [32, 512]; Minimum road length, segments |
| `roadsideVillage.windowSegments` | integer | `24` | [24, 256]; Village candidate window, segments |
| `roadsideVillage.targetNodeCountMin` | integer | `6` | [1, 24]; Minimum village node count |
| `roadsideVillage.targetNodeCountMax` | integer | `14` | [roadsideVillage.targetNodeCountMin, 24]; Maximum village node count |
| `roadsideVillage.maxHeightDiff` | integer | `4` | [0, 12]; Maximum village height difference, blocks |
| `roadsideVillage.maxLocalSlope` | integer | `4` | [0, 8]; Maximum local rise, blocks |
| `roadsideVillage.minCurveAngle` | number | `0` | [0.0, 180.0]; Minimum curve angle, degrees |
| `roadsideVillage.maxCurveAngle` | number | `70` | [roadsideVillage.minCurveAngle, 180.0]; Maximum curve angle, degrees |
| `roadsideVillage.roadBufferBlocks` | integer | `6` | [4, 64]; Building setback, blocks |
| `roadsideVillage.buildingGapInterval` | integer | `3` | [2, 8]; Gap between buildings |
| `roadsideVillage.maxStepHeight` | integer | `3` | [1, 6]; Maximum building step height, blocks |
| `roadsideVillage.maxDistanceFromCenter` | integer | `96` | [16, 128]; Maximum distance from village center, blocks |
| `roadsideVillage.spawnChance` | number | `0.3` | [0.0, 1.0]; Village spawn probability |

### client

| Key | Type | Default | Values and effect |
|---|---|---|---|
| `client.loadingTipsEnabled` | boolean | `true` | true / false; Show loading tips |
| `client.loadingProgressEnabled` | boolean | `true` | true / false; Show generation progress |
| `client.loadingProgressDebugEnabled` | boolean | `false` | true / false; Show detailed generation counters |

### Special rules

- Nonpositive prediction radii revert to 1024; negative structure offsets revert to 60/15. Null lists become empty. IDs, tags and wildcards use the mod structure selector; empty lists add no candidates.
- Nonpositive initial radius becomes 64; nonpositive dynamic radius becomes 128. Nonpositive stride is calculated as `max(8,min(256,radius/2))` and limited to the radius.
- `aStarStep < 4` is used as 8; values above 128 are capped at 128.
- Invalid duty cycles become 50 (normal) or 20 (idle). Nonpositive initial threads use the machine default. Unknown, null or empty OpenCL preference becomes `AUTO`; case and surrounding whitespace are normalized.
- `targetNodeCountMax` cannot fall below `targetNodeCountMin`; `maxCurveAngle` cannot fall below `minCurveAngle`.
- Disabling bridges prevents their construction. Zero lengths and parameters without a configuration clamp remain subject to generation consumers; do not use negative numbers to disable features.
- Accurate acceleration requires an FP64 GPU. CPU is used when no compatible device exists or validation differs. The first batch of each accurate program is validated even with `openclValidateSamples=false`.

## Material files

`config/roadweaver/presets/<id>.json` stores one JSON preset per file. The preset editor saves these files. Restart after manual edits. Complete defaults for every generated file follow. `dimensions` may be omitted, empty or `["minecraft:overworld"]`; the loader removes presets specifying other dimensions.

| Key | Type / values | Effect / default |
|---|---|---|
| `id` | string | Identifier; missing/blank uses the file name. Later duplicate IDs are ignored. |
| `name` | string | Editor name; missing/blank uses `id`. |
| `type` | `ARTIFICIAL` / `NATURAL` | Road type; missing/invalid becomes `ARTIFICIAL`. |
| `dimensions` | optional string[] | Omitted by default; Overworld only. |
| `materials` | string[] | Registered block IDs; invalid IDs and air are removed. Presets with no valid material are ignored. |
| `slabMaterials` | string[] | Block IDs, normally slabs; missing/empty remains empty. |

<details>
<summary>stone_street.json</summary>

```json
{
  "id": "stone_street",
  "name": "Stone Street",
  "type": "ARTIFICIAL",
  "materials": [
    "minecraft:stone_bricks",
    "minecraft:polished_andesite"
  ],
  "slabMaterials": [
    "minecraft:stone_brick_slab",
    "minecraft:polished_andesite_slab"
  ]
}
```

</details>

<details>
<summary>mud_road.json</summary>

```json
{
  "id": "mud_road",
  "name": "Mud Road",
  "type": "ARTIFICIAL",
  "materials": [
    "minecraft:mud_bricks",
    "minecraft:packed_mud"
  ],
  "slabMaterials": [
    "minecraft:mud_brick_slab"
  ]
}
```

</details>

<details>
<summary>aged_stone.json</summary>

```json
{
  "id": "aged_stone",
  "name": "Aged Stone",
  "type": "ARTIFICIAL",
  "materials": [
    "minecraft:stone_bricks",
    "minecraft:mossy_stone_bricks",
    "minecraft:cracked_stone_bricks"
  ],
  "slabMaterials": [
    "minecraft:stone_brick_slab",
    "minecraft:mossy_stone_brick_slab"
  ]
}
```

</details>

<details>
<summary>natural_plains.json</summary>

```json
{
  "id": "natural_plains",
  "name": "Plains Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:gravel",
    "minecraft:coarse_dirt"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_sunflower_plains.json</summary>

```json
{
  "id": "natural_sunflower_plains",
  "name": "Sunflower Plains Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:gravel",
    "minecraft:coarse_dirt"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_meadow.json</summary>

```json
{
  "id": "natural_meadow",
  "name": "Meadow Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:moss_block",
    "minecraft:coarse_dirt"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_forest.json</summary>

```json
{
  "id": "natural_forest",
  "name": "Forest Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:rooted_dirt"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_flower_forest.json</summary>

```json
{
  "id": "natural_flower_forest",
  "name": "Flower Forest Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:moss_block"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_birch_forest.json</summary>

```json
{
  "id": "natural_birch_forest",
  "name": "Birch Forest Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:birch_slab"
  ]
}
```

</details>

<details>
<summary>natural_old_growth_birch_forest.json</summary>

```json
{
  "id": "natural_old_growth_birch_forest",
  "name": "Old Growth Birch Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:rooted_dirt"
  ],
  "slabMaterials": [
    "minecraft:birch_slab"
  ]
}
```

</details>

<details>
<summary>natural_dark_forest.json</summary>

```json
{
  "id": "natural_dark_forest",
  "name": "Dark Forest Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:coarse_dirt",
    "minecraft:rooted_dirt",
    "minecraft:podzol"
  ],
  "slabMaterials": [
    "minecraft:dark_oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_cherry_grove.json</summary>

```json
{
  "id": "natural_cherry_grove",
  "name": "Cherry Grove Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:moss_block",
    "minecraft:coarse_dirt"
  ],
  "slabMaterials": [
    "minecraft:cherry_slab"
  ]
}
```

</details>

<details>
<summary>natural_taiga.json</summary>

```json
{
  "id": "natural_taiga",
  "name": "Taiga Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:coarse_dirt",
    "minecraft:podzol",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_old_growth_pine_taiga.json</summary>

```json
{
  "id": "natural_old_growth_pine_taiga",
  "name": "Old Growth Pine Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:podzol",
    "minecraft:coarse_dirt",
    "minecraft:rooted_dirt"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_old_growth_spruce_taiga.json</summary>

```json
{
  "id": "natural_old_growth_spruce_taiga",
  "name": "Old Growth Spruce Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:podzol",
    "minecraft:coarse_dirt",
    "minecraft:rooted_dirt"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_snowy_taiga.json</summary>

```json
{
  "id": "natural_snowy_taiga",
  "name": "Snowy Taiga Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:snow_block",
    "minecraft:coarse_dirt",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_snowy_plains.json</summary>

```json
{
  "id": "natural_snowy_plains",
  "name": "Snowy Plains Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:snow_block",
    "minecraft:packed_ice",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_ice_spikes.json</summary>

```json
{
  "id": "natural_ice_spikes",
  "name": "Ice Spikes Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:packed_ice",
    "minecraft:blue_ice",
    "minecraft:snow_block"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_snowy_slopes.json</summary>

```json
{
  "id": "natural_snowy_slopes",
  "name": "Snowy Slopes Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:snow_block",
    "minecraft:powder_snow",
    "minecraft:stone"
  ],
  "slabMaterials": [
    "minecraft:stone_slab"
  ]
}
```

</details>

<details>
<summary>natural_frozen_peaks.json</summary>

```json
{
  "id": "natural_frozen_peaks",
  "name": "Frozen Peaks Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:packed_ice",
    "minecraft:snow_block",
    "minecraft:stone"
  ],
  "slabMaterials": [
    "minecraft:stone_slab"
  ]
}
```

</details>

<details>
<summary>natural_grove.json</summary>

```json
{
  "id": "natural_grove",
  "name": "Grove Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:snow_block",
    "minecraft:powder_snow",
    "minecraft:dirt_path"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_windswept_hills.json</summary>

```json
{
  "id": "natural_windswept_hills",
  "name": "Windswept Hills Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:stone",
    "minecraft:gravel",
    "minecraft:cobblestone"
  ],
  "slabMaterials": [
    "minecraft:stone_slab",
    "minecraft:cobblestone_slab"
  ]
}
```

</details>

<details>
<summary>natural_windswept_gravelly_hills.json</summary>

```json
{
  "id": "natural_windswept_gravelly_hills",
  "name": "Windswept Gravelly Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:gravel",
    "minecraft:stone",
    "minecraft:cobblestone"
  ],
  "slabMaterials": [
    "minecraft:stone_slab"
  ]
}
```

</details>

<details>
<summary>natural_windswept_forest.json</summary>

```json
{
  "id": "natural_windswept_forest",
  "name": "Windswept Forest Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:coarse_dirt",
    "minecraft:stone",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_stony_peaks.json</summary>

```json
{
  "id": "natural_stony_peaks",
  "name": "Stony Peaks Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:stone",
    "minecraft:calcite",
    "minecraft:andesite"
  ],
  "slabMaterials": [
    "minecraft:stone_slab",
    "minecraft:andesite_slab"
  ]
}
```

</details>

<details>
<summary>natural_jagged_peaks.json</summary>

```json
{
  "id": "natural_jagged_peaks",
  "name": "Jagged Peaks Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:stone",
    "minecraft:snow_block",
    "minecraft:packed_ice"
  ],
  "slabMaterials": [
    "minecraft:stone_slab"
  ]
}
```

</details>

<details>
<summary>natural_desert.json</summary>

```json
{
  "id": "natural_desert",
  "name": "Desert Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:sandstone",
    "minecraft:smooth_sandstone",
    "minecraft:sand",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:sandstone_slab",
    "minecraft:smooth_sandstone_slab"
  ]
}
```

</details>

<details>
<summary>natural_badlands.json</summary>

```json
{
  "id": "natural_badlands",
  "name": "Badlands Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:red_sand",
    "minecraft:terracotta",
    "minecraft:orange_terracotta"
  ],
  "slabMaterials": [
    "minecraft:red_sandstone_slab"
  ]
}
```

</details>

<details>
<summary>natural_eroded_badlands.json</summary>

```json
{
  "id": "natural_eroded_badlands",
  "name": "Eroded Badlands Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:red_sand",
    "minecraft:terracotta",
    "minecraft:red_terracotta"
  ],
  "slabMaterials": [
    "minecraft:red_sandstone_slab"
  ]
}
```

</details>

<details>
<summary>natural_wooded_badlands.json</summary>

```json
{
  "id": "natural_wooded_badlands",
  "name": "Wooded Badlands Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:coarse_dirt",
    "minecraft:terracotta",
    "minecraft:red_sand"
  ],
  "slabMaterials": [
    "minecraft:red_sandstone_slab",
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_jungle.json</summary>

```json
{
  "id": "natural_jungle",
  "name": "Jungle Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:rooted_dirt",
    "minecraft:mud"
  ],
  "slabMaterials": [
    "minecraft:jungle_slab"
  ]
}
```

</details>

<details>
<summary>natural_sparse_jungle.json</summary>

```json
{
  "id": "natural_sparse_jungle",
  "name": "Sparse Jungle Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:jungle_slab"
  ]
}
```

</details>

<details>
<summary>natural_bamboo_jungle.json</summary>

```json
{
  "id": "natural_bamboo_jungle",
  "name": "Bamboo Jungle Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:podzol",
    "minecraft:rooted_dirt"
  ],
  "slabMaterials": [
    "minecraft:bamboo_slab",
    "minecraft:jungle_slab"
  ]
}
```

</details>

<details>
<summary>natural_swamp.json</summary>

```json
{
  "id": "natural_swamp",
  "name": "Swamp Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:mud",
    "minecraft:muddy_mangrove_roots",
    "minecraft:dirt_path"
  ],
  "slabMaterials": [
    "minecraft:mud_brick_slab",
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_mangrove_swamp.json</summary>

```json
{
  "id": "natural_mangrove_swamp",
  "name": "Mangrove Swamp Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:mud",
    "minecraft:muddy_mangrove_roots",
    "minecraft:mangrove_roots"
  ],
  "slabMaterials": [
    "minecraft:mud_brick_slab",
    "minecraft:mangrove_slab"
  ]
}
```

</details>

<details>
<summary>natural_savanna.json</summary>

```json
{
  "id": "natural_savanna",
  "name": "Savanna Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:acacia_slab"
  ]
}
```

</details>

<details>
<summary>natural_savanna_plateau.json</summary>

```json
{
  "id": "natural_savanna_plateau",
  "name": "Savanna Plateau Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:coarse_dirt",
    "minecraft:stone"
  ],
  "slabMaterials": [
    "minecraft:acacia_slab"
  ]
}
```

</details>

<details>
<summary>natural_windswept_savanna.json</summary>

```json
{
  "id": "natural_windswept_savanna",
  "name": "Windswept Savanna Trail",
  "type": "NATURAL",
  "materials": [
    "minecraft:coarse_dirt",
    "minecraft:stone",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:acacia_slab",
    "minecraft:stone_slab"
  ]
}
```

</details>

<details>
<summary>natural_beach.json</summary>

```json
{
  "id": "natural_beach",
  "name": "Beach Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:sand",
    "minecraft:sandstone",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:sandstone_slab"
  ]
}
```

</details>

<details>
<summary>natural_snowy_beach.json</summary>

```json
{
  "id": "natural_snowy_beach",
  "name": "Snowy Beach Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:snow_block",
    "minecraft:sand",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_stony_shore.json</summary>

```json
{
  "id": "natural_stony_shore",
  "name": "Stony Shore Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:stone",
    "minecraft:cobblestone",
    "minecraft:gravel"
  ],
  "slabMaterials": [
    "minecraft:stone_slab",
    "minecraft:cobblestone_slab"
  ]
}
```

</details>

<details>
<summary>natural_river.json</summary>

```json
{
  "id": "natural_river",
  "name": "River Bank Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:dirt_path",
    "minecraft:gravel",
    "minecraft:sand"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

<details>
<summary>natural_frozen_river.json</summary>

```json
{
  "id": "natural_frozen_river",
  "name": "Frozen River Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:packed_ice",
    "minecraft:gravel",
    "minecraft:snow_block"
  ],
  "slabMaterials": [
    "minecraft:spruce_slab"
  ]
}
```

</details>

<details>
<summary>natural_mushroom_fields.json</summary>

```json
{
  "id": "natural_mushroom_fields",
  "name": "Mushroom Fields Path",
  "type": "NATURAL",
  "materials": [
    "minecraft:mycelium",
    "minecraft:dirt_path",
    "minecraft:coarse_dirt"
  ],
  "slabMaterials": [
    "minecraft:oak_slab"
  ]
}
```

</details>

## Tectonic configuration

Tectonic manages its own `config/tectonic.json`. Close the server before editing it. The reference above covers RoadWeaver files; Tectonic settings follow its own documentation. Terrain changes give this fork a new derived-cache identity. Existing chunks and roads remain.
