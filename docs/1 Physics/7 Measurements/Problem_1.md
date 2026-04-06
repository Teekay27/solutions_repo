# Problem 1


# Measuring Earth's Gravitational Acceleration with a Pendulum

## 1. Procedure and Data Collection

*Notes*: We’re tasked with measuring the acceleration due to gravity $g$ using a simple pendulum. The period $T$ of a simple pendulum (for small angles) is given by:
$$T = 2\pi \sqrt{\frac{L}{g}}$$
where $L$ is the length of the pendulum, and $g$ is the gravitational acceleration. Solving for $g$:
$$g = \frac{4\pi^2 L}{T^2}$$

### 1.1 Materials and Setup
- **String Length**: Let’s assume a length of $L = 1.0$ m (1 meter).
- **Weight**: A small bag of coins.
- **Measuring Tools**:
  - Ruler with a resolution of 1 mm (0.001 m), so uncertainty in length $\delta L = \frac{\text{resolution}}{2} = 0.0005$ m.
  - Stopwatch with a resolution of 0.01 s, so uncertainty in a single time measurement $\delta t_{\text{res}} = 0.005$ s.
- **Setup**: The weight is attached to the string, and the string is fixed to a support. The length $L$ is measured from the suspension point to the center of the weight.

*Notes*: The measured length is $L = 1.0 \pm 0.0005$ m.

### 1.2 Data Collection
*Notes*: We displace the pendulum by a small angle (<15°) and measure the time for 10 full oscillations, repeating this 10 times. Let’s simulate realistic data for the time of 10 oscillations ($t_{10}$), assuming a true $g \approx 9.81$ m/s² and adding some random variation to mimic human timing errors.

First, calculate the expected period $T$ for $L = 1.0$ m and $g = 9.81$ m/s²:
$$T = 2\pi \sqrt{\frac{1.0}{9.81}} \approx 2\pi \sqrt{0.1019} \approx 2\pi \cdot 0.3192 \approx 2.006 \, \text{s}$$
Time for 10 oscillations: $t_{10} = 10 \cdot T \approx 20.06$ s.

Simulate 10 measurements with a mean of 20.06 s and a standard deviation of 0.1 s (to account for human reaction time variability):

| Trial | Time for 10 Oscillations, $t_{10}$ (s) |
|-------|----------------------------------------|
| 1     | 20.05                                  |
| 2     | 20.12                                  |
| 3     | 19.98                                  |
| 4     | 20.07                                  |
| 5     | 20.15                                  |
| 6     | 20.03                                  |
| 7     | 20.09                                  |
| 8     | 20.00                                  |
| 9     | 20.14                                  |
| 10    | 20.06                                  |

*Notes*: These values are generated to be realistic, with slight variations due to timing errors.

## 2. Calculations

### 2.1 Calculate the Period
- **Mean Time for 10 Oscillations**:
  $$\bar{t}_{10} = \frac{20.05 + 20.12 + 19.98 + 20.07 + 20.15 + 20.03 + 20.09 + 20.00 + 20.14 + 20.06}{10} = \frac{200.69}{10} = 20.069 \, \text{s}$$

- **Standard Deviation of $t_{10}$**:
  First, compute the variance:
  $$\sigma_{t_{10}}^2 = \frac{1}{10-1} \sum_{i=1}^{10} (t_{10,i} - \bar{t}_{10})^2$$
  Deviations: $(20.05 - 20.069)^2 = (-0.019)^2 = 0.000361$, $(20.12 - 20.069)^2 = 0.051^2 = 0.002601$, ..., $(20.06 - 20.069)^2 = (-0.009)^2 = 0.000081$.
  Sum of squared deviations: $0.000361 + 0.002601 + 0.004761 + 0.000169 + 0.006561 + 0.000529 + 0.000441 + 0.004761 + 0.005041 + 0.000081 = 0.025306$.
  $$\sigma_{t_{10}}^2 = \frac{0.025306}{9} \approx 0.0028118, \quad \sigma_{t_{10}} = \sqrt{0.0028118} \approx 0.0530 \, \text{s}$$

- **Uncertainty in the Mean Time**:
  $$u_{\bar{t}_{10}} = \frac{\sigma_{t_{10}}}{\sqrt{N}} = \frac{0.0530}{\sqrt{10}} \approx \frac{0.0530}{3.162} \approx 0.0168 \, \text{s}$$

- **Period $T$ and Its Uncertainty**:
  $$T = \frac{\bar{t}_{10}}{10} = \frac{20.069}{10} = 2.0069 \, \text{s}$$
  $$u_T = \frac{u_{\bar{t}_{10}}}{10} = \frac{0.0168}{10} = 0.00168 \, \text{s}$$

*Notes*: So, $T = 2.0069 \pm 0.00168$ s.

### 2.2 Determine $g$
Using the formula:
$$g = \frac{4\pi^2 L}{T^2}$$
- $4\pi^2 \approx 4 \times 9.8696 = 39.4784$
- $L = 1.0$ m
- $T = 2.0069$ s, so $T^2 = (2.0069)^2 \approx 4.0276$
$$g = \frac{39.4784 \times 1.0}{4.0276} \approx 9.803 \, \text{m/s}^2$$

### 2.3 Propagate Uncertainties
The relative uncertainty in $g$ comes from uncertainties in $L$ and $T$. Using the formula for error propagation:
$$\frac{\delta g}{g} = \sqrt{\left(\frac{\delta L}{L}\right)^2 + \left(\frac{2 \delta T}{T}\right)^2}$$
- **Relative uncertainty in $L$**:
  $$\frac{\delta L}{L} = \frac{0.0005}{1.0} = 0.0005$$
- **Relative uncertainty in $T$**:
  $$\frac{\delta T}{T} = \frac{0.00168}{2.0069} \approx 0.000837$$
  So, $\frac{2 \delta T}{T} = 2 \times 0.000837 \approx 0.001674$.
- **Total relative uncertainty**:
  $$\frac{\delta g}{g} = \sqrt{(0.0005)^2 + (0.001674)^2} = \sqrt{0.00000025 + 0.000002802} = \sqrt{0.000003052} \approx 0.001747$$
- **Absolute uncertainty in $g$**:
  $$\delta g = g \cdot \frac{\delta g}{g} = 9.803 \times 0.001747 \approx 0.0171 \, \text{m/s}^2$$

*Notes*: So, $g = 9.803 \pm 0.017$ m/s².

## 3. Analysis

### 3.1 Comparison with Standard Value
The standard value of $g$ at Earth’s surface is approximately $g_{\text{standard}} = 9.81$ m/s² (though it varies slightly with location, e.g., 9.80665 m/s² at sea level). Our measured value is:
$$g = 9.803 \pm 0.017 \, \text{m/s}^2$$
- The standard value 9.81 lies within the uncertainty range (9.786 to 9.820), so our measurement is consistent with the expected value.
- The difference is $9.81 - 9.803 = 0.007$ m/s², which is less than the uncertainty, indicating good agreement.

### 3.2 Discussion on Uncertainties and Limitations

- **Effect of Measurement Resolution on $L$**:
  - The ruler’s resolution (1 mm) gives $\delta L = 0.0005$ m, contributing a relative uncertainty of 0.0005 (0.05%). This is small but non-negligible. A more precise tool (e.g., a caliper with 0.1 mm resolution) would reduce $\delta L$ to 0.00005 m, lowering the contribution to $\delta g$.
  - If $L$ were measured incorrectly (e.g., not to the center of mass), it could introduce a systematic error, biasing $g$.

- **Variability in Timing and Its Impact on $T$**:
  - The standard deviation of $t_{10}$ (0.0530 s) reflects variability in timing, likely due to human reaction time. The uncertainty in the mean $u_{\bar{t}_{10}} = 0.0168$ s translates to $u_T = 0.00168$ s, contributing a relative uncertainty in $T$ of 0.000837. Since $g \propto \frac{1}{T^2}$, this uncertainty is doubled in $g$, making timing the dominant source of error (0.001674 vs. 0.0005 from $L$).
  - Using a stopwatch with better resolution or automating the timing (e.g., with a photogate) would reduce this uncertainty.

- **Assumptions and Experimental Limitations**:
  - **Small Angle Approximation**: The formula $T = 2\pi \sqrt{\frac{L}{g}}$ assumes small angles (<15°). Larger angles introduce nonlinear effects, increasing the period and underestimating $g$. We kept the angle small, but any deviation could cause a systematic error.
  - **Air Resistance and Friction**: The model assumes no air resistance or friction at the pivot. In reality, these dampen the oscillations, slightly increasing the measured period and underestimating $g$. This effect is small for a short experiment but could be significant over many oscillations.
  - **Length to Center of Mass**: We assumed $L$ is measured to the center of the weight. If the weight is not a point mass, the effective length may differ, introducing a systematic error.
  - **Local Variations in $g$**: The true $g$ varies with altitude and latitude (e.g., 9.78 m/s² at the equator, 9.83 m/s² at the poles). Our comparison assumes a nominal 9.81 m/s², but the actual local value may differ slightly.

*Notes*: The primary sources of uncertainty are the timing variability and, to a lesser extent, the length measurement. Systematic errors (e.g., angle, air resistance) are likely small but could explain the slight deviation from 9.81 m/s².

## 4. Deliverables

### 4.1 Tabulated Data
| Parameter                          | Value              |
|------------------------------------|--------------------|
| Length $L$ (m)                     | 1.0                |
| Uncertainty in $L$, $\delta L$ (m) | 0.0005             |
| Mean time for 10 oscillations, $\bar{t}_{10}$ (s) | 20.069             |
| Standard deviation of $t_{10}$, $\sigma_{t_{10}}$ (s) | 0.0530             |
| Uncertainty in mean time, $u_{\bar{t}_{10}}$ (s) | 0.0168             |
| Period $T$ (s)                     | 2.0069             |
| Uncertainty in $T$, $u_T$ (s)      | 0.00168            |
| Calculated $g$ (m/s²)              | 9.803              |
| Uncertainty in $g$, $\delta g$ (m/s²) | 0.017              |

**Measurements of $t_{10}$ (s)**: 20.05, 20.12, 19.98, 20.07, 20.15, 20.03, 20.09, 20.00, 20.14, 20.06.

### 4.2 Discussion
The experiment successfully measured $g$ as $9.803 \pm 0.017$ m/s², consistent with the standard value of 9.81 m/s². The uncertainty is dominated by timing variability, which could be reduced with better timing methods. Systematic errors, such as the small angle assumption and air resistance, may contribute to the slight deviation but are within the uncertainty range. Improving measurement precision (e.g., using a caliper for $L$, automating timing) and controlling experimental conditions (e.g., minimizing air resistance) would enhance accuracy.

---

### Rendering in VS Code
- **File**: Save as `measure_gravity_pendulum.md`.
- **Rendering**: Use the "Markdown+Math" extension; preview with `Ctrl+Shift+V` to see equations like $T$ and $$g$$.

This solution provides a detailed, realistic simulation of the experiment, with calculations, uncertainty analysis, and a thorough discussion. Let me know if you’d like to adjust the data or explore additional factors!
