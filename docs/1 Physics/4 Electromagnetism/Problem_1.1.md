# Problem 1 (Shorted)

**Simulating the Lorentz Force**

---

## 1. Applications of the Lorentz Force

The Lorentz force law,  
$$
\mathbf{F} = q\mathbf{E} + q\mathbf{v} \times \mathbf{B},
$$  
governs the dynamics of charged particles in electric ($\mathbf{E}$) and magnetic ($\mathbf{B}$) fields.

### Key Applications:
- **Particle Accelerators**: Magnetic fields guide particles in circular paths; electric fields accelerate them.
- **Mass Spectrometers**: Different mass-to-charge ratios cause unique curvatures in magnetic fields.
- **Plasma Confinement**: Magnetic traps (e.g., tokamaks) confine charged plasma using helical motion.

| Field Setup             | Force Direction                                | Resulting Motion               |
|-------------------------|------------------------------------------------|--------------------------------|
| $\mathbf{E}$ only       | Along $\mathbf{E}$                             | Linear acceleration            |
| $\mathbf{B}$ only       | Perpendicular to $\mathbf{v}, \mathbf{B}$      | Circular/helical motion        |
| $\mathbf{E} \perp \mathbf{B}$ | Orthogonal force, causes drift              | Spiral with drift velocity     |

---

## 2. Simulating Particle Motion

### Governing Equation:
$$
m\frac{d\mathbf{v}}{dt} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})
$$

### Methods:
- **Euler Method**: Simple but less accurate for oscillatory systems.
- **Boris Algorithm**: Preserves energy in magnetic fields.
- **Runge-Kutta (RK4)**: Offers high accuracy at greater computational cost.

### Motion Types:
- **Circular**: $\mathbf{v} \perp \mathbf{B}$, no $\mathbf{E}$.
- **Helical**: $\mathbf{v}$ has parallel and perpendicular components to $\mathbf{B}$.
- **Drift**: $\mathbf{E} \perp \mathbf{B}$ causes uniform drift:
  $$
  \mathbf{v}_\text{drift} = \frac{\mathbf{E} \times \mathbf{B}}{B^2}
  $$

---

## 3. Parameter Exploration

Simulation results depend on:

- **Field Strengths**:
  - $E \rightarrow$ linear acceleration
  - $B \rightarrow$ tighter curvature, smaller Larmor radius
- **Initial Velocity**:
  - Perpendicular component: affects orbit size
  - Parallel component: affects pitch of helical motion
- **Charge $q$**:
  - Affects direction (sign) and magnitude of motion
- **Mass $m$**:
  - Heavier particles move slower, larger radius

Real-world example:  
$$
r_L = \frac{mv}{|q|B}, \quad \omega_c = \frac{|q|B}{m}
$$

---

## 4. Visualization

Visualizing charged particle trajectories under the Lorentz force helps build intuition about their motion in different electromagnetic fields. Using Python, we generate labeled 2D and 3D plots to illustrate key features like:

- **Larmor radius** $r_L$  
- **Helical pitch** (spiral spacing along field lines)  
- **Drift velocity** $\mathbf{v}_\text{drift} = \frac{\mathbf{E} \times \mathbf{B}}{B^2}$

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

### 4.3 $\mathbf{E} \times \mathbf{B}$ Drift Motion
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.animation import FuncAnimation
from IPython.display import HTML
import base64
from io import BytesIO

# Crazy Parameters
q, m = 10.0, 0.1                          # Very high charge-to-mass ratio
B = np.array([0, 0, 5.0])                # Strong magnetic field in z-direction
v0 = np.array([5.0, 0.0, 0.1])           # High x velocity, small z component for tight helix
r0 = np.array([0.0, 0.0, 0.0])
dt, T = 0.001, 5.0                       # Small dt for smooth animation
N = int(T / dt)

# Initialize arrays
r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0], v[0] = r0, v0

# Compute trajectory
for i in range(N - 1):
    F = q * np.cross(v[i], B)
    a = F / m
    v[i + 1] = v[i] + a * dt
    r[i + 1] = r[i] + v[i] * dt

# Create 3D animation
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.set_xlim(-3, 3)
ax.set_ylim(-3, 3)
ax.set_zlim(0, 5)
ax.set_title("Crazy 3D Helical Motion")
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('z')

# Line with fading color
colors = plt.cm.plasma(np.linspace(0, 1, N))
line, = ax.plot([], [], [], lw=2)
point, = ax.plot([], [], [], 'ro')  # Current position

# Plot fading trail manually with segments
def update_3d(i):
    ax.clear()
    ax.set_xlim(-3, 3)
    ax.set_ylim(-3, 3)
    ax.set_zlim(0, 5)
    ax.set_title("Crazy 3D Helical Motion")
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_zlabel('z')

    # Plot color-fading segments
    step = max(1, i // 200)
    for j in range(0, i - 1, step):
        ax.plot(r[j:j+2, 0], r[j:j+2, 1], r[j:j+2, 2], color=colors[j], lw=1)

    # Red dot for current position
    ax.plot([r[i, 0]], [r[i, 1]], [r[i, 2]], 'ro')
    return []

# Animate
ani = FuncAnimation(fig, update_3d, frames=N, interval=20, blit=False)

# Save as GIF
gif_path = 'crazy_helical_motion_v2.gif'
ani.save(gif_path, writer='pillow', fps=30)

# Display GIF in notebook
with open(gif_path, 'rb') as f:
    gif_data = f.read()
b64_gif = base64.b64encode(gif_data).decode('utf-8')
html = f'<img src="data:image/gif;base64,{b64_gif}">'
HTML(html)
```
![Crazy Helical Motion](../../_pics/Physics/4%20Electromagnetism/Problem_1/crazy_helical_motion.gif)

---

### Colab: Electromagnetism Problem 1
[Souce Code](https://colab.research.google.com/drive/16Epk_vNwaF5WNNwd9b1NzThMiUeVFneC?usp=sharing)

---

## 5. Numerical Methods Summary

- Use **Euler** for simplicity.
- Prefer **Boris** or **RK4** for accuracy and energy stability.
- Keep $\Delta t$ small enough to resolve cyclotron motion:
  $$
  \Delta t \ll \frac{2\pi m}{|q|B}
  $$