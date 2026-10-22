# EEG32 2.1 — approved pre-fab corrections

Saved 1 October 2026 as **2.1-prefab-bench**, continuing the completed 2.0 passive project. Architecture, placements, nominal circuit values, ADS1299 pin/package mappings, acquisition GPIOs, all 32 channels, shared REF and separate BIAS are preserved. The only pin-net changes are the two previously unused nRF GPIO grounds. **This checkpoint remains on fabrication/process qualification and human-contact review hold.**

| Approved correction | Implemented result | Remaining qualification |
|---|---|---|
| nRF P0.25/P0.26 erratum | U1.37/U1.38 directly grounded to exposed VSS via two new tracks, following Nordic unused-pin guidance | Exact delivered silicon lot/build code unconfirmed; record FICR and forbid firmware driving these pins. [Evidence and scope](NRF-ERRATUM.md). |
| BOM MPNs/specifications | 225 unique references populated in schematic, PCB and CSV; 213 fitted parts, 12 non-purchased PCB features; no missing MPN/spec fields | MLCC effective capacitance, inductor/load behavior, lot/lifecycle/legacy-code procurement qualification remain. [BOM qualification](BOM-QUALIFICATION.md). |
| FFC mating definition | Exact Molex 0151660431, 0.50 mm/40 contacts, 102 mm, Type A; both-end orientation and full 40-circuit map specified | Cable 0.30 ±0.05 mm tail tolerance exceeds connector ±0.03 mm. Screen both ends or qualify supplier lot. Remote breakout/electrode termination is not supplied. [Mating contract](FFC-MATING.md). |
| Assembly documentation | Six EP vias marked filled/capped; EP/stencil/first-article requirements, pin-1/polarity silk marks, two side centroid files, bottom C15 handling and SWD fixture map | Assembler must approve paste/reflow/EP inspection, panel tooling and orientation import. [Assembly instructions](ASSEMBLY.md). |
| Manufacturing rules | Explicit provisional JLCPCB 4-layer/1 oz/ENIG/green profile; via, mask/legend rules; local copper/ring exception inventory | Actual house/stackup unspecified; supplier must accept small U1/U2 lands, mask webs, capped vias and RF stackup. [Manufacturing profile](MANUFACTURING.md). |

No boost-converter, ADS input RC, BIAS-compensation, crystal-layout, antenna-matching, analog-route or BLE-architecture redesign was performed. Those retained implementations need measurements against the defined requirements, rather than speculative edits. No patient-protection network was added because a verified protection/isolation design basis has not been provided. No firmware, remote breakout PCB or physical bench measurements are included.

Final saved-source results, KiCad **10.0.5**:

| Check | Result |
|---|---|
| ERC | **0 errors, 2 warnings** |
| DRC | **0 errors, 0 warnings** |
| Unconnected PCB items | **0** |
| Schematic/PCB parity findings | **0** |
| Preservation verification | **9,639 checks passed, 0 issues** |
| Existing track/via geometry | All **5,408** original items retained; exactly two new GPIO-to-GND tracks |
| CH01–CH32 | Unchanged J601 1–32 → R601–R632/C601–C632 → the same four ADS IN1P–IN8P destinations |
| REF | J601.33 → R633 → EEG_REF_ADC → all four SRB1/pin17 destinations, unchanged |
| BIAS | J601.34 remains separate; R634 connects the U101/pin63 BIAS_DRIVE path; three slave BIAS outputs remain NC |

The two unsuppressed ERC warnings identify the intentional bidirectional GPIO-to-GND power-flag connections. Three inherited ERC categories remain ignored: four_way_junction, simulation_model_issue, single_global_label. There are no ERC marker exclusions, no DRC ignored categories and no DRC exclusions. Results are scoped accordingly; they do not assert every ERC category was run. [ERC.json](ERC.json), [DRC.json](DRC.json), [final-counts.json](final-counts.json), [preservation-verification.json](preservation-verification.json), [channel-map.csv](channel-map.csv), [system-pin-map.csv](system-pin-map.csv).

Files changed in the working project: EEG32.kicad_pro, EEG32.kicad_pcb, EEG32.kicad_dru; all nine .kicad_sch pages (EEG32, MCU, Power, PassiveInputs, ReferenceBias, AFE1–AFE4); BOM.csv, README.md, ERC.json and DRC.json. Added prefab scripts, this release directory's documents/reports/exports/source evidence, and versioned checkpoints. EEG32.kicad_sym, EEG32.pretty and library tables are copied unchanged. [changed-files.csv](changed-files.csv) records baseline/current hashes. The 2.0 before-change checkpoint is preserved separately; old passive/integration/audit outputs remain historical.

All eleven bench items remain pending: +5VA ripple/noise with BLE, shorted ADS noise, startup/low battery, master/slave clock startup, BIAS stability, REF disconnect, electrode-offset headroom, 32-channel 500-SPS acquisition, BLE throughput/drop detection, HF crystal startup/frequency, and antenna return loss/range. [BENCH-VALIDATION.md](BENCH-VALIDATION.md) defines setups, evidence and acceptance dependencies.

Before human connection, supervisor/safety review must establish intended use/applied-part classification, electrode properties, all energy and wired interfaces, normal/single-fault patient currents, isolation/protection ratings, ESD/EMC/clinical exposure, analog loading and fault recovery, then approve a verified design and complete-system tests. [SAFETY-REVIEW-INPUTS.md](SAFETY-REVIEW-INPUTS.md) records the required inputs and unresolved signoff.

Versioned editable checkpoint: `checkpoints/EEG32-2.1-prefab-20261001/EEG32.kicad_pro`. Portable package: `EEG32-passive-prefab-2.1-20261001.zip`. The package carries the current KiCad sources, libraries, review documents, verification baseline and SHA-256 manifest; it is not an order-ready Gerber release.
