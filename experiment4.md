 # EXPERIMENT 4
 # DIFFERENTIAL  AMPLIFIER ANALYSIS
## Aim
   To design and analyze a MOS differential amplifier circuit using 180 nm CMOS technology, and to study its performance characteristics such as gain, input common-mode range, output swing, and frequency response.

## Introduction
A differential amplifier is an analog circuit that amplifies the difference between two input voltages while rejecting any signal that is common to both inputs. This property is known as common-mode rejection and is essential for minimizing noise and interference in electronic systems.

The two input signals are defined as:
V_id = V_in1 - V_in2  
V_cm = (V_in1 + V_in2) / 2  
where V_id is the differential input voltage and V_cm is the common-mode voltage.

A basic differential amplifier consists of two matched transistors forming a differential pair, biased by a constant current source known as the tail current. The total current remains constant and is shared between the two transistors:
I_tail = I_1 + I_2  

When the input voltages are equal, the current splits equally between the two transistors, resulting in equal output voltages. When a difference is applied between the inputs, the current is steered from one transistor to the other, producing a corresponding change in output voltages.
The output voltage is obtained by converting the current through the load into voltage:
V_out = V_DD - I_D × R_D  

The transconductance of the transistor determines how effectively the input voltage controls the current:
g_m = (2 × I_D) / V_ov  

The gain of the differential amplifier is given by:
Single-ended gain:
A_v = - (g_m × R_D) / 2  

Differential gain:
A_d = g_m × R_D  

The amplifier ideally responds only to the differential input and rejects the common-mode input. The effectiveness of this rejection is measured using the Common-Mode Rejection Ratio (CMRR):
CMRR = A_d / A_cm  

A higher CMRR indicates better rejection of noise and interference.
Differential amplifiers operate linearly only within a limited input range defined by the overdrive voltage:
|V_id| ≤ V_ov  

Beyond this range, one transistor turns off, and the circuit becomes nonlinear.
Differential amplifiers are widely used in operational amplifiers, analog signal processing, communication systems, and sensor interfaces due to their high gain, stability, and noise rejection capability.

# Circuit 1 - NMOS Differential Amplifier with Resistive Load and tail current

##  Theory

A differential amplifier is a fundamental analog circuit used to amplify the difference between two input signals while rejecting any common-mode signal present at both inputs. It forms the core building block of many analog systems, including operational amplifiers.
This circuit consists of two NMOS transistors (M1 and M2) configured as a differential pair, with their sources connected together and biased using a constant current source (I1). The drains are connected to resistive loads (R1 and R2), which convert variations in drain current into output voltage.
The total current supplied by the tail current source remains constant:

## Working Principle

- The circuit consists of two matched NMOS transistors (M1 and M2) forming a differential pair.
- The sources of both transistors are connected to a constant tail current source, which provides a fixed current (I_SS).
- The drains are connected to resistive loads (R_D), which convert current variations into output voltages.
- The amplifier responds to the difference between the two input voltages:
  V_id = V_in1 - V_in2
- The total tail current remains constant:
  I_SS = I_D1 + I_D2
- When a differential input is applied, the tail current is redistributed between the two transistors.

- If V_in1 > V_in2:
  - M1 conducts more current
  - M2 conducts less current

- If V_in2 > V_in1:
  - M2 conducts more current
  - M1 conducts less current

- The change in drain current produces voltage changes across the load resistors:
  V_out = V_DD - I_D × R_D

- The output voltages at the two drains are equal in magnitude but opposite in phase.

- For small differential input (|V_id| ≤ V_ov):
  - Both transistors operate in saturation
  - The circuit behaves linearly
  - Output is proportional to input difference

- For large differential input:
  - One transistor turns OFF
  - The other carries nearly all the current
  - The circuit becomes non-linear

- The circuit converts differential input voltage into differential output voltage by current steering.

## Cirucit Diagram
<img width="895" height="735" alt="image" src="https://github.com/user-attachments/assets/c08e28ac-6d43-47cd-9f4a-e71198fd52ce" />

## DC Analysis

## Given Specifications

V_DD = 0.9 V  
V_SS = -0.9 V  
V_T = 0.36 V  
V_inCM = 0 V  
V_P = -0.7 V  
Power ≤ 1.8 mW  
εr = 3.9  
ε0 = 8.854 × 10^-12 F/m  
t_ox = 4.1 × 10^-9 m  
μn = 273.809 cm²/Vs  
μp = 115.689 cm²/Vs  
L = 480 nm  

## Calculations

1. Tail current:

P = V × I  
1.8 mW = 1.8 V × I  
I_SS = 1 mA  

2. Branch current:

I_D1 = I_D2 = I_SS / 2  
I_D = 0.5 mA  

3. Load resistance:

V_out = V_DD - I_D × R_D  
At midpoint (V_out = 0):
R_D = V_DD / I_D  
R_D = 0.9 / (0.5 × 10^-3)  
R_D = 1.8 kΩ  

4. Gate-source voltage:

V_GS = V_G - V_S  
V_GS = 0 - (-0.7) = 0.7 V  

5. Overdrive voltage:

V_ov = V_GS - V_T  
V_ov = 0.7 - 0.36 = 0.34 V  

6. Saturation check:

V_DS = V_D - V_S = 0 - (-0.7) = 0.7 V  
Condition:  
V_DS ≥ V_ov  
0.7 ≥ 0.34  → Saturation ✔  

7. Oxide capacitance:

C_ox = (εr × ε0) / t_ox  
C_ox = (3.9 × 8.854 × 10^-12) / (4.1 × 10^-9)  
C_ox = 8.42 × 10^-3 F/m²  

8. Mobility conversion:
μn = 273.809 × 10^-4 = 0.02738 m²/Vs  

9. Width calculation:

I_D = (1/2) × μn × C_ox × (W/L) × V_ov²  
0.5 × 10^-3 = (1/2) × 0.02738 × 8.42 × 10^-3 × (W / 480 × 10^-9) × (0.34)²  
W ≈ 18 μm  
Change length to 17.37u , so that we get the required 0.5m A as current

10. Input common-mode range:

V_inCM(min) = V_S + V_T  
V_inCM(min) = -0.7 + 0.36 = -0.34 V  

V_inCM(max) = V_D + V_T  
V_inCM(max) = 0 + 0.36 = 0.36 V  

Final:  
-0.34 V ≤ V_inCM ≤ 0.36 V  


11. Output common-mode range:

V_outCM(max) = V_DD = 0.9 V  

V_outCM(min) = V_S + V_ov  
V_outCM(min) = -0.7 + 0.34 = -0.36 V  

Final:  
-0.36 V ≤ V_outCM ≤ 0.9 V  

12. Differential input range:

Linear region:  

|V_id| ≤ V_ov  
|V_id| ≤ 0.34 V  
-0.34 V ≤ V_id ≤ 0.34 V  

Full conduction limit:  

|V_id| ≤ √2 × V_ov  
|V_id| ≤ 0.48 V  

## Differential Amplifier Operation Cases

## Case (i): When V_in1 = V_in2

- Transistors M1 and M2 are identical and equally biased  
- Tail current splits equally:
  I_SS = I_D1 + I_D2  
  I_D1 = I_D2 = I_SS / 2  

- Output voltages are equal:
  V_out1 = V_DD - I_D1 × R_D  
  V_out2 = V_DD - I_D2 × R_D  
- Since I_D1 = I_D2:
 V_out1 = V_out2  

<img width="1335" height="748" alt="image" src="https://github.com/user-attachments/assets/2ab247f5-b9ea-45e5-980a-d7ffb167a683" />

## Case (ii): When V_in1 > V_in2

- Transistor M1 conducts more current:
  I_D1 > I_D2  
- Current redistribution:
  I_SS = I_D1 + I_D2  

- Output voltages:
  V_out1 = V_DD - I_D1 × R_D  
  V_out2 = V_DD - I_D2 × R_D  
- Since I_D1 > I_D2:
  V_out1 < V_out2  

## Case (iii): When V_in1 < V_in2

- Transistor M2 conducts more current:
  I_D2 > I_D1  
- Current redistribution:
  I_SS = I_D1 + I_D2  

- Output voltages:
  V_out1 = V_DD - I_D1 × R_D  
  V_out2 = V_DD - I_D2 × R_D  
- Since I_D2 > I_D1:
  V_out2 < V_out1  

## Final Observation
- The differential amplifier converts input voltage difference into current difference and then into output voltage difference.  
- Outputs are always opposite in nature (one increases while the other decreases).  

## Explanation of Operating Ranges 

### Input Common-Mode Range (V_inCM)

- Ensures both transistors remain ON and in saturation  
- Minimum limit when transistor just turns ON  
  V_inCM(min) = V_S + V_T  
- Maximum limit set by saturation condition  
  V_inCM(max) = V_D + V_T  
- Defines proper biasing of the differential pair  

### Output Common-Mode Range (V_outCM)

- Determines allowable output voltage swing  
- Maximum value limited by supply  
  V_outCM(max) = V_DD  
- Minimum value set by saturation condition  
  V_outCM(min) = V_S + V_ov  
- Ensures transistor does not enter triode region  


### Differential Input Range (V_id)

- Determines linear operation of the amplifier  
- Linear region condition  
  |V_id| ≤ V_ov  
- Both transistors conduct in this range  
- Output is proportional to input difference  
- For larger inputs  
  |V_id| ≤ √2 × V_ov  
- Beyond this, one transistor turns OFF  
- Circuit becomes non-linear  

### Key Points
- V_inCM → ensures proper biasing  
- V_outCM → ensures proper output swing  
- V_id → ensures linear amplification  

 # Transient Analysis
 # To Check Linearity
  a) Condition for linear region:
 <img width="1904" height="843" alt="image" src="https://github.com/user-attachments/assets/a4b87a21-6349-4af1-9d21-f0819cd16d2e" />

|V_id| < √2 × V_ov  
10m < 0.48  ✔ (Linear operation)

b) Condition for non-linear region:
<img width="1912" height="836" alt="image" src="https://github.com/user-attachments/assets/2d816808-bfe0-4157-b356-cd920770f804" />

|V_id| > √2 × V_ov  
0.9 > 0.48  ✔ (Non-linear operation)

## Comparison: Linear vs Non-Linear Operation

| Parameter              | Linear Region                     | Non-Linear Region              |
|-----------------------|----------------------------------|--------------------------------|
| Condition             | |V_id| < √2 V_ov                 | |V_id| > √2 V_ov               |
| Transistor state      | Both ON                          | One OFF                        |
| Current distribution  | Shared between M1 & M2           | Entire current in one transistor |
| Output behavior       | Proportional to input            | Clipping / saturation          |
| Operation type        | Amplification                    | Switching                      |
| Distortion            | Low                              | High                           |
| Gain                  | Constant                         | Varies                         |
| Application           | Analog amplification             | Digital-like behavior          |

## Interpretation

- When |V_id| is small, the circuit operates in the linear region where both transistors conduct and the output is a faithful amplified version of the input.
- As |V_id| increases beyond √2 V_ov, one transistor turns OFF and the circuit enters the non-linear region, causing distortion and clipping.
- Therefore, for proper amplifier operation, the input signal must be kept within the linear range.

## 2. Practical Gain

A_v = ΔV_out / ΔV_in  
A_v = (46.29 mV + 46.29 mV) / (20 mV)  
A_v = 92.58 / 20  
A_v = 4.629 V/V  

Gain in dB:

A_v(dB) = 20 log(A_v)  
A_v(dB) = 20 log(4.629)  
A_v(dB) = 12.606 dB  

## 3. Theoretical Gain

Assume:
λ = 0.1 V⁻¹  

### Output resistance:

r_o = 1 / (λ × I_D)  
r_o = 1 / (0.1 × 0.5 × 10^-3)  
r_o = 20 kΩ  

Effective output resistance:

r_o_eff = r_o1 || r_o2  
r_o_eff = 20k || 20k  
r_o_eff = 10 kΩ  

Total output resistance:

R_out = r_o_eff || R_D  
R_out = 10k || 1.8k  
R_out ≈ 1.53 kΩ  

### Transconductance:

g_m = 2I_D / V_ov  
g_m = (2 × 0.5 × 10^-3) / 0.34  
g_m = 2.94 mS  

### Gain:
A_v = g_m × R_out  
A_v = (2.94 × 10^-3) × (1.53 × 10^3)  
A_v = 4.498 V/V  


Gain in dB:
A_v(dB) = 20 log(A_v)  
A_v(dB) = 20 log(4.498)  
A_v(dB) = 13.06 dB  

## Final Results
Practical Gain = 4.629 V/V ≈ 12.606 dB  
Theoretical Gain = 4.498 V/V ≈ 13.06 dB 

## Reason for Difference Between Practical and Theoretical Gain

- Theoretical gain is calculated using ideal assumptions such as constant λ, no parasitic effects, and perfectly matched devices.
- Practical gain is obtained from simulation, which includes real device behavior from the technology model (TSMC 180 nm).
- In practical circuits, channel length modulation (λ) is not constant and may be higher than assumed, reducing output resistance and gain.
- Parasitic capacitances (Cgs, Cgd, wiring capacitance) affect the gain, especially at higher frequencies.
- Resistive loading and finite output resistance reduce the effective gain compared to ideal calculations.
- Device mismatches and non-ideal current source behavior also introduce small variations.
- Numerical approximations and rounding during hand calculations contribute to slight differences.

## Conclusion
The difference between practical and theoretical gain is expected due to non-ideal effects present in real circuits. However, since both values are close, the design is considered accurate and valid.

# AC Analysis
<img width="1915" height="864" alt="image" src="https://github.com/user-attachments/assets/8221a5b2-876f-44f9-85ee-88ca6cedde38" />

## From Plot
Midband gain = 13.358 dB  
f_L = 0 Hz  
f_H = 10.186 GHz  

## 1. Bandwidth

BW = f_H - f_L  
BW = 10.186 GHz - 0  
BW = 10.186 GHz  

## 2. -3 dB Gain

A_v(-3 dB) = Midband gain - 3  
A_v(-3 dB) = 13.358 - 3  
A_v(-3 dB) = 10.358 dB  

## 3. Linear Gain

A_v = 10^(Gain / 20)  
A_v = 10^(13.358 / 20)  
A_v ≈ 4.78 V/V  

## 4. Unity Gain Bandwidth (UGB)

UGB = A_v × f_H  
UGB = 4.78 × 10.186 GHz  
UGB ≈ 48.68 GHz  
UGB cannot be observed in the plot because the gain does not reach 0 dB within the shown frequency range.  
Hence, it is calculated theoretically using UGB = A_v × f_3dB assuming a single dominant pole.

## 5. Gain Bandwidth Product (GBP)

GBP = A_v × BW  
GBP = 4.78 × 10.186 GHz  
GBP ≈ 48.68 GHz  

# Circuit 2 - Differential Amplifier Using PMOS Active Load and NMOS Current Source

## Theory

- This circuit is a CMOS differential amplifier that employs a PMOS current mirror as the active load and an NMOS transistor as the tail current source.
- The NMOS transistors (M1, M2) act as the differential pair, converting the input voltage difference into corresponding current variations.
- The PMOS transistors (M3, M4) function as an active load, eliminating the need for resistors and forming a current mirror configuration.
- The NMOS transistor (M5) operates as a constant current source, ensuring proper biasing and stable operation.
- The circuit amplifies the differential input signal:
  V_id = V_in1 - V_in2  

## Special Features

- Achieves higher voltage gain compared to resistive load configurations  
- Increased output resistance due to active load enhances gain  
- Offers better power efficiency using current mirror structure  
- Provides improved common-mode rejection (CMRR)  
- Converts differential signals into a single-ended output  
- Occupies less chip area, making it suitable for integrated circuits  
- Commonly used as the input stage in operational amplifiers

## Circuit diagram
<img width="900" height="650" alt="image" src="https://github.com/user-attachments/assets/9cb741ce-a076-4d21-b389-7cac4ff3d927" />

## DC Analysis
## Given Specifications

V_DD = 0.9 V  
V_SS = -0.9 V  
V_T = 0.36 V  
V_P = -0.7 V  
εr = 3.9  
ε0 = 8.854 × 10^-12 F/m  
t_ox = 4.1 × 10^-9 m  
μn = 273.809 cm²/Vs  
μp = 115.689 cm²/Vs  
L = 480 nm  


## 1. M5 (NMOS Tail Current Source)
Previously Calculated I_total = 1m A
For saturation:

V_DS ≥ V_GS - V_T  
V_G = V_bias  
From condition:
V_G ≈ -0.334 V  

| Parameter | Expression | Substitution | Result |
|----------|------------|-------------|--------|
| V_GS | V_G - V_S | -0.334 - (-0.9) | 0.566 V |
| V_ov | V_GS - V_T | 0.566 - 0.36 | 0.2 V |
| V_DS | V_D - V_S | -0.7 - (-0.9) | 0.2 V |
| Condition | V_DS ≥ V_GS - V_T | 0.2 ≥ 0.2 | Saturation |
| W | I_D = (1/2) μ_n C_ox (W/L) V_ov² | W = (2×1×10^-3×480×10^-9)/(0.02738×8.42×10^-3×0.206²) | ≈ 104 μm |
Change length to 219.7u , so that we get the required 1m A as current

### Points:
- M5 acts as a constant current source and controls the total tail current.  
- It operates near saturation, ensuring stable current supply.  
- Slight mismatch in condition is acceptable in practical design.  

## 2. M1, M2 (NMOS Differential Pair)

| Parameter | Expression | Substitution | Result |
|----------|------------|-------------|--------|
| V_GS | V_G - V_S | 0 - (-0.7) | 0.7 V |
| V_ov | V_GS - V_T | 0.7 - 0.36 | 0.34 V |
| V_DS | V_D - V_S | 0 - (-0.7) | 0.7 V |
| Condition | V_DS ≥ V_GS - V_T | 0.7 ≥ 0.34 | Saturation ✔ |
| I_D | I_SS / 2 | 1 mA / 2 | 0.5 mA |
| g_m | 2I_D / V_ov | (2×0.5 mA)/0.34 | 2.94 mS |
| W | I_D = (1/2) μ_n C_ox (W/L) V_ov² | W = (2×0.5×10^-3×480×10^-9)/(0.02738×8.42×10^-3×0.34²) | ≈ 18 μm |
Change length to 30.625u , so that we get the required 0.5m A as current

### Points:
- M1 and M2 form the differential input stage.  
- Both transistors operate in saturation for linear amplification.  
- They convert input voltage difference into current difference.  
- Transconductance (g_m) determines the gain of the amplifier.  

## 3. M3, M4 (PMOS Active Load)

| Parameter | Expression | Substitution | Result |
|----------|------------|-------------|--------|
| V_SG | V_S - V_G | 0.9 - 0 | 0.9 V |
| V_ov | V_SG - |V_T| | 0.9 - 0.36 | 0.54 V |
| V_SD | V_S - V_D | 0.9 - 0 | 0.9 V |
| Condition | V_SD ≥ V_SG - |V_T| | 0.9 ≥ 0.54 | Saturation ✔ |
| W | I_D = (1/2) μ_p C_ox (W/L) V_ov² | W = (2×0.5×10^-3×480×10^-9)/(0.01157×8.42×10^-3×0.34²) | ≈ 16.9 μm |
Change length to 38.21u, so that we get the required 0.5m A as current

### Points:
- M3 and M4 act as an active load using current mirror configuration.  
- Active load increases output resistance and hence gain.  
- Provides better performance compared to resistive load.  
- Ensures efficient current transfer and amplification.

  <img width="1597" height="738" alt="image" src="https://github.com/user-attachments/assets/190a9f16-4184-4d29-b843-6e34367229d7" />

## Input Common-Mode Range (V_inCM)

| Parameter        | Expression                          | Substitution                  | Result     |
|------------------|--------------------------------------|--------------------------------|------------|
| V_inCM(min)      | V_SS + V_ov(M5) + V_T               | -0.9 + 0.2 + 0.36             | -0.34 V    |
| V_inCM(max)      | V_DD - V_ov(PMOS) + V_T             | 0.9 - 0.2 + 0.36              | 1.06 V     |

## Final Range
-0.34 V ≤ V_inCM ≤ 1.06 V  

## Output Common-Mode Range (V_outCM)

| Parameter        | Expression            | Substitution        | Result     |
|------------------|----------------------|---------------------|------------|
| V_outCM(min)     | V_S + V_ov           | -0.7 + 0.34         | -0.36 V    |
| V_outCM(max)     | V_DD                 | 0.9                 | 0.9 V      |

## Final Range
-0.36 V ≤ V_outCM ≤ 0.9 V  

## Transient Analysis
 # To Check Linearity
  a) Condition for linear region:
     |V_id| < √2 × V_ov  
     10m < 0.48  ✔ (Linear operation)
     <img width="1916" height="861" alt="image" src="https://github.com/user-attachments/assets/160def4a-bd40-4aeb-a5d0-6ac966117f6e" />

b) Condition for non-linear region:
     <img width="1913" height="847" alt="image" src="https://github.com/user-attachments/assets/52201c49-16df-45e8-9dd7-f6f6f48c6fe0" />

  |V_id| > √2 × V_ov  
  0.9 > 0.48  ✔ (Non-linear operation)
  
  ## Gain Calculation

### 1. Practical Gain

A_v = ΔV_out / ΔV_in  
A_v = (20.17 mV + 17.68 mV) / 20 mV  
A_v = 37.85 / 20  
A_v = 1.89 V/V  

### Gain in dB

A_v(dB) = 20 log(A_v)  
A_v(dB) = 20 log(1.89)  
A_v(dB) = 5.529 dB  

### 2. Theoretical Gain

A_v = √[(μ_n × (W/L)_n) / (μ_p × (W/L)_p)]  

### Substitution

μ_n = 273.809 × 10^-4  
μ_p = 115.689 × 10^-4  

(W/L)_n = 38.2 / 480×10^-9  
(W/L)_p = 30.625 / 480×10^-9  

### Calculation

A_v = √[(273.809 × 38.2) / (115.689 × 30.625)]  
A_v = √(10462.9 / 3542.9)  
A_v = √(2.95)  
A_v ≈ 1.718 V/V  

### Gain in dB

A_v(dB) = 20 log(A_v)  
A_v(dB) = 20 log(1.718)  
A_v(dB) ≈ 4.70 dB  

## Gain Comparison

| Parameter            | Expression / Method                          | Substitution / Value                  | Result            |
|----------------------|----------------------------------------------|--------------------------------------|-------------------|
| Practical Gain (A_v) | ΔV_out / ΔV_in                               | (20.17 + 17.68) / 20                 | 1.89 V/V          |
| Practical Gain (dB)  | 20 log(A_v)                                  | 20 log(1.89)                         | 5.529 dB          |
| Theoretical Gain (A_v) | √[(μ_n (W/L)_n) / (μ_p (W/L)_p)]          | √[(273.809×38.2)/(115.689×30.625)]   | 1.72 V/V          |
| Theoretical Gain (dB) | 20 log(A_v)                                 | 20 log(1.72)                         | 4.70 dB           |

## Final Observation
Practical gain is slightly higher than theoretical gain due to non-ideal effects and approximation in hand calculations.

## AC Analysis
<img width="1907" height="891" alt="image" src="https://github.com/user-attachments/assets/9b3923fc-e60e-47c7-8c63-527d439951fa" />

## Midband Gain

A_v(dB) = 5.55 dB  

Convert to linear:
A_v = 10^(A_v(dB)/20)  
A_v = 10^(5.55/20)  
A_v = 1.894 V/V  

## Bandwidth (BW)
At -3 dB point:
A_v(dB) - 3 = 5.55 - 3 = 2.55 dB  

From graph:
f_L = 0 Hz  
f_H = 2.96 GHz  

BW = f_H - f_L  
BW = 2.96 GHz - 0  
BW = 2.96 GHz  

## Unity Gain Bandwidth (UGB)
<img width="1910" height="848" alt="image" src="https://github.com/user-attachments/assets/25951472-4038-4006-a80f-4da5ba5261c8" />

From Plot
UGB (at 0 dB) = 5.19 GHz  

### Theoretical UGB

UGB = f_3dB × A_v 
UGB = 2.96 × 1.894  
UGB = 5.60 GHz  

## Final Results

| Parameter               | Value                     |
|------------------------|---------------------------|
| Midband Gain (dB)      | 5.55 dB                  |
| Midband Gain (linear)  | 1.894 V/V                |
| Bandwidth (BW)         | 2.96 GHz                 |
| UGB (Practical)        | 5.19 GHz                 |
| UGB (Theoretical)      | 5.60 GHz                 |


# Circuit 3 - CMOS Differential Amplifier with PMOS Current Mirror Load and NMOS Tail Current Source (Bias-Controlled using VB1 and VB2)

## Working 

- This is a CMOS differential amplifier that uses a PMOS current mirror as an active load and a biased NMOS transistor as a tail current source.
- M3 and M4 form the NMOS differential pair, which converts the input voltage difference into current variation.
- M1 and M2 act as PMOS active load, implemented as a current mirror to enhance gain and output resistance.
- M5 acts as a tail current source, and its bias is controlled using VB1 to maintain constant current.
- VB2 is used to properly bias the PMOS current mirror, ensuring correct operation in saturation.
- The circuit amplifies the differential input:
  V_id = V_in1 - V_in2  
- Capacitors C1 and C2 are used for AC coupling, allowing signal transmission while blocking DC components.

## Special Features

- Uses bias voltages (VB1, VB2) for precise control of operating point  
- Provides higher gain due to active load configuration  
- Improved stability and linearity due to controlled biasing  
- Better performance compared to simple resistive load differential amplifier  
- Suitable for low-voltage analog design  

## One-Line Description
A CMOS differential amplifier with PMOS active load and externally biased NMOS current source for improved gain, stability, and precise bias control.
  
## Circuit Diagram 

<img width="779" height="700" alt="image" src="https://github.com/user-attachments/assets/efe1e024-663b-4c0d-98e3-4f6977b545c3" />

## DC Analysis

## Complete MOSFET Calculation (W, VB1, VB2, Saturation Check)

## Given
V_DD = 0.9 V  
V_SS = -0.9 V  
V_T = 0.36 V  
I_SS = 1 mA  
μ_n = 0.02738 m²/Vs  
μ_p = 0.01157 m²/Vs  
C_ox = 8.42 × 10^-3 F/m²  
L = 480 nm  

## 1. M5 (NMOS Tail Current Source)

### Step 1: Bias Voltage (VB1)
V_GS = V_ov + V_T  
V_GS = 0.206 + 0.36 = 0.566 V  
V_G = V_S + V_GS  
V_G = -0.9 + 0.566 = -0.334 V  
VB1 ≈ -0.35 V  

### Step 2: Width Calculation
I_D = (1/2) μ_n C_ox (W/L) V_ov²  
W = (2 I_D L) / (μ_n C_ox V_ov²)  
W = (2×1×10^-3×480×10^-9)/(0.02738×8.42×10^-3×0.206²)  
W ≈ 104 μm  
Change length to 340.5um , so that we get the required 0.5m A as current

### Step 3: Saturation Check
V_DS = -0.7 - (-0.9) = 0.2 V  
V_ov = 0.206 V  
0.2 ≥ 0.206 → ≈ Saturation ✔  

## 2. M3, M4 (NMOS Differential Pair)

### Step 1: Current
I_D = I_SS / 2 = 0.5 mA  

### Step 2: Voltages
V_GS = 0 - (-0.7) = 0.7 V  
V_ov = 0.7 - 0.36 = 0.34 V  

### Step 3: Width Calculation
W = (2×0.5×10^-3×480×10^-9)/(0.02738×8.42×10^-3×0.34²)  
W ≈ 18 μm  
Change length to 32um , so that we get the required 0.5m A as current

### Step 4: Saturation Check
V_DS = 0 - (-0.7) = 0.7 V  
0.7 ≥ 0.34 → Saturation ✔  

## 3. M1, M2 (PMOS Active Load)

### Step 1: Bias Voltage (VB2)
V_D=0
V_SD ≥ V_SG - V_T
V_D ≤ V_G + V_T
0 ≤ V_G + 0.36
-0.36 ≤ V_G
V_G ≥ -0.36
To ensure saturation:
VB2 ≈ -0.36 V  

### Step 2: Current
I_D = 0.5 mA 

### Step 3: Width Calculation
W = (2×0.5×10^-3×480×10^-9)/(0.01157×8.42×10^-3×0.34²)  
W ≈ 16.9 μm  
Change length to 13.876um , so that we get the required 0.5m A as current

### Step 4: Saturation Check
V_SD = 0.9 - 0 = 0.9 V  
V_ov = 0.54 V  
0.9 ≥ 0.54 → Saturation ✔  

## Final Results

| Transistor | Width (W) | Bias Voltage | Region |
|------------|----------|--------------|--------|
| M5         | 104 μm   | VB1 = -0.35 V | Saturation |
| M3, M4     | 18 μm    | —            | Saturation |
| M1, M2     | 16.9 μm  | VB2 = -0.367 V | Saturation |

## Final Conclusion
- All MOSFETs operate in saturation  
- Bias voltages ensure proper operation  
- Circuit is correctly designed for amplification

## Common-Mode Voltage Ranges

## 1. Input Common-Mode Range (V_inCM)

| Parameter        | Expression                          | Substitution                  | Result     |
|------------------|--------------------------------------|--------------------------------|------------|
| V_inCM(min)      | V_SS + V_ov(M5) + V_T               | -0.9 + 0.206 + 0.36           | -0.334 V   |
| V_inCM(max)      | V_DD - V_ov(PMOS) + V_T             | 0.9 - 0.54 + 0.36             | 0.72 V     |

### Final Range
-0.334 V ≤ V_inCM ≤ 0.72 V  

## 2. Output Common-Mode Range (V_outCM)

| Parameter        | Expression            | Substitution        | Result     |
|------------------|----------------------|---------------------|------------|
| V_outCM(min)     | V_S + V_ov(NMOS)     | -0.7 + 0.34         | -0.36 V    |
| V_outCM(max)     | V_DD - V_ov(PMOS)    | 0.9 - 0.54          | 0.36 V     |

### Final Range
-0.36 V ≤ V_outCM ≤ 0.36 V  

  <img width="1701" height="908" alt="image" src="https://github.com/user-attachments/assets/d470f3ba-f2a8-4662-b669-b7523d1b6d23" />

## Transient Analysis
 ## To Check Linearity
  a) Condition for linear region:
     |V_id| < √2 × V_ov  
     5m < 0.48  ✔ (Linear operation)
     <img width="1917" height="862" alt="image" src="https://github.com/user-attachments/assets/d46fe47e-6fc8-4153-a21b-1d2192a86bf2" />

b) Condition for non-linear region:
    <img width="1899" height="856" alt="image" src="https://github.com/user-attachments/assets/963acf70-0654-46c6-a7f4-81e4f0d8e937" />

  |V_id| > √2 × V_ov  
  0.9 > 0.48  ✔ (Non-linear operation)
  
## Practical Gain Calculation

A_v = ΔV_out / ΔV_in  
A_v = (16.72 mV + 24.12 mV) / 10 mV  
A_v = 40.84 / 10  
A_v = 40.84 V/V  

### Gain in dB
A_v(dB) = 20 log(A_v)  
A_v(dB) = 20 log(40.84)  
A_v(dB) ≈ 32.22 dB  

## Final Result
A_v ≈ 40.84 V/V  
A_v ≈ 32.22 dB  

## Theoritical Gain

## Given
I_D = 0.5 mA  
V_ov(n) = 0.34 V  
λ ≈ 0.1 V^-1  

### Step 1: Transconductance
g_mn = 2I_D / V_ov  
g_mn = (2 × 0.5 × 10^-3) / 0.34  
g_mn = 2.94 mS  

### Step 2: Output Resistance
r_on = 1 / (λ I_D)  
r_on = 1 / (0.1 × 0.543 × 10^-3)  
r_on = 11.156 kΩ  

### Step 3: Practical Output Resistance
Due to non-ideal current mirror:
R_out ≈ r_on  
R_out ≈ 11.156 kΩ

### Step 4: Gain
A_v = g_mn × R_out  
A_v = 2.94 × 10^-3 × 11.156 × 10^3  
A_v = 32.8 V/V  

### Step 5: Gain in dB
A_v(dB) = 20 log(32.8)  
A_v(dB) ≈ 30.31 dB  

## Final Result
A_v ≈ 32.8 V/V  
A_v ≈ 30.31 dB  

## Conclusion
- This matches simulation (~32.5 dB) closely  
- Difference due to:
  - Parasitics  
  - Channel length modulation variation  
  - Mirror inefficiency  

## Practical vs Theoretical Gain

| Parameter               | Practical Gain                  | Theoretical Gain              |
|------------------------|--------------------------------|-------------------------------|
| Method                 | From waveform (ΔVout/ΔVin)     | Small-signal analysis         |
| Expression             | ΔVout / ΔVin                   | g_m × R_out                   |
| Gain (V/V)             | 40.84 V/V                      | 32.8 V/V                      |
| Gain (dB)              | 32.22 dB                       | 30.31 dB                      |

## AC Analysis
<img width="1911" height="832" alt="image" src="https://github.com/user-attachments/assets/394ae933-1f51-472b-9dc9-272db8ff3a60" />

## 1. Midband Gain

Given:
A_v(dB) = 32.74 dB  

Convert to linear:
A_v = 10^(A_v(dB)/20)  
A_v = 10^(32.74 / 20)  
A_v ≈ 43.35 V/V  

## 2. -3 dB Frequency

A_v(-3dB) = A_v(dB) - 3  
A_v(-3dB) = 32.74 - 3  
A_v(-3dB) = 29.74 dB  
This corresponds to cutoff frequency f_H  

## 3. Bandwidth (BW)

From graph:
f_L = 0 Hz  
f_H = 411.958 MHz  

BW = f_H - f_L  
BW = 411.958 MHz  

## 4. Unity Gain Bandwidth (UGB)

UGB = A_v (linear) × f_3dB  
UGB = 43.35 × 411.958 × 10^6  
UGB ≈ 17.85 GHz  

## Final Results
Midband Gain = 32.74 dB (≈ 43.35 V/V)  
Bandwidth = 411.958 MHz  
UGB ≈ 17.85 GHz  

UGB is not directly visible in the graph, so it is calculated theoretically.

# Comparison of Differential Amplifier Circuits

| Parameter | Circuit 1: NMOS + Resistive Load | Circuit 2: PMOS Active Load | Circuit 3: PMOS Active Load + Bias Control |
|----------|----------------------------------|-----------------------------|--------------------------------------------|
| Structure | NMOS differential pair with resistors | NMOS pair + PMOS current mirror load | Fully CMOS with bias-controlled loads |
| Load Type | Resistive (R_D) | Active load (PMOS mirror) | Active load + bias (VB1, VB2) |
| Tail Source | Ideal current source | NMOS current source | NMOS current source (bias-controlled) |
| Gain (Practical) | 4.63 V/V (~12.6 dB) | 1.89 V/V (~5.55 dB) | 40.84 V/V (~32.22 dB) |
| Gain (Theoretical) | ~4.5 V/V (~13 dB) | ~1.7 V/V (~4.7 dB) | ~32.8 V/V (~30.31 dB) |
| Output Resistance | Low (due to R_D) | High (active load) | Very high (active load + biasing) |
| Bandwidth | 10.186 GHz | 2.96 GHz | 411.958 MHz |
| UGB | ~48.68 GHz | ~5.60 GHz | ~17.85 GHz |
| V_inCM Range | Narrow (-0.34 to 0.36 V) | Wide (-0.34 to 1.06 V) | Moderate (-0.334 to 0.72 V) |
| V_outCM Range | Wide (-0.36 to 0.9 V) | Wide (-0.36 to 0.9 V) | Limited (-0.36 to 0.36 V) |
| Linearity Range | V_id ≤ 0.34 V | V_id ≤ 0.34 V | V_id ≤ 0.34 V |
| Power Efficiency | Low | Better | Best |
| Area | Large (resistors) | Compact | Compact |
| Design Complexity | Simple | Moderate | Complex |
| Biasing | Simple | Moderate | Precise (VB1, VB2 required) |
| Gain Accuracy | Moderate | Low | High |

# Applications (Brief)

### Circuit 1 – NMOS Differential Amplifier with Resistive Load
- Basic analog amplification circuits  
- Sensor signal conditioning  
- Low-frequency amplifier stages  
- Educational and fundamental analog design  
- Simple differential signal processing  

### Circuit 2 – Differential Amplifier with PMOS Active Load
- Operational amplifier input stages  
- Analog front-end circuits  
- Low-power integrated CMOS designs  
- High gain amplification stages  
- Signal processing systems  

### Circuit 3 – CMOS Differential Amplifier with Bias Control (VB1, VB2)
- High-gain precision amplifiers  
- Low-voltage analog circuits  
- CMOS integrated analog blocks  
- Communication and RF front-end stages  
- High-performance differential signal processing

# Result

- All three differential amplifier circuits were successfully designed and analyzed using 180 nm CMOS technology under ±0.9 V supply conditions.
- Circuit 1 (NMOS with resistive load) achieved a midband gain of ≈ 12.6 dB with very high bandwidth (~10.18 GHz), limited by low output resistance.
- Circuit 2 (PMOS active load) showed reduced gain ≈ 5.55 dB and bandwidth ≈ 2.96 GHz due to current mirror limitations, but improved integration and power efficiency.
- Circuit 3 (bias-controlled CMOS differential amplifier) achieved the highest gain ≈ 32.2 dB with bandwidth ≈ 411.96 MHz, due to increased effective output resistance.
- All MOSFETs in each circuit were verified to operate in saturation, ensuring proper amplification.
- The results clearly demonstrate the gain–bandwidth trade-off:
  Higher gain (Circuit 3) → Lower bandwidth  
  Lower gain (Circuit 1) → Higher bandwidth  
- Practical results closely match theoretical analysis with minor deviations due to non-ideal effects such as channel length modulation and parasitic capacitances.

  # Interpretation of Results

- The experiment demonstrates the operation of CMOS differential amplifiers in 180 nm technology under low-voltage conditions (±0.9 V), validating differential amplification through current steering.
- The results confirm that the **voltage gain is primarily determined by transconductance (g_m) and output resistance (R_out)**:
  A_v ≈ g_m × R_out  
- It is observed that **output resistance plays a dominant role** in enhancing gain. Circuits with higher effective R_out achieve significantly higher voltage gain.
- A clear **gain–bandwidth trade-off** is verified:
  - Increasing gain leads to reduced bandwidth  
  - Lower gain results in wider bandwidth  
- The frequency response shows that **dominant pole behavior** is introduced due to parasitic capacitances, which limits the high-frequency performance.
- All circuits operate in the **saturation region**, ensuring proper amplification and linear operation within the input constraint:
  |V_id| ≤ V_ov  
- Practical gain values are slightly lower than theoretical predictions due to **non-ideal effects**, including:
  - Channel length modulation (finite r_o)  
  - Parasitic capacitances (Cgs, Cgd)  
  - Short-channel effects in 180 nm technology  
- The use of active devices instead of resistors improves integration and increases output resistance, but introduces additional parasitics and design complexity.
- Proper biasing is essential to maintain saturation and stable operation, directly affecting gain and linearity.
- The results validate that **CMOS differential amplifiers exhibit a trade-off between gain, bandwidth, and complexity**, which must be optimized based on application requirements.
- Overall, the experiment confirms practical analog design principles and highlights the impact of device physics and circuit topology on amplifier performance.

## Key Interpretation

- **Circuit 1** is simple but has **low gain and larger area** due to resistors.  
- **Circuit 2** improves efficiency and integration using **active load**, but gain is still moderate.  
- **Circuit 3** provides **highest gain and best performance** due to **bias-controlled operation**, but is more complex.  

Circuit 3 is **best for high gain and precision**, while Circuit 1 is **best for learning/basic design**.
