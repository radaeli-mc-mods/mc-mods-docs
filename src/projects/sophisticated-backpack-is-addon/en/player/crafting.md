---
title: Remote Crafting
description: Choose a recipe and fill the backpack crafting grid from available items.
---

# Remote Crafting

The Remote Crafting upgrade replaces the regular Crafting Upgrade in a backpack. Open its tab to choose a recipe and select **Fetch ingredients**. Compatible items already in the 3×3 grid stay in place; the upgrade fills the remaining recipe slots from the backpack and, when linked, its network. The **+** button fetches missing ingredients from the linked network when available. The grid, result, and returned containers use the normal Sophisticated Backpacks crafting screen.

## Use a recipe viewer

With JEI installed, use its recipe transfer button while the backpack screen is open. A regular click transfers one crafting operation. Hold **Shift** to fill stacks for as many complete crafts as the available items and grid slots allow. If there is not enough stock for a complete batch, the upgrade still fills what it can for one recipe.

When the upgrade is linked, the JEI transfer can draw from the backpack, linked network, and your main inventory. Without a linked network, the normal Sophisticated Backpacks transfer remains available.

If **Refill crafting grid** is enabled in Sophisticated Backpacks, crafting checks local sources first and then retrieves a consumed ingredient from the linked network when needed.

## Show or hide manual controls

The tab has a **Show manual controls** / **Hide manual controls** button. It hides or shows the recipe selector and **Fetch ingredients** button without changing the selected recipe, crafting grid, result, source priority, or refill behavior.

The crafting.manualControls setting in [Configuration](configuration) controls the default visibility:

| Value | Behavior |
| --- | --- |
| AUTO | Show the manual controls unless JEI recipe transfer is ready for the open backpack screen. |
| SHOW | Always show the recipe selector and **Fetch ingredients**. |
| HIDE | Always hide the recipe selector and **Fetch ingredients**. |

The tab button saves SHOW or HIDE. To return to AUTO, set that value in the client configuration file.
