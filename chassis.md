This document is under construction.

# Introduction

This document describes the 8-blade inverter chassis discussed in [1].
This includes everything in the inverter, except the blades.

Here are the included components:

1. 8-blade box
2. Battery connectors and bus bars
3. L1, L2, Neutral connectors and bus bars
4. Controller board
5. Power measurement board
6. L1 blade signal board
7. L2 blade signal board
8. Cooling (TBD)

# Safety Warning

This inverter design uses a high-voltage DC connections for the battery which pose a serious
risk of injury or death if mishandled.

The AC voltages can also be fatal.

Extreme caution must be used when working on this equipment.

# 8-Blade Box

The box containing the inverter has a width of 17.23 inches / 437.65 mm and a
height of 10.5 inches / 266.7 inches.
With those dimensions, it will take 6U in a 19 inch / 482.6 mm rack.
It can also be placed into a non-rack configuration.

The depth of an 8-blade chassis is 31.75 inches / 806.35 mm.

The orientation of the X/Y/Z axis for positions mentioned in this document are:

X -- positive towards the viewer, negative away from the viewer, 0 is the back edge of the front panel that mounts to the rack
Y -- positive to the right, 0 is the center of the front panel
Z -- positive is up, 0 is the bottom edge of the front panel

# Battery Connectors and Bus Bars

The inverter has three connections to the battery:

1. Battery positive
2. Battery midpoint (Neutral)
3. Battery negative

The battery connections on the chassis use SurLok Plus connectors.
These connectors are more expensive, but have minimized exposed electrical surfaces which reduces
the risk of accidental electrocution, compared to connectors with exposed wires.
This is a serious concern with the 500-600 volt batteries used with this inverter.

These connectors are 35 mm wide.
With 5 mm spacing between connectors, they are mounted 40 mm center-to-center.

The battery bus bars are copper straps 1/8 inch / 3.175 mm thick and 1/2 inch / 12.7 mm wide.
With a J value of 5A / mm<sup>2</sup>, these bus bars have a current capacity of 201.6 amps.

The bus bars are composed of 2 sections.
The bottom section runs along the bottom of the inverter chassis to the front of the chassis,
and part way up the front.
There is a 4 inch / 101.6 mm gap, and the top section of the bus bars runs the rest of the way
to the top of the chassis, over to the connectors and down to the connector mounting studs.

The bottom section of the bus bars has a spacing between the bars of 0.63 inch / 16 mm, with a
center-to-center spacing of 1.13 inch / 28.7 mm.
The top section of the bus bars has a spacing of 40 mm center-to-center.

The power measurement board connects the two sections of each bus bar and provides voltage and
current measurement for each bus bar.
This board also compensates for the different spacing between the top and bottom sections of the bus bars.

The connection from the blade to a bus bar is via a copper tab bent 90 degrees with a 3 mm bend radius.
The thickness of the copper tab is set by the blade designer, but the width is the same as the bus bar.


# L1, L2, Neutral Connectors and Bus Bars

The inverter has three connections for AC output:

1. Line 1 (L1)
2. Line 2 (L2)
3. Neutral

The recommended connector to use for AC output is the same SurLok Plus connectors used for the battery.
As noted above, these connectors are 35 mm wide, and with a 5 mm spacing, are mounted 40 mm
center-to-center.

The AC bus bars are copper straps 1/8 inch / 3.175 mm thick and 3/4 inch / 19 mm wide.
With a J value of 5A / mm<sup>2</sup>, these bus bars have a current capacity of 301.6 amps.

The bus bars are composed of 2 sections.
The bottom section runs along the bottom of the inverter chassis to the front of the chassis,
and part way up the front.
There is a 4 inch / 101.6 mm gap, and the top section of the bus bars runs the rest of the way
to the top of the chassis, over to the connectors and down to the connector mounting studs.

The bottom section of the bus bars have a spacing between the bars of 0.63 inch / 16 mm, with a
center-to-center spacing of 1.38 inch / 35 mm.
The top section of the bus bars has a spacing of 40 mm center-to-center.

The power measurement board connects the two sections of each bus bar and provides voltage and
current measurement for each bus bar.
This board also compensates for the different spacing of the top and bottom sections of the bus bars.

# Power Measurement Board

TBD

# Controller Board

TBD

# L1 Blade Signal Board

The L1 blade signal board connects the digital signals and low voltage power from the controller
board to the 4 L1 blades.

## Controller Connector

The controller connector is a 2x12 connector with 0.1 inch / 2.54 mm spacing, and the following pins:

The letters after the pin numbers have the following meanings:

| Letter | Meaning                         |
| ------ | ------------------------------- |
|    P   | Power                           |
|    C   | Signal from controller to blade |
|    B   | Signal from blade to controller |

 1. P 24 volt supply (for gate driver)
 2. P 24 volt supply
 3. P 3.3 volt supply
 4. P 3.3 volt supply
 5. P Ground
 6. P Ground
 7. B B1 Presence pin.  Weak pull down resistor.
 8. B B2 Presence pin
 9. B B3 Presence pin
10. B B4 Presence pin
11. C B1 Disable pin
12. C B2 Disable pin
13. C B3 Disable pin
14. C B4 Disable pin
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

## Blade Connector

There is one blade connector for each of the four L1 blades.
The blade connector is a 2x12 connector with with 0.1 inch / 2.54 mm spacing, and the following pins:

 1. P 24 volt supply (for gate driver)
 2. P 24 volt supply
 3. P 3.3 volt supply
 4. P 3.3 volt supply
 5. P Ground
 6. P Ground
 7. B Presence pin.  Strong pull up resistor on the blade
 8. C Disable pin.  Disables gate drivers for this blade.
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


# L2 Blade Signal Board

TBD

# Cooling

TBD

# References

1. [Inverter Design Manual](https://github.com/icosalogic/inverter_design_manual)
