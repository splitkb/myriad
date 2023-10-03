---
layout: default
title: Electrical Specifications
parent: Specification
nav_order: 2
---

# Electrical Specification
Unless stated otherwise, all IO pins use 3.3V.

IO pins are driven from a microcontroller, so expect them to sink/source about 10mA. You can power a LED from them, but don't expect them to drive a servo.

# Power
The keyboard provides three potential power sources to the card.

## 3V3
This is the main supply for digital logic. It is always available. The keyboard has to convert the 5V provided from USB into 3V3, so anything drawing very large amounts of current should use the 5V rail instead.

Keyboards are expected to supply about 500mA on the 3V3 rail.

## 5V
Used to supply power-hungry components, like RGB LEDs. It is available on both sides of a split keyboard.

The 5V supply must be protected by an overcurrent fuse on the keyboard. As with any USB device, expect it to supply about 500mA.

{: .note }
Controller modules are not required to supply 5V to the keyboard: the keyboard is required to operate with only 3V3.

## Raw
Direct power from the USB connector, used for things like battery charging.

A module can **passively** measure the voltage on the two CC pins to determine roughly how much power can be drawn. The highest voltage determines the maximum current allowed:

|Voltage      |Allowed current|
|-------------|---------------|
|< 0.2V       |None, USB disconnected |
|0.2V - 0.66V |500 mA         |
|0.66V - 1.23V|1500 mA        |
|> 1.23V      |2000 mA        |

A module may **never** draw more than 2000 mA, as that is the absolute limit of the connector.

{: .warning }
USB PD communication is **explicitly forbidden**. The module may **only** measure the voltage present on the CC pins.

{: .note }
On split keyboards, raw power is only available on the primary half.

# Ground
Ground pins have been distributed along the connector. Connect ground pins close to high-speed connections for better signal integrity.

All ground pins are connected on the keyboard, feel free to leave some disconnected when not needed.

# Reserved pins
For compatibility with future revisions, all reserved pins **must** be left floating.
