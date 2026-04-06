# SRMC Power Stage

**3-Phase Asymmetric Half-Bridge for 18/12 SRM**  
**DC Bus:** 48 V nominal (up to ~60 V)  
**Phase Current:** up to 100 A peak  
**Switching Frequency:** 20 kHz (PWM / chop mode)  
**Gate Driver:** Bootstrap topology using LM5106

## Overview
Each phase uses a classic asymmetric half-bridge:
- 2 × N-channel MOSFETs (High-side + Low-side)
- 2 × ultrafast Schottky freewheel diodes
- 1 × LM5106 gate driver IC
- 1 × ACS773 current sensor (on phase output)

## Component Placement Notes

### Per Phase (x3)
- **High-side MOSFET** → Connected between +48 V and phase output  
- **Low-side MOSFET** → Connected between phase output and GND  
- **High-side freewheel diode** → Cathode to +48 V, Anode to phase output  
- **Low-side freewheel diode** → Cathode to phase output, Anode to GND  
- **LM5106 Gate Driver** → Drives both MOSFETs in the phase  
- **Current Sensor (ACS773)** → Placed on the **phase output** (between half-bridge switching node and motor winding)

### PWM Signal Connection (MCU to Gate Driver)
