---
layout: default
title: Examples
parent: Card Identification
grand_parent: Specification
nav_order: 1
---

# Example Card Identification Values
Here is the EEPROM data used by splitkb.com's Myriad modules. Decoding them is currently left as an excercise for the reader.

## Encoder
```
0x4d, 0x59, 0x52, 0x01, 0x00, 0x00, 0x72, 0x1a, 0x0c, 0xeb, 0x5d, 0x00, 0x01, 0x05, 0x01, 0x00,
0x01, 0x00, 0x00, 0x02, 0x0b, 0x73, 0x70, 0x6c, 0x69, 0x74, 0x6b, 0x62, 0x2e, 0x63, 0x6f, 0x6d,
0x03, 0x15, 0x4d, 0x79, 0x72, 0x69, 0x61, 0x64, 0x20, 0x45, 0x6e, 0x63, 0x6f, 0x64, 0x65, 0x72,
0x20, 0x4d, 0x6f, 0x64, 0x75, 0x6c, 0x65, 0x04, 0x22, 0x68, 0x74, 0x74, 0x70, 0x73, 0x3a, 0x2f,
0x2f, 0x73, 0x70, 0x6c, 0x69, 0x74, 0x6b, 0x62, 0x2e, 0x63, 0x6f, 0x6d, 0x2f, 0x6d, 0x79, 0x72,
0x69, 0x61, 0x64, 0x2d, 0x65, 0x6e, 0x63, 0x6f, 0x64, 0x65, 0x72, 0x11, 0x03, 0x22, 0x24, 0x23,
0x10, 0x02, 0x20, 0x06, 0x12, 0x03, 0x08, 0x05, 0x22
```

## Joystick
```
0x4d, 0x59, 0x52, 0x01, 0x00, 0x00, 0x7b, 0x1b, 0x81, 0xb2, 0x5a, 0x00, 0x01, 0x05, 0x01, 0x00,
0x02, 0x00, 0x00, 0x02, 0x0b, 0x73, 0x70, 0x6c, 0x69, 0x74, 0x6b, 0x62, 0x2e, 0x63, 0x6f, 0x6d,
0x03, 0x16, 0x4d, 0x79, 0x72, 0x69, 0x61, 0x64, 0x20, 0x4a, 0x6f, 0x79, 0x73, 0x74, 0x69, 0x63,
0x6b, 0x20, 0x4d, 0x6f, 0x64, 0x75, 0x6c, 0x65, 0x04, 0x23, 0x68, 0x74, 0x74, 0x70, 0x73, 0x3a,
0x2f, 0x2f, 0x73, 0x70, 0x6c, 0x69, 0x74, 0x6b, 0x62, 0x2e, 0x63, 0x6f, 0x6d, 0x2f, 0x6d, 0x79,
0x72, 0x69, 0x61, 0x64, 0x2d, 0x6a, 0x6f, 0x79, 0x73, 0x74, 0x69, 0x63, 0x6b, 0x12, 0x03, 0x4a,
0x48, 0x00, 0x10, 0x02, 0x20, 0x06
```

## Macropad
```
0x4d, 0x59, 0x52, 0x01, 0x00, 0x00, 0x7b, 0x1b, 0xec, 0xea, 0x66, 0x00, 0x01, 0x05, 0x01, 0x00,
0x03, 0x00, 0x00, 0x02, 0x0b, 0x73, 0x70, 0x6c, 0x69, 0x74, 0x6b, 0x62, 0x2e, 0x63, 0x6f, 0x6d,
0x03, 0x16, 0x4d, 0x79, 0x72, 0x69, 0x61, 0x64, 0x20, 0x4d, 0x61, 0x63, 0x72, 0x6f, 0x70, 0x61,
0x64, 0x20, 0x4d, 0x6f, 0x64, 0x75, 0x6c, 0x65, 0x04, 0x23, 0x68, 0x74, 0x74, 0x70, 0x73, 0x3a,
0x2f, 0x2f, 0x73, 0x70, 0x6c, 0x69, 0x74, 0x6b, 0x62, 0x2e, 0x63, 0x6f, 0x6d, 0x2f, 0x6d, 0x79,
0x72, 0x69, 0x61, 0x64, 0x2d, 0x6d, 0x61, 0x63, 0x72, 0x6f, 0x70, 0x61, 0x64, 0x10, 0x02, 0x24,
0x06, 0x10, 0x02, 0x22, 0x06, 0x10, 0x02, 0x26, 0x06, 0x10, 0x02, 0x20, 0x06, 0x12, 0x03, 0x08,
0x05, 0x22
```