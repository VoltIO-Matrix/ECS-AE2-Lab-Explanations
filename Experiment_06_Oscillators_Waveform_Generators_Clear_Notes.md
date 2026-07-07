# Experiment 06 — Oscillators and Waveform Generators

## Clear and easy explanation

This practical has two main parts:

1. **Wien-bridge oscillator** — generates a sine wave.
2. **Square-wave, triangular-wave and sawtooth-wave generator** — generates non-sinusoidal waveforms.

---

# 1) What is an oscillator?

An oscillator is a circuit that produces a repeating waveform **without needing an external input signal**.

Simple idea:

```text
DC power supply → oscillator circuit → AC waveform output
```

The oscillator uses DC power and feedback to create a continuous waveform.

Common oscillator outputs:

- sine wave
- square wave
- triangular wave
- sawtooth wave
- pulse waveform

---

# 2) Basic idea of oscillation

For a circuit to oscillate, it must satisfy the **Barkhausen condition**:

```text
Loop gain = 1
Total phase shift = 0° or 360°
```

Simple meaning:

- the feedback signal must return in the correct phase
- the gain must be enough to keep the oscillation going

If gain is too small:

```text
oscillation dies
```

If gain is too large:

```text
output clips/distorts
```

If gain is correct:

```text
stable sine wave or waveform is produced
```

---

# Part A — Wien-Bridge Oscillator

---

# 3) What is a Wien-bridge oscillator?

A Wien-bridge oscillator is an op-amp oscillator that produces a **sine wave**.

It uses an RC bridge network to decide the oscillation frequency.

In this practical, the Wien-bridge oscillator uses:

- 741 op-amp
- resistors
- capacitors
- feedback network
- Zener diodes for amplitude control

---

# 4) Frequency of Wien-bridge oscillator

The practical sheet gives:

```text
fo = 1 / [2π√(R1R2C1C2)]
```

If:

```text
R1 = R2 = R
C1 = C2 = C
```

then the equation becomes:

```text
fo = 1 / (2πRC)
```

So the frequency depends on the RC combination.

---

# 5) What happens when R or C changes?

From:

```text
fo = 1 / (2πRC)
```

If `R` increases:

```text
frequency decreases
```

If `C` increases:

```text
frequency decreases
```

If `R` decreases:

```text
frequency increases
```

If `C` decreases:

```text
frequency increases
```

So:

```text
Large RC → low frequency
Small RC → high frequency
```

---

# 6) Theoretical frequency calculations

## Case 1: R = 10 kΩ, C = 0.047 µF

```text
R = 10,000 Ω
C = 0.047 × 10^-6 F

fo = 1 / (2πRC)
fo ≈ 338.6 Hz
```

So:

```text
fo ≈ 339 Hz
```

---

## Case 2: R = 10 kΩ, C = 0.01 µF

```text
fo = 1 / (2π × 10000 × 0.01 × 10^-6)
fo ≈ 1591.5 Hz
```

So:

```text
fo ≈ 1.59 kHz
```

---

## Case 3: R = 3.3 kΩ, C = 0.047 µF

```text
fo = 1 / (2π × 3300 × 0.047 × 10^-6)
fo ≈ 1026 Hz
```

So:

```text
fo ≈ 1.03 kHz
```

---

# 7) Why do we adjust Rf?

In the Wien-bridge oscillator, the op-amp gain must be enough to start and maintain oscillation.

The practical says to set `Rf` around 20 kΩ and increase it if oscillation does not start.

Simple meaning:

- `Rf` controls amplifier gain
- if gain is too low, oscillation will not start
- if gain is high enough, oscillation begins
- if gain is too high, output may distort

---

# 8) Why use Zener diodes D1 and D2?

The Zener diodes limit the output amplitude.

Without Zeners:

- output amplitude can become large
- waveform may clip or distort

With Zeners:

- output is limited
- amplitude becomes more stable
- circuit is protected from excessive output swing

So Zeners act like an **amplitude stabilizer**.

---

# Part B — Square, triangular and sawtooth wave generator

---

# 9) Figure 3 circuit idea

Figure 3 uses two op-amps:

## Op-amp A1
Works like a **Schmitt trigger / comparator**.

Its output is a square wave.

## Op-amp A2
Works like an **integrator**.

It converts the square wave into a triangular wave.

So:

```text
A1 output → square wave
A2 output → triangular wave
```

---

# 10) How square wave becomes triangular wave

The output of A1 is a square wave.

That square wave goes through resistor `R1` into the integrator capacitor `C1` around A2.

An integrator adds the input over time.

So:

```text
constant positive square level → ramp in one direction
constant negative square level → ramp in opposite direction
```

Therefore:

```text
square wave → triangular wave
```

---

# 11) Feedback between A1 and A2

The triangular output from A2 is fed back to A1.

A1 compares the triangular waveform with threshold levels.

When the triangle reaches an upper threshold, A1 switches.

When the triangle reaches a lower threshold, A1 switches back.

This continuous switching creates oscillation.

---

# 12) Role of R2 and R3

In the procedure:

```text
R3 = 4R2
```

Examples:

```text
R2 = 10 kΩ, R3 = 40 kΩ
R2 = 4.7 kΩ, R3 = 18.8 kΩ
```

These resistors set the threshold levels of A1.

Changing them changes the waveform amplitude and frequency.

---

# 13) Sawtooth waveform generation

The practical later changes the non-inverting terminal voltage of A2 to:

```text
-5 V, -10 V, +5 V, +10 V
```

This changes the charging/discharging balance of the integrator.

If the capacitor charges and discharges at different rates, the triangle becomes a **sawtooth** waveform.

Simple idea:

```text
equal rise and fall slopes → triangle wave
unequal rise and fall slopes → sawtooth wave
```

---

# 14) Waveform summary

| Circuit section | Output waveform | Reason |
|---|---|---|
| Wien bridge oscillator | Sine wave | RC bridge selects sinusoidal frequency |
| A1 in Figure 3 | Square wave | comparator switches high/low |
| A2 in Figure 3 | Triangular wave | integrator ramps up/down |
| Biased A2 condition | Sawtooth wave | unequal charging/discharging slopes |

---

# 15) Discussion answers

## Q1) How does the RC combination affect the frequency of the Wien-bridge oscillator?

The frequency is:

```text
fo = 1 / (2πRC)
```

So frequency is inversely proportional to `RC`.

- larger R or C gives lower frequency
- smaller R or C gives higher frequency

---

## Q2) Difference in output amplitude with and without Zeners in Wien-bridge oscillator

Without Zeners:

- output amplitude may become large
- waveform may distort or clip
- amplitude is less controlled

With Zeners:

- amplitude is limited
- output is more stable
- distortion due to excessive amplitude is reduced

So the output amplitude with Zeners is usually more controlled and limited.

---

## Q3) Features and applications of Figure 3 circuit

Features:

- produces square and triangular waves at the same time
- can be adjusted by changing resistor values
- can produce sawtooth waveform when bias is added
- uses two op-amps: comparator + integrator

Applications:

- function generators
- testing circuits
- timing circuits
- pulse generation
- waveform generation for labs
- sweep circuits

---

# 16) Final conclusion

This experiment shows how op-amp circuits can generate waveforms. The Wien-bridge oscillator generates a sine wave, and its frequency depends on the RC network. Zener diodes help control the output amplitude. The waveform generator circuit uses one op-amp as a comparator to produce a square wave and another op-amp as an integrator to produce a triangular wave. By changing bias conditions, the triangular wave can be changed into a sawtooth waveform.

---

# 17) Super short memory note

```text
Wien bridge oscillator → sine wave
Comparator A1 → square wave
Integrator A2 → triangle wave
Biased integrator → sawtooth wave
```

```text
fo = 1/(2πRC)
Large RC → low frequency
Small RC → high frequency
```
