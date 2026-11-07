---
title: Ambiente de desenvolvimento
---

# Ambiente de desenvolvimento

Este guia é para quem compila ou estende o mod. As APIs CC:Tweaked usadas durante o jogo e exemplos Lua estão em [Para jogadores](../player/computer-craft).

## Ambiente de build

O código atual usa Java 21, Minecraft 1.21.1 e NeoForge 21.1.236. O desenvolvimento também usa Create 6.0.10+, Create Aeronautics 1.3+, Sable 2.0.5, CC:Tweaked 1.120.0+ e R-Ui Lib 0.9.0+. Create Aeronautics vem incluído no mod; Create, Aeronautics, Sable, CC:Tweaked e R-Ui Lib são dependências locais de compilação/execução durante o desenvolvimento.

```powershell
.\gradlew.bat build
.\gradlew.bat runClient
```

O [guia de desenvolvimento no repositório](https://github.com/radaelilucca/mc-fly-by-instruments/blob/main/docs/development.md) documenta configuração de JARs de dependências, tarefas GameTest e o escopo de release. Comece pelo [código-fonte do mod](https://github.com/radaelilucca/mc-fly-by-instruments).

## Desenvolvimento do Ponder

O cliente de desenvolvimento normal carrega PonderJS, KubeJS e Rhino de run/mods. Mantenha cópias em libs para compilação e validação isolada; execute o cliente normal sem -PponderTutorials para evitar mods duplicados. Coloque as versões indicadas em libs ou ajuste ponderjs_jar, kubejs_jar e rhino_jar. A integração continua opcional para jogadores; veja [Tutoriais Ponder](../player/ponder). Os scripts são carregados diretamente dos recursos do mod.

O guia de origem docs/ponder-development.md explica o cliente isolado (runPonderValidationClient -PponderTutorials -PponderValidation), os testes de ausência das dependências e o GameTest dedicado (runPonderValidationServer -PponderServerValidation). Os harnesses ficam fora dos JARs normais.
