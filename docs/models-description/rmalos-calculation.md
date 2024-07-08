# RMaLOS High-Level Functionality Overview  
  
## Introduction  
  
The `RMaLOS` class encapsulates a model for simulating signal propagation in a Rural Macro-cell-Line-of-Sight (RMa-LOS) environment for wireless communication systems. This document provides a high-level overview of the functionalities provided by the `RMaLOS` class and the methodologies it uses for performing various calculations.  
  
## Functionalities and Calculations  
  
The `RMaLOS` class offers three core methods, each designed to compute specific aspects of signal strength and quality in rural wireless communication scenarios:  
  
### 1. Path Loss Calculation (`pathloss`)  
  
The `pathloss` method computes the attenuation of the signal, known as path loss, as it travels from the base station (BS) antenna to the user equipment (UE) transmitter. The factors considered for this computation include:  
  
- `hbs`: The height of the BS antenna.  
- `hut`: The height of the UE transmitter.  
- `f`: The frequency at which the system operates.  
- `d`: The distance between the BS and UE.  
- `h`: The average height of the surrounding buildings.  
  
The method employs a specific path loss model tailored for line-of-sight conditions in rural areas. It introduces the concept of a breakpoint distance (`dbp`), which signifies a threshold beyond which the path loss increases at a different rate. Depending on whether the actual distance `d` is less than or greater than `dbp`, the method uses one of two formulas (`pl1` or `pl2`) to calculate the path loss.  
  
### 2. Transmit Power Per Resource Block Calculation (`ptxrb`)  
  
The `ptxrb` method determines the power allocated to each Resource Block (RB), a fundamental frequency allocation unit in LTE systems. The calculation is based on:  
  
- `bw`: The total bandwidth available.  
- `pnomref`: The nominal reference power.  
  
The method considers the fixed frequency width of an RB (180 kHz) and adjusts the number of RBs to fit within the specified bandwidth, accounting for guard bands and standardized LTE bandwidth configurations.  
  
### 3. Maximum Received Power Calculation (`lpmax`)  
  
The `lpmax` method calculates the peak power that the receiver's antenna is capable of receiving. This calculation incorporates:  
  
- `ptxrb`: The transmit power per RB.  
- `gtx`: The gain of the transmitting antenna.  
- `grx`: The gain of the receiving antenna.  
- `pathloss`: The path loss as computed by the `pathloss` method.  
  
By adding the transmit power and antenna gains and then subtracting the path loss, the method estimates the power level that would be received at the antenna.  
  
## Conclusion  
  
The `RMaLOS` class provides essential tools for estimating and optimizing signal propagation in rural wireless networks. By considering key environmental and technical parameters, the class enables precise calculations of path loss, transmit power per RB, and received power at the antenna, which are vital for ensuring adequate network coverage and service quality.  
