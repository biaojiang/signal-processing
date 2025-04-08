# Exams – Final Fall 2005, Problem 1(a)

## Problem Statement

Let \( x[n] \) be a **real-valued, causal** sequence with discrete-time Fourier transform \( X(e^{j\omega}) \).  
You are given:

\[
\Im\{X(e^{j\omega})\} = 3\sin(2\omega) - 2\sin(3\omega)
\]

Determine a possible choice for \( x[n] \).

---

## Solution

### 🔹 Step 1: Use DTFT Property

For real-valued \( x[n] \), the imaginary part of the DTFT is given by:

\[
\Im\{X(e^{j\omega})\} = -\sum_{n=-\infty}^{\infty} x[n] \sin(\omega n)
\]

This is essentially the sine Fourier series component of \( x[n] \).

### 🔹 Step 2: Match Terms

Given:

\[
\Im\{X(e^{j\omega})\} = 3\sin(2\omega) - 2\sin(3\omega)
\]

Then:

\[
- x[2] = 3 \Rightarrow x[2] = -3 \\
- x[3] = -2 \Rightarrow x[3] = 2
\]

No sine term for \( n = 0 \), so **\( x[0] \)** does not affect the imaginary part of the DTFT.

Since the sequence is causal and real-valued, \( x[n] = 0 \) for \( n < 0 \), and all other \( x[n] \) not explicitly found above are 0.  
However, \( x[0] \) can be **any real value**, because it contributes **only to the real part** of \( X(e^{j\omega}) \).

---

## ✅ Final Answer

The general solution is:

\[
x[n] = x[0]\delta[n] - 3\delta[n - 2] + 2\delta[n - 3]
\]

Where \( x[0] \in \mathbb{R} \) is arbitrary.

Or written out:

```
x[0] = arbitrary
x[1] = 0
x[2] = -3
x[3] = 2
x[n] = 0 for all other n ≥ 0
```

---

## Notes

This solution uses the symmetry and orthogonality of the sine basis in DTFT. Since the sequence is causal and real-valued, all nonzero components must appear for \( n \geq 0 \), and the imaginary part determines only the sine-weighted coefficients.

---

### 🔍 What Is a Causal System?

In discrete-time signal processing:

> A **causal system or sequence** is one where  
> **$x[n] = 0$** for all $n < 0$

That is, the system/output doesn’t depend on **future** values of the input. All non-zero values are at $n \geq 0$.
