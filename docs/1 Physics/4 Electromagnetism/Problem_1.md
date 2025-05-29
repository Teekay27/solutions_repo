# Problem 1

# Trajectories of a Freely Released Payload Near Earth

## 1. Analysis of Possible Trajectories

*Notes*: When a payload is released from a moving rocket near Earth, its path depends on its initial position, velocity, and Earth’s gravitational pull. Let’s explore the possible trajectories it might follow.



- **Types of Trajectories**: The path of an object under gravity is a conic section, determined by its specific energy:


  - **Elliptical**: If the payload’s energy is negative, it’s bound to Earth and follows a closed, elliptical orbit (like a satellite). This happens if the speed is less than the escape velocity but enough to orbit.

  - **Parabolic**: If the energy is exactly zero, the payload just escapes Earth’s gravity, following a parabolic path. This occurs at the escape velocity.


  - **Hyperbolic**: If the energy is positive, the payload has excess speed and escapes Earth on a hyperbolic path, never returning. This happens if the speed exceeds the escape velocity.
  

- **Key Factors**:
  - **Initial Position**: The altitude and distance from Earth’s center affect the gravitational force.


  - **Initial Velocity**: The speed and direction determine the trajectory type.


  - **Earth’s Gravity**: Acts as the central force, following Newton’s law of gravitation.



*Notes*: To classify the trajectory, we need to compute the specific energy and compare the payload’s speed to the local escape velocity.

## 2. Mathematical Derivation of Trajectories

*Notes*: Let’s set up the equations to determine the payload’s path using gravitational principles.



- **Newton’s Law of Gravitation**: The force on the payload (mass $m$) at distance $r$ from Earth’s center (mass $M$) is:

  $F = \frac{G M m}{r^2}$
  
  where $G$ is the gravitational constant.


- **Equations of Motion**: In a 2D plane (for simplicity), use Cartesian coordinates $(x, y)$ with Earth at the origin. The acceleration due to gravity is:

  $a_x = -\frac{G M x}{r^3}, \quad a_y = -\frac{G M y}{r^3}, \quad r = \sqrt{x^2 + y^2}$

  This gives the second-order differential equations:
  $\frac{d^2 x}{dt^2} = -\frac{G M x}{(x^2 + y^2)^{3/2}}, \quad \frac{d^2 y}{dt^2} = -\frac{G M y}{(x^2 + y^2)^{3/2}}$
  

- **Specific Energy**: To classify the trajectory, compute the specific energy $\epsilon$ (energy per unit mass):

  - Kinetic energy per unit mass: $\frac{1}{2} v^2$, where $v = \sqrt{v_x^2 + v_y^2}$.

  - Potential energy per unit mass: $-\frac{G M}{r}$.

  - Total specific energy:
    $\epsilon = \frac{1}{2} v^2 - \frac{G M}{r}$


  - Trajectory type:
    - $\epsilon < 0$: Elliptical (bound orbit).
    - $\epsilon = 0$: Parabolic (just escapes).
    - $\epsilon > 0$: Hyperbolic (escapes).

- **Escape Velocity**: At distance $r$, the escape velocity is the speed where $\epsilon = 0$:
  $\frac{1}{2} v_{\text{esc}}^2 - \frac{G M}{r} = 0 \implies v_{\text{esc}} = \sqrt{\frac{2 G M}{r}}$



*Notes*: We’ll use these equations to simulate the payload’s path numerically, since analytical solutions are complex for most initial conditions.

## 3. Numerical Analysis Setup

*Notes*: Let’s define the initial conditions for the payload:



- **Altitude**: Released at 400 km above Earth’s surface (typical for low Earth orbit, like the ISS).


  - Earth’s radius: $R = 6,371$ km.
  - Distance from Earth’s center: $r = 6,371 + 400 = 6,771$ km = $6.771 \times 10^6$ m.
- **Position**: Start at $(x, y) = (6.771 \times 10^6, 0)$ m (along the x-axis).


- **Velocity**: Test three cases to get different trajectories:


  - **Elliptical**: Speed less than escape velocity, tangential (circular orbit speed).


  - **Parabolic**: Speed equal to escape velocity, tangential.

  - **Hyperbolic**: Speed greater than escape velocity, tangential.
  
- **Earth’s Data**:
  - Mass: $M = 5.972 \times 10^{24}$ kg.
  - $G = 6.6743 \times 10^{-11}$ m³/kg·s².

- **Local Escape Velocity**:
  $v_{\text{esc}} = \sqrt{\frac{2 \times 6.6743 \times 10^{-11} \times 5.972 \times 10^{24}}{6.771 \times 10^6}}$


  Numerator: $2 \times 6.6743 \times 10^{-11} \times 5.972 \times 10^{24} = 7.978 \times 10^{14}$
  Fraction: $\frac{7.978 \times 10^{14}}{6.771 \times 10^6} \approx 1.178 \times 10^8$

  Square root: $v_{\text{esc}} = \sqrt{1.178 \times 10^8} \approx 10,853$ m/s = 10.85 km/s.

- **Circular Orbit Velocity** (first cosmic velocity at this altitude):
  $v_{\text{circ}} = \sqrt{\frac{6.6743 \times 10^{-11} \times 5.972 \times 10^{24}}{6.771 \times 10^6}}$


  Numerator: $6.6743 \times 10^{-11} \times 5.972 \times 10^{24} = 3.989 \times 10^{14}$


  Fraction: $\frac{3.989 \times 10^{14}}{6.771 \times 10^6} \approx 5.892 \times 10^7$


  Square root: $v_{\text{circ}} = \sqrt{5.892 \times 10^7} \approx 7,676$ m/s = 7.68 km/s.

*Notes*: We’ll simulate with speeds of 7.68 km/s (elliptical), 10.85 km/s (parabolic), and 12 km/s (hyperbolic), all in the y-direction (tangential).

## 4. Implementation

*Notes*: We’ll use Python to numerically solve the equations of motion and plot the trajectories.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Constants
G = 6.6743e-11  # m^3/kg·s^2
M_earth = 5.972e24  # kg
R_earth = 6.371e6  # m (Earth's radius)

# Initial conditions
altitude = 400e3  # 400 km
r0 = R_earth + altitude  # Distance from Earth's center
v_circ = np.sqrt(G * M_earth / r0)  # Circular orbit speed
v_esc = np.sqrt(2 * G * M_earth / r0)  # Escape velocity

# Test three velocities: elliptical, parabolic, hyperbolic
velocities = [v_circ, v_esc, 12e3]  # m/s
labels = ['Elliptical (v = 7.68 km/s)', 'Parabolic (v = 10.85 km/s)', 'Hyperbolic (v = 12 km/s)']

# Time array
t = np.linspace(0, 7200, 1000)  # 2 hours

# Differential equations: state = [x, y, vx, vy]
def equations(state, t, G, M):
    x, y, vx, vy = state
    r = np.sqrt(x**2 + y**2)
    ax = -G * M * x / r**3
    ay = -G * M * y / r**3
    return [vx, vy, ax, ay]

# Simulate trajectories
trajectories = []
for v in velocities:
    # Initial state: start at (r0, 0) with velocity in y-direction
    state0 = [r0, 0, 0, v]
    sol = odeint(equations, state0, t, args=(G, M_earth))
    trajectories.append(sol)

# Plotting
plt.figure(figsize=(10, 8))

# Plot Earth as a circle
theta = np.linspace(0, 2*np.pi, 100)
x_earth = R_earth * np.cos(theta)
y_earth = R_earth * np.sin(theta)
plt.plot(x_earth, y_earth, 'b-', label='Earth')

# Plot trajectories
for i, traj in enumerate(trajectories):
    x, y = traj[:, 0], traj[:, 1]
    plt.plot(x, y, label=labels[i])

plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.title('Payload Trajectories Near Earth (Released at 400 km Altitude)')
plt.axis('equal')
plt.legend()
plt.grid(True)
plt.show()

# Classify trajectories by specific energy
for i, v in enumerate(velocities):
    r = r0
    epsilon = 0.5 * v**2 - G * M_earth / r
    print(f"{labels[i]}:")
    print(f"  Speed: {v/1000:.2f} km/s")
    print(f"  Specific Energy: {epsilon:.2e} J/kg")
    print(f"  Trajectory: {'Elliptical' if epsilon < 0 else 'Parabolic' if abs(epsilon) < 1e3 else 'Hyperbolic'}")
```
![alt text](image-1.png)
*Notes on Code*:


- **Setup**: Defines Earth’s properties and initial conditions at 400 km altitude.

- **Velocities**: Tests three speeds: circular (elliptical), escape (parabolic), and above escape (hyperbolic).


- **Simulation**: Uses `odeint` to solve the differential equations numerically.

- **Plot**: Shows Earth as a circle and the payload’s path for each case.

- **Energy Check**: Computes specific energy to confirm trajectory types.

## 5. Relation to Space Scenarios

*Notes*:
- **Orbital Insertion**: The elliptical trajectory (v = 7.68 km/s) represents a payload entering a stable orbit, like deploying a satellite. This speed matches the first cosmic velocity at that altitude.


- **Reentry**: If the speed is too low (below circular velocity), the trajectory would dip into the atmosphere, leading to reentry (not simulated here due to no air resistance).


- **Escape**: The parabolic (v = 10.85 km/s) and hyperbolic (v = 12 km/s) trajectories show the payload escaping Earth, relevant for missions to the Moon or beyond.

*Notes*: These trajectories are key for planning space missions, ensuring payloads reach their intended orbits or destinations.

## Discussion on Extensions

*Notes*:
- **Air Resistance**: Including drag would affect reentry trajectories, slowing the payload and heating it up.

- **Earth’s Rotation**: The planet’s spin adds an initial velocity, slightly altering the required speeds.

- **Other Forces**: Solar radiation or other planets’ gravity could perturb the path in real missions.

*Notes*: This simulation provides a foundation for understanding payload motion, critical for satellite deployment and interplanetary travel.

---



### Rendering and Running in VS Code
- **File**: Save as `payload_trajectories.md`.
- **Rendering**: Use the "Markdown+Math" extension; preview with `Ctrl+Shift+V` to see equations like $v_{\text{esc}}$ and $$F$$.
- **Code**: Extract to `payload_trajectories.py` or use a `.ipynb` with the "Jupyter" extension.
- **Requirements**: Install `numpy`, `matplotlib`, `scipy` (`pip install numpy matplotlib scipy`).

### Output Notes
- **Plot**: Shows Earth and three trajectories:
  - Elliptical: A closed loop (orbit).
  - Parabolic: A path that just escapes.
  - Hyperbolic: A path that curves away sharply.
- **Energy**:
  - Elliptical: Negative energy (bound).
  - Parabolic: Near-zero energy (just escapes).
  - Hyperbolic: Positive energy (escapes easily).

This solution explains payload trajectories clearly, with theory, simulation, and visuals, making it easy to understand their role in space missions. Let me know if you’d like to adjust initial conditions or add more features!
