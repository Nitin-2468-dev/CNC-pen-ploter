# CNC Pen Plotter — Planned Pinout & Wiring

This page documents the **planned electrical connections** for the A3 CNC Pen Plotter using an MKS DLC32 V2.1 controller running FluidNC.

For illustrated assembly and wiring steps, see the [CNC Pen Plotter assembly guide (PDF)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/download/v1.0/GUIDE_updated.pdf). This guide is easier to follow visually than the preliminary generated wiring diagram.

> **Status:** This is a design-level wiring plan, not a tested machine. The physical machine has not yet been assembled. The tables below use the connector labels from the CAD/wiring schedule; they do **not** claim that the final FluidNC GPIO configuration has been tested.

## 1. Controller and hardware

| Item           | Planned hardware                      | Qty. | Purpose                                 |
| -------------- | ------------------------------------- | ---: | --------------------------------------- |
| Controller     | MKS DLC32 V2.1                        |    1 | CNC motion controller                   |
| Firmware       | FluidNC                               |    1 | Motion control and G-code               |
| X motor        | NEMA 17 stepper                       |    1 | Moves the X-axis carriage               |
| Y motors       | NEMA 17 stepper                       |    2 | Move the gantry on both sides           |
| Pen lift       | SG90 servo                            |    1 | Raises and lowers the pen               |
| X endstop      | KW11-3Z-style mechanical limit switch |    1 | X-axis homing input                     |
| Y endstop      | KW11-3Z-style mechanical limit switch |    1 | Y-axis homing input                     |
| Power supply   | Mean Well LRS-150-24                  |    1 | 24 V DC system power                    |
| Buck converter | DC-DC step-down converter             |    1 | Supplies low-voltage power to the servo |

The two Y motors are intended to operate as the two sides of the same Y axis. Their final FluidNC axis/motor configuration still needs to be checked when the controller configuration is prepared.

## 2. Controller connector labels used

These are the **physical connector/pin labels** in the wiring model. They are not ESP32 GPIO numbers.

| Controller connector | Pins used              | Connects to                  |
| -------------------- | ---------------------- | ---------------------------- |
| Main power           | `V24+`, `GND`          | LRS-150-24 output `V+`, `V-` |
| X motor output       | `1A`, `1B`, `2A`, `2B` | NEMA17-X coils A and B       |
| Y1 motor output      | `1A`, `1B`, `2A`, `2B` | NEMA17-Y1 coils A and B      |
| Y2 motor output      | `1A`, `1B`, `2A`, `2B` | NEMA17-Y2 coils A and B      |
| X endstop            | `GND`, `S`             | Limit Switch X `COM`, `NO`   |
| Y endstop            | `GND`, `S`             | Limit Switch Y `COM`, `NO`   |
| Servo signal         | `SERVO SIGNAL`         | Servo `SIG`                  |

## 3. Stepper motor wiring

Each stepper motor uses four conductors. The A and B coil designations below follow the current wiring schedule; verify the actual motor lead pairs against the motor documentation before powering the drivers.

| Wire ID | From                   | To                    | Conductor diameter | Color |
| ------- | ---------------------- | --------------------- | -----------------: | ----- |
| X1      | DLC32 / X Driver `1A`  | NEMA17-X / `COIL A+`  |             0.5 mm | Red   |
| X2      | DLC32 / X Driver `1B`  | NEMA17-X / `COIL A-`  |             0.5 mm | Blue  |
| X3      | DLC32 / X Driver `2A`  | NEMA17-X / `COIL B+`  |             0.5 mm | Green |
| X4      | DLC32 / X Driver `2B`  | NEMA17-X / `COIL B-`  |             0.5 mm | Black |
| Y1      | DLC32 / Y1 Driver `1A` | NEMA17-Y1 / `COIL A+` |             0.5 mm | Red   |
| Y2      | DLC32 / Y1 Driver `1B` | NEMA17-Y1 / `COIL A-` |             0.5 mm | Blue  |
| Y3      | DLC32 / Y1 Driver `2A` | NEMA17-Y1 / `COIL B+` |             0.5 mm | Green |
| Y4      | DLC32 / Y1 Driver `2B` | NEMA17-Y1 / `COIL B-` |             0.5 mm | Black |
| Y5      | DLC32 / Y2 Driver `1A` | NEMA17-Y2 / `COIL A+` |             0.5 mm | Red   |
| Y6      | DLC32 / Y2 Driver `1B` | NEMA17-Y2 / `COIL A-` |             0.5 mm | Blue  |
| Y7      | DLC32 / Y2 Driver `2A` | NEMA17-Y2 / `COIL B+` |             0.5 mm | Green |
| Y8      | DLC32 / Y2 Driver `2B` | NEMA17-Y2 / `COIL B-` |             0.5 mm | Black |

The four Y2 conductors are planned to run inside one grey cable sheath with an overall diameter of approximately 2.207 mm.

## 4. Power wiring

| Wire ID | From                    | To                     | Diameter | Color |
| ------- | ----------------------- | ---------------------- | -------: | ----- |
| P1      | LRS-150-24 / `V+`       | DLC32 / `V24+`         |     1 mm | Red   |
| P2      | LRS-150-24 / `V-`       | DLC32 / `GND`          |     1 mm | Black |
| B1      | LRS-150-24 / `V+`       | Buck converter / `IN+` |   0.5 mm | Red   |
| B2      | LRS-150-24 / `V-`       | Buck converter / `IN-` |   0.5 mm | Black |
| B3      | Buck converter / `OUT+` | Servo / `V5+`          |   0.5 mm | Red   |
| B4      | Buck converter / `OUT-` | Servo / `GND`          |   0.5 mm | Black |

**Important:** Set and measure the buck converter output to the servo's supported supply voltage before connecting the servo. Do not feed the 24 V supply directly to the servo. The buck converter input negative and controller ground are planned to share the LRS-150-24 `V-` reference as shown above.

## 5. Servo signal wiring

| Wire ID | From                   | To            | Diameter | Color  |
| ------- | ---------------------- | ------------- | -------: | ------ |
| S1      | DLC32 / `SERVO SIGNAL` | Servo / `SIG` |   0.5 mm | Yellow |

The servo has three connections: `V5+`, `GND`, and `SIG`. The signal lead is separate from the servo's power leads.

## 6. Limit switch wiring

The mechanical switches use `COM` and `NO` in the current design schedule. The switch's normally-open/closed behavior, FluidNC input polarity, homing direction, and pull-up settings must be checked during configuration and commissioning.

| Wire ID | From                    | To                     | Diameter | Color  |
| ------- | ----------------------- | ---------------------- | -------: | ------ |
| LIM1    | DLC32 / X Endstop `GND` | Limit Switch X / `COM` |   0.5 mm | Black  |
| LIM2    | DLC32 / X Endstop `S`   | Limit Switch X / `NO`  |   0.5 mm | Yellow |
| LIM3    | DLC32 / Y Endstop `GND` | Limit Switch Y / `COM` |   0.5 mm | Black  |
| LIM4    | DLC32 / Y Endstop `S`   | Limit Switch Y / `NO`  |   0.5 mm | Yellow |

## 7. Electrical connection summary

- **Power:** LRS-150-24 `V+` feeds the controller's `V24+` and the buck converter `IN+`. LRS-150-24 `V-` feeds controller `GND` and buck converter `IN-`.
- **Motors:** X1–X4 connect the X motor. Y1–Y4 connect the first Y motor. Y5–Y8 connect the second Y motor.
- **Pen lift:** B3/B4 supply servo power from the buck converter; S1 carries the controller's servo signal.
- **Homing:** LIM1/LIM2 connect the X switch; LIM3/LIM4 connect the Y switch.

## 8. FluidNC GPIO configuration status

The **physical wiring labels are documented above**, but the final FluidNC GPIO and axis configuration is not yet confirmed. The repository's [`fluidnc-config.yaml`](./fluidnc-config.yaml) is still a placeholder, and the hardware has not been assembled and tested.

Before treating this as a final operational pinout, verify:

- the exact DLC32 V2.1 motor-output labels and how both Y motors are driven by FluidNC;
- the controller's supported servo-signal output and its correct FluidNC configuration;
- the X/Y endstop input mapping and switch polarity;
- the actual motor coil pairs and rotation direction;
- power and ground continuity, and the buck converter output voltage.

Do not treat this plan as a tested firmware configuration. Update the GPIO mapping and `fluidnc-config.yaml` only once the precise board terminals and intended motor arrangement have been verified.

## References

- [CNC Pen Plotter assembly guide (PDF)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/download/v1.0/GUIDE_updated.pdf) — illustrated assembly and wiring steps.
- [Firmware directory](./README.md)
- [FluidNC configuration placeholder](./fluidnc-config.yaml)
- [FluidNC official MKS DLC32 V2.1 example configuration](https://github.com/bdring/fluidnc-config-files/blob/main/official/MKS_DLC32_21_XYZ.yaml) — reference only; it is not this machine's validated configuration.
- [MKS-DLC32 hardware wiring documentation](https://github.com/makerbase-mks/MKS-DLC32/wiki/Hardware-Wiring)
