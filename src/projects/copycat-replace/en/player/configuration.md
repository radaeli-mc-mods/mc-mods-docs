---
title: Configuration
description: Server action limit, file locations, and reload behavior.
---

# Configuration

The server administrator or singleplayer world owner edits **copycat_replace-server.toml** (TOML). Its limit controls the world's connected actions and is sent to clients for the preview. There is no separate addon client config or additional protection setting.

## File locations

| Variant | Active file |
| --- | --- |
| Forge 1.20.1 / 47.4.0 | `<server>/<world>/serverconfig/copycat_replace-server.toml`, generated when the world loads. In singleplayer: `saves/<world>/serverconfig/`. |
| NeoForge 1.21.1 / 21.1.236 | `config/copycat_replace-server.toml`, generated when SERVER configuration loads. An existing `<world>/serverconfig/copycat_replace-server.toml` overrides it for that world. In singleplayer: `saves/<world>/serverconfig/`. |

For a world-specific NeoForge limit, stop the server or close the world, copy the base file to that world's serverconfig directory, edit the copy, and load the world again. Worlds without an override use the shared base. Creating an override while the world is open takes effect on the next world load. On Forge, `defaultconfigs/copycat_replace-server.toml` can provide the template for newly created world files; it does not replace an existing world's settings.

## Complete defaults

Generated Forge default:

```toml
#Maximum connected Copycat positions affected by one bulk action (1-256).
#Range: 1 ~ 256
max_connected_blocks = 64
```

Generated NeoForge default:

```toml
#Maximum connected Copycat positions affected by one bulk action (1-256).
# Default: 64
# Range: 1 ~ 256
max_connected_blocks = 64
```

## Schema

| Key | Type | Default | Accepted values | Effect |
| --- | --- | --- | --- | --- |
| `max_connected_blocks` | Integer | 64 | 1–256 inclusive, in block positions | Maximum positions affected by one connected apply, replace, or remove action, including the origin. A multi-part block counts once. |

There are no groups or other editable addon keys. A value of 1 limits the group to the origin; 0 and negative values are invalid. Stock, connectivity, type, material, and permissions can further reduce the result. The preview is an estimate and cannot account for unknown server claims.

The loader clamps numbers below 1 to 1 and above 256 to 256; missing keys or incompatible value types use the default 64. Use integers; fractional numeric input may be converted to an integer by the loader. Malformed TOML can trigger loader file recovery or a load error. Back up the file before editing.

## Applying changes

NeoForge watches the active file. Forge also checks this addon's active file every 20 server ticks and waits for two identical reads to handle grouped file-save notifications. A valid reload updates the server rule and sends the new preview limit to connected clients. If config watching is disabled in NeoForge settings, restart the server or reopen the world. Moving or creating a world override also requires loading the world again.

**Bulk Action on Connected Copycats** is remapped in **Controls** and defaults to **Left Alt**; it is not a TOML key. Claim rules are managed by your server's protection mod.

[Connected materials](connected-materials) explains how the limit applies during play.
