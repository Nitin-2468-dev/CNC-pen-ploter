# CNC Pen Ploter

This is an A3 CNC pen plotter inspired by the OpenBuilds ACRO system and designed for handwriting, drawing, and future painting experiments.

The machine uses a V-slot motion system, FluidNC firmware, and a custom servo-powered pen-lift mechanism.

![Render](Images/render1.png)

## Features

* A3 drawing area
* FluidNC controller
* MKS DLC32 V2.1
* Servo pen lift
* GT2 belt drive
* V-slot aluminum extrusion frame
* Future laser upgrade support

## Specifications

| Item          | Value                                   |
| ------------- | --------------------------------------- |
| Working Area  | A3                                      |
| Motion System | GT2 Belt Drive                          |
| Controller    | MKS DLC32 V2.1                          |
| Firmware      | FluidNC                                 |
| Motors        | 3 × NEMA17 Stepper Motors               |
| Pen Lift      | SG90 Servo                              |
| Frame         | 2020 / 2040 V-Slot Aluminium Extrusions |
| Power Supply  | Meanwell LRS-150-24                     |

## Bill of Materials

The updated BOM is provided as an Excel spreadsheet, with a CSV copy for quick reference.

* [Updated BOM Spreadsheet](./BOM/CNC_Pen-ploter_updated_(sheet2).xlsx)
* [BOM CSV](./BOM/BOM.csv)
* [Cost Summary](./BOM/Cost-Summary.md)

## Assembly Guide

* [CNC Pen Plotter Assembly & Wiring Guide](./Docs/GUIDE_updated.pdf)

The guide contains the complete 41-page assembly sequence, parts lists, axis assembly, pen-lift assembly, electronics assembly, and wiring steps.

## CAD Files

The complete CAD assembly, source files, and design history are available on Onshape:

* [View Onshape Project](https://cad.onshape.com/documents/cf470daa2010d17c98d59f14/w/9217e9e7d147d62c9b62fa11/e/110cbc33f4cd917d186821d2?renderMode=0&uiState=6a961a29e612142b9e0b4a56)

* [old Onshape Project](https://cad.onshape.com/documents/d076f74775598c2c224d3ddc/w/a742f32d9e5f68d3a0ed4f3e/e/59cbca8dd54cfc34bc3f8ac0?renderMode=0&leftPanel=false&uiState=6a25ab40411915944ca1e2be)

3D printable components can be found here:

* [Printed Parts](./CAD/3D%20print/README.md)

## Electronics

The assembly guide includes the current electronics mounting and wiring sequence. Controller configuration files and FluidNC settings are located in the [`Firmware`](./Firmware/README.md) directory.

## Build Status

* [x] CAD Design Complete
* [x] Bill of Materials Complete
* [ ] Parts Ordered
* [ ] Parts Received
* [ ] Assembly Complete
* [ ] Electronics Wired
* [ ] First Motion Test
* [ ] First Drawing

## Gallery

### CAD Animation

* [Watch Demo Video](https://www.youtube.com/watch?v=2c1DS8Nv8dU)

* [Development](./Images/README.md)

![Belt](./Images/Belt.png)
![Controller](./Images/Cotroller.png)
![Pen lift](./Images/pen_lift.png)


[![GUIDE](./Docs/01.png)](./Docs/README.md)

## License

This project is licensed under the CERN Open Hardware Licence Version 2 - Strongly Reciprocal (CERN-OHL-S v2).

See [LICENSE.md](./LICENSE.md) for details.
