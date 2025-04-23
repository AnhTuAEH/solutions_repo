# Problem 1

## 1. Geometry Setup

To study interference patterns, we start by placing point sources at the vertices of a regular polygon.

### 1.1 Regular Polygon
A regular polygon has equal sides and angles. Let the number of sources be:
$$
N \geq 3
$$

### 1.2 Vertex Coordinates
Assume the polygon is inscribed in a circle centered at the origin with radius $R$. The angle between adjacent vertices is:
$$
\Delta \theta = \frac{2\pi}{N}, \quad \theta_i = i \Delta \theta
$$
Coordinates of the $i$-th vertex:
$$
x_{0i} = R \cos(\theta_i), \quad y_{0i} = R \sin(\theta_i)
$$

### 1.3 Choosing Radius $R$
Radius $R$ determines source spacing and pattern scale. A chord length of:
$$
d = 2R \sin\left(\frac{\pi}{N}\right)
$$
Choosing $d \sim (2-5) \lambda$ gives rich interference.

## 2. Wave Definition

Each source emits a circular wave described by:
$$
\eta_i(x, y, t) = \frac{A}{\sqrt{r_i}} \cos(k r_i - \omega t + \phi)
$$
Where $r_i = \sqrt{(x - x_{0i})^2 + (y - y_{0i})^2}$ is the distance from source $i$ to point $(x, y)$. Common assumptions:
- All sources have same $A, k, \omega, \phi$.
- Initial phase $\phi = 0$.
- Non-dispersive medium.

## 3. Superposition Principle

Total displacement:
$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \frac{A}{\sqrt{r_i}} \cos(k r_i - \omega t + \phi)
$$

### Interference Conditions
- **Constructive**: $k(r_i - r_j) = 2n\pi$
- **Destructive**: $k(r_i - r_j) = (2n + 1)\pi$

Patterns arise from the geometry and wave interactions.

## 4. Wave Parameters

- **Amplitude ($A$)**: maximum surface displacement.
- **Wavelength ($\lambda$)**: defines wave number $k = 2\pi/\lambda$.
- **Frequency ($f$)**: defines $\omega = 2\pi f$.
- **Phase ($\phi$)**: typically zero for all sources.

These define wave behavior and interference scale.

## 5. Simulation Grid

### 5.1 Domain
Choose spatial domain $[x_{\min}, x_{\max}], [y_{\min}, y_{\max}]$ large enough to capture wave effects:
$$
(x_{\max} - x_{\min}) \gtrsim 6\lambda, \quad (y_{\max} - y_{\min}) \gtrsim 6\lambda
$$

### 5.2 Resolution
Grid spacing:
$$
\Delta x, \Delta y \leq \frac{\lambda}{10}
$$
Construct grid using meshgrid in Python.

### 5.3 Boundary Effects
Keep sources away from edges. Use absorbing or periodic boundaries as needed.

## 6. Time Component

Each wave evolves in time:
$$
\eta_i(x, y, t) = \frac{A}{\sqrt{r_i}} \cos(k r_i - \omega t + \phi)
$$

### Visualization Modes
- **Snapshot**: Fixed $t = t_0$. Shows static interference.
- **Animation**: Vary $t$ over interval with step $\Delta t \leq 1/(20f)$.

Use animations or contour plots to show dynamics.

## 7. Visualization

### 7.1 Single Source – Static Wavefronts

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# Wave parameters
A = 1
lambda_ = 1
k = 2 * np.pi / lambda_
f = 1
omega = 2 * np.pi * f
phi = 0

# Grid
x = np.linspace(-5, 5, 400)
y = np.linspace(-5, 5, 400)
X, Y = np.meshgrid(x, y)
r = np.sqrt((X - 0)**2 + (Y - 0)**2)

# Setup plot
fig, ax = plt.subplots()
img = ax.imshow(np.zeros_like(X), extent=[-5, 5, -5, 5], cmap='viridis', origin='lower')
plt.colorbar(img, ax=ax)
ax.set_title("Single Source Wavefronts")

# Animation function
def update(frame):
    t = frame / 20
    eta = A / np.sqrt(r + 1e-6) * np.cos(k * r - omega * t + phi)
    img.set_data(eta)
    return [img]

ani = animation.FuncAnimation(fig, update, frames=100, interval=50, blit=True)
ani.save("single_source.gif", writer="pillow")
plt.close()
```
![Single Source 2D](../../_pics/Physics/3%20Waves/Problem_1/single_source.gif)

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.animation import FuncAnimation

# Parameters
A = 1
lambda_ = 1
k = 2 * np.pi / lambda_
f = 1
omega = 2 * np.pi * f
phi = 0

# Grid
x = np.linspace(-5, 5, 150)
y = np.linspace(-5, 5, 150)
X, Y = np.meshgrid(x, y)
r = np.sqrt((X - 0)**2 + (Y - 0)**2)

# Setup plot
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')

# Initialize the surface plot
surf = ax.plot_surface(X, Y, np.zeros_like(X), cmap='viridis', edgecolor='none')
ax.set_zlim(-2, 2)
ax.set_title("Single Source – 3D Animated Surface")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("Displacement")

def update(frame):
    global surf  # Make surf accessible within the function
    t = frame / 20
    eta = A / np.sqrt(r + 1e-6) * np.cos(k * r - omega * t + phi)

    # Remove the previous surface plot
    surf.remove()

    # Plot the new surface
    surf = ax.plot_surface(X, Y, eta, cmap='viridis', edgecolor='none')
    return [surf]  # Return the updated surface

ani = FuncAnimation(fig, update, frames=60, interval=100, blit=False) # blit=False is recommended for 3D animations
ani.save("single_source_3d.gif", writer="pillow")
plt.close()
```
![Single Source 3D](../../_pics/Physics/3%20Waves/Problem_1/single_source_3d.gif)

### 7.2 Two Sources – Interference Pattern

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# Wave parameters
A = 1
lambda_ = 1
k = 2 * np.pi / lambda_
f = 1
omega = 2 * np.pi * f
phi = 0

# Grid
x = np.linspace(-5, 5, 400)
y = np.linspace(-5, 5, 400)
X, Y = np.meshgrid(x, y)

# Two sources
sources = [(-1.5, 0), (1.5, 0)]

# Setup plot
fig, ax = plt.subplots()
img = ax.imshow(np.zeros_like(X), extent=[-5, 5, -5, 5], cmap='plasma', origin='lower')
plt.colorbar(img, ax=ax)
ax.set_title("Two Source Interference")

def update(frame):
    t = frame / 20
    eta_sum = np.zeros_like(X)
    for x0, y0 in sources:
        r = np.sqrt((X - x0)**2 + (Y - y0)**2)
        eta_sum += A / np.sqrt(r + 1e-6) * np.cos(k * r - omega * t + phi)
    img.set_data(eta_sum)
    return [img]

ani = animation.FuncAnimation(fig, update, frames=100, interval=50, blit=True)
ani.save("two_sources.gif", writer="pillow")
plt.close()
```
![Two Sources 2D](../../_pics/Physics/3%20Waves/Problem_1/two_sources.gif)

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.animation import FuncAnimation

# Parameters
A = 1
lambda_ = 1
k = 2 * np.pi / lambda_
f = 1
omega = 2 * np.pi * f
phi = 0

# Grid
x = np.linspace(-5, 5, 150)
y = np.linspace(-5, 5, 150)
X, Y = np.meshgrid(x, y)

# Two source coordinates
sources = [(-1.5, 0), (1.5, 0)]

fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
ax.set_zlim(-3, 3)
ax.set_title("Two Sources – 3D Animated Surface")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("Displacement")

# Initialize the surface plot outside the update function
surf = ax.plot_surface(X, Y, np.zeros_like(X), cmap='plasma', edgecolor='none')

def update(frame):
    global surf  # Make surf accessible within the function
    t = frame / 20
    eta_sum = np.zeros_like(X)
    for x0, y0 in sources:
        r = np.sqrt((X - x0)**2 + (Y - y0)**2)
        eta_sum += A / np.sqrt(r + 1e-6) * np.cos(k * r - omega * t + phi)

    # Remove the previous surface plot
    surf.remove()

    # Plot the new surface
    surf = ax.plot_surface(X, Y, eta_sum, cmap='plasma', edgecolor='none')
    return [surf]  # Return the updated surface

ani = FuncAnimation(fig, update, frames=60, interval=100, blit=False) # blit=False is recommended for 3D animations
ani.save("two_sources_3d.gif", writer="pillow")
plt.close()
```
![Two Sources 3D](../../_pics/Physics/3%20Waves/Problem_1/two_sources_3d.gif)

### 7.3 Three Sources – Interference from Triangle Configuration

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# Wave parameters
A = 1
lambda_ = 1
k = 2 * np.pi / lambda_
f = 1
omega = 2 * np.pi * f
phi = 0

# Grid
x = np.linspace(-5, 5, 400)
y = np.linspace(-5, 5, 400)
X, Y = np.meshgrid(x, y)

# Triangle config
R = 2
sources = [(R * np.cos(2*np.pi*i/3), R * np.sin(2*np.pi*i/3)) for i in range(3)]

fig, ax = plt.subplots()
img = ax.imshow(np.zeros_like(X), extent=[-5, 5, -5, 5], cmap='inferno', origin='lower')
plt.colorbar(img, ax=ax)
ax.set_title("Triangle Interference – Three Sources")

def update(frame):
    t = frame / 20
    eta_sum = np.zeros_like(X)
    for x0, y0 in sources:
        r = np.sqrt((X - x0)**2 + (Y - y0)**2)
        eta_sum += A / np.sqrt(r + 1e-6) * np.cos(k * r - omega * t + phi)
    img.set_data(eta_sum)
    return [img]

ani = animation.FuncAnimation(fig, update, frames=100, interval=50, blit=True)
ani.save("three_sources.gif", writer="pillow")
plt.close()
```
![Three Sources 2D](../../_pics/Physics/3%20Waves/Problem_1/three_sources.gif)

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.animation import FuncAnimation

# Parameters
A = 1
lambda_ = 1
k = 2 * np.pi / lambda_
f = 1
omega = 2 * np.pi * f
phi = 0

# Grid
x = np.linspace(-5, 5, 150)
y = np.linspace(-5, 5, 150)
X, Y = np.meshgrid(x, y)

# Triangle configuration
R = 2
sources = [(R * np.cos(2 * np.pi * i / 3), R * np.sin(2 * np.pi * i / 3)) for i in range(3)]

fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
ax.set_zlim(-3, 3)
ax.set_title("Three Sources – 3D Animated Surface")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("Displacement")

# Initialize surface plot
surf = ax.plot_surface(X, Y, np.zeros_like(X), cmap='inferno', edgecolor='none')

def update(frame):
    global surf  # Make surf accessible within the function
    t = frame / 20
    eta_sum = np.zeros_like(X)
    for x0, y0 in sources:
        r = np.sqrt((X - x0)**2 + (Y - y0)**2)
        eta_sum += A / np.sqrt(r + 1e-6) * np.cos(k * r - omega * t + phi)

    # Remove the previous surface plot
    surf.remove()

    # Plot the new surface
    surf = ax.plot_surface(X, Y, eta_sum, cmap='inferno', edgecolor='none')
    return [surf]

ani = FuncAnimation(fig, update, frames=60, interval=100, blit=False) # blit=False is important for 3D animations
ani.save("three_sources_3d.gif", writer="pillow")
plt.close()
```
![Three Sources 3D](../../_pics/Physics/3%20Waves/Problem_1/three_sources_3d.gif)

### Colab: Waves: Problem 1
[Souce Code](https://colab.research.google.com/drive/1QYGANHK5S8mYIYQiMliTVS6BT689dSWk?usp=sharing)

## 8. Analysis

Analyzing the resulting interference pattern reveals regions of amplification and cancellation.

### 8.1 Constructive Interference
Occurs when waves are in phase:
$$
k(r_i - r_j) = 2\pi n
$$
Leads to high displacement regions (bright fringes or peaks).

### 8.2 Destructive Interference
Occurs when waves are out of phase:
$$
k(r_i - r_j) = (2n + 1)\pi
$$
Leads to wave cancellation (dark zones or troughs).

### 8.3 Pattern Symmetry
Pattern symmetry follows the polygon's geometry:
- Two sources: symmetry about midpoint.
- Three (triangle): $120^\circ$ rotational symmetry.
- Four or more: increasing complexity, matching polygonal symmetry.

### 8.4 Visual Cues
- Bright ridges = constructive zones
- Dark lines = destructive zones
- Radial or rotational motifs reflect geometric layout

Contours or threshold filters can aid interpretation.

