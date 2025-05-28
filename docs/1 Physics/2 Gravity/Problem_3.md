# Problem 3

# Trajectories of a Freely Released Payload Near Earth

## 1. Analysis of Possible Trajectories

*Notes*: When a payload is released from a moving rocket near Earth, its path depends on its starting position, speed, direction, and Earth’s gravity. Let’s explore the possible paths it might take.

- **Types of Trajectories**: The path of an object under gravity is a conic section, determined by its energy:


  - **Elliptical**: If the payload doesn’t have enough energy to escape Earth, it follows a closed, oval-shaped (elliptical) orbit, like a satellite circling Earth.
  - **Parabolic**: If the payload has just enough energy to escape, it follows a parabolic path, reaching infinity (far away) with no speed left.
  - **Hyperbolic**: If the payload has extra energy, it escapes Earth on a hyperbolic path, moving away forever with some speed remaining.

- **What Affects the Path**:


  - **Starting Position**: How high above Earth and how far from Earth’s center.

  - **Starting Velocity**: How fast it’s going and in what direction.


  - **Earth’s Gravity**: Pulls the payload toward the center, shaping its path.



*Notes*: To determine the trajectory, we’ll calculate the payload’s energy and compare its speed to the escape speed at its position.





## 2. Mathematical Derivation of Trajectories

*Notes*: Let’s set up the math to describe the payload’s motion using gravity and physics principles.



- **Gravity Force**: Earth pulls the payload toward its center. The force on the payload (mass $m$) at distance $r$ from Earth’s center (mass $M$) is given by Newton’s law of gravitation:


  $$F = \frac{G M m}{r^2}$$


  Here, $G$ is the gravitational constant.

- **Motion Equations**: We’ll use coordinates  

 $(x, y)$ 
 
 in a 2D plane, with Earth at $(0, 0)$. The distance 
  $r$ is:

  $$r = \sqrt{x^2 + y^2}$$


  The gravitational force causes acceleration toward the center, split into 
  
  $x$ and
   $y$ directions:


  $$a_x = -\frac{G M x}{r^3}, \quad a_y = -\frac{G M y}{r^3}$$


  This gives us equations for how $x$ and $y$ change over time:


  $$\frac{d^2 x}{dt^2} = -\frac{G M x}
  {(x^2 + y^2)^{3/2}}, \quad \frac{d^2 y}
  {dt^2} = -\frac{G M y}{(x^2 + y^2)^{3/2}}$$



- **Energy to Classify the Path**: We can determine the trajectory by calculating the specific energy 


$\epsilon$
 (energy per unit mass):
  - Speed: $v = \sqrt{v_x^2 + v_y^2}$, where $v_x$ and $v_y$ are the velocities in the $x$ and $y$ directions.



  - Kinetic energy per unit mass: $\frac{1}{2} v^2$.


  - Potential energy per unit mass: $-\frac{G M}{r}$.


  - Total specific energy:
    $$\epsilon = \frac{1}{2} v^2 - \frac{G M}{r}$$


  - Trajectory type:
    - $\epsilon < 0$: Elliptical (bound orbit).


    - $\epsilon = 0$: Parabolic (just escapes).


    - $\epsilon > 0$: Hyperbolic (escapes with extra speed).

- **Escape Velocity**: The speed needed to just escape (parabolic trajectory) at distance

 $r$ is when $\epsilon = 0$:
  $$\frac{1}{2} v_{\text{esc}}^2 - \frac{G M}{r} = 0 \implies v_{\text{esc}} = \sqrt{\frac{2 G M}{r}}$$

*Notes*: These equations are complex to solve analytically, so we’ll use numerical methods to simulate the payload’s path.

## 3. Numerical Analysis Setup

*Notes*: Let’s define the starting conditions for the payload to simulate different trajectories.

- **Starting Altitude**: The payload is released 400 km above Earth’s surface, a typical altitude for low Earth orbit (like the International Space Station).
  - Earth’s radius:
  
   $R = 6,371$ km = $6.371 \times 10^6$ m.



  - Distance from Earth’s center: $r = 6,371 + 400 = 6,771$ km = $6.771 \times 10^6$ m.


- **Starting Position**: We’ll place the payload at 

$(x, y) = (6.771 \times 10^6, 0)$ m, 




meaning it’s 6,771 km along the x-axis from Earth’s center.
- **Starting Velocity**: We’ll test three speeds to get different trajectories, all in the y-direction (tangential to Earth’s surface, like an orbit):
  - **Elliptical**: Speed equal to the circular orbit speed at this altitude.
  - **Parabolic**: Speed equal to the escape velocity.
  - **Hyperbolic**: Speed greater than the escape velocity.
- **Earth’s Data**:


  - Mass: $M = 5.972 \times 10^{24}$ kg.

  
  - Gravitational constant: $G = 6.6743 \times 10^{-11}$ m³/kg·s².

- **Local Escape Velocity** (second cosmic velocity at this altitude):
  The escape velocity at distance $r$ is:
  
  
  
  $$v_{\text{esc}} = \sqrt{\frac{2 G M}{r}}$$



  Substitute the values:


  $$v_{\text{esc}} = \sqrt{\frac{2 \times (6.6743 \times 10^{-11}) \times (5.972 \times 10^{24})}{6.771 \times 10^6}}$$


  Numerator:
  
  
  $$2 \times 6.6743 \times 10^{-11} \times 5.972 \times 10^{24} = 7.978 \times 10^{14}$$



  Fraction:


  $$\frac{7.978 \times 10^{14}}{6.771 \times 10^6} \approx 1.178 \times 10^8$$


  Square root:


  $$v_{\text{esc}} = \sqrt{1.178 \times 10^8} \approx 10,853 \, \text{m/s} = 10.85 \, \text{km/s}$$




- **Circular Orbit Velocity** (first cosmic velocity at this altitude):
  The speed for a circular orbit at distance 
  
  $r$ is:
  $$v_{\text{circ}} = \sqrt{\frac{G M}{r}}$$


  Substitute the values:



  $$v_{\text{circ}} = \sqrt{\frac{(6.6743 \times 10^{-11}) \times (5.972 \times 10^{24})}{6.771 \times 10^6}}$$



  Numerator:


  $$6.6743 \times 10^{-11} \times 5.972 \times 10^{24} = 3.989 \times 10^{14}$$



  Fraction:


  $$\frac{3.989 \times 10^{14}}{6.771 \times 10^6} \approx 5.892 \times 10^7$$



  Square root:


  $$v_{\text{circ}} = \sqrt{5.892 \times 10^7} \approx 7,676 \, \text{m/s} = 7.68 \, \text{km/s}$$

  

*Notes*: We’ll simulate three trajectories:
- Elliptical: 7.68 km/s (circular orbit speed).
- Parabolic: 10.85 km/s (escape speed).
- Hyperbolic: 12 km/s (above escape speed).

## 4. Implementation

*Notes*: We’ll use Python to numerically solve the motion equations and plot the trajectories.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Constants
G = 6.6743e-11  # m^3/kg·s^2 (gravitational constant)
M_earth = 5.972e24  # kg (Earth's mass)
R_earth = 6.371e6  # m (Earth's radius)

# Initial conditions
altitude = 400e3  # 400 km above Earth's surface
r0 = R_earth + altitude  # Distance from Earth's center
v_circ = np.sqrt(G * M_earth / r0)  # Circular orbit speed
v_esc = np.sqrt(2 * G * M_earth / r0)  # Escape velocity

# Test three velocities: elliptical, parabolic, hyperbolic
velocities = [v_circ, v_esc, 12e3]  # m/s (7.68 km/s, 10.85 km/s, 12 km/s)
labels = ['Elliptical (v = 7.68 km/s)', 'Parabolic (v = 10.85 km/s)', 'Hyperbolic (v = 12 km/s)']

# Time array (simulate for 2 hours)
t = np.linspace(0, 7200, 1000)

# Differential equations: state = [x, y, vx, vy]
def equations(state, t, G, M):
    x, y, vx, vy = state
    r = np.sqrt(x**2 + y**2)
    ax = -G * M * x / r**3
    ay = -G * M * y / r**3
    return [vx, vy, ax, ay]

# Simulate trajectories for each velocity
trajectories = []
for v in velocities:
    # Initial state: start at (r0, 0) with velocity in y-direction
    state0 = [r0, 0, 0, v]
    sol = odeint(equations, state0, t, args=(G, M_earth))
    trajectories.append(sol)

# Plotting
plt.figure(figsize=(10, 8))

# Draw Earth as a circle
theta = np.linspace(0, 2*np.pi, 100)
x_earth = R_earth * np.cos(theta)
y_earth = R_earth * np.sin(theta)
plt.plot(x_earth, y_earth, 'b-', label='Earth')

# Plot each trajectory
for i, traj in enumerate(trajectories):
    x, y = traj[:, 0], traj[:, 1]
    plt.plot(x, y, label=labels[i])

plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.title('Payload Trajectories Near Earth (Released at 400 km Altitude)')
plt.axis('equal')  # Make the plot look circular
plt.legend()
plt.grid(True)
plt.show()

# Check the specific energy to confirm trajectory types
for i, v in enumerate(velocities):
    r = r0
    epsilon = 0.5 * v**2 - G * M_earth / r
    print(f"{labels[i]}:")
    print(f"  Speed: {v/1000:.2f} km/s")
    print(f"  Specific Energy: {epsilon:.2e} J/kg")
    print(f"  Trajectory: {'Elliptical' if epsilon < 0 else 'Parabolic' if abs(epsilon) < 1e3 else 'Hyperbolic'}")
```
![alt text](image-3.png)

*Notes on Code*:
- **Setup**: Defines Earth’s properties and the payload’s starting position at 400 km altitude.
- **Velocities**: Tests three speeds: circular orbit speed (7.68 km/s), escape speed (10.85 km/s), and a higher speed (12 km/s).
- **Simulation**: Uses `odeint` to solve the motion equations numerically, tracking the payload’s position over time.
- **Plot**: Shows Earth as a blue circle and the three trajectories in different colors.
- **Energy Check**: Calculates the specific energy to confirm whether each path is elliptical, parabolic, or hyperbolic.

## 5. Relation to Space Scenarios

*Notes*: Let’s connect these trajectories to real space missions:
- **Orbital Insertion**: The elliptical trajectory (speed = 7.68 km/s) shows the payload entering a stable orbit around Earth, like a satellite being deployed. This speed matches the circular orbit speed at 400 km, so it forms a circular orbit (a special kind of ellipse).
- **Reentry**: If the speed were lower than 7.68 km/s, the payload would fall back toward Earth, possibly reentering the atmosphere (we didn’t include air resistance here, so this isn’t shown).
- **Escape**: The parabolic (10.85 km/s) and hyperbolic (12 km/s) trajectories show the payload escaping Earth’s gravity, which is what you’d want for a mission to the Moon, Mars, or beyond.

*Notes*: Understanding these paths helps space engineers plan missions, like releasing satellites into orbit or sending probes to other planets.

## Discussion on Extensions

*Notes*: Here are some ways to make this simulation more realistic:
- **Air Resistance**: If the payload gets too close to Earth, air resistance would slow it down and heat it up, affecting reentry paths.
- **Earth’s Rotation**: Earth’s spin gives the payload an extra starting speed depending on the launch location, which could change the trajectory.
- **Other Forces**: In real missions, things like the Sun’s gravity, solar radiation, or the Moon’s pull can nudge the payload off its path.

*Notes*: This simulation gives us a starting point to understand how payloads move, which is super important for planning space missions like satellite launches or trips to other planets.

---

### Rendering and Running in VS Code
- **File**: Save as `payload_trajectories.md`.
- **Rendering**: Use the "Markdown+Math" extension; preview with `Ctrl+Shift+V` to see equations like $v_{\text{esc}}$ and $$F$$.
- **Code**: Extract the Python code to `payload_trajectories.py` or use a `.ipynb` file with the "Jupyter" extension.
- **Requirements**: Install `numpy`, `matplotlib`, and `scipy` (`pip install numpy matplotlib scipy`).

### Output Notes
- **Plot**: The graph shows:
  - Earth as a blue circle.
  - Three trajectories:
    - **Elliptical**: A closed loop (a circular orbit in this case).
    - **Parabolic**: A path that curves away, just escaping.
    - **Hyperbolic**: A path that curves away more sharply, escaping with extra speed.
- **Energy Results**:
  - Elliptical: Negative energy (bound to Earth).
  - Parabolic: Energy near zero (just escapes).
  - Hyperbolic: Positive energy (escapes easily).

This solution explains the payload’s possible paths in a simple way, with clear math, a simulation, and pictures to show what happens. It’s all set for you to copy and paste! Let me know if you’d like to try different starting speeds or add more features.