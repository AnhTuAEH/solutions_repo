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
import matplotlib.pyplot as plt

plt.figure(figsize=(6, 6))
plt.scatter(x[inside], y[inside], color='blue', s=1, label='Inside Circle')
plt.scatter(x[~inside], y[~inside], color='red', s=1, label='Outside Circle')
theta = np.linspace(0, 2 * np.pi, 300)
plt.plot(np.cos(theta), np.sin(theta), color='black', linewidth=1.5, label='Unit Circle')
plt.gca().set_aspect('equal')
plt.title('Monte Carlo Estimation of $\pi$')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()
plt.grid(True)
plt.show()
```
![Monte Carlo Estimation of PI](../../_pics/Physics/6%20Statistics/Problem_2/monte-carlo-estimation-of-pi.png)

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
import matplotlib.pyplot as plt

N = 200
x_center = np.random.uniform(0, 10, N)
y_center = np.random.uniform(0, 10, N)
theta = np.random.uniform(0, np.pi, N)

L = 1.0
t = 1.5

dx = (L / 2) * np.cos(theta)
dy = (L / 2) * np.sin(theta)
x_start = x_center - dx
x_end = x_center + dx
y_start = y_center - dy
y_end = y_center + dy

crosses = ((y_start // t) != (y_end // t))

plt.figure(figsize=(8, 8))
for i in range(N):
    color = 'red' if crosses[i] else 'blue'
    plt.plot([x_start[i], x_end[i]], [y_start[i], y_end[i]], color=color, linewidth=1)

for y_line in np.arange(0, 10 + t, t):
    plt.axhline(y=y_line, color='black', linestyle='--', linewidth=0.5)

plt.title("Buffon's Needle Simulation")
plt.xlabel('x')
plt.ylabel('y')
plt.axis('equal')
plt.grid(True)
plt.show()
```
![Buffon's Needle Simulation](../../_pics/Physics/6%20Statistics/Problem_2/buffon-needle-simulation.png)

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
