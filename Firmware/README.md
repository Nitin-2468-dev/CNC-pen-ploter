# CNC Pen Plotter — FluidNC Firmware

This folder contains the planned controller information and configuration for the CNC Pen Plotter. The controller is an **MKS DLC32 V2.1** running **FluidNC**.

> [!WARNING]
> **Development draft — not tested on a physical machine.** The plotter has not yet been assembled and commissioned. Do not upload the configuration and run motion commands until the motor outputs, limit-switch inputs, servo signal pin, travel, direction, and step calibration have been verified against the actual board and wiring.

## Hardware

| Component                 | Quantity | Purpose                                                                                         |
| ------------------------- | -------: | ----------------------------------------------------------------------------------------------- |
| MKS DLC32 V2.1            |        1 | ESP32-based motion controller                                                                   |
| NEMA 17 stepper motors    |        3 | One X-axis motor and two Y-axis motors                                                          |
| SG90 servo                |        1 | Pen up / pen down movement                                                                      |
| Mechanical limit switches |        2 | X and Y homing                                                                                  |
| Mean Well LRS-150-24      |        1 | 24 V DC power supply                                                                            |
| DC buck converter         |        1 | Step down 24 V to the servo's required supply voltage; set and measure output before connecting |

The two Y motors move opposite sides of the gantry and must be configured so they move the gantry together. The current plan is to use the controller's X and Y driver outputs for X and the left Y motor, then use the Z driver output as the second motor on the logical Y axis.

## Files in this folder

- [`fluidnc-config.yaml`](./fluidnc-config.yaml) — proposed FluidNC machine configuration; requires verification and commissioning.
- [`fluidnc-pinout.md`](./fluidnc-pinout.md) — planned controller connections and wire schedule.
- [Assembly guide (PDF)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/download/v1.0/GUIDE_updated.pdf) — the 41-page guide includes the assembly sequence, electronics assembly, and wiring steps.

## Planned motor and limit-switch mapping

The signal names below follow the standard MKS DLC32 V2.1 FluidNC reference configuration. Confirm the labels and wiring on your exact board before use.

| Logical axis / motor   | Driver output | Step output | Direction output | Limit input                                                                |
| ---------------------- | ------------- | ----------- | ---------------- | -------------------------------------------------------------------------- |
| X / `motor0`           | X             | `I2SO.1`    | `I2SO.2`         | X−, commonly `gpio.36` in the reference configuration                      |
| Y / `motor0` (left Y)  | Y             | `I2SO.5`    | `I2SO.6`         | Y−, commonly `gpio.35` in the reference configuration                      |
| Y / `motor1` (right Y) | Z             | `I2SO.3`    | `I2SO.4`         | Uses the logical Y-axis homing arrangement; verify direction and mechanics |

Using the Z driver output for the second Y motor is a **proposed mapping**, not an extra Z movement axis. FluidNC must define both motors under the same logical Y axis and their directions must be tested at low speed before normal operation.

## Servo / pen lift — resolve the pin assignment first

The SG90 needs three connections: signal, regulated supply, and ground. The planned power path is:

1. The 24 V supply feeds the DLC32 controller and the buck converter input.
2. Adjust the buck converter and measure its output at **5.0 V** before connecting the servo.
3. Connect buck output positive to servo V+, and buck output ground to servo GND.
4. Connect the servo signal to a controller output confirmed to support the intended FluidNC RC-servo configuration. The controller and servo must share a common ground reference.

> [!CAUTION]
> The current local `fluidnc-config.yaml` draft assigns the servo signal to `gpio.22`. The standard MKS DLC32 V2.1 reference configuration uses `gpio.22` for the probe input. **Do not assume GPIO22 is available for the servo.** Verify the board's actual servo header/pin mapping, then update the YAML and wiring diagram together before use. Do not connect the servo signal to a pin based only on a connector label without checking the board pin map.

## Motion values that still need calibration

The proposed YAML includes starting values rather than measured machine settings:

- **80 steps/mm** assumes a 1.8° stepper, a 20-tooth GT2 pulley, 2 mm belt pitch, and 1/16 microstepping. Confirm the actual driver microstep setting.
- **X and Y travel values** are placeholders until the assembled machine's usable travel is measured.
- **Motor direction** must be checked with short, low-speed jogs. Both Y motors must move the gantry without fighting each other.
- **Homing direction and switch state** must be checked before relying on homing or enabling soft limits.
- **Servo pulse limits and pen travel** must be tuned with the mechanism clear of mechanical stops.

Soft limits should stay disabled until homing and travel measurements are reliable. Use conservative feed rates during first tests.

## Commissioning checklist

- [ ] Confirm the board revision and physical X, Y, Z, endstop, and servo-related terminal labels.
- [ ] Confirm the selected stepper-driver modules and microstep jumpers/settings.
- [ ] With power off, check every motor coil pair and verify the wire order at both ends.
- [ ] Verify limit-switch wiring and the input's idle/pressed state in FluidNC.
- [ ] Resolve the servo signal pin conflict described above.
- [ ] Set the buck converter to the servo's rated voltage and measure it before connecting the servo.
- [ ] Confirm a shared ground between the controller and servo supply.
- [ ] Test each axis using short, low-speed moves with hands clear of the mechanism.
- [ ] Verify both Y motors move in the correct direction together; stop immediately if they oppose each other or rack the gantry.
- [ ] Verify homing direction and switch action before enabling soft limits.
- [ ] Update this README and the YAML with the tested values.

**Safety:** Never connect or disconnect stepper motors while the controller is powered. Disconnect power before changing wiring. The configuration and diagram are planning documents until tested on the real machine.

## References

- [FluidNC project](https://github.com/bdring/FluidNC)
- [Official MKS DLC32 V2.1 XYZ example](https://github.com/bdring/fluidnc-config-files/blob/main/official/MKS_DLC32_21_XYZ.yaml)
- [FluidNC configuration specification](https://github.com/bdring/FluidNC/blob/main/tools/fluidnc-config-spec.md)
- [MKS DLC32 repository](https://github.com/makerbase-mks/MKS-DLC32)

## Assembly and wiring guide

Rather than relying on the preliminary wiring-diagram image, use the illustrated [CNC Pen Plotter assembly guide (PDF)](https://github.com/Nitin-2468-dev/CNC-pen-ploter/releases/download/v1.0/GUIDE_updated.pdf). It contains the step-by-step assembly sequence, electronics assembly, and wiring instructions.

For the connection-by-connection reference, see [`fluidnc-pinout.md`](./fluidnc-pinout.md). The FluidNC configuration and pin mapping in this folder are still drafts and must be verified against the actual controller before powering the machine.
