# Problem 2

**Estimating $\pi$ with Monte Carlo Methods**

*This report presents two Monte Carlo methods for estimating the mathematical constant $\pi$: a geometric point-sampling method using a unit circle and Buffon’s Needle, a classic probabilistic approach. Both methods are explored through theory, simulation, visualization, and analysis of convergence behavior.*

## Part 1: Estimating $\pi$ Using a Circle

### 1. Theoretical Foundation

Monte Carlo methods approximate $\pi$ by comparing areas within geometric shapes. A unit circle inside a square of side 2 gives:

$$
P(\text{point in circle}) = \frac{\pi}{4}
$$

Generating $N$ points $(x_i, y_i) \in [-1, 1]^2$, we estimate $\pi$ as:

$$
\pi \approx 4 \cdot \frac{N_{\text{circle}}}{N}
$$

### 2. Simulation

Generate $N$ uniform points and count how many fall inside the unit circle:

```python
import numpy as np

N = 10000
x = np.random.uniform(-1, 1, N)
y = np.random.uniform(-1, 1, N)
inside = x**2 + y**2 <= 1
pi_estimate = 4 * np.sum(inside) / N
```

### 3. Visualization

Plot the points with a unit circle boundary:

```python
import numpy as np
import matplotlib.pyplot as plt

# Number of points
N = 10000

# Generate random points in [-1, 1] x [-1, 1]
x = np.random.uniform(-1, 1, N)
y = np.random.uniform(-1, 1, N)

# Check which points fall inside the unit circle
inside = x**2 + y**2 <= 1

# Estimate π
pi_estimate = 4 * np.sum(inside) / N

# Print the estimated value of π
print(f"Monte Carlo Estimation of π")
print(f"Estimated value of π using {N} points: {pi_estimate:.6f}")

# (Optional) Calculate absolute error
pi_error = abs(np.pi - pi_estimate)
print(f"Absolute error: {pi_error:.6f}")

# Plot the result
plt.figure(figsize=(6, 6))
plt.scatter(x[inside], y[inside], color='blue', s=1, label='Inside Circle')
plt.scatter(x[~inside], y[~inside], color='red', s=1, label='Outside Circle')

# Plot the actual unit circle for reference
theta = np.linspace(0, 2 * np.pi, 300)
plt.plot(np.cos(theta), np.sin(theta), color='black', linewidth=1.5, label='Unit Circle')

plt.gca().set_aspect('equal')
plt.title('Monte Carlo Estimation of π')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()
plt.grid(True)
plt.show()
```
![Monte Carlo Estimation of PI](../../_pics/Physics/6%20Statistics/Problem_2/monte-carlo-estimation-of-pi_v2.png)

### 4. Analysis

As $N$ increases, the estimate stabilizes. Error decreases as:

$$
\text{Error} \propto \frac{1}{\sqrt{N}}
$$

This method is simple, fast, and converges well for educational purposes.

---

## Part 2: Estimating $\pi$ Using Buffon’s Needle

### 1. Theoretical Foundation

Drop a needle of length $L$ on parallel lines spaced $t$ apart. The crossing probability is:

$$
P = \frac{2L}{\pi t} \Rightarrow \pi \approx \frac{2L \cdot N}{t \cdot C}
$$

### 2. Simulation

Generate angles $\theta \sim \mathcal{U}(0, \pi)$ and distances $d \sim \mathcal{U}(0, t/2)$. Check if:

$$
\frac{L}{2} \sin(\theta) \geq d
$$

```python
import numpy as np

N = 100000
L = 1.0
t = 1.5

theta = np.random.uniform(0, np.pi, N)
d = np.random.uniform(0, t / 2, N)
crosses = (L / 2) * np.sin(theta) >= d
C = np.sum(crosses)
pi_estimate = (2 * L * N) / (t * C)
```

### 3. Visualization

Simulate and plot needle drops with crossing indicators:

```python
import numpy as np
import matplotlib.pyplot as plt

# -------------------------------
# Buffon’s Needle Simulation
# -------------------------------

# Simulation parameters
N = 100000  # Number of needles
L = 1.0     # Length of the needle
t = 1.5     # Distance between parallel lines

# Generate random needle angles and distances
theta = np.random.uniform(0, np.pi, N)
d = np.random.uniform(0, t / 2, N)

# Check which needles cross a line
crosses = (L / 2) * np.sin(theta) >= d
C = np.sum(crosses)

# Estimate π
pi_estimate = (2 * L * N) / (t * C)
error = abs(np.pi - pi_estimate)

# Print the results
print(f"Estimated π using {N} needles: {pi_estimate:.6f}")
print(f"Absolute error: {error:.6f}")

# -------------------------------
# Visualization (for a smaller subset)
# -------------------------------
N_vis = 200  # number of needles to visualize
x_center = np.random.uniform(0, 10, N_vis)
y_center = np.random.uniform(0, 10, N_vis)
theta_vis = np.random.uniform(0, np.pi, N_vis)

dx = (L / 2) * np.cos(theta_vis)
dy = (L / 2) * np.sin(theta_vis)

x_start = x_center - dx
x_end = x_center + dx
y_start = y_center - dy
y_end = y_center + dy

# Check which visualized needles cross a line
crosses_vis = ((y_start // t) != (y_end // t))

# Plotting
plt.figure(figsize=(8, 8))
for i in range(N_vis):
    color = 'red' if crosses_vis[i] else 'blue'
    plt.plot([x_start[i], x_end[i]], [y_start[i], y_end[i]], color=color, linewidth=1)

# Draw horizontal lines
for y_line in np.arange(0, 10 + t, t):
    plt.axhline(y=y_line, color='black', linestyle='--', linewidth=0.5)

plt.title("Buffon's Needle Simulation")
plt.xlabel('x')
plt.ylabel('y')
plt.axis('equal')
plt.grid(True)
plt.show()
```
![Buffon's Needle Simulation](../../_pics/Physics/6%20Statistics/Problem_2/buffon-needle-simulation_v2.png)

### 4. Analysis

Buffon’s method converges more slowly due to the geometry of the event. Error scales as:

$$
\text{Error} \propto \frac{1}{\sqrt{N}}
$$

While less efficient, it demonstrates the power of probabilistic modeling in geometry.

---

## Conclusion

Monte Carlo simulations offer intuitive methods for approximating $\pi$. The circle method provides rapid convergence and clear visualizations, while Buffon’s Needle highlights randomness and geometry in action. Both methods showcase how probability enables numerical insight into mathematical constants.

## Colab: Statistics Problem 2
[Souce Code](https://colab.research.google.com/drive/1qac6E1WaORLxslxGJ4dQI_IMBSB2R73m?usp=sharing)
