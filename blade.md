This document is under construction.

# Introduction

This document describes the layout and interfaces for the blade board used in the inverter.
The blade holds all the power components and some logic components for switching.
Populating the inverter chassis with an appropriate number of blades, the inverter's
target power level can be reached.

The inverter has slots for 4 blades each for L1 and L2.

# Blade board dimensions

The blade is 434 mm long, 240 mm wide, and 3.175 mm thick / 17.09 inch by 9.45 inch by 0.125 inch.
This is twice as thick as an average PCB because the average 1/16 inch 1.6 mm PCB flexes noticeably
from the weight of the large inductor.

All the connections on the blade are along the bottom edge of the blade that is first
inserted into the inverter chassis.

The following table shows the location of the connections located along the right bottom
edge of the blade when viewed from the front of the inverter.
All the conductors are separated by 16 mm.

Dimensions are in mm.

| Connection       | Offset | Width |
| ---------------- | ------ | ----- |
| Battery Positive |  16.00 | 12.70 |
| Battery Middle   |  44.70 | 12.70 |
| Battery Negative |  73.40 | 12.70 |
| Signal Connector | 102.10 | 30.48 |
| Neutral          | 148.58 | 19.05 |
| Line Alt         | 183.63 | 19.05 |
| Line Out         | 218.68 | 19.05 |

# Power Connections

There are 5 power connections for the blade:

1. Battery positive
2. Battery middle
3. Battery negative
4. Line output
5. Neutral (connected to battery middle)

These connections attach to the main power conductors running along the floor of the inverter chassis.
Attachment is by threaded fasteners through the conductor bus and the blade connector.
The dimensions of these connections are sized according to the power level of the blade.

All power traces on the blade are the same thickness -- 0.022 inch / 0.5588 mm / 17 oz.

The width of the battery traces on the blade is 0.5 inch / 12.7 mm.
The width of the output traces is 0.75 inch / 19.35 mm.

# Signal Connections

The signal connections provide power for the gate drivers and ancillary logic running on the blade.
There is also additional connections to permit the main controller to detect the presence of a
blade and identify the blade variant.

The signal connector is a 2x12 header on a board near the floor of the inverter chassis,
parallel to the power busses.

Here are the pin assignments for the signal connector:

 1. P 24 volt supply (for gate driver)
 2. P 24 volt supply
 3. P 3.3 volt supply
 4. P 3.3 volt supply
 5. P Ground
 6. P Ground
 7. B Presence pin.  Weak pull down resistor on the chassis, strong pull up resistor on the blade
                     allows the controller to detect when a blade is inserted at that position.
 8. C Disable pin.  Disables gate drivers for this blade.  Allows controller to determine output power and efficiency.
 9. B A0 -- I2C / blade address.
10. B A1 -- I2C / blade address.
11. B A2 -- I2C / blade address.
12. TBD
13. TBD
14. TBD
15. P Ground
16. P Ground
17. C Q1 -- Gate driver signal for Q1 MOSFET
18. C Q2 -- Gate driver signal for Q2 MOSFET
19. C Q3 -- Gate driver signal for Q3 MOSFET
20. C Q4 -- Gate driver signal for Q4 MOSFET
21. P Ground
22. P Ground
23. C SDA -- I2C data signal
24. C SCL -- I2C clock signal

The dimenasions of the 2x12 connector are 1.2 inches / 30.48 mm long by 0.2 inch / 0.508 mm wide.

Each blade position in the chassis is wired with a unique I2C/blade address.
Even if blades have different power components, the I2C components are identical.
There are two I2C components on each blade:

1. A 16-bit 8-channel ADC for reading the temperature of the MOSFETs, capacitors and inductor.
2. An 8- or 16-bit GPIO expander that the controller can access to determine the blade variant and perform other TBD operations.

The bit assignments for the GPIO expander are:

0. BV0 -- Blade variant bit 0
1. BV1 -- Blade variant bit 1
2. BV2 -- Blade variant bit 2
3. BV3 -- Blade variant bit 3
4. BV4 -- Blade variant bit 4
5. TBD
6. TBD
7. TBD

This architecture allows a large number of blade variants to be developed and supported without
requiring incompatible changes to the chassis/blade interface.
It also allows the same controller software to run on chassis with different numbers of available
blade positions.

When a blade is inserted, A0 and A1 are used to set the I2C address of the components on that blade.
A2 and A3 are used by the controller to set the output channel of an I2C multiplexer.
Every 4 blade positions are grouped together and accessed through a unique channel of the multiplexer.
This allows supporting 16 (or more) blades, even if the I2C components on the blade support only a maximum of 4 unique addresses.

At start up, the main controller scans the presence bits for each blade position, to determine
if a blade is inserted at that position.
The controller then queries the GPIO expander on each blade to identify what variant is inserted.
After that, the controller knows the hardware configuration and can proceed starting inverter operation.
