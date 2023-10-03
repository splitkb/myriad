---
layout: default
title: Pinout
parent: Specification
nav_order: 3
---

# Pins
*Odd pins are on the top, even pins are on the bottom*

|\#|Group|Name|Description|
|---|------|-----|----|-----------|
|01|[Power](electrical.html#power)|GND|Ground|
|02|[Power](electrical.html#power)|Shield|Case shield|
|03|USB|D-||
|04|USB|CC 1||
|05|USB|D+||
|06|USB|CC 2||
|07|[Power](electrical.html#power)|GND||
|08-15|*(Unused)*|*Key A*|Board cutout|
|16|[Power](electrical.html#power)|3V3||
|17|[Power](electrical.html#power)|Raw||
|18|[Power](electrical.html#power)|3V3||
|19|[Power](electrical.html#power)|Raw||
|20|[Power](electrical.html#power)|5V||
|21|[Power](electrical.html#power)|Raw||
|22|[Power](electrical.html#power)|5V||
|23|[Power](electrical.html#power)|Raw||
|24-31|*(Unused)*|*(Reserved)*|Leave disconnected|
|32|[GPIO](#gpio)|GPIO 1|General-purpose IO|
|33|*(Unused)*|*(Reserved)*|Leave disconnected|
|34|[GPIO](#gpio)|GPIO 2|General-purpose IO|
|35|*(Unused)*|*(Reserved)*|Leave disconnected|
|36|[GPIO](#gpio)|GPIO 3|General-purpose IO|
|37|*(Unused)*|*(Reserved)*|Leave disconnected|
|38|[GPIO](#gpio)|GPIO 4|General-purpose IO|
|39|*(Unused)*|*(Reserved)*|Leave disconnected|
|40|[Power](electrical.html#power)|GND|Ground|
|41|*(Unused)*|*(Reserved)*|Leave disconnected|
|42|[SPI](#spi)|Matrix CS|Chip select, on-keyboard matrix shift registers, active-low. Intended for Myriad MCU modules|
|43|*(Unused)*|*(Reserved)*|Leave disconnected|
|44|[SPI](#spi)|Myriad CS|Chip select, Myriad module, active-low|
|45|*(Unused)*|*(Reserved)*|Leave disconnected|
|46|[Power](electrical.html#power)|GND|Ground|
|47|*(Unused)*|*(Reserved)*|Leave disconnected|
|48|[SPI](#spi)|SCK|Clock|
|49|*(Unused)*|*(Reserved)*|Leave disconnected|
|50|[SPI](#spi)|SDI|Data Keyboard->Myriad|
|51|*(Unused)*|*(Reserved)*|Leave disconnected|
|52|[SPI](#spi)|SDO|Data Myriad->Keyboard|
|53|*(Unused)*|*(Reserved)*|Leave disconnected|
|54|[Power](electrical.html#power)|GND|Ground|
|55|Keyboard|Split Comm.|Serial link between halves, only for Myriad MCU modules|
|56|[Serial](#serial)|RTS|Request-to-send, Keyboard->Myriad|
|57|[Power](electrical.html#power)|GND|Ground|
|58|[Serial](#serial)|CTS|Clear-to-send, Myriad->Keyboard|
|59|Keyboard|Reset|Reset keyboard & module, active-low. Has pull-up on keyboard side|
|60|[Serial](#serial)|RX|Data Myriad->Keyboard|
|61|[I2C](#i2c)|SCL|Clock|
|62|[Serial](#serial)|TX|Data Keyboard->Myriad|
|63|[I2C](#i2c)|SDA|Data|
|64|[Power](electrical.html#power)|GND|Ground|
|65|Keyboard|Controller Enable|Connect to ground to disable onboard controller. Intended for Myriad MCU modules|
|66|[PWM](#pwm)|PWM 1|Pulse-width modulation|
|67|Keyboard|Module|Module presence|Indicates presence of Myriad module to keyboard. Short to ground on module side is mandatory.|
|68|[PWM](#pwm)|PWM 2|Pulse-width modulation|
|69|[Power](electrical.html#power)|GND|Ground|
|70|[Power](electrical.html#power)|GND|Ground|
|71|RGB|RGB out|RGB data Keyboard->Myriad, output from last LED on keyboard|
|72|[ADC](#adc)|ADC 1|Analog input|
|73|RGB|RGB in|RGB data Myriad->Keyboard, input to first LED on keyboard. Intended for Myriad MCU modules|
|74|[ADC](#adc)|ADC 2|Analog input|
|75|RGB|RGB Enable|RGB LED power switch, active-??. Optional for LEDs placed on Myriad|

# Power
## 3V3

## 5V

## Raw
Foo bar

# Basic IO
## GPIO
Bar baz

## PWM
fesfs

## ADC
fess

# Advanced IO
## SPI
fesf

## I2C
fesf

## Serial
fsefes

# Known pin mappings
fefse