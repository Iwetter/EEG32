# Check provenance

The final reports were produced by KiCad 10.0.5 CLI from the saved revision 2.1 sources. The standalone checkpoint was then checked from its own directory, using its local libraries and included 2.0 comparison inputs; it produced the same counts and passed all 9,639 preservation checks. See standalone-checkpoint-verification.json and the package MANIFEST.json.

Commands used, with the project directory as working directory:

```text
kicad-cli sch erc EEG32.kicad_sch --output prefab-20261001/ERC.json --format json --severity-all
kicad-cli pcb drc EEG32.kicad_pcb --output prefab-20261001/DRC.json --format json --schematic-parity --all-track-errors --severity-all
KiCad-Python scripts/prefab_verify.py
```

The working board was also zone-refilled and saved using DRC's --refill-zones --save-board options before checkpointing. The final saved zones travel with the checkpoint. `KiCad-Python` means KiCad's bundled Python with pcbnew available (this host: C:/Program Files/KiCad/10.0/bin/python.exe). The verification script selects the original workspace baseline or the portable package's verification-baseline directory. It regenerates the netlist and comparison reports; it does not edit copper. The FFC export separately checks all 40 lateral contact positions and validates the specified facing-connector map.

Re-running exports updates their timestamps/hashes. Treat MANIFEST.json as identifying the delivered files; a later run requires a new manifest to describe its new report files. The mutation/package scripts document this task's implementation; prefab_package.py expects the original workspace with its full preserved baseline. Do not execute the historical organize_schematics.py as a project generator; prefab_correct.py imports only its pin-coordinate/stub helper definitions.
