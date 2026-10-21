# uC-CDI

High-voltage power and trigger stage for a microcontroller-controlled
capacitor discharge ignition (CDI) system, intended for small engines.
An external MCU controls the charge enable and spark timing; this board
generates the high voltage, stores the discharge energy, and fires the
ignition coil. Board revision: v0.9.

## Hardware

### Charging stage
- LM2577T-ADJ switching regulator (U1) configured as a flyback/boost
  converter, driving custom transformer T1 (22 T / 330 T / 21 T windings on
  an E20 core) to generate the high-voltage rail
- UF4007 fast-recovery rectifiers (D2, D6, D7) in the HV path
- 1.5 µF discharge/storage capacitor (C4)
- Charge-voltage regulation through zener feedback into the LM2577 FB pin
  (D2/D4 network), with 120 V (D10), 200 V (D9) and 24 V (D4) zener clamps

### Discharge / trigger stage
- TIC116 SCR (Q3) dumps the storage capacitor into the ignition coil
- Isolated gate drive through pulse transformer T2 (1P:1S)
- 2N7002K small-signal MOSFET (Q2) in the trigger path, driven by the
  external MCU timing signal
- Separate grounds (GND / GND1) isolating the control side from the
  ignition side

### Interface
External connections (power in, trigger in, HV output to the coil, grounds)
are broken out on through-hole test-point pads TP1–TP6.

## Repository contents

| File                        | Description                            |
|-----------------------------|----------------------------------------|
| `board-v09.kicad_pro`       | KiCad 7 project file                   |
| `board-v09.kicad_sch`       | Schematic                              |
| `board-v09.kicad_pcb`       | PCB layout (mixed SMD/THT)             |

## Requirements

- KiCad 7 or later

## Warning

This board generates and stores several hundred volts. The 1.5 µF
discharge capacitor can hold a lethal charge after power is removed —
verify it is fully discharged before handling.

## Status

Work in progress — schematic and PCB layout exist (v0.9).
No firmware in this repository.

## License

No license file is currently included; the design files are provided as-is.
