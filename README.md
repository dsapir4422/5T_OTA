# 5T_OTA
In this project we will show the design of a single ended Operational Transconductance Amplifier in a buffer configuration
we will use CMOS general pdk 90nm (gpdk90) technology by Cadence. 

**Specifications**
* $Gain = 35dB$
* $PM > 60 [deg]$
* $ICMR- = 1.1[V]$
* $ICMR+ = 1.6[V]$
* Settling time: $T_s < 500[ns]$
* Voltage accuracy: $V_{acc} = 500[uV]$
* Static offset < 8mV
* $I_{ref} = 10uA$
* $V_{AA} = 2[V]$
* $C_{L} = 100[pF]$

# Hand calculations & Design assumption
We will start with some basic hand calculations to determine - $I_{tail}$, and Vov for each transistor - 

$T_s = T_{slew} + T_{sm,sig}$ = $\frac{V_{slew}*C_L}{I_{tail}}$ + $\frac{C_L}{g_m}$ * $ln(\frac{(V_{swing}-V_{slew})}{V_{acc}})$

After plugging the numbers from spec (see Excel attached) we calculate $I_{tail} > 220[uA]$

**Calculating Vov** - 

$V_{ICMR-} = V_{gs1} + V_{ov5} = 1.1[V]$
$V_{ICMR+} = V_{AA} - V_{sg3} + V_{th1} = 1.6[V]$

from simulation of worst case corner (SS, 125) we saw that $V_{th} = 0.7[V]$. 

We will target for high $V_{ov}$ for the current mirrors M5,M3,M5 $\approx 0.2V$ and 0.1V for the gm stage (M1,M2)

**Other assumptions** - 

For low noise $gm_3 > gm_1$ $=>V_{ov1} > V_{ov3}$

$L = 2u$ for low mismatch and high gain

$g_{m1,2}$ will be high for low settling time and high gain

Open loop Gain: $A_v = g_{m2}*r_{o2}||r_{o4}$ (assuming M1=M2, M3=M4)

# Design & Simulations
Taken from Razavi's book - Design of analog CMOS integrated circuits - 

<img src="https://github.com/dsapir4422/5T_OTA/assets/87266625/dcd6fdf5-c6d9-4c4c-baa0-e622a7b912d2" align="middle" width="400" height="250"  alt="Image Alt Text" />

Where Iss (Itail) will be implemented with NMOS and a current mirror to provide reference current. 
*****************

We used multiplier and a restriction of w < 10u for better layout. 

Final design (SS,125 corner) - 
![image](https://github.com/dsapir4422/5T_OTA/assets/87266625/bd706f7f-8750-462d-b15e-d6b907f6cae7)

Simulation results over corners - 
![image](https://github.com/dsapir4422/5T_OTA/assets/87266625/9db7c461-2dd8-43d3-b2d5-f8a82b176954)

**Simulation analysis explained** - 
* Open loop Gain (Av_dB) and PM - we extract from STB simulation
* Settling time and Static offset - we extract from transient simulation and calculator using the following formula's -

**Settling time** -
![image](https://github.com/dsapir4422/5T_OTA/assets/87266625/eabc5f28-6e3f-47ba-abc7-e29ffbc1e3fd)

Ramp voltage starts from 10us, delta from settling voltage (point A) to 500uV (point B) is roughly at 10.5uA => $T_s = 500[ns]$

To calculate over corners we used Cadence calculator - 
![image](https://github.com/dsapir4422/5T_OTA/assets/87266625/0957061e-7735-47af-ab83-0c7e5cebfccf)

**Static offset** - 
![image](https://github.com/dsapir4422/5T_OTA/assets/87266625/b966c705-c4bf-4145-83b7-1bf9c8c45ccb)
The difference between output voltage and the input voltage from Ramp is the static offset

![image](https://github.com/dsapir4422/5T_OTA/assets/87266625/085b95ab-3a49-470a-bf5d-0582cc286dc9)



