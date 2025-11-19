## Introduction
Ray tracing through cosmological N-body simulations is a cornerstone technique in [modern cosmology](@entry_id:752086), providing the essential bridge between theoretical models of [structure formation](@entry_id:158241) and the wealth of data from observational surveys. By simulating the deflection of light by the cosmic web, we can create high-fidelity virtual universes to test our understanding of gravity, dark matter, and cosmic evolution. This article addresses the challenge of accurately modeling these lensing effects, which are critical for interpreting results from large-scale surveys. It provides a comprehensive guide to this powerful method, starting with the foundational theory and numerical implementation. In the "Principles and Mechanisms" chapter, we will break down how the three-dimensional matter distribution from a simulation is translated into observable lensing signals using the multiple-lens-plane algorithm. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase how these simulations are used to probe [dark matter halos](@entry_id:147523), constrain [cosmological parameters](@entry_id:161338), and connect with other observational probes. Finally, the "Hands-On Practices" section offers concrete exercises to reinforce the practical aspects of implementing and interpreting these simulations.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms that underpin the simulation of [gravitational lensing](@entry_id:159000) by tracing light rays through cosmological $N$-body simulations. We will begin by establishing the theoretical connection between the three-dimensional matter distribution and the observable two-dimensional lensing fields. We then translate this theory into a discrete, computationally tractable algorithm—the multiple-lens-plane method—and explore its nuances, including the critical distinction between the Born approximation and full non-linear [ray tracing](@entry_id:172511). Subsequently, we will detail the practical steps for converting raw simulation data into the necessary inputs for this algorithm. Finally, we will conduct a rigorous examination of the primary numerical and physical [systematics](@entry_id:147126) that can affect the accuracy and interpretation of simulation results, from the scale of individual particles to the scale of the entire simulation volume.

### From 3D Potential to 2D Lensing Fields

The deflection of light in a weak gravitational field is governed by the gradient of the Newtonian [gravitational potential](@entry_id:160378), $\Phi$, integrated along the path of a light ray. In a cosmological context, we work in a comoving coordinate system where the background expansion of the universe is factored out. For a light ray traveling along the line of sight, we can define a two-dimensional **[lensing potential](@entry_id:161831)**, $\psi(\boldsymbol{\theta})$, on the [celestial sphere](@entry_id:158268), where $\boldsymbol{\theta}$ is the [angular position](@entry_id:174053) vector. This potential is a weighted projection of the 3D potential $\Phi$ along the comoving line-of-sight distance, $\chi$. Its significance lies in the fact that the deflection angle, $\boldsymbol{\alpha}(\boldsymbol{\theta})$, which describes the displacement of a source image on the sky, is simply the gradient of this potential:

$$
\boldsymbol{\alpha}(\boldsymbol{\theta}) = \nabla_{\boldsymbol{\theta}} \psi(\boldsymbol{\theta})
$$

The [lens equation](@entry_id:161034), $\boldsymbol{\beta} = \boldsymbol{\theta} - \boldsymbol{\alpha}(\boldsymbol{\theta})$, relates the true, unlensed source position $\boldsymbol{\beta}$ to the observed image position $\boldsymbol{\theta}$. The local distortion of an image is characterized by the Jacobian matrix of this mapping, $\mathbf{A}_{ij} = \partial \beta_i / \partial \theta_j = \delta_{ij} - \partial_i \partial_j \psi(\boldsymbol{\theta})$. This matrix can be decomposed to describe how an infinitesimal circular source is mapped to an ellipse. This decomposition defines the three fundamental [weak lensing](@entry_id:158468) observables [@problem_id:3483286]:

1.  The **convergence**, $\kappa$, which describes the isotropic change in image size.
2.  The two components of **shear**, $\gamma_1$ and $\gamma_2$, which describe the anisotropic stretching that deforms the image shape. The shear is often represented as a complex number, $\gamma = \gamma_1 + i\gamma_2$.

By comparing the general form of the Jacobian matrix in terms of these observables with its definition in terms of the potential, we arrive at the core relationships on the lens plane:

$$
\kappa(\boldsymbol{\theta}) = \frac{1}{2} \nabla_{\boldsymbol{\theta}}^2 \psi(\boldsymbol{\theta}) = \frac{1}{2} \left( \frac{\partial^2}{\partial \theta_1^2} + \frac{\partial^2}{\partial \theta_2^2} \right) \psi(\boldsymbol{\theta})
$$

$$
\gamma_1(\boldsymbol{\theta}) = \frac{1}{2} \left( \frac{\partial^2}{\partial \theta_1^2} - \frac{\partial^2}{\partial \theta_2^2} \right) \psi(\boldsymbol{\theta})
$$

$$
\gamma_2(\boldsymbol{\theta}) = \frac{\partial^2}{\partial \theta_1 \partial \theta_2} \psi(\boldsymbol{\theta})
$$

The first of these equations, when inverted, reveals a profound connection between the projected mass and the [lensing potential](@entry_id:161831). The convergence $\kappa$ is defined as the surface mass density of the lens, $\Sigma$, normalized by a **critical [surface density](@entry_id:161889)**, $\Sigma_{\text{crit}}$, a geometric factor that depends on the distances to the lens and source. The relation $\nabla_{\boldsymbol{\theta}}^2 \psi = 2\kappa$ is therefore the two-dimensional **Poisson equation** for lensing [@problem_id:3483342]. It states that the [lensing potential](@entry_id:161831) at any point is sourced by the entire mass distribution on the plane, analogous to how the [electrostatic potential](@entry_id:140313) is sourced by charges. The validity of this simple, powerful relation rests on several key assumptions: the [weak-field limit](@entry_id:199592) of General Relativity, the thin-lens approximation (projecting mass onto a plane), and the flat-sky approximation (treating a small patch of the [celestial sphere](@entry_id:158268) as a Euclidean plane). Crucially, this relation is local to a single lens plane and holds independently of how one calculates the full light path through multiple planes.

### The Lensing Kernel and Cosmological Weighting

While the 2D Poisson equation describes lensing by a single plane, the full effect is an integral over the entire line of sight to a source. The convergence $\kappa$ for a source at [comoving distance](@entry_id:158059) $\chi_s$ is a weighted projection of the three-dimensional matter [density contrast](@entry_id:157948), $\delta(\boldsymbol{x}, \chi) = (\rho(\boldsymbol{x}, \chi) - \bar{\rho}(\chi))/\bar{\rho}(\chi)$:

$$
\kappa(\boldsymbol{\theta}) = \int_0^{\chi_s} W(\chi) \, \delta(\chi \boldsymbol{\theta}, \chi) \, d\chi
$$

The function $W(\chi)$ is the **lensing kernel**, which quantifies the efficiency of matter at a given distance $\chi$ in lensing a source at $\chi_s$. To understand this kernel, we must first define the relevant [cosmological distances](@entry_id:160000) in our background Friedmann-Lemaître-Robertson-Walker (FLRW) model. For a spatially [flat universe](@entry_id:183782), the **[comoving distance](@entry_id:158059)** to an object at redshift $z$ is given by integrating along a light ray's path:

$$
\chi(z) = c \int_0^z \frac{dz'}{H(z')}
$$

where $c$ is the speed of light and $H(z)$ is the Hubble parameter at [redshift](@entry_id:159945) $z'$. The physical size of an object is related to its [angular size](@entry_id:195896) on the sky via the **[angular diameter distance](@entry_id:157817)**, $D_A(z)$, which for a [flat universe](@entry_id:183782) is simply related to the [comoving distance](@entry_id:158059) by $D_A(z) = \chi(z) / (1+z)$.

With these definitions, the lensing kernel for convergence is found to be [@problem_id:3483348]:

$$
W(\chi) = \frac{3 H_0^2 \Omega_{m,0}}{2c^2} \frac{1}{a(\chi)} g(\chi)
$$

Here, $H_0$ is the Hubble constant today, $\Omega_{m,0}$ is the present-day matter [density parameter](@entry_id:265044), and $a(\chi)$ is the cosmological scale factor at distance $\chi$. The kernel consists of two parts: a physical component, $\frac{3 H_0^2 \Omega_{m,0}}{2c^2 a(\chi)}$, which arises from the comoving Poisson equation relating the potential to the [density contrast](@entry_id:157948), and a purely geometric component, $g(\chi)$. This **lensing efficiency factor** is given by:

$$
g(\chi) = \frac{\chi (\chi_s - \chi)}{\chi_s}
$$

This factor can be understood as the ratio of comoving angular diameter distances $\frac{D_{ls} D_l}{D_s}$, where in a [flat universe](@entry_id:183782) these are simply the comoving distances to the lens ($\chi$), from the lens to the source ($\chi_s - \chi$), and to the source ($\chi_s$). The function $g(\chi)$ is zero at the observer ($\chi=0$) and the source ($\chi=\chi_s$), and peaks roughly halfway between, confirming the intuition that lenses are most effective when located midway between the observer and the source.

### The Multiple-Lens-Plane Algorithm

To perform lensing calculations numerically, the continuous [line-of-sight integral](@entry_id:751289) is discretized into a sum over a series of thin lens planes. This is the essence of the **multiple-lens-plane algorithm**. The way in which the contributions of these planes are combined defines two distinct approaches.

#### The Born Approximation

The simplest approach is the **Born approximation** [@problem_id:3483329]. This is a first-order perturbative method that assumes the total deflection of a light ray is small. Consequently, the lensing effect of all matter is calculated along the initial, unperturbed straight-line path from the observer to the source. In the multi-plane context, this means the deflection and shear from each plane are computed at the same initial [angular position](@entry_id:174053), and the total effect is found by simply summing these contributions, weighted by the appropriate geometric factors. Mathematically, for a source at plane $s$, the total Jacobian is approximated as:

$$
\mathbf{A}_s \approx \mathbf{I} - \sum_{i=1}^{s-1} \frac{\chi_{is}}{\chi_s} \mathbf{U}_i(\boldsymbol{\theta}_1)
$$

where $\mathbf{I}$ is the identity matrix, $\chi_{is} = \chi_s - \chi_i$ is the [comoving distance](@entry_id:158059) from lens plane $i$ to the source plane, $\mathbf{U}_i$ is the tidal matrix (Hessian of $\psi_i$), and every term is evaluated at the initial ray angle $\boldsymbol{\theta}_1$.

#### Full Ray Tracing with Lens-Lens Coupling

A more accurate, non-linear approach is to perform **full [ray tracing](@entry_id:172511)**, which accounts for the fact that a light ray's path is progressively bent as it traverses the universe. This introduces **lens-lens coupling**: the deflection caused by an early lens plane alters the position at which the ray strikes a later plane, thereby changing the lensing effect experienced there [@problem_id:3483300].

This is implemented with a [recursive algorithm](@entry_id:633952). Let a ray start at angle $\boldsymbol{\theta}_1$ and have a position $\boldsymbol{\theta}_i$ and Jacobian $\mathbf{A}_i$ upon reaching plane $i$. To propagate it to the next plane, $j$, one must account for all deflections from preceding planes $k  j$. The full [recursion relations](@entry_id:754160) for the angle and Jacobian at plane $j$ are:

$$
\boldsymbol{\theta}_j = \boldsymbol{\theta}_1 - \sum_{i=1}^{j-1} \frac{\chi_{ij}}{\chi_j} \boldsymbol{\alpha}_i(\boldsymbol{\theta}_i)
$$

$$
\mathbf{A}_j = \mathbf{I} - \sum_{i=1}^{j-1} \frac{\chi_{ij}}{\chi_j} \mathbf{U}_i(\boldsymbol{\theta}_i) \mathbf{A}_i
$$

The key differences from the Born approximation are twofold. First, the deflection $\boldsymbol{\alpha}_i$ and tidal field $\mathbf{U}_i$ are evaluated at the ray's actual, deflected position $\boldsymbol{\theta}_i$ at that plane. Second, the Jacobian [recursion](@entry_id:264696) involves the product $\mathbf{U}_i \mathbf{A}_i$, meaning the tidal field of plane $i$ acts upon a ray bundle that has already been stretched and rotated by all previous planes. This non-commutative matrix product is the source of higher-order lensing effects that are absent in the Born approximation, such as the generation of image rotation (an antisymmetric component in the Jacobian) and corresponding **B-mode** patterns in the shear field, even from purely scalar [density perturbations](@entry_id:159546) [@problem_id:3483329].

### From Simulation Data to Lens Planes

The practical implementation of the multi-plane algorithm requires constructing the lens planes from the output of an $N$-body simulation. This involves projecting a three-dimensional distribution of particles onto a two-dimensional grid [@problem_id:3483292].

The first step is to convert a particle's 3D comoving position $(x, y, z)$ within the simulation box to a 2D [angular position](@entry_id:174053) $(\theta_x, \theta_y)$ on the sky. For a lens plane at [comoving distance](@entry_id:158059) $\chi_l$, and assuming the [small-angle approximation](@entry_id:145423), this is a simple geometric projection:

$$
\theta_x = \frac{x - x_c}{\chi_l}, \quad \theta_y = \frac{y - y_c}{\chi_l}
$$

where $(x_c, y_c)$ is the comoving coordinate of the line-of-sight axis.

Next, the mass of each particle within a given slab of comoving thickness $\Delta\chi$ is projected onto a 2D pixel grid. To avoid artificial discreteness effects, this is not done by simply assigning each particle to the nearest pixel (Nearest Grid Point scheme). A superior method is the **Cloud-in-Cell (CIC)** [mass assignment](@entry_id:751704) scheme. In CIC, a particle is treated as a uniform square cloud the size of a grid cell. Its mass is distributed among the four nearest grid points, with the weight for each point being proportional to the overlapping area. This is equivalent to [bilinear interpolation](@entry_id:170280).

After accumulating the mass from all relevant particles into a 2D mass map, $M_{ij}$, the final step is to obtain the physical **surface mass density**, $\Sigma_{ij}$. This is done by dividing the mass in each pixel by the pixel's physical area, $A_{\text{pix}}$, on the lens plane. This area is determined by the angular size of a pixel, $\Delta\theta$, and the [angular diameter distance](@entry_id:157817) to the lens, $D_A(z_l)$: $A_{\text{pix}} = (D_A(z_l) \Delta\theta)^2$. For a simulation box of side length $L$ placed at [redshift](@entry_id:159945) $z_l$ and mapped onto an $N_{\text{pix}} \times N_{\text{pix}}$ grid, this area simplifies elegantly:

$$
A_{\text{pix}} = \left( \frac{\chi_l}{1+z_l} \cdot \frac{L}{N_{\text{pix}} \chi_l} \right)^2 = \left( \frac{L}{N_{\text{pix}} (1+z_l)} \right)^2
$$

This procedure, repeated for multiple simulation snapshots placed along the past [light cone](@entry_id:157667), generates the stack of lens planes required for the ray-tracing algorithm.

### Numerical Approximations and Systematics

The accuracy of lensing simulations is limited by a range of numerical and physical [systematics](@entry_id:147126). Understanding these is paramount for interpreting the results.

#### Geometric Approximations

The most common geometric simplification is the **flat-sky approximation**, which treats the curved [celestial sphere](@entry_id:158268) as a flat Euclidean plane. This is computationally convenient, allowing the use of Fast Fourier Transforms instead of more complex spherical harmonic transforms. However, this approximation has limitations [@problem_id:3483302]. The fractional geometric error in distances scales as $\sim\theta^2$, where $\theta$ is the [angular size](@entry_id:195896) of the sky patch. For a $10^\circ$ patch, this error is about $0.5\%$, but it grows rapidly for larger fields. Furthermore, a finite flat patch of size $\theta_{\text{patch}}$ cannot represent angular modes with wavelengths larger than the patch itself, meaning it is fundamentally unable to capture power at low multipoles, $\ell \lesssim 2\pi / \theta_{\text{patch}}$. A full-sky treatment avoids these issues but requires working in [spherical geometry](@entry_id:268217), using [spin-weighted spherical harmonics](@entry_id:160698) to represent the shear field, and explicitly parallel-transporting tensor quantities across the sphere.

#### Simulation-Induced Systematics

These [systematics](@entry_id:147126) arise directly from the properties of the $N$-body simulation itself [@problem_id:3483354].

*   **Finite Mass Resolution**: The density field is represented by a finite number of discrete particles. This introduces **Poisson shot noise** into the [matter power spectrum](@entry_id:161407), which behaves as a constant ("white noise") term, $P_{\text{sn}} = 1/\bar{n}_p$, where $\bar{n}_p$ is the mean particle number density. Since the cosmological [power spectrum](@entry_id:159996) falls with increasing [wavenumber](@entry_id:172452) $k$, [shot noise](@entry_id:140025) inevitably dominates at small scales (high $k$, and thus high $\ell$ in projection).

*   **Finite Force Resolution**: To avoid numerical divergences, the [gravitational force](@entry_id:175476) between particles is softened at small separations. This is characterized by a comoving [softening length](@entry_id:755011), $\epsilon$. This procedure effectively smooths the density field, suppressing power in the [gravitational potential](@entry_id:160378) and density at wavenumbers $k \gtrsim 1/\epsilon$. In projection, this leads to a suppression of lensing power at angular multipoles $\ell \gtrsim \chi/\epsilon$.

*   **Discretization of the Light Cone**: Using a finite number of lens planes separated by $\Delta\chi$ to approximate the continuous [line-of-sight integral](@entry_id:751289) is a form of [numerical quadrature](@entry_id:136578). This introduces a **[quadrature error](@entry_id:753905)**, which for a well-designed (e.g., midpoint-rule) scheme scales as $(\Delta\chi)^2$. Using more, thinner planes reduces this error.

#### Finite Volume Effects

These effects stem from the fact that the simulation occupies a finite cubic volume of side length $L$.

*   **Missing Modes**: A periodic box of size $L$ cannot represent density fluctuations with wavelengths larger than $L$. This means the simulation fundamentally lacks power for all modes with wavenumbers $k  2\pi/L$. This leads to a systematic underestimation of clustering on large scales.

*   **Super-Sample Covariance (SSC)**: This is a more subtle and profound consequence of the [finite volume](@entry_id:749401) [@problem_id:3483290]. The missing long-wavelength modes are not just an absence of power; they represent a real physical environment in which the small-scale structures within the box would have evolved. A patch of the universe that happens to be embedded in a large overdensity (a super-sample mode) will form structures more rapidly, leading to enhanced small-scale power. Since our simulation box has a fixed mean density (zero by construction), it cannot capture this modulation of small-scale power by the large-scale environment. The result is that the covariance matrix of power spectrum measurements estimated from a suite of such simulations will be biased low. It will be missing the **super-sample covariance** term, which correlates different multipoles and is approximately a rank-1 contribution to the full covariance matrix. This is a physical effect absent from the simulations, not a numerical artifact within them, and it must be modeled and added back in to obtain an accurate covariance estimate for real-world surveys.