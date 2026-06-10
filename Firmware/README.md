# Firmware

CNC Pen Ploter uses FluidNC running on an MKS DLC32 V2.1 controller.

## Controller

- MKS DLC32 V2.1
- ESP32 Based
- Wi-Fi Enabled

## Firmware

FluidNC

## Current Status

The machine has not yet been assembled, therefore the final firmware configuration has not been tested.

Configuration files included in this directory are based on the planned hardware layout and may require adjustment during commissioning.

## Planned Hardware

| Device | Quantity |
|----------|---------:|
| NEMA17 Stepper Motor | 3 |
| SG90 Servo | 1 |
| Limit Switch | 2 |
| MKS DLC32 V2.1 | 1 |

## Planned Features

- XY Motion Control
- Servo Pen Lift
- Homing Switches
- Web UI Control
- Wi-Fi Connectivity
- G-code Streaming

## References

- https://github.com/bdring/FluidNC
- https://github.com/makerbase-mks/MKS-DLC32