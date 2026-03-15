# Common Source Amplifier with Active Load and Current Source

## Introduction

The Common Source (CS) amplifier is one of the most fundamental amplifier configurations used in analog integrated circuits. It provides voltage amplification along with a 180° phase inversion between input and output signals.

In practical IC design, instead of using passive resistors as loads, active devices such as MOS transistors are used. A PMOS transistor can act as an **active load**, providing very high output resistance which increases the achievable gain of the amplifier.

Similarly, a MOS transistor can be used as a **current source** to bias the amplifier. Using a current source improves bias stability and ensures that the drain current remains almost constant.

In this experiment, a **Common Source amplifier with PMOS active load and NMOS current source** is designed and analyzed using **TSMC 180nm technology in LTSpice**. The circuit is studied through DC analysis, transient analysis, and AC analysis.

---

# Aim

To design and analyze a **Common Source amplifier with PMOS active load and NMOS current source** using **TSMC 180nm technology in LTSpice**, and study its DC operating point, transient response, and frequency response.

---

# Circuit Diagram

<p align="center">
<img src="WhatsApp Image 2026-03-11 at 7.51.23 PM.jpeg" width="600">
</p>

<p align="center">
Figure 1: Common Source Amplifier with Active Load and Current Source
</p>

The circuit consists of three MOS transistors:

- **M1 (NMOS)** – main amplifying transistor  
- **M2 (PMOS)** – active load transistor  
- **M3 (NMOS)** – current source transistor  

The PMOS transistor acts as the load of the amplifier, while the bottom NMOS transistor provides a constant bias current for proper operation.

---

# DC Analysis

DC analysis is carried out to determine the proper biasing conditions for all transistors so that they operate in the saturation region and provide maximum signal swing.

---

## Power Constraint

The power consumption of the circuit must satisfy

P ≤ 1 mW

The maximum allowable drain current is therefore

ID ≤ P / VDD

ID ≤ (1 × 10⁻³) / 1.8

ID ≤ 555.5 µA

To keep the circuit safely within the power limit, the operating current is chosen as

ID = 400 µA

---

## Overdrive Voltage Relations

For MOS transistors, the overdrive voltage is defined as

Vov = VGS − VT

For each transistor

NMOS (M1):

Vov₁ = VGS₁ − VTN

Current source NMOS (M3):

Vov₃ = VGS₃ − VTN

PMOS (M2):

Vov₂ = VSG₂ − |VTP|

For symmetry of operation, the overdrive voltage of the transistors is assumed to be equal.

---

## Saturation Conditions

To maintain saturation for all MOSFETs, the following conditions must be satisfied.

### For M3 (current source transistor)

VDS3 ≥ Vov

Since

VDS3 = Vx

Therefore

Vx ≥ Vov

Minimum value of node voltage

Vx(min) = Vov

---

### For M1 (amplifying transistor)

VDS1 ≥ Vov

VDS1 = Vout − Vx

Therefore

Vout − Vx ≥ Vov

Vout ≥ Vov + Vx

---

### For M2 (PMOS active load)

VSD2 ≥ Vov

VSD2 = VDD − Vout

Thus

VDD − Vout ≥ Vov

Vout ≤ VDD − Vov

---

## Output Voltage Range

From the above conditions

Minimum output voltage

Vout(min) = 2Vov

Maximum output voltage

Vout(max) = VDD − Vov

Thus the output range becomes

2Vov ≤ Vout ≤ VDD − Vov

---

## Output Swing

Maximum swing is

Vswing = VDD − 3Vov

To allow sufficient swing,

VDD − 3Vov ≥ 0

Therefore

Vov(max) = VDD / 3

Vov(max) = 1.8 / 3

Vov(max) = 0.6 V

Minimum overdrive voltage approaches zero, so the optimum value is taken as the midpoint

Vov(optimum) = 0.6 / 2

Vov = 0.3 V

---

## NMOS Gate Voltage

For NMOS transistor

VGS(min) = VTN

VTN = 0.366 V

Maximum gate voltage

VGS(max) = 0.366 + 0.6

VGS(max) = 0.966 V

Chosen value

VGS = 0.666 V

---

## PMOS Gate Voltage

For PMOS transistor

VSG = Vov + |VTP|

VSG = 0.3 + 0.39

VSG = 0.69 V

Thus

VB1 = VDD − VSG

VB1 = 1.8 − 0.69

VB1 = 1.11 V

---

## Bias Voltages

For M1

Vin = VGS + Vx

Vin = 0.666 + 0.3

Vin ≈ 0.966 V

For M3

VB2 = VGS = 0.666 V

For M2

VB1 = 1.11 V
## Transistor Width Calculation

The transistor width is calculated using the MOSFET current equation in saturation region

\[
I_D = \frac{1}{2}\mu C_{ox}\frac{W}{L}(V_{ov})^2
\]

Rearranging the equation,

\[
W = \frac{2 I_D L}{\mu C_{ox}(V_{ov})^2}
\]

## NMOS Width

Given:

\(I_D = 400\,\mu A\)  
\(L = 560\,nm\)  
\(V_{ov} = 0.3\,V\)  
\(\mu_n C_{ox} = 115.6 \times 10^{-6}\,A/V^2\)

\[
W_n =
\frac{2 \times (400 \times 10^{-6}) \times (560 \times 10^{-9})}
{(115.6 \times 10^{-6})(0.3)^2}
\]

\[
W_n \approx 43.1\,\mu m
\]

## PMOS Width

Using PMOS process parameter

\(k_p = 9.7361 \times 10^{-5}\,A/V^2\)

\[
W_p =
\frac{2 \times (400 \times 10^{-6}) \times (560 \times 10^{-9})}
{(9.7361 \times 10^{-5})(0.3)^2}
\]

\[
W_p \approx 51.1\,\mu m
\]

The theoretical widths obtained from the above calculations were then adjusted during simulation in order to obtain the correct DC operating point. The final transistor widths used in the LTSpice simulation are:

- **NMOS (M1, M3)** : \(W = 36.05\,\mu m\)  
- **PMOS (M2)** : \(W = 108.05\,\mu m\)
---

## Output Voltage

Using midpoint of the output range

Vout = (VDD + Vov) / 2

Vout = (1.8 + 0.3) / 2

Vout = 1.05 V

---

## Output Swing

Minimum output voltage

Vout(min) = 2Vov = 0.6 V

Maximum output voltage

Vout(max) = 1.8 − 0.3 = 1.5 V

Thus

Output swing ≈ 0.9 Vpp

---

# Transient Analysis

<p align="center">
<img src="WhatsApp Image 2026-03-11 at 7.54.13 PM.jpeg" width="700">
</p>

<p align="center">
Figure 2: Transient Response of the Amplifier
</p>

From the transient waveform:

Output voltage

Vout(max) = 1.080 V  
Vout(min) = 1.021 V  

Input voltage

Vin(max) = 975.56 mV  
Vin(min) = 956.42 mV  

Output peak-to-peak voltage

Vout(pp) = 1.080 − 1.021

Vout(pp) = 59 mV

Input peak-to-peak voltage

Vin(pp) = 975.56 − 956.42

Vin(pp) = 19.14 mV

Voltage gain

Av = Vout(pp) / Vin(pp)

Av = 59 / 19.14

Av ≈ 3.08 V/V

Gain in dB

Av(dB) = 20 log(3.08)

Av(dB) ≈ 9.77 dB

---

# AC Analysis

<p align="center">
<img src="WhatsApp Image 2026-03-11 at 7.55.17 PM.jpeg" width="700">
</p>

<p align="center">
Figure 3: Frequency Response of the Amplifier
</p>

From the AC analysis plot

Midband gain

Av ≈ 3.08 V/V  
Av(dB) ≈ 9.53 dB  

3 dB bandwidth

f3dB = 54.978 MHz

Unity gain bandwidth

UGB = 162.467 MHz

---

## Verification of Unity Gain Bandwidth

For a single-pole amplifier

UGB ≈ Av × f3dB

UGB ≈ 3.08 × 54.978 MHz

UGB ≈ 169.33 MHz

This value is close to the simulated unity gain bandwidth of

UGB ≈ 162.467 MHz

The small difference occurs due to non-ideal device effects and parasitic capacitances in the MOS transistors.

---

# Results

| Parameter | Value |
|----------|------|
| Supply Voltage | 1.8 V |
| Drain Current | 400 µA |
| Overdrive Voltage | 0.3 V |
| Output Bias Voltage | 1.05 V |
| Output Swing | 0.9 Vpp |
| Transient Gain | 3.08 V/V |
| Gain (dB) | 9.77 dB |
| 3 dB Bandwidth | 54.978 MHz |
| Unity Gain Bandwidth | 162.467 MHz |

---

# Inference

In this experiment, a Common Source amplifier with PMOS active load and NMOS current source was designed and analyzed using LTSpice. The DC analysis ensured that all transistors operate in saturation while providing sufficient output voltage swing.

By properly selecting the overdrive voltage and bias voltages, the output operating point was centered around 1.05 V, which allows symmetrical signal swing.

Transient analysis confirmed that the circuit provides voltage amplification with a gain of approximately 3 V/V. AC analysis showed that the amplifier maintains a constant gain in the midband region and begins to roll off after the 3 dB frequency due to the effect of parasitic capacitances.

The experiment demonstrates how active loads and current source biasing are used in integrated circuits to achieve stable biasing and improved amplifier performance.
