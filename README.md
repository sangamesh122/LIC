# LIC LAB – COMMON SOURCE (CS) AMPLIFIER DESIGN

## EXPERIMENT – DESIGN AND ANALYSIS OF CS AMPLIFIER USING 180nm NMOS (TSMC)

---

# AIM

To design a Common Source (CS) amplifier using an NMOS transistor in 180nm TSMC technology in LTSpice with a supply voltage of 1.8V and power constraint less than or equal to 1mW, and to analyze its DC operating point, transient response, voltage gain, bandwidth, and unity gain frequency.

---

# INTRODUCTION TO COMMON SOURCE AMPLIFIER

The Common Source amplifier is one of the most fundamental and widely used MOSFET amplifier configurations in analog circuit design. In this configuration, the source terminal is connected to ground, the input signal is applied at the gate, and the output is taken from the drain terminal.

The reason this configuration is so popular is because it provides a reasonably high voltage gain along with a 180-degree phase shift between input and output. When the MOSFET operates in the saturation region, it behaves like a voltage-controlled current source. A small variation in gate voltage produces a change in drain current, and this change across the drain resistor gets converted into an amplified voltage at the output node.

For proper amplification, it is very important that the transistor is biased correctly so that it remains in the saturation region for the entire input signal swing.

---

# GIVEN PARAMETERS

- Technology: TSMC 180nm
- Supply voltage, $V_{DD} = 1.8V$
- Power constraint ≤ 1mW
- Channel length, $L_n = 560nm$
- Threshold voltage, $V_T ≈ 0.366V$
- Electron mobility, $\mu_n = 273.81 \times 10^{-4} \, m^2/Vs$
- Load capacitor, $C_L = 10pF$

---

# OBJECTIVES

In this experiment, the following parameters are to be determined:

1. Proper DC operating point (Q-point)
2. Drain resistor value $R_D$
3. Transistor width $W$
4. Voltage gain (theoretical and simulated)
5. Gain in dB
6. 3dB frequency
7. Bandwidth
8. Unity Gain Bandwidth

---
---

## CIRCUIT DIAGRAM

<p align="center">
  <img src="(Screenshot%202026-02-22%20171731%20-%20Copy.png)" width="650">
</p>

<p align="center">
  <em>Figure 1: Common Source Amplifier Circuit Designed in LTSpice with VDD = 1.8V and RD = 2250Ω</em>
</p>

The above figure shows the complete circuit used for the design. The NMOS transistor is biased using a DC gate voltage of 0.9V, and a small AC signal is superimposed over it. The drain resistor converts the small variations in drain current into amplified voltage variations at the output node.
# DC ANALYSIS – DESIGNING THE Q POINT

## Step 1: Applying Power Constraint

The total power consumed by the circuit is given by:

$$
P = V_{DD} I_D
$$

Since the maximum allowed power is 1mW,

$$
I_D \le \frac{1 \times 10^{-3}}{1.8}
$$

$$
I_D \le 555.5\mu A
$$

To stay safely within this limit and also maintain reasonable gain, I assumed:

$$
I_D = 400\mu A
$$

---

## Step 2: Choosing a Proper Operating Voltage

it is always a good design practice to bias the drain voltage approximately at half of the supply voltage.

$$
V_{DS} = \frac{V_{DD}}{2} = 0.9V
$$

---

## Step 3: Calculating Drain Resistance

Using:

$$
R_D = \frac{V_{DD} - V_{DS}}{I_D}
$$

$$
R_D = \frac{1.8 - 0.9}{400 \times 10^{-6}}
$$

$$
R_D = 2250\Omega
$$

So the drain resistor was fixed as 2.25kΩ.

---

## Step 4: Ensuring Saturation Condition

For an NMOS transistor to operate in saturation:

$$
V_{DS} \ge V_{GS} - V_T
$$

I selected:

$$
V_{GS} = 0.9V
$$

Since:

$$
V_{GS} - V_T = 0.9 - 0.366 = 0.534V
$$

And because:

$$
V_{DS} = 0.9V > 0.534V
$$

the transistor clearly satisfies the saturation condition. This confirms that the device is operating in the correct region required for amplification.

---

## Step 5: Calculating Transistor Width

The drain current in saturation is given by:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_T)^2
$$

Rearranging for width:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{GS} - V_T)^2}
$$

Initially, the calculated width came out to be approximately:

$$
W = 6.67\mu m
$$

However, after running the simulation, the drain current was slightly lower than the intended 400µA. This happens because practical transistor models include second-order effects that slightly alter the expected current.

To correct this and achieve the desired operating current, I increased the width to:

$$
W = 9.08\mu m
$$

After this adjustment, the operating point matched the design target.

---

## DC OPERATING POINT (FROM LTSPICE)

From simulation:

- $V(vin) = 0.9V$
- $V(vout) = 0.90005V$

The output voltage being almost exactly 0.9V confirms that the drain node is properly centered. This means the transistor is biased correctly, and the Q-point lies safely in the saturation region.

---

# TRANSIENT ANALYSIS

## Input Signal

- Type: Sine wave  
- Frequency = 1kHz  
- Amplitude = 10mV  
- DC Offset = 0.9V  

The small amplitude ensures that:

$$
v_{gs} \ll (V_{GS} - V_T)
$$

Since the overdrive voltage is 0.534V and the input amplitude is only 10mV, the small-signal model assumption of amplitude is valid for the linear amplification which is much lesser than the overdrive voltage.

---

## Simulation Results

Measured values:

$$
V_{in(pp)} = 19.237mV
$$

$$
V_{out(pp)} = 63.997mV
$$

---

## Voltage Gain

$$
A_v = \frac{V_{out(pp)}}{V_{in(pp)}}
$$

$$
A_v = 3.326
$$

In dB:

$$
A_v(dB) = 20\log_{10}(3.326)
$$

$$
A_v = 10.438dB
$$

The waveform clearly shows that the output is inverted with respect to the input, which confirms the 180-degree phase shift characteristic of a CS amplifier. Also, the output amplitude is more than three times the input amplitude, verifying amplification.

---

# THEORETICAL GAIN

For a CS amplifier:

$$
A_v = -g_m R_D
$$

Where:

$$
g_m = \frac{2I_D}{V_{GS} - V_T}
$$

$$
g_m = 1.498 \times 10^{-3}
$$

Thus,

$$
A_v = 3.37
$$

In dB:

$$
A_v = 10.55dB
$$

---

## Reason for Slight Difference Between Theory and Simulation

The theoretical calculation assumes an ideal MOSFET and ignores practical second-order effects. In reality:

- Channel length modulation is present.
- Parasitic capacitances exist in the device structure.
- The SPICE model includes more accurate physical parameters.

Because of these factors, the simulated gain (3.326) is slightly lower than the theoretical value (3.37). This small variation is expected in practical circuit analysis.

---

# AC ANALYSIS

## 3dB Frequency (With Load Capacitor)

From simulation:

$$
f_{3dB} = 7.328 \, MHz
$$

---

## Unity Gain Bandwidth (UGB)

$$
UGB = A_{midband} \times f_{3dB}
$$

Using:

$$
A_{midband} = 3.326
$$

$$
f_{3dB} = 7.328 \, MHz
$$

$$
UGB = 3.326 \times 7.328
$$

$$
UGB ≈ 24.37 \, MHz
$$

From simulation, the frequency at which gain becomes 0dB is approximately:

$$
23.29 \, MHz
$$

This value is very close to the calculated unity gain bandwidth, therefore the relationship is verified:

$$
UGB = A_v \times f_{3dB}
$$

The small deviation again arises due to parasitic capacitance effects.

---

# RESULTS

| Parameter | Value |
|-----------|--------|
| $R_D$ | 2250 Ω |
| $W$ | 9.08 µm |
| $I_D$ | 400 µA |
| Gain (Transient) | 3.326 |
| Gain (Theoretical) | 3.37 |
| Gain (dB) | ~10.4 dB |
| 3dB Frequency | 7.328 MHz |
| Unity Gain Frequency | ~23–24 MHz |

---

# INFERENCE

From this experiment, it is clear that proper DC biasing is extremely important for linear amplification. By carefully selecting the drain current and bias voltages, the transistor was successfully maintained in saturation throughout operation.

The transient analysis confirmed that the amplifier provides voltage gain along with 180-degree phase inversion. The theoretical and simulated gains are very close, which tells that the design was properly done.

The AC analysis demonstrated that adding a load capacitor introduces pole and higher frequencies are attenueated, thereby reducing bandwidth. The unity gain bandwidth relationship was verified successfully from simulation results.

Overall, the design and analysis of the Common Source amplifier using 180nm technology was successfully completed.
