# LIC LAB – COMMON SOURCE (CS) AMPLIFIER DESIGN

## EXPERIMENT – DESIGN AND ANALYSIS OF CS AMPLIFIER USING 180nm NMOS (TSMC)

---

# AIM

To design and analyze a Common Source (CS) amplifier using an NMOS transistor in **TSMC 180nm technology** using LTSpice, with:

- $V_{DD} = 1.8V$
- Power constraint ≤ 1 mW
- Load capacitor $C_L = 10pF$
- Channel length $L_n = 560nm$

And to determine:

- DC Operating Point (Q-Point)
- Voltage Gain (Transient and Theoretical)
- Gain in dB
- Bandwidth
- 3dB Frequency

---

# INTRODUCTION TO COMMON SOURCE (CS) AMPLIFIER

The Common Source amplifier is one of the most basic and widely used MOSFET amplifier configurations.

In this configuration:

- Input is applied to the **gate**
- Output is taken from the **drain**
- Source is common (connected to ground)

The CS amplifier provides:

- High voltage gain
- 180° phase shift
- Moderate input impedance
- Moderate output impedance

When the MOSFET operates in **saturation region**, it behaves like a controlled current source and provides amplification.

---

# GIVEN PARAMETERS

## Technology Parameters (TSMC 180nm)

- Channel Length, $L_n = 560nm$
- $V_{DD} = 1.8V$
- Power limit ≤ 1 mW
- Threshold Voltage, $V_T ≈ 0.366V$
- Electron mobility, $\mu_n = 273.81 \times 10^{-4} \, m^2/Vs$
- Oxide thickness, $T_{ox} = 4.1nm$
- Permittivity:
  $$
  C_{ox} = \frac{\varepsilon_0 \varepsilon_r}{T_{ox}}
  $$
  $$
  C_{ox} = 8.6 \times 10^{-3} F/m^2
  $$

---

# WHAT IS TO BE FOUND

1. Proper DC operating point
2. Drain resistor value $R_D$
3. Width of transistor $W$
4. Voltage gain (Theoretical and Simulation)
5. Gain in dB
6. Bandwidth
7. 3dB frequency

---

# DC ANALYSIS (Q-POINT DESIGN)

## Step 1: Power Constraint

Given:

$$
P = V_{DD} I_D
$$

Since power ≤ 1 mW,

$$
I_D \le \frac{1 \times 10^{-3}}{1.8}
$$

$$
I_D \le 555.5\mu A
$$

We assume:

$$
I_D = 400\mu A
$$

---

## Step 2: Choose Symmetrical Biasing

For maximum output swing:

$$
V_{DS} = \frac{V_{DD}}{2} = 0.9V
$$

---

## Step 3: Calculate Drain Resistance

$$
R_D = \frac{V_{DD} - V_{DS}}{I_D}
$$

$$
R_D = \frac{1.8 - 0.9}{400 \times 10^{-6}}
$$

$$
R_D = 2250 \Omega
$$

---

## Step 4: Choose Gate Voltage

To operate in saturation:

$$
V_{DS} \ge V_{GS} - V_T
$$

We selected:

$$
V_{GS} = 0.9V
$$

---

## Step 5: Calculate Transistor Width

Drain current equation in saturation:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_T)^2
$$

Rearranging for W:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{GS} - V_T)^2}
$$

Initially calculated:

$$
W = 6.67 \mu m
$$

But from simulation, actual current was slightly less than required.

So width was increased to:

$$
W = 9.08 \mu m
$$

This ensured correct $I_D$ and proper operating point.

---

## DC OPERATING POINT (From Simulation)

From LTSpice:

- $V(n001) = 1.8V$
- $V(vin) = 0.9V$
- $V(vout) = 0.90005V$

This confirms:

- MOSFET is in saturation
- Proper biasing is achieved
- Q-point is correctly centered

---

# TRANSIENT ANALYSIS

## Input Signal

Sine wave:

- Frequency = 1 kHz
- Amplitude = 10 mV
- DC Offset = 0.9 V

---

## From Simulation

Measured:

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
A_v = \frac{63.997}{19.237}
$$

$$
A_v = 3.326
$$

In dB:

$$
A_v(dB) = 20\log_{10}(3.326)
$$

$$
A_v = 10.438 dB
$$

Waveform clearly shows:

- Output is inverted
- Amplified
- Proper linear operation

---

# THEORETICAL GAIN

Small signal gain:

$$
A_v = -g_m R_D
$$

Where:

$$
g_m = \frac{2I_D}{V_{GS} - V_T}
$$

$$
g_m = \frac{2 \times 400\mu}{0.534}
$$

$$
g_m = 1.498 \times 10^{-3}
$$

Thus:

$$
A_v = 1.498 \times 10^{-3} \times 2250
$$

$$
A_v = 3.37
$$

In dB:

$$
A_v = 10.55 dB
$$

---

## Why Theoretical and Simulation Differ Slightly?

The difference occurs because:

1. Channel length modulation is ignored in theory
2. Parasitic capacitances are ignored
3. Mobility degradation effects not included
4. LTSpice uses complete transistor model

Hence small deviation (3.37 vs 3.326) is expected.

---

# AC ANALYSIS

## Without Capacitor

3dB frequency:

$$
f_{3dB} = 1.2966 GHz
$$

Bandwidth:

$$
BW = 1.2966 GHz
$$

---

## With Load Capacitor $C_L = 10pF$

From simulation:

- 3dB frequency = 7.328 MHz
- 0dB frequency = 23.29 MHz

This reduction occurs because:

$$
f = \frac{1}{2\pi R_D C_L}
$$

Adding capacitor introduces dominant pole and reduces bandwidth.

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
| 3dB Frequency (with CL) | 7.328 MHz |

---

# INFERENCE

1. Proper DC biasing ensures linear operation.
2. Gain from simulation matches closely with theoretical calculation.
3. Output waveform shows correct 180° phase inversion.
4. Addition of load capacitor reduces bandwidth significantly.
5. CS amplifier provides moderate gain and is suitable for voltage amplification applications.

The experiment successfully demonstrates design and analysis of a CS amplifier in 180nm technology.

---
