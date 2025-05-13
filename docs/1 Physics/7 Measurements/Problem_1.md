# Problem 1

**Measuring Earth's Gravitational Acceleration with a Pendulum**

## 1. Experiment Overview

This experiment estimates gravitational acceleration $g$ using a simple pendulum, focusing on measurement, uncertainty analysis, and result interpretation.

### 1.1 Materials & Setup

* **Charging cable** (~1.0 m), **smartphone** used as the pendulum bob.
* **Ruler or tape measure** (resolution \( r \)), **stopwatch or phone timer**.
* **Door handle** used as the support to hang the pendulum; ensure motion is in a vertical plane.

Measure pendulum length \( L \) from the point where the cable hangs on the door handle to the center of mass of the phone:

$$
\Delta L = \frac{r}{2}
$$

Keep angle \( \theta < 15^\circ \) to satisfy:

$$
T = 2\pi \sqrt{\frac{L}{g}}, \quad \sin(\theta) \approx \theta
$$

---

## 2. Data Collection & Timing

Gently release pendulum. Measure time for 10 oscillations ($T_{10}$), repeated 10 times:

| Trial | $T_{10}$ (s) |
|-------|--------------|
| 1     | 19.58        |
| 2     | 20.01        |
| 3     | 20.12        |
| 4     | 19.96        |
| 5     | 19.75        |
| 6     | 19.85        |
| 7     | 20.03        |
| 8     | 19.89        |
| 9     | 20.25        |
| 10    | 20.32        |


Compute:

$$
\overline{T}_{10} = \frac{1}{n} \sum T_{10,i}, \quad \sigma_T = \sqrt{\frac{1}{n-1} \sum (T_{10,i} - \overline{T}_{10})^2}, \quad \Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
$$

$$
T = \frac{\overline{T}_{10}}{10}, \quad \Delta T = \frac{\Delta T_{10}}{10}
$$

---

## 3. Calculating $g$ and Uncertainty

$$
g = \frac{4\pi^2 L}{T^2}, \quad
\Delta g = g \cdot \sqrt{ \left( \frac{\Delta L}{L} \right)^2 + \left( 2 \cdot \frac{\Delta T}{T} \right)^2 }
$$

Report:

$$
g = \bar{g} \pm \Delta g \quad \text{m/s}^2
$$

---

## 4. Results Summary

| Quantity               | Value       |
| ---------------------- | ----------- |
| $\overline{T}\_{10}$ | 19.9760 s   |
| $\sigma\_T$          | 0.2235 s    |
| $\Delta T\_{10}$     | 0.0707 s    |
| $T$                  | 1.9976 s    |
| $\Delta T$           | 0.00707 s   |
| $L$                  | 1.050 m     |
| $\Delta L$           | 0.0005 m    |
| $g$                  | 10.388 m/s² |
| $\Delta g$           | 0.074 m/s²  |

| Quantity               | Value        |
|------------------------|--------------|
| $\overline{T}_{10}$    | 19.9760 s    |
| $\sigma_T$             | 0.2235 s     |
| $\Delta T_{10}$        | 0.0707 s     |
| $T$                    | 1.9976 s     |
| $\Delta T$             | 0.00707 s    |
| $L$                    | 1.050 m      |
| $\Delta L$             | 0.0005 m     |
| $g$                    | 10.388 m/s²  |
| $\Delta g$             | 0.074 m/s²   |

---

## 5. Visualization

![T10 vs Trial](../../_pics/Physics/7%20Measurements/Problem_1/t10_vs_trials.png)

### Python Code to Generate Plot and Compute $g$

```python
import numpy as np
import matplotlib.pyplot as plt

# Replace with your actual measurements
t10_values = np.array([19.58, 20.01, 20.12, 19.96, 19.75, 19.85, 20.03, 19.89, 20.25, 20.32])
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
plt.title('Measured Time for 10 Pendulum Oscillations ($T_{10}$) vs. Trial Number')
plt.xlabel('Trial Number')
plt.ylabel(r'$T_{10}$ (s)')
plt.grid(True, linestyle='--', alpha=0.6)
plt.legend()
plt.tight_layout()
plt.savefig("t10_vs_trials.png", dpi=300)
plt.show()
```

### Histogram of T₁₀ Measurements
```python
import numpy as np
import matplotlib.pyplot as plt

# Data
t10_values = np.array([19.58, 20.01, 20.12, 19.96, 19.75, 19.85, 20.03, 19.89, 20.25, 20.32])
T10_mean = np.mean(t10_values)

# Plot
plt.figure(figsize=(8, 5))
plt.hist(t10_values, bins='auto', edgecolor='black', alpha=0.7)
plt.axvline(T10_mean, color='red', linestyle='--', label=f'Mean = {T10_mean:.2f} s')
plt.xlabel('T₁₀ (s)')
plt.ylabel('Frequency')
plt.title('Distribution of T₁₀ Measurements')
plt.grid(True, linestyle='--', alpha=0.6)
plt.legend()
plt.tight_layout()
plt.show()
```
![T10 vs Trial](../../_pics/Physics/7%20Measurements/Problem_1/histogram_t10.png)

### Colab Measurements Problem 1
[Souce Code](https://colab.research.google.com/drive/1HUtq7RRQ6GR3qvYTUgwvtYOdLsazqWwU#scrollTo=fBGiMl0CDPkF)

### Interpretation

* Data shows low variation and a stable mean.
* Confirms reliability of $\overline{T}_{10}$ and $g$.

---

## 6. Analysis

### 6.1 Comparison with Standard Value

Compared to the standard gravitational acceleration value $g_{\text{standard}} = 9.810\ \text{m/s}^2$:

* The measured value is:

$$
g = 10.388 \pm 0.074\ \text{m/s}^2
$$

* This result is significantly higher than expected, even when accounting for geographical variation in $g$ (typically between $9.78$ and $9.83\ \text{m/s}^2$).

This discrepancy suggests the presence of systematic error in the experiment.

Possible sources of error include:

- **Underestimated pendulum length**: If the length $L$ was measured too short (e.g., not fully to the phone's center of mass), this would lead to an overestimation of $g$.
- **Reaction time error**: Manual stopwatch timing may have caused the measured period to appear shorter than it actually was, again leading to an inflated $g$ value.
- **Non-ideal pendulum motion**: If the pendulum was not swinging in a single vertical plane or the initial angle exceeded $15^\circ$, this could violate the small-angle approximation and distort results.

> The discrepancy may come from an underestimated pendulum length (if the full vertical distance was not properly measured to the phone's center of mass) or from reaction-time errors when using a manual stopwatch. Either would cause the period to appear shorter and artificially increase the calculated value of $g$.



### 6.2 Uncertainty Sources

* $\Delta L$: Ruler resolution.
* $\Delta T$: Human reaction time.
* Assumptions: small-angle approximation, minimal drag.

### 6.3 Improvements

* Use photogates for timing.
* Use rigid stand and point-mass bob.
* Increase number of trials.

---

## 7. Conclusion

In this experiment, we estimated the gravitational acceleration $g$ by analyzing the motion of a simple pendulum.

A smartphone was suspended on a cable of measured length, and the time for 10 oscillations ($T_{10}$) was recorded across 10 trials. Using the average period and the pendulum length, the gravitational acceleration was calculated with propagated uncertainties.

The final result is:

$$
g = 10.388 \pm 0.074\ \text{m/s}^2
$$

This value is higher than the standard gravitational acceleration $g_{\text{standard}} = 9.810\ \text{m/s}^2$, indicating the presence of systematic error in the measurements.

Potential causes include:

- Underestimation of pendulum length $L$
- Human reaction time errors when using a manual stopwatch
- Small deviations from the ideal conditions assumed in the pendulum model (e.g., angle > $15^\circ$, non-planar motion)

Despite the discrepancy, the experiment successfully demonstrated a reliable method for estimating $g$ using simple tools and reinforced principles of uncertainty analysis and error propagation.

For improved accuracy, future repetitions of the experiment should use:

- Electronic timing systems (e.g., video analysis or photogates)
- More precise length measurements
- Smaller release angles and a rigid pendulum setup