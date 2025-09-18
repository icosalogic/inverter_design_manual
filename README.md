Note: This document is under construction.

# Introduction

This document describes the design and implementation of high voltage, high current DC-AC inverters for residential markets.
In this case, "high voltage" means that the source battery for the inverter is high enough that it can power the inverter without a transformer, even at minimum state-of-charge (SoC).
High current means that the inverter design is capable of implementing at least 100-amp and 200-amp inverters, and possibly even 300-amp or 400-amp inverters.

# Residential Inverter Market

This design is primarily targeted to the North American inverter market, which uses a nominal 120V 60 Hz standard.
Most dwellings have a electrical supply consisting of 3 wires, L1, L2 and neutral.
L1 and L2 are 180 degrees out of phase, and provide 120V service with respect to the neutral wire.
L1 and L2 can be used in tandem to provide a nominal 240V supply for appliances that require more power.
It is common for average-sized dwellings to have 100 amp supply, with newer and larger homes use 200 amp or even 300 amp supplies.

# Inverter Architecture

TBD

## Half Bridge vs T-Type

TBD

# Battery

The requirement for the battery is that it is able to provide sufficient voltage and current.
Since a 120V RMS voltage source has a peak voltage of 169.7V, the peak-to-peak voltage is 339.4V.
Using the T-Type architecture as explained above, the battery will have 3 lines: positive, middle (0V) and negative.
Generally, this will be provided by a battery with two identical halves, which together have sufficient voltage
headroom to provide adequate power to the inverter at minimum SoC.

The following table describes possible battery configurations for the two most common lithium chemistries.

| Chemistry | Cell Min V | Cell Max V | S Half | S Full | Half Min V | Half Max V | Full Min V | Full Max V |
| --------- | ---------- | ---------- | ------ | ------ | ---------- | ---------- | ---------- | ---------- |
| Li        | 3.0        | 4.2        | 64     | 128.0  |    192.0   |    268.8   |   384.0    |    537.6   |
| LiFePo    | 3.0        | 3.65       | 72     | 144.0  |    216.0   |    262.8   |   432.0    |    525.6   |

# DC Link Capacitor

TBD

# MOSFETs

TBD

# Output Filter

TBD

## LCL vs LC Filters

TBD

# Cooling

TBD

# Considerations for Optimization

Residential electrical usage has a lot of transients.
Air conditioners, hot water heaters, ovens, etc. turn on and off.
Many devices like microwaves, toaster ovens, and coffe makers are used for at most a few minutes at a time, at most a few times a day.
Here is an example usage graph from my house in California.
The house has 100 amp electrical panel, and has gas water heater, clothes dryer, furnace and stove top.
Everything else is electric.

![Example residential electrical usage](media/usage_20250626.png)

Aggregating this data for a whole year and plotting a histogram of KW used per minute yeilds the following graph.

![Residential usage histogram](media/usage_histogram_2024.png)

If you sum the minutes the inverter would need to run at a given power level, you get the following graph.

![Residential cumulative usage](media/usage_cumulative_2024.png)

This shows that the inverter would run 92.6% of the time at 1 KW or less, and 98.9% of the time at 2 KW or less.
This usage pattern would change with the conversion of the gas appliances to electric, and even more with the purchase of an EV.
Even so, the point remains:  Inverters spend the majority of their time running at very low power levels, and design
optimizations should take this into consideration.
Designers should not focus all their attention on optimizing an inverter at maximum power, while ignoring
optimizations at lower power levels.

# Summary

TBD

