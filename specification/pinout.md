---
layout: default
title: Pinout
parent: Specification
nav_order: 3
---

# Myriad Pinout
This document serves as a reference when creating Myriad cards. You don't need to make your own symbols - we already did that [for you](design.html#resources)

- *Odd pins are on the top, even pins are on the bottom*
- *Pins marked with a 🚧 may only be used by [controller cards](#controller-cards)*
- *Unless explicitly stated otherwise, all IO pins use 3.3V.*

|\#|Group|Name|Description|
|---|------|-----|----|-----------|
|01|[Power](electrical.html#power)|GND|Ground|
|02|[Power](electrical.html#power)|Shield|Case shield|
|03|[USB](#usb)|D- [🚧](#controller-cards)|USB data|
|04|[USB](#usb)|CC 1|USB current sense|
|05|[USB](#usb)|D+ [🚧](#controller-cards)|USB data|
|06|[USB](#usb)|CC 2|USB current sense|
|07|[Power](electrical.html#power)|GND|Ground|
|08-15|*(Unused)*|*Key A*|Board cutout|
|16|[Power](electrical.html#power)|3V3||
|17|[Power](electrical.html#power)|Raw||
|18|[Power](electrical.html#power)|3V3||
|19|[Power](electrical.html#power)|Raw||
|20|[Power](electrical.html#power)|5V||
|21|[Power](electrical.html#power)|Raw||
|22|[Power](electrical.html#power)|5V||
|23|[Power](electrical.html#power)|Raw||
|24-31|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|32|[GPIO](#gpio)|GPIO 1|General-purpose IO|
|33|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|34|[GPIO](#gpio)|GPIO 2|General-purpose IO|
|35|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|36|[GPIO](#gpio)|GPIO 3|General-purpose IO|
|37|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|38|[GPIO](#gpio)|GPIO 4|General-purpose IO|
|39|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|40|[Power](electrical.html#power)|GND|Ground|
|41|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|42|[SPI](#spi)|[Matrix CS](#matrix-data) [🚧](#controller-cards)|Chip Select, keyboard matrix|
|43|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|44|[SPI](#spi)|Myriad CS|Chip Select, Myriad module|
|45|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|46|[Power](electrical.html#power)|GND|Ground|
|47|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|48|[SPI](#spi)|SCK|Clock|
|49|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|50|[SPI](#spi)|SDI|Data, Module to Keyboard|
|51|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|
|52|[SPI](#spi)|SDO|Data, Keyboard to Module|
|53|Misc|[Split Comm.](#split-communication) TX [🚧](#controller-cards)|Serial link between halves, transmit|
|54|[Power](electrical.html#power)|GND|Ground|
|55|Misc|[Split Comm.](#split-communication) RX [🚧](#controller-cards)|Serial link between halves, receive|
|56|[Serial](#serial)|RTS|Request-To-Send, Keyboard to Module|
|57|[Power](electrical.html#power)|GND|Ground|
|58|[Serial](#serial)|CTS|Clear-To-Send, Module to Keyboard|
|59|Misc|[Reset](#reset)|Reset keyboard & module|
|60|[Serial](#serial)|RX|Data, Module to Keyboard|
|61|[I2C](#i2c)|SCL|Clock|
|62|[Serial](#serial)|TX|Data, Keyboard to Module|
|63|[I2C](#i2c)|SDA|Data|
|64|[Power](electrical.html#power)|GND|Ground|
|65|Misc|[Controller Disable](#controller-disable) [🚧](#controller-cards)|Keyboard controller override|
|66|[PWM](#pwm)|PWM 1|Pulse-width modulation|
|67|Misc|[Module Present](#module-presence)|Myriad module inserted|
|68|[PWM](#pwm)|PWM 2|Pulse-width modulation|
|69|[Power](electrical.html#power)|GND|Ground|
|70|[Power](electrical.html#power)|GND|Ground|
|71|RGB|[RGB Out](#rgb)|RGB data, Keyboard to Module|
|72|[ADC](#adc)|ADC 1|Analog input|
|73|RGB|[RGB In](#rgb-1) [🚧](#controller-cards)|RGB data, Module to Keyboard|
|74|[ADC](#adc)|ADC 2|Analog input|
|75|*(Unused)*|*(Reserved)*|[Leave disconnected](electrical.html#reserved-pins)|

# Basic IO

### Reset
The Myriad module and keyboard share an active-low Reset signal. This can be used both to have a press of the on-keyboard reset button reset hardware placed on the Myriad card, or to have an additional reset button for the keyboard on the Myriad card. The keyboard will provide a pull-up.

### Module Presence
All [identifiable](card_identification/) Myriad cards **must** short Module Presence to Ground to indicate that a card has been inserted. Leave it floating for cards which cannot be automatically identified.

### Signals

|\#| Pin |
|--|-----|
|59| Reset |
|67| Module presence |

## GPIO
GPIO pins can be used for general low-speed IO such as reading a push button or controlling a LED. They can be used for both input and output.

GPIO pins have support for internal pullup resistors, but internal pulldown resistors are not guaranteed. If you need pulldown resistors, you have to add them yourself.

### Signals

|\#| Pin |
|--|-----|
|32| GPIO 1 |
|34| GPIO 2 |
|36| GPIO 3 |
|38| GPIO 4 |

## PWM
The two PWM pins can be used to output analog-like signals, such as lighting with varying brightness or a speaker.

They can double as additional GPIO outputs if needed.

### Signals

|\#| Pin |
|--|-----|
|66| PWM 1 |
|68| PWM 2 |

## ADC
The two ADC pins can be used to read analog signals, for example from potentiometers or joysticks.

They can double as additional GPIO inputs if needed.

### Signals

|\#| Pin |
|--|-----|
|72| ADC 1 |
|74| ADC 2 |

## RGB
The Myriad module may have one or more WS2812B-compatible RGB LEDs. It is chained through similar LEDs on the keyboard itself, if any.

{: .warning }
Because the RGB data is provided by the previous LED in the chain, this is a **5V signal**.

### Signals

|\#| Pin |
|--|-----|
|71| RGB Out |

# Advanced IO
## SPI
[SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface) is the primary high-speed data bus for Myriad. It can transfer data at a rate of over 1Mbps, which should be sufficient for even the most demanding accessories.

### Implementation Notes

- **The module may only interact with SDI / SDO when CS is LOW**. When CS is HIGH, all signals coming from the keyboard should be ignored and all signals going back to the keyboard should be left in a [Hi-Z](https://en.wikipedia.org/wiki/High_impedance#Digital_electronics) state as hardware on the keyboard itself might be using the SPI bus.
- The keyboard will provide a pullup on CS.
- Phasing, polarity, and clock speed are not specified.

{: .warning }
SPI pins should **not** be reused as additional GPIO.

### Signals

|\#| Pin | From | To |
|-|-----|------|----|
|44| CS / SS | Keyboard | Module |
|48| SCK / SCLK | Keyboard | Module |
|50| SDI / MISO | Module | Keyboard |
|52| SDO / MOSI | Keyboard | Module |

## I²C
[I²C](https://en.wikipedia.org/wiki/I%C2%B2C) is the primary low-speed data bus for Myriad. It can transfer data at a rate of 100kbps, which is sufficient for undemanding applications.

The I²C bus is primarily used for [card identification](card_identification/), although the Myriad module is free to use it for other purposes.

### Implementation Notes
- **Address range `1010 000X` - `1010 111X` is reserved**, where X is the R/W bit.
- Speed is limited to 100kbps.
- The keyboard may add additional devices to the I²C bus.

{: .warning }
I²C pins should **not** be reused as additional GPIO.

### Signals

|\#| Pin |
|--|-----|
|61| Clock |
|63| Data |

## Serial
A full serial bus is present to simplify interaction with high-speed hardware which doesn't support SPI.

They can double as additional GPIO inputs if needed, but signal direction should be respected.

### Implementation Notes
- Baud rate is not specified.
- Use of RTS/CTS for flow control is optional.

### Signals

|\#| Pin | From | To |
|-|-----|------|----|
|56| RTS | Keyboard | Module |
|58| CTS | Module | Keyboard |
|60| RX | Module | Keyboard |
|62| TX | Keyboard | Module |

# Controller Cards
A "Controller Card" is a Myriad module which takes over the tasks of the on-keyboard microcontroller. Adding a Controller Card essentially turns the entire board into an io expander.

Several lines on the Myriad connector are reserved for use by Controller Cards, as they will be used by the keyboard's microcontroller when regular cards are used.

## Controller Disable
To indicate the presence of a controller card, the card must short pin 65 to Ground. If a keyboard microcontroller detects this short on bootup, it immediately enters a low-power sleep mode and does not interact with the keyboard hardware.

Regular cards must leave this pin floating.

### Signals

|\#| Pin |
|--|-----|
|65| Controller Disable |

## Power
### Wired
Controller cards intended for wired operation should use the regular 3V3 and 5V rails to source their power from the keyboard.

### Wireless
Controller cards intended for wireless operation must instead *provide* power to the keyboard. The card is **required** to provide 3V3 to the keyboard, and the keyboard shall provide basic functionality with only 3V3 provided.

Additionally, the card *may* provide 5V. The keyboard may attach high-power functionality (such as RGB LEDs) directly to the 5V bus - they will not be available with cards which only provide 3V3.

The card may use the RAW pins to source battery charging powers - see the [Power section](electrical.html#power). 

{: .note }
Wireless cards providing power to the keyboard should take into account the RAW->5V->3V3 power supply already present on the keyboard.

## Matrix Data
The controller card can read the current state of the key matrix via the SPI bus. If the keyboard has encoders, their state will also be included. Most keyboards will implement this using cheap shift registers, but other implementations are allowed.

The matrix data is read using the same pins as regular SPI, but their direction is reversed. Note that it uses a **different** Chip Select pin, though!

### Signals

|\#| Pin | From | To |
|-|-----|------|----|
|**42**| CS / SS | Keyboard | Module |
|48| SCK / SCLK | Module | Keyboard |
|50| SDI / MISO | Keyboard | Module |
|52| SDO / MOSI | Module | Keyboard |

## Split Communication
Split keyboards consists of two halves, with a communications link between them. When a controller card is in use, it may use this link to communicate with its partner inserted into the other half.

### Implementation Notes
- The communications link is full-duplex. You **must** use separate pins for transmit and receive - using a single pin for both does not work as the keyboard may be using a level converter. 

### Signal Directions

|\#| Pin | From | To |
|-|-----|------|----|
|53| TX | This side | Other side |
|55| RX | Other side | This side |

## RGB
The keyboard may have one or more chained WS2812B-compatible RGB LEDs which can be driven by a controller card.

{: .note }
Despite it feeding a WS2812B LED, it is a 3V3 signal. Any level conversion is left to the keyboard.

### Signals

|\#| Pin |
|--|-----|
|73| RGB In |

## USB
Controller cards may use the USB bus to communicate with a host computer. Keep in mind that signal quality is likely going to be relatively poor due to routing limitations: Full-speed communication (12Mbps) will work, but High-speed (480Mbps) is not guaranteed.

The USB connector also provides the CC signals needed to sense the [absolute power limit](electrical.html#raw).

### Signals

|\#| Pin |
|--|-----|
|03| D- |
|04| CC 1 |
|05| D+ |
|06| CC 2 |

# Known Pin Mappings
The table below describes the physical connectivity between the microcontroller and the Myriad connector of some keyboards implementing Myriad.

|Myriad \#|Name|[Elora](/myriad-products.html#elora)|
|---------|----|---------|
|32|GPIO 1|GP4|
|34|GPIO 2|GP5|
|36|GPIO 3|GP6|
|38|GPIO 4|GP8|
|44|SPI Myr. CS|GP9|
|48|SPI SCK|GP10|
|50|SPI SDI|GP12|
|52|SPI SDO|GP11|
|56|Ser. RTS|GP19|
|58|Ser. CTS|GP18|
|60|Ser. RX|GP17|
|61|I2C SCL|GP1|
|62|Ser. TX|GP16|
|63|I2C SDA|GP0|
|65|Cont. Disable|GP2|
|66|PWM 1|GP23|
|67|Mod. Present|GP3|
|68|PWM 2|GP24|
|71|RGB Out|GP15|
|72|ADC 1|GP26|
|74|ADC 2|GP27|
