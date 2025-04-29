# Problem 1

**Investigating the Range as a Function of the Angle of Projection**

Projectile motion provides a fundamental framework for understanding physics in two dimensions. This document derives the governing equations, analyzes the range as a function of the angle of projection, explores practical applications, and implements simulations to visualize key relationships.

---

## 1. Theoretical Foundation

### Derivation of Equations of Motion

Consider a projectile launched with initial velocity $v_0$ at angle $\theta$ from height $h$, under gravity $g$ as the sole force. Using Newton’s second law, $\vec{F} = m \vec{a}$, with $F_x = 0$ and $F_y = -mg$:

- Horizontal: $\frac{d^2x}{dt^2} = 0$.
- Vertical: $\frac{d^2y}{dt^2} = -g$.

Initial conditions are $x(0) = 0$, $y(0) = h$, $\frac{dx}{dt}(0) = v_{0x} = v_0 \cos\theta$, $\frac{dy}{dt}(0) = v_{0y} = v_0 \sin\theta$. Solving:

$$
x(t) = (v_0 \cos\theta) t,
$$

$$
y(t) = h + (v_0 \sin\theta) t - \frac{1}{2} g t^2.
$$

### Trajectory Equation

Eliminate $t$ from $x(t)$: $t = \frac{x}{v_0 \cos\theta}$. Substitute into $y(t)$:

$$
y = h + (v_0 \sin\theta) \frac{x}{v_0 \cos\theta} - \frac{1}{2} g \left( \frac{x}{v_0 \cos\theta} \right)^2,
$$

$$
y = h + x \tan\theta - \frac{g x^2}{2 v_0^2 \cos^2\theta}.
$$

This parabolic form depends on $v_0$, $\theta$, $h$, and $g$, defining a family of solutions.

### Family of Solutions

For $h = 0$, the range $R$ (where $y = 0$) is:

$$
0 = R \tan\theta - \frac{g R^2}{2 v_0^2 \cos^2\theta},
$$

$$
R = \frac{v_0^2 \sin 2\theta}{g}.
$$

Varying $v_0$, $\theta$, $h$, or $g$ generates distinct trajectories, e.g., higher $v_0$ flattens the curve, while $h \neq 0$ shifts the landing point.

---

## 2. Analysis of the Range

### Range Formula

For $h = 0$:

$$
R = \frac{v_0^2 \sin 2\theta}{g}.
$$

### Key Parameters

- $v_0$: Range scales as $v_0^2$.
- $g$: Inversely proportional to $R$.
- $\theta$: $\sin 2\theta$ peaks at 1, affecting $R$ symmetrically about 45°.

### Parameter Effects

- **Increasing $v_0$**: If $v_0$ doubles, $R$ quadruples (e.g., from 10 m/s to 20 m/s, $R$ increases by 4×).
- **Changing $g$**: On the Moon ($g = 1.62 \, \text{m/s}^2$), $R$ is $9.81 / 1.62 \approx 6$ times larger than on Earth.
- **Varying $\theta$**: $R = 0$ at $\theta = 0^\circ, 90^\circ$; peaks at $\theta = 45^\circ$.

### Optimal Angle

Maximize $R = \frac{v_0^2}{g} \sin 2\theta$:

$$
\frac{dR}{d\theta} = \frac{v_0^2}{g} \cdot 2 \cos 2\theta = 0,
$$

$$
\theta = 45^\circ, \quad R_{\text{max}} = \frac{v_0^2}{g}.
$$

---

## 3. Practical Applications

### Scenarios

- **Basketball**: Shots follow $y = x \tan\theta - \frac{g x^2}{2 v_0^2 \cos^2\theta}$.
- **Artillery**: Targets require adjusted $R$.
- **Space Launches**: Early trajectories approximate projectiles.

### Uneven Terrain

For landing height $h_f$:

$$
h_f = h + R \tan\theta - \frac{g R^2}{2 v_0^2 \cos^2\theta},
$$

solve the quadratic for $R$. For $h > h_f$, $R$ increases.

### Additional Factors

- **Air Resistance**: $F_d = -k v^2$ reduces $R$, solved numerically.
- **Wind**: Adds $w t$ to $x(t)$, shifting $R$.

### Adaptations

Use numerical methods (e.g., Runge-Kutta) for drag; adjust $x(t) = (v_0 \cos\theta + w) t$ for wind.

---

## 4. Implementation

### Simulation Tool

Below are Python scripts simulating projectile motion.

#### Code 1: Plotting the Trajectory for a Single Set of Parameters

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
v0 = 20.0  # Initial velocity (m/s)
theta_deg = 45  # Angle in degrees
g = 9.81  # Gravitational acceleration (m/s^2)
h = 0.0  # Initial height (m)

# Convert angle to radians
theta = np.radians(theta_deg)

# Time of flight (for h = 0, adjust if h != 0)
t_flight = 2 * v0 * np.sin(theta) / g
t = np.linspace(0, t_flight, 100)

# Position equations
x = v0 * np.cos(theta) * t
y = h + v0 * np.sin(theta) * t - 0.5 * g * t**2

# Plot
plt.figure(figsize=(8, 6))
plt.plot(x, y, label=f'θ = {theta_deg}°', color='blue')
plt.title('Projectile Trajectory')
plt.xlabel('Horizontal Distance (m)')
plt.ylabel('Vertical Height (m)')
plt.grid(True)
plt.legend()
plt.axhline(0, color='black', linewidth=0.5)
plt.show()
```

![Code 1](../../_pics/Physics/1%20Mechanics/Problem_1/code_1.png)

#### Code 2: Range vs. Angle for Different Initial Velocities

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
g = 9.81  # Gravitational acceleration (m/s^2)
angles_deg = np.linspace(0, 90, 91)  # Angles from 0° to 90°
angles_rad = np.radians(angles_deg)
v0_values = [10, 20, 30]  # Different initial velocities (m/s)

# Plot
plt.figure(figsize=(8, 6))
for v0 in v0_values:
    R = (v0**2 * np.sin(2 * angles_rad)) / g
    plt.plot(angles_deg, R, label=f'v₀ = {v0} m/s')

plt.title('Range vs. Angle of Projection')
plt.xlabel('Angle θ (degrees)')
plt.ylabel('Range R (m)')
plt.grid(True)
plt.legend()
plt.show()
```

![Code 2](../../_pics/Physics/1%20Mechanics/Problem_1/code_2.png)

#### Code 3: Range vs. Angle for Different Gravitational Accelerations

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
v0 = 20.0  # Initial velocity (m/s)
angles_deg = np.linspace(0, 90, 91)  # Angles from 0° to 90°
angles_rad = np.radians(angles_deg)
g_values = {'Earth': 9.81, 'Moon': 1.62, 'Mars': 3.72}  # Gravity (m/s^2)

# Plot
plt.figure(figsize=(8, 6))
for planet, g in g_values.items():
    R = (v0**2 * np.sin(2 * angles_rad)) / g
    plt.plot(angles_deg, R, label=f'{planet} (g = {g} m/s²)')

plt.title('Range vs. Angle for Different Gravities')
plt.xlabel('Angle θ (degrees)')
plt.ylabel('Range R (m)')
plt.grid(True)
plt.legend()
plt.show()
```

![Code 3](../../_pics/Physics/1%20Mechanics/Problem_1/code_3.png)

#### Code 4: Trajectory with Non-Zero Initial Height

```python
import matplotlib.pyplot as plt
import numpy as np
 
# Constants
g = 9.81  # gravity (m/s^2)
v0 = 25   # initial speed (m/s)
angle_deg = 45  # launch angle (degrees)
angle_rad = np.radians(angle_deg)
 
# Initial heights to test
initial_heights = [0, 10, 20]  # in meters
labels = [f"h0 = {h} m" for h in initial_heights]
 
# Time array
t = np.linspace(0, 5, num=500)  # simulate for 5 seconds
 
# Plotting
plt.figure(figsize=(10, 6))
for h0, label in zip(initial_heights, labels):
    # Equations of motion
    x = v0 * np.cos(angle_rad) * t
    y = h0 + v0 * np.sin(angle_rad) * t - 0.5 * g * t**2
    # Only keep points where y >= 0 (above ground)
    mask = y >= 0
    plt.plot(x[mask], y[mask], label=label)
 
plt.title("Projectile Motion for Different Initial Heights")
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.legend()
plt.grid(True)
plt.show()
```

![Code 4](../../_pics/Physics/1%20Mechanics/1%20Mechanics/Problem_1/code_4_fixed.png)

### Deliverables
- **Equations**: Derived $x(t)$, $y(t)$, and $R$.
- **Graphs**: Trajectory and $R$ vs. $\theta$ plots.
- **Limitations**: Ideal model ignores drag; extend with numerical solvers.

---

## Conclusion
The range $R = \frac{v_0^2 \sin 2\theta}{g}$ peaks at 45°, scales with $v_0^2$, and adapts to real-world factors via modifications, demonstrated through simulations.

# Colab
[Souce Code](https://colab.research.google.com/drive/1fMO_9xAKT-KOVi1EgB00NlsG1eOGbN1T?usp=sharing)