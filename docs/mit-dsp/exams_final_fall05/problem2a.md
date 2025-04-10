# Problem 2(a) – Is the Overall System Discrete-Time LTI?

## Given
- **T1 = T2 = 10^-4 s**
- **Ω0 = (4π)/T1**
- Discrete-time filter H1(e^(jω)) with passband ±ω0
- Continuous-time filter H2(jΩ) with passband ±Ω0
- System: x[n] → D/C (with period T1) → H2(jΩ) → C/D (with period T2) → y[n]

## Question
> “Is there a **non-zero** ω0 > 0 such that the **overall system from x[n] to y[n]** behaves like a **discrete-time LTI system**? If yes, specify such ω0. Otherwise, explain why not.”

---

## Analysis

For the **overall** discrete-time system to be LTI, two main conditions must hold:

1. **No unwanted aliasing** when going from discrete to continuous and back.
2. **Time-invariance** in the discrete domain (shifting x by k samples shifts y by k samples).

Let’s examine the sampling rates and passbands:

1. **D/C at T1 = 10^-4 s**  
   - A discrete frequency ω ∈ [−π, π] in H1 maps to a continuous frequency Ω = (ω / T1).
   - So the passband ±ω0 in discrete time becomes ±(ω0 / T1) in continuous time.

2. **Continuous Filter H2(jΩ)** with passband ±Ω0 = ±(4π / T1).  
   - So H2 passes continuous frequencies up to ±(4π / T1) = ±40000π.

3. **C/D at T2 = 10^-4 s**  
   - After filtering, we sample at fs2 = 1/T2 = 10^4 Hz.  
   - The maximum non-aliased frequency in continuous domain is ±(π / T2) = ±(π / 10^-4) = ±31400.

### Key Observation: Potential Aliasing

- H2 passes frequencies up to 40000π ≈ 125,663.7 rad/s.
- But sampling again at T2 = 10^-4 s only has a Nyquist limit of ±31,400 rad/s.
- This large passband (±125,663.7) **exceeds** ±31,400, so **any** non-zero ω0 that tries to use part of that band above 31,400 rad/s will be aliased.

### Trying to Restrict ω0

We might hope that choosing a small ω0 < π would keep (ω0 / T1) < π / T2. But let’s check:

1. (ω0 / T1) ≤ π / T2  
   With T1 = T2 = 10^-4,
   ⇒ ω0 ≤ π.

2. But H1’s passband is ±ω0, so in continuous domain it’s ±(ω0 / T1).  
   We require it also be ≤ Ω0 = 4π / T1, i.e. ω0 ≤ 4π. This is less strict than π, so no conflict here.

At first glance, that might imply we can set ω0 = π and not exceed the second Nyquist limit. But we must check **how H2’s broad passband** interacts with the sampling at T2.

- If H2 truly is 1 up to ±40000π, then **frequencies above ±31400** will alias upon sampling with T2.
- The path includes frequencies beyond ±31400 rad/s in the continuous domain, unless H1 forcibly restricts them *before* D/C. But H1 is in the discrete domain, so it doesn’t actually limit anything in the analog domain beyond ±(π / T1)=±31400.

### Conclusion

**We cannot cleanly limit the analog passband** to ±31400 only, because H2’s passband is ±125663.7 rad/s and does not forcibly remove frequencies above 31400. The second sampling step (C/D at T2) will alias them back into discrete frequencies. Thus, the system is **not guaranteed** to remain LTI for any nonzero ω0 > 0.

> **Answer**: **No**, there is **no non-zero** ω0 for which the overall system is guaranteed to be discrete-time LTI. Any band that tries to pass through H2 up to ±40000π rad/s will exceed the second Nyquist limit ±31400 rad/s, resulting in aliasing.

---

## Appendix: Proof of Equivalent Discrete-Time Filter When T1 = T2

We prove that the cascade of:
1. D/C conversion with period T1
2. Continuous-time LTI filter H2(jΩ)
3. C/D conversion with period T2 = T1

is equivalent to a discrete-time LTI system with frequency response:

\[
H'_2(e^{j\omega}) = H_2\left(j\frac{\omega}{T_1}\right), \quad |\omega| < \pi
\]

### Step-by-Step:

- Start with input \( x[n] \) with DTFT \( X(e^{j\omega}) \).
- D/C conversion turns it into impulse train:
  \[
  x_a(t) = \sum_n x[n] \delta(t - nT_1)
  \]
- Its Fourier transform:
  \[
  X_a(j\Omega) = \frac{1}{T_1} X(e^{j\Omega T_1}) \quad 	\text{(assuming no
  aliasing)}
  \]
- Filtering gives:
  \[
  Y_a(j\Omega) = H_2(j\Omega) \cdot X_a(j\Omega)
  \]
- Resampling at \( T_2 = T_1 \):
  \[
  y[n] = y_a(nT_1), \quad \Rightarrow \quad Y(e^{j\omega}) = Y_a\left(j\frac{\omega}{T_1}\right)
  \]
- Substitute:
  \[
  Y(e^{j\omega}) = \frac{1}{T_1} H_2\left(j\frac{\omega}{T_1}\right) X(e^{j\omega})
  \]

Thus, the system behaves as:
\[
H'_2(e^{j\omega}) = H_2\left(j\frac{\omega}{T_1}\right) \quad 	\text{(up to scale)}
\]

This is the formal justification for treating the whole analog path as a discrete-time LTI filter with a scaled frequency argument.
