# CNC Pen Plotter

A custom A3-format CNC pen plotter designed in CAD and inspired by the [OpenBuilds ACRO DrawBot](https://openbuilds.com/). The design uses V-slot aluminium extrusions, GT2 belt motion, three NEMA 17 stepper motors, and a servo-driven pen-lift mechanism.

> **Project status: CAD and documentation phase.** The repository's firmware notes state that the machine has not yet been assembled and that the final FluidNC configuration has not been tested. The files here document the planned build; physical motion and drawing have not been verified.

![CNC Pen Plotter CAD render](Images/render1.png)

## Quick links

- [Project video/demo on YouTube](https://youtu.be/2c1DS8Nv8dU)
- [Hack Club Forge project page](https://forge.hackclub.com/projects/3639)
- [Latest release (v1.0)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/tag/v1.0)
- [Assembly guide PDF (download from the release)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/download/v1.0/GUIDE_updated.pdf)
- [Updated BOM spreadsheet](BOM/CNC_Pen-ploter_updated_(sheet2).xlsx)
- [BOM CSV](BOM/BOM.csv)
- [Onshape CAD assembly](https://cad.onshape.com/documents/cf470daa2010d17c98d59f14/w/9217e9e7d147d62c9b62fa11/e/110cbc33f4cd917d186821d2?renderMode=0&uiState=6a961a29e612142b9e0b4a56)

## Overview

This project is a planned A3-format pen plotter for writing and drawing. The design was developed in Onshape, with a full assembly and exported STEP files in the repository. The mechanical design includes an X carriage, two Y-axis motor assemblies, V-slot wheels and extrusions, GT2 belts, a servo pen lift, electronics mounting, and cable routing.

The repository contains design files and assembly documentation. It is not yet a validated, ready-to-build machine: the firmware configuration is a placeholder pending assembly and testing.

## Planned features

- A3-format drawing target (the actual usable drawing area has not yet been measured).
- Belt-driven X/Y motion using GT2 belts and V-slot extrusions.
- Three NEMA 17 stepper motors: one for X and two for Y.
- Servo-driven pen-up / pen-down mechanism using an SG90-class servo.
- Two limit switches planned for homing.
- MKS DLC32 V2.1 controller running FluidNC.
- STEP exports and STL files for the CAD and printable components.

These are design intentions and documented component choices, not claims that the assembled machine has been tested.

## Planned hardware

| Component | Planned specification | Notes |
|---|---|---|
| Controller | MKS DLC32 V2.1 (ESP32-based) | FluidNC is planned; final configuration is untested. |
| Stepper motors | 3 × NEMA 17, 42 × 42 mm | 1 × X and 2 × Y, as described in the planned pinout. |
| Motor drivers | 3 × DRV8825 | Listed in the assembly guide/BOM. |
| Pen lift | 1 × SG90 servo | Intended for pen-up / pen-down movement. |
| Limit switches | 2 | One planned for X and one for Y homing. |
| Power supply | Mean Well LRS-150-24, 24 V DC | Verify wiring and protection before powering. |
| Motion system | GT2 belt drive, 20-tooth pulleys, Delrin V-wheels | See the BOM for quantities and supplier references. |
| Frame | 2020 / 2040 V-slot aluminium extrusion | Exact cut lengths and hardware are in the BOM and guide. |
| Voltage converter | XL6009 DC-DC module | Voltage/current settings and the exact servo power arrangement still need commissioning checks. |

**Important:** This table summarizes the planned design. Check the current BOM, CAD, and assembly guide together before ordering or wiring parts. Prices and supplier availability can change.

## Bill of materials

- [Updated BOM spreadsheet (XLSX)](BOM/CNC_Pen-ploter_updated_(sheet2).xlsx)
- [BOM CSV](BOM/BOM.csv)
- [BOM folder and historical files](BOM/)

The BOM lists mechanical hardware, extrusions, printed parts, electronics, wires, connectors, and supplier links. Treat the listed prices and total as estimates, not live quotes. The separate [BOM notes](BOM/README.md) currently contain older filenames and a cost summary; consult the XLSX/CSV as the main item-level references and reconcile the summary before relying on its total.

## Assembly guide

Download the 41-page [CNC Pen Plotter Assembly & Wiring Guide (PDF)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/download/v1.0/GUIDE_updated.pdf) from the [v1.0 release](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/tag/v1.0).

The guide includes:

- Overall assembly illustration and parts lists (pages 1–4)
- X-axis carriage and assembly (pages 5–12)
- Y-axis carriages and assembly (pages 13–19)
- Main axis/frame assembly (pages 20–26)
- Servo pen-lift assembly (pages 27–30)
- Electronics mounting (pages 31–36)
- Wiring sequence (pages 37–41)

Review the complete guide before assembly. In particular, carefully verify power-supply polarity, voltage-converter settings, controller connections, and switch/servo pin assignments against the hardware documentation before applying power.

## CAD files

The repository includes exported CAD files:

- [Complete assembly — STEP](CAD/Final%20Build.step)
- [Complete assembly with cables — STEP](CAD/Final%20Build%20with%20Cables.step)
- [Assembly export — ZIP](CAD/Final%20Build.zip)
- [Printable and component CAD files](CAD/3D%20print/)
- [Onshape assembly](https://cad.onshape.com/documents/cf470daa2010d17c98d59f14/w/9217e9e7d147d62c9b62fa11/e/110cbc33f4cd917d186821d2?renderMode=0&uiState=6a961a29e612142b9e0b4a56)
- [Earlier Onshape document](https://cad.onshape.com/documents/d076f74775598c2c224d3ddc/w/a742f32d9e5f68d3a0ed4f3e/e/59cbca8dd54cfc34bc3f8ac0?renderMode=0&leftPanel=false&uiState=6a25ab40411915944ca1e2be)

The [3D print folder README](CAD/3D%20print/README.md) lists printed parts and recommended print settings. Some names in that guide do not match the exported filenames, so check the actual filenames in the folder before slicing.

## Electronics and firmware

- [Firmware overview](Firmware/README.md)
- [Planned pinout](Firmware/fluidnc-pinout.md)
- [FluidNC configuration placeholder](Firmware/fluidnc-config.yaml)
- [FluidNC project](https://github.com/bdring/FluidNC)
- [Makerbase MKS DLC32 resources](https://github.com/makerbase-mks/MKS-DLC32)

The current `fluidnc-config.yaml` contains only a TODO comment. The pinout document is marked as planned and does not yet specify final GPIO assignments. Do not flash the placeholder as a working configuration. Complete and validate the pin mapping, motor directions, steps/mm, travel limits, homing behaviour, and servo settings during commissioning.

## Development images

- [Development timeline and screenshots](Images/README.md)
- [Overall CAD render](Images/render1.png)
- [Belt routing](Images/Belt.png)
- [Controller placement](Images/Cotroller.png)
- [Pen-lift mechanism](Images/pen_lift.png)

These images document the CAD/design work; unless explicitly labelled otherwise, they should not be interpreted as photographs of a completed, operating machine.

## Current status and roadmap

Status based on the repository documentation:

- [x] CAD assembly and design files exported
- [x] BOM files committed
- [x] Assembly and wiring guide published as a release asset
- [x] Planned hardware selected and documented
- [ ] Parts ordered and received — confirm current status
- [ ] Mechanical assembly completed
- [ ] Electronics wiring inspected and tested
- [ ] FluidNC configuration completed and validated
- [ ] Motor directions, homing switches, and pen servo tested
- [ ] First controlled motion test
- [ ] First drawing test

Update this checklist as the physical build progresses, and distinguish completed tests from planned work.

## Safety

This design includes mains-powered equipment and a 24 V DC power supply. Mains wiring can cause serious injury or fire. Disconnect power before changing wiring, verify protective earthing and strain relief, use suitable fusing and enclosures, and have mains-side work checked by a qualified person. Confirm the controller, drivers, servo, and converter wiring from their manufacturers' documentation before powering the machine.

## Credits and licensing

This design is inspired by the [OpenBuilds ACRO DrawBot](https://openbuilds.com/). Please consult the upstream project for its original design and attribution details.

The repository includes [LICENSE.md](LICENSE.md), which applies the **CERN Open Hardware Licence Version 2 — Strongly Reciprocal (CERN-OHL-S v2)** to covered source. Read the complete licence before reusing or distributing the design. External components, upstream designs, and third-party software may have their own terms.

## Contributing and feedback

Issues and corrections are welcome. Helpful contributions include verified assembly photos, tested FluidNC pin assignments, measured travel limits, reproducible drawing tests, corrected BOM links, and improvements to the assembly guide.

When reporting a problem, include the file or assembly step involved, the hardware revision, and what you observed.
