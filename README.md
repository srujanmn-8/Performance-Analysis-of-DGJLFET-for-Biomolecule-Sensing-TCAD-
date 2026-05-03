# Gate Engineered Recessed Double Gate Junctionless FET Biosensor

![Tool](https://img.shields.io/badge/Tool-Silvaco%20ATLAS-blue)
![Technology](https://img.shields.io/badge/Channel-Silicon%2020nm-orange)
![Dielectric](https://img.shields.io/badge/Gate%20Dielectric-HfO₂-purple)
![Application](https://img.shields.io/badge/Application-Biosensing-green)
![Status](https://img.shields.io/badge/Simulation-Complete-brightgreen)

---

## Overview

This project designs and simulates a **Recessed Double-Gate Junctionless Field-Effect Transistor (R-DGJLFET)** for label-free biomolecule detection using dielectric modulation. Two device structures — Conventional DGJLFET (C-DGJLFET) and Recessed DGJLFET (R-DGJLFET) — were modelled and compared using **Silvaco ATLAS** TCAD simulation.

The nanocavity embedded under the gate acts as the sensing zone. When biomolecules of different dielectric constants (k = 1 to 8) occupy the cavity, the gate-channel coupling changes, producing measurable shifts in drain current, threshold voltage, and subthreshold slope — enabling label-free detection.

---

## Device Specifications

| Parameter | C-DGJLFET | R-DGJLFET |
|-----------|-----------|-----------|
| Channel material | Silicon (Si) | Silicon (Si) |
| Gate dielectric | HfO₂ (k ≈ 4.7) | HfO₂ (k ≈ 4.7) |
| Source/Drain contacts | Aluminium | Aluminium |
| Channel length | 20 nm | 25 nm |
| Gate workfunction (ΦM) | 5.1 eV | 5.1 eV |
| Doping concentration (Nd) | 1×10¹⁷ cm⁻³ | 1×10¹⁷ cm⁻³ |
| Oxide thickness (Tsi) | 10 nm | 1 nm |
| Drain bias (VDS) | 0.05 V – 1 V | 0.05 V – 1 V |
| Gate bias sweep (VGS) | 0 – 3 V | 0 – 3 V |
| Temperature | 300 K | 300 K |
| Physical models | fermi, cvt, srh, bgn, auger, fldmob, mos | fermi, cvt, srh, bgn, auger, fldmob, mos |

---

## Device Structure

```
         ┌──────────────────────────────┐
         │        Top Gate (Al)          │  ΦM = 5.1 eV
         ├──────────────────────────────┤
         │         HfO₂ (k=4.7)         │  Gate dielectric
         ├──────┬───────────────┬───────┤
 Source  │  Si  │  Nanocavity   │  Si   │  Drain
 (Al)    │      │  (sensing     │       │  (Al)
         │      │   zone, k=1-8)│       │
         ├──────┴───────────────┴───────┤
         │         HfO₂ (k=4.7)         │
         ├──────────────────────────────┤
         │        Bottom Gate (Al)       │
         └──────────────────────────────┘
```

**Key difference — R-DGJLFET:** The recessed cavity extends closer to the source side, concentrating the electric field at the sensing interface for stronger gate-channel coupling and higher sensitivity.

---

## Simulation Setup

**Tool:** Silvaco ATLAS  
**Extraction metrics:**
- **Vth** — extracted where log₁₀(ID) = −7 A
- **Subthreshold Slope (SS)** — inverse of max derivative of log(ID) vs VG
- **DIBL** — change in Vth between VDS = 0.05 V and 1 V
- **Current Sensitivity (S)** — I_ON,filled / I_ON,empty

**Biomolecule permittivity values simulated (k):** 1, 2.53, 3.57, 4.7, 6.3, 8

---

## Results

### Biosensor Performance vs Dielectric Constant (k)

| k | Biomolecule | DIBL (V) | SS (V/dec) | IOFF (A) | ION (A) | ION/IOFF | Vt (V) |
|---|------------|----------|-----------|---------|---------|---------|--------|
| 1 | Air (baseline) | 0.03573 | 0.06483 | 2.04E-17 | 1.55E-05 | 7.57E+11 | 0.6686 |
| 2.53 | Keratin | 0.03025 | 0.06398 | 1.34E-17 | 1.58E-05 | 1.19E+12 | 0.6656 |
| 3.57 | Protein | 0.02774 | 0.06358 | 1.10E-17 | 1.60E-05 | 1.46E+12 | 0.6618 |
| 4.7 | HfO₂ equiv. | 0.02568 | 0.06325 | 9.56E-18 | 1.61E-05 | 1.68E+12 | 0.6583 |
| 6.3 | Bacteriophage | 0.02354 | 0.06290 | 8.46E-18 | 1.62E-05 | 1.91E+12 | 0.6543 |
| 8 | Keratin (high) | 0.02191 | 0.06262 | 7.77E-18 | 1.63E-05 | 2.09E+12 | 0.6458 |

**Key trend:** As k increases from 1 → 8, DIBL decreases (better SCE control), ION/IOFF improves from 7.57×10¹¹ → 2.09×10¹², and Vt shifts lower — all confirming the dielectric modulation sensing mechanism.

### C-DGJLFET vs R-DGJLFET Comparison

| Device | DIBL | IOFF (A) | ION (A) | ION/IOFF | Vt (V) |
|--------|------|---------|---------|---------|--------|
| C-DGJLFET | 0.0160463 | 5.55E-16 | 1.81E-03 | 3.26E+12 | 0.50695 |
| R-DGJLFET | 0.0155242 | 2.92E-18 | 1.59E-04 | **5.45E+13** | 0.64851 |

**R-DGJLFET improvement over C-DGJLFET:**
- ION/IOFF ratio: **~16.7× higher** (5.45×10¹³ vs 3.26×10¹²)
- IOFF: **~190× lower** — significantly reduced leakage
- DIBL: Slightly lower — better short-channel effect control

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Silvaco ATLAS | TCAD device simulation |
| TonyPlot | Waveform and structure visualization |
| Python / Excel | Post-processing and graph generation |

---

## References

1. Raj, A., Sharma, S.K. Exploring the Potential of Dielectric Modulated SOI Junctionless FinFETs for Label-Free Biosensing. J. Electron. Mater. 53, 766–772 (2024). https://doi.org/10.1007/s11664-023-10844-6
