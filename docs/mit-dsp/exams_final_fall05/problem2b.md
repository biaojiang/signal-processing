# Problem 2(b): Discrete-Time LTI System Conditions

**Question:**  
Assume that \( T_1 = 10^{-4} \) s and \( \omega_0 = \pi \). Determine the most general conditions on \( \Omega_0 > 0 \) and \( T_2 \), if any, so that the overall system from \( x[n] \) to \( y[n] \) in Figure 2-1 is a discrete-time LTI system.

---

## ✅ Key Idea

We analyze the system:

```
x[n] → H₁(e^{jω}) → D/C (T₁) → H₂(jΩ) → C/D (T₂) → y[n]
```

The system can be made **discrete-time LTI** if the scaling of the frequency axis caused by D/C and C/D is properly undone.

---

## ✅ Frequency Domain Interpretation

- The D/C block maps discrete-time frequency \( \omega \) to continuous frequency:
  \[
  \Omega = \frac{\omega}{T_1}
  \]
- The C/D block scales back by \( T_2 \):
  \[
  \omega' = \Omega T_2 = \omega \cdot \frac{T_2}{T_1}
  \]

So the **net scaling** is \( \frac{T_2}{T_1} \).

To preserve the DT frequency characteristics and ensure LTI behavior, we require this scaling to be either:
- handled by proper resampling
- or exactly undone

---

## ✅ Official Answer and Interpretation

The official solution sets:
\[
T_2 = \frac{2}{3} T_1
\]

With this:
- The D/C and C/D blocks together act as a **sample rate converter** by a factor of \( \frac{3}{2} \)
- This can be realized in discrete-time as:
  \[
  ↑3 	o H_2'(e^{j\omega}) 	o ↓2
  \]

No additional constraint is required on \( \Omega_0 \). The analog filter \( H_2(j\Omega) \) is absorbed into an equivalent DT filter \( H_2'(e^{j\omega}) \).

---

## ✅ Equivalent Discrete-Time LTI System

Through multirate system equivalence, the overall system becomes:

```
↑2 → H₁(e^{jω}) → H₂'(e^{jω}) → ↓2
```

And the final frequency response is:
\[
\frac{1}{2} H_1(e^{j\omega/2}) H_2'(e^{j\omega/2}) + \frac{1}{2} H_1(e^{j(\omega/2 - \pi)}) H_2'(e^{j(\omega/2 - \pi)})
\]

This confirms that the system from \( x[n] \) to \( y[n] \) is **LTI** with no restriction on \( \Omega_0 \), as long as \( T_2 = \frac{2}{3} T_1 \).

---

## ✅ Final Answer Summary

The system is discrete-time LTI **if and only if**:
\[
\boxed{T_2 = \frac{2}{3} T_1}
\]
with **no additional condition on \( \Omega_0 \)** required.
