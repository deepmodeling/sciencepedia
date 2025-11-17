## Introduction
Understanding how local soil conditions modify [seismic waves](@entry_id:164985) is a cornerstone of [earthquake engineering](@entry_id:748777). The complex patterns of ground shaking observed during earthquakes are often governed by the amplification and resonance that occur as waves travel through near-surface soil deposits. While analyzing these phenomena in the time domain can be intricate, frequency-domain analysis offers a powerful and elegant alternative. This approach simplifies the complex problem of wave propagation into algebraic operations, providing deep insights into the mechanisms of site amplification. This article demystifies the theory and practice of frequency-domain [site response analysis](@entry_id:754930). The journey begins in "Principles and Mechanisms," where we lay the mathematical groundwork with the Fourier Transform and explore the physics of [wave propagation in soils](@entry_id:756647). Next, "Applications and Interdisciplinary Connections" demonstrates how these principles are applied to solve real-world problems in geotechnical engineering, seismology, and [soil-structure interaction](@entry_id:755022). Finally, "Hands-On Practices" offers practical exercises to solidify your understanding of these critical computational methods.

## Principles and Mechanisms

Frequency-domain analysis provides a powerful framework for understanding and quantifying the modification of [seismic waves](@entry_id:164985) as they propagate through near-surface soil deposits. By decomposing complex time-domain motions into their constituent harmonic components, we can leverage the principles of [linear systems theory](@entry_id:172825) and wave mechanics to develop profound insights into the phenomena of site amplification, resonance, and damping. This chapter elucidates the fundamental principles and mechanisms that govern site response in the frequency domain, moving from the mathematical foundations to the physical processes and their practical implementation in computational models.

### Mathematical Foundations: The Fourier Transform

The cornerstone of frequency-domain analysis is the **Fourier Transform**, a mathematical operation that resolves a time-dependent signal into its [frequency spectrum](@entry_id:276824). For a continuous signal in time, $x(t)$, its representation in the angular frequency domain, $X(\omega)$, is obtained through the Continuous-Time Fourier Transform (CTFT). While several conventions exist for the normalization of the transform pair, a standard in engineering and signal processing is the asymmetric form. The forward transform is defined as:

$$ X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-i\omega t} dt $$

This integral computes the [complex amplitude](@entry_id:164138), $X(\omega)$, of the harmonic component with [angular frequency](@entry_id:274516) $\omega$ present in the signal $x(t)$. The original time-domain signal can be perfectly reconstructed from its spectrum using the Inverse Continuous-Time Fourier Transform (ICTFT):

$$ x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(\omega) e^{i\omega t} d\omega $$

The factor of $\frac{1}{2\pi}$ ensures that the successive application of the transform and its inverse recovers the original signal.

In computational practice, we work with digitized seismic records, which are discrete sequences of data sampled at uniform time intervals. For a signal $a(t)$ sampled at an interval $\Delta t$ to produce a sequence of $N$ points, $\{a_n\}_{n=0}^{N-1}$ where $a_n = a(n\Delta t)$, the computational tool is the **Discrete Fourier Transform (DFT)**. A common convention for the DFT pair, consistent with many numerical libraries, is:

$$ X_k = \sum_{n=0}^{N-1} x_n e^{-i \frac{2\pi k n}{N}} $$

$$ x_n = \frac{1}{N} \sum_{k=0}^{N-1} X_k e^{i \frac{2\pi k n}{N}} $$

Here, $X_k$ is the [complex amplitude](@entry_id:164138) at the $k$-th discrete frequency bin. To evaluate a continuous theoretical model, such as a site transfer function, on the same frequency grid as the DFT, we must establish the relationship between the discrete frequency index $k$ and the continuous [angular frequency](@entry_id:274516) $\omega$. The total duration of the record is $T = N \Delta t$. The [frequency resolution](@entry_id:143240) of the DFT is $\Delta f = 1/T = 1/(N \Delta t)$. The discrete frequencies $f_k$ are integer multiples of this resolution, $f_k = k \Delta f$. Converting to [angular frequency](@entry_id:274516) ($\omega = 2\pi f$), the discrete angular frequency bins are given by:

$$ \omega_k = \frac{2\pi k}{N \Delta t} \quad \text{for } k=0, 1, \dots, N-1 $$

This set of definitions provides a consistent mathematical framework for moving between continuous theory and discrete computation [@problem_id:3559022].

A critical consideration in practice is that the DFT implicitly treats the finite-length record as one period of an infinitely repeating signal. This is equivalent to multiplying the "true," infinite-duration signal by a rectangular window in the time domain. Due to the convolution theorem, this multiplication in time corresponds to a convolution in the frequency domain with the Fourier transform of the rectangular window—a sinc function. The prominent side lobes of the sinc function cause energy from strong frequency components to "leak" into the estimates of adjacent, weaker components. This **[spectral leakage](@entry_id:140524)** can introduce significant bias into spectral estimates. To mitigate this, the time-series data for both input and output motions are often tapered using a [window function](@entry_id:158702), such as a cosine taper or a **Hann window**, before performing the DFT. These windows have much lower side lobes, which drastically reduces leakage from distant frequencies. The trade-off is a wider main lobe, which slightly reduces the ability to resolve closely spaced frequency components. This practice is crucial for obtaining accurate estimates of transfer functions, especially near sharp resonances where spectral amplitudes change rapidly [@problem_id:3559030] [@problem_id:3559031].

### The Site Transfer Function

In [site response analysis](@entry_id:754930), the soil column is often idealized as a **Linear Time-Invariant (LTI)** system. This idealization assumes that the soil's response is directly proportional to the excitation (linearity) and that its properties do not change over time ([time invariance](@entry_id:198838)). For such a system, the relationship between an input signal, $x_{in}(t)$, and the corresponding output signal, $x_{out}(t)$, is described by the [convolution integral](@entry_id:155865) with the system's [impulse response function](@entry_id:137098), $h(t)$.

In the frequency domain, this complex relationship simplifies to algebraic multiplication. If $X_{in}(\omega)$, $X_{out}(\omega)$, and $H(\omega)$ are the Fourier transforms of $x_{in}(t)$, $x_{out}(t)$, and $h(t)$ respectively, then:

$$ X_{out}(\omega) = H(\omega) X_{in}(\omega) $$

The function $H(\omega)$ is the system's **transfer function**. It is a [complex-valued function](@entry_id:196054) of frequency that represents the intrinsic dynamic characteristics of the site. Its magnitude, $|H(\omega)|$, describes the amplification or de-amplification of a harmonic component at frequency $\omega$, while its phase, $\arg(H(\omega))$, describes the phase shift introduced by the system at that frequency.

A key property of LTI systems is that the transfer function is independent of the kinematic quantity used to define it, provided a "like-for-like" ratio is used. For example, let us define transfer functions for displacement ($H_u$), velocity ($H_v$), and acceleration ($H_a$) as ratios of the surface motion spectrum to the input motion spectrum of the same type. Using the differentiation property of the Fourier transform, where the transform of a time derivative $\dot{f}(t)$ is $i\omega F(\omega)$, we find:

$$ H_v(\omega) = \frac{\hat{v}_{surf}(\omega)}{\hat{v}_{in}(\omega)} = \frac{i\omega \hat{u}_{surf}(\omega)}{i\omega \hat{u}_{in}(\omega)} = \frac{\hat{u}_{surf}(\omega)}{\hat{u}_{in}(\omega)} = H_u(\omega) $$

$$ H_a(\omega) = \frac{\hat{a}_{surf}(\omega)}{\hat{a}_{in}(\omega)} = \frac{(i\omega)^2 \hat{u}_{surf}(\omega)}{(i\omega)^2 \hat{u}_{in}(\omega)} = \frac{\hat{u}_{surf}(\omega)}{\hat{u}_{in}(\omega)} = H_u(\omega) $$

Thus, for any LTI system, the displacement, velocity, and acceleration [transfer functions](@entry_id:756102) are identical: $H_u(\omega) = H_v(\omega) = H_a(\omega)$. This fundamental result stems directly from the commutation of the [differentiation operator](@entry_id:140145) and the LTI system operator. If, however, a "mixed-type" transfer function is defined, such as the ratio of surface acceleration to input displacement, the frequency-dependent factors do not cancel. For instance, $\hat{a}_{surf}(\omega)/\hat{u}_{in}(\omega) = -\omega^2 H_u(\omega)$ [@problem_id:3559058].

### Wave Propagation Mechanics in Viscoelastic Media

The transfer function of a soil site is fundamentally governed by the physics of [wave propagation](@entry_id:144063). For vertically propagating shear waves in a horizontally layered medium, the governing [one-dimensional wave equation](@entry_id:164824) in the frequency domain is:

$$ G^*(\omega) \frac{d^2 u}{dz^2} + \rho \omega^2 u = 0 $$

Here, $u$ is the complex displacement amplitude, $z$ is the spatial coordinate, $\rho$ is the mass density, and $G^*(\omega)$ is the **complex shear modulus**. The [complex modulus](@entry_id:203570) is a convenient way to represent linear viscoelastic behavior, encapsulating both stiffness and [energy dissipation](@entry_id:147406). It is written as $G^*(\omega) = G'(\omega) + iG''(\omega)$, where $G'(\omega)$ is the **storage modulus** (representing elastic stiffness) and $G''(\omega)$ is the **loss modulus** (representing energy dissipation or damping).

The ratio of energy dissipated per cycle to the maximum stored elastic energy is related to the material **[damping ratio](@entry_id:262264)**, $\xi$. For harmonic loading, this can be shown to be equal to $\xi(\omega) = \frac{G''(\omega)}{2G'(\omega)}$. Different [rheological models](@entry_id:193749) imply different frequency dependencies for the [damping ratio](@entry_id:262264) [@problem_id:3559034]:

*   **Kelvin-Voigt Model**: $G^*(\omega) = G + i\omega\eta$, where $G$ is the elastic modulus and $\eta$ is viscosity. This model yields a damping ratio $\xi(\omega) = \frac{\omega\eta}{2G}$, which increases linearly with frequency. This is often unrealistic for soils over the frequency range of seismic interest.
*   **Hysteretic Model**: $G^*(\omega) = G(1+2i\xi)$, where the damping ratio $\xi$ is assumed to be a constant material parameter. This model, also known as the constant-loss model, is widely used in frequency-domain [site response analysis](@entry_id:754930) because it provides a more realistic, frequency-independent damping over a broad band of frequencies.

The wave equation can be rewritten as a Helmholtz equation, $\frac{d^2 u}{dz^2} + (k^*)^2 u = 0$, where $k^* = \omega \sqrt{\rho/G^*(\omega)}$ is the **[complex wavenumber](@entry_id:274896)**. The imaginary part of $k^*$ represents the attenuation of the wave as it propagates.

A crucial concept in [wave propagation](@entry_id:144063) is **shear impedance**, defined as $Z(\omega) = \rho \beta^*(\omega)$, where $\beta^*(\omega) = \sqrt{G^*(\omega)/\rho}$ is the complex [shear wave velocity](@entry_id:754765). Impedance can be interpreted as the material's resistance to shear motion. At the interface between two media with different impedances, an incident wave is partially reflected and partially transmitted. For a shear wave normally incident from medium 1 to medium 2, continuity of displacement and traction at the interface dictates the amplitudes of the reflected and transmitted waves. The displacement transmission coefficient, $t_u$, is the ratio of the transmitted displacement amplitude to the incident displacement amplitude and is given by:

$$ t_u(\omega) = \frac{2 Z_1(\omega)}{Z_1(\omega) + Z_2(\omega)} $$

When a wave travels from a stiffer, denser medium (higher impedance, $Z_1$) to a softer, less dense medium (lower impedance, $Z_2$), such as from rock to soil, the magnitude of the denominator, $|Z_1 + Z_2|$, is less than $2|Z_1|$. This leads to a transmission coefficient magnitude $|t_u(\omega)| > 1$. This phenomenon, where the displacement amplitude increases upon entering a lower-impedance medium, is a fundamental mechanism of seismic amplification [@problem_id:3559067].

### Resonant Amplification in a Soil Layer

The interplay of reflections from multiple boundaries within a [soil profile](@entry_id:195342) leads to the phenomenon of resonance. Consider the canonical problem of a single, homogeneous soil layer of thickness $H$ and [shear wave velocity](@entry_id:754765) $\beta$ overlying rigid bedrock. By [solving the wave equation](@entry_id:171826) with boundary conditions of prescribed motion at the base and zero stress at the free surface, one can derive the transfer function relating surface motion to base motion:

$$ T(\omega) = \frac{1}{\cos(k^*H)} $$

For an undamped medium ($\xi=0$, so $k^*$ is real, $k=\omega/\beta$), the transfer function amplitude $|T(\omega)|$ approaches infinity when the denominator is zero. This defines the **resonant frequencies** of the layer:

$$ \cos\left(\frac{\omega_n H}{\beta}\right) = 0 \quad \implies \quad \frac{\omega_n H}{\beta} = (2n-1)\frac{\pi}{2}, \quad n=1, 2, 3, \dots $$

The fundamental resonance ($n=1$) occurs at an [angular frequency](@entry_id:274516) $\omega_0 = \frac{\pi\beta}{2H}$, which corresponds to a frequency in Hertz of $f_0 = \frac{\beta}{4H}$. This is the well-known "quarter-wavelength" condition: resonance occurs when the layer thickness is one-quarter of the wavelength of the seismic wave.

When material damping is introduced, the [complex wavenumber](@entry_id:274896) $k^*$ prevents the denominator from becoming zero. The amplification at resonance is finite. For small, [hysteretic damping](@entry_id:750492) ($\xi \ll 1$), the peak amplification at the [fundamental frequency](@entry_id:268182) is approximately:

$$ A_{max} = |T(f_0)| \approx \frac{2}{\pi\xi} $$

This shows that the peak amplification is inversely proportional to the [damping ratio](@entry_id:262264). Damping also broadens the resonance peak. The **half-power bandwidth**, $\Delta f$, which measures the width of the resonance peak at an amplitude of $A_{max}/\sqrt{2}$, can be shown to be:

$$ \Delta f \approx 2\xi f_0 $$

These results for a single layer provide critical intuition: site amplification is controlled by the impedance contrast (which produces the reflections), the layer thickness and velocity (which determine the resonant frequencies), and the material damping (which limits the peak amplification and broadens the response) [@problem_id:3559038].

### Practical and Computational Considerations

#### Defining the Input Motion

A critical step in any [site response analysis](@entry_id:754930) is correctly defining the input motion. A common misconception is to use a recording from a nearby rock outcrop directly as the input at the base of the soil column. This is incorrect. The motion at a free surface, such as an outcrop, is the superposition of the incident upward-propagating wave and the wave reflected from the free surface. For SH waves, the reflection is perfect and in-phase, causing the outcrop surface motion to be twice the amplitude of the incident upward-propagating wave. The motion that drives the soil column from below is only this upward-propagating component, often called the **within-motion** or incident motion. Therefore, to obtain the correct input for a [site response analysis](@entry_id:754930), the outcrop record must be processed. This process, known as **[deconvolution](@entry_id:141233)**, involves mathematically removing the free-surface effect, typically by dividing the outcrop spectrum by two [@problem_id:3559031].

#### Stochastic and Nonlinear Analysis

While deterministic analysis using a single time history is common, [earthquake ground motion](@entry_id:748778) is inherently a random process. A stochastic approach characterizes the input motion by its **Power Spectral Density (PSD)**, $S_{in}(\omega)$, which describes the distribution of power across frequencies. For an LTI system, the output PSD is related to the input PSD by a simple and elegant formula:

$$ S_{out}(\omega) = |H(\omega)|^2 S_{in}(\omega) $$

This relationship holds provided the system is LTI and the input process is **Wide-Sense Stationary (WSS)**, meaning its statistical properties (like mean and autocorrelation) do not change over time. This powerful result allows for the statistical characterization of the surface motion given a statistical description of the bedrock motion and the site's transfer function [@problem_id:3559059].

Real soil behavior is nonlinear: stiffness degrades and damping increases as [shear strain](@entry_id:175241) levels rise. The **Equivalent-Linear (EQL)** method is a widely-used approximation to account for this behavior. It is an iterative procedure performed in the frequency domain:
1.  **Initialize**: Start with small-strain properties ($G_{max}$, low damping) for each layer.
2.  **Analyze**: Compute the linear response of the layered system to the input motion, and determine the strain time history in each layer.
3.  **Update**: For each layer, calculate an "effective" shear strain (typically 65% of the peak strain). Use strain-dependent modulus reduction and damping curves to find new values for $G$ and $\xi$ compatible with this effective strain.
4.  **Iterate**: Repeat the analysis with the updated properties until the properties in all layers converge to a stable solution.

This process finds a set of linear properties that are consistent with the strain levels they produce, effectively approximating the nonlinear response with a [secant modulus](@entry_id:199454) and an equivalent [viscous damping](@entry_id:168972) [@problem_id:3559025].

#### Numerical Stability in Layered Media

The computation of the transfer function for a multi-layered [soil profile](@entry_id:195342) is often performed using the **[propagator matrix](@entry_id:753816)** method. This involves defining a $2 \times 2$ matrix for each layer that propagates the state vector (displacement and traction) from the top to the bottom of the layer. The total propagator for the entire stack is the product of the individual layer matrices. However, in a viscoelastic medium (i.e., with damping), the [complex wavenumber](@entry_id:274896) leads to solution components that grow or decay exponentially with depth. The [propagator matrix](@entry_id:753816) mixes these growing and decaying terms. For deep soil profiles or at high frequencies, the exponential growth term dominates, and the [numerical precision](@entry_id:173145) of a computer is insufficient to retain information about the decaying solution. This leads to an exponentially growing condition number for the total [propagator matrix](@entry_id:753816), causing severe numerical instability. This is an inherent flaw of the classical [propagator](@entry_id:139558) formulation, not just an issue of [roundoff error](@entry_id:162651). To overcome this, numerically stable alternatives, such as methods based on **scattering matrices** or [global stiffness matrix assembly](@entry_id:196781), have been developed. These methods avoid the explicit multiplication of ill-conditioned matrices and are robust for any frequency or number of layers [@problem_id:3559079].