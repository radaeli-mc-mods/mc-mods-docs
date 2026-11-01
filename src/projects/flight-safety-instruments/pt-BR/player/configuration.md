---
title: Configurações
---

# Configurações

Esta referência se aplica ao Fly by Instruments no Minecraft 1.21.1 / NeoForge.

## aeronautics_fly_by_instruments-server.toml

Formato: TOML. O arquivo base é gerado em config/ no diretório da instância ou servidor. O dono do mundo ou administrador edita o arquivo. Um arquivo de mesmo nome em saves/&lt;mundo&gt;/serverconfig/ (singleplayer) ou &lt;mundo&gt;/serverconfig/ (servidor dedicado) substitui a configuração base para esse mundo. Os valores do servidor valem para todos os jogadores conectados.

Feche o mundo ou pare o servidor antes de editar e reabra/reinicie para aplicar o arquivo. Respeite os limites inclusivos abaixo; o NeoForge valida a configuração contra este schema e corrige entradas inválidas durante o carregamento.

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

| Chave | Tipo | Padrão | Valores aceitos (inclusivos) | Efeito |
| --- | --- | --- | --- | --- |
| `maxAvionicsNetworkBlocks` | Inteiro | 4096 | 1–1000000 | Máximo de nós/dispositivos visitados na descoberta de uma rede. |
| `sensorScanIntervalTicks` | Inteiro | 5 | 1–1200 | Ticks entre varreduras dos sensores (20 ticks = 1 segundo a 20 TPS). |
| `radarAltimeterMaxRange` | Inteiro | 128 | 1–4096 | Distância máxima de medição do altímetro, em blocos. |
| `terrainScannerMaxRange` | Inteiro | 128 | 1–4096 | Distância máxima dos dois scanners de terreno, em blocos. |
| `lampLightLevel` | Inteiro | 5 | 0–15 | Luz máxima de bloco do painel totalmente aceso; 0 desativa a luz de bloco. |
| `wireMaxSpan` | Inteiro | 24 | 2–64 | Maior vão entre nós consecutivos do fio, em blocos. |
| `wireMaxPoints` | Inteiro | 32 | 2–128 | Máximo de pontos num fio, incluindo as duas extremidades. |
| `wireBlocksPerItem` | Inteiro | 8 | 1–64 | Comprimento de fio por item, em blocos; custo arredondado para cima. |

Todas as chaves são inteiros no nível principal. Não há grupos, listas, identificadores de texto ou enums neste arquivo. O mod não registra arquivo separado de configuração de cliente/comum.

Faixas, frequências, abertura, sensibilidade, indicações e waypoints são salvos nos dispositivos, não neste arquivo. As teclas Wiring View e Ponder são ajustadas nos Controles do Minecraft. Veja os [Tutoriais Ponder](ponder) e os guias funcionais.
