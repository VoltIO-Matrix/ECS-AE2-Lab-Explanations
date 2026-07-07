# Experiment 04 — Comparator and Schmitt Trigger

## Easy Clear Explanation

This practical has two main circuits:

1. **Comparator**
2. **Schmitt Trigger**

Both circuits use an op-amp, but here the op-amp is not used like a normal amplifier. It is used like a **switching circuit**.

---

## 1) Main idea of this experiment

A normal amplifier makes a signal bigger.

But a **comparator** compares two voltages:

- input voltage `V_in`
- reference voltage `V_ref`

Then it decides which one is bigger.

If the input is bigger than the reference, the output goes to one saturation level.
If the input is smaller than the reference, the output goes to the opposite saturation level.

So a comparator is like an electronic **yes/no decision maker**.

---

## 2) Basic comparator equation

The practical sheet gives:

```text
V_o = A(V_+ - V_-)
```

where:

| Symbol | Meaning |
|---|---|
| `V_o` | output voltage |
| `A` | open-loop gain of the op-amp |
| `V_+` | voltage at non-inverting input |
| `V_-` | voltage at inverting input |

### Simple meaning

The op-amp checks this difference:

```text
V_+ - V_-
```

If the answer is positive, output goes high.
If the answer is negative, output goes low.

---

## 3) Why does output jump high or low?

The op-amp open-loop gain is extremely high.

For a 741 op-amp, open-loop gain can be around:

```text
A ≈ 10^5 to 10^6
```

So even a tiny input difference becomes very large.

Example:

```text
V_+ - V_- = 0.001 V
A = 100000

V_o = 100000 × 0.001 = 100 V
```

But the op-amp cannot output 100 V because the supply is only about `±15 V`.

So the output saturates:

- near positive saturation
- or near negative saturation

---

## 4) Comparator output rule

```text
If V+ > V-  → output HIGH
If V+ < V-  → output LOW
```

This is the most important comparator rule.

---

## 5) What is a zero-crossing detector?

A zero-crossing detector is a comparator where:

```text
V_ref = 0 V
```

It detects when the input signal crosses zero.

If a sine wave is given to a zero-crossing detector, the output becomes a square-like wave.

```text
Sine input  →  square output
```

---

## 6) Comparator circuit in this practical

In Figure 2:

- `V_in` comes from the signal generator
- `V_ref` comes from the 10 kΩ potentiometer
- the op-amp compares `V_in` and `V_ref`
- the output is observed using the oscilloscope
- rectifier diodes protect/clamp the input section

You test three reference voltages:

1. `V_ref = 0 V`
2. `V_ref = +0.5 V`
3. `V_ref = -0.5 V`

---

## 7) What happens when `V_ref = 0 V`?

The output changes when the sine wave crosses 0 V.

So this is called zero-crossing detection.

```text
Input sine:

   /\      /\
  /  \    /  \
_/    \__/    \__

Output square:

____      ____
    |____|    |____
```

---

## 8) What happens when `V_ref = +0.5 V`?

Now the input must go above `+0.5 V` before the output changes.

So the switching level moves upward.

The output pulse becomes narrower or shifted because the sine wave is above `+0.5 V` for less time.

---

## 9) What happens when `V_ref = -0.5 V`?

Now the output changes when the input crosses `-0.5 V`.

So the switching level moves downward.

Again, the output waveform changes because the reference level changed.

---

# Part B — Schmitt Trigger

---

## 10) What is a Schmitt Trigger?

A Schmitt trigger is a comparator with **positive feedback**.

Because of positive feedback, it does not have only one switching point.

It has two switching points:

1. upper threshold
2. lower threshold

This is called **hysteresis**.

---

## 11) What is hysteresis?

Hysteresis means the output changes at different input voltages depending on whether the input is increasing or decreasing.

Simple idea:

```text
When input rises    → switches at upper threshold
When input falls    → switches at lower threshold
```

This makes the output more stable.

---

## 12) Why is Schmitt Trigger useful?

Real input signals can be noisy.

A normal comparator can switch many times if the input is noisy near the reference voltage.

A Schmitt trigger avoids this because it waits until the input crosses a clear upper or lower threshold.

So it is very useful for:

- cleaning noisy signals
- converting slow changing signals into sharp digital outputs
- switch debouncing
- waveform shaping

---

## 13) Schmitt Trigger circuit in this practical

In Figure 3:

- input sine wave is applied to the inverting input
- output is fed back to the non-inverting input
- `R_1` and `R_2` form the feedback network
- the Zener diode clamps the output level

Because output is fed back to the input, the circuit has positive feedback.

---

## 14) Function of the Zener diode

The Zener diode is `1N4733A`, approximately `5.1 V`.

It clamps the output voltage near a fixed value.

This helps keep the Schmitt trigger thresholds stable and predictable.

---

## 15) Threshold voltage equation

The feedback divider gives a fraction of output voltage to the input.

Simplified equation:

```text
V_T = βV_out
```

where:

```text
β = R_1 / (R_1 + R_2)
```

So:

```text
V_T = [R_1 / (R_1 + R_2)] × V_out
```

Since output can be positive or negative, the circuit has:

```text
+V_T and -V_T
```

These are the two switching thresholds.

---

## 16) Effect of changing `R_2`

In the practical, `R_2` is first `100 kΩ`, then changed to `200 kΩ`.

The threshold fraction is:

```text
β = R_1 / (R_1 + R_2)
```

If `R_2` increases, the denominator becomes larger.

So `β` becomes smaller.

Therefore threshold voltage becomes smaller.

### When `R_2 = 100 kΩ`

```text
β = 1k / (1k + 100k)
β = 1 / 101
β ≈ 0.0099
```

If output is about `5.1 V`:

```text
V_T ≈ 0.0099 × 5.1
V_T ≈ 0.050 V
```

### When `R_2 = 200 kΩ`

```text
β = 1k / (1k + 200k)
β = 1 / 201
β ≈ 0.0050
```

```text
V_T ≈ 0.0050 × 5.1
V_T ≈ 0.025 V
```

### Meaning

Increasing `R_2` reduces the threshold voltage and reduces the hysteresis width.

---

## 17) Comparator vs Schmitt Trigger

| Feature | Comparator | Schmitt Trigger |
|---|---|---|
| Feedback | no positive feedback | has positive feedback |
| Switching levels | one level | two levels |
| Noise immunity | lower | higher |
| Output stability | can chatter with noise | stable |
| Main use | compare voltages | clean noisy/slow signals |

---

# 18) Discussion Answers

## Q1) What is the function of the rectifier diodes in Figure 2?

They protect and clamp the op-amp input section.

They prevent a large voltage difference between the op-amp inputs.

---

## Q2) What is the function of the Zener diode in Figure 3?

The Zener diode clamps the output voltage to about `5.1 V`.

This gives controlled output levels and stable Schmitt trigger thresholds.

---

## Q3) What is the significance of `V_ref` in comparator operation?

`V_ref` is the switching reference level.

The comparator output changes when `V_in` crosses `V_ref`.

- `V_ref = 0 V` → zero-crossing detector
- `V_ref = +0.5 V` → switches at +0.5 V
- `V_ref = -0.5 V` → switches at -0.5 V

---

## Q4) What is the significance of `R_1` and `R_2` in the Schmitt trigger?

`R_1` and `R_2` set the feedback ratio.

That feedback ratio decides the upper and lower threshold voltages.

So they control the hysteresis width.

---

## Q5) What parameter is most important in op-amp comparator operation?

Important parameters include:

- slew rate
- response time
- input offset voltage
- output saturation voltage
- input common-mode range

Most important simple answer:

```text
Switching speed / slew rate
```

---

## Q6) Explain the differences between comparator and Schmitt trigger.

A comparator has one reference level and changes output when input crosses that level.

A Schmitt trigger has two threshold levels because of positive feedback.

Therefore, a Schmitt trigger is better for noisy or slowly changing input signals.

---

## Q7) What are limitations of an op-amp as a comparator?

A 741 op-amp is not a perfect comparator.

Limitations:

- slower switching
- limited slew rate
- saturation recovery delay
- output may not match digital logic levels
- input voltage range limitations

---

## 19) Final simple conclusion

This experiment explains how an op-amp can be used as a comparator and as a Schmitt trigger. A comparator compares an input voltage with a reference voltage and gives a high or low output. When the reference is zero, it works as a zero-crossing detector. A Schmitt trigger is a comparator with positive feedback, so it has two switching thresholds. This hysteresis makes it more stable and better for noisy signals.

---

## 20) Super short memory note

```text
Comparator:
Vin compared with Vref
One switching level

Schmitt Trigger:
Comparator + positive feedback
Two switching levels
Better noise immunity
```
