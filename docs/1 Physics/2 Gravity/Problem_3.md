# Problem 3

## 1. Physics and Mathematical Foundations

### 1.1 Newton’s Law of Gravitation

Newton’s Law of Gravitation states that every mass attracts every other mass with a force $F$ given by:

$$
F = G \frac{m_1 m_2}{r^2}
$$

where:
- $F$ is the gravitational force,
- $G$ is the gravitational constant ($G \approx 6.67430 \times 10^{-11} \, \text{m}^3 \text{kg}^{-1} \text{s}^{-2}$),
- $m_1$ and $m_2$ are the masses of the two objects,
- $r$ is the distance between the centers of the two masses.

The gravitational force acts along the line joining the two masses.

---

### 1.2 Newton’s Second Law Applied to Gravity

Newton's Second Law states that the force on an object is proportional to its acceleration:

$$
\vec{F} = m \vec{a}
$$

Applying this to gravitational force:

$$
m \vec{a} = -G \frac{M m}{r^2} \hat{r}
$$

Simplifying:

$$
\vec{a} = -G \frac{M}{r^2} \hat{r}
$$

where:
- $\vec{a}$ is the acceleration vector,
- $M$ is the mass of the Earth,
- $\hat{r}$ is the unit vector pointing from the payload to the Earth's center.

This acceleration governs the motion of a freely falling payload near Earth.

---

### 1.3 Conic Sections and Trajectory Classification

The path followed by the payload is a conic section determined by the total specific mechanical energy $\varepsilon$:

$$
\varepsilon = \frac{v^2}{2} - \frac{GM}{r}
$$

where:
- $v$ is the magnitude of velocity,
- $r$ is the radial distance from Earth's center.

The type of trajectory depends on $\varepsilon$:
- If $\varepsilon < 0$, the trajectory is **elliptical** (bound orbit).
- If $\varepsilon = 0$, the trajectory is **parabolic** (escape at exactly escape velocity).
- If $\varepsilon > 0$, the trajectory is **hyperbolic** (escape with surplus energy).

The general equation for conic sections in polar coordinates:

$$
r(\theta) = \frac{p}{1 + e \cos(\theta)}
$$

where:
- $p$ is the semi-latus rectum,
- $e$ is the eccentricity:
  - $0 \leq e < 1$ for an ellipse,
  - $e = 1$ for a parabola,
  - $e > 1$ for a hyperbola.

---

### 1.4 Orbital Energy (Specific Mechanical Energy)

Specific mechanical energy $\varepsilon$ combines kinetic and potential energy per unit mass:

$$
\varepsilon = \frac{v^2}{2} - \frac{GM}{r}
$$

where:
- Positive $\varepsilon$ implies unbound (hyperbolic) motion,
- Zero $\varepsilon$ corresponds to parabolic escape,
- Negative $\varepsilon$ indicates a bound (elliptical) orbit.

The escape velocity $v_{\text{esc}}$ is derived by setting $\varepsilon = 0$:

$$
v_{\text{esc}} = \sqrt{\frac{2GM}{r}}
$$

Thus, if the initial velocity $v > v_{\text{esc}}$, the payload will escape Earth’s gravity.

---

### 1.5 Kepler’s Laws of Planetary Motion

1. **First Law (Law of Ellipses)**:
   Every orbit of a planet or object is an ellipse with the center of mass at one of the two foci.

2. **Second Law (Law of Equal Areas)**:
   A line joining a planet and the Sun sweeps out equal areas during equal intervals of time.
   
   Mathematically:

   $$
   \frac{dA}{dt} = \text{constant}
   $$

   where $A$ is the area swept out.

3. **Third Law (Law of Harmonies)**:
   The square of the orbital period $T$ is proportional to the cube of the semi-major axis $a$:

   $$
   T^2 \propto a^3
   $$

   or more precisely:

   $$
   T^2 = \frac{4\pi^2}{GM} a^3
   $$

These laws govern the orbital behavior of payloads near Earth and help predict future positions and velocities.

## 2. Identify and Define Initial Conditions

To model and simulate the trajectory of a payload released near Earth, it is essential to specify the initial conditions precisely. These parameters determine the entire motion under gravitational forces.

---

### 2.1 Initial Position (Vector Relative to Earth’s Center)

The initial position $\vec{r}_0$ of the payload is given relative to the center of Earth:

$$
\vec{r}_0 = (x_0, y_0, z_0)
$$

where:
- $x_0$, $y_0$, and $z_0$ are the Cartesian coordinates of the payload in an inertial reference frame,
- Alternatively, the position can be expressed in polar coordinates $(r_0, \theta_0, \phi_0)$:
  - $r_0$ is the radial distance from Earth's center,
  - $\theta_0$ is the azimuthal angle (longitude),
  - $\phi_0$ is the polar angle (colatitude).

For many problems, assuming motion in a plane (e.g., equatorial plane) simplifies calculations by setting $z_0 = 0$.

---

### 2.2 Initial Velocity (Vector at Release)

The initial velocity $\vec{v}_0$ of the payload must be defined with both magnitude and direction:

$$
\vec{v}_0 = (v_{x,0}, v_{y,0}, v_{z,0})
$$

or alternatively in polar terms:

$$
\vec{v}_0 = v_{r,0} \hat{r} + v_{\theta,0} \hat{\theta}
$$

where:
- $v_{r,0}$ is the radial component (along $\hat{r}$),
- $v_{\theta,0}$ is the transverse component (perpendicular to $\hat{r}$ in the orbital plane).

The **initial velocity vector** relative to the local horizontal critically determines the type of trajectory:
- **Purely radial** launch ($v_{\theta,0} = 0$) results in a straight path,
- **Purely tangential** launch ($v_{r,0} = 0$) can lead to circular or elliptical orbits,
- **Mixed** radial and tangential velocities create general elliptical, hyperbolic, or parabolic paths.

---

### 2.3 Initial Altitude Above Earth’s Surface

The altitude $h_0$ is the height of the payload above the Earth's surface:

$$
h_0 = r_0 - R_E
$$

where:
- $r_0$ is the distance from the Earth's center,
- $R_E$ is the radius of the Earth ($R_E \approx 6371 \, \text{km}$).

The altitude is crucial because it influences the local gravitational force magnitude.

The local gravitational acceleration $g(h)$ at altitude $h$ is given by:

$$
g(h) = \frac{GM}{(R_E + h)^2}
$$

---

### 2.4 Gravitational Parameter of Earth (GM Value)

The gravitational parameter $\mu$ (also called standard gravitational parameter) is defined as:

$$
\mu = GM
$$

where:
- $G$ is the gravitational constant,
- $M$ is the mass of the Earth.

Numerically:

$$
\mu \approx 3.986 \times 10^{14} \, \text{m}^3 \, \text{s}^{-2}
$$

Using $\mu$ simplifies many orbital mechanics equations, for instance:

- Specific mechanical energy:

$$
\varepsilon = \frac{v^2}{2} - \frac{\mu}{r}
$$

- Orbital velocity at a distance $r$ for circular orbit:

$$
v_{\text{circ}} = \sqrt{\frac{\mu}{r}}
$$

- Escape velocity from distance $r$:

$$
v_{\text{esc}} = \sqrt{\frac{2\mu}{r}}
$$

Knowledge of $\mu$ enables precise calculations of the payload’s motion and trajectory classification.

## 3. Trajectory Analysis

Understanding the trajectory of a payload released near Earth involves deriving its equations of motion under gravitational forces, analyzing specific orbital energy, and considering the influence of initial velocity magnitude and direction.

---

### 3.1 Equations of Motion (Second-Order Differential Equations)

The motion of a payload under Earth's gravity is governed by Newton’s Second Law:

$$
\vec{F} = m \vec{a}
$$

Substituting the gravitational force:

$$
m \vec{a} = -G \frac{Mm}{r^2} \hat{r}
$$

Simplifying:

$$
\vec{a} = -\frac{\mu}{r^2} \hat{r}
$$

where $\mu = GM$ is the standard gravitational parameter.

In Cartesian coordinates $(x, y, z)$, the second-order differential equations of motion are:

$$
\ddot{x} = -\frac{\mu x}{(x^2 + y^2 + z^2)^{3/2}}
$$

$$
\ddot{y} = -\frac{\mu y}{(x^2 + y^2 + z^2)^{3/2}}
$$

$$
\ddot{z} = -\frac{\mu z}{(x^2 + y^2 + z^2)^{3/2}}
$$

where $\ddot{x}$, $\ddot{y}$, and $\ddot{z}$ are the second derivatives of position with respect to time (accelerations).

These equations describe the continuous motion of the payload influenced solely by Earth's gravitational field.

---

### 3.2 Specific Orbital Energy and Trajectory Classification

The **specific mechanical energy** $\varepsilon$ is the sum of the specific kinetic and specific potential energies:

$$
\varepsilon = \frac{v^2}{2} - \frac{\mu}{r}
$$

where:
- $v$ is the magnitude of the velocity vector,
- $r$ is the radial distance from Earth's center.

**Classification based on $\varepsilon$:**
- **Elliptical Orbit (Bound)**:
  
  $$
  \varepsilon < 0
  $$

  The payload remains gravitationally bound to Earth, following a closed, elliptical path.

- **Parabolic Trajectory (Escape at Minimum Energy)**:

  $$
  \varepsilon = 0
  $$

  The payload reaches exactly escape velocity and follows a parabolic trajectory, escaping Earth's gravity without excess energy.

- **Hyperbolic Trajectory (Escape with Excess Energy)**:

  $$
  \varepsilon > 0
  $$

  The payload escapes Earth's gravity with surplus kinetic energy, following an open hyperbolic path.

---

### 3.3 Effect of Initial Velocity Direction and Magnitude

The initial velocity $\vec{v}_0$ relative to the local horizontal plane significantly influences the resulting trajectory:

- **Purely Horizontal Launch**:
  - When the velocity is tangential to the surface (local horizontal),
  - Enables orbital motion (circular or elliptical) if the speed is appropriate.
  
- **Purely Radial Launch**:
  - When the velocity is directed straight outward or inward,
  - Leads to vertical ascent or descent,
  - If $v_0 \geq v_{\text{esc}}$, the object escapes along a parabolic or hyperbolic path.

- **Mixed Direction Launch**:
  - A combination of radial and tangential components,
  - Creates general elliptical or hyperbolic trajectories,
  - The trajectory’s shape and energy depend on the proportion of radial versus tangential velocity components.

#### Decomposition of Initial Velocity:

Given an angle $\alpha$ between the initial velocity vector and the local horizontal:

$$
v_{r,0} = v_0 \sin(\alpha)
$$

$$
v_{\theta,0} = v_0 \cos(\alpha)
$$

where:
- $v_{r,0}$ is the initial radial velocity component,
- $v_{\theta,0}$ is the initial tangential (horizontal) velocity component.

The effective orbital behavior thus depends on both the **magnitude** and the **angle** of the initial velocity.

---

### 3.4 Summary

Accurately setting up the equations of motion and understanding specific orbital energy are fundamental for classifying the payload’s trajectory after release. The initial velocity vector’s magnitude and direction relative to the local horizontal critically determine whether the payload will:
- Remain in orbit,
- Fall back to Earth,
- Escape Earth's gravitational influence entirely.

## 4. Numerical Simulation Setup

Numerical simulations are essential for modeling the trajectory of a payload released near Earth. Due to the nonlinear nature of gravitational acceleration, analytical solutions are often impractical for general initial conditions, necessitating the use of numerical integration techniques.

---

### 4.1 Choosing a Numerical Integration Method

The equations of motion derived earlier form a system of second-order ordinary differential equations (ODEs). To solve them numerically, it is standard practice to transform them into a system of first-order ODEs by introducing velocity components as independent variables.

Let:

$$
\vec{r} = (x, y, z), \quad \vec{v} = (\dot{x}, \dot{y}, \dot{z})
$$

Then the system becomes:

$$
\dot{\vec{r}} = \vec{v}
$$

$$
\dot{\vec{v}} = -\frac{\mu}{r^3} \vec{r}
$$

where $r = \|\vec{r}\|$.

#### Recommended Numerical Methods:

- **Euler's Method** (First-order accuracy):
  - Simple but prone to large errors over time.
  - Only suitable for very small time steps.

- **Runge-Kutta Methods**:
  - **Runge-Kutta 2nd Order (RK2)**: Moderate accuracy, relatively easy to implement.
  - **Runge-Kutta 4th Order (RK4)**: High accuracy, widely used for orbit simulations.

**Runge-Kutta 4th Order (RK4)** algorithm for advancing from $t_n$ to $t_{n+1} = t_n + \Delta t$:

$$
\begin{aligned}
k_1 &= f(t_n, y_n) \\
k_2 &= f\left(t_n + \frac{\Delta t}{2}, y_n + \frac{\Delta t}{2}k_1\right) \\
k_3 &= f\left(t_n + \frac{\Delta t}{2}, y_n + \frac{\Delta t}{2}k_2\right) \\
k_4 &= f\left(t_n + \Delta t, y_n + \Delta t \, k_3\right) \\
y_{n+1} &= y_n + \frac{\Delta t}{6} (k_1 + 2k_2 + 2k_3 + k_4)
\end{aligned}
$$

where $y$ represents the state vector containing both $\vec{r}$ and $\vec{v}$.

---

### 4.2 Time-Stepping and Tolerances for Numerical Accuracy

The **choice of time step** $\Delta t$ is crucial:
- If $\Delta t$ is too large, the simulation will suffer from significant numerical errors (e.g., energy drift).
- If $\Delta t$ is too small, the simulation will be accurate but computationally expensive.

Typical considerations:
- **Adaptive time-stepping** can be employed, adjusting $\Delta t$ based on local truncation error estimates.
- Otherwise, use a **fixed $\Delta t$** small enough to accurately resolve the motion:
  
  - Rule of thumb: $\Delta t$ should be at least $1000$ times smaller than the orbital period for stable simulations.
  
Tolerance settings (if using adaptive methods like Runge-Kutta-Fehlberg):
- **Relative Tolerance** $\sim 10^{-9}$
- **Absolute Tolerance** $\sim 10^{-12}$

Maintaining energy conservation can serve as a good diagnostic for checking numerical accuracy.

---

### 4.3 Simplifications: Accounting Only for Earth's Gravity

In this model:
- Only **central gravitational force** from Earth is considered.
- **Atmospheric drag**, **solar radiation pressure**, **third-body effects** (e.g., Moon, Sun) are **ignored** unless specified otherwise.

The governing acceleration thus remains:

$$
\vec{a} = -\frac{\mu}{r^3} \vec{r}
$$

Assumptions:
- Earth is treated as a perfect sphere.
- Earth's rotation effects (like Coriolis or centrifugal forces) are neglected unless explicitly modeled in a rotating reference frame.
- No oblateness (no $J_2$ perturbation).

This simplifies the dynamics to a classic two-body problem under Newtonian gravity.

---

### 4.4 Summary

For accurate simulation of a payload’s trajectory near Earth:
- Use **Runge-Kutta 4th order** method for numerical integration.
- Choose appropriate **time step sizes** and consider **adaptive time-stepping** for high accuracy.
- Focus solely on **Earth’s gravitational attraction** unless additional forces are explicitly required.

Proper numerical setup ensures reliable, physically consistent simulations essential for analyzing orbital dynamics.

## 5. Computational Tool and Visualization

Calculate $v_{\text{circ}}$ and $v_{\text{esc}}$ for 1000 km altitude once and print/display them:

```python
r0 = R_earth + 1_000_000  # 1000 km altitude
v_circ = np.sqrt(G*M_earth/r0)
v_esc = np.sqrt(2*G*M_earth/r0)

print(f"Circular orbital velocity at 1000 km: {v_circ/1000:.2f} km/s")
print(f"Escape velocity at 1000 km: {v_esc/1000:.2f} km/s")
```

### 5.1 Crashing or Suborbital Trajectories
```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11
M_earth = 5.972e24
R_earth = 6.371e6

# Simulation function
def simulate_orbit(v0, steps=100000, dt=1):
    r0 = R_earth + 1_000_000  # 1000 km above surface
    x, y = r0, 0
    vx, vy = 0, v0
    pos = []
    r_min, r_max = float('inf'), 0
    escaped = False

    for _ in range(steps):
        r = np.sqrt(x**2 + y**2)
        if r < R_earth:
            break
        pos.append((x, y))
        a = -G * M_earth / r**2
        ax = a * x / r
        ay = a * y / r
        vx += ax * dt
        vy += ay * dt
        x += vx * dt
        y += vy * dt
        r_min = min(r_min, r)
        r_max = max(r_max, r)
        if r > 20 * R_earth:
            escaped = True
            break

    return np.array(pos), r_min, r_max, escaped

# Part 1: Low velocities (crash back)
velocities = [4000, 5000, 6000, 7000, 8000]  # m/s

plt.figure(figsize=(8,8))
theta = np.linspace(0, 2*np.pi, 100)
# plt.fill(R_earth*np.cos(theta), R_earth*np.sin(theta), color='lightblue', label='Earth')
plt.fill(R_earth*np.cos(theta)/1000, R_earth*np.sin(theta)/1000, color='lightblue', label='Earth')
plt.plot(0, 0, 'oy', label='Center of Earth')

for v0 in velocities:
    traj, r_min, r_max, escaped = simulate_orbit(v0)
    x, y = traj[:,0], traj[:,1]
    # plt.plot(x, y, label=f'{v0/1000:.1f} km/s')
    plt.plot(x/1000, y/1000, label=f'{v0/1000:.1f} km/s')
    print(f"v0={v0/1000:.1f} km/s | Perigee: {r_min/1000:.1f} km | Apogee: {r_max/1000:.1f} km | Escaped: {escaped}")

plt.title('Low Velocities: Crashing/Short Trajectories')
plt.xlabel('x [km]')
plt.ylabel('y [km]')
plt.legend()
plt.grid()
plt.axis('equal')
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_3/5_1.png)

### 5.2 Circular and Elliptical Orbits (Bounded)
```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11
M_earth = 5.972e24
R_earth = 6.371e6

# Simulation function
def simulate_orbit(v0, steps=100000, dt=1):
    r0 = R_earth + 1_000_000  # 1000 km above surface
    x, y = r0, 0
    vx, vy = 0, v0
    pos = []
    r_min, r_max = float('inf'), 0
    escaped = False

    for _ in range(steps):
        r = np.sqrt(x**2 + y**2)
        if r < R_earth:
            break
        pos.append((x, y))
        a = -G * M_earth / r**2
        ax = a * x / r
        ay = a * y / r
        vx += ax * dt
        vy += ay * dt
        x += vx * dt
        y += vy * dt
        r_min = min(r_min, r)
        r_max = max(r_max, r)
        if r > 20 * R_earth:
            escaped = True
            break

    return np.array(pos), r_min, r_max, escaped
# Part 2: Medium velocities (orbiting)

velocities = [9000, 9100, 9200, 9300, 9400, 9500, 9600, 9700, 9800, 9900, 10000]  # m/s

plt.figure(figsize=(8,8))
theta = np.linspace(0, 2*np.pi, 100)
# plt.fill(R_earth*np.cos(theta), R_earth*np.sin(theta), color='lightblue', label='Earth')
plt.fill(R_earth*np.cos(theta)/1000, R_earth*np.sin(theta)/1000, color='lightblue', label='Earth')
plt.plot(0, 0, 'oy', label='Center of Earth')


for v0 in velocities:
    traj, r_min, r_max, escaped = simulate_orbit(v0)
    x, y = traj[:,0], traj[:,1]
    # plt.plot(x, y, label=f'{v0/1000:.1f} km/s')
    plt.plot(x/1000, y/1000, label=f'{v0/1000:.1f} km/s')
    print(f"v0={v0/1000:.1f} km/s | Perigee: {r_min/1000:.1f} km | Apogee: {r_max/1000:.1f} km | Escaped: {escaped}")

plt.title('Medium Velocities: Circular/Elliptical Orbits')
plt.xlabel('x [km]')
plt.ylabel('y [km]')
plt.legend()
plt.grid()
plt.axis('equal')
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_3/5_2.png)

### 5.3 Escape Trajectories
```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11
M_earth = 5.972e24
R_earth = 6.371e6

# Simulation function
def simulate_orbit(v0, steps=100000, dt=1):
    r0 = R_earth + 1_000_000  # 1000 km above surface
    x, y = r0, 0
    vx, vy = 0, v0
    pos = []
    r_min, r_max = float('inf'), 0
    escaped = False

    for _ in range(steps):
        r = np.sqrt(x**2 + y**2)
        if r < R_earth:
            break
        pos.append((x, y))
        a = -G * M_earth / r**2
        ax = a * x / r
        ay = a * y / r
        vx += ax * dt
        vy += ay * dt
        x += vx * dt
        y += vy * dt
        r_min = min(r_min, r)
        r_max = max(r_max, r)
        if r > 20 * R_earth:
            escaped = True
            break

    return np.array(pos), r_min, r_max, escaped
# Part 3: High velocities (escape trajectories)

velocities = [11000, 12000, 13000, 14000, 15000, 16000, 17000, 18000, 19000, 20000]  # m/s

plt.figure(figsize=(8,8))
theta = np.linspace(0, 2*np.pi, 100)
# plt.fill(R_earth*np.cos(theta), R_earth*np.sin(theta), color='lightblue', label='Earth')
plt.fill(R_earth*np.cos(theta)/1000, R_earth*np.sin(theta)/1000, color='lightblue', label='Earth')
plt.plot(0, 0, 'oy', label='Center of Earth')

for v0 in velocities:
    traj, r_min, r_max, escaped = simulate_orbit(v0)
    x, y = traj[:,0], traj[:,1]
    # plt.plot(x, y, label=f'{v0/1000:.1f} km/s')
    plt.plot(x/1000, y/1000, label=f'{v0/1000:.1f} km/s')
    print(f"v0={v0/1000:.1f} km/s | Perigee: {r_min/1000:.1f} km | Apogee: {r_max/1000:.1f} km | Escaped: {escaped}")

plt.title('High Velocities: Escape Trajectories')
plt.xlabel('x [km]')
plt.ylabel('y [km]')
plt.legend()
plt.grid()
plt.axis('equal')
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_3/5_3.png)

### 5.4 3D View
```python
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')
ax.plot(x/1000, y/1000, np.zeros_like(x), label='Payload Trajectory')
ax.scatter(0, 0, 0, color='blue', s=500, label='Earth')

ax.set_xlabel('x (km)')
ax.set_ylabel('y (km)')
ax.set_zlabel('z (km)')
ax.set_title('3D Trajectory Plot (Flat Plane)')
ax.legend()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_3/5_4.png)

### 5.5 Colab
[Souce Code](https://colab.research.google.com/drive/1uR28Taww4q6VLSa5Y8Dah7bp0z9iBUga?usp=sharing)


## 6. Discussion and Interpretation

The trajectory of a payload released near Earth is determined primarily by its initial speed relative to the local horizontal direction. Different regimes of initial speed result in fundamentally different behaviors, each with important implications for space missions and engineering.

---

### 6.1 Physical Behavior at Different Initial Speeds

#### 1. Below Orbital Speed

If the initial speed $v_0$ is **less than** the required orbital speed $v_{\text{circ}}$, the payload does not achieve a stable orbit. Instead, gravitational attraction dominates and the payload:

- Follows a **suborbital** or **ballistic** trajectory,
- Ascends to a maximum altitude and then falls back toward Earth,
- Example: **Suborbital flights** like early test rockets or ballistic missile paths.

Mathematically:

$$
v_0 < \sqrt{\frac{\mu}{r_0}}
$$

where:
- $\mu$ is the Earth's gravitational parameter,
- $r_0$ is the initial distance from Earth's center.

---

#### 2. At Orbital Speed

If $v_0$ is **equal to** the circular orbital speed:

$$
v_0 = \sqrt{\frac{\mu}{r_0}}
$$

then the payload enters a **circular orbit** around Earth, maintaining a constant altitude.

If the launch is at a different angle or slightly different magnitude, the payload can enter an **elliptical orbit** instead, characterized by varying altitude between perigee (closest approach) and apogee (farthest point).

Characteristics:
- **Circular orbit**: constant radius $r$.
- **Elliptical orbit**: varying radius, energy still negative ($\varepsilon < 0$).

---

#### 3. Above Escape Speed

If the initial speed $v_0$ **exceeds** the escape velocity $v_{\text{esc}}$, the payload overcomes Earth's gravitational binding energy.

Escape velocity:

$$
v_{\text{esc}} = \sqrt{\frac{2\mu}{r_0}}
$$

Two cases arise:
- **Exactly at escape velocity**:
  - The payload follows a **parabolic trajectory** ($\varepsilon = 0$).
  - It barely escapes, reaching infinite distance with zero residual velocity.

- **Above escape velocity**:
  - The payload follows a **hyperbolic trajectory** ($\varepsilon > 0$).
  - It escapes Earth with surplus kinetic energy and continues moving indefinitely.

---

### 6.2 Real-World Applications

Understanding the link between initial speed and trajectory is crucial in space engineering and operations:

#### 1. Satellite Deployment

- Precise insertion into orbit requires achieving the correct orbital velocity.
- Slight deviations result in elliptical or unstable orbits.
- Low Earth Orbit (LEO) satellites typically require speeds around $7.8 \, \text{km/s}$ at an altitude of about $300 \, \text{km}$.

#### 2. Spacecraft Reentry Planning

- For reentry missions (e.g., returning astronauts or probes):
  - Controlled reduction of orbital speed ensures the spacecraft descends safely.
  - Reentry corridors must be carefully calculated to avoid burning up or bouncing off the atmosphere.

#### 3. Space Escape Maneuvers

- Missions escaping Earth (e.g., missions to the Moon, Mars) must achieve escape velocity.
- Upper rocket stages are used to provide the additional speed required beyond orbital velocity.
- Example: **Apollo missions** required a **Trans-Lunar Injection (TLI)** maneuver to leave Earth's gravitational influence.

---

### 6.3 Summary

The initial velocity of a released payload dictates whether it:
- **Falls back to Earth**,
- **Enters stable orbit**,
- **Escapes Earth's gravity**.

Mastering these relationships is fundamental for designing satellite deployments, planning space missions, and ensuring the success of reentry and escape trajectories.

## 7. Conclusion

In this study, we explored the dynamics of payloads released near Earth under the influence of gravitational forces. Through theoretical analysis, numerical simulations, and visualizations, we classified possible trajectories into ballistic, orbital, and escape paths. The results underscore the critical dependence of trajectory type on initial velocity magnitude and direction. These findings have direct applications in satellite deployment, reentry planning, and interplanetary mission design, highlighting the importance of precise velocity control in space operations.

