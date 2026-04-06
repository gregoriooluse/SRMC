# SRMC - Switched Reluctance Motor Controller (SRMC)
The goal of this project is to provide an easy to use infrastructure for motor controllers based on the Switched Reluctance Motor technology. It will use an asymmetric half bridge with two power electronic devices per phase, a high side and low side device, with either integrated or separate as required or available by technology free-wheeling diodes.
The planned commutation strategies will be on SECs, Hysteresis Chop Control, Angle Control and Flux Virtualization Control for high speeds.
The development strategy is to start with an Arduino Shield, then to leverage existing knowledge from related projects (EECS476 PMSM Controller (trapezoidal, sinusoidal and FOC control algorithms based on a TMS320 devkit and the DRV-8301 chip) ) then to decide to either move to STM32 or stay with TMS320 based on available FPGA technology integration as this device will require FPGA to properly execute the higher rpm control strategies.

The project will start with the following for now...
-An open-source 3-phase Switched Reluctance Motor (SRM) controller designed for an **18/12 pole** motor, targeting up to **12,000 rpm**.  
Built around the **TMS320F28069M** LaunchPad using **C2000Ware**.

### Project Goals
- Clean implementation of SRM control laws (commutation, current chopping, angle advance)
- Full asymmetric half-bridge power stage (48 V, up to 100 A per phase)
- CAN communication for commands and status
- Option for Diagnostics over IP (future)
- Well-documented hardware and software for learning and extension

### Hardware Overview
- **MCU**: TMS320F28069M LaunchPad
- **Power Stage**: 3× Asymmetric half-bridge using discrete MOSFETs
- **Position Feedback**: Hall-effect rotor position transducer (3 sensors)
- **Sensing**: Phase currents, DC bus voltage, board temperature
- **Switching Frequency**: 20 kHz (PWM chop mode at low/medium speeds)
- **Gate Drivers**: 3× TI LM5106 (bootstrap)

### Repository Structure
SRMC/
├── README.md
├── hardware/
│   ├── power_stage.md          ← Power stage description and circuit notes
│   ├── pin_assignments.md      ← Complete GPIO + ADC pin map
│   ├── BOM.md                  ← Bill of Materials
│   └── schematics/             ← (KiCad files will go here later)
├── software/
│   └── c2000/                  ← CCS project and source code (coming soon)
├── docs/
│   └── control_laws.md         ← SRM theory and control strategy
└── .gitignore


### Hardware Documentation
- **[Power Stage](hardware/power_stage.md)** — MOSFETs, diodes, LM5106 gate drivers, and connection notes
- **[Pin Assignments](hardware/pin_assignments.md)** — Full GPIO and ADC mapping for the F28069M
- **[Bill of Materials](hardware/BOM.md)** — Current parts list

### Next Steps
- Create initial C2000Ware project in Code Composer Studio
- Configure peripherals using SysConfig (ePWM, ADC, GPIO, CAN)
- Implement basic commutation and current control
- Add Hall sensor decoding and enable/fault handling

### Getting Started
1. Clone the repository
2. Review the hardware documentation
3. Install latest **C2000Ware** and Code Composer Studio
4. Follow the software setup guide (coming soon)

---

**Contributions and questions are welcome!**
