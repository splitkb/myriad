---
layout: default
title: Versioning
parent: Specification
nav_order: 5
---
# Versioning
The Myriad System mostly uses standard [semantic versioning](https://semver.org/), with a version number formatted as `MAJOR.MINOR.PATCH`.

MAJOR indicates an incompatible breaking change, MINOR indicates a backwards-compatible hardware addition, and PATCH is used primarily to indicate backwards-compatible additions to the [Card Identification](card_identification/) data format.

This means a keyboard with Myriad 1.2 is *guaranteed* to fully support all cards made for Myriad 1.0 to 1.2. A card made for Myriad 1.3 can still be inserted without any issues, but due to missing hardware features not all features might be available.

A card made with Myriad 1.2.3 will be electrically compatible with a keyboard made for Myriad 1.2.0, but it might require custom coding. The keyboard could be updated from Myriad 1.2.0 to 1.2.3, making the custom code unnecessary.

A card for a theoretical future Myriad 2.0 will be completely incompatible with any Myriad 1.x keyboards and vice versa.

# Version History
## 1.0.0
- Initial release
