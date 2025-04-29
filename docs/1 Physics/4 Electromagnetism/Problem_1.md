# Problem 1

**Simulating the Lorentz Force**

## 1. Exploration of Applications

The **Lorentz force** describes the motion of a charged particle under the influence of **electric** and **magnetic fields**, and is one of the cornerstones of classical and modern electromagnetism.

### 1.1 Fundamental Equation

The Lorentz force acting on a particle of charge $q$ moving with velocity $\mathbf{v}$ in an electric field $\mathbf{E}$ and magnetic field $\mathbf{B}$ is given by:

$$
\mathbf{F} = q\mathbf{E} + q\mathbf{v} \times \mathbf{B}
$$

This vector equation has two key components:

- The **electric force**: $q\mathbf{E}$, which acts in the direction of the electric field.
- The **magnetic force**: $q\mathbf{v} \times \mathbf{B}$, which acts perpendicular to both the velocity of the particle and the magnetic field.

---

### 1.2 Real-World Applications

The Lorentz force plays a pivotal role in several technological and scientific domains:

#### • Particle Accelerators

In **cyclotrons**, **synchrotrons**, and **linear accelerators**, particles are steered and accelerated using electromagnetic fields.

- Magnetic fields enforce circular or helical motion:
  $$
  r = \frac{mv}{|q|B}
  $$

- Electric fields provide kinetic energy:
  $$
  \Delta K = qEd
  $$

#### • Mass Spectrometers

Used in chemistry and physics to identify atoms and molecules based on their mass-to-charge ratio.

#### • Plasma Confinement (Fusion Reactors)

In **tokamaks** and **stellarators**, magnetic fields confine high-energy plasma in a donut-shaped chamber.

---

### 1.3 Summary of Field Effects

| Field Type         | Direction of Force                | Effect on Motion                          |
|--------------------|----------------------------------|-------------------------------------------|
| $\mathbf{E}$ only  | Parallel to $\mathbf{E}$         | Linear acceleration or deceleration       |
| $\mathbf{B}$ only  | Perpendicular to $\mathbf{v}$ and $\mathbf{B}$ | Circular or helical motion       |
| $\mathbf{E} \perp \mathbf{B}$ | Orthogonal force due to $\mathbf{v} \times \mathbf{B}$ | Drift or spiral trajectories     |

## 2. Simulating Particle Motion

### 2.1 Governing Equation

$$
\mathbf{F} = m \frac{d\mathbf{v}}{dt} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})
$$

### 2.2 Numerical Implementation

Euler method used initially:
$$
\mathbf{v}_{n+1} = \mathbf{v}_n + \frac{q}{m}(\mathbf{E} + \mathbf{v}_n \times \mathbf{B})\Delta t
$$
$$
\mathbf{r}_{n+1} = \mathbf{r}_n + \mathbf{v}_n \Delta t
$$

---

### 2.4 Boris Algorithm Implementation (Alternative to Euler)

```python
# Boris algorithm for stable motion in magnetic fields
q, m = 1.0, 1.0
B = np.array([0, 0, 1.0])
E = np.array([0.0, 0.0, 0.0])
v0 = np.array([1.0, 0.0, 0.0])
r0 = np.array([0.0, 0.0, 0.0])
dt, T = 0.01, 10
N = int(T / dt)

r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0], v[0] = r0, v0

t = (q * B / m) * (dt / 2)
t_mag2 = np.dot(t, t)
s = 2 * t / (1 + t_mag2)

for i in range(N - 1):
    v_minus = v[i] + (q * E / m) * (dt / 2)
    v_prime = v_minus + np.cross(v_minus, t)
    v_plus = v_minus + np.cross(v_prime, s)
    v[i + 1] = v_plus + (q * E / m) * (dt / 2)
    r[i + 1] = r[i] + v[i + 1] * dt
```

---

### 2.5 Types of Motion

#### • Circular Motion

Occurs when:
- $\mathbf{E} = 0$
- $\mathbf{v} \perp \mathbf{B}$

Result:
- Constant-speed circular motion in the plane perpendicular to $\mathbf{B}$

#### • Helical Motion

Occurs when:
- $\mathbf{v}$ has both parallel and perpendicular components with respect to $\mathbf{B}$
- $\mathbf{E} = 0$ or parallel to $\mathbf{B}$

Result:
- Particle moves in a **spiral** (helix) along field lines with pitch determined by $v_\parallel$

#### • Drift Motion

Occurs under:
- $\mathbf{E} \perp \mathbf{B}$

Result:
- Circular/helical motion superimposed with **uniform drift**:

  $$
  \mathbf{v}_\text{drift} = \frac{\mathbf{E} \times \mathbf{B}}{B^2}
  $$

---

These simulations are vital in visualizing how charged particles behave in various field environments, providing insights into devices such as **mass spectrometers**, **magnetic confinement systems**, and **beam control in accelerators**.

---

## 3. Parameter Exploration

The dynamics of charged particles under the Lorentz force are highly sensitive to physical parameters. Exploring variations in these parameters allows us to understand how they shape the trajectory and motion characteristics such as speed, curvature, and drift.

The Lorentz force remains our starting point:

$$
\mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})
$$

This governs the acceleration and thus the trajectory of the particle according to Newton's second law:

$$
\mathbf{F} = m \frac{d\mathbf{v}}{dt}
$$

---

### 3.1 Key Parameters and Their Effects

#### • Electric Field Strength ($E$)

The electric field contributes directly to **linear acceleration**:

$$
\mathbf{a}_E = \frac{q\mathbf{E}}{m}
$$

- **Stronger $E$** leads to higher linear acceleration.
- Dominant in configurations where $\mathbf{B} = 0$ or $\mathbf{v} \parallel \mathbf{E}$.
- In combined fields, $E$ affects **drift velocity** and can induce **helical stretching**.

---

#### • Magnetic Field Strength ($B$)

The magnetic component of the Lorentz force is velocity-dependent:

$$
\mathbf{F}_B = q(\mathbf{v} \times \mathbf{B})
$$

- **Stronger $B$** increases the curvature of motion.
- In pure $\mathbf{B}$ fields, it reduces the **Larmor radius**:

  $$
  r_L = \frac{mv_\perp}{|q|B}
  $$

- It also increases the **gyrofrequency**:

  $$
  \omega_c = \frac{|q|B}{m}
  $$

  where $\omega_c$ is the **cyclotron frequency**.

---

#### • Initial Velocity ($\mathbf{v}$)

- The direction and magnitude of initial velocity define the **geometry** of motion:
  - Perpendicular to $\mathbf{B}$ $\rightarrow$ circular motion
  - Parallel to $\mathbf{B}$ $\rightarrow$ linear motion
  - Mixed components $\rightarrow$ helical motion

- **Magnitude** affects:
  - Radius of curvature ($r_L$ increases with $v_\perp$)
  - Speed of drift in crossed fields:

    $$
    \mathbf{v}_\text{drift} = \frac{\mathbf{E} \times \mathbf{B}}{B^2}
    $$

---

#### • Particle Charge ($q$)

Charge affects both magnitude and direction of the Lorentz force:

- **Sign of $q$** reverses the direction of the magnetic force:

  $$
  \text{If } q > 0: \text{ right-hand rule applies} \\
  \text{If } q < 0: \text{ reverse direction (left-hand motion)}
  $$

- Affects radius and frequency as:

  $$
  r_L \propto \frac{1}{|q|}, \quad \omega_c \propto |q|
  $$

---

#### • Particle Mass ($m$)

- **Inversely proportional** to acceleration for a given force:

  $$
  \mathbf{a} = \frac{\mathbf{F}}{m}
  $$

- Affects Larmor radius and cyclotron frequency:

  $$
  r_L \propto m, \quad \omega_c \propto \frac{1}{m}
  $$

Heavier particles exhibit **larger orbits** and **slower rotation** under the same field conditions.

---

### 3.2 Visual Exploration Goals

By varying the above parameters in simulations, one should:

- **Track trajectory changes**: curvature, helical pitch, drift.
- **Compare motion types**: linear vs circular vs spiral.
- **Identify scaling laws** for:
  - Larmor radius: $r_L = \frac{mv_\perp}{|q|B}$
  - Cyclotron frequency: $\omega_c = \frac{|q|B}{m}$

Parameter exploration is essential for tuning real-world applications, from optimizing cyclotron paths to designing magnetic traps and beamlines.

---

### 3.3 Real-World System Example: Cyclotron Motion

Proton in a cyclotron:
- $B = 1\ \text{T}$
- $v = 1 \times 10^6\ \text{m/s}$

Larmor radius:
$$
    r_L = \frac{mv}{|q|B} = \frac{1.67 \times 10^{-27} \cdot 10^6}{1.6 \times 10^{-19} \cdot 1} \approx 0.0104\ \text{m}
$$

---

### 3.4 Interactive Parameter Exploration (Optional for Jupyter/Colab)

```python
import ipywidgets as widgets
from IPython.display import display

def update_simulation(B_field=1.0, velocity=1.0):
    # Call a simulation function with updated B and v
    pass

display(widgets.FloatSlider(value=1.0, min=0.1, max=5.0, step=0.1, description='B Field'))
display(widgets.FloatSlider(value=1.0, min=0.1, max=5.0, step=0.1, description='Velocity'))
```

---

## 4. Visualization

Visualizing charged particle trajectories under the Lorentz force is critical for developing intuition about their motion in various electromagnetic field configurations. In this section, we use Python and standard scientific libraries to produce labeled, informative 2D and 3D plots that illustrate:

- **Larmor radius** $r_L$
- **Helical pitch** (distance between spiral turns along the field direction)
- **Drift velocity** $\mathbf{v}_\text{drift} = \frac{\mathbf{E} \times \mathbf{B}}{B^2}$

---

### 4.1 Circular Motion in \(xy\)-Plane

Charged particle moves in a circle under a uniform magnetic field ($\mathbf{B}$ along $z$). No electric field; pure cyclotron motion with constant radius and speed.

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

# Parameters
q, m = 1.0, 1.0
B = np.array([0, 0, 1.0])
v0 = np.array([1.0, 0.0, 0.0])
r0 = np.array([0.0, 0.0, 0.0])
dt, T = 0.01, 10
N = int(T / dt)

# Calculate trajectory
r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0], v[0] = r0, v0

for i in range(N - 1):
    F = q * np.cross(v[i], B)
    a = F / m
    v[i + 1] = v[i] + a * dt
    r[i + 1] = r[i] + v[i] * dt

# Create animation
fig, ax = plt.subplots()
ax.set_xlim(-2, 2)
ax.set_ylim(-2, 2)
ax.set_aspect('equal')
line, = ax.plot([], [], lw=2)
point, = ax.plot([], [], 'ro')

def update(i):
    line.set_data(r[:i + 1, 0], r[:i + 1, 1])  # Trajectory line
    point.set_data([r[i, 0]], [r[i, 1]])       # Current point (wrapped in lists)
    return line, point

# Create animation
ani = FuncAnimation(fig, update, frames=N - 1, interval=30, blit=True)

# Display animation inline in Jupyter Notebook
plt.title("Circular Motion in xy-plane (Animated)")
plt.xlabel('x')
plt.ylabel('y')
# plt.grid(True)
# plt.show()

# Save animation as GIF
gif_path = 'circular_motion.gif'
ani.save(gif_path, writer='pillow', fps=30)


# Display GIF in Colab using HTML
with open(gif_path, 'rb') as f:
    gif_data = f.read()
b64_gif = base64.b64encode(gif_data).decode('utf-8')
html = f'<img src="data:image/gif;base64,{b64_gif}">'
HTML(html)
```
![Circular Motion](../../_pics/Physics/4%20Electromagnetism/Problem_1/circular_motion.gif)

---

### 4.2 3D Helical Motion

Particle follows a helical path due to velocity components both parallel and perpendicular to $\mathbf{B}$. Circular motion + forward motion along field lines.

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.animation import FuncAnimation
from IPython.display import HTML
import base64
from io import BytesIO

# Parameters
q, m = 1.0, 1.0
B = np.array([0, 0, 1.0])
v0 = np.array([1.0, 0.0, 0.5])  # Initial velocity with z-component for helical motion
r0 = np.array([0.0, 0.0, 0.0])
dt, T = 0.01, 10
N = int(T / dt)

# Calculate trajectory
r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0], v[0] = r0, v0

for i in range(N - 1):
    F = q * np.cross(v[i], B)
    a = F / m
    v[i + 1] = v[i] + a * dt
    r[i + 1] = r[i] + v[i] * dt

# Create 3D animation
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.set_xlim(-2, 2)
ax.set_ylim(-2, 2)
ax.set_zlim(0, 6)
line, = ax.plot([], [], [], lw=2)
point, = ax.plot([], [], [], 'ro')

def update_3d(i):
    # Update line (trajectory)
    line.set_data(r[:i, 0], r[:i, 1])
    line.set_3d_properties(r[:i, 2])
    # Update point (current position)
    point.set_data([r[i, 0]], [r[i, 1]])  # Wrap in lists to provide sequences
    point.set_3d_properties([r[i, 2]])    # Wrap in list to provide sequence
    return line, point

# Create animation
ani = FuncAnimation(fig, update_3d, frames=N - 1, interval=30, blit=False)  # blit=False for 3D

# Set plot labels and title
ax.set_title("3D Helical Motion (Animated)")
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('z')

# Save animation as GIF
gif_path = 'helical_motion.gif'
ani.save(gif_path, writer='pillow', fps=30)

# Display GIF in Colab using HTML
with open(gif_path, 'rb') as f:
    gif_data = f.read()
b64_gif = base64.b64encode(gif_data).decode('utf-8')
html = f'<img src="data:image/gif;base64,{b64_gif}">'
HTML(html)
```
![Helical Motion](../../_pics/Physics/4%20Electromagnetism/Problem_1/helical_motion.gif)

---

### 4.3 $\mathbf{E} \times \mathbf{B}$ Drift Motion

In crossed electric and magnetic fields, the particle spirals while drifting uniformly perpendicular to both $\mathbf{E}$ and $\mathbf{B}$.

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
from IPython.display import HTML
import base64
from io import BytesIO

# Parameters
q, m = 1.0, 1.0
E = np.array([1.0, 0.0, 0.0])  # Electric field
B = np.array([0.0, 0.0, 1.0])  # Magnetic field
r0 = np.array([0.0, 0.0, 0.0])
v0 = np.array([0.5, 0.0, 0.0])  # Initial velocity
dt, T = 0.01, 10
N = int(T / dt)

# Calculate trajectory
r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0], v[0] = r0, v0

for i in range(N - 1):
    F = q * (E + np.cross(v[i], B))  # Lorentz force with E and B fields
    a = F / m
    v[i + 1] = v[i] + a * dt
    r[i + 1] = r[i] + v[i] * dt

# Calculate E × B drift
drift = np.cross(E, B) / np.dot(B, B)  # Drift velocity: (E × B) / |B|^2

# Create 2D animation
fig, ax = plt.subplots()
ax.set_xlim(0, 10)
ax.set_ylim(-2, 2)
ax.set_aspect('equal')
line, = ax.plot([], [], lw=2, label='Trajectory')
point, = ax.plot([], [], 'ro', label='Particle')
drift_line, = ax.plot([], [], 'r--', label='Drift')

def update_drift(i):
    # Update trajectory line
    line.set_data(r[:i, 0], r[:i, 1])
    # Update particle position
    point.set_data([r[i, 0]], [r[i, 1]])  # Wrap in lists to provide sequences
    # Update drift line
    if i > 1:  # Ensure enough points for linspace
        t = np.linspace(0, r[i, 0], 50)  # Use fixed number of points for smoothness
        drift_y = drift[1] * t + r[0, 1]  # Drift along y-axis
        drift_line.set_data(t, drift_y)
    else:
        drift_line.set_data([], [])  # Empty data for initial frames
    return line, point, drift_line

# Create animation
ani = FuncAnimation(fig, update_drift, frames=N - 1, interval=30, blit=True)

# Set plot labels, title, and legend
plt.title("Drift Motion in Crossed E × B Fields (Animated)")
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.legend()

# Save animation as GIF
gif_path = 'drift_motion.gif'
ani.save(gif_path, writer='pillow', fps=30)

# Display GIF in Colab using HTML
with open(gif_path, 'rb') as f:
    gif_data = f.read()
b64_gif = base64.b64encode(gif_data).decode('utf-8')
html = f'<img src="data:image/gif;base64,{b64_gif}">'
HTML(html)
```
![Drift Motion](../../_pics/Physics/4%20Electromagnetism/Problem_1/drift_motion.gif)

---

### Colab: Electromagnetism Problem 1
[Souce Code](https://colab.research.google.com/drive/16Epk_vNwaF5WNNwd9b1NzThMiUeVFneC?usp=sharing)

---

### Summary of Visual Insights

- **Larmor radius** is determined by the perpendicular velocity component and magnetic field:
  
  $$
  r_L = \frac{mv_\perp}{|q|B}
  $$

- **Helical pitch** corresponds to the distance moved in the field direction per revolution:

  $$
  \text{Pitch} = v_\parallel T = \frac{2\pi m v_\parallel}{|q|B}
  $$

- **Drift velocity** from crossed fields appears as a linear translation of the helix:

  $$
  \mathbf{v}_{\text{drift}} = \frac{\mathbf{E} \times \mathbf{B}}{B^2}
  $$

These visualizations provide powerful tools to explore particle behavior and validate analytic predictions.

## 5. Numerical Implementation

Simulating the motion of charged particles under electromagnetic forces involves solving **ordinary differential equations (ODEs)** derived from the **Lorentz force law**:

$$
\mathbf{F} = m\frac{d\mathbf{v}}{dt} = q\left( \mathbf{E} + \mathbf{v} \times \mathbf{B} \right)
$$

This gives a coupled system of first-order ODEs:

$$
\frac{d\mathbf{v}}{dt} = \frac{q}{m}(\mathbf{E} + \mathbf{v} \times \mathbf{B}), \quad \frac{d\mathbf{r}}{dt} = \mathbf{v}
$$

These equations are **nonlinear** and cannot usually be solved analytically. Therefore, we use numerical methods.

---

### Euler Method (First-Order Approximation)

The **Euler method** is the simplest approach, using forward differences:

$$
\mathbf{v}_{n+1} = \mathbf{v}_n + \frac{q}{m}(\mathbf{E} + \mathbf{v}_n \times \mathbf{B})\Delta t
$$

$$
\mathbf{r}_{n+1} = \mathbf{r}_n + \mathbf{v}_n \Delta t
$$

- **Pros**: Easy to implement  
- **Cons**: Low accuracy, error grows with time, unstable for stiff or oscillatory systems

---

### Runge-Kutta Method (4th Order, RK4)

The **RK4 method** offers a much more accurate solution. It approximates the next state using intermediate "slopes":

Let $\mathbf{f}(t, \mathbf{y})$ be the derivative function for velocity and position:

1. Compute intermediate steps:
   $$
   \begin{aligned}
   \mathbf{k}_1 &= f(t_n, \mathbf{y}_n) \\
   \mathbf{k}_2 &= f(t_n + \frac{\Delta t}{2}, \mathbf{y}_n + \frac{\Delta t}{2} \mathbf{k}_1) \\
   \mathbf{k}_3 &= f(t_n + \frac{\Delta t}{2}, \mathbf{y}_n + \frac{\Delta t}{2} \mathbf{k}_2) \\
   \mathbf{k}_4 &= f(t_n + \Delta t, \mathbf{y}_n + \Delta t \mathbf{k}_3)
   \end{aligned}
   $$

2. Update the solution:
   $$
   \mathbf{y}_{n+1} = \mathbf{y}_n + \frac{\Delta t}{6}(\mathbf{k}_1 + 2\mathbf{k}_2 + 2\mathbf{k}_3 + \mathbf{k}_4)
   $$

Where $\mathbf{y}$ can represent either $\mathbf{r}$ or $\mathbf{v}$.

- **Pros**: Much more accurate and stable than Euler, handles oscillatory behavior well
- **Cons**: More computationally expensive

---

### Recommendation

- Use **Euler method** for quick visualizations or conceptual understanding.
- Use **RK4** or the **Boris method** for precision and stability in realistic physics simulations (e.g., plasma modeling, cyclotron motion, fusion confinement).

---

### Numerical Stability

Time step size $\Delta t$ must be small enough to resolve **gyro-motion**:

$$
\Delta t \ll \frac{2\pi m}{|q|B} = T_{\text{cyclotron}}
$$

Choosing too large a step causes inaccurate or even unstable results.
