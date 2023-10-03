---
layout: default
title: Card Identification
parent: Specification
has_children: true
nav_order: 4
---



# EEPROM addressing



# Header

| Length | Format | Description |
|--------|--------|-------------|
| 3 | `4D 59 52` | [Magic number](https://en.wikipedia.org/wiki/Magic_number_(programming)), ASCII characters `MYR`.
| 2 | uint8 `major`, uint8 `minor` | [Version number](versioning.html), currently `01 01`. Major version numbers are breaking, minor version numbers are backwards compatible.
| 4 | uint32 | Payload Checksum. [Adler-32](https://en.wikipedia.org/wiki/Adler-32) checksum of the entire payload
| 2 | uint16 | Payload length in bytes.
| n | -      | Payload, consists of one or more [entries](#payload-entries).

# Payload entries

| Length | Format | Description |
|--------|--------|-------------|
| 1 | uint8 | [Entry type](#entry-types).
| 1 | uint8 | Data length in bytes.
| n | - | Data, format depends on entry type.

## Mandatory entries
### Card Identifier

| Length | Format | Description |
|--------|--------|-------------|
| 1 | uint8 | Vendor ID.
| 1 | uint8 | Product ID.
| 1 | uint8 | Product revision.

## Optional entries