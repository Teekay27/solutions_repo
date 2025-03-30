# Problem 2
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

## Theoretical Foundation
 The forced damped pendulum is governed by the equation:
 $$ \ddot{\theta} + b \dot{\theta} + \omega_0^2 \sin\theta = A \cos(\omega t) $$
where:
 - $b$ is the damping coefficient,
 - $\omega_0$ is the natural frequency,
 - $A$ is the driving amplitude,
 - $\omega$ is the driving frequency.

 For small angles, we approximate $\sin\theta \approx \theta$,
 reducing the equation to:
 $$ \ddot{\theta} + b \dot{\theta} + \omega_0^2 \theta = A \cos(\omega t) $$
 This is a linear, nonhomogeneous differential equation that exhibits
 resonance when $\omega$ is close to $\omega_0$.

 Energy Considerations
 The total energy of the system consists of kinetic and potential energy:
 $$ E = \frac{1}{2} m L^2 \dot{\theta}^2 + mgL(1 - \cos\theta) $$
 Damping dissipates energy over time, and the external force injects energy into the system,
 leading to complex behaviors such as periodic motion, quasiperiodicity, and chaos.
