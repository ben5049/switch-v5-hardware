# Switch v5 Errata

## Contents

- [1 Switch v5](#1-switch-v5)
    - [1.1 Wrong IO voltage on switch 1 ports 3 & 4](#11-wrong-io-voltage-on-switch-1-ports-3--4)


## Key

- A = limitation present, workaround available
- N = limitation present, no workaround available
- P = limitation present, partial workaround available
- "-" = limitation absent

## 1 Switch v5

| **Bug**                                                                                 | **5.0.0** | **5.1.0** |
|-----------------------------------------------------------------------------------------|-----------|-----------|
| [Wrong IO voltage on switch 1 ports 3 & 4](#11-wrong-io-voltage-on-switch-1-ports-3--4) | A         | -         |

### 1.1 Wrong IO Voltage on Switch 1 Ports 3 & 4

The IO voltage on the SJA1105Q switch chip 1 ports 3 and 4 is incorrectly set to 3.3V when it should be set to 1.8V. This means PHY 3 doesn't work, and no data can be transferred between the left half of the switch (PHYs 0-3) and the right half of the switch (PHYs 4-6 and the host MCU). By cutting two planes and soldering on a wire between the port 3 & 4 supply capacitors and 1.8V, it is possible to fix this issue. However PHY3 and switch 0 may be damaged if the device was turned on and traffic was sent into switch 1.

![]()

