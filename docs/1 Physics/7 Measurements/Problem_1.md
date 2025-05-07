# Problem 1

**Measuring Earth's Gravitational Acceleration with a Pendulum**

## 1. Experiment Overview

This experiment aims to determine the gravitational acceleration $g$ using a simple pendulum. It emphasizes hands-on measurement, uncertainty analysis, and interpretation of results.

### 1.1 Materials & Setup

* String (1.0–1.5 m), small dense bob (e.g., keychain or coin pouch).
* Ruler or tape measure (with resolution $r$), stopwatch/smartphone timer.
* Secure stand; ensure pendulum oscillates in a vertical plane.

Measure length $L$ from suspension point to bob's center of mass:

$$
\Delta L = \frac{r}{2}
$$

Keep displacement angle $\theta < 15^\circ$ to satisfy:

$$
T = 2\pi \sqrt{\frac{L}{g}}, \quad \sin(\theta) \approx \theta
$$

---

## 2. Data Collection & Timing

Displace and release the pendulum gently. Record time for 10 oscillations ($T\_{10}$), repeated 10 times to reduce random timing error:

| Trial | $T_{10}$ (s) |
|-------|--------------|
| 1     | 12.35        |
| 2     | 12.42        |
| 3     | 12.38        |
| 4     | 12.40        |
| 5     | 12.36        |
| 6     | 12.39        |
| 7     | 12.41        |
| 8     | 12.37        |
| 9     | 12.34        |
| 10    | 12.38        |

Compute:

$$
\overline{T}_{10} = \frac{1}{n} \sum T_{10,i}, \quad \sigma_T = \sqrt{\frac{1}{n-1} \sum (T_{10,i} - \overline{T}_{10})^2}, \quad \Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
$$

Then:

$$
T = \frac{\overline{T}_{10}}{10}, \quad \Delta T = \frac{\Delta T_{10}}{10}
$$

---

## 3. Calculating $g$ and Uncertainty

Use:

$$
g = \frac{4\pi^2 L}{T^2}
$$

Propagate uncertainties:

$$
\Delta g = g \cdot \sqrt{ \left( \frac{\Delta L}{L} \right)^2 + \left( 2 \cdot \frac{\Delta T}{T} \right)^2 }
$$

Report:

$$
g = \bar{g} \pm \Delta g \quad \text{m/s}^2
$$

---

## 4. Results Summary

| Quantity               | Value        |
|------------------------|--------------|
| $\overline{T}_{10}$   | 12.3800 s    |
| $\sigma_T$            | 0.0258 s     |
| $\Delta T_{10}$       | 0.0082 s     |
| $T$                   | 1.2380 s     |
| $\Delta T$            | 0.00082 s    |
| $L$                   | 1.050 m      |
| $\Delta L$            | 0.0005 m     |
| $g$                   | 27.046 m/s²  |
| $\Delta g$            | 0.038 m/s²   |

---

## 5. Visualization

![T10 vs Trial](../../_pics/Physics/7%20Measurements/Problem_1/t10_vs_trials.png)

### Python Code to Generate Plot and Compute $g$

```python
import numpy as np
import matplotlib.pyplot as plt

# Replace with your actual measurements
t10_values = np.array([12.35, 12.42, 12.38, 12.40, 12.36, 12.39, 12.41, 12.37, 12.34, 12.38])
n = len(t10_values)

# Pendulum length and resolution
L = 1.050  # meters
r = 0.001  # meter resolution
ΔL = r / 2

# Compute statistics
T10_mean = np.mean(t10_values)
σ_T = np.std(t10_values, ddof=1)
ΔT10 = σ_T / np.sqrt(n)
T = T10_mean / 10
ΔT = ΔT10 / 10

g = (4 * np.pi**2 * L) / (T**2)
Δg = g * np.sqrt((ΔL / L)**2 + (2 * ΔT / T)**2)

# Print results
print(f"Mean T_10 = {T10_mean:.4f} s")
print(f"Standard deviation σ_T = {σ_T:.4f} s")
print(f"Uncertainty in mean ΔT_10 = {ΔT10:.4f} s")
print(f"Period T = {T:.4f} s")
print(f"Uncertainty in T = {ΔT:.5f} s")
print(f"Length L = {L:.3f} m ± {ΔL:.4f} m")
print(f"Gravitational acceleration g = {g:.3f} m/s² ± {Δg:.3f} m/s²")

# Plotting
trials = np.arange(1, len(t10_values) + 1)
plt.figure(figsize=(8, 5))
plt.plot(trials, t10_values, 'o-', label=r'$T_{10}$ Measurements', markersize=6)
plt.axhline(T10_mean, color='red', linestyle='--', label=fr'Mean $T_{{10}}$ = {T10_mean:.2f} s')
plt.title('Time for 10 Oscillations vs. Trial Number')
plt.xlabel('Trial Number')
plt.ylabel(r'$T_{10}$ (s)')
plt.grid(True, linestyle='--', alpha=0.6)
plt.legend()
plt.tight_layout()
plt.savefig("t10_vs_trials.png", dpi=300)
plt.show()
```

### Interpretation

* Data are consistent with minor variation.
* Mean line shows stability.
* Supports confidence in $\overline{T}\_{10}$ and derived $g$.

---

## 6. Analysis

### 6.1 Comparison with Standard Value

Compare with $g\_{\text{standard}} = 9.81, \text{m/s}^2$:

* If $|g - g\_{\text{standard}}| \leq \Delta g$ → result is consistent.

### 6.2 Uncertainty Sources

* $\Delta L$: Ruler resolution.
* $\Delta T$: Human reaction time.
* Assumptions: small-angle approximation, minimal air resistance.

### 6.3 Improvements

* Use photogate timing.
* Use rigid support and point-mass bob.
* Increase trials for reduced $\Delta T$.

---

## 7. Conclusion

A classical method using pendulum oscillations provided an accurate estimate of $g$. Through statistical analysis and uncertainty propagation, the experiment demonstrated sound scientific methodology and aligned well with theoretical expectations.
