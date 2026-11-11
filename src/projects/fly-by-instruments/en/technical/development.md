---
title: Development setup
---

# Development setup

This guide is for people building or extending the mod. Player-facing CC:Tweaked APIs and in-game examples are documented under [For players](../player/computer-craft).

## Build environment

The current source targets Java 21, Minecraft 1.21.1, and NeoForge 21.1.236. Development also uses Create 6.0.10+, Create Aeronautics 1.3+, Sable 2.0.5, CC:Tweaked 1.120.0+, and R-Ui Lib 0.10.0+. Create Aeronautics is installed as its bundled distribution; Create, Aeronautics, Sable, CC:Tweaked, and R-Ui Lib are local compile/runtime dependencies for development.

```powershell
.\gradlew.bat build
.\gradlew.bat runClient
```

The source repository's [development guide](https://github.com/radaelilucca/mc-fly-by-instruments/blob/main/docs/development.md) documents dependency JAR configuration, GameTest tasks, and release scope. Start from the [mod source](https://github.com/radaelilucca/mc-fly-by-instruments).

VS Code also provides the **Run NeoForge Client (without CC:Tweaked)** task.

## Optional CC:Tweaked integration

CC:Tweaked is a compile-time API dependency and an optional runtime integration. The mod registers its computer integration only when `computercraft` is loaded. Core block entities publish through CC-independent event interfaces; peripheral instances are created lazily and cached per block entity.

Use `-PwithoutComputerCraft` to omit CC:Tweaked from the development runtime while retaining the API for compilation. Also remove any manually installed CC:Tweaked JAR from the selected development instance.

```powershell
.\gradlew.bat -PwithoutComputerCraft test
.\gradlew.bat -PwithoutComputerCraft -PtableGameTests runGameTestServer
.\gradlew.bat -PwithoutComputerCraft runClient
```

With this flag, `test` runs the dedicated absence regression test. Run `.\gradlew.bat test build` separately for the full suite with CC:Tweaked.

## Ponder development

The ordinary development client loads PonderJS, KubeJS and Rhino from run/mods. Keep copies in libs for compilation and isolated validation; run the normal client without -PponderTutorials to avoid duplicate mods. Place the supplied versions in libs or set ponderjs_jar, kubejs_jar and rhino_jar. The tutorial integration remains optional for players; see [Ponder tutorials](../player/ponder). The scripts load directly from the mod resources.

The source guide docs/ponder-development.md covers the isolated client harness (runPonderValidationClient -PponderTutorials -PponderValidation), dependency absence checks and dedicated GameTest gate (runPonderValidationServer -PponderServerValidation). Validation harnesses are excluded from normal JARs.
