# Exams – Final Fall 2005, Problem 1(b)
## Problem Statement

Let \( y_r[n] \) be a real-valued sequence with DTFT \( Y_r(e^{j\omega}) \). Define the complex signal:

\[
y[n] = y_r[n] + j\,y_i[n}
\]

with DTFT:

\[
Y(e^{j\omega}) = Y_r(e^{j\omega}) + j\,Y_i(e^{j\omega}) = Y_r(e^{j\omega}) \left( 1 + j H(e^{j\omega}) \right)
\]

Determine a system \( H(e^{j\omega}) \) so that:

\[
Y(e^{j\omega}) =
\begin{cases}
Y_r(e^{j\omega}), & -\pi < \omega < 0 \\
0, & 0 < \omega < \pi
\end{cases}
\]

---

## Solution

We use the relation:

\[
Y(e^{j\omega}) = Y_r(e^{j\omega}) (1 + j H(e^{j\omega}))
\]

To satisfy the condition on \( Y(e^{j\omega}) \), we solve:

\[
1 + j H(e^{j\omega}) =
\begin{cases}
1, & -\pi < \omega < 0 \\
0, & 0 < \omega < \pi
\end{cases}
\]

Solving for \( H(e^{j\omega}) \):

- For \( -\pi < \omega < 0 \):
  \[
  1 + j H(e^{j\omega}) = 1 \Rightarrow H(e^{j\omega}) = 0
  \]
  
- For \( 0 < \omega < \pi \):
  \[
  1 + j H(e^{j\omega}) = 0 \Rightarrow H(e^{j\omega}) = -\frac{1}{j} = j
  \]

---

## ✅ Final Answer

\[
H(e^{j\omega}) =
\begin{cases}
0, & -\pi < \omega < 0 \\
j, & 0 < \omega < \pi
\end{cases}
\]

This filter applied to the real-valued input \( Y_r(e^{j\omega}) \) produces the correct imaginary part \( Y_i(e^{j\omega}) \), ensuring that the total output \( Y(e^{j\omega}) \) meets the specified constraints.
