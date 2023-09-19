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

# Hand calculations
We will start with some basic hand calculations to determine - $I_{tail}$, and Vov for each transistor - 

$T_s = T_{slew} + T_{sm,sig}$ = $\frac{V_{slew}*C_L}{I_{tail}}$ + $\frac{C_L}{g_m}$ * $ln(\frac{(V_{swing}-V_{slew})}{V_{acc}})$

After plugging the numbers from spec (see Excel attached) we calculate $I_{tail} > 220[uA]$

**Calculating Vov**

$V_{ICMR-} = V_{gs1} + V_{ov5} = 1.1[V]$
$V_{ICMR+} = V_{AA} - V_{sg3} + V_{th1} = 1.6[V]$

from simulation of worst case corner (SS, 125) we saw that $V_{th} = 0.7[V]$. 

We will target for high $V_{ov}$ for the current mirrors M5,M3,M5 $\approx 0.2V$ and 0.1V for the gm stage (M1,M2)

For low noise $gm_3 > gm_1$ $=>V_{ov1} > V_{ov3}$

$L = 2u$ for low mismatch.

# Design
Taken from Razavi's book - Design of analog CMOS integrated circuits - 

<img src="https://github.com/dsapir4422/5T_OTA/assets/87266625/dcd6fdf5-c6d9-4c4c-baa0-e622a7b912d2" align="left" width="400" height="250" />

