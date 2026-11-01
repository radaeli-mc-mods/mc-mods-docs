---
title: Connected materials
description: Apply, replace, or remove materials across matching face-connected Copycats.
---

# Connected materials

Hold **Bulk Action on Connected Copycats** while right-clicking. The default is **Left Alt**, remappable in **Controls**. The HUD shows a local estimate and highlights the selected positions.

| Action | Hands | Target |
| --- | --- | --- |
| Apply | Wrench and material | Empty Copycat |
| Replace | Wrench and new material | Copycat with the material to replace |
| Remove | Wrench only; other hand empty | Copycat with the material to remove |

For example, place four face-connected Copycats of the same type, hold a Wrench and four stone blocks, then hold the key and right-click the empty group. Up to four positions receive stone, subject to the server limit and permissions. Repeat with another material to replace stone. Empty the material hand to remove the clicked material from the group.

## Selection and limits

- Only six-face connections of the same Copycat type are included; diagonal contact does not connect blocks.
- Applying follows eligible empty targets; replacing/removing follows the clicked material. Other materials remain intact, including different materials on multi-part shapes.
- The server limit defaults to **64 positions**, including the origin, and can be set from **1 to 256**. One multi-part block counts as one position.
- Survival uses the material stack in the selected hand and stops when it runs out. It does not refill from other inventory stacks.
- Unloaded chunks are excluded. A position denied by server interaction or edit permissions is excluded and does not propagate the action through that path.
- The preview does not know server claims, so the actual result can be smaller than the estimate. A permitted alternate connection can still reach a position beyond a blocked path.

[Configuration](configuration) explains how to change the server limit. Hold **Sneak** to bypass replacement and use Create's normal Wrench action.
