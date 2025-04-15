# Identity (b): Downsampling, Delay, and Filter Shift

## ❓ Problem Statement

Determine whether the following proposed identity is valid:

### Top Path
- Delay by 1 sample (\(z^{-1}\))
- Downsample by 2
- Filter with \(h[n]\)
- Upsample by 2
- Advance by 1 sample (\(z\))

### Bottom Path
- Advance by 1 sample (\(z\))
- Downsample by 2
- Filter with \(h[n+1]\)
- Upsample by 2
- Delay by 2 samples (\(z^{-2}\))

---

## ❌ Official Verdict: Identity is **Not Valid**

A counterexample using:

- **Input**: \( x[n] = \delta[n - 1] \)
- **Filter**: \( h[n] = \delta[n - 1] \)

### ▶️ Top Path:

1. Apply \( z^{-1} \): \( \delta[n - 2] \)
2. Downsample by 2: \( \delta[2m - 2] = \delta[m - 1] \)
3. Filter with \( \delta[n - 1] \): output \( \delta[m - 2] \)
4. Upsample by 2: \( \delta[n - 4] \) (nonzero at even indices only)
5. Apply \( z \): advance to \( \delta[n - 3] \)

✅ Final Output: \( \delta[n - 3] \)

### ▶️ Bottom Path:

1. Apply \( z \): \( \delta[n] \)
2. Downsample by 2: \( \delta[2m] = \delta[m] \)
3. Filter with \( h[n + 1] = \delta[n] \): output \( \delta[m] \)
4. Upsample by 2: \( \delta[n] \)
5. Apply \( z^{-2} \): delay to \( \delta[n - 2] \)

✅ Final Output: \( \delta[n - 2] \)

---

## 📌 Final Answer

The identity **is not valid**.  
A simple counterexample with \( x[n] = h[n] = \delta[n - 1] \) proves that the two paths yield different outputs:
\[
\delta[n - 3] \neq \delta[n - 2]
\]
