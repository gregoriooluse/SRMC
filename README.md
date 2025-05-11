# SRMC
Switched Reluctance Motor Controller (SRMC)
The goal of this project is to provide an easy to use infrastructure for motor controllers based on the Switched Reluctance Motor technology. It will use an asymmetric half bridge with two power electronic devices per phase, a high side and low side device, with either integrated or separate as required or available by technology free-wheeling diodes.
The planned commutation strategies will be on SECs, Hysteresis Chop Control, Angle Control and Flux Virtualization Control for high speeds.
The development strategy is to start with an Arduino Shield, then to leverage existing knowledge from related projects (EECS476 PMSM Controller (trapezoidal, sinusoidal and FOC control algorithms based on a TMS320 devkit and the DRV-8301 chip) ) then to decide to either move to STM32 or stay with TMS320 based on available FPGA technology integration as this device will require FPGA to properly execute the higher rpm control strategies.
