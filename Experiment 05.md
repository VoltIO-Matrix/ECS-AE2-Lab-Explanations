# Experiment 05 — Active Filters

## Clear and easy explanation

This practical is about **active filters** using a 741 op-amp.

You study three filter types:

1. **Low-pass filter**
2. **High-pass filter**
3. **Band-pass filter**

The practical asks you to measure output voltage at different frequencies, calculate gain in dB, draw Bode plots, and find cutoff frequencies and bandwidth.

---

# 1) What is a filter?

A filter is a circuit that allows some frequencies to pass and reduces other frequencies.

Simple idea:

```text
Filter = frequency selector
```

It does not treat all frequencies equally.

Some frequencies pass easily. Some frequencies are attenuated.

---

# 2) What is an active filter?

An **active filter** uses an active component such as an op-amp.

In this experiment, the active component is the **741 op-amp**.

Active filters can:

- filter frequencies
- provide voltage gain
- use resistors and capacitors without inductors
- give better signal strength than passive filters

---

# 3) Active filter vs passive filter

| Feature | Passive filter | Active filter |
|---|---|---|
| Components | R, C, L only | R, C + op-amp |
| Gain | usually no gain | can have gain |
| Power supply | not needed | needed |
| Loading effect | more | less |
| Inductors | sometimes needed | usually not needed |

---

# 4) Low-pass filter

A low-pass filter allows **low frequencies** to pass and reduces **high frequencies**.

```text
Low frequency  → pass
High frequency → block/reduce
```

### Shape of response

```text
Gain
 ^
 |───────────────
 |               \
 |                \
 |                 \
 +----------------------> frequency
                 fc
```

The important frequency is the **cutoff frequency** `f_c`.

Below `f_c`, signal passes.
Above `f_c`, signal reduces.

---

# 5) High-pass filter

A high-pass filter allows **high frequencies** to pass and reduces **low frequencies**.

```text
Low frequency  → block/reduce
High frequency → pass
```

### Shape of response

```text
Gain
 ^
 |                 ─────────────
 |                /
 |               /
 |______________/
 +----------------------> frequency
               fc
```

Below `f_c`, signal is attenuated.
Above `f_c`, signal passes.

---

# 6) Band-pass filter

A band-pass filter allows only a **middle range** of frequencies to pass.

It blocks/reduces:

- very low frequencies
- very high frequencies

```text
Low frequencies   → reduced
Middle frequencies → pass
High frequencies  → reduced
```

### Shape of response

```text
Gain
 ^
 |          ┌──────────┐
 |         /            \
 |        /              \
 |_______/                \_______
 +---------------------------------> frequency
        fL      passband      fH
```

The passband is between:

- lower cutoff frequency `f_L`
- higher cutoff frequency `f_H`

Bandwidth is:

```text
Bandwidth = f_H - f_L
```

---

# 7) Important terms

## Passband
The frequency range where the filter allows the signal to pass with little attenuation.

## Stopband
The frequency range where the filter strongly reduces the signal.

## Cutoff frequency
The frequency where the gain falls by **3 dB** from the passband value.

At cutoff:

```text
Output ≈ 0.707 × passband output
```

## Bode plot
A graph of gain in dB versus frequency on a logarithmic frequency axis.

---

# 8) Main equations

## Cutoff frequency

```text
f_c = 1 / (2πRC)
```

where:

- `R` = filter resistor
- `C` = filter capacitor

This equation is used for both first-order low-pass and high-pass filters.

---

## Voltage gain

The practical uses a non-inverting op-amp amplifier.

Gain:

```text
A_v = 1 + R_f/R_1
```

Gain in dB:

```text
A_v(dB) = 20 log10(1 + R_f/R_1)
```

In Figure 2:

- `R_f = 10 kΩ`
- `R_1 = 10 kΩ`

So:

```text
A_v = 1 + 10k/10k = 2
```

```text
A_v(dB) = 20 log10(2) ≈ 6.02 dB
```

So the passband gain is about **2 times** or **6 dB**.

---

# 9) Low-pass filter in Figure 2

Figure 2 is a first-order active low-pass filter.

The RC network is connected to the non-inverting input of the op-amp.

Given:

- `R = 3.3 kΩ`
- `C = 0.047 µF`

Cutoff frequency:

```text
f_c = 1 / (2πRC)
```

Convert:

```text
R = 3300 Ω
C = 0.047 µF = 0.047 × 10^-6 F
```

Then:

```text
f_c = 1 / (2π × 3300 × 0.047 × 10^-6)
f_c ≈ 1026 Hz
```

So:

```text
f_c ≈ 1.03 kHz
```

### Meaning

The low-pass filter passes frequencies below about **1 kHz** and attenuates frequencies above about **1 kHz**.

---

# 10) High-pass filter

To make the high-pass filter, the practical says to interchange `R` and `C` in Figure 2.

So the same values are used:

- `R = 3.3 kΩ`
- `C = 0.047 µF`

The cutoff frequency is still:

```text
f_c ≈ 1.03 kHz
```

But the behavior changes:

- below 1 kHz → attenuated
- above 1 kHz → passed

---

# 11) Band-pass filter in Figure 3

The band-pass filter is made by combining:

1. a high-pass section at the input
2. an amplifier section
3. a low-pass section at the output

So only a selected middle range of frequencies passes.

The practical asks you to design it for approximately:

```text
lower cutoff ≈ 1 kHz
upper cutoff ≈ 10 kHz
```

So the passband is roughly:

```text
1 kHz to 10 kHz
```

Bandwidth:

```text
Bandwidth = f_H - f_L
Bandwidth = 10 kHz - 1 kHz
Bandwidth = 9 kHz
```

---

# 12) Choosing components for band-pass filter

Use:

```text
f_c = 1 / (2πRC)
```

The provided capacitors include:

- `0.047 µF`
- `4.7 nF`

The provided resistors include:

- `3.3 kΩ`
- `10 kΩ`

### Lower cutoff around 1 kHz

Using:

```text
R = 3.3 kΩ
C = 0.047 µF
```

gives:

```text
f_L ≈ 1.03 kHz
```

### Upper cutoff around 10 kHz

Using:

```text
R = 3.3 kΩ
C = 4.7 nF
```

gives:

```text
f_H = 1 / (2π × 3300 × 4.7 × 10^-9)
f_H ≈ 10.26 kHz
```

So those values are suitable for about 1 kHz to 10 kHz band-pass operation.

---

# 13) How to do the experiment

## Low-pass filter

1. Connect Figure 2.
2. Set input to `1 Vpp` sine wave at `100 Hz`.
3. Vary frequency from `100 Hz` to `10 kHz`.
4. Measure output voltage.
5. Calculate gain in dB.
6. Draw Bode plot.
7. Find cutoff frequency from the plot.

## High-pass filter

1. Interchange resistor and capacitor in Figure 2.
2. Repeat the same measurements.
3. Draw Bode plot.
4. Find cutoff frequency.

## Band-pass filter

1. Construct Figure 3.
2. Choose values for about `1 kHz` lower cutoff and `10 kHz` upper cutoff.
3. Vary frequency from `100 Hz` to `100 kHz`.
4. Measure output voltage.
5. Calculate gain in dB.
6. Draw Bode plot.
7. Find `f_L`, `f_H`, and bandwidth.

---

# 14) How to calculate gain in dB

First calculate ordinary voltage gain:

```text
A_v = V_out / V_in
```

Then convert to dB:

```text
Gain(dB) = 20 log10(A_v)
```

### Example

If:

```text
V_in = 1 Vpp
V_out = 2 Vpp
```

Then:

```text
A_v = 2 / 1 = 2
Gain(dB) = 20 log10(2) ≈ 6.02 dB
```

---

# 15) How to identify cutoff from Bode plot

1. Find the passband gain.
2. Subtract 3 dB.
3. Find the frequency where the graph reaches that level.

Example:

If passband gain is `6 dB`, then cutoff level is:

```text
6 dB - 3 dB = 3 dB
```

So the cutoff frequency is where gain becomes **3 dB**.

---

# 16) Discussion answers

## Q1) Discuss the differences between the three Bode plots.

### Low-pass filter

- gain is high at low frequencies
- gain decreases after cutoff frequency
- high frequencies are attenuated

### High-pass filter

- gain is low at low frequencies
- gain increases and becomes flat after cutoff
- low frequencies are attenuated

### Band-pass filter

- low frequencies are attenuated
- middle frequencies pass
- high frequencies are attenuated
- it has two cutoff frequencies: `f_L` and `f_H`

---

## Q2) How do theoretical cutoff frequencies compare with experimental values? If they differ by more than 10%, explain reasons.

The theoretical and experimental values should be close, but they may not be exactly equal.

Reasons for difference:

- resistor tolerance
- capacitor tolerance
- 741 op-amp limitations
- breadboard parasitic capacitance
- oscilloscope reading error
- signal generator frequency/amplitude error
- loading effect
- wires and contact resistance

If the difference is more than 10%, the most likely reasons are component tolerances and measurement errors.

---

# 17) Final conclusion

This experiment shows how active filters can select frequency ranges using resistors, capacitors, and an op-amp. A low-pass filter passes low frequencies, a high-pass filter passes high frequencies, and a band-pass filter passes only a selected middle range. The cutoff frequency is calculated using `f_c = 1/(2πRC)`, and the gain is calculated in dB using `20 log10(V_out/V_in)`. The Bode plot is used to find the cutoff frequencies and bandwidth experimentally.

---

# 18) Super short memory note

```text
Low-pass  = low frequencies pass
High-pass = high frequencies pass
Band-pass = middle band passes
```

```text
fc = 1/(2πRC)
Gain(dB) = 20 log10(Vout/Vin)
Bandwidth = fH - fL
```
