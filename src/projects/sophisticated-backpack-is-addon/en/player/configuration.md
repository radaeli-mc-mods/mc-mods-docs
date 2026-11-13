---
title: Configuration
description: Client configuration file and Remote Crafting visibility setting.
---

# Configuration

Digital Storage Expansion provides a client configuration file on Forge 1.20.1 and NeoForge 1.21.1 / 26.1.2. It applies only to the player’s client.

## Client file

- **File:** config/sophisticated_backpacks_digital_storages_expansion-client.toml
- **Format:** TOML
- **Who it affects:** the client where the file is stored; it does not change server settings.
- **Purpose:** controls whether Remote Crafting’s manual recipe selector and **Fetch ingredients** button are shown.

```toml
[crafting]
	#Controls when the recipe selector and Fetch ingredients button are shown.
	#Allowed Values: AUTO, SHOW, HIDE
	manualControls = "AUTO"
```

### crafting.manualControls

| Type | Default | Accepted values | Effect |
| --- | --- | --- | --- |
| Enum | AUTO | AUTO, SHOW, HIDE | AUTO shows manual controls unless JEI transfer is ready for the open backpack screen. SHOW always displays them. HIDE always conceals them. |

The button in the Remote Crafting tab saves an explicit SHOW or HIDE choice. To restore automatic behavior, set manualControls to AUTO in this file. The setting does not change the crafting grid, selected recipe, result, source priority, or refill behavior.

Upgrade filters, source priority, and other function settings are saved on each upgrade item and changed in its backpack tab. See [Filters and source priority](filters), the [upgrade catalog](upgrades), and the [Remote Crafting guide](crafting).

Remote Pump uses Sophisticated Backpacks pump settings for fluid filter slots and throughput calculation. Those settings belong to Sophisticated Backpacks, not this addon; consult that mod’s configuration documentation for their file location and behavior.
