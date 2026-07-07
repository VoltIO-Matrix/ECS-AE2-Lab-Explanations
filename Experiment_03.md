# Experiment 03 — Easy Notes

# Op-Amp Integrator and Differentiator

These notes explain the practical in a **simple and easy-to-understand way**.

---

## 1) What is this practical about?

This practical is about two op-amp circuits:

1. **Op-amp integrator**
2. **Op-amp differentiator**

They are called mathematical circuits because they behave like math operations.

| Circuit | Mathematical action | Simple meaning |
|---|---|---|
| Integrator | Integration | Finds the area / smooth total change |
| Differentiator | Differentiation | Finds how fast the signal changes |

---

## 2) Very simple idea

### Integrator
An integrator changes a **square wave** into a **triangle wave**.

```text
Input square wave:

     ____      ____
____|    |____|    |____

Output triangle wave:

    /\      /\
   /  \    /  \
__/    \__/    \__
```

### Differentiator
A differentiator changes a **square wave** into **sharp spikes**.

```text
Input square wave:

     ____      ____
____|    |____|    |____

Output spike wave:

    |\      |\
____| \_____| \____
    | /     | /
    |/      |/
```

---

## 3) What is integration in simple words?

Integration means adding up the signal over time.

Easy example:

- If the input is constantly positive, the output slowly increases.
- If the input is constantly negative, the output slowly decreases.

That is why a square wave becomes a triangle wave.

### Why?
A square wave has flat high and low levels.

When the input is high:
- the integrator output ramps in one direction.

When the input is low:
- the output ramps in the opposite direction.

So the output becomes triangular.

---

## 4) What is differentiation in simple words?

Differentiation means measuring how fast the input changes.

A square wave changes suddenly at its edges.

So the differentiator gives:
- a spike when the square wave rises
- another opposite spike when the square wave falls

When the square wave is flat, there is no change, so the output is almost zero.

---

## 5) Main difference between integrator and differentiator

| Feature | Integrator | Differentiator |
|---|---|---|
| Main idea | Adds signal over time | Detects fast change |
| Square wave output | Triangle wave | Spike wave |
| Sine wave output | Negative cosine wave | Positive cosine wave |
| Works better at | Higher frequency region | Lower frequency region |
| Main component position | Capacitor in feedback path | Capacitor in input path |

---

# Part A — Op-Amp Integrator

---

## 6) Integrator circuit idea

In the integrator circuit:

- input resistor is `R_i`
- feedback capacitor is `C_f`
- feedback resistor is `R_f`

The capacitor is in the **feedback path**.

```text
Input -- R_i -- op-amp input
              |
              C_f feedback
              |
            Output
```

---

## 7) Important integrator equation

The practical sheet gives this type of relationship:

`V_o = - (R_f / R_i) × [1 / (1 + jωR_fC_f)] × V_in`

Do not panic. The simple meaning is:

- at low frequency, it behaves more like an inverting amplifier
- at suitable higher frequency, it behaves like an integrator
- at very high frequency, gain becomes very small

---

## 8) Proper integrator equation

For proper integration, the simplified equation is:

`V_o = -1/(R_i C_f) ∫ V_in dt`

### Meaning of each part

| Symbol | Meaning |
|---|---|
| `V_o` | output voltage |
| `V_in` | input voltage |
| `R_i` | input resistor |
| `C_f` | feedback capacitor |
| `∫ V_in dt` | integration of input signal |
| minus sign | output is inverted |

### Simple meaning
The output is the **integral of the input**, but inverted.

---

## 9) Integrator waveform examples

### Square input → triangle output

```text
Input:

     ____      ____
____|    |____|    |____

Output:

    /\      /\
   /  \    /  \
__/    \__/    \__
```

### Sine input → negative cosine output

If input is:

`sin(ωt)`

Output becomes approximately:

`-cos(ωt)`

So the practical asks you to adjust frequency until the output looks like a **negative-going cosine wave**.

---

## 10) Why does square wave become triangle wave?

A square wave has two constant levels:

- positive level
- negative level

The integrator adds these levels over time.

So:

- positive constant input → output slopes upward or downward
- negative constant input → output slopes in the opposite direction

That creates straight-line ramps, making a triangle wave.

---

## 11) Integrator frequency response graph

```text
Gain in dB
 ^
 |\
 | \
 |  \
 |   \
 |    \
 |     \
 +----------------------> log frequency
       integrator region
```

For an ideal integrator:

- when frequency increases, gain decreases
- slope is about `-20 dB/decade`

### Simple meaning
Integrator gives more gain at lower frequencies and less gain at higher frequencies.

But in the practical circuit, it only acts as a good integrator in a selected frequency range.

---

## 12) Condition for proper integration

For proper integration:

`ω R_f C_f >> 1`

Since:

`ω = 2πf`

we can write:

`2πf R_f C_f >> 1`

### Simple meaning
The input frequency must be high enough compared with the cutoff frequency.

So:

`f >> 1 / (2π R_f C_f)`

This means the circuit behaves properly as an integrator when the frequency is sufficiently above its lower cutoff frequency.

---

## 13) Integrator cutoff frequency

`f_c = 1 / (2πR_fC_f)`

In the practical integrator circuit:

- `R_f = 100 kΩ`
- `C_f = 0.01 µF`, `0.047 µF`, or `0.1 µF`

### For `C_f = 0.01 µF`

`f_c = 1 / (2π × 100kΩ × 0.01µF)`

`f_c ≈ 159 Hz`

### For `C_f = 0.047 µF`

`f_c ≈ 33.9 Hz`

### For `C_f = 0.1 µF`

`f_c ≈ 15.9 Hz`

### What happens when capacitor increases?

When `C_f` increases:

- cutoff frequency decreases
- integration can happen at lower frequencies
- output triangle amplitude usually changes

---

# Part B — Op-Amp Differentiator

---

## 14) Differentiator circuit idea

In the differentiator circuit:

- input capacitor is `C_i`
- feedback resistor is `R_f`
- small input resistor `R_i` is used for stability
- feedback capacitor `C_f` is used to reduce noise and high-frequency problems

The capacitor is mainly in the **input path**.

```text
Input -- C_i -- op-amp input
              |
              R_f feedback
              |
            Output
```

---

## 15) Proper differentiator equation

For a simple differentiator:

`V_o = -R_f C_i × dV_in/dt`

### Meaning of each part

| Symbol | Meaning |
|---|---|
| `V_o` | output voltage |
| `R_f` | feedback resistor |
| `C_i` | input capacitor |
| `dV_in/dt` | rate of change of input |
| minus sign | output is inverted |

### Simple meaning
The output depends on **how fast the input changes**.

If the input changes quickly, output is large.
If the input is flat, output is nearly zero.

---

## 16) Differentiator waveform examples

### Square input → spike output

```text
Input:

     ____      ____
____|    |____|    |____

Output:

    +        +
    |        |
____|________|________
    |        |
    -        -
```

### Triangle input → square output

```text
Input triangle:

    /\      /\
   /  \    /  \
__/    \__/    \__

Output square:

____      ____
    |____|    |____
```

### Sine input → cosine output

If input is:

`sin(ωt)`

Output becomes approximately:

`cos(ωt)`

In this practical, the differentiator output for sine input is expected to be a **positive-going cosine wave**.

---

## 17) Why square wave gives spikes

A square wave has sudden changes at its edges.

The differentiator responds strongly only when the input changes.

So:

- rising edge → one spike
- falling edge → opposite spike
- flat part → almost zero output

That is why the output is a spike waveform.

---

## 18) Differentiator frequency response graph

```text
Gain in dB
 ^
 |      /
 |     /
 |    /
 |   /
 |  /
 | /
 +----------------------> log frequency
    differentiator region
```

For an ideal differentiator:

- when frequency increases, gain increases
- slope is about `+20 dB/decade`

But practical differentiators limit high-frequency gain to avoid noise.

---

## 19) Practical differentiator full equation

The sheet gives:

`V_o = - [jωC_iR_f / ((1 + jωC_iR_i)(1 + jωC_fR_f))] V_in`

### Simple meaning
This equation shows the practical differentiator has limits.

It differentiates only in a useful frequency range.

- `C_i` and `R_i` affect the lower side
- `C_f` and `R_f` affect the higher side
- very high frequencies are reduced to prevent noise

---

## 20) Conditions for proper differentiation

For proper differentiation, the input frequency should be in the correct region:

`R_f C_i >> R_i C_f`

and the frequency should satisfy approximately:

`1/(R_f C_i) << ω << 1/(R_i C_f)`

### In frequency form

`1/(2πR_fC_i) << f << 1/(2πR_iC_f)`

### Simple meaning
The frequency must be:

- high enough to make differentiation happen
- but not too high, otherwise noise and op-amp limitations affect the output

---

# 21) Combined frequency response from the practical

The practical shows this idea:

```text
Gain dB
 ^
 |          /\
 |         /  \
 |        /    \
 |_______/      \_______> log f
     Diff   Inv   Int
```

### Meaning
At different frequency ranges, the same circuit style may behave like:

1. **Differentiator** at lower region
2. **Inverting amplifier** in middle region
3. **Integrator** at higher region

This is why frequency selection is very important.

---

# 22) Procedure summary

## Part A — Integrator

1. Build the integrator circuit.
2. Apply a square wave input.
3. Set input amplitude to `1 Vpp`.
4. Start around `1 kHz`.
5. Adjust frequency until output becomes a good triangle wave.
6. Repeat for different `C_f` values:
   - `0.01 µF`
   - `0.047 µF`
   - `0.1 µF`
7. Then apply sine wave input.
8. Adjust frequency until output becomes negative-going cosine.
9. Record output type, amplitude, and frequency.

---

## Part B — Differentiator

1. Build the differentiator circuit.
2. Apply a square wave input.
3. Set input amplitude to `1 Vpp`.
4. Start around `1 kHz`.
5. Adjust frequency until output becomes good spikes.
6. Repeat for different `C_i` values:
   - `0.1 µF`
   - `0.01 µF`
   - `0.047 µF`
7. Then apply sine wave input.
8. Adjust frequency until output becomes positive-going cosine.
9. Record output type, amplitude, and frequency.

---

# 23) How to understand the data tables

You mainly record:

- input waveform type
- input amplitude
- input frequency
- output waveform type
- output amplitude
- output frequency

### Important point
The output frequency should usually be the **same as input frequency**.

Only the waveform shape and amplitude change.

Example:

| Input | Circuit | Output |
|---|---|---|
| Square wave | Integrator | Triangle wave |
| Sine wave | Integrator | Negative cosine wave |
| Square wave | Differentiator | Spike wave |
| Triangle wave | Differentiator | Square wave |
| Sine wave | Differentiator | Positive cosine wave |

---

# 24) Discussion answers

---

## Q1) For proper integration, what must the relationship be between `R_fC_f` and input frequency?

For proper integration:

`ωR_fC_f >> 1`

or:

`f >> 1/(2πR_fC_f)`

### Simple answer
The input frequency must be much greater than the cutoff frequency decided by `R_fC_f`.

---

## Q2) What characteristic is common to both the integrator and amplifier?

Both circuits use an op-amp with **negative feedback** and both can invert the signal.

So both can produce an output that is **180° out of phase** with the input.

---

## Q3) Relationship between triangle amplitude and square wave amplitude/frequency

For an integrator with square wave input:

- if square wave amplitude increases, triangle amplitude increases
- if frequency increases, triangle amplitude decreases

### Simple rule
Triangle output amplitude is directly proportional to input amplitude and inversely proportional to frequency.

```text
Higher input amplitude -> bigger triangle
Higher frequency       -> smaller triangle
```

---

## Q4) What parameter is important when selecting an op-amp for an integrator?

Important parameters are:

- input offset voltage
- bias current
- slew rate
- bandwidth / gain-bandwidth product
- low drift

### Simple answer
Choose an op-amp with low offset, low bias current, and enough bandwidth.

---

## Q5) If input to an integrator is a pulse waveform with 20% duty cycle, what is the output?

The output will be a ramp waveform, but it will not be symmetrical.

Because the input is high only for 20% of the time and low for 80% of the time.

### Simple answer
Output becomes an **unequal triangular/ramp waveform**.

```text
Input pulse 20% duty:

   __        __
__|  |______|  |______

Output ramp idea:

  /\____    /\____
 /     \   /     \
/       \_/       \_
```

The charging and discharging times are different.

---

## Q6) For proper differentiation, what must be the relationship between `R_fC_i` and `R_iC_f`?

For proper practical differentiation:

`R_fC_i >> R_iC_f`

and the frequency should be between the lower and upper limits:

`1/(2πR_fC_i) << f << 1/(2πR_iC_f)`

### Simple answer
The differentiator must operate in the middle useful range, not too low and not too high.

---

## Q7) If input to a differentiator is a triangle wave, what is the output?

A triangle wave has straight rising and falling slopes.

The derivative of a constant slope is a constant value.

So output becomes a square wave.

### Final answer
Triangle input → square wave output.

---

## Q8) What parameter is important when selecting an op-amp for differentiator application?

Important parameters are:

- high slew rate
- sufficient bandwidth
- low noise
- stable operation at high frequency
- good gain-bandwidth product

### Simple answer
Choose an op-amp with high slew rate, enough bandwidth, and low noise.

---

# 25) Very short viva answers

### What is an integrator?
A circuit whose output is proportional to the integral of the input.

### What is a differentiator?
A circuit whose output is proportional to the rate of change of the input.

### What is the output of an integrator for square input?
Triangle wave.

### What is the output of a differentiator for square input?
Spike waveform.

### What is the output of an integrator for sine input?
Negative cosine wave.

### What is the output of a differentiator for sine input?
Positive cosine wave.

### Why is there a feedback resistor in practical integrator?
To prevent saturation at very low frequencies and DC.

### Why is there a feedback capacitor in practical differentiator?
To reduce high-frequency noise and improve stability.

---

# 26) Final simple conclusion

This experiment shows how op-amps can perform mathematical operations. The integrator produces an output related to the area under the input waveform, so a square wave becomes a triangle wave. The differentiator produces an output related to the rate of change of the input, so a square wave becomes spikes. Correct resistor and capacitor values are important because both circuits work properly only within a certain frequency range.

---

# 27) Super short memory note

```text
Integrator:
Square -> Triangle
Sine   -> -Cosine

Differentiator:
Square   -> Spikes
Triangle -> Square
Sine     -> Cosine
```

```text
Integrator = area / adding over time
Differentiator = rate of change / sudden change detector
```
