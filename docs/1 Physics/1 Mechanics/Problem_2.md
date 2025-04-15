# Problem 2 

## 1. Theoretical Foundation
The forced damped pendulum is a nonlinear system governed by:
$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin\theta = A \cos(\omega t)
$$
For small angles, $\sin\theta \approx \theta$, yielding a linear equation:
$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
$$
where $\omega_0 = \sqrt{g/L}$. Solutions include transient decay and a steady-state response:
$$
\theta_p(t) = D \cos(\omega t - \phi), \quad D = \frac{A}{\sqrt{(\omega_0^2 - \omega^2)^2 + (b \omega)^2}}
$$
Resonance occurs when $\omega \approx \omega_0$, maximizing amplitude.

## 2. System Dynamics
- **Damping $(b)$**: Higher $b$ reduces oscillation amplitude and shifts resonance.
- **Driving Amplitude $(A)$**: Larger $A$ increases response, introducing nonlinear effects.
- **Driving Frequency $(\omega)$**: Controls synchronization and energy transfer.
- **Chaos**: Increasing $A$ can induce period doubling and chaotic behavior.

## 3. Applications
- **Energy Harvesting**: Piezoelectric devices optimize energy capture by tuning $\omega_0$.
- **Bridges**: Wind-induced oscillations (e.g., Tacoma Narrows) align with resonance behavior.
- **Oscillating Circuits**: Analogous to RLC circuits with $\omega_0$ and damping.

## 4. Implementation of the Forced Damped Pendulum Simulation

This section demonstrates three different pendulum scenarios:
1. Pure pendulum (no damping, no external force)
2. Damped pendulum
3. Forced pendulum without damping

### 4.1 Pure Pendulum (No Damping, No External Force)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Define the system
def pure_pendulum(state, t):
    theta, v = state
    dtheta_dt = v
    dv_dt = -np.sin(theta)  # No damping (b=0) and no external force (A=0)
    return [dtheta_dt, dv_dt]

# Parameters
t = np.linspace(0, 50, 1000)  # Time array
initial_conditions = [0.1, 0]  # [theta0, v0]

# Solve
sol = odeint(pure_pendulum, initial_conditions, t)
theta = sol[:, 0]
v = sol[:, 1]

# Create subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))

# Time series plot
ax1.plot(t, theta, 'b-', label='θ(t)')
ax1.set_xlabel('Time (s)')
ax1.set_ylabel('θ (rad)')
ax1.set_title('Pure Pendulum: θ vs Time')
ax1.grid(True)
ax1.legend()

# Phase space plot
ax2.plot(theta, v, 'r-', lw=0.5)
ax2.set_xlabel('θ (rad)')
ax2.set_ylabel('θ̇ (rad/s)')
ax2.set_title('Pure Pendulum: Phase Space')
ax2.grid(True)

plt.tight_layout()
plt.show()
```

**Output**: Two plots showing the pure pendulum motion:
1. Left: Time series of angular displacement θ(t)
2. Right: Phase space trajectory showing the conservation of energy (closed orbit)

![pure_pendulum](../../_pics/Physics/1%20Mechanics/Problem_2/pure_pendulum.png)

### 4.2 Damped Pendulum

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Define the system
def damped_pendulum(state, t, b):
    theta, v = state
    dtheta_dt = v
    dv_dt = -b * v - np.sin(theta)  # With damping (b≠0) but no external force (A=0)
    return [dtheta_dt, dv_dt]

# Parameters
t = np.linspace(0, 50, 1000)
b = 0.5  # Damping coefficient
initial_conditions = [0.1, 0]

# Solve
sol = odeint(damped_pendulum, initial_conditions, t, args=(b,))
theta = sol[:, 0]
v = sol[:, 1]

# Create subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))

# Time series plot
ax1.plot(t, theta, 'b-', label='θ(t)')
ax1.set_xlabel('Time (s)')
ax1.set_ylabel('θ (rad)')
ax1.set_title('Damped Pendulum: θ vs Time')
ax1.grid(True)
ax1.legend()

# Phase space plot
ax2.plot(theta, v, 'r-', lw=0.5)
ax2.set_xlabel('θ (rad)')
ax2.set_ylabel('θ̇ (rad/s)')
ax2.set_title('Damped Pendulum: Phase Space')
ax2.grid(True)

plt.tight_layout()
plt.show()
```

**Output**: Two plots showing the damped pendulum motion:
1. Left: Time series showing the decaying oscillations
2. Right: Phase space trajectory showing the energy dissipation (spiral trajectory)

![damped_pendulum](../../_pics/Physics/1%20Mechanics/Problem_2/damped_pendulum.png)

### 4.3 Forced Pendulum without Damping

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Define the system
def forced_pendulum(state, t, A, omega):
    theta, v = state
    dtheta_dt = v
    dv_dt = -np.sin(theta) + A * np.cos(omega * t)  # No damping (b=0) but with external force (A≠0)
    return [dtheta_dt, dv_dt]

# Parameters
t = np.linspace(0, 50, 1000)
A = 0.5  # External force amplitude
omega = 2/3  # Driving frequency
initial_conditions = [0.1, 0]

# Solve
sol = odeint(forced_pendulum, initial_conditions, t, args=(A, omega))
theta = sol[:, 0]
v = sol[:, 1]

# Create subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))

# Time series plot
ax1.plot(t, theta, 'b-', label='θ(t)')
ax1.set_xlabel('Time (s)')
ax1.set_ylabel('θ (rad)')
ax1.set_title('Forced Pendulum: θ vs Time')
ax1.grid(True)
ax1.legend()

# Phase space plot
ax2.plot(theta, v, 'r-', lw=0.5)
ax2.set_xlabel('θ (rad)')
ax2.set_ylabel('θ̇ (rad/s)')
ax2.set_title('Forced Pendulum: Phase Space')
ax2.grid(True)

plt.tight_layout()
plt.show()
```

**Output**: Two plots showing the forced pendulum motion:
1. Left: Time series showing the driven oscillations
2. Right: Phase space trajectory showing the complex dynamics due to the external force

![forced_pendulum](../../_pics/Physics/1%20Mechanics/Problem_2/forced_pendulum.png)

## 5. Colab
[Souce Code](https://colab.research.google.com/drive/14i_omnGOp-ujAiWQA9HpNzs27sd6lCpt?usp=sharing)

## 6. Forced Damped Pendulum: Chaos & Resonance

### 6.1 Chaotic Motion in the Forced Damped Pendulum
For certain values of the damping coefficient $ b $, driving amplitude $ A $, and driving frequency $ \omega $, the forced damped pendulum exhibits chaotic behavior. A common set of parameters leading to chaos is:
- $ b = 0.5 $ (moderate damping)
- $ A = 1.2 $ (strong forcing)
- $ \omega = \frac{2}{3} $ (driving frequency)

Let's simulate the chaotic motion:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Define the system
def chaotic_pendulum(state, t, b, A, omega):
    theta, v = state
    dtheta_dt = v
    dv_dt = -b * v - np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, dv_dt]

# Parameters
t = np.linspace(0, 100, 5000)  # Extended time for chaotic behavior
b = 0.5
A = 1.2
omega = 2/3
initial_conditions = [0.1, 0]

# Solve
sol = odeint(chaotic_pendulum, initial_conditions, t, args=(b, A, omega))
theta = sol[:, 0]
v = sol[:, 1]

# Create subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))

# Time series plot
ax1.plot(t, theta, 'b-', label='θ(t)')
ax1.set_xlabel('Time (s)')
ax1.set_ylabel('θ (rad)')
ax1.set_title('Chaotic Pendulum: θ vs Time')
ax1.grid(True)
ax1.legend()

# Phase space plot
ax2.plot(theta, v, 'r-', lw=0.5)
ax2.set_xlabel('θ (rad)')
ax2.set_ylabel('θ̇ (rad/s)')
ax2.set_title('Chaotic Pendulum: Phase Space')
ax2.grid(True)

plt.tight_layout()
plt.show()
```

![6_1](../../_pics/Physics/1%20Mechanics/Problem_2/6_1.png)

#### Expected Output:
1. **Time Series Plot**: Irregular oscillations with no periodic pattern.
2. **Phase Space Plot**: A strange attractor instead of a closed orbit, characteristic of chaotic dynamics.

---

### 6.2 Resonance in the Forced Damped Pendulum
Resonance occurs when the driving frequency $ \omega $ is close to the system’s natural frequency $ \omega_0 = \sqrt{g/L} $. This results in large oscillations.

Let’s simulate resonance by setting:
- $ b = 0.1 $ (low damping)
- $ A = 0.5 $ (moderate forcing)
- $ \omega = \omega_0 \approx 1 $ (resonance condition)

```python
# Define the system
def resonance_pendulum(state, t, b, A, omega):
    theta, v = state
    dtheta_dt = v
    dv_dt = -b * v - np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, dv_dt]

# Parameters
t = np.linspace(0, 100, 5000)  # Long simulation to see resonance effects
b = 0.1
A = 0.5
omega = 1  # Resonance condition
initial_conditions = [0.1, 0]

# Solve
sol = odeint(resonance_pendulum, initial_conditions, t, args=(b, A, omega))
theta = sol[:, 0]
v = sol[:, 1]

# Create subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))

# Time series plot
ax1.plot(t, theta, 'b-', label='θ(t)')
ax1.set_xlabel('Time (s)')
ax1.set_ylabel('θ (rad)')
ax1.set_title('Resonance: θ vs Time')
ax1.grid(True)
ax1.legend()

# Phase space plot
ax2.plot(theta, v, 'r-', lw=0.5)
ax2.set_xlabel('θ (rad)')
ax2.set_ylabel('θ̇ (rad/s)')
ax2.set_title('Resonance: Phase Space')
ax2.grid(True)

plt.tight_layout()
plt.show()
```

![6_2](../../_pics/Physics/1%20Mechanics/Problem_2/6_2.png)

#### Expected Output:
1. **Time Series Plot**: Oscillations with increasing amplitude over time.
2. **Phase Space Plot**: Large periodic orbits, showing energy accumulation due to resonance.

