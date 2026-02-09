## Applications and Interdisciplinary Connections

The preceding chapters have established the fundamental principles and mechanisms of the Cloud-in-Cell (CIC) mass assignment scheme, focusing on its mathematical construction as a first-order interpolation method and its representation in Fourier space. Having built this theoretical foundation, we now turn our attention to the practical application of these principles. This chapter will explore how the CIC scheme is utilized in scientific computing, primarily within the domain of computational cosmology, and what consequences and artifacts arise from its use.

Our objective is not to re-derive the core concepts but to demonstrate their utility, extension, and integration in diverse, real-world, and interdisciplinary contexts. We will see that while CIC is a powerful and widely used tool, a sophisticated understanding of its properties is essential for the accurate interpretation of simulation results and for distinguishing numerical artifacts from physical phenomena. We will examine applications ranging from the measurement of fundamental cosmological statistics and the conservation of physical quantities to advanced numerical techniques such as adaptive mesh refinement and curvilinear grids. Finally, we will connect these simulation-centric applications to the analysis of observational data, highlighting the scheme's broad relevance in modern astrophysics.

### Core Applications and Artifacts in Cosmological Simulations

The Particle-Mesh (PM) method is a cornerstone of modern N-body simulations, and the CIC scheme is arguably the most common choice for the mass assignment step within this framework. Its balance of computational efficiency and accuracy makes it an attractive default. However, its use introduces several characteristic numerical artifacts that must be understood and corrected to extract valid scientific conclusions.

#### Power Spectrum Estimation and Window Function Corrections

A primary goal of cosmological simulations is to compute the matter power spectrum, $P(k)$, which quantifies the variance of density fluctuations as a function of scale. In a PM simulation, this is achieved by first using CIC to assign particle masses to a grid, yielding a discrete density field. This grid is then processed with a Fast Fourier Transform (FFT) to measure the power in each Fourier mode.

The CIC assignment process is equivalent to convolving the underlying continuous density field with a triangular kernel. According to the convolution theorem, this real-space smoothing corresponds to a multiplicative suppression in Fourier space. Consequently, the measured power spectrum, $P_{\text{meas}}(\mathbf{k})$, is systematically lower than the true power spectrum, $P_{\text{true}}(\mathbf{k})$. This suppression is described by the squared modulus of the CIC "window function," $W_{\text{CIC}}(\mathbf{k})$, which is the Fourier transform of the assignment kernel. For a three-dimensional Cartesian grid with spacing $\Delta$, the CIC window function is a separable product of the one-dimensional window functions:

$$
W_{\text{CIC}}(\mathbf{k}) = \prod_{i \in \{x,y,z\}} \left[ \mathrm{sinc}\left(\frac{k_i \Delta}{2}\right) \right]^2
$$

where $\mathrm{sinc}(u) \equiv \sin(u)/u$. The measured power spectrum is therefore related to the true spectrum by $P_{\text{meas}}(\mathbf{k}) \approx |W_{\text{CIC}}(\mathbf{k})|^2 P_{\text{true}}(\mathbf{k})$, neglecting other effects like aliasing. To obtain an unbiased estimate of the true power spectrum, one must perform a deconvolution by dividing the measured power by this window function squared. This correction is largest at high wavenumbers (small scales), where the CIC window function deviates most significantly from unity. Accurate power spectrum estimation is thus critically dependent on this correction procedure [@problem_id:3481241].

The CIC scheme belongs to a family of B-spline interpolation methods. The Nearest-Grid-Point (NGP) scheme corresponds to a zeroth-order B-spline (a top-hat kernel), while the Triangular-Shaped-Cloud (TSC) and Piecewise Cubic Spline (PCS) schemes correspond to second- and third-order B-splines, respectively. Higher-order schemes employ smoother kernels, which translate to window functions that are flatter near $k=0$ but fall off more rapidly towards the Nyquist frequency. This provides better accuracy for large-scale modes but more significant suppression of small-scale modes. When measuring delicate features in the power spectrum, such as the Baryon Acoustic Oscillations (BAO), the choice of assignment scheme affects the measured amplitude of these features. The CIC scheme offers a practical compromise, providing substantially better accuracy and reduced aliasing than NGP, without the larger computational stencil and increased cost of TSC or higher-order methods [@problem_id:3466958].

#### Discreteness Effects: Shot Noise

Representing a continuous density field with a finite number of discrete particles inherently introduces a source of noise known as shot noise. For a purely random (Poisson) distribution of particles with mean number density $\bar{n}$, the power spectrum of the particle distribution itself is constant, $P_{\text{shot}}(k) = 1/\bar{n}$. However, when this particle distribution is assigned to a grid using the CIC scheme, the resulting gridded density field exhibits a shot noise power spectrum that is modulated by the assignment window:

$$
P_{\text{shot, meas}}(\mathbf{k}) = \frac{1}{\bar{n}} |W_{\text{CIC}}(\mathbf{k})|^2
$$

For a general cosmological density field, the particles are not randomly distributed but trace the underlying structure. The total measured power spectrum is, to a good approximation, the sum of the window-convolved true power spectrum and the window-convolved shot noise.

$$
P_{\text{meas}}(\mathbf{k}) \approx |W_{\text{CIC}}(\mathbf{k})|^2 P_{\text{true}}(k) + \frac{1}{\bar{n}} |W_{\text{CIC}}(\mathbf{k})|^2
$$

This relationship reveals a crucial two-step correction procedure required to recover the true power spectrum. First, the estimated shot noise contribution must be subtracted from the measured power spectrum. Second, the result must be deconvolved by dividing by the squared window function. Failure to correctly model the window function's effect on the shot noise component would lead to a systematic bias in the recovered cosmological signal [@problem_id:3481170].

#### Real-Space Effects and Conservation Properties

The effects of CIC are not confined to Fourier space. The real-space convolution with a triangular kernel smooths the density field, altering its local statistical properties. This is particularly evident in the two-point correlation function, $\xi(r)$, which is the Fourier transform of the power spectrum. The value of the correlation function at zero lag, $\xi(0)$, represents the variance of the field, $\sigma^2$. The CIC smoothing reduces the variance of the field on the grid. This can be quantified by considering the autocorrelation of the CIC window. To leading order in the grid spacing $\Delta$, the measured variance is related to the true variance and the curvature of the correlation function at the origin:

$$
\xi_{\text{CIC}}(0) \approx \xi(0) + \frac{1}{2}\Delta^2 \xi''(0)
$$

Since for a typical cosmological correlation function $\xi''(0)$ is negative (reflecting a central cusp), this formula shows that CIC smoothing systematically reduces the measured variance. This is a direct manifestation of the kernel's smoothing effect in real space [@problem_id:3466965]. This implicit smoothing by CIC also compounds with any explicit filtering applied to the field. The total effective smoothing kernel is the convolution of the CIC kernel and the explicit filter, and its impact on the variance can be precisely calculated using Parseval's theorem [@problem_id:3466925].

Despite these modifications to the field's statistical properties, the CIC scheme, when used symmetrically for both mass deposition and force interpolation, excels at preserving fundamental physical laws. In a periodic PM simulation, this symmetric application guarantees exact conservation of total linear momentum to machine precision. This arises because the forces on any pair of particles are guaranteed to be equal and opposite, and self-forces are eliminated. However, total energy is not exactly conserved. Grid-based forces are inherently anisotropic—their magnitude depends on the orientation of the wavevector relative to the grid axes, especially near the Nyquist frequency. Smoother kernels like CIC and TSC suppress these high-frequency modes more effectively than NGP, thereby reducing the impact of force anisotropy and improving the overall statistical isotropy of the simulation [@problem_id:3509633]. The anisotropy and suppression of high-$k$ modes are fundamental properties of PM methods, and CIC offers a robust and well-understood way to manage these effects [@problem_id:3466903].

### Advanced Numerical Techniques and Extensions

The principles underlying CIC are general and can be extended beyond simple, uniform Cartesian grids. This flexibility allows its use in more sophisticated numerical frameworks designed to handle complex geometries or increase computational efficiency.

#### Practical Implementation and Extension to Other Quantities

The practical implementation of CIC in a simulation code requires careful handling of boundary conditions. For a periodic domain, a particle located near one edge of the simulation box must deposit a portion of its mass onto cells at the opposite edge. This is achieved algorithmically by calculating the indices of the neighboring cells and applying a modulo operator with respect to the number of cells along each dimension, ensuring a seamless and continuous deposition across the periodic boundaries [@problem_id:3516891].

Furthermore, the applicability of CIC is not limited to mass density. It can be used to grid any extensive physical quantity. In hydrodynamical or multi-fluid cosmological simulations (e.g., of baryons and dark matter), it is essential to compute fields such as momentum density $(\rho\mathbf{v})$ on the grid. A key principle for maintaining momentum conservation is to use the exact same assignment kernel for mass density and momentum density. The grid-based velocity is then defined as the ratio of the gridded momentum density to the gridded mass density, $\mathbf{v}_{\text{grid}} = (\rho \mathbf{v})_{\text{grid}} / \rho_{\text{grid}}$. In this momentum-conserving framework, the resulting velocity field on the grid is also effectively smoothed. Under linear assumptions, its power spectrum is suppressed by the same CIC window function, a bias that must be accounted for when analyzing the simulation's velocity statistics [@problem_id:3466956].

#### CIC in Adaptive Mesh Refinement (AMR)

To overcome the resolution limits of a single fixed grid, many modern simulations employ Adaptive Mesh Refinement (AMR). In AMR, regions of high density are recursively covered by finer sub-grids. CIC can be used for mass assignment on each level of this grid hierarchy. However, this requires a consistent framework for transferring data between levels.

-   **Restriction**: When transferring data from a fine grid to a coarse grid (e.g., to compute the gravitational potential on the coarse level), a mass-conserving restriction operator must be used. A simple and effective choice is to define the density in a coarse cell as the average of the densities in the constituent fine cells.

-   **Prolongation**: When providing boundary conditions for a fine grid from a coarse grid, a prolongation operator is needed. To maintain accuracy, this is typically a higher-order interpolation, such as a piecewise linear reconstruction on the coarse grid using slope-limited gradients to prevent spurious oscillations.

The interplay between CIC deposition and these inter-grid transfer operators is complex. Analyzing the propagation of a simple density wave through an AMR hierarchy reveals how different paths (e.g., depositing directly to a coarse grid vs. depositing to a fine grid and restricting) can lead to different final amplitudes, highlighting the potential for numerical artifacts to arise at refinement boundaries [@problem_id:3466957].

#### CIC on Curvilinear Grids

While most cosmological simulations use Cartesian grids, certain astrophysical problems, such as accretion disks or the evolution of a single galaxy, possess symmetries that are better captured by curvilinear coordinate systems (e.g., spherical or cylindrical). The CIC scheme can be generalized to such grids through a powerful change-of-variables technique. The core principle is to find a coordinate transformation, for instance from spherical coordinates $(r, \theta, \phi)$ to a new set of coordinates $(q_r, q_\theta, q_\phi)$, such that the volume element becomes Cartesian: $dV = r^2 \sin\theta \,dr\,d\theta\,d\phi = dq_r\,dq_\theta\,dq_\phi$.

Once this transformation is found, the grid is constructed to be uniform in the $(q_r, q_\theta, q_\phi)$ space. Mass assignment is then performed as standard, trilinear CIC interpolation within this transformed, logically Cartesian space. This elegant procedure automatically ensures that the mass assignment is properly volume-weighted in the original physical space, thereby conserving mass and other key properties of the scheme. This extension demonstrates that CIC is not merely a recipe for Cartesian grids but a manifestation of a deeper principle of interpolation within a space of uniform measure [@problem_id:3466932].

### Connections to Observational Data Analysis

The impact of the CIC scheme extends beyond simulations to the analysis of observational data, where similar gridding techniques are used. Understanding the artifacts introduced by CIC is crucial for making robust comparisons between theory, simulations, and observations.

#### Disentangling Physical and Numerical Effects

A persistent challenge in computational science is distinguishing physical effects from numerical artifacts. The CIC window function provides a clear example. Consider a universe with Warm Dark Matter (WDM), where the free-streaming of dark matter particles physically suppresses the formation of small-scale structures. This physical suppression is often modeled as a Gaussian filter on the power spectrum, $T_{\text{WDM}}(k) = \exp(-k^2 / (2 k_{\text{fs}}^2))$. When simulating a WDM model with a PM code, the measured power spectrum will be suppressed by both the physical WDM cutoff and the numerical CIC window. The total suppression factor is the product of the two individual suppressions: $S(k) = |T_{\text{WDM}}(k)|^2 |W_{\text{CIC}}(k)|^2$. To correctly infer physical parameters, such as the free-streaming scale $k_{\text{fs}}$, from a simulation, one must accurately model and deconvolve the known numerical suppression from the CIC scheme [@problem_id:3466914].

#### Application to 2D Observational Maps

The principles of CIC are directly applicable to the analysis of 2D observational data. A prominent example is in weak gravitational lensing, where the subtle distortions of background galaxy shapes are used to map the projected mass distribution of the universe. To compute the angular power spectrum ($C_\ell$) of the lensing convergence field, one typically starts by gridding a catalog of galaxy ellipticities onto a 2D pixelated map. Using a 2D version of CIC for this gridding process introduces a 2D window function, $W_{\text{2D}}(\boldsymbol{\ell})$, that suppresses power at high angular frequencies (large $\ell$). This suppression is anisotropic and depends on the pixel size. It must be carefully modeled when comparing the measured angular power spectrum with theoretical predictions, demonstrating the scheme's relevance in observational cosmology [@problem_id:3466931].

#### From Grid Density to Astrophysical Objects

One of the primary products of cosmological simulations is a catalog of dark matter halos, whose properties, such as their mass function, are compared with observations. A common technique for identifying halos is to apply a density threshold to the gridded density field and identify connected groups of suprathreshold cells. The CIC smoothing inherent to the mass assignment directly impacts this procedure. The smoothing lowers the central densities of halos, which can cause some low-mass halos to fall below the detection threshold or lead to an underestimation of halo masses. Conversely, the broadening of halo profiles can cause two physically distinct but nearby halos to be merged into a single object by the halo finder. Correcting for these biases, for instance by calibrating the mass loss for isolated halos and implementing a de-blending algorithm for merged peaks, is a critical step in extracting an accurate halo mass function from a simulation. This provides a direct link between the low-level choice of a mass assignment scheme and a high-level scientific measurement [@problem_id:3516924].

Finally, the analysis of CIC artifacts extends to the frontiers of cosmological research. Probes of the early universe, such as searches for primordial non-Gaussianity, rely on measuring higher-order statistics like the bispectrum and trispectrum. Just as with the power spectrum, the measurement of these higher-order correlators is biased by the CIC window. The measured $n$-point function is suppressed by a product of $n$ window functions. For the trispectrum, this means $T_{\text{meas}} \approx \left(\prod_{i=1}^4 W_{\text{CIC}}(\mathbf{k}_i)\right) T_{\text{true}}$. This multiplicative bias is generally non-negligible and must be corrected to obtain unbiased constraints on fundamental parameters like the non-Gaussianity amplitude $f_{\text{NL}}$ [@problem_id:3466946].

In summary, the Cloud-in-Cell scheme is far more than a simple interpolation algorithm. It is a foundational component of modern scientific computing in astrophysics, whose predictable and well-characterized properties have profound implications for the accuracy and interpretation of both simulated and observed data. A thorough grasp of its effects, from Fourier-space windowing to real-space smoothing, is indispensable for any researcher in the field.