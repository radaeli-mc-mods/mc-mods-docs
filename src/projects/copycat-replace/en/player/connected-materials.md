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

Hold the action key and scroll the mouse wheel to change the mode without changing the selected hotbar slot. The HUD shows the active mode. Release the key to return the wheel to normal hotbar control. The mode is remembered for this connection; reconnecting starts in Connected mode.

| Mode | Selection |
| --- | --- |
| Connected | Six-face connections of the same Copycat type |
| Plane | Same type, in the plane through the clicked position perpendicular to the clicked face |
| All types | Six-face connections across any supported Copycat type |

For a wall, click its front face in Plane mode to stay in that wall layer. For a floor, click the top face. Diagonal contact never connects blocks.

- Applying follows eligible empty targets; replacing/removing follows the clicked material. Other materials remain intact, including different materials on multi-part shapes.
- The server limit defaults to **64 positions**, including the origin, and can be set from **1 to 256**. One multi-part block counts as one position.
- Survival consumes the selected hand stack first, then identical items from the main inventory (hotbar and storage slots). Item tags/components must match; armor and the other hand are excluded. This is always active for group actions, with no extra configuration. Insufficient stock changes only the positions you can pay for. Creative consumes nothing.
- Unloaded chunks are excluded. A position denied by server interaction or edit permissions is excluded and does not propagate the action through that path.
- On Fabric 1.20.1, Open Parties and Claims **0.26.3** can protect Copycats in claimed chunks. A bulk edit stops along a route when it reaches a position you cannot edit.
- The preview does not know server claims, so the actual result can be smaller than the estimate. A permitted alternate connection can still reach a position beyond a blocked path.

[Configuration](configuration) explains how to change the server limit. Hold **Sneak** to bypass replacement and use Create's normal Wrench action.

A rejected material shows a short message above the hotbar. A denied action, unchanged material or exhausted stack does not produce an invalid-material warning.

For example, hold one gold block and keep another 64 identical gold blocks in your main inventory: a permitted group can use all 65, up to the configured position limit. Refunds during that action do not increase its initial material budget. Individual replacements still use only the hand stack.

For multi-part shapes, applying selects a part using the clicked face and the same relative hit coordinates at each position, including across different shapes. Replacing/removing follows all existing parts with the clicked material at each selected position. Other materials remain intact.
