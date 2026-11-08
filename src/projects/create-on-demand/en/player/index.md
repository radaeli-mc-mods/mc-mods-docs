---
title: Install and use
description: "Install Create: On Demand and request products from a Create factory."
---

# Install and use

## Requirements

- **Minecraft 1.20.1:** Forge **47.4.0** or newer and Create **6.0.8**.
- **Minecraft 1.21.1:** NeoForge **21.1.236** or newer and Create **6.0.10**.
- Install the matching Create: On Demand JAR on both the client and server.

## Set up your factory

1. Configure recipes on your Factory Gauges and connect the ingredient gauges.
2. Leave gauges in **Maintain stock and accept orders** to publish their recipes for orders. New gauges use this mode by default. Choose **Maintain stock** on gauges that should not accept orders; their normal stock slider continues to work.
3. Build and power the machines. Route ingredients to their processing addresses and return finished products to storage monitored by the producing gauge's network.

Create: On Demand follows the gauge connections you configured. It does not discover recipes from JEI, build or power machines, route items, or load chunks.

## Request a product

1. Open the **Stock Keeper** and choose **All** or **Craftable**. Craftable products appear with a green mark, including products with no stock.
2. Click a craftable product with zero stock. To request fresh crafting while stock is available, use **Ctrl + left-click**.
3. Choose a quantity and review the preview. It lists **Items to craft** in production order or **Missing materials** if supplies are short.
4. Confirm. An order with missing materials waits for them to be replenished. In the **Orders** panel, track active work or cancel an order.

The requested amount means that many new final products. Recipe batches may make extras, which stay in storage. Ingredients already in storage are reused. Cancelling stops work that has not been sent; it does not recover ingredients already in transit.

## Deliver an order

Enter an address in the Stock Keeper before confirming the order. When the requested quantity returns to the producing network, Packagers send exactly that quantity to the saved address, possibly in several boxes. Surplus stays in storage. The Orders panel shows the destination and packaging progress. Without an address, finished products remain in storage.

## Configuration

The mod has no editable configuration files. The order mode is selected on each Factory Gauge's recipe screen; see [Configuration](configuration) for details.
