# KiCAD JLCPCB Library Generator

Generate a KiCad symbol library (`.kicad_sym`) from a list of JLCPCB components while reusing stock KiCad footprints.

## What it does

- Reads a SQLite DB of components keyed by `LCSC` part number.
- Maps each part to a stock KiCad footprint.
- Generates a KiCad symbol library in the modern s-expression `.kicad_sym` format.
- Writes common symbol fields such as `Value`, `Footprint`, `Datasheet`, `LCSC`, `Manufacturer`, and `MPN`.
- Where possible adds fields from attributes and unit prices at 10,100,& 1k
- Libraries created by this are output to [FutureProofHomes/kicad-jlcpcb-libraries](https://github.com/FutureProofHomes/kicad-jlcpcb-libraries)

## What it does not do

- It does not generate custom footprints.
- It does not guarantee a valid mapping for every JLCPCB/LCSC package.
- It does not fetch live catalog data; this project uses a 3rd party cached BD from JLCPCB, updated daily, see [upstream](https://yaqwsx.github.io/jlcparts).

## Repository layout

```text
.
├── README.md
├── src/
│   ├── jlc_kicad_lib/
│   |   ├── __init__.py
│   |   ├── footprint_lookup.py
│   |   ├── generator.py
│   |   ├── library_definition.py
│   |   └── main.py
|   ├── kicad-library-utils
|   └── kicad-symbols
```

## Quick start

```bash
./generate.sh
```

## Input

The github action checks for changes in the remote library every 30 minutes, if there is it triggeres a run.
This script fetches the latest SQLite DB from https://yaqwsx.github.io/jlcparts and generates some basic libraries from it.

## Current scope

This scaffold supports a small set of symbols:

- Resistors (SMD Chip)
- Resistor array (SMD Chip)
- Capacitors (SMD MLCC, SMD Tantalum)
- Diodes (SMD General, Schottky, Zener)
- Inductors (SMD Ferrite Bead, SMD Inductor)
- LEDs (SMD)
- BJT's (SMD)
- MOSFET's (SMD)
