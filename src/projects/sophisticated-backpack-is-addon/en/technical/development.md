---
title: Build and artifact checks
description: Build and inspect the Forge production artifact of Digital Storage Expansion.
---

# Build and artifact checks

This reference covers the Forge 1.20.1 module in the 0.4.1 source tree. Run the Gradle wrapper from the repository root with Java 21 for Gradle and a Java 17 toolchain for Forge compilation and runtime.

```powershell
.\gradlew.bat :forge:build
.\gradlew.bat :forge:verifyForgeProductionJar
.\gradlew.bat :forge:testForgeProductionJarVerification
```

The build includes both artifact checks through `:forge:check`, plus the existing tests and Forge GameTests. The production verifier runs after `reobfJar` and opens its JAR in `forge/build/libs`. The named development artifact in `forge/build/devlibs` is not the distributable.

## What the artifact check establishes

The verifier checks the manifest's `MixinConfigs` declaration, the Mixin configuration's explicit refmap reference, the packaged refmap and accessor class, and the `pickupDelay` mapping to `f_31986_:I` in both the default and `searge` contexts. It also checks the Jar-in-Jar declaration and embedded MixinExtras runtime needed by the pickup context. The bundled version is 0.4.1, with the Jar-in-Jar range `[0.4.1,)` for shared selection.

The regression task rejects temporary copies with a missing refmap reference, missing refmap, missing accessor mapping, incorrect `searge` mapping, missing manifest, missing Jar-in-Jar metadata, or missing MixinExtras declaration. It uses the same verifier as the production task.

To inspect a previously built JAR:

```powershell
.\gradlew.bat :forge:verifyForgeProductionJar -PforgeProductionJar=C:/path/to/addon.jar
```

A relative path is resolved from the repository root. The override changes only the inspected file; the task still depends on `reobfJar`. Invalid artifacts fail the task with an error describing the missing contract.

## Runtime checks

Artifact checks establish packaging, not gameplay compatibility. Load the final JAR in an isolated Java 17 Minecraft 1.20.1 installation with Forge and Sophisticated Core/Backpacks. Test the supported baseline and the exact versions used in a reported issue. Validate the title screen, a new world, and dedicated-server loading separately from development launches.

For Magnet, check infinite pickup delay (`32767`), finite delay, partial transfers, and coexistence with Pickup. Preserve the existing eligibility rules and inspect the first causal error if a later startup failure appears.
