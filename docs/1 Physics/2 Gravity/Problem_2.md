# Problem 2

## Definitions & Concepts

### 1.1 Escape Velocity

Escape velocity is the minimum speed an object must reach to break free from the gravitational pull of a celestial body, without any further propulsion.

The general formula for escape velocity is derived from the conservation of energy:

$$
\frac{1}{2}mv^2 = \frac{GMm}{r}
$$

Solving for velocity:

$$
v_{esc} = \sqrt{\frac{2GM}{r}}
$$

Where:
- $v_{esc}$ is the escape velocity,
- $G$ is the gravitational constant $(6.674 \times 10^{-11}\,\text{m}^3\,\text{kg}^{-1}\,\text{s}^{-2})$,
- $M$ is the mass of the celestial body,
- $r$ is the distance from the center of the body to the point of escape (typically the planet’s radius).

### 1.2 First Cosmic Velocity (Orbital Velocity)

The first cosmic velocity refers to the minimum horizontal speed an object must have to remain in a stable, circular orbit just above the surface of a celestial body, without falling back to the surface.

It is derived by equating gravitational force to centripetal force:

$$
\frac{GMm}{r^2} = \frac{mv^2}{r}
$$

Solving for $v$:

$$
v_{orb} = \sqrt{\frac{GM}{r}}
$$

This is also called the **orbital velocity**, and it is lower than escape velocity:

$$
v_{orb} = \frac{v_{esc}}{\sqrt{2}}
$$

### 1.3 Second Cosmic Velocity

The second cosmic velocity is simply another term for **escape velocity** from a planetary body. It is the minimum speed required to completely escape the gravitational influence of the planet and enter into space, assuming no further propulsion.

Thus:

$$
v_{2nd} = v_{esc} = \sqrt{\frac{2GM}{r}}
$$

### 1.4 Third Cosmic Velocity

The third cosmic velocity is the speed required for a spacecraft to escape not only Earth’s gravity, but also the Sun’s gravity, starting from Earth’s orbit. This is relevant for interstellar missions.

This involves both Earth’s orbital velocity around the Sun and the Sun’s gravitational influence. It can be approximated by:

$$
v_{3rd} = \sqrt{v_{esc,\odot}^2 + v_{orb,\oplus}^2}
$$

Where:
- $v_{esc,\odot}$ is the escape velocity from the Sun at Earth’s distance,
- $v_{orb,\oplus}$ is Earth’s orbital speed around the Sun ($\approx 29.78\,\text{km/s}$).

A simplified expression (ignoring Earth's gravity) for escaping the Solar System from Earth’s orbit:

$$
v_{3rd} \approx \sqrt{\frac{2GM_{\odot}}{r_{\oplus}}}
$$

Where:
- $M_{\odot}$ is the mass of the Sun,
- $r_{\oplus}$ is the average distance from Earth to the Sun ($\approx 1.496 \times 10^{11}\,\text{m}$).

### 1.5 Physical Meaning in Space Exploration

- **First Cosmic Velocity** is the target speed for launching satellites into low Earth orbit. It represents the threshold for achieving continuous free-fall around Earth.

- **Second Cosmic Velocity** is critical for missions intending to leave Earth's orbit — such as lunar missions or probes bound for other planets.

- **Third Cosmic Velocity** pertains to missions aiming to exit the Solar System, such as the **Voyager** and **Pioneer** spacecraft. Achieving this velocity allows an object to overcome the Sun’s gravitational hold.

Understanding these velocities is fundamental for determining fuel requirements, launch windows, and mission design in **astrodynamics** and **interplanetary navigation**.

## Mathematical Derivations

### 2.1 Escape Velocity

To derive the escape velocity, we equate the kinetic energy of an object to the gravitational potential energy required to escape the gravitational field of a body.

- Kinetic energy of the object:
  $$
  KE = \frac{1}{2}mv^2
  $$

- Gravitational potential energy of the object (at distance $r$ from the center of mass $M$):
  $$
  U = -\frac{GMm}{r}
  $$

For escape, the total mechanical energy must be zero:

$$
\frac{1}{2}mv^2 - \frac{GMm}{r} = 0
$$

Solving for $v$:

$$
v_{esc} = \sqrt{\frac{2GM}{r}}
$$

This velocity is independent of the mass of the escaping object and depends only on the mass and radius of the celestial body.

---

### 2.2 First Cosmic Velocity (Orbital Velocity)

This is the velocity required to keep an object in circular orbit just above the surface of a planet. It is derived by balancing the gravitational force and the required centripetal force:

- Gravitational force:
  $$
  F_g = \frac{GMm}{r^2}
  $$

- Centripetal force:
  $$
  F_c = \frac{mv^2}{r}
  $$

Setting $F_g = F_c$:

$$
\frac{GMm}{r^2} = \frac{mv^2}{r}
$$

Cancelling $m$ and solving for $v$:

$$
v_{orb} = \sqrt{\frac{GM}{r}}
$$

This is the **first cosmic velocity** and is precisely the speed needed for stable circular orbit at altitude zero (neglecting atmosphere).

---

### 2.3 Third Cosmic Velocity

The third cosmic velocity is the speed required to escape the Sun’s gravitational field from Earth’s orbit.

The Sun’s gravitational potential energy at Earth’s orbital distance:

$$
U = -\frac{GM_{\odot}m}{r_{\oplus}}
$$

Kinetic energy needed to escape from the Sun’s gravity:

$$
\frac{1}{2}mv^2 = \frac{GM_{\odot}m}{r_{\oplus}}
$$

Solving for $v$:

$$
v_{3rd} = \sqrt{\frac{2GM_{\odot}}{r_{\oplus}}}
$$

However, since Earth is already moving at orbital velocity $v_{\oplus} \approx 29.78$ km/s, the spacecraft only needs additional velocity beyond this:

$$
v_{3rd,\,launch} = \sqrt{v_{esc,\odot}^2 + v_{\oplus}^2}
$$

In practice, this value is adjusted depending on the spacecraft's launch trajectory and timing (e.g., gravity assists).

---

### 2.4 Influence of Mass and Radius

From the escape velocity formula:

$$
v_{esc} = \sqrt{\frac{2GM}{r}}, \quad v_{orb} = \sqrt{\frac{GM}{r}}
$$

We can draw the following conclusions:

- **Mass ($M$)**: As the mass of the celestial body increases, both escape and orbital velocities increase.
- **Radius ($r$)**: As the radius increases, the velocities decrease. This is because the gravitational potential becomes weaker farther from the center of mass.

Thus, denser and more massive planets like **Jupiter** have significantly higher escape velocities than **Mars**.

---

### 2.5 Assumptions in Derivations

These derivations rely on several simplifying assumptions:

- The celestial body is a **perfect sphere** with mass concentrated at the center (i.e., it behaves as a point mass).
- No atmospheric **drag** or **air resistance** is considered (ideal vacuum conditions).
- No **rotational effects** (e.g., Coriolis force or frame-dragging from planet spin).
- The motion is assumed to be **purely radial** (for escape) or **circular** (for orbit).
- The object has no propulsion after initial velocity is imparted (i.e., ballistic motion).

These assumptions allow for clean analytical expressions but differ from real-world engineering, where rocket burns, drag, and non-uniform mass distributions are considered.

## Calculations

### 3.1 Constants and Celestial Parameters

We begin by defining the necessary physical constants and planetary data:

#### Universal Constants

- Gravitational constant:
  $$
  G = 6.674 \times 10^{-11}\,\text{m}^3\,\text{kg}^{-1}\,\text{s}^{-2}
  $$

#### Planetary Data

| Planet  | Mass $(M)$ [kg]           | Radius $(r)$ [m]         | Distance from Sun $(r_{\odot})$ [m] |
|---------|----------------------------|---------------------------|--------------------------------------|
| Earth   | $5.972 \times 10^{24}$     | $6.371 \times 10^6$       | $1.496 \times 10^{11}$               |
| Mars    | $6.417 \times 10^{23}$     | $3.390 \times 10^6$       | $2.279 \times 10^{11}$               |
| Jupiter | $1.898 \times 10^{27}$     | $6.9911 \times 10^7$      | $7.785 \times 10^{11}$               |

#### Solar Mass

- Mass of the Sun:
  $$
  M_{\odot} = 1.989 \times 10^{30}\,\text{kg}
  $$

---

### 3.2 Formulas

- **First Cosmic Velocity** (Orbital):
  $$
  v_{orb} = \sqrt{\frac{GM}{r}}
  $$

- **Second Cosmic Velocity** (Escape):
  $$
  v_{esc} = \sqrt{\frac{2GM}{r}}
  $$

- **Third Cosmic Velocity** (Escape from the Sun at planetary orbit):
  $$
  v_{3rd} = \sqrt{\frac{2GM_{\odot}}{r_{\odot}}}
  $$

Note: We assume these are launched directly from the surface or orbital path with negligible atmospheric drag and no propulsion.

---

### 3.3 Numerical Calculations

#### Earth

- $v_{orb,\oplus} = \sqrt{\frac{6.674 \times 10^{-11} \cdot 5.972 \times 10^{24}}{6.371 \times 10^6}} \approx 7.91\,\text{km/s}$
- $v_{esc,\oplus} = \sqrt{2} \cdot v_{orb,\oplus} \approx 11.19\,\text{km/s}$
- $v_{3rd,\oplus} = \sqrt{\frac{2 \cdot 6.674 \times 10^{-11} \cdot 1.989 \times 10^{30}}{1.496 \times 10^{11}}} \approx 42.1\,\text{km/s}$

#### Mars

- $v_{orb,\text{Mars}} \approx \sqrt{\frac{6.674 \times 10^{-11} \cdot 6.417 \times 10^{23}}{3.390 \times 10^6}} \approx 3.56\,\text{km/s}$
- $v_{esc,\text{Mars}} \approx \sqrt{2} \cdot v_{orb,\text{Mars}} \approx 5.03\,\text{km/s}$
- $v_{3rd,\text{Mars}} \approx \sqrt{\frac{2 \cdot 6.674 \times 10^{-11} \cdot 1.989 \times 10^{30}}{2.279 \times 10^{11}}} \approx 38.5\,\text{km/s}$

#### Jupiter

- $v_{orb,\text{Jup}} \approx \sqrt{\frac{6.674 \times 10^{-11} \cdot 1.898 \times 10^{27}}{6.9911 \times 10^7}} \approx 42.1\,\text{km/s}$
- $v_{esc,\text{Jup}} \approx \sqrt{2} \cdot v_{orb,\text{Jup}} \approx 59.5\,\text{km/s}$
- $v_{3rd,\text{Jup}} \approx \sqrt{\frac{2 \cdot 6.674 \times 10^{-11} \cdot 1.989 \times 10^{30}}{7.785 \times 10^{11}}} \approx 18.5\,\text{km/s}$

---

### 3.4 Summary Table

| Planet  | $v_{orb}$ [km/s] | $v_{esc}$ [km/s] | $v_{3rd}$ [km/s] |
|---------|------------------|------------------|------------------|
| Earth   | 7.91             | 11.19            | 42.1             |
| Mars    | 3.56             | 5.03             | 38.5             |
| Jupiter | 42.1             | 59.5             | 18.5             |

---

### Remarks

- **Earth** has a balanced gravity well and a moderately high third cosmic velocity.
- **Mars**, due to its smaller mass and radius, has the lowest escape velocities — making it a practical target for missions.
- **Jupiter** has extreme gravitational requirements for launching from the surface, but its position farther from the Sun reduces the third cosmic velocity needed for solar escape.

These values are foundational for mission planning and propulsion calculations in aerospace engineering.

## Visualization and Verification

### 4.1 Kepler's Third Law Verification: $T^2 \propto r^3$

```python
import numpy as np
import matplotlib.pyplot as plt

# Semi-major axes in AU and periods in years (data from real planets)
r = np.array([0.39, 0.72, 1.00, 1.52, 5.20, 9.58])  # Mercury to Saturn
T = np.array([0.24, 0.62, 1.00, 1.88, 11.86, 29.46])

plt.figure()
plt.plot(r**3, T**2, 'o-', label="$T^2$ vs $r^3$")
plt.xlabel("$r^3$ (AU$^3$)")
plt.ylabel("$T^2$ (years$^2$)")
plt.title("Verification of Kepler's Third Law")
plt.grid(True)
plt.legend()
plt.annotate("Linear relationship confirms $T^2 \\propto r^3$",
             xy=(1,1), xytext=(5, 500),
             arrowprops=dict(arrowstyle="->"))
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_2/4_1.png)

### 4.2 Log-Log Plot to Check the Slope (Expected ≈ 1)

```python
plt.figure()
plt.loglog(r, T, 'o-', label="Log-Log Plot")
plt.xlabel("log($r$) [AU]")
plt.ylabel("log($T$) [years]")
plt.title("Log-Log Plot of Kepler's Third Law")
plt.grid(True, which='both')

# Fit and show slope
slope, intercept = np.polyfit(np.log10(r), np.log10(T), 1)
plt.text(0.1, 0.3, f"Slope ≈ {slope:.2f}", transform=plt.gca().transAxes)
plt.legend()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_2/4_2.png)

### 4.3 Comparison of Cosmic Velocities Across Planets

```python
import matplotlib.pyplot as plt

planets = ['Earth', 'Mars', 'Jupiter']
v_orb = [7.91, 3.56, 42.1]
v_esc = [11.19, 5.03, 59.5]
v_3rd = [42.1, 38.5, 18.5]

x = np.arange(len(planets))
width = 0.25

plt.figure()
plt.bar(x - width, v_orb, width, label='1st Cosmic (Orbital)')
plt.bar(x, v_esc, width, label='2nd Cosmic (Escape)')
plt.bar(x + width, v_3rd, width, label='3rd Cosmic (Solar Escape)')

plt.xticks(x, planets)
plt.ylabel('Velocity (km/s)')
plt.title('Cosmic Velocities for Earth, Mars, and Jupiter')
plt.legend()
plt.grid(axis='y')
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_2/4_3.png)

### 4.4 Mass/Radius vs Escape Velocity Relationship

```python
mass = np.array([5.972e24, 6.417e23, 1.898e27])  # kg
radius = np.array([6.371e6, 3.390e6, 6.9911e7])  # m
labels = ['Earth', 'Mars', 'Jupiter']
G = 6.674e-11

v_esc = np.sqrt(2 * G * mass / radius) / 1000  # km/s

plt.figure()
plt.scatter(mass/radius, v_esc)
for i, label in enumerate(labels):
    plt.annotate(label, (mass[i]/radius[i], v_esc[i]))

plt.xlabel('Mass/Radius (kg/m)')
plt.ylabel('Escape Velocity (km/s)')
plt.title('Escape Velocity vs Mass/Radius')
plt.grid(True)
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_2/4_4.png)

### 4.5 Simulated Escape Trajectory (Ballistic Approx.) (Optional)

```python
from scipy.integrate import solve_ivp

G = 6.674e-11
M_earth = 5.972e24
R_earth = 6.371e6

def trajectory(t, y):
    r, v = y
    a = -G * M_earth / r**2
    return [v, a]

# Initial condition: just above Earth's surface with v_esc
v0 = np.sqrt(2 * G * M_earth / R_earth)
sol = solve_ivp(trajectory, [0, 10000], [R_earth, v0], t_eval=np.linspace(0, 10000, 1000))

plt.figure()
plt.plot(sol.t, (sol.y[0] - R_earth)/1000)
plt.xlabel("Time (s)")
plt.ylabel("Altitude above surface (km)")
plt.title("Escape Trajectory from Earth")
plt.grid(True)
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_2/4_5.png)

## Applications & Discussion

### 5.1 Relevance of Cosmic Velocities in Space Missions

#### a. Satellite Launches

For a satellite to maintain a stable **low Earth orbit (LEO)**, it must achieve the **first cosmic velocity**, i.e., the orbital velocity:

$$
v_{orb} = \sqrt{\frac{GM}{r}}
$$

For Earth, this corresponds to approximately $7.91\,\text{km/s}$ just above the surface. Rockets are designed to deliver payloads into this velocity band with high precision. Failing to reach this speed causes the satellite to re-enter the atmosphere; exceeding it without further control may lead to escape trajectories.

Launch profiles often include a **vertical ascent phase** (to clear the atmosphere), followed by a **gravity turn** to achieve horizontal velocity for orbit.

---

#### b. Planetary Missions

To send a spacecraft to **Mars**, **Jupiter**, or any other planet, it must at minimum achieve the **second cosmic velocity**:

$$
v_{esc} = \sqrt{\frac{2GM}{r}} \approx 11.19\,\text{km/s} \quad \text{(for Earth)}
$$

However, this speed only places the spacecraft on a **heliocentric (Sun-centered)** trajectory. To intercept another planet, precise **Hohmann transfer orbits** are computed, often using gravitational slingshots for energy efficiency.

The **launch window** is crucial, since planets move in elliptical orbits. Delta-v budgets are carefully calculated to ensure the spacecraft escapes Earth's gravity and enters the correct interplanetary trajectory.

---

#### c. Interstellar Travel

To escape the **Solar System**, a spacecraft must reach or exceed the **third cosmic velocity**:

$$
v_{3rd} = \sqrt{\frac{2GM_{\odot}}{r_{\oplus}}} \approx 42.1\,\text{km/s}
$$

This is far beyond the capacity of conventional chemical rockets for direct launch. Missions such as **Voyager 1** achieved this by combining multiple **gravity assists** (Jupiter, Saturn) to boost their velocity incrementally.

Interstellar travel requires either:
- High-efficiency propulsion (e.g., ion drives, solar sails),
- Long mission durations (decades or centuries),
- Or breakthrough physics (e.g., nuclear or fusion propulsion).

---

### 5.2 Engineering and Fuel Implications

Achieving each velocity level involves **substantial energy expenditure**, and the relationship is non-linear due to the **rocket equation**:

$$
\Delta v = v_e \ln\left( \frac{m_0}{m_f} \right)
$$

Where:
- $\Delta v$ is the required change in velocity,
- $v_e$ is the effective exhaust velocity of the propulsion system,
- $m_0$ and $m_f$ are the initial and final mass of the rocket.

#### Implications:

- Achieving higher $\Delta v$ requires either:
  - Extremely efficient engines (high $v_e$),
  - Large fuel-to-payload ratios (increasing $m_0/m_f$),
  - Or **staging**: discarding parts of the rocket after burnout.

- For **LEO satellites**, small rockets or reusable launchers suffice.
- For **planetary missions**, **multi-stage rockets** like the Saturn V or SLS are necessary.
- For **interstellar probes**, current propulsion is inadequate without significant advances in fuel efficiency or entirely new energy sources.

---

### Summary

Understanding and overcoming the thresholds set by the **first, second, and third cosmic velocities** is at the core of mission planning in astrodynamics. Each level defines a new frontier:

- $v_{orb}$ enables **orbiting**,
- $v_{esc}$ enables **exploration**,
- $v_{3rd}$ hints at the **possibility of escape** from our solar neighborhood.

Each requires innovation in both physics and engineering — combining mathematical precision, materials science, and propulsion technologies to make the cosmos accessible.
