## Introduction
The grand challenge of [numerical cosmology](@entry_id:752779) lies in modeling the evolution of an effectively infinite, homogeneous, and isotropic universe using finite computational resources. Simulating a representative patch of the cosmos requires a method to handle the edges of the computational domain without introducing nonphysical artifacts that would contaminate the results. The standard and most elegant solution to this problem is the implementation of **[periodic boundary conditions](@entry_id:147809) (PBCs)**, a foundational concept that underpins virtually all modern [cosmological simulations](@entry_id:747925).

This article provides a comprehensive, graduate-level exploration of periodic boundary conditions. It addresses the critical need for a robust computational framework that allows for the study of [gravitational instability](@entry_id:160721) and [cosmic structure formation](@entry_id:137761) in a statistically meaningful way. By understanding the principles, applications, and inherent limitations of PBCs, you will gain a deeper insight into the engine that drives [cosmological simulations](@entry_id:747925) and the interpretation of their results.

Our journey is structured into three parts. First, in **"Principles and Mechanisms,"** we will delve into the theoretical framework, from the 3-torus topology that eliminates boundaries to the discretization of Fourier space that enables powerful spectral gravity solvers and Particle-Mesh techniques. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these principles are put into practice to generate initial conditions, evolve the cosmic fluid, create mock observational catalogs, and how these concepts connect to other fields like [condensed matter](@entry_id:747660) physics and [high-performance computing](@entry_id:169980). Finally, the **"Hands-On Practices"** section offers practical coding exercises designed to solidify your understanding by implementing key algorithms like a spectral Poisson solver and the Zel'dovich approximation.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental challenge of simulating [cosmic structure formation](@entry_id:137761): modeling a statistically representative portion of an infinite, homogeneous, and isotropic universe using a finite computational volume. The solution to this challenge lies in the adoption of **[periodic boundary conditions](@entry_id:147809) (PBCs)**, a choice that has profound implications for the physical interpretation, mathematical formulation, and numerical implementation of [cosmological simulations](@entry_id:747925). This chapter delves into the principles and mechanisms underpinning the use of periodic volumes, from the resulting discretization of Fourier space to the practical algorithms used to evolve the self-gravitating fluid of dark matter.

### The Periodic Universe: A Three-Torus Topology

The core idea of [periodic boundary conditions](@entry_id:147809) is to eliminate surface artifacts. In a simulation box of side length $L$, any particle or field exiting one face of the cube instantaneously re-enters through the opposite face with the same velocity vector. For a scalar field, such as the [density contrast](@entry_id:157948) $\delta(\mathbf{x})$, this is expressed mathematically as:
$$
\delta(\mathbf{x} + L\hat{\mathbf{e}}_i) = \delta(\mathbf{x})
$$
for each Cartesian [unit vector](@entry_id:150575) $\hat{\mathbf{e}}_i$, where $i \in \{x, y, z\}$.

Geometrically, this is equivalent to "gluing" opposite faces of the cubic domain together. The resulting [topological space](@entry_id:149165) is a **three-torus ($3$-torus)**. This choice ingeniously creates a computational volume that has no edges or boundaries, providing the most faithful discrete approximation to a small, translationally invariant patch of an infinite universe [@problem_id:3481567]. A particle moving within this volume never encounters a wall; its trajectory simply wraps around the toroidal space.

While this is a powerful and elegant solution, it immediately introduces a fundamental scale into the simulation: the box size $L$. The [periodicity](@entry_id:152486) implies that no physical correlations or structures can be properly represented on scales larger than the box itself. This limitation is a recurring theme we will explore throughout this chapter.

### Discretization of Fourier Space

The toroidal topology of the periodic domain makes the Fourier series the natural mathematical language for describing fields within it. Any periodic function, such as the [density contrast](@entry_id:157948) $\delta(\mathbf{x})$, can be represented as a discrete sum of plane waves:
$$
\delta(\mathbf{x}) = \sum_{\mathbf{k}} \tilde{\delta}(\mathbf{k}) e^{i\mathbf{k} \cdot \mathbf{x}}
$$
where $\tilde{\delta}(\mathbf{k})$ are the complex Fourier coefficients. For these [plane wave basis](@entry_id:265736) functions to respect the [periodicity](@entry_id:152486) of the box, they too must satisfy $e^{i\mathbf{k} \cdot (\mathbf{x} + L\hat{\mathbf{e}}_i)} = e^{i\mathbf{k} \cdot \mathbf{x}}$. This requires that $e^{i k_i L} = 1$ for each component $i$, which is only true if $k_i L$ is an integer multiple of $2\pi$.

This leads to a crucial consequence: the allowed wavevectors $\mathbf{k}$ are not continuous. They must belong to a discrete lattice in Fourier space (or $\mathbf{k}$-space):
$$
\mathbf{k} = \frac{2\pi}{L}(n_x, n_y, n_z) \quad \text{where} \quad (n_x, n_y, n_z) \in \mathbb{Z}^3
$$
The components of the wavevectors are integer multiples of a fundamental spacing, $\Delta k = 2\pi/L$ [@problem_id:3481613] [@problem_id:3481621]. The smallest non-zero wavenumber magnitude that can be represented is called the **fundamental wavenumber**, $k_f = 2\pi/L$, corresponding to a wavelength equal to the box size, $\lambda_{\text{max}} = L$. This sets a hard lower limit on the frequencies (and an upper limit on the wavelengths) that can be directly modeled in the simulation.

When we further discretize the [real-space](@entry_id:754128) volume onto a uniform Cartesian grid of $N$ points per side for numerical computation, a second limit emerges. The grid spacing, $\Delta x = L/N$, defines the smallest scale that can be resolved. This introduces the **Nyquist [wavenumber](@entry_id:172452)**, $k_{\text{Ny}} = \pi/\Delta x = N\pi/L$. Any fluctuations with wavenumbers higher than the Nyquist frequency cannot be represented on the grid and are subject to aliasing. Therefore, the range of scales accessible to a simulation is bounded by these two fundamental limits:
$$
k_f = \frac{2\pi}{L} \le |\mathbf{k}| \le k_{\text{Ny}} = \frac{N\pi}{L}
$$

The density of discrete modes in $\mathbf{k}$-space is uniform. The elementary volume occupied by a single mode is $(\Delta k)^3 = (2\pi/L)^3 = 8\pi^3/L^3$. The density of modes is the reciprocal, $\rho_k = L^3 / (8\pi^3)$. In the [continuum limit](@entry_id:162780), where the grid of modes is very fine, the number of modes within a small volume of $\mathbf{k}$-space, $d^3k$, is simply $\rho_k d^3k$. For a thin spherical shell of radius $k$ and thickness $\Delta k$, the volume is approximately $4\pi k^2 \Delta k$. The number of modes within this shell is therefore:
$$
N_{\text{modes}} = \rho_k V_{\text{shell}} = \left(\frac{L^3}{8\pi^3}\right) (4\pi k^2 \Delta k) = \frac{L^3 k^2 \Delta k}{2\pi^2}
$$
For instance, in a simulation with a box size of $L = 1000\,h^{-1}\,\mathrm{Mpc}$, the number of Fourier modes in a shell of width $\Delta k = 0.04\,h\,\mathrm{Mpc}^{-1}$ centered at $k = 0.20\,h\,\mathrm{Mpc}^{-1}$ is approximately $8.11 \times 10^4$ [@problem_id:3481613]. This mode-counting formula is essential for correctly normalizing statistical estimators like the power spectrum.

A further refinement to mode counting comes from the fact that the [density contrast](@entry_id:157948) $\delta(\mathbf{x})$ is a real-valued field. This imposes a **Hermitian symmetry** on its Fourier transform: $\tilde{\delta}(-\mathbf{k}) = \tilde{\delta}(\mathbf{k})^*$, where the asterisk denotes [complex conjugation](@entry_id:174690). This means the Fourier coefficients for $\mathbf{k}$ and $-\mathbf{k}$ are not independent. Consequently, the number of independent complex degrees of freedom in Fourier space is roughly half the total number of [lattice points](@entry_id:161785) [@problem_id:3481551]. This is a critical consideration when assessing the statistical power and [information content](@entry_id:272315) of a simulation.

### Solving for Gravity: The Spectral Method

The primary task in an N-body simulation is to compute the gravitational forces acting on each particle. In an expanding universe, the peculiar [gravitational potential](@entry_id:160378) $\phi$ is related to the [density contrast](@entry_id:157948) $\delta$ via the comoving Poisson equation:
$$
\nabla^2\phi(\mathbf{x}, t) = 4\pi G\,a^{2}(t)\,\bar{\rho}(t)\,\delta(\mathbf{x}, t)
$$
where $G$ is Newton’s constant, $a(t)$ is the scale factor, and $\bar{\rho}(t)$ is the mean comoving matter density.

The power of the Fourier representation becomes apparent here. The Laplacian operator $\nabla^2$ in real space transforms into a simple multiplication by $-|\mathbf{k}|^2 = -k^2$ in Fourier space. Applying a Fourier transform to the entire equation yields:
$$
-k^2 \tilde{\phi}(\mathbf{k}) = 4\pi G a^2 \bar{\rho} \tilde{\delta}(\mathbf{k})
$$
This transforms a [partial differential equation](@entry_id:141332) into a simple algebraic equation for each mode $\mathbf{k}$. The solution for the potential's Fourier coefficients is immediate for all $k \neq 0$:
$$
\tilde{\phi}(\mathbf{k}) = - \frac{4\pi G a^2 \bar{\rho}}{k^2} \tilde{\delta}(\mathbf{k})
$$
The term $-1/k^2$ is the Fourier-space representation of the gravitational **Green's function** for a periodic domain. This [spectral method](@entry_id:140101) provides a highly efficient and accurate way to solve for the [gravitational potential](@entry_id:160378).

A special case is the **$\mathbf{k=0}$ mode**, which corresponds to the spatial average (or DC component) of the fields. By construction, a [cosmological simulation](@entry_id:747924) is set up such that the average density within the box, $\langle\rho\rangle$, is equal to the cosmic mean density $\bar{\rho}$. This implies that the mean of the [density contrast](@entry_id:157948) is zero: $\langle\delta\rangle = 0$. The $\mathbf{k=0}$ Fourier coefficient, $\tilde{\delta}(\mathbf{0})$, is precisely this mean value, so $\tilde{\delta}(\mathbf{0}) = 0$ [@problem_id:3481621]. The Poisson equation for $k=0$ becomes $0 \cdot \tilde{\phi}(\mathbf{0}) = 0$, leaving $\tilde{\phi}(\mathbf{0})$ undetermined. Since the absolute value of the potential is physically irrelevant (only its gradient, the force, matters), we are free to set this mean potential to zero by a choice of gauge: $\tilde{\phi}(\mathbf{0})=0$. This procedure is not just a mathematical convenience; it ensures that the center of mass of the entire simulation box does not experience any spurious net acceleration, a fundamental requirement of [momentum conservation](@entry_id:149964) in a closed system [@problem_id:3481621].

To illustrate the method, consider a simple density field composed of fundamental modes, $\delta(\mathbf{x}) = \delta_{0}[\cos(2\pi x/L) + \cos(2\pi y/L) + \cos(2\pi z/L)]$ [@problem_id:3481558]. By inspection, the only non-zero Fourier coefficients $\tilde{\delta}(\mathbf{k})$ are for the six wavevectors $\mathbf{k} = (\pm 2\pi/L, 0, 0)$ and its permutations. For these modes, $k^2 = (2\pi/L)^2$. Applying the spectral solution, we can find the corresponding $\tilde{\phi}(\mathbf{k})$ and transform back to real space to find the potential $\phi(\mathbf{x})$.

### From Particles to Mesh and Back

The spectral method for gravity operates on a grid, but the matter in the universe is composed of discrete particles (or fluid elements represented by particles). The bridge between these two representations is the **Particle-Mesh (PM)** technique. This involves two key steps: [mass assignment](@entry_id:751704) and force interpolation.

**Mass Assignment:** To create a gridded density field $\delta_{i,j,k}$ from a distribution of particles, we use a **[mass assignment](@entry_id:751704) scheme**. This involves distributing each particle's mass to one or more nearby grid cells according to a shape function or kernel. Common schemes include [@problem_id:3481548]:
*   **Nearest Grid Point (NGP):** The simplest scheme. The entire mass of a particle is assigned to the single grid cell that its center is closest to. This results in a blocky, discontinuous density field.
*   **Cloud-In-Cell (CIC):** A particle's mass is distributed bilinearly (in 2D) or trilinearly (in 3D) to the $2^3=8$ cells that form the cube containing the particle. This produces a smoother density field than NGP.
*   **Triangular Shaped Cloud (TSC):** A higher-order scheme that distributes mass quadratically to the surrounding $3^3=27$ cells, resulting in an even smoother density field and its first derivative.

These schemes must be implemented carefully to preserve fundamental physical properties. One such property is **[mass conservation](@entry_id:204015)**: the total mass assigned to the grid must exactly equal the sum of the individual particle masses. This is guaranteed if the assignment kernel weights for any given particle sum to unity. Another is **shift-equivariance**: if all particles are shifted by an integer number of grid cells, the resulting mass grid should be a simple cyclic permutation of the original grid [@problem_id:3481548].

The consistency of these [numerical schemes](@entry_id:752822) is paramount. For example, the discrete formulation of Gauss's Law on a periodic grid requires the sum of the divergence of the gravitational field over all cells to be exactly zero. If a [mass assignment](@entry_id:751704) scheme has a normalization error and deposits a total mass $(1+\varepsilon)M$ instead of the true total mass $M$, it introduces a spurious monopole into the system. The discrete Poisson equation then predicts a non-zero net flux, proportional to $-4\pi G \varepsilon M$, which is inconsistent with the periodic topology [@problem_id:3481607].

**Force Interpolation and Time Integration:** Once the gravitational potential $\phi$ (or [force field](@entry_id:147325) $\mathbf{g}=-\nabla\phi$) is calculated on the grid, it must be interpolated back to the particle positions to update their velocities. To maintain [momentum conservation](@entry_id:149964), this interpolation is performed using the same shape function as the [mass assignment](@entry_id:751704) step. This duality between assignment and interpolation is known as **adjointness** [@problem_id:3481548].

Particle positions and velocities are evolved using a numerical integrator. To handle the Hamiltonian nature of gravity and ensure good long-term energy conservation, a **[symplectic integrator](@entry_id:143009)** is used. A standard choice is the **Kick-Drift-Kick (KDK) Leapfrog** scheme [@problem_id:3481581]. For a time step $\Delta t$, the update proceeds as follows:
1.  **Kick:** Update particle velocities by a half-step using the current forces: $\mathbf{v}(t+\Delta t/2) = \mathbf{v}(t) + \mathbf{a}(\mathbf{x}(t))\frac{\Delta t}{2}$.
2.  **Drift:** Update particle positions by a full step using the half-step velocities: $\mathbf{x}(t+\Delta t) = \mathbf{x}(t) + \mathbf{v}(t+\Delta t/2)\Delta t$. After this step, apply periodic boundary conditions by taking the modulo of each position coordinate with the box length $L$.
3.  **Kick:** Update velocities by the final half-step using the forces at the new positions: $\mathbf{v}(t+\Delta t) = \mathbf{v}(t+\Delta t/2) + \mathbf{a}(\mathbf{x}(t+\Delta t))\frac{\Delta t}{2}$.

This time-reversible, second-order scheme is robust and widely used in [cosmological simulations](@entry_id:747925).

### Physical and Numerical Limitations

While powerful, the PBC framework is an approximation with inherent limitations and numerical artifacts.

**Spectral Leakage:** The discrete Fourier transform (DFT) implicitly assumes that the signal being analyzed is perfectly periodic within the box. If the true underlying field contains a wave that is not commensurate with the box size (i.e., its wavelength is not $L/n$ for some integer $n$), its power will not be confined to a single DFT bin. Instead, it "leaks" into all other frequency bins. The fraction of power from a single non-commensurate plane wave that is captured by the nearest discrete Fourier mode $m$ can be shown to be $R = \sin^2(\pi \varepsilon) / (N^2 \sin^2(\pi\varepsilon/N))$, where $\varepsilon$ measures the mismatch between the true frequency and the nearest discrete frequency, and $N$ is the number of grid points [@problem_id:3481580]. This is a fundamental property of the DFT known as the Dirichlet kernel and is a source of error when analyzing fields with continuous spectra.

**Phase Mixing (Landau Damping):** In a system of collisionless particles with a velocity dispersion, macroscopic [density perturbations](@entry_id:159546) can decay even in the absence of gravitational interactions. This process, known as **[phase mixing](@entry_id:199798)** or Landau damping, occurs because particles stream at different speeds. An initially coherent overdensity gets smeared out as faster particles stream away from the peak and slower particles lag behind. For an initial sinusoidal density perturbation of wavenumber $k$ in a gas with velocity dispersion $\sigma$, the amplitude of the perturbation decays over time as $\exp(-\frac{1}{2}k^2\sigma^2t^2)$ in the [free-streaming limit](@entry_id:749576) [@problem_id:3481575]. This is a real physical effect that N-body simulations naturally capture, and it is a key mechanism for damping the [growth of structure](@entry_id:158527) on very small scales.

**Missing Modes and Super-Sample Covariance:** The most significant physical limitation of a finite periodic volume is the absence of modes with wavelengths $\lambda > L$. These "super-sample" modes are not just unresolved; they are effectively set to zero. In the real universe, these long-wavelength fluctuations provide the large-scale tidal environment in which the smaller, "in-sample" structures evolve. The presence of a large over- or under-density with a scale larger than the box can coherently enhance or suppress the growth of all structures within it. This coupling between super-sample and in-sample modes induces correlations in structure formation that are not captured in a single simulation, an effect known as **super-sample covariance (SSC)**. This is a fundamental [systematic uncertainty](@entry_id:263952) in all finite-volume [cosmological simulations](@entry_id:747925) that is not removed by [periodic boundary conditions](@entry_id:147809) [@problem_id:3481567].

In conclusion, periodic boundary conditions provide an indispensable framework for modern [cosmological simulations](@entry_id:747925). They allow us to model a representative piece of an infinite universe by creating a boundary-free toroidal domain amenable to powerful [spectral methods](@entry_id:141737) for gravity. However, this choice imposes a discrete Fourier space, introduces fundamental limits on the accessible scales, and gives rise to specific numerical artifacts and physical limitations, such as super-sample covariance, which must be carefully considered when interpreting simulation results. Understanding these principles and mechanisms is the first step toward mastering the art and science of [numerical cosmology](@entry_id:752779).