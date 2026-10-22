# Electrode protection/isolation — supervisor and safety review required

**Do not connect this checkpoint to a human until the supervisor and qualified safety reviewer approve the complete system and its protection/isolation design.** This revision adds no invented patient-protection network. The existing 4.99 kΩ input resistors, 4.7 nF filters and BIAS resistance/compensation are preserved functional circuitry; they have not been demonstrated as sufficient patient protection, an isolation barrier or compliance evidence.

The reviewer must establish the following inputs before a protection design can be selected and verified:

| Input | Required decision/evidence |
|---|---|
| Intended use and environment | Research/clinical purpose, essential performance, subjects/population, contact duration, operator, jurisdiction and applicable standards/ethics approval. |
| Applied part | Wet/gel electrode type, count/material/contact area, impedance/offset range, REF and driven BIAS behavior, required BF/CF or other classification and normal/single-fault limits. |
| Complete energy/interface diagram | Battery chemistry/protection, charger, USB/host, SWD probe, instrument/fixture grounds, accessible conductive enclosure, cables and all possible concurrent connections. Battery-only intent must be enforced and assessed, not inferred. |
| Protection/isolation basis | Maximum credible external voltages/currents, polarity, duration/energy, normal and single faults, means of patient protection, required isolation voltage, leakage/auxiliary-current limits, creepage/clearance and component failure modes. |
| Disturbance and clinical coexistence | ESD/contact discharge, RF/EMC, nearby electrosurgery/defibrillation exposure if applicable, electrode hot-plug/disconnect, liquid ingress and charge accumulation. Explicitly include/exclude environments through a reviewed intended-use requirement. |
| Analog compatibility | Allowed protection leakage, capacitance, noise, impedance imbalance, input bias/offset error, clamping level versus ADS absolute maxima/PGA headroom, recovery and BIAS loop loading. |
| Mechanical/user controls | Connector retention/keying, strain relief, insulation, exposed pads, enclosure, cleaning, misuse and prevention of programming/charging/instrument connection while electrodes contact a person. |
| Verification and signoff | Approved protection schematic/calculations, component ratings/derating, independent review, normal/single-fault analysis, leakage/isolation tests on the complete system, EMC and fault-response tests, bench evidence and written human-use authorization. |

Review applicability of the current general medical-electrical requirements and the EEG particular standard; applicability and classification require the actual intended use. IEC's catalog lists **IEC 60601-1** and **IEC 80601-2-26:2019**, with its 2024 amendment/consolidated option. Do not rely on the superseded 2012 EEG particular standard as the final basis. [IEC 60601-1 catalog](https://webstore.iec.ch/en/publication/67497), [IEC 80601-2-26 catalog and amendment links](https://webstore.iec.ch/en/publication/26376).

Present status: phantom-only bench hardware. No patient-leakage, auxiliary-current, isolation, single-fault, defibrillation, EMC or human-use qualification has been performed. Protection/isolation implementation is intentionally deferred until a verified design basis and supervisor/safety review exist.
