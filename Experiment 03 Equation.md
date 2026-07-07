# Experiment 03 — Step-by-Step Equation Derivations

# Op-Amp Integrator and Differentiator

This file explains and derives the main equations in **Experiment 03** in a simple step-by-step way.

---

## 0) Important basic op-amp ideas

Before deriving the equations, remember these two ideal op-amp rules.

### Rule 1: Input current is almost zero

An ideal op-amp does not take current into its input terminals.

So:

`I_+ ≈ 0`

`I_- ≈ 0`

### Rule 2: Virtual ground

In these circuits, the non-inverting terminal `+` is connected to ground.

Because of negative feedback:

`V_- ≈ V_+`

Since:

`V_+ = 0 V`

Then:

`V_- ≈ 0 V`

So the inverting terminal behaves like ground, even though it is not physically connected to ground.

This point is called **virtual ground**.

---

## 1) Useful component equations

## 1.1 Resistor current equation

For a resistor:

`I = V / R`

If input voltage is `V_in` and the inverting input is at virtual ground:

`I_R = (V_in - 0) / R`

So:

`I_R = V_in / R`

---

## 1.2 Capacitor current equation

For a capacitor:

`I_C = C × dV/dt`

This means capacitor current depends on how fast voltage changes.

For AC sinusoidal analysis, capacitor impedance is:

`Z_C = 1 / (jωC)`

where:

- `j = √(-1)`
- `ω = 2πf`
- `f` = frequency in Hz
- `C` = capacitance

---

# Part A — Op-Amp Integrator

---

## 2) Ideal inverting integrator circuit

In a basic integrator:

- input resistor = `R_i`
- feedback capacitor = `C_f`
- input voltage = `V_in`
- output voltage = `V_o`

Simple circuit idea:

```text
V_in ---- R_i ----●---- op-amp - input
                  |
                  | virtual ground
                  |
              C_f feedback
                  |
                 V_o
```

---

## 3) Deriving the ideal integrator equation

### Step 1: Current through input resistor

Because the inverting input is virtual ground:

`V_- ≈ 0`

So current through `R_i` is:

`I_i = (V_in - V_-) / R_i`

Since `V_- = 0`:

`I_i = V_in / R_i`

---

### Step 2: Same current flows through feedback capacitor

The op-amp input takes almost no current.

So the input resistor current must flow through the feedback capacitor.

Therefore:

`I_i = I_C`

---

### Step 3: Capacitor voltage

The feedback capacitor is connected between the virtual ground node and output.

Voltage across capacitor is:

`V_C = V_- - V_o`

Since `V_- = 0`:

`V_C = 0 - V_o`

So:

`V_C = -V_o`

---

### Step 4: Current through capacitor

Capacitor current is:

`I_C = C_f × dV_C/dt`

Substitute `V_C = -V_o`:

`I_C = C_f × d(-V_o)/dt`

So:

`I_C = -C_f × dV_o/dt`

---

### Step 5: Equate currents

We know:

`I_i = I_C`

So:

`V_in / R_i = -C_f × dV_o/dt`

Rearrange:

`dV_o/dt = - V_in / (R_i C_f)`

---

### Step 6: Integrate both sides

`dV_o/dt = - V_in / (R_i C_f)`

Integrating:

`V_o = -1/(R_i C_f) ∫ V_in dt`

### Final ideal integrator equation

`V_o = -1/(R_i C_f) ∫ V_in dt`

---

## 4) Meaning of the ideal integrator equation

`V_o = -1/(R_i C_f) ∫ V_in dt`

### Simple meaning
The output is proportional to the **area under the input waveform**.

The minus sign means the output is inverted.

### Component effect

- If `R_i` increases, output amplitude decreases.
- If `C_f` increases, output amplitude decreases.
- If input amplitude increases, output amplitude increases.

---

## 5) Deriving square wave to triangle wave

Suppose the input is a constant positive voltage for half cycle.

Let:

`V_in = +V_p`

From integrator equation:

`dV_o/dt = - V_in / (R_i C_f)`

Substitute:

`dV_o/dt = - V_p / (R_i C_f)`

This is a constant negative slope.

So output becomes a straight falling line.

When input becomes negative:

`V_in = -V_p`

Then:

`dV_o/dt = -(-V_p)/(R_i C_f)`

`dV_o/dt = +V_p/(R_i C_f)`

This is a constant positive slope.

So output becomes a straight rising line.

### Therefore

```text
Square wave input -> triangle wave output
```

```text
Input square:

     ____      ____
____|    |____|    |____

Output triangle:

    /\      /\
   /  \    /  \
__/    \__/    \__
```

---

## 6) Triangle wave amplitude relation

For a square wave with peak value `V_p` and frequency `f`:

Time for half cycle is:

`T/2 = 1/(2f)`

Slope magnitude of output is:

`V_p/(R_i C_f)`

Change in output during half cycle:

`ΔV = slope × time`

So:

`ΔV = [V_p/(R_i C_f)] × [1/(2f)]`

Therefore:

`ΔV = V_p/(2f R_i C_f)`

This is the change from one peak to the other, so it is approximately the output peak-to-peak value:

`V_o(pp) ≈ V_p/(2f R_i C_f)`

Since square wave input peak-to-peak is:

`V_in(pp) = 2V_p`

Then:

`V_p = V_in(pp)/2`

So:

`V_o(pp) ≈ [V_in(pp)/2] / [2fR_iC_f]`

Final:

`V_o(pp) ≈ V_in(pp)/(4fR_iC_f)`

### Simple meaning

Triangle amplitude:

- increases when input amplitude increases
- decreases when frequency increases
- decreases when `R_i` increases
- decreases when `C_f` increases

Most important:

`V_o(pp) ∝ 1/f`

So if frequency becomes larger, triangle wave becomes smaller.

---

## 7) Sine input to integrator

Suppose:

`V_in = V_m sin(ωt)`

Integrator equation:

`V_o = -1/(R_i C_f) ∫ V_m sin(ωt) dt`

Take constants outside:

`V_o = -V_m/(R_i C_f) ∫ sin(ωt) dt`

We know:

`∫ sin(ωt) dt = -cos(ωt)/ω`

So:

`V_o = -V_m/(R_i C_f) × [-cos(ωt)/ω]`

Therefore:

`V_o = V_m/(ωR_iC_f) cos(ωt)`

Depending on the sign convention used in the lab, the output may be described as a cosine or negative-going cosine because the op-amp is inverting and phase shifts are observed on the oscilloscope.

### Important amplitude result

`V_o(max) = V_m/(ωR_iC_f)`

Since:

`ω = 2πf`

`V_o(max) = V_m/(2πfR_iC_f)`

### Simple meaning

For sine input in an integrator:

- output is cosine-shaped
- output amplitude decreases when frequency increases

---

# 8) Practical integrator with feedback resistor

In the experiment, the integrator has:

- `R_i` at input
- `C_f` in feedback
- `R_f` also in feedback

The feedback resistor `R_f` is placed in parallel with `C_f`.

### Why is `R_f` added?

A pure capacitor feedback integrator can saturate due to tiny DC offset.

So `R_f` is added to:

- prevent DC saturation
- make the circuit stable at very low frequencies
- make it practical

---

## 9) Deriving the practical integrator transfer equation

The feedback path has `R_f` parallel with `C_f`.

For an inverting op-amp:

`V_o / V_in = - Z_f / R_i`

where:

- `Z_f` = feedback impedance
- `R_i` = input resistor

---

### Step 1: Impedance of capacitor

`Z_C = 1/(jωC_f)`

---

### Step 2: Parallel combination of `R_f` and `C_f`

Feedback impedance:

`Z_f = R_f || Z_C`

For parallel components:

`Z_f = (R_f × Z_C)/(R_f + Z_C)`

Substitute `Z_C = 1/(jωC_f)`:

`Z_f = [R_f × 1/(jωC_f)] / [R_f + 1/(jωC_f)]`

Multiply top and bottom by `jωC_f`:

`Z_f = R_f / (1 + jωR_fC_f)`

---

### Step 3: Use inverting amplifier formula

`V_o / V_in = -Z_f/R_i`

Substitute `Z_f`:

`V_o / V_in = - [R_f/(1 + jωR_fC_f)] / R_i`

So:

`V_o / V_in = - (R_f/R_i) × 1/(1 + jωR_fC_f)`

### Final practical integrator equation

`V_o = - (R_f/R_i) × [1/(1 + jωR_fC_f)] × V_in`

This is the equation shown in the practical sheet.

---

## 10) Low-frequency behavior of practical integrator

At low frequency:

`ωR_fC_f << 1`

So:

`1 + jωR_fC_f ≈ 1`

Then:

`V_o/V_in ≈ -R_f/R_i`

### Meaning
At low frequency, the circuit behaves like a normal inverting amplifier.

---

## 11) Integrator behavior condition

At higher frequency:

`ωR_fC_f >> 1`

So:

`1 + jωR_fC_f ≈ jωR_fC_f`

Then:

`V_o/V_in = - (R_f/R_i) × 1/(jωR_fC_f)`

Cancel `R_f`:

`V_o/V_in = -1/(jωR_iC_f)`

This is the frequency-domain form of an integrator.

### Proper integration condition

`ωR_fC_f >> 1`

or:

`2πfR_fC_f >> 1`

So:

`f >> 1/(2πR_fC_f)`

---

## 12) Integrator cutoff frequency

The boundary frequency is:

`f_c = 1/(2πR_fC_f)`

For proper integration, input frequency should be much greater than this value.

---

## 13) Practical integrator cutoff examples

Given in experiment:

`R_f = 100 kΩ`

### Case 1: `C_f = 0.01 µF`

Convert:

`100 kΩ = 100,000 Ω`

`0.01 µF = 0.01 × 10^-6 F = 10^-8 F`

Now:

`f_c = 1/(2πR_fC_f)`

`f_c = 1/(2π × 100,000 × 10^-8)`

`f_c ≈ 159 Hz`

---

### Case 2: `C_f = 0.047 µF`

`0.047 µF = 0.047 × 10^-6 F`

`f_c = 1/(2π × 100,000 × 0.047 × 10^-6)`

`f_c ≈ 33.9 Hz`

---

### Case 3: `C_f = 0.1 µF`

`0.1 µF = 0.1 × 10^-6 F`

`f_c = 1/(2π × 100,000 × 0.1 × 10^-6)`

`f_c ≈ 15.9 Hz`

---

# Part B — Op-Amp Differentiator

---

## 14) Ideal inverting differentiator circuit

In a basic differentiator:

- input capacitor = `C_i`
- feedback resistor = `R_f`
- input voltage = `V_in`
- output voltage = `V_o`

Simple circuit idea:

```text
V_in ---- C_i ----●---- op-amp - input
                  |
                  | virtual ground
                  |
              R_f feedback
                  |
                 V_o
```

---

## 15) Deriving the ideal differentiator equation

### Step 1: Input capacitor current

For capacitor:

`I_C = C_i × dV/dt`

The inverting input is virtual ground:

`V_- ≈ 0`

So capacitor voltage is approximately:

`V_C = V_in - 0`

`V_C = V_in`

Therefore:

`I_C = C_i × dV_in/dt`

---

### Step 2: Same current flows through feedback resistor

Op-amp input current is almost zero.

So capacitor current flows through feedback resistor `R_f`.

Current through feedback resistor:

`I_f = (V_- - V_o)/R_f`

Since `V_- = 0`:

`I_f = (0 - V_o)/R_f`

`I_f = -V_o/R_f`

---

### Step 3: Equate currents

`I_C = I_f`

So:

`C_i × dV_in/dt = -V_o/R_f`

Rearrange:

`V_o = -R_f C_i × dV_in/dt`

### Final ideal differentiator equation

`V_o = -R_f C_i × dV_in/dt`

---

## 16) Meaning of differentiator equation

`V_o = -R_f C_i × dV_in/dt`

### Simple meaning
Output depends on how fast input changes.

- fast input change → large output
- slow input change → small output
- no input change → zero output

The minus sign means the output is inverted.

---

## 17) Square wave input to differentiator

A square wave has sudden changes:

- rising edge
- falling edge

During flat parts:

`dV_in/dt = 0`

So:

`V_o ≈ 0`

At rising and falling edges:

`dV_in/dt` is very large

So output becomes spikes.

### Therefore

```text
Square wave input -> spike waveform output
```

```text
Input square:

     ____      ____
____|    |____|    |____

Output spikes:

    +        +
    |        |
____|________|________
    |        |
    -        -
```

---

## 18) Triangle wave input to differentiator

A triangle wave has straight line slopes.

During rising part:

`dV_in/dt = constant positive value`

During falling part:

`dV_in/dt = constant negative value`

So output becomes two constant levels.

### Therefore

```text
Triangle wave input -> square wave output
```

---

## 19) Sine input to differentiator

Suppose:

`V_in = V_m sin(ωt)`

Differentiator equation:

`V_o = -R_fC_i × d/dt [V_m sin(ωt)]`

Take constants outside:

`V_o = -R_fC_i V_m × d/dt [sin(ωt)]`

We know:

`d/dt [sin(ωt)] = ω cos(ωt)`

So:

`V_o = -R_fC_i V_m × ω cos(ωt)`

### Final sine differentiator output

`V_o = -ωR_fC_iV_m cos(ωt)`

Depending on oscilloscope reference and inversion, it is observed as a cosine waveform with phase shift.

### Important amplitude result

`V_o(max) = ωR_fC_iV_m`

Since:

`ω = 2πf`

`V_o(max) = 2πfR_fC_iV_m`

### Simple meaning
For sine input in a differentiator:

- output is cosine-shaped
- output amplitude increases when frequency increases

---

# 20) Practical differentiator circuit

A pure differentiator is noisy and unstable because gain increases with frequency.

So the practical circuit adds:

- small input resistor `R_i`
- feedback capacitor `C_f`

These limit the frequency range and reduce noise.

---

## 21) Deriving the practical differentiator transfer equation

For an inverting op-amp:

`V_o / V_in = - Z_f / Z_i`

where:

- `Z_i` = input impedance
- `Z_f` = feedback impedance

---

## 22) Input impedance `Z_i`

Input side has `R_i` in series with `C_i`.

Capacitor impedance:

`Z_Ci = 1/(jωC_i)`

So:

`Z_i = R_i + 1/(jωC_i)`

Put into one fraction:

`Z_i = (1 + jωC_iR_i)/(jωC_i)`

---

## 23) Feedback impedance `Z_f`

Feedback side has `R_f` in parallel with `C_f`.

Capacitor impedance:

`Z_Cf = 1/(jωC_f)`

Parallel combination:

`Z_f = R_f || Z_Cf`

`Z_f = R_f/(1 + jωC_fR_f)`

---

## 24) Substitute into inverting formula

Start:

`V_o/V_in = -Z_f/Z_i`

Substitute:

`V_o/V_in = - [R_f/(1 + jωC_fR_f)] / [(1 + jωC_iR_i)/(jωC_i)]`

Dividing by a fraction means multiplying by its reciprocal:

`V_o/V_in = - [R_f/(1 + jωC_fR_f)] × [jωC_i/(1 + jωC_iR_i)]`

Rearrange:

`V_o/V_in = - [jωC_iR_f] / [(1 + jωC_iR_i)(1 + jωC_fR_f)]`

### Final practical differentiator equation

`V_o = - [jωC_iR_f / ((1 + jωC_iR_i)(1 + jωC_fR_f))] V_in`

This is the equation shown in the practical sheet.

---

# 25) Differentiator operation regions

The practical differentiator works properly only in a middle frequency range.

## 25.1 Lower limit

For differentiation, the input capacitor action must dominate.

Condition:

`ωR_fC_i >> 1`

So:

`f >> 1/(2πR_fC_i)`

This is the lower frequency limit.

---

## 25.2 Upper limit

At very high frequency, the circuit should not amplify too much noise.

The feedback capacitor limits high-frequency gain.

Condition:

`ωR_iC_f << 1`

So:

`f << 1/(2πR_iC_f)`

This is the upper frequency limit.

---

## 25.3 Combined condition

For proper differentiation:

`1/(2πR_fC_i) << f << 1/(2πR_iC_f)`

Also, the time constants must satisfy:

`R_fC_i >> R_iC_f`

### Simple meaning
The differentiator must operate:

- not too low in frequency
- not too high in frequency
- inside the safe middle region

---

# 26) Differentiator frequency limit examples

From the practical differentiator circuit:

- `R_i = 82 Ω`
- `R_f = 1.5 kΩ`
- `C_f = 0.0047 µF`
- `C_i` may be `0.1 µF`, `0.01 µF`, or `0.047 µF`

---

## 26.1 Upper cutoff due to `R_i` and `C_f`

`f_upper = 1/(2πR_iC_f)`

Convert:

`R_i = 82 Ω`

`C_f = 0.0047 µF = 0.0047 × 10^-6 F`

So:

`f_upper = 1/(2π × 82 × 0.0047 × 10^-6)`

`f_upper ≈ 413 kHz`

---

## 26.2 Lower cutoff for `C_i = 0.1 µF`

`f_lower = 1/(2πR_fC_i)`

`R_f = 1.5 kΩ = 1500 Ω`

`C_i = 0.1 µF = 0.1 × 10^-6 F`

`f_lower = 1/(2π × 1500 × 0.1 × 10^-6)`

`f_lower ≈ 1061 Hz`

So:

`f_lower ≈ 1.06 kHz`

---

## 26.3 Lower cutoff for `C_i = 0.01 µF`

`C_i = 0.01 µF = 0.01 × 10^-6 F`

`f_lower = 1/(2π × 1500 × 0.01 × 10^-6)`

`f_lower ≈ 10.6 kHz`

---

## 26.4 Lower cutoff for `C_i = 0.047 µF`

`C_i = 0.047 µF = 0.047 × 10^-6 F`

`f_lower = 1/(2π × 1500 × 0.047 × 10^-6)`

`f_lower ≈ 2.26 kHz`

---

# 27) Frequency response explanation

The practical sheet shows three regions:

```text
Gain dB
 ^
 |          /\
 |         /  \
 |        /    \
 |_______/      \_______> log f
     Diff   Inv   Int
```

### Left side: Differentiator region

Gain increases with frequency.

Slope is approximately:

`+20 dB/decade`

### Middle: Inverting amplifier region

Gain is almost constant.

### Right side: Integrator region

Gain decreases with frequency.

Slope is approximately:

`-20 dB/decade`

---

# 28) Quick comparison of integrator and differentiator equations

| Circuit | Main equation | Meaning |
|---|---|---|
| Integrator | `V_o = -1/(R_iC_f) ∫V_in dt` | Output depends on area under input |
| Differentiator | `V_o = -R_fC_i dV_in/dt` | Output depends on rate of change |

---

# 29) Easy memory section

## Integrator

```text
Input square  -> Output triangle
Input sine    -> Output cosine / negative cosine
Higher f      -> smaller output
```

Main equation:

`V_o = -1/(R_iC_f) ∫V_in dt`

Condition:

`f >> 1/(2πR_fC_f)`

---

## Differentiator

```text
Input square   -> Output spikes
Input triangle -> Output square
Input sine     -> Output cosine
Higher f       -> larger output, until practical limit
```

Main equation:

`V_o = -R_fC_i dV_in/dt`

Condition:

`1/(2πR_fC_i) << f << 1/(2πR_iC_f)`

---

# 30) Final simple conclusion

The integrator and differentiator equations come from the same basic op-amp idea: the inverting input is at virtual ground and almost no current enters the op-amp. In the integrator, resistor current charges the feedback capacitor, producing an output proportional to the integral of the input. In the differentiator, the input capacitor current depends on how fast the input changes, producing an output proportional to the derivative of the input. Practical circuits add extra resistors and capacitors to make the circuits stable and useful only in a selected frequency range.
