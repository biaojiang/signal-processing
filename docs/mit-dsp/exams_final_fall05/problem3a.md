# Identity (a): Downsampling and Delay

## ❓ Problem Statement

Determine whether the following proposed identity is valid:

- **Top Path**: Downsample by 2 → Half-sample delay  
- **Bottom Path**: Delay by 1 sample (\( z^{-1} \)) → Downsample by 2  

The question is whether the two systems are **equivalent**.

---

## ❌ Conclusion: The Identity is **Not Valid**

The two systems produce different outputs for the same input. A counterexample using \( \delta[n] \) (the unit impulse) proves this.

---

## 🔍 Detailed Reasoning

### ▶️ Top Path:

- Input: \( \delta[n] \)
- After downsampling by 2: \( x_d[m] = \delta[2m] \Rightarrow x_d[0] = 1 \), all others 0
- After applying a **half-sample delay**: not well-defined in integer time, but produces **nonzero output** for some interpolated values (not identically zero)

Hence, output is **not zero** in general.

### ▶️ Bottom Path:

- Input: \( \delta[n] \)
- Apply unit delay: \( x[n] = \delta[n - 1] \)
- Downsample by 2: \( x_d[m] = \delta[2m - 1] = 0 \) for all integer \( m \)

So output is **zero for all** \( m \).

---

## 📎 Official Solution Visualization

The official solution illustrates the same counterexample:

```
Top path:
δ[n] → ↓2 → [Half-sample delay] → ≠ 0 for some n

Bottom path:
δ[n] → z⁻¹ → ↓2 → 0 for all n

Therefore:   a₁ ≠ a₂
```

This shows clearly that the two systems produce different results — thus **invalid identity**.

---

## ✅ Key Insight

- A **half-sample delay** introduces a fractional phase shift (\( e^{-j\omega/2} \)), not equivalent to a unit delay (\( z^{-1} \))
- Downsampling **does not commute** with non-integer delays
- You cannot move a delay across a downsampler without adjusting both magnitude and phase correctly

---

## 📌 Final Answer

The identity is **not valid**.  
The top and bottom systems are **not equivalent**, as proven by the \( \delta[n] \) counterexample.
