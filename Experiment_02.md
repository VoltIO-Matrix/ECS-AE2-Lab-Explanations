# Experiment 02 — Easy Short Notes

## Topic
**Frequency Response of an AC Inverting Amplifier**

---

## 1) What is this practical about?

This practical checks **how amplifier gain changes when frequency changes**.

In simple words:
- at **low frequency** → gain is small
- at **middle frequency** → gain is almost constant and best
- at **high frequency** → gain drops again

So we study the **frequency response** of the amplifier.

---

## 2) Main idea in one line

**The amplifier does not amplify all frequencies equally.**

---

## 3) Why do we use the capacitor?

The input capacitor `C_i` is used to:
- block **DC**
- allow **AC**
- create the **low-frequency cutoff**

### Very simple idea
The capacitor does **not** suddenly cut everything.
It reduces low frequencies **gradually**.

So:
- very low frequency → strongly reduced
- a little higher frequency → less reduced
- high enough frequency → passes properly

That is why we still measure gain in that region.

---

## 4) Super easy graph idea

```text
Gain
 ^
 |                    _____________
 |                   /             \
 |                  /               \
 |                 /                 \
 |________________/                   \__________> Frequency
              low-cutoff            high-cutoff
```

### Meaning of the graph
- **Left side**: low frequency region → capacitor effect → gain is small
- **Middle flat part**: normal amplifier region → gain is maximum and stable
- **Right side**: high frequency region → op-amp limitation → gain falls

---

## 5) Why do we check gain in the low-frequency region?

Because the capacitor is **not an ON/OFF switch**.

It does not say:
- below this frequency = zero
- above this frequency = full gain

Instead it says:
- lower frequency = lower gain
- higher frequency = higher gain

So we measure that region to find:
- where gain starts becoming normal
- the **low-cutoff frequency**
- the **bandwidth**

---

## 6) Inverting amplifier gain

For normal operating frequencies:

`A_v = -R_f / R_i`

From the circuit:
- `R_f = 470 kΩ`
- `R_i = 10 kΩ`

So:

`A_v = -470/10 = -47`

### Meaning
- magnitude of gain = **47**
- minus sign means output is **inverted**

---

## 7) Gain in dB

`Gain(dB) = 20 log10(A_v)`

If gain = 47:

`Gain(dB) = 20 log10(47) ≈ 33.4 dB`

So the middle flat region is about **33.4 dB**.

---

## 8) What is cutoff frequency?

Cutoff frequency is the point where gain becomes:

- **0.707 × maximum gain**
- or **3 dB below maximum gain**

If midband gain is `33.4 dB`, then cutoff level is:

`33.4 - 3 = 30.4 dB`

So on the graph, find where the gain becomes **30.4 dB**.

- left point → `f_L`
- right point → `f_H`

---

## 9) Bandwidth

`Bandwidth = f_H - f_L`

where:
- `f_L` = low-cutoff frequency
- `f_H` = high-cutoff frequency

---

## 10) Why low-frequency gain becomes small

Capacitor reactance is:

`X_C = 1 / (2πfC)`

When frequency `f` is small:
- `X_C` becomes big
- capacitor opposes the signal more
- less signal enters the amplifier
- output becomes smaller
- gain becomes smaller

When frequency increases:
- `X_C` becomes smaller
- signal passes more easily
- gain rises to normal value

---

## 11) Easy capacitor graph

```text
Capacitor opposition (Xc)
 ^
 |\
 | \
 |  \
 |   \
 |    \
 |     \
 |      \
 +------------------------------> Frequency
      low f               high f
```

### Meaning
- at low frequency → capacitor opposition is high
- at high frequency → capacitor opposition is low

That is why low-frequency gain is low.

---

## 12) Dual supply vs single supply

## Figure 3 — Dual supply
Uses:
- `+15 V`
- `-15 V`

### Good side
- easier signal handling
- output can go positive and negative easily
- simpler circuit idea

---

## Figure 4 — Single supply
Uses one main supply, so it needs:
- resistor divider for bias
- output capacitor `C_o`

### Why?
Because the op-amp needs a DC midpoint to work properly with one supply.

### Good side
- simpler power source
- useful in battery circuits

### Bad side
- needs more biasing parts
- more chance of distortion if bias is not correct

---

## 13) Gain-bandwidth product

`GBP = Gain × Bandwidth ≈ constant`

For a 741 op-amp, usually:

`GBP ≈ 1 MHz`

### Simple meaning
If gain increases, bandwidth decreases.
If gain decreases, bandwidth increases.

---

## 14) Important theoretical values

### Midband gain
`A_v = 47`

### Midband gain in dB
`≈ 33.4 dB`

### Low cutoff (approx.)
Using `C_i = 0.01 µF` and `R_i = 10 kΩ`:

`f_L ≈ 1 / (2πRC)`

`f_L ≈ 1.59 kHz`

### High cutoff (approx.)
Using `GBP ≈ 1 MHz`:

`f_H ≈ 1,000,000 / 47 ≈ 21.3 kHz`

### Bandwidth
`BW ≈ 21.3 kHz - 1.59 kHz ≈ 19.7 kHz`

---

## 15) How to fill the table

Measure:
- input voltage `V_in`
- output voltage `V_o`

Then calculate:

`A_v = V_o / V_in`

`Gain(dB) = 20 log10(A_v)`

### Example
If:
- `V_in = 0.1 V`
- `V_o = 4.7 V`

Then:
- `A_v = 4.7 / 0.1 = 47`
- `Gain(dB) ≈ 33.4 dB`

---

## 16) Very short discussion answers

### 1. What is frequency response?
It is how gain changes with frequency.

### 2. What is bandwidth?
It is the useful frequency range of the amplifier.

### 3. Why use the input capacitor?
To block DC, pass AC, and set the low cutoff frequency.

### 4. Why does gain fall at high frequency?
Because the 741 op-amp has limited bandwidth.

### 5. Why is the output inverted?
Because this is an inverting amplifier.

---

## 17) Answers to the practical questions

### Q1) Theoretical bandwidth?
Approximate values:
- `f_L ≈ 1.59 kHz`
- `f_H ≈ 21.3 kHz`
- `BW ≈ 19.7 kHz`

Measured values may be a little different due to real component errors and op-amp non-ideal behavior.

### Q2) If `C_i = 0.1 µF`, what is the new low cutoff?
It becomes about:

`f_L ≈ 159 Hz`

So bigger capacitor → lower cutoff frequency.

### Q3) What determines high cutoff frequency?
Mainly the op-amp **gain-bandwidth product**.

### Q4) For `f_H = 50 kHz`, what should the gain be?
Using `GBP ≈ 1 MHz`:

`Gain = 1,000,000 / 50,000 = 20`

### Q5) Advantages and disadvantages of single-supply amplifier?
**Advantages:** simple supply, useful for battery circuits.

**Disadvantages:** needs biasing, coupling capacitors, and can distort more easily.

---

## 18) Best simple conclusion

This practical shows that an AC inverting amplifier has a useful frequency range. At low frequencies the capacitor reduces the gain, at middle frequencies the gain stays almost constant, and at high frequencies the gain drops because of the 741 op-amp limitation. From the graph we can find the low cutoff, high cutoff, and bandwidth.

---

## 19) Final super short memory note

```text
Low frequency  -> capacitor reduces gain
Middle region  -> gain is constant
High frequency -> op-amp reduces gain
```

```text
Need to find:
fL, fH, Bandwidth, Gain(dB)
```
