# Configurações

RoadWeaver 2.4.1-1.21.1 — NeoForge 1.21.1.

## Arquivo principal

`config/roadweaver/roadweaver.json` é JSON. O mod cria o arquivo na primeira inicialização. No servidor, controla geração; no cliente, as opções `client` controlam a tela de carregamento. Feche o jogo/servidor antes de editar e reinicie para aplicar as alterações por arquivo. Não há comando de recarga deste arquivo. A interface salva alterações com `ConfigService.markDirty`; mudanças na geração afetam trabalhos futuros, não reconstruindo chunks existentes.

O padrão abaixo foi serializado de `new ModConfig()` em uma máquina com 16 processadores lógicos. `sharedWorkerThreads` é `max(1,min(4,CPUs−1))`; `initialGenerationThreads` é `max(1,min(128,CPUs))`; `maxConcurrentGenerations` é `max(1,min(2,sharedWorkerThreads))`. Os demais valores são fixos.

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

Os intervalos abaixo incluem os extremos. Os valores são ajustados para o intervalo pelo validador, exceto as regras especiais após as tabelas. Use nomes exatos de enum. JSON inválido mantém a configuração carregada ou os padrões na inicialização; não é convertido automaticamente em um arquivo válido.

### structurePrediction

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `structurePrediction.enabled` | boolean | `true` | true / false; Ativa este subsistema |
| `structurePrediction.structureAvoidanceEnabled` | boolean | `true` | true / false; Evita estruturas ao traçar estradas |
| `structurePrediction.predictRadiusChunks` | integer | `1024` | [1, 2147483647]; Raio de previsão de estruturas, chunks |
| `structurePrediction.biomePrefilter` | boolean | `true` | true / false; Filtra candidatos a estruturas pelo bioma |
| `structurePrediction.structureWhitelist` | string[] | `["#minecraft:village"]` | IDs de estruturas, tags `#namespace:id` e curingas; Estruturas a conectar |
| `structurePrediction.structureBlacklist` | string[] | `[]` | IDs de estruturas, tags `#namespace:id` e curingas; Estruturas a excluir |
| `structurePrediction.villageRoadOffset` | integer | `60` | [0, 2147483647]; Distância dos centros das vilas, blocos |
| `structurePrediction.otherStructureRoadOffset` | integer | `15` | [0, 2147483647]; Distância de outras estruturas, blocos |

### planning

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `planning.initialPlanRadiusChunks` | integer | `128` | [1, 2048]; Raio do planejamento inicial, chunks |
| `planning.dynamicPlanEnabled` | boolean | `true` | true / false; Planeja enquanto jogadores exploram |
| `planning.dynamicPlanRadiusChunks` | integer | `128` | [1, 2048]; Raio de planejamento na exploração, chunks |
| `planning.dynamicPlanStrideChunks` | integer | `64` | [1, planning.dynamicPlanRadiusChunks]; Movimento antes de replanejar, chunks |
| `planning.planningAlgorithm` | string | `"RNG"` | KNN, DELAUNAY, RNG, MST, SNAP_BRANCH; Algoritmo da rede de estradas |
| `planning.terrainSamplingMode` | string | `"COARSE_CORRIDOR"` | LEGACY_DIRECT, COARSE_CORRIDOR, FULL_REGION; Estratégia de planejamento do terreno |
| `planning.debugRawPaths` | boolean | `false` | true / false; Registra caminhos para a sobreposição de depuração |

### pathfindingCost

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `pathfindingCost.orthoStepCost` | number | `1` | [0, número finito]; Custo de passo reto na busca |
| `pathfindingCost.diagStepCost` | number | `1.414` | [0, número finito]; Custo de passo diagonal na busca |
| `pathfindingCost.elevationWeight` | integer | `80` | [0, 2147483647]; Peso da penalidade de elevação |
| `pathfindingCost.biomeWeight` | integer | `2` | [0, 2147483647]; Peso da penalidade de bioma |
| `pathfindingCost.stabilityWeight` | integer | `15` | [0, 2147483647]; Peso da penalidade de estabilidade |
| `pathfindingCost.waterDepthWeight` | integer | `80` | [0, 2147483647]; Peso da penalidade de profundidade da água |
| `pathfindingCost.nearWaterCost` | integer | `80` | [0, 2147483647]; Custo de busca próximo à água |
| `pathfindingCost.waterProximityCost` | integer | `20` | [0, 2147483647]; Configuração armazenada; atualmente só participa da identidade do cache de caminhos |
| `pathfindingCost.heuristicWeight` | number | `15` | [0, número finito]; Peso da heurística de busca |
| `pathfindingCost.deviationWeight` | number | `0.5` | [0, número finito]; Peso de desvio da rota |
| `pathfindingCost.aStarStep` | integer | `8` | [4, 128]; Espaçamento da busca, blocos |
| `pathfindingCost.aStarMaxSteps` | integer | `200000` | [3000, 200000]; Máximo de iterações da busca |
| `pathfindingCost.pathfindingAlgorithm` | string | `"GRADIENT_DESCENT"` | ASTAR_BASIC, ASTAR_BIDIRECTIONAL, GRADIENT_DESCENT, POTENTIAL_FIELD; Algoritmo da busca de caminhos |

### roadAppearance

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `roadAppearance.roadsEnabled` | boolean | `true` | true / false; Ativa a colocação das estradas |
| `roadAppearance.allowArtificial` | boolean | `true` | true / false; Permite materiais artificiais |
| `roadAppearance.allowNatural` | boolean | `true` | true / false; Permite materiais naturais |
| `roadAppearance.placeWaypoints` | boolean | `false` | true / false; Coloca pontos de referência |
| `roadAppearance.spawnCabinEnabled` | boolean | `true` | true / false; Gera a cabana no spawn |
| `roadAppearance.averagingRadius` | integer | `8` | Inteiro; sem ajuste no validador de configuração; Raio da média de altura, blocos |
| `roadAppearance.roadWidth` | integer | `3` | [0, 15]; Largura da estrada, blocos |
| `roadAppearance.roadSignsEnabled` | boolean | `true` | true / false; Coloca placas na estrada |
| `roadAppearance.lampInterval` | integer | `32` | [1, 2048]; Espaçamento das luminárias, blocos |
| `roadAppearance.roadClearHeight` | integer | `4` | [1, 16]; Espaço livre acima da estrada, blocos |
| `roadAppearance.tunnelEnabled` | boolean | `false` | true / false; Ativa túneis |
| `roadAppearance.tunnelClearHeight` | integer | `5` | [2, 16]; Altura livre do túnel, blocos |
| `roadAppearance.preventTreesOnRoad` | boolean | `true` | true / false; Impede árvores no espaço da estrada |
| `roadAppearance.maxSlopeStepPerTwoSegments` | integer | `1` | [0, 8]; Subida permitida por dois segmentos, blocos |
| `roadAppearance.slopeLimitEnabled` | boolean | `true` | true / false; Limita a inclinação da estrada |

### bridge

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `bridge.enabled` | boolean | `true` | true / false; Ativa este subsistema |
| `bridge.deckClearance` | integer | `2` | [1, 8]; Altura da ponte acima do nível do mar, blocos |
| `bridge.maxLengthBlocks` | integer | `100` | [0, 10000]; Comprimento máximo da ponte, blocos |
| `bridge.useBuoysInstead` | boolean | `false` | true / false; Usa boias no lugar de pontes |
| `bridge.useBuoysWhenSkipped` | boolean | `false` | true / false; Marca trechos de ponte omitidos com boias |
| `bridge.buoyIntervalBlocks` | integer | `32` | [4, 256]; Espaçamento das boias, blocos |
| `bridge.pierInterval` | integer | `6` | [3, 32]; Espaçamento dos pilares, blocos |
| `bridge.pierWidth` | integer | `1` | [1, 3]; Largura dos pilares, blocos |
| `bridge.pierMaxHeight` | integer | `20` | [6, 64]; Altura máxima dos pilares, blocos |
| `bridge.keepLamps` | boolean | `true` | true / false; Mantém luminárias nas pontes |
| `bridge.rampSegments` | integer | `4` | [0, 12]; Segmentos da rampa da ponte |
| `bridge.minWaterDepth` | integer | `1` | Inteiro; sem ajuste no validador de configuração; Profundidade para detectar ponte, blocos |
| `bridge.minLength` | integer | `5` | Inteiro; sem ajuste no validador de configuração; Trecho mínimo de ponte, segmentos |
| `bridge.mergeGap` | integer | `8` | Inteiro; sem ajuste no validador de configuração; Intervalo para unir trechos de ponte, segmentos |

### performance

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `performance.sharedWorkerThreads` | integer | `4` | [1, 128]; Quantidade de workers em segundo plano |
| `performance.initialGenerationThreads` | integer | `16` | [1, 128]; Quantidade de workers na geração inicial |
| `performance.maxConcurrentGenerations` | integer | `2` | [1, 128]; Trabalhos simultâneos de estradas |
| `performance.threadDutyCycle` | integer | `50` | [1, 100]; Fração de atividade dos workers, porcentagem |
| `performance.idleGenerationEnabled` | boolean | `false` | true / false; Gera estradas em tempo ocioso |
| `performance.idleMaxConcurrentGenerations` | integer | `1` | [1, 8]; Trabalhos ociosos simultâneos |
| `performance.idleThreadDutyCycle` | integer | `20` | [1, 100]; Fração de atividade ociosa, porcentagem |
| `performance.openclCoarseSamplingEnabled` | boolean | `true` | true / false; Ativa alturas grosseiras por OpenCL |
| `performance.openclAccurateSamplingEnabled` | boolean | `true` | true / false; Ativa alturas precisas por OpenCL |
| `performance.openclDevicePreference` | string | `"AUTO"` | AUTO, GPU, CPU; Dispositivo preferido para OpenCL grosseiro |
| `performance.openclMinSamples` | integer | `1024` | [0, 1100000]; Lote mínimo da GPU grosseira, amostras |
| `performance.openclValidateSamples` | boolean | `false` | true / false; Compara lotes da GPU com a CPU |

### roadsideStructure

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `roadsideStructure.enabled` | boolean | `true` | true / false; Ativa este subsistema |
| `roadsideStructure.maxStructuresPerRoad` | integer | `3` | [0, 20]; Máximo de estruturas por estrada |
| `roadsideStructure.smallStructureOffset` | integer | `8` | [1, 64]; Afastamento de estruturas pequenas, blocos |
| `roadsideStructure.mediumStructureOffset` | integer | `12` | [1, 64]; Afastamento de estruturas médias, blocos |
| `roadsideStructure.largeStructureOffset` | integer | `16` | [1, 64]; Afastamento de estruturas grandes, blocos |

### roadsideVillage

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `roadsideVillage.enabled` | boolean | `true` | true / false; Ativa este subsistema |
| `roadsideVillage.maxVillagesPerRoad` | integer | `6` | [0, 8]; Máximo de vilas ao longo da estrada |
| `roadsideVillage.minRoadSegments` | integer | `32` | [32, 512]; Comprimento mínimo da estrada, segmentos |
| `roadsideVillage.windowSegments` | integer | `24` | [24, 256]; Janela candidata a vila, segmentos |
| `roadsideVillage.targetNodeCountMin` | integer | `6` | [1, 24]; Quantidade mínima de nós da vila |
| `roadsideVillage.targetNodeCountMax` | integer | `14` | [roadsideVillage.targetNodeCountMin, 24]; Quantidade máxima de nós da vila |
| `roadsideVillage.maxHeightDiff` | integer | `4` | [0, 12]; Desnível máximo da vila, blocos |
| `roadsideVillage.maxLocalSlope` | integer | `4` | [0, 8]; Subida local máxima, blocos |
| `roadsideVillage.minCurveAngle` | number | `0` | [0.0, 180.0]; Ângulo mínimo da curva, graus |
| `roadsideVillage.maxCurveAngle` | number | `70` | [roadsideVillage.minCurveAngle, 180.0]; Ângulo máximo da curva, graus |
| `roadsideVillage.roadBufferBlocks` | integer | `6` | [4, 64]; Recuo das construções, blocos |
| `roadsideVillage.buildingGapInterval` | integer | `3` | [2, 8]; Intervalo entre construções |
| `roadsideVillage.maxStepHeight` | integer | `3` | [1, 6]; Desnível máximo de construção, blocos |
| `roadsideVillage.maxDistanceFromCenter` | integer | `96` | [16, 128]; Distância máxima do centro da vila, blocos |
| `roadsideVillage.spawnChance` | number | `0.3` | [0.0, 1.0]; Probabilidade de gerar vila |

### client

| Chave | Tipo | Padrão | Valores e efeito |
|---|---|---|---|
| `client.loadingTipsEnabled` | boolean | `true` | true / false; Mostra dicas no carregamento |
| `client.loadingProgressEnabled` | boolean | `true` | true / false; Mostra progresso da geração |
| `client.loadingProgressDebugEnabled` | boolean | `false` | true / false; Mostra contadores detalhados da geração |

### Regras especiais

- Raios de previsão não positivos voltam a 1024; offsets de estruturas negativos voltam a 60/15. Listas nulas viram vazias. IDs, tags e curingas seguem a seleção de estruturas do mod; listas vazias não acrescentam candidatos.
- Raio inicial não positivo vira 64; raio dinâmico não positivo vira 128. Stride não positivo é calculado com `max(8,min(256,raio/2))` e limitado ao raio.
- `aStarStep < 4` é usado como 8; valores acima de 128 são limitados a 128.
- Duty cycle inválido vira 50 (normal) ou 20 (ocioso). Threads iniciais não positivas voltam ao padrão da máquina. Preferência OpenCL desconhecida, nula ou vazia vira `AUTO`; maiúsculas/minúsculas e espaços são normalizados.
- `targetNodeCountMax` nunca fica abaixo de `targetNodeCountMin`; `maxCurveAngle` nunca fica abaixo de `minCurveAngle`.
- Desativar pontes impede sua construção. Valores de comprimento zero e parâmetros sem clamp continuam sujeitos aos consumidores de geração; não use valores negativos para tentar desativar recursos.
- A aceleração precisa exige GPU FP64. Sem dispositivo compatível ou com resultados divergentes, a CPU é usada. O primeiro lote de cada programa preciso é validado mesmo com `openclValidateSamples=false`.

## Arquivos de materiais

`config/roadweaver/presets/<id>.json` contém um preset JSON por arquivo. O editor de presets salva esses arquivos. Reinicie após edição manual. Os padrões completos de cada arquivo estão abaixo. `dimensions` pode ser omitido, vazio ou `["minecraft:overworld"]`; presets com outras dimensões são removidos pelo carregador.

| Chave | Tipo / valores | Efeito / padrão |
|---|---|---|
| `id` | string | Identificador; ausente/vazio usa o nome do arquivo. Duplicatas posteriores são ignoradas. |
| `name` | string | Nome no editor; ausente/vazio usa `id`. |
| `type` | `ARTIFICIAL` / `NATURAL` | Tipo de estrada; valor inválido/ausente vira `ARTIFICIAL`. |
| `dimensions` | string[] opcional | Omitido por padrão; apenas Overworld. |
| `materials` | string[] | IDs de blocos registrados; inválidos e ar são descartados. Se não sobrar nenhum, o preset é ignorado. |
| `slabMaterials` | string[] | IDs de blocos, normalmente lajes; ausente/vazio mantém lista vazia. |

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

## Configuração do Tectonic

O Tectonic administra seu próprio `config/tectonic.json`. Feche o servidor antes de alterá-lo. A documentação acima descreve arquivos do RoadWeaver; a configuração do Tectonic segue sua própria documentação. Ao mudar o terreno, os caches derivados do fork usam uma nova identidade. Chunks e estradas existentes permanecem.
