# CS Amplifier with Active Load and Diode Connected MOSFET

---

# Aim

To design and analyze a **Common Source amplifier with active load and diode connected MOSFET** using **TSMC 180nm technology in LTSpice**, and to study its DC biasing, transient response, and AC frequency characteristics.

---

# Introduction

The Common Source (CS) amplifier is one of the most widely used amplifier configurations in analog integrated circuit design. It provides significant voltage gain along with a phase inversion between the input and output signals.

In integrated circuits, passive resistors are often replaced by MOS transistors to save chip area and improve performance. A **PMOS transistor acting as an active load** provides high output resistance, which helps increase the gain of the amplifier.

In this circuit, a **diode connected MOSFET** is used to establish proper biasing conditions. This configuration helps maintain stable operating current and ensures that the transistors operate in the saturation region.

The amplifier is designed under a power constraint and analyzed using **DC analysis, transient analysis, and AC analysis**.

---

# Circuit Diagram

<p align="center">
<img src="Screenshot 2026-03-15 195248.png" width="600">
</p>

<p align="center">
Figure 1: CS Amplifier with Active Load and Diode Connected MOSFET
</p>

---

# DC Biasing Calculations

## Power Constraint

The maximum power consumption is limited to

P ≤ 1 mW

Maximum allowable drain current

ID ≤ P / VDD

ID ≤ (1 × 10⁻³) / 1.8

ID ≤ 555.55 µA

To ensure safe operation within the power limit, the operating current is chosen as

ID = 400 µA

---

# Overdrive Voltage Relations

For MOS transistors operating in saturation,

Vov = VGS − VT

For the three transistors:

NMOS (M1):

Vov1 = VGS1 − VTN

NMOS (M3):

Vov3 = VGS3 − VTN

PMOS (M2):

Vov2 = VSG2 − |VTP|

To maintain symmetry of operation, the overdrive voltages of the transistors are considered equal.

---

# Saturation Conditions

### For M3 MOSFET

VDS3 ≥ Vov

Minimum condition

VDS3(min) = Vov

Thus

Vx(min) = Vov

---

### For M1 MOSFET

VDS1 ≥ Vov

VDS1 = Vout − VDS3

Thus

Vout ≥ Vov + VDS3

Vout ≥ Vov + Vx

---

### For M2 MOSFET

VSD2 ≥ Vov

VSD2 = VDD − Vout

Thus

VDD − Vout ≥ Vov

Vout ≤ VDD − Vov

---

# Output Voltage Range

Minimum output voltage

Vout(min) = 2Vov

Maximum output voltage

Vout(max) = VDD − Vov

Thus the output range becomes

2Vov ≤ Vout ≤ VDD − Vov

---

# Maximum Output Swing

Output swing

Vswing = VDD − 3Vov

For maximum swing

VDD − 3Vov ≥ 0

Thus

Vov(max) = VDD / 3

Vov(max) = 1.8 / 3

Vov(max) = 0.6 V

Minimum overdrive voltage approaches zero.

Therefore the optimum overdrive voltage is taken as the midpoint:

Vov = 0.6 / 2

Vov = 0.3 V

---

# Gate Voltage Calculations

## For NMOS

VGS(min) = VTN = 0.366 V

VGS(max) = 0.366 + 0.6

VGS(max) = 0.966 V

Chosen value

VGS = 0.666 V

---

## For PMOS

VSG = Vov + |VTP|

VSG = 0.3 + 0.39

VSG = 0.69 V

Thus

VB1 = VDD − VSG

VB1 = 1.8 − 0.69

VB1 = 1.11 V

---

# Input Voltage

For transistor M1

Vin = VGS + Vx

Vin = 0.666 + 0.3

Vin ≈ 0.966 V

---

# Output Voltage

Optimum output voltage is chosen as

Vout = (VDD + Vov) / 2

Vout = (1.8 + 0.3) / 2

Vout = 1.05 V

---

# Output Voltage Limits

Minimum output voltage

Vout(min) = 2Vov = 0.6 V

Maximum output voltage

Vout(max) = VDD − Vov

Vout(max) = 1.8 − 0.3

Vout(max) = 1.5 V

Thus

Output swing = 0.9 Vpp

---

# Transistor Width Calculation

The width of MOS transistors is calculated using the saturation current equation

ID = (1/2) μCox (W/L) (Vov²)

Rearranging the equation

W = (2 ID L) / ( μCox Vov² )

Using

ID = 400 µA  
L = 560 nm  
Vov = 0.3 V  

Substituting these values gives the theoretical transistor widths for NMOS and PMOS.

However, when these theoretical values were used in simulation, the correct DC operating point was not obtained. Therefore, the transistor widths were adjusted in the simulator to achieve proper biasing conditions.

Final transistor widths used in simulation:

NMOS width = **430.2 µm**

PMOS width = **108.590 µm**

---

# Transient Analysis

<p align="center">
<img src="Screenshot 2026-03-15 194736.png" width="700">
</p>

<p align="center">
Figure 2: Transient Response of the Amplifier
</p>

From the simulation waveform:

Output voltage

Vout(max) = 1522.29 mV  
Vout(min) = 592.70 mV  

Input voltage

Vin(max) = 975.99 mV  
Vin(min) = 956.02 mV  

Output peak-to-peak voltage

Vout(pp) = 1522.29 − 592.70

Vout(pp) = 929.59 mV

Input peak-to-peak voltage

Vin(pp) = 975.99 − 956.02

Vin(pp) = 19.97 mV

Voltage gain

Av = Vout(pp) / Vin(pp)

Av = 929.59 / 19.97

Av ≈ 46.54 V/V

Gain in dB

Av(dB) = 20 log(46.54)

Av(dB) ≈ 33.56 dB

---

# AC Analysis

<p align="center">
<img src="Screenshot 2026-03-15 195203.png" width="700">
</p>

<p align="center">
Figure 3: Frequency Response of the Amplifier
</p>

From the AC analysis plot

Midband gain

Av = 35.69 dB

Av ≈ 60.88 V/V

3 dB bandwidth

f3dB = 1.00 MHz

Unity gain bandwidth

UGB = 61.17 MHz

---

# Verification of Unity Gain Bandwidth

UGB = Midband Gain × 3 dB Frequency

UGB = 60.88 × 1.00 MHz

UGB ≈ 60.88 MHz

This value closely matches the simulated unity gain bandwidth.

---

# Results

| Parameter | Value |
|-----------|------|
| Supply Voltage | 1.8 V |
| Drain Current | 400 µA |
| Overdrive Voltage | 0.3 V |
| Output Bias Voltage | 1.05 V |
| Output Swing | 0.9 Vpp |
| Voltage Gain | 46.54 V/V |
| Gain (dB) | 33.56 dB |
| 3 dB Bandwidth | 1 MHz |
| Unity Gain Bandwidth | 61.17 MHz |

---

# Inference

In this experiment, a Common Source amplifier with active load and diode connected MOSFET was successfully designed and analyzed using LTSpice. The DC analysis ensured that all MOS transistors operate in the saturation region while satisfying the given power constraint.

By selecting an optimum overdrive voltage of 0.3 V, the output bias voltage was centered around 1.05 V, allowing symmetrical output voltage swing. The transient analysis confirmed that the amplifier provides significant voltage amplification, with a gain of approximately 46.54 V/V.

The AC analysis showed that the amplifier maintains constant gain in the midband region and begins to decrease after the 3 dB frequency due to parasitic capacitances present in the MOS devices.

This experiment demonstrates the importance of proper biasing and transistor sizing in achieving the desired gain and bandwidth in MOSFET amplifiers.
