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

The IO voltage on the SJA1105Q switch chip 1 ports 3 and 4 is incorrectly set to 3.3V when it should be set to 1.8V. This means PHY 3 doesn't work, and no data can be transferred between the left half of the switch (PHYs 0-3) and the right half of the switch (PHYs 4-6 and the host MCU). By cutting two planes and soldering on a wire between the port 3 & 4 supply capacitors and 1.8V, it is possible to fix this issue. However, PHY3 and switch 0 may be damaged if the device was turned on and traffic was sent at 3.3V.

To fix this issue two cuts need to be made. One from the top going down to inner layer 2, and one simpler one from the bottom. Both are shown in green in the images below:

![wrong-io-voltage-layout-top](/docs/images/wrong-io-voltage-layout-top.png)
![wrong-io-voltage-layout-bottom](/docs/images/wrong-io-voltage-layout-bottom.png)

After doing these cuts, a wire needs to be soldered to connect the now floating VDDIO_MII pins to 1.8V. The final bodge can be seen below:

![wrong-io-voltage-bodge-top](/docs/images/wrong-io-voltage-bodge-top.png)
![wrong-io-voltage-bodge-bottom](/docs/images/wrong-io-voltage-bodge-bottom.png)

Note that care must be taken not to damage the trace running parallel to the top cut since it is a 50MHz clock that drives PHYs 3 to 5.
