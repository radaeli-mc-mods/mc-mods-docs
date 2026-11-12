---
title: Build and artifact checks
description: Build the three Minecraft targets and run unit tests, native network tests, and artifact checks.
---

# Build and artifact checks

The source tree has independent builds for Forge 1.20.1 (Java 17), NeoForge 1.21.1 (Java 21), and NeoForge 26.1.2 (Java 25). Install all three JDKs, plus Node.js for the artifact verifier. The root Gradle wrapper coordinates the targets:

```powershell
.\gradlew.bat checkAll
.\gradlew.bat buildAll
```

`checkAll` runs the common Java tests and each target's checks. `buildAll` also builds and inspects all three distribution JARs. It does not require `clean`. Project identity and version come from the root `gradle.properties`; `-Pmod_version=<version>` propagates to every target.

Distribution JARs are written to `targets/<minecraft>/<loader>/build/libs/`. Common Java sources and compatible textures are included in each artifact. Backend mods and integration fixtures are not bundled.

## NeoForge 26.1.2 dependencies and profiles

The build uses NeoForge 26.1.2.124, Java 25, ModDevGradle 2.0.148, and Gradle 9.4.0. `targets/26.1.2/dependencies.lock.json` records the audited backend versions, immutable download origins, and SHA-256 hashes. Public artifacts are fetched when missing and verified before compilation. SCC 1.6.5 is versioned under `libs/26.1.2/` with its license. No dependency path points to a Downloads folder.

From `targets/26.1.2`, run one isolated profile:

```powershell
.\gradlew.bat :neoforge:check -PbackendProfile=all
.\gradlew.bat :neoforge:runClient -PbackendProfile=all
.\gradlew.bat :neoforge:runServer -PbackendProfile=all
.\gradlew.bat :neoforge:runRestartVerify -PbackendProfile=all
```

Profiles are `none`, `ae2`, `rs`, `toms`, `scc`, and `all`. Core and Backpacks are always loaded; GuideME is included with AE2. Checks validate the actual loaded backend set, run JUnit with the official ephemeral test server, and run GameTests with native blocks, storage networks, installed upgrades, and native menu or tick flows. Empty or incomplete required profiles and unexpected JUnit skips fail the build.

JUnit XML and HTML reports are under `neoforge/build/test-results/<profile>` and `neoforge/build/reports/tests/<profile>`. Native integration summaries and logs are under `neoforge/build/reports/integration/<profile>`. CI runs all six profiles separately and uploads reports even on failure.

The `all` check also starts two separate JVMs against the same test world. The first saves backpacks with known reservations and uncertain deliveries; the second verifies native backend contents, restores known resources once, and keeps uncertain deliveries quarantined. `runRestartVerify` runs both phases. Their native XML reports and logs are in `neoforge/build/reports/restart/<phase>`. Test-only world-preservation hooks are excluded from the production JAR.

## Artifact checks

From the repository root:

```powershell
.\gradlew.bat verify-forge-1.20.1
.\gradlew.bat verify-neoforge-1.21.1
.\gradlew.bat verify-neoforge-26.1.2
```

The verifier checks metadata, Minecraft and loader identity, version, bytecode, all nine upgrades, recipes, tags, translations, models, local texture references, Mixins, and exclusion of dependency code and test fixtures.

Forge additionally inspects the reobfuscated production JAR, its Mixin refmap and accessor mapping, and the bundled MixinExtras runtime. Seven damaged artifact fixtures exercise the same verifier. To inspect a separate Forge JAR, run from `targets/1.20.1`:

```powershell
.\gradlew.bat :forge:verifyForgeProductionJar -PforgeProductionJar=C:/path/to/addon.jar
.\gradlew.bat :forge:testForgeProductionJarVerification
```

Relative override paths are resolved from `targets/1.20.1`. The named artifact in `forge/build/devlibs` is not the distribution JAR.

Artifact checks and server automation do not establish GUI appearance or multiplayer behavior. Validate screens, synchronized controls, linked icons and animations, and two players with different permissions in a separate client and dedicated-server session. World migration between Minecraft versions is outside this build contract.
