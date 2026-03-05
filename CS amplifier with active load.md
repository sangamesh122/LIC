# DESIGN AND ANALYSIS OF COMMON SOURCE AMPLIFIER WITH ACTIVE LOAD

---

# AIM

To design and analyze a Common Source (CS) amplifier using NMOS and PMOS transistors in 180nm technology with a supply voltage of 1.8V while satisfying a power constraint of less than 1mW. The DC operating point is determined first, followed by transient and AC simulations in LTSpice.

---

# GIVEN PARAMETERS

Supply Voltage

VDD = 1.8V

Power Constraint

P ≤ 1 mW

Maximum allowable drain current

ID ≤ P / VDD

ID ≤ 10⁻³ / 1.8

ID ≤ 555.5 µA

Chosen operating current

ID = 400 µA

Threshold Voltages

VTN = 0.366 V  
|VTP| = 0.39 V

Channel Length

L = 560 nm

---

# CIRCUIT DIAGRAM

<p align="center">
  <img src="Screenshot 2026-02-26 155307.png" width="650">
</p>

<p align="center">
  <em>Figure 1: Common Source Amplifier with PMOS Active Load</em>
</p>

The circuit consists of an NMOS transistor acting as the amplifying device and a PMOS transistor acting as the active load. The NMOS controls the current through the circuit while the PMOS provides a high resistance load, which helps in achieving higher gain compared to a simple resistor load.

---

# DC ANALYSIS (BIAS DESIGN)

## 1. Overdrive Voltage Constraints

For proper operation, both transistors must remain in saturation.

### NMOS saturation condition

VDS1 ≥ Vov

VDS1 = Vout − VS

Therefore

Vout − VS ≥ Vov

### PMOS saturation condition

VSD2 ≥ Vov

VSD2 = VDD − Vout

Therefore

1.8 − Vout ≥ Vov

---

## 2. Maximum Allowable Overdrive Voltage

Combining the above two conditions

Vov ≤ Vout − VS  
Vov ≤ 1.8 − Vout

Equating both limits

Vout − VS = 1.8 − Vout

2Vout = 1.8 + VS

Vout = (1.8 + VS) / 2

---

## 3. Source Voltage Selection

The source voltage is determined by the source resistor.

VS = ID RS

To maintain proper headroom and strong inversion, a small source voltage is chosen.

VS ≈ 0.2 V

Thus

RS = VS / ID

RS = 0.2 / (400 × 10⁻⁶)

RS = 500 Ω

---

## 4. Output Voltage Selection

Using

Vout = (1.8 + VS) / 2

Vout = (1.8 + 0.2) / 2

Vout = 1.0 V

To slightly improve voltage swing, the output voltage was chosen as

Vout = 1.1 V

This still satisfies both saturation conditions.

---

## 5. Overdrive Voltage Choice

From NMOS condition

Vov ≤ 1.1 − 0.2

Vov ≤ 0.9 V

From PMOS condition

Vov ≤ 1.8 − 1.1

Vov ≤ 0.7 V

Thus

Vov,max = 0.7 V

In practical analog design

0.2 V ≤ Vov ≤ 0.3 V

Therefore

Vov = 0.25 V

---

## 6. NMOS Gate Bias

VGS = VTN + Vov

VGS = 0.366 + 0.25

VGS = 0.616 V

Input bias voltage

VB1 = VGS + VS

VB1 = 0.616 + 0.2

VB1 = 0.816 V

---

## 7. PMOS Gate Bias

For PMOS

Vov = VSG − |VTP|

VSG = Vov + |VTP|

VSG = 0.25 + 0.39

VSG = 0.64 V

Since PMOS source is connected to VDD

VSG = VDD − VG

0.64 = 1.8 − VG

VG = 1.16 V

VB2 = 1.16 V

---

## 8. Saturation Check

NMOS

VDS = 1.1 − 0.2

VDS = 0.9 V

0.9 > 0.25

NMOS operates in saturation.

PMOS

VSD = 1.8 − 1.1

VSD = 0.7 V

0.7 > 0.25

PMOS also operates in saturation.

Thus both transistors operate correctly in saturation.

---

## 9. NMOS Width Calculation

Using the MOS current equation

ID = (1/2) μn Cox (W/L) (Vov)²

Rearranging

Wn = (2 ID L) / (μn Cox (Vov)²)

Substituting values

Wn ≈ 30.44 µm

---

## 10. PMOS Width Calculation

Using PMOS mobility parameter

kp = 9.7361 × 10⁻⁵ A/V²

From the current equation

Wp = 73.56 µm

---

## NOTE ON WIDTH ADJUSTMENT

During simulation, the transistor widths were slightly modified to obtain the correct DC operating point. Adjusting the width allows the drain current to reach the desired value while keeping the circuit properly biased.

From simulation values:

CMOSN width ≈ 54 µm  
CMOSP width ≈ 165.255 µm

This adjustment ensured that the circuit achieved the correct operating point.

---

# TRANSIENT ANALYSIS

<p align="center">
  <img src="Screenshot 2026-03-05 121026.png" width="750">
</p>

<p align="center">
  <em>Figure 2: Transient Response of the Amplifier</em>
</p>

From the simulation waveform:

Vout(pp) = 531.403 mV

Vin(pp) = 19.768 mV

Voltage Gain

Av = Vout / Vin

Av = 26.88

In dB

Av(dB) = 20 log(Av)

Av ≈ 28.58 dB

The transient response clearly shows that the output signal is amplified and inverted relative to the input signal, confirming proper CS amplifier operation.

---

# AC ANALYSIS

<p align="center">
  <img src="Screenshot 2026-02-26 161607.png" width="750">
</p>

<p align="center">
  <em>Figure 3: Frequency Response of the Amplifier</em>
</p>

### Without Load Capacitor

Midband Gain = 28.76 dB

3 dB Gain = 25.76 dB

3 dB Bandwidth

BW = 52.612 MHz

Unity Gain Bandwidth

UGB ≈ 1.714 GHz

Verification

UGB = Av × BW

UGB ≈ 26.88 × 52.612M

UGB ≈ 1.41 GHz

which is close to the simulated value.

---

### With Load Capacitor

Midband Gain = 28.76 dB

3 dB Bandwidth

BW = 772.909 kHz

Unity Gain Bandwidth

UGB ≈ 21.216 MHz

Verification

UGB = Av × BW

UGB ≈ 26.88 × 772.909k

UGB ≈ 20.77 MHz

which closely matches the simulated value.

---

# RESULTS

| Parameter | Value |
|--------|--------|
| Drain Current | 400 µA |
| Overdrive Voltage | 0.25 V |
| Source Resistance | 500 Ω |
| Output Voltage | 1.1 V |
| NMOS Width | 30.44 µm |
| PMOS Width | 73.56 µm |
| Transient Gain | 26.88 |
| Gain in dB | 28.58 dB |
| Bandwidth (no load) | 52.612 MHz |
| Unity Gain Frequency | 1.714 GHz |
| Bandwidth (with load capacitor) | 772.909 kHz |

---

# INFERENCE

From this experiment, the Common Source amplifier with PMOS active load was successfully designed and analyzed. The DC analysis ensured that both NMOS and PMOS transistors operated in the saturation region with proper biasing conditions.

Transient analysis confirmed that the amplifier provides significant voltage gain along with phase inversion, which is characteristic of the CS configuration.

The AC analysis showed that the amplifier achieves a large unity gain bandwidth when no load capacitor is connected. However, when a load capacitor is introduced, the bandwidth decreases significantly because the increased capacitance at the output node shifts the dominant pole to a lower frequency.

Thus, the experiment clearly demonstrates the effect of device sizing, biasing conditions, and output capacitance on the performance of a MOSFET amplifier.
