# SRMC Pin Assignments

**MCU:** TMS320F28069M LaunchPad  
**Project:** 3-Phase 18/12 Switched Reluctance Motor Controller  
**Switching Frequency:** 20 kHz  
**Date:** Draft 2 - April 2026

## Complete Pin Map

| Category                  | Signal                        | Pin / Resource       | Notes / Connection                                      |
|---------------------------|-------------------------------|----------------------|---------------------------------------------------------|
| **PWM Outputs**           | Phase A High-side PWM         | GPIO 0  (ePWM1A)     | → 22 Ω resistor → LM5106 Phase A HI                     |
| **PWM Outputs**           | Phase A Low-side PWM          | GPIO 1  (ePWM1B)     | → 22 Ω resistor → LM5106 Phase A LI                     |
| **PWM Outputs**           | Phase B High-side PWM         | GPIO 2  (ePWM2A)     | → 22 Ω resistor → LM5106 Phase B HI                     |
| **PWM Outputs**           | Phase B Low-side PWM          | GPIO 3  (ePWM2B)     | → 22 Ω resistor → LM5106 Phase B LI                     |
| **PWM Outputs**           | Phase C High-side PWM         | GPIO 4  (ePWM3A)     | → 22 Ω resistor → LM5106 Phase C HI                     |
| **PWM Outputs**           | Phase C Low-side PWM          | GPIO 5  (ePWM3B)     | → 22 Ω resistor → LM5106 Phase C LI                     |
| **Position Feedback**     | Hall Sensor 1                 | GPIO 6               | Digital input from Hall-effect transducer               |
| **Position Feedback**     | Hall Sensor 2                 | GPIO 7               | Digital input                                           |
| **Position Feedback**     | Hall Sensor 3                 | GPIO 8               | Digital input                                           |
| **Control Signals**       | Global Enable (12-36 V)       | GPIO 9               | Input — requires external level shifting / protection   |
| **Protection**            | Fault Input                   | GPIO 10              | From gate drivers or power stage                        |
| **ADC - Currents**        | Phase A Current               | ADCINA0              | From ACS773ECB-200B-PFF-T (3.3 V powered)               |
| **ADC - Currents**        | Phase B Current               | ADCINA2              | From ACS773ECB-200B-PFF-T                               |
| **ADC - Currents**        | Phase C Current               | ADCINA3              | From ACS773ECB-200B-PFF-T                               |
| **ADC - Voltage**         | DC Bus Voltage                | ADCINA4              | From resistor divider (scaled to 0–3.3 V)               |
| **ADC - Temperature**     | Board Temperature Sensor      | ADCINA5              | On-board NTC or external sensor                         |
| **Communication**         | CAN RX                        | GPIO 30 (CANRXA)     | To CAN transceiver                                      |
| **Communication**         | CAN TX                        | GPIO 31 (CANTXA)     | To CAN transceiver                                      |
| **Debug / Status**        | Status LED                    | GPIO 34              | Blue LED on LaunchPad (optional)                        |
| **Debug / Status**        | Fault LED                     | GPIO 39              | Red LED on LaunchPad (optional)                         |

## Notes
- PWM pins use ePWM1–3 with HRPWM support for clean 20 kHz chopping.
- **Current sensors**: ACS773ECB-200B-PFF-T powered directly from LaunchPad 3.3 V rail.
- Hall sensors on GPIO 6/7/8 can use interrupts for commutation.
- Enable pin (GPIO 9) needs external level shifting for 12–36 V input.
- ADC channels allow simultaneous sampling of all three phase currents.
- JTAG pins reserved for programming/debugging.
