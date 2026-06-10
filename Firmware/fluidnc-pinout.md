# Planned Pinout

## Controller

* MKS DLC32 V2.1
* Firmware: FluidNC

## Motors

| Axis   | Motor Count |
| ------ | ----------: |
| X Axis |  1 × NEMA17 |
| Y Axis |  2 × NEMA17 |
| Total  |  3 × NEMA17 |

The two Y-axis motors are mechanically linked and move the gantry on both sides of the machine.

## Pen Lift

| Device     | Quantity |
| ---------- | -------: |
| SG90 Servo |        1 |

Used for pen up / pen down movement.

## Limit Switches

| Axis   | Quantity |
| ------ | -------: |
| X Axis |        1 |
| Y Axis |        1 |
| Total  |        2 |

Used for homing and machine positioning.

## Power Supply

| Device         | Specification       |
| -------------- | ------------------- |
| Power Supply   | Meanwell LRS-150-24 |
| Output Voltage | 24V DC              |
| Max Current    | 6.5A                |

## Planned Connections

* X Motor
* Left Y Motor
* Right Y Motor
* SG90 Pen Lift Servo
* X Limit Switch
* Y Limit Switch
* 24V Power Input

Final FluidNC pin assignments will be added after assembly and testing.
