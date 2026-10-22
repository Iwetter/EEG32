# EEG32

**A 32-channel EEG acquisition board design in KiCad.**

An electronics design project using four ADS1299 analog front ends and an nRF52832 acquisition controller, with shared reference, separate bias, passive inputs, and documented connector/assembly interfaces.

## Project status

The repository captures the `2.1-prefab-bench` design checkpoint dated October 1, 2026. It contains editable schematics and PCB layout, component libraries, a BOM, and pre-fabrication engineering documentation. Fabrication, bench performance, and human-connected use have not been validated. The design documentation retains the outstanding manufacturing and safety review holds.

## Engineering focus

- Multi-channel analog acquisition and MCU interfaces.
- Hierarchical schematic organization and a routed PCB.
- Footprint/library management and component procurement documentation.
- Connector orientation, assembly centroids, and pre-fabrication checks.
- Explicit separation of electrical-rule results from physical qualification.

## Explore the design

| File or directory | Contents |
|---|---|
| [`EEG32.kicad_pro`](EEG32.kicad_pro) | KiCad project entry point |
| [`EEG32.kicad_sch`](EEG32.kicad_sch) | Root schematic and hierarchical sheets |
| [`EEG32.kicad_pcb`](EEG32.kicad_pcb) | PCB layout |
| [`EEG32.pretty/`](EEG32.pretty/) | Project footprints |
| [`BOM.csv`](BOM.csv) | Bill of materials |
| [`prefab-20261001/`](prefab-20261001/) | Release notes, assembly details, qualification, and bench plans |
| [`ERC.json`](ERC.json), [`DRC.json`](DRC.json) | Saved design-check outputs |

Open `EEG32.kicad_pro` with KiCad 10 and keep the repository's relative libraries together. Review [the release report](prefab-20261001/RELEASE-REPORT.md), [bench-validation plan](prefab-20261001/BENCH-VALIDATION.md), and [safety-review inputs](prefab-20261001/SAFETY-REVIEW-INPUTS.md) before interpreting the saved check results.

The source edition excludes historical checkpoints, duplicated archives, machine-local settings, and downloaded vendor documents. References in historical qualification notes may point to files from the original development package.

**Tools:** KiCad · PCB layout · ADS1299 · nRF52832 · ERC/DRC

[Ian Hall's engineering portfolio](https://github.com/Iwetter)
