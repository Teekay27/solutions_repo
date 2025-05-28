# Problem 1

# Interference Patterns on a Water Surface

## 1. Problem Setup and Wave Equation

*Notes*: We’re tasked with analyzing the interference patterns created by circular waves on a water surface, emitted from point sources at the vertices of a regular polygon. Let’s break this down step by step.

The wave from a single point source at position
 $(x_s, y_s)$ 
 is given by the Single Disturbance equation:


$h(x, y, t) = A \cos(k r - \omega t + \phi)$

where:


- $h(x, y, t)$ is the displacement of the water surface at point $(x, y)$ and time $t$,

- $A$ is the amplitude of the wave,

- $k = \frac{2\pi}{\lambda}$ is the wave number, with $\lambda$ being the wavelength,

- $\omega = 2\pi f$ is the angular frequency, with $f$ being the frequency,

- $r = \sqrt{(x - x_s)^2 + (y - y_s)^2}$ is the distance from the source to the point $(x, y)$,

# Interference Patterns on a Water Surface

Interference occurs when waves from different sources overlap. On a water surface, this can be seen when ripples from various points meet and form patterns—constructive interference where waves reinforce each other, and destructive interference where they cancel out. These visual patterns help us understand wave behavior and interactions in a tangible way.

A single circular wave on the water surface from a point source is modeled as:

$$
\eta(x, y, t) = \frac{A}{\sqrt{r}} \cdot \cos(kr - \omega t + \phi)
$$

Where:  
- \( \eta(x, y, t) \) is the displacement of the water surface at point \( (x, y) \) and time \( t \),  
- \( A \) is the amplitude of the wave,  
- \( r \) is the distance from the source to point \( (x, y) \),  
- \( k = \frac{2\pi}{\lambda} \) is the wave number,  
- \( \omega = 2\pi f \) is the angular frequency,  
- \( \phi \) is the phase offset.

Now, suppose we place point sources at the vertices of a regular polygon (like a square or triangle). Each source emits a wave described by the equation above. The principle of superposition tells us that the total displacement at any point is the sum of displacements from each source:

$$
\eta_{\text{total}}(x, y, t) = \sum_{i=1}^{N} \frac{A}{\sqrt{r_i}} \cdot \cos(k r_i - \omega t + \phi)
$$

Where \( r_i \) is the distance from the \( i \)-th source to the point \( (x, y) \), and \( N \) is the number of sources.

This superposition results in a complex interference pattern that depends on the number and position of the sources.

To visualize this, we can simulate the system using Python. Here's the code:

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1.0  # Amplitude
wavelength = 1.0
k = 2 * np.pi / wavelength  # Wave number
omega = 2 * np.pi  # Angular frequency
phi = 0  # Phase
t = 0  # Time snapshot

# Grid
x = np.linspace(-5, 5, 500)
y = np.linspace(-5, 5, 500)
X, Y = np.meshgrid(x, y)

# Define number of sources and polygon radius
N = 4  # Number of sources (e.g., square)
radius = 2.5
angles = np.linspace(0, 2 * np.pi, N, endpoint=False)
sources = [(radius * np.cos(a), radius * np.sin(a)) for a in angles]

# Initialize displacement
eta_total = np.zeros_like(X)

# Superpose waves from each source
for sx, sy in sources:
    R = np.sqrt((X - sx)**2 + (Y - sy)**2)
    eta = A / np.sqrt(R + 1e-6) * np.cos(k * R - omega * t + phi)
    eta_total += eta

# Plot the interference pattern
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, eta_total, levels=100, cmap='plasma')
plt.colorbar(label='Water Surface Displacement')
plt.title('Water Wave Interference Pattern from Regular Polygon Sources')
plt.xlabel('x')
plt.ylabel('y')
plt.axis('equal')
plt.show()



*Notes*: This equation gives the combined wave displacement. The interference pattern depends on the differences in $r_i$, which affect the phase $k r_i$ at each point.

## 6. Step 5: Analyze Interference Patterns

*Notes*: Let’s understand what creates the interference pattern:
- **Constructive Interference**: Occurs when the waves are in phase, meaning the phase difference $k (r_i - r_j)$ between any two waves is a multiple of $2\pi$. This happens when the path difference $r_i - r_j$ is a multiple of the wavelength $\lambda$ (since $k = \frac{2\pi}{\lambda}$, so $k (r_i - r_j) = 2\pi \frac{r_i - r_j}{\lambda}$). The waves add up, making the displacement larger.


- **Destructive Interference**: Occurs when the waves are out of phase by $\pi$ (180 degrees), so the phase difference $k (r_i - r_j) = (2n+1)\pi$. This happens when the path difference is an odd multiple of $\lambda/2$. The waves cancel out, making the displacement zero.



*Notes*: The pattern will be symmetric because the square is symmetric. We expect:
- High displacement (constructive) where the distances from the sources allow the waves to align.
- Low or zero displacement (destructive) where the waves cancel out.



## 7. Step 6: Visualization with Python

*Notes*: We’ll use Python to simulate the interference pattern on a 2D grid at a fixed time $t$. Let’s choose some values:
- Amplitude: $A = 1$ m.
- Wavelength: $\lambda = 0.5$ m, so $k = \frac{2\pi}{\lambda} = \frac{2\pi}{0.5} \approx 12.566$ rad/m.
- Frequency: $f = 1$ Hz, so $\omega = 2\pi f = 2\pi \approx 6.283$ rad/s.
- Time: $t = 0$ s (to see the initial pattern; we can animate later if needed).

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
A = 1.0  # Amplitude (m)
lambda_ = 0.5  # Wavelength (m)
k = 2 * np.pi / lambda_  # Wave number (rad/m)
f = 1.0  # Frequency (Hz)
omega = 2 * np.pi * f  # Angular frequency (rad/s)
t = 0.0  # Time (s)

# Source positions (vertices of a square with side length 2, so a = 1)
sources = [(1, 1), (1, -1), (-1, -1), (-1, 1)]

# Create a grid of points
x = np.linspace(-3, 3, 200)  # x from -3 to 3 meters
y = np.linspace(-3, 3, 200)  # y from -3 to 3 meters
X, Y = np.meshgrid(x, y)

# Calculate the total displacement
H = np.zeros_like(X)  # Total displacement
for (xs, ys) in sources:
    r = np.sqrt((X - xs)**2 + (Y - ys)**2)  # Distance from source to point
    H += A * np.cos(k * r - omega * t)  # Add wave from this source

# Plotting
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, H, levels=50, cmap='seismic')  # Contour plot with color
plt.colorbar(label='Displacement (m)')
plt.contour(X, Y, H, levels=[0], colors='black')  # Zero displacement lines (destructive)
plt.scatter([s[0] for s in sources], [s[1] for s in sources], c='black', marker='o', label='Sources')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.title('Interference Pattern from Four Sources (Square)')
plt.axis('equal')
plt.legend()
plt.grid(True)
plt.show()
```
![alt text](image.png)

*Notes on Code*:
- **Setup**: Defines the wave parameters and positions of the four sources at the square’s vertices.
- **Grid**: Creates a 2D grid of points $(x, y)$ to calculate the displacement.
- **Superposition**: Sums the displacement from each source at every point on the grid.
- **Plot**: Uses a contour plot to show the displacement, with colors indicating amplitude (red for positive, blue for negative). Black lines show where displacement is zero (destructive interference). Black dots mark the sources.

## 8. Explanation of Interference Patterns

*Notes*: Let’s analyze the plot:
- **Constructive Interference**: Bright red or blue areas show where the displacement is large (positive or negative). This happens where the waves from the sources arrive in phase, like along the axes ($x = 0$ or $y = 0$), where the distances from opposite sources are equal, so the path difference is zero.
- **Destructive Interference**: Black lines show where the displacement is zero. This happens where waves cancel out, like where the path difference between sources is $\lambda/2$ (0.25 m), causing a phase difference of $\pi$.
- **Symmetry**: The pattern is symmetric about the x-axis, y-axis, and diagonals, because the square is symmetric.
- **Nodal Lines**: The black lines form a grid-like pattern, showing regions where destructive interference creates “calm” spots on the water.

*Notes*: The pattern looks like a checkerboard, with alternating regions of high and low displacement, typical of interference from multiple coherent sources.

## Discussion on Extensions

*Notes*:
- **Different Polygons**: A triangle (3 sources) would create a simpler pattern, while a pentagon (5 sources) would be more complex, with more interference points.
- **Animation**: We could vary $t$ to animate the waves, showing how the pattern moves over time.
- **Phase Differences**: If the sources had different initial phases $\phi$, the pattern would shift, changing where constructive and destructive regions occur.
- **Real-World Applications**: This interference is similar to what happens in acoustics (sound waves), optics (light waves), or even quantum mechanics (wavefunctions), helping us design things like antennas or predict wave behavior in nature.

*Notes*: This simulation helps us see how waves combine, a key idea in physics with applications from water waves to technology.

---

### Rendering and Running in VS Code
- **File**: Save as `interference_patterns.md`.
- **Rendering**: Use the "Markdown+Math" extension; preview with `Ctrl+Shift+V` to see equations like $h(x, y, t)$ and $$k$$.
- **Code**: Extract the Python code to `interference_patterns.py` or use a `.ipynb` file with the "Jupyter" extension.
- **Requirements**: Install `numpy` and `matplotlib` (`pip install numpy matplotlib`).

### Output Notes
- **Plot**: The contour plot shows:
  - Red and blue regions: High displacement (constructive interference).
  - Black lines: Zero displacement (destructive interference).
  - Black dots: The four sources at the square’s vertices.
- **Pattern**: A symmetric, grid-like pattern with alternating high and low displacement areas, showing how the waves interfere.

This solution explains wave interference in a simple way, with clear math, a simulation, and a visual representation of the pattern. It’s all set for you to copy and paste! Let me know if you’d like to try a different polygon or add animation.

