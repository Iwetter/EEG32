# Manufacturing profile and local exceptions

**Board house/order and final stackup were not supplied.** The configured profile is explicitly **PROVISIONAL-JLCPCB-4L-1OZ-ENIG-GREEN**, using the published capability page reviewed 1 October 2026. It is a concrete review baseline, not confirmation of the intended supplier or an accepted order. The saved board remains 68.3×55.7 mm, 4-layer, nominal 1.6 mm. No copper layer, dielectric thickness, board outline, antenna keepout or existing trace/via geometry was redesigned. ENIG is now the saved surface-finish requirement.

| Feature | Saved rule / requirement |
|---|---|
| General different-net clearance | 0.200 mm |
| Absolute copper-clearance floor | 0.127 mm, used only by the named local rules below |
| Track width | ≥0.1524 mm |
| Through-via diameter / hole | ≥0.450 / ≥0.200 mm; blind/microvias prohibited |
| Through-via annular ring | ≥0.125 mm, except the five documented RF vias at ≥0.100 mm |
| Hole-to-hole and hole-to-other-copper clearance | ≥0.200 mm |
| Copper-to-routed-edge clearance | ≥0.300 mm |
| Mask opening to other-net copper | ≥0.090 mm |
| Soldermask | Green; nominal pad-to-mask expansion 0.000 mm; require ≥0.100 mm mask webs in fabrication DFM |
| Printed legend | Height ≥1.000 mm, stroke ≥0.150 mm, pad clearance ≥0.150 mm; defaults corrected accordingly |
| MCU exposed-pad vias | Six existing GND vias, resin-filled and copper-capped/planarized; exact list in exposed-pad-vias.csv |

These copper/legend thresholds meet or exceed the applicable published JLCPCB 4-layer/1 oz minima except for the explicitly retained small-land exception below. The supplier lists 0.2 mm preferred via holes, a 0.10 mm minimum diameter-minus-hole difference, and filled/capped via capability. Its generic minimum SMD land is 0.25×0.25 mm. [JLCPCB capabilities](https://jlcpcb.com/capabilities/pcb-capabilities). A green mask and 1 oz outer copper are required by this profile; changing color/copper weight requires a new DFM check.

| Exception | Location / dimensions | Basis and disposition |
|---|---|---|
| U1 QFN48 escape clearance 0.127 mm | Named area X65.5–74.0, Y28.5–37.5 mm | Existing fine-pitch escape. Remains above published 1 oz copper spacing minimum. No general clearance reduction. |
| RF reference clearance 0.127 mm | Named area X72.4–78.5, Y27.4–34.3 mm | Existing RF reference routing. Copper geometry retained. |
| X2 clock clearance 0.127 mm | Named area X69.0–74.5, Y23.8–31.5 mm | Existing fine-pitch oscillator region. Crystal circuit/layout retained. |
| Five RF via rings 0.1016 mm | Ø0.508 mm / drill 0.3048 mm; exact positions in local-rule-exceptions.csv | Named RF-area rule overrides 0.125 mm ring floor to 0.100 mm. Diameter-minus-hole is 0.2032 mm. Preserves RF copper; fits the published via criterion. |
| Small U1 and U2 SMD lands | U1: 48 lands with 0.20 mm minor dimension; U2: five lands below 0.25 mm | Retained Nordic/ABLIC package lands. **Requires explicit supplier DFM acceptance beyond the generic 0.25 mm land table.** KiCad DRC does not qualify the fabricator's minimum land/process. No enlargement made. |

The .kicad_dru file defines copper/ring exceptions by named areas and prohibits unrelated tracks in the antenna area. All DRC categories are enabled; no excluded markers hide these conditions. Fab-layer text may be smaller than the printed legend because it is an assembly drawing, not ink on the board. [local-rule-exceptions.csv](local-rule-exceptions.csv) and [assembly-marks.json](assembly-marks.json) provide machine-readable locations.

Before releasing Gerbers, the actual board house must confirm: the retained stackup/dielectric values and copper thicknesses; RF feed impedance with that stackup; the small U1/U2 lands and fine-pitch mask webs; all six filled/capped EP vias; the surface finish; and panel/rail/tooling/fiducial/stencil requirements. The saved stackup retains 35 µm outer copper, 15.2 µm inner copper and dielectric thicknesses 0.2104 / 1.065 / 0.2104 mm; these are inherited design values, not an accepted supplier stackup. Do not silently substitute a standard stackup while claiming controlled RF impedance.

The checkpoint deliberately contains editable KiCad files and review exports rather than an order-ready Gerber bundle. Once the supplier accepts this profile and exceptions, regenerate fabrication outputs from that same checked source, retain its hash and verify layer/drill/mask/paste registration. Human-contact release is a separate safety gate described in SAFETY-REVIEW-INPUTS.md.
