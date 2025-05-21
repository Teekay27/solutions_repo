# Problem 1


# Orbital Period and Orbital Radius

## 1. Theoretical Foundation

Kepler’s Third Law connects a planet’s orbital period to its distance from the central body, revealing the elegance of gravitational dynamics. Let’s derive it for circular orbits.

### Derivation of Kepler’s Third Law
*Notes*: Consider a body of mass $m$ in a circular orbit of radius $r$ around a central mass $M$ (where $M \gg m$, so the central body is effectively fixed). Two forces balance: gravitational attraction and centripetal force required for circular motion.

- **Gravitational Force**: Newton’s law gives:
  $$F_g = \frac{G M m}{r^2}$$
  where $G$ is the gravitational constant.
- **Centripetal Force**: For circular motion with orbital speed $v$ and period $T$ (time for one orbit):
  $$F_c = \frac{m v^2}{r}, \quad v = \frac{2\pi r}{T}$$
  Substitute $v$:
  $$F_c = \frac{m}{r} \left(\frac{2\pi r}{T}\right)^2 = \frac{m 4\pi^2 r^2}{r T^2} = \frac{4\pi^2 m r}{T^2}$$

Equate $F_g = F_c$:
$$\frac{G M m}{r^2} = \frac{4\pi^2 m r}{T^2}$$
Cancel $m$ (since $m \neq 0$):
$$\frac{G M}{r^2} = \frac{4\pi^2 r}{T^2}$$
Multiply both sides by $T^2$ and divide by $r$:
$$\frac{G M T^2}{r^3} = 4\pi^2$$
Rearrange:
$$T^2 = \frac{4\pi^2}{G M} r^3$$

*Notes*: This is Kepler’s Third Law for circular orbits: $T^2 \propto r^3$, with the constant $\frac{4\pi^2}{G M}$ depending only on the central mass $M$.

## 2. Implications for Astronomy

*Notes*: This relationship is a powerful tool:
- **Planetary Masses**: If $T$ and $r$ are measured for a satellite (e.g., a moon or artificial satellite), $M$ of the central body can be calculated:
  $$M = \frac{4\pi^2 r^3}{G T^2}$$
- **Distances**: For planets orbiting the Sun, comparing $T^2/r^3$ ratios confirms the law and allows distance estimation if $M$ is known.
- **Universality**: Applies to any gravitational system (planets, moons, binary stars).

*Examples*:
- **Moon around Earth**: $T \approx 27.32$ days, $r \approx 384,400$ km, used to estimate Earth’s mass.
- **Earth around Sun**: $T = 1$ year, $r = 1$ AU, calibrates the Sun’s mass.

*Notes*: It’s foundational for orbit design (e.g., geostationary satellites) and exoplanet studies.

## 3. Analysis of Real-World Examples

*Notes*: Let’s verify with data:
- **Moon**: $T = 27.32$ days = $2.36 \times 10^6$ s, $r = 3.844 \times 10^8$ m, $G = 6.6743 \times 10^{-11}$ m³/kg·s², Earth’s $M \approx 5.972 \times 10^{24}$ kg.


  - $T^2 = (2.36 \times 10^6)^2 = 5.57 \times 10^{12}$ s²

  - $r^3 = (3.844 \times 10^8)^3 = 5.68 \times 10^{25}$ m³
  
  - Check: $\frac{4\pi^2}{G M} = \frac{39.478}{6.6743 \times 10^{-11} \cdot 5.972 \times 10^{24}} \approx 9.91 \times 10^{-14}$ s²/m³
  - $T^2 / r^3 = 5.57 \times 10^{12} / 5.68 \times 10^{25} \approx 9.8 \times 10^{-14}$ s²/m³—matches closely!

*Notes*: Small discrepancies reflect measurement precision or circular orbit assumption.

## 4. Implementation

*Notes*: We’ll simulate circular orbits and plot $T^2$ vs. $r^3$ to verify the law.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.6743e-11  # m^3/kg·s^2
M_earth = 5.972e24  # kg
M_sun = 1.989e30  # kg

# Orbital period function
def orbital_period(r, M):
    return np.sqrt((4 * np.pi**2 * r**3) / (G * M))

# Orbital radii (m)
r_values = np.logspace(6, 9, 100)  # 10^6 to 10^9 m

# Compute periods
T_earth = orbital_period(r_values, M_earth)  # Around Earth
T_sun = orbital_period(r_values, M_sun)      # Around Sun

# Plot T^2 vs r^3
plt.figure(figsize=(12, 6))

# Log-log plot
plt.subplot(1, 2, 1)
plt.loglog(r_values**3, T_earth**2, 'b-', label='Earth (M = 5.972e24 kg)')
plt.loglog(r_values**3, T_sun**2, 'r-', label='Sun (M = 1.989e30 kg)')
plt.xlabel('r³ (m³)')
plt.ylabel('T² (s²)')
plt.title('T² vs r³ (Kepler\'s Third Law)')
plt.grid(True, which="both", ls="--")
plt.legend()

# Circular orbit visualization (Moon example)
r_moon = 3.844e8  # m
T_moon = orbital_period(r_moon, M_earth)
theta = np.linspace(0, 2*np.pi, 100)
x_moon = r_moon * np.cos(theta)
y_moon = r_moon * np.sin(theta)

plt.subplot(1, 2, 2)
plt.plot(x_moon, y_moon, 'b-', label=f'Moon Orbit (r = {r_moon/1e6:.1f} Mm)')
plt.plot(0, 0, 'ko', label='Earth')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.title('Circular Orbit Visualization')
plt.axis('equal')
plt.legend()

plt.tight_layout()
plt.show()

# Verify with Moon data
print(f"Moon: T = {T_moon/86400:.2f} days, r = {r_moon/1e6:.1f} Mm")

# Verify with Moon data
print(f"Moon: T = {T_moon/86400:.2f} days, r = {r_moon/1e6:.1f} Mm")
```
![alt text](image.png)


*Notes on Code*:
- **Function**: `orbital_period` computes $T = \sqrt{\frac{4\pi^2 r^3}{G M}}$.
- **Data**: $r$ spans realistic ranges; $T$ calculated for Earth and Sun.
- **Plots**:
  - Left: Log-log $T^2$ vs. $r^3$—a straight line confirms $T^2 \propto r^3$.
  - Right: Visualizes the Moon’s orbit as a circle.
- **Verification**: Moon’s $T$ matches ~27 days.

## Discussion on Extensions

*Notes*: 
- **Elliptical Orbits**: Kepler’s Third Law generalizes to $T^2 = \frac{4\pi^2}{G M} a^3$, where $a$ is the semi-major axis. The derivation uses angular momentum and energy conservation, not circular motion.
- **Other Bodies**: Applies to binary stars (combined mass $M_1 + M_2$) or exoplanets, adjusting $M$.

*Limitations*:
- Assumes $M \gg m$ (central mass dominates).
- Ignores perturbations (e.g., other planets).

*Notes*: Elliptical extension broadens applicability to most orbits.

---

### Rendering and Running in VS Code
- **File**: Save as `orbital_period.md`.
- **Rendering**: Use "Markdown+Math" extension; preview with `Ctrl+Shift+V`.
- **Code**: Extract to `orbital_period.py` or use a `.ipynb` with the "Jupyter" extension.
- **Requirements**: Install `numpy`, `matplotlib` (`pip install numpy matplotlib`).

### Output Notes
- **Graph**: $T^2$ vs. $r^3$ is linear on a log-log scale, slope depends on $M$.
- **Orbit**: Moon’s path is circular, visually confirming the setup.
- **Moon Data**: $T \approx 27.32$ days matches reality.

This solution fully explores Kepler’s Third Law with theory, examples, and simulation. 