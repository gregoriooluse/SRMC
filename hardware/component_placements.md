- 22 Ω resistor placed physically close to the LM5106 pin for noise suppression.
- Keep PWM traces short (< 15 cm / 6 inches) and run ground return nearby.

## Selected Components

**Power Stage Bill of Materials (per phase × 3)**

| Item                        | Part Number                    | Qty per Phase | Total Qty | Location / Notes                              |
|-----------------------------|--------------------------------|---------------|-----------|-----------------------------------------------|
| N-Channel MOSFET            | Infineon IPB180N10S4-03        | 2             | 6         | High-side & Low-side switches                 |
| Schottky Freewheel Diode    | Vishay VS-100BGQ100-N4         | 2             | 6         | Freewheeling paths (fast recovery)            |
| Gate Driver IC              | TI LM5106                      | 1             | 3         | Drives one full half-bridge                   |
| Series Resistor (PWM)       | 22 Ω, 1/8 W, 1%                | 2             | 6         | Between MCU GPIO and LM5106 HI/LI pins        |
| Current Sensor              | ACS773ECB-200B-PFF-T           | 1             | 3         | On phase output (measures ±200 A)             |

**Additional Notes:**
- All MOSFETs and diodes will be mounted on heatsinks.
- Bootstrap capacitor and bootstrap diode for each LM5106 will be added per datasheet (typical values: 1 µF bootstrap cap + 1N4148 or similar).
- Gate resistors (10–22 Ω) between LM5106 outputs and MOSFET gates are recommended.
- Current sensors are powered directly from the LaunchPad’s 3.3 V rail and connect directly to ADC inputs.
- The ACS773 is galvanically isolated, providing good safety and noise immunity.
