---
title: Attitude instruments
---

# Attitude instruments

The experimental Attitude Reference Unit measures an aircraft's pitch, roll, heading, turn rate, vertical speed and slip. It publishes readings across the avionics cable network. The experimental Attitude Indicator displays pitch and roll on a Modular Table. Both blocks are creative-only in version 0.4.0-beta.1.

## Attitude Reference Unit

Place the unit on the aircraft and connect a Wire Connector on it to the avionics network. The copper marker identifies its Nose axis; the brass marker identifies Up. These directions must be perpendicular. Use the Create Wrench on a face to set Nose, then use the wrench on the unit again to set Up. The block itself does not need to rotate. A newly placed unit uses the direction you faced for Nose and the block's top for Up.

If the aircraft rests at a small angle, open the unit with an empty hand and choose Calibrate level to treat the current pitch and roll as zero. Calibration is available when both angles are within 15° of level. Reset calibration clears the offsets. Damping cycles through Off, Light and Strong to smooth the published attitude values.

On a moving aircraft, the unit reports pitch (nose up is positive), roll (right wing down is positive), heading, turn rate (right is positive), vertical speed and slip. Near a vertical nose angle, roll and heading are held at their last defined values and the reading is marked degraded. Outside a moving aircraft, it reports level flight.

## Attitude Indicator

Install the module on a Modular Table by right-clicking with it in hand. It occupies 2 × 2 cells and can span joined tables. A floor-mounted table uses a slanted housing; wall and ceiling tables use a flat plate.

Connect the table to the same cable network as an Attitude Reference Unit. The indicator uses the nearest usable unit on the same aircraft. Right-click the installed module with an empty hand to open its screen and inspect pitch, roll and source states.

- A usable reference unit shows the artificial horizon. Nose-up moves the horizon down; right-wing-down is positive roll.
- A nose near vertical shows a small amber ATT flag while holding the last defined roll.
- With no usable reference unit, or an incomplete cable network, the display shows a black screen with a red ATT flag.
- A Radar Altimeter on the network adds an altitude tape showing clearance above ground in blocks. The lowest valid clearance supplies the reading; outside radar range the tape shows ----.
- Use the screen's Altitude tape switch to show or hide the tape. The horizon expands when the tape is hidden.

The indicator does not require an Avionics Computer. Its Modular Table is itself an endpoint of the avionics network.