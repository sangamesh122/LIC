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
  <img src="https://github.com/sangamesh122/LIC/blob/main/Screenshot%202026-02-22%20171731.png" width="650">
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

## COMPLETE DC ANALYSIS

<p align="center">
  <img src="https://github.com/sangamesh122/LIC/blob/main/Screenshot%202026-02-19%20154648.png" width="700">
</p>

<p align="center">
  <em>Figure 3: Complete DC Analysis Showing Circuit Along with Biasing Results</em>
</p>

This figure shows the circuit along with the DC operating point results obtained after simulation. The drain voltage being approximately equal to 0.9V confirms that the transistor is correctly biased and operating in the saturation region. This establishes the Q-point of the amplifier.
---

## DC OPERATING POINT (FROM LTSPICE)

From simulation:

- $V(vin) = 0.9V$
- $V(vout) = 0.90005V$

The output voltage being almost exactly 0.9V confirms that the drain node is properly centered. This means the transistor is biased correctly, and the Q-point lies safely in the saturation region.
---

## DC OPERATING POINT (NUMERICAL VALUES)

<p align="center">
  <img src="https://github.com/sangamesh122/LIC/blob/main/Screenshot%202026-02-22%20171740.png" width="600">
</p>

<p align="center">
  <em>Figure 2: LTSpice DC Operating Point Values Showing Node Voltages</em>
</p>

From the operating point window, it can be clearly observed that the output voltage is very close to 0.9V. This confirms that the drain node is properly centered at half the supply voltage, which ensures maximum symmetrical output swing and stable operation in saturation region.
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

## TRANSIENT ANALYSIS

<p align="center">
  <img src="https://github.com/sangamesh122/LIC/blob/main/Screenshot%202026-02-20%20205559.png" width="750">
</p>

<p align="center">
  <em>Figure 4: Transient Response Showing Amplified and Inverted Output Waveform</em>
</p>

The transient waveform clearly shows that the output signal is amplified compared to the input signal. It can also be observed that the output is 180 degrees out of phase with the input, which confirms the expected behavior of a Common Source amplifier.
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

# AC ANALYSIS (FREQUENCY RESPONSE)

To understand the frequency behaviour of the Common Source amplifier, AC analysis was carried out under two different conditions:

1. Without external load capacitor (only internal parasitic capacitance ≈ 50 fF)
2. With external load capacitor ($C_L = 10pF$)

This comparison helps in clearly understanding how capacitance at the output node affects bandwidth.

---

## AC RESPONSE WITHOUT LOAD CAPACITOR (Only 50 fF Parasitic)

<p align="center">
  <img src="https://github.com/sangamesh122/LIC/blob/main/Screenshot%202026-02-26%20002900.png" width="750">
</p>

<p align="center">
  <em>Figure: AC Response of CS Amplifier with Only Parasitic Capacitance (≈50 fF)</em>
</p>

In this case, the 10pF load capacitor was not connected. However, the intrinsic parasitic capacitance of the MOSFET (approximately 50 fF) was still present at the drain node.

From simulation, the 3dB frequency obtained was:

$$
f_{3dB} = 1.3051 \, GHz
$$

Since this is a single dominant pole system, the bandwidth is equal to the 3dB frequency:

$$
BW = 1.3051 \, GHz
$$

Because the capacitance at the output node is extremely small, the RC time constant is very small. As a result, the dominant pole occurs at a very high frequency, allowing the amplifier to maintain its gain up to the GHz range before roll-off begins.

---

## AC RESPONSE WITH LOAD CAPACITOR ($C_L = 10pF$)

<p align="center">
  <img src="https://github.com/sangamesh122/LIC/blob/main/Screenshot%202026-02-20%20205404.png" width="750">
</p>

<p align="center">
  <em>Figure: AC Response of CS Amplifier with 10pF Load Capacitor</em>
</p>

When a 10pF capacitor was connected at the output node, the total capacitance increased significantly.

From simulation:

$$
f_{3dB} = 7.328 \, MHz
$$

Thus,

$$
BW = 7.328 \, MHz
$$

The unity gain frequency observed from the plot was approximately:

$$
f_{UGB} \approx 23.29 \, MHz
$$

---

## Verification of Unity Gain Bandwidth

For a single-pole amplifier, the unity gain bandwidth is given by:

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
UGB \approx 24.37 \, MHz
$$

The calculated value (24.37 MHz) is very close to the simulated unity gain frequency (~23.29 MHz), confirming that the amplifier behaves approximately as a single dominant pole system.

---

## Explanation of Dominant Pole (From Circuit Perspective)

The dominant pole in this circuit is formed at the drain node due to the combination of:

- Drain resistance $R_D$
- Total capacitance at the output node

This forms an RC network, whose pole frequency is approximately:

$$
f_p = \frac{1}{2\pi R_D C_{total}}
$$

Where:

$$
C_{total} = C_{parasitic} + C_L
$$

At low frequencies, the capacitor behaves almost like an open circuit, so the gain remains constant (midband region).

At high frequencies, the capacitor reactance decreases and it provides a path to ground, which reduces the output signal amplitude. This causes the gain to roll off at −20 dB/decade.

Since this RC network allows low frequencies to pass and attenuates high frequencies, the output node behaves as a **low-pass filter**.

When only 50 fF is present, the pole is in the GHz range.  
When 10 pF is added, the capacitance increases drastically, shifting the pole to the MHz range and reducing the bandwidth significantly.

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
| 3dB Frequency (Parasitic Only) | 1.3051 GHz |
| 3dB Frequency (With 10pF Load) | 7.328 MHz |
| Unity Gain Frequency | ~23–24 MHz |

---

# INFERENCE

From this experiment, it is clearly observed that proper DC biasing ensures that the MOSFET operates in the saturation region, allowing linear amplification with symmetrical signal swing.

The transient analysis confirmed that the amplifier provides voltage gain along with a 180° phase shift, which is characteristic of a Common Source configuration. The close agreement between theoretical and simulated gain validates the design calculations.

The AC analysis demonstrated that the bandwidth of the amplifier is strongly dependent on the capacitance present at the output node. When only small parasitic capacitance (50 fF) is present, the bandwidth extends into the GHz range. However, when a 10pF load capacitor is added, it dominates the output capacitance and shifts the dominant pole to a much lower frequency, reducing the bandwidth to the MHz range.

Thus, the experiment clearly verifies how the RC network at the drain node determines the high-frequency response of the CS amplifier.

 of the Common Source amplifier using 180nm technology was successfully completed.
