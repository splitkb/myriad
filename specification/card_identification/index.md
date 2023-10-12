---
layout: default
title: Card Identification
parent: Specification
has_children: true
nav_order: 4
---

# Card Identification
Myriad uses EEPROM chips placed on the card to allow identification of the card inserted. This allows the keyboard to automatically configure the card for use, allowing for a seamless no-code experience.

# EEPROM Selection and Addressing
The Myriad ecosystem use standard 2kb-16kb I²C EEPROM chips, such as the [Zetta ZD24C16A](https://datasheet.lcsc.com/lcsc/2109141830_Zetta-ZD24C08A-STGMT_C2896640.pdf). They use the address range `1010 000X` - `1010 111X`.

The EEPROM chips use 2kb pages, with the 3 LSBs of the device address used for page selection. If no page selection is possible, the relevant bit is set to 0. This means a 2kb EEPROM chip will *always* use address `1010 000X`, but a 16kb chip will use the entire `1010 000X` - `1010 111X` range.

Write protection is allowed, but not mandatory.

# Header

| Length | Format | Description |
|--------|--------|-------------|
| 3 | 0x`4D 59 52` | [Magic number](https://en.wikipedia.org/wiki/Magic_number_(programming)), ASCII characters `MYR`.
| 3 | uint8 `major`, uint8 `minor`, uint8 `patch` | [Version number](versioning.html), currently `01 00 00`.
| 4 | uint32 | Payload Checksum. [Adler-32](https://en.wikipedia.org/wiki/Adler-32) checksum of the entire payload.
| 2 | uint16 | Payload length in bytes.
| n | -      | Payload, consists of one or more [entries](#payload-entries).

# Payload entries
Payload entries follow the following format:

| Length | Format | Description |
|--------|--------|-------------|
| 1 | uint8 | Entry type identifier.
| 1 | uint8 | Data length in bytes.
| n | - | Data, format depends on entry type.

Note that this allows the reader to trivially skip unsupported entry types. Payload entries may appear in any order. Some payload entry types may be repeated.

# Payload Entry Types
Note that new entry types may be added from time to time in order to support additional functionality.

## Metadata
### Card Identifier
*Mandatory: No. Repeatable: No. Since: 1.0.0.*

{: .warning }
This entry **must** be present!

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x01` | Entry type identifier.
| 1 | `0x05` | Data length in bytes.
| 2 | uint16 | [Vendor ID](vendor_ids.html).
| 2 | uint16 | Product ID.
| 1 | uint8 | Product revision.

Assignment of Product ID and revision is left to each individual vendor. However, the combination of Product ID and revision **must** uniquely identify a distinct product. If two products have the same ID and revision, they must be fully interchangeable both electronically and from software.

### Vendor Name
*Mandatory: No. Repeatable: No. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x02` | Entry type identifier.
| 1 | `n` | Data length in bytes.
| n | utf-8 | Vendor Name String.

A human-readable string identifying the vendor. The string is *not* null-terminated.

### Product Name
*Mandatory: No. Repeatable: No. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x03` | Entry type identifier.
| 1 | `n` | Data length in bytes.
| n | utf-8 | Product Name String.

A human-readable string identifying the product. The string is *not* null-terminated.

### Product URL
*Mandatory: No. Repeatable: No. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x04` | Entry type identifier.
| 1 | `n` | Data length in bytes.
| n | utf-8 | Product URL String.

A human-readable string representing a URL pointing to a website with more information about the product. The string is *not* null-terminated.

## General IO
### Button / Switch
*Mandatory: No. Repeatable: Yes. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x10` | Entry type identifier.
| 1 | `0x02` | Data length in bytes.
| 1 | uint8 | [Pin number](/specificatio/pinout.html) on the connector.
| 1 | uint8 | Configuration bit field

The configuration bit field uses the following format:

| Bit     | Meaning |
|---------|---------|
| 0 (LSB) | 0: Momentary, 1: Toggle
| 1       | 0: No pullup needed, 1: Pullup needed
| 2       | 0: Do not invert, 1: Invert value
| 3       | *Reserved, set to 0*
| 4       | *Reserved, set to 0*
| 5       | *Reserved, set to 0*
| 6       | *Reserved, set to 0*
| 7 (MSB) | *Reserved, set to 0*

Describes a simple push button or switch, which provides either a high or low value to a gpio pin.

### Rotary Encoder
*Mandatory: No. Repeatable: Yes. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x11` | Entry type identifier.
| 1 | `0x03` | Data length in bytes.
| 1 | uint8 | [Pin number](/specificatio/pinout.html) on the connector, contact A.
| 1 | uint8 | [Pin number](/specificatio/pinout.html) on the connector, contact B.
| 1 | uint8 | Configuration bit field

The configuration bit field uses the following format:

| Bit     | Meaning |
|---------|---------|
| 0 (LSB) | 0: Smooth, 1: Tactile
| 1       | 0: No pullups needed, 1: Pullups needed
| 2-4     | Encoder resolution
| 5-7 (MSB) | Encoder default position

Describes a rotary encoder, like the EC11.

### 2D Joystick
*Mandatory: No. Repeatable: Yes. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x12` | Entry type identifier.
| 1 | `0x03` | Data length in bytes.
| 1 | uint8 | [Pin number](/specificatio/pinout.html) on the connector, X axis.
| 1 | uint8 | [Pin number](/specificatio/pinout.html) on the connector, Y axis.
| 1 | uint8 | Configuration bit field

The configuration bit field uses the following format:

| Bit     | Meaning |
|---------|---------|
| 0 (LSB) | 0: Do not invert X, 1: Invert X axis.
| 1       | 0: Do not invert Y, 1: Invert Y axis.
| 2       | *Reserved, set to 0*
| 3       | *Reserved, set to 0*
| 4       | *Reserved, set to 0*
| 5       | *Reserved, set to 0*
| 6       | *Reserved, set to 0*
| 7 (MSB) | *Reserved, set to 0*

Describes an analog joystick.

### Addressable RGB LEDs
*Mandatory: No. Repeatable: No. Since: 1.0.0.*

| Length | Format | Description |
|--------|--------|-------------|
| 1 | `0x12` | Entry type identifier.
| 1 | `0x03` | Data length in bytes.
| 1 | uint8 | LED count.
| 1 | uint8 | Power usage per LED, black (`00 00 00`), in 0.1 mA.
| 1 | uint8 | Power usage per LED, white (`FF FF FF`), in 1 mA.

Describes a set of WS2812B-compatible RGB LEDs, connected to the dedicated [RGB Out](/specification/pinout.html#rgb) pin.

Power usage values are used to dynamically adjust maximum brightness in order to stay within keyboard power limits. If unknown, use `0`.
