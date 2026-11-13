---
title: Upgrade catalog
description: What each Digital Storage Expansion upgrade does.
---

# Upgrade catalog

The mod adds nine upgrades for Sophisticated Backpacks. Each is a single universal item for its function: link it to AE2, Refined Storage, or Tom's Simple Storage; SCC 1.5.3 or newer is also supported on NeoForge 1.21.1. No separate item is needed for each network.

The icons below show each upgrade unlinked. Once linked, an upgrade's screen darkens and its icon takes the color of its network; see [Linking](linking#how-a-linked-upgrade-looks).

| Icon | Upgrade | What it does |
| --- | --- | --- |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_deposit_upgrade.png" alt="Remote Deposit" width="32"> | **Remote Deposit** | Deposit matching items from the backpack into the linked network with its tab button. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_restock_upgrade.png" alt="Remote Restock" width="32"> | **Remote Restock** | Retrieve matching items from the linked network into the backpack with its tab button. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_pickup_upgrade.png" alt="Remote Pickup" width="32"> | **Remote Pickup** | Route newly collected items that match its filter to the backpack or network. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_magnet_upgrade.png" alt="Remote Magnet" width="32"> | **Remote Magnet** | Collect nearby item drops that match its filter and route them to the backpack or network. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_refill_upgrade.png" alt="Remote Refill" width="32"> | **Remote Refill** | Replenish configured player inventory slots from the backpack or network. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_feeding_upgrade.png" alt="Remote Feeding" width="32"> | **Remote Feeding** | Feed the player carrying the backpack with configured food when hunger or injury conditions call for it. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_alchemy_upgrade.png" alt="Remote Alchemy" width="32"> | **Remote Alchemy** | Automatically use configured consumables when their per-slot conditions are met. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_pump_upgrade.png" alt="Remote Pump" width="32"> | **Remote Pump** | Transfer configured fluids between the backpack tank or network and containers, nearby fluid handlers, or world fluids. Tom's Simple Storage is item-only. |
| <img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrades/remote_crafting_upgrade.png" alt="Remote Crafting" width="32"> | **Remote Crafting** | Choose a recipe in the backpack and fill its empty crafting slots with ingredients from the backpack and linked network. Ingredients already in the grid stay in place. |

With JEI installed on Forge 1.20.1 or NeoForge 1.21.1/26.1.2, Remote Crafting can fill its grid from the backpack, player inventory, and linked network. Hold Shift while using the recipe transfer button to fill as many recipe batches as available items allow. When `Refill crafting grid` is enabled, crafting also retrieves a consumed ingredient from the linked network after local sources run out.

Use [Linking](linking) to connect an upgrade. See [Filters and source priority](filters) for allow/block filters, stored-item matching, and Backpack first versus Linked network first.
On **NeoForge 26.1.2**, all nine upgrades also support **SCC 1.6.5**, with the same plain-fluid limitation for Pump.

For manual controls, batch transfers, and the client visibility setting, see the [Remote Crafting guide](crafting).
