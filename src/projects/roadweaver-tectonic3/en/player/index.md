# Tectonic 3 compatibility

This guide covers the [RoadWeaver fork](https://github.com/radaelilucca/RoadWeaver-Tectonic3), version 2.4.1-1.21.1, on NeoForge 1.21.1 with Tectonic 3.0.28.

## Install and use

Install this fork's RoadWeaver JAR on the client and server. Use one RoadWeaver JAR per installation. Tectonic remains optional; when installed, it also requires Lithostitched. Tectonic 3.0.28 includes Apollib. Keep the same worldgen mods and configuration on both sides.

Create or open your world. Roads are planned between configured structures. Press **H** to open the road map; its settings button opens configuration. Wait for planning and generation before approaching new road segments.

## Existing worlds

Back up the world before updating mods. Existing chunks and persisted roads remain. Terrain samples, map images and pending path caches are rebuilt under a worldgen identity that includes the effective Tectonic configuration. Roads are applied while new chunks generate; installing the fork does not pave previously explored chunks.

## Terrain and performance

The fork follows Tectonic's configured vertical limits and fluid levels. Both regular and alternate noise scaling are supported. OpenCL is optional: accurate acceleration needs an FP64 GPU, and incompatible devices or numerical mismatches use CPU sampling. Changing the initial planning radius changes the amount of terrain sampled.

Administrators with permission level 2 can run **/roadweaver diagnostics** to see the active generator limits, fluid model, worldgen identity, backend and fallback reason.

See [Configuration](configuration.md) for defaults and all settings.
