---
title: API para desenvolvedores
description: "Altere a curva de pressão do ar do Sable de uma dimensão a partir do seu mod."
---

# API para desenvolvedores

Verificado com o Sable 2.0.5 no Minecraft 1.21.1 (NeoForge 21.1.236). Pacote: `com.radaeli.createaeronauticseasypressurecurve`.

## Como funciona

O Sable calcula a pressão do ar a cada chamada (`DimensionPhysicsData.getAirPressure`, que é `basePressure × pressureFunction(y)`) e não guarda nada em cache. O mod:

1. guarda uma cópia da física de dimensão do datapack (o baseline);
2. reconstrói o mapa do Sable como baseline mais os overrides salvos sempre que uma curva muda, e o envia a todos os jogadores;
3. depois de um reload de datapack, captura o novo baseline e reaplica os overrides antes da sincronização do próprio Sable (`OnDatapackSyncEvent` com prioridade `HIGHEST`), de modo que o pacote enviado pelo Sable já os leva.

Um override substitui apenas o `pressure_function` e define `base_pressure` como `1.0`, então o `value` de cada ponto é a pressão real. Os overrides ficam em um `SavedData` chamado `create_aeronautics_easy_pressure_curve`, no armazenamento de dados do overworld.

## `PressureCurveService`

| Método | Lado | Descrição |
| --- | --- | --- |
| `Optional<PressureCurve> getOverride(MinecraftServer, ResourceKey<Level>)` | servidor | O override salvo, se houver. |
| `PressureCurve getEffective(Level)` | ambos | A curva em vigor, com o `base_pressure` incorporado aos valores. No cliente, lê o que o Sable sincronizou. |
| `PressureCurve getDatapackCurve(ServerLevel)` | servidor | A curva do datapack (ou padrão do Sable), ignorando qualquer override. |
| `double sample(Level, double altitude)` | ambos | Pressão em uma altitude, como o Sable a calcula. |
| `void set(MinecraftServer, ResourceKey<Level>, PressureCurve)` | servidor | Salva o override, reconstrói o mapa do Sable e o envia a todos os jogadores. |
| `void reset(MinecraftServer, ResourceKey<Level>)` | servidor | Remove o override e volta ao datapack. |

`set` e `reset` podem ser chamados de qualquer thread; fora da thread do servidor, o trabalho é enfileirado nela.

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

Este exemplo foi conferido contra a API, mas não foi compilado como projeto separado.

## `PressureCurve`

Um record de `List<PressureCurvePoint(altitude, value, slope)>`. Ele é sempre válido: de 1 a 64 pontos, números finitos, `value >= 0` e altitudes estritamente crescentes (os pontos são ordenados; dois na mesma altitude são rejeitados). Caso contrário, o construtor lança `IllegalArgumentException`; `PressureCurve.tryCreate(List)` devolve um `DataResult`.

Tem um `CODEC` JSON (um array com os mesmos campos do `pressure_function` do Sable) e um `STREAM_CODEC`. `withPoint`, `withoutPoint(index)` e `scaled(factor)` devolvem novas curvas, e `toSable()` / `fromSable(...)` convertem de e para a `BezierResourceFunction` do Sable.

## `SetPressureCurvePayload`

Um payload do cliente para o servidor (`create_aeronautics_easy_pressure_curve:set_pressure_curve`) com uma dimensão e uma curva opcional; sem curva, significa reset. O servidor o ignora se quem enviou não tiver permissão de nível 2. Monte um com `SetPressureCurvePayload.set(dimension, curve)` ou `SetPressureCurvePayload.reset(dimension)`.

## Limites

- Somente a API pública acima é contrato. `SablePressureBridge` é interna.
- O servidor precisa do mod. No cliente ele é opcional: o payload é registrado como opcional, então clientes sem o mod entram normalmente, e o editor avisa quando o servidor não tem o mod.
