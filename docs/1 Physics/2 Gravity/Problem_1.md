# Problem 1

## 1. Theoretical Derivation of Kepler’s Third Law

### 1.1 Newton's Law of Universal Gravitation

The gravitational force between two masses is given by Newton’s Law:

$$
F_g = G \frac{Mm}{r^2}
$$

Where:
- $F_g$ is the gravitational force,
- $G$ is the universal gravitational constant,
- $M$ is the mass of the central (larger) body (e.g., the Sun),
- $m$ is the mass of the orbiting body (e.g., a planet),
- $r$ is the orbital radius (distance between the centers of the two bodies).

### 1.2 Centripetal Force Requirement for Circular Motion

For an object in circular motion, the centripetal force required to keep it in orbit is:

$$
F_c = \frac{mv^2}{r}
$$

Where:
- $m$ is the mass of the orbiting body,
- $v$ is its orbital speed,
- $r$ is the radius of the circular orbit.

### 1.3 Equating Gravitational and Centripetal Forces

In a stable circular orbit, the gravitational force provides the necessary centripetal force:

$$
F_g = F_c
$$

Thus:

$$
G \frac{Mm}{r^2} = \frac{mv^2}{r}
$$

Cancel $m$ from both sides:

$$
G \frac{M}{r^2} = \frac{v^2}{r}
$$

Multiply both sides by $r$:

$$
G \frac{M}{r} = v^2
$$

### 1.4 Orbital Period and Velocity

The orbital period $T$ is the time taken to complete one full orbit. For a circular orbit of radius $r$, the orbital speed $v$ is:

$$
v = \frac{2\pi r}{T}
$$

Substitute this into the previous equation:

$$
G \frac{M}{r} = \left( \frac{2\pi r}{T} \right)^2
$$

Simplify the right-hand side:

$$
G \frac{M}{r} = \frac{4\pi^2 r^2}{T^2}
$$

Multiply both sides by $T^2$:

$$
G M T^2 = 4\pi^2 r^3
$$

Finally, solve for $T^2$:

$$
T^2 = \frac{4\pi^2}{G M} r^3
$$

### 1.5 Result: Kepler’s Third Law

This shows the square of the orbital period is proportional to the cube of the orbital radius:

$$
T^2 \propto r^3
$$

The constant of proportionality depends on the mass of the central object ($M$):

$$
T^2 = \left( \frac{4\pi^2}{G M} \right) r^3
$$

This is the mathematical expression of **Kepler’s Third Law** for circular orbits, derived from Newtonian mechanics.

## 2. Conceptual Discussion: Significance of Kepler's Third Law

### 2.1 Importance in Astronomy

Kepler’s Third Law:

$$
T^2 \propto r^3
$$

provides a foundational relationship between the orbital period ($T$) of a body and its average distance ($r$) from the object it orbits. When derived from Newtonian mechanics, this relationship becomes:

$$
T^2 = \left( \frac{4\pi^2}{G M} \right) r^3
$$

This is significant for several reasons:

- It connects orbital motion directly to the **gravitational force** and the **mass of the central body**.
- It allows astronomers to **infer hidden properties** of celestial systems using observable quantities like period and radius.
- It plays a key role in **planetary science**, **stellar systems**, **exoplanet detection**, and **satellite engineering**.

---

### 2.2 Determining Masses of Celestial Bodies

Rearranging the Newtonian form of Kepler’s Third Law:

$$
M = \frac{4\pi^2 r^3}{G T^2}
$$

This equation enables us to calculate the **mass ($M$)** of the central object (e.g., Earth, the Sun, or a star), provided the orbital period ($T$) and orbital radius ($r$) of a satellite or planet are known.

#### Example:

- Knowing the Moon’s orbital radius and period allows us to compute Earth’s mass.
- Observing the orbit of a moon around Jupiter allows astronomers to determine **Jupiter’s mass**.

---

### 2.3 Measuring Distances Between Planets and Stars

If the central mass $M$ is already known (e.g., solar mass), then:

$$
r^3 = \frac{G M T^2}{4\pi^2}
$$

This allows astronomers to compute **orbital radii** from observed periods.

#### Applications:

- Calculating the average distances of planets from the Sun.
- Estimating the distances of exoplanets from their host stars (based on transit and radial velocity data).

---

### 2.4 Applications to Natural and Artificial Satellites

Kepler's Third Law is universally valid for any object under gravitational orbit, whether natural or artificial.

#### Natural Satellites:
- Describes the motion of **moons** around planets.
- Crucial for studying **tidal locking**, **orbital resonances**, and **planetary system formation**.

#### Artificial Satellites:
- Essential for placing satellites in stable orbits around Earth (e.g., **geostationary orbit**).
- Used to design communication satellites, GPS constellations, and space probes.

For artificial satellites orbiting Earth:

$$
T^2 = \left( \frac{4\pi^2}{G M_E} \right) r^3
$$

where $M_E$ is Earth's mass. Engineers use this to determine the required altitude ($r$) for a given orbital period ($T$).

---

### 2.5 Summary

Kepler’s Third Law is more than a mathematical curiosity—it is a powerful tool for:

- Estimating **masses** and **distances** in the universe.
- Understanding both **natural orbital mechanics** and **human-made satellite systems**.
- Providing a bridge between **observable orbital motion** and **invisible gravitational forces**.

## 3. Real-World Applications of Kepler’s Third Law

Kepler’s Third Law, in its Newtonian form:

$$
T^2 = \left( \frac{4\pi^2}{G M} \right) r^3
$$

can be tested and verified using real astronomical and artificial satellite data. The law enables calculations of orbital parameters across a wide range of systems—from the Moon to distant planets, to GPS satellites.

---

### 3.1 The Moon Orbiting Earth

**Known values:**
- Orbital radius: $r \approx 3.84 \times 10^8 \ \text{m}$
- Orbital period: $T \approx 27.32 \ \text{days} \approx 2.36 \times 10^6 \ \text{s}$
- Mass of Earth: $M_E \approx 5.97 \times 10^{24} \ \text{kg}$

**Prediction using Newtonian Kepler’s Law:**

$$
T^2 = \frac{4\pi^2 r^3}{G M_E}
$$

Plugging in values:

$$
T^2 \approx \frac{4\pi^2 (3.84 \times 10^8)^3}{6.674 \times 10^{-11} \cdot 5.97 \times 10^{24}} \approx 5.57 \times 10^{12} \ \text{s}^2
$$

Taking square root:

$$
T \approx \sqrt{5.57 \times 10^{12}} \approx 2.36 \times 10^6 \ \text{s}
$$

✅ **Match with observed period** confirms validity.

---

### 3.2 Earth and Planets Orbiting the Sun

**Standard form using Astronomical Units (AU) and Earth years:**

If $T$ is in Earth years and $r$ in AU (Astronomical Units), then:

$$
T^2 = r^3
$$

| Planet       | Orbital Radius $r$ (AU) | Period $T$ (years) | $T^2$ | $r^3$ |
|--------------|--------------------------|---------------------|--------|--------|
| Earth        | 1.00                     | 1.00                | 1.00   | 1.00   |
| Mars         | 1.52                     | 1.88                | 3.53   | 3.51   |
| Jupiter      | 5.20                     | 11.86               | 140.7  | 140.6  |
| Saturn       | 9.58                     | 29.46               | 867.9  | 880.3  |

✅ **Close agreement** of $T^2$ and $r^3$ supports Kepler's Law.

---

### 3.3 Artificial Satellites (e.g., GPS Satellites)

**GPS satellite parameters:**
- Orbital radius: $r \approx 2.66 \times 10^7 \ \text{m}$
- Orbital period: $T \approx 12 \ \text{hours} \approx 4.32 \times 10^4 \ \text{s}$
- Mass of Earth: $M_E = 5.97 \times 10^{24} \ \text{kg}$

**Use Kepler’s Law:**

$$
T^2 = \frac{4\pi^2 r^3}{G M_E}
$$

Calculate predicted $T$:

$$
T \approx \sqrt{ \frac{4\pi^2 (2.66 \times 10^7)^3}{6.674 \times 10^{-11} \cdot 5.97 \times 10^{24}} } \approx 4.32 \times 10^4 \ \text{s}
$$

✅ Prediction matches design specification for GPS satellites.

---

### Comparison Summary

Kepler’s Third Law accurately predicts orbital behavior across:

- **Natural satellites** (e.g., Moon, planetary moons).
- **Planetary orbits** (in both AU and SI units).
- **Artificial satellites** (critical for telecommunications and navigation).

This universality confirms the **power and elegance** of Kepler’s Third Law when paired with Newton’s laws of motion and gravitation.

## 4. Visualization and Verification

### 4.1 Real Data Plot: $T^2$ vs $r^3$ for Planets

To test Kepler’s Third Law using Solar System planets, we compute $T^2$ and $r^3$ using known orbital data:

- $r$: orbital radius in AU
- $T$: orbital period in Earth years

We expect:

$$
T^2 = r^3
$$

```python
import matplotlib.pyplot as plt
import numpy as np

# Planetary data
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn']
r = np.array([0.39, 0.72, 1.00, 1.52, 5.20, 9.58])  # AU
T = np.array([0.24, 0.62, 1.00, 1.88, 11.86, 29.46])  # years

T_squared = T**2
r_cubed = r**3

plt.figure(figsize=(8, 5))
plt.scatter(r_cubed, T_squared, color='teal', s=70, edgecolor='black')

for i, planet in enumerate(planets):
    plt.annotate(planet, (r_cubed[i], T_squared[i]), textcoords="offset points", xytext=(5,5))

plt.title("$T^2$ vs $r^3$ for Planets in the Solar System", fontsize=14)
plt.xlabel("$r^3$ (AU³)")
plt.ylabel("$T^2$ (years²)")
plt.grid(True, linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_1/4_1.png)

```python
import matplotlib.pyplot as plt
import numpy as np

# Planetary data
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn']
r = np.array([0.39, 0.72, 1.00, 1.52, 5.20, 9.58])  # AU
T = np.array([0.24, 0.62, 1.00, 1.88, 11.86, 29.46])  # years

# Compute T^2 and r^3
T_squared = T**2
r_cubed = r**3

# Plot in log-log scale
plt.figure(figsize=(8, 5))
plt.loglog(r_cubed, T_squared, 'o', color='teal', markersize=8, markeredgecolor='black')

# Annotations
for i, planet in enumerate(planets):
    plt.annotate(planet, (r_cubed[i], T_squared[i]), textcoords="offset points", xytext=(6,4))

plt.title("Log-Log Plot: $T^2$ vs $r^3$ for Planets", fontsize=14)
plt.xlabel("$r^3$ (AU³)", fontsize=12)
plt.ylabel("$T^2$ (years²)", fontsize=12)
plt.grid(True, which='both', linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_1/4_1_2.png)

### 4.2 Real Data: Log-Log Plot and Slope Verification

To avoid compression near the origin and test proportionality:

- Transform both sides to logarithmic scale.
- Fit a line to the log-log data.
- Slope $\approx 1$ confirms $T^2 \propto r^3$.

```python
from scipy.stats import linregress

log_r3 = np.log10(r_cubed)
log_T2 = np.log10(T_squared)

slope, intercept, r_value, _, _ = linregress(log_r3, log_T2)

plt.figure(figsize=(8, 5))
plt.plot(log_r3, log_T2, 'o-', color='darkgreen')
plt.title("Log-Log Plot: $\\log(T^2)$ vs $\\log(r^3)$", fontsize=14)
plt.xlabel("$\\log(r^3)$")
plt.ylabel("$\\log(T^2)$")
plt.grid(True, which='both', linestyle='--', alpha=0.6)
plt.text(min(log_r3), max(log_T2)-0.2, f"Slope ≈ {slope:.3f}", color='red', fontsize=12)
plt.tight_layout()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_1/4_2.png)

### 4.3 Simulated Data: Verifying $T^2 \propto r^3$

Using Newton’s formulation:

$$
T = 2\pi \sqrt{\frac{r^3}{G M}}
$$

Simulate orbits for different radii and verify $T^2$ vs $r^3$.
```python
# Simulate a system with Sun-like central mass
G = 6.674e-11  # m^3 kg^-1 s^-2
M = 1.989e30   # kg (Sun's mass)

r_vals = np.linspace(0.5e11, 2.5e11, 6)  # meters
T_vals = 2 * np.pi * np.sqrt(r_vals**3 / (G * M))  # seconds

# Convert to AU and years
AU = 1.496e11
year = 3.154e7
r_AU = r_vals / AU
T_years = T_vals / year

plt.figure(figsize=(8, 5))
plt.plot(r_AU**3, T_years**2, 'o-', color='darkorange')
plt.title("Simulated: $T^2$ vs $r^3$", fontsize=14)
plt.xlabel("$r^3$ (AU³)")
plt.ylabel("$T^2$ (years²)")
plt.grid(True, linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_1/4_3.png)

### 4.4 Simulated Log-Log Plot and Slope Check
```python
log_r_sim = np.log10(r_AU**3)
log_T_sim = np.log10(T_years**2)

slope_sim, _, _, _, _ = linregress(log_r_sim, log_T_sim)

plt.figure(figsize=(8, 5))
plt.plot(log_r_sim, log_T_sim, 'o-', color='purple')
plt.title("Simulated: Log-Log Plot", fontsize=14)
plt.xlabel("$\\log(r^3)$")
plt.ylabel("$\\log(T^2)$")
plt.grid(True, which='both', linestyle='--', alpha=0.6)
plt.text(min(log_r_sim), max(log_T_sim)-0.2, f"Slope ≈ {slope_sim:.3f}", color='red', fontsize=12)
plt.tight_layout()
plt.show()
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_1/4_4.png)

### 4.5 Simulated Orbit Animation: Earth Orbiting the Sun
To enhance visual understanding, we simulate the circular orbit of Earth around the Sun using `matplotlib.animation`. This helps demonstrate:

- Constant radius motion in a circular orbit
- Uniform angular speed
- Central gravitational attraction (Sun remains at the focus)

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from IPython.display import HTML

# Constants
G = 6.674e-11              # Gravitational constant (m^3/kg/s^2)
M = 1.989e30               # Mass of the Sun (kg)
r = 1.5e11                 # Orbital radius (1 AU in meters)

# Generate orbital positions
theta = np.linspace(0, 2 * np.pi, 360)
x = r * np.cos(theta)
y = r * np.sin(theta)

# Set up the figure
fig, ax = plt.subplots(figsize=(6,6))
planet, = ax.plot([], [], 'bo', markersize=8)   # Earth
sun, = ax.plot(0, 0, 'yo', markersize=12)       # Sun
orbit, = ax.plot(x, y, 'k--', linewidth=0.5)    # Orbit path

ax.set_xlim(-r * 1.2, r * 1.2)
ax.set_ylim(-r * 1.2, r * 1.2)
ax.set_aspect('equal')
ax.set_title('Earth Orbiting the Sun')

# Animation update function
def update(frame):
    planet.set_data([x[frame]], [y[frame]])
    return planet,

# Create animation
ani = animation.FuncAnimation(fig, update, frames=len(theta), interval=20)

# Display animation (for Jupyter/Colab)
HTML(ani.to_jshtml())
```
![Code 1](../../_pics/Physics/2%20Gravity/Problem_1/4_5_earth_orbit.gif)

## 5. Conclusion

Kepler’s Third Law, which relates the square of the orbital period to the cube of the orbital radius ($T^2 \propto r^3$), stands as a cornerstone of classical and celestial mechanics. Through theoretical derivation from Newton’s laws, conceptual interpretation, real-world validation, and computational modeling, we have demonstrated its universality and predictive power.

- **Theoretically**, we derived the law from Newton's law of gravitation and circular motion, showing how gravitational interactions dictate orbital dynamics.
- **Conceptually**, we discussed its significance in astronomy, especially in calculating the masses of celestial bodies and determining distances in planetary systems.
- **Empirically**, we validated the law using real astronomical data from the Solar System and artificial satellites, all of which confirm the $T^2 \propto r^3$ relationship with high precision.
- **Computationally**, we simulated orbits using Newtonian mechanics and verified the proportionality through numerical data and log-log analysis.

This multifaceted approach not only reinforces the law’s correctness but also showcases its essential role in both scientific understanding and modern technological applications. Kepler’s Third Law exemplifies the profound connection between simple mathematical relationships and the grand structure of the cosmos.

