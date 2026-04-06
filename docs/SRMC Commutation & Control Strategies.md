SRMC Commutation & Control Strategies

Table of Contents

[Commutation Techniques](#commutation-techniques)

[Sensor Excited Commutation (on SECs)](#sensor-excited-commutation-on-secs)

[Chop Control](#chop-control)

[Angle Control](#angle-control)

[Flux Control](#flux-control)

[What data is required to operate?](#what-data-is-required-to-operate)

[Rotor position detection](#rotor-position-detection)

[Rotor Position Transducer](#rotor-position-transducer)

[Quadrature Encoder](#quadrature-encoder)

[Topics to cover](#topics-to-cover)

## Commutation Techniques

### Sensor Excited Commutation (on SECs)

Slightly tongue and cheek, in an effort to separate the strategy from the common phase off hall effect devices (off HEDs) this is a strategy that is based on ultra low RPM ranges (typically below 500rpm) and will command the power electronic device switching based on rotor position transducers and will always be full conduction (180°) the limitation is the amount of time it takes for the current to build up in the coil and is therefore the limiting factor for this commutation strategy especially at middle to higher speeds.

### Chop Control

We know for a fact that at low speeds if and where chop control method dominates that the switching frequency of the power electronic device in our case most likely IGBT will be highest when there a high number of chop events which depends on the hysteresis level (10% vs 1% or 50% of the current chop level).

The slower the motor is spinning the more opportunity for the phase winding current to reach the chop level and the further need for either soft ( one switch off, one diode conducting) or hard chopping (two switches off, two diodes conducting, current flowing back to the source DC Bus).

There is another topic which I don't currently understand which is the inductive load vs the IGBT performance and the limitation of the Gate Driver Circuit which is said to contain the switching losses (?) how do you measure or confirm that? what is the inductive load level measured by (Phase inductance, winding inductance?)

why does the inductance of the circuit for the IGBT matter? how does it affect the turn on turn off levels what is the difference between a low inductive and high inductive load profile's performance. what are the metrics for measuring / evaluating this?

So the chopping control method would have or could have potentially one of the highest switching frequencies across all control modes depending on the maximum speed of the motor and type of control used at top speed. In either case the chopping frequency would depend on circuit inductance at turn on, motor rpm, number of chopping events, chopping methodology used ( soft vs hard, alternating soft chopping switches between the two on a six switch assymetric half bridge controller assumed) if the alternating switch soft chopping method is used you can assume that the switching frequency would be half the calculated frequency of the electrical cycle based on number of chops and rpm.

### Angle Control

For angle control which dominates the mid-range speeds, the switching frequency will eventually line up with the electrical cycle and can be calculated as such. this can be seen visually when observing a regular Angle control operating point on an oscilloscope and (\* normal meaning no chop events or Free Wheeling events) you can see that when the switch turns on the current takes the full electrical cycle to reach it's final value if it even does actually (in most cases does not reach the established chop level which in this scenario should only really be used for thermal or device protection against overcurrent events) in which case you will see a single chop event towards the end of the current waveform and a gradual decline / degradation towards zero in which case there is essentially an on, charge up to value, then off event during a single electrical cycle. for full conduction and possibly less for under or over conduction (full conduction is 180° which is considered the movement of the rotor from the fully unaligned position to the fully aligned position, under conduction is any angle control operating point 180°). this is why in a sense the switching frequency of the igbt (or power electronic device) is in a sense algined with the electrical cycle during angle control at midrange speeds.

### Flux Control

During Flux control the switching frequency is incfreased (needs verification) due to the fact that the current level (desired or targeted) takes multiple electrical cycles to reach its final value since the back EMF is so high during high speeds and requires additional current or time to increase to it's final value since in a sense the current never fully decays to zero Amps. it is something I do not currently understand, why does the switching frequency increase when observably the curernt waveform looks almost identical with the angle control waveforms with the exception of the higher rpms and higher back emf and the never decaying to zero events. what is it or how do you calculate the switching frequency of the igbt while at higher rpms.

**Note:** One thing of note that was not mentioned above is the Motor geometry the number of stator and rotor poles or the ratio to number of phases, A combination of the two which determines the number of switching events required for a single motor rotation. which would increase substantially at higher pole ratios to lower number of phases or even same number of phases and only increased pole numbers. (36/24 3phase vs 12/8 3phase vs 6/4 3phase)

### What data is required to operate?

Motor Current, High side and low side current for each phase.

Rotor Position, Direction, Speed

Motor Temperature,

Motor Inductance, Minimum inductance

Power Module Temperature

Total phase current which should be the amount of current presently in the motor a sum of the total currents on the phase winding current sensors coming back into the controller or going out to the motor (I dont know) I will have to try both and see which is more effective.

Average current in the controller, this was used for paralleling controllers multiple converters for a single motor you want to know what the average current is across all controllers so you take an average across each controller which requires a locally interconnected circuit across controllers (common to each control card) to calculate the actual averag\`e current.

### Rotor position detection

You need to create a reference for the pole passing of the rotor to the stator. There needs to be an exact position of the rotor with respect to the stator pole. you need to know the fully unaligned position of the rotor for each phase's pole pass event. you need to create a angle measurement system for that series of events. Fully unaligned (pre-pole pass), fully aligned, fully unaligned (post-pole pass).

we can call this the electrical angle position, the electrical reference angle. how many degrees in a unaligned, aligned, unaligned sequence (poll pass event) is arbitrary. I am used to 360°. so we can go with that.

0° = fully unaligned.

180 = fully aligned

360 = fully unaligned again.

In order to do this my understanding as of now is that I need to create a replica wheel component for a rotor position transducer I need to replicate the rotor teeth (poles) with a wheel that can be detected by hall effect sensors.

### Rotor Position Transducer

Needs to have a steel ring with teeth that represent the teeth on the rotor so there may need to be a few different designs based on the motor design geometry. if there are 6, 8, 10 or 12 rotor poles there needs to be 6, 8, 10 or 12 rotor position ring teeth.

That is how I understand the device operation as of now.

That still doesn't tell me how far apart the hall effect sensors need to be positioned for each phase how far apart do they need to be so that they represent a true rise and falling edge of the rotor pole position. There needs to be some interpretation of the actual rotor position vs ring teeth and hall effect edge detection based on timing and a waveform. I need to think about this more so that I can represent an accurate picture of the device.

### Quadrature Encoder

you can use a quadrature encoder to detect and establish rotor position with respect to a pole passing event, however I do not really understand how that is done currently and also how the device will be mechanically aligned so there needs to be some investigation of how this works (as seen below).

Quadrature encoder works by producing a set of square waves it has four states, thus the quadrature.

A Signal Rising B signal Off

A Signal Falling B signal On

B Signal Rising A signal Off

B Signal Falling A Signal On

Another way to look at the above statement

States

A, B

L, L

H, L

L, H

H, H

you could align the phase A alignment with the rising of Signal A Bsignal Off.

then what would you do to get the following three phases lined up?

### Topics to cover

-   How does an SRM operate?
-   How does a Switched Reluctance Motor Get Controlled?
-   What are some popular SRM control algorithms?
-   What does a SRM Motor Control Circuit Look like?
-   What type of control circuit will be used?
-   Commutation Techniques Planned Based on the below subsection descriptions
-   Chop Control (Hysteresis Current Controller)
-   Flux Control (Constant Current Region, Saturation Protection)
-   Angle Control
-   Controller Operation Modes Planned
-   Speed Control
-   Torque Control
-   Direct Control
-   Current Control Techniques
-   Does speed affect which control method is used?
-   How does the control mode / type / algorithm affect the hardware?
