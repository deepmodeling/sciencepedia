## Introduction
Weak gravitational lensing is one of the most powerful tools in modern cosmology, allowing us to map the distribution of all matter—both visible and dark—across the cosmos. It manifests as a subtle, coherent distortion in the shapes of distant galaxies, caused by the bending of their light as it travels through the inhomogeneous large-scale structure of the Universe. The central challenge for cosmologists is to accurately interpret these minute distortions to reconstruct the underlying mass distribution and constrain the fundamental parameters that govern our Universe's evolution. This article provides a graduate-level foundation for understanding and utilizing this crucial observational technique.

The following chapters will guide you through the theory and practice of weak gravitational lensing. We begin with **Principles and Mechanisms**, which lays out the mathematical framework connecting the matter density field to the lensing potential, shear, and convergence. Next, **Applications and Interdisciplinary Connections** explores how these principles are put to use, from creating mass maps of the cosmic web and performing precision cosmology to testing the tenets of General Relativity. Finally, the **Hands-On Practices** section provides opportunities to engage directly with key concepts through guided numerical exercises, such as building a ray-tracing simulation and confronting the mass-sheet degeneracy.

## Principles and Mechanisms

Gravitational lensing provides a direct probe of the total matter distribution in the Universe, irrespective of its composition or dynamical state. This chapter delves into the fundamental principles and mechanisms that govern weak gravitational lensing, bridging the gap between theoretical cosmology and observational reality. We will begin by formalizing the distortion of light paths, connect these distortions to the underlying matter density, explore their observational consequences, and finally, address the principal challenges inherent in their measurement and interpretation.

### The Lensing Potential and the Jacobian Matrix

The journey of light from distant sources to an observer is perturbed by the gravitational influence of intervening matter. In the weak lensing regime, these perturbations are small and can be described by a scalar field on the sky known as the **lensing potential**, $\psi(\boldsymbol{\theta})$, where $\boldsymbol{\theta}$ is the angular position on the celestial sphere. This potential dictates the mapping between the true, unlensed angular position of a source, $\boldsymbol{\beta}$, and its observed, lensed position, $\boldsymbol{\theta}$. For small deflections, this mapping is given by:

$\boldsymbol{\beta} = \boldsymbol{\theta} - \nabla \psi(\boldsymbol{\theta})$

where $\nabla$ is the two-dimensional angular gradient operator. The local properties of this mapping are encapsulated by its Jacobian matrix, $\mathbf{A}$, which describes how an infinitesimal area on the source plane is distorted into an observed image.

$\mathbf{A}_{ij} = \frac{\partial \beta_i}{\partial \theta_j} = \delta_{ij} - \frac{\partial^2 \psi}{\partial \theta_i \partial \theta_j} = \delta_{ij} - \Psi_{ij}$

Here, $\delta_{ij}$ is the Kronecker delta and $\Psi_{ij} = \partial_i \partial_j \psi$ is the Hessian matrix of the lensing potential. The Jacobian matrix can be decomposed to describe the physical effects on the observed image. It is conventional to parameterize the distortion in terms of the **convergence**, $\kappa$, and the two components of **shear**, $\gamma_1$ and $\gamma_2$:

$\mathbf{A} = \begin{pmatrix} 1 - \kappa - \gamma_1  & -\gamma_2 \\ -\gamma_2 & 1 - \kappa + \gamma_1 \end{pmatrix}$

By comparing this form with the definition $\mathbf{A} = \mathbf{I} - \mathbf{\Psi}$, we can identify the convergence and shear components directly from the second derivatives of the lensing potential:

$\kappa = \frac{1}{2}(\Psi_{11} + \Psi_{22}) = \frac{1}{2}\nabla^2\psi$

$\gamma_1 = \frac{1}{2}(\Psi_{11} - \Psi_{22})$

$\gamma_2 = \Psi_{12} = \Psi_{21}$

The convergence, $\kappa$, describes an isotropic change in the image size, while the shear, $\boldsymbol{\gamma} = (\gamma_1, \gamma_2)$, describes an anisotropic stretching or squashing of the image, which transforms circular sources into ellipses.

For example, consider a simple, hypothetical lensing potential given by $\psi(\theta_x, \theta_y) = \frac{a}{2}(\theta_x^2 + \theta_y^2) + \frac{b}{2}(\theta_x^2 - \theta_y^2)$ [@problem_id:3502414]. The Hessian matrix is constant across the field: $\Psi_{11} = a+b$, $\Psi_{22} = a-b$, and $\Psi_{12} = 0$. From the definitions, we can immediately identify the convergence as $\kappa = a$ and the shear components as $\gamma_1 = b$ and $\gamma_2 = 0$.

The operator that connects the potential $\psi$ to the convergence $\kappa$ is the Laplacian, $\nabla^2$. The specific form of this operator depends on the geometry of the space. In the **flat-sky approximation**, valid for small survey areas, the sky is treated as a tangent plane. Here, the Laplacian acts on Fourier modes $e^{i\boldsymbol{\ell} \cdot \boldsymbol{\theta}}$ with an eigenvalue of $-\ell^2$, leading to the Fourier-space relation $\hat{\kappa}(\boldsymbol{\ell}) = \frac{1}{2}\ell^2 \hat{\psi}(\boldsymbol{\ell})$. On a **curved sky**, which is the correct description for large areas, the appropriate basis functions are the spherical harmonics $Y_{\ell m}$, which are eigenfunctions of the Laplace-Beltrami operator with eigenvalues $-\ell(\ell+1)$. This yields the relation $\kappa_{\ell m} = \frac{1}{2}\ell(\ell+1)\psi_{\ell m}$. The discrepancy between the factors $\ell^2$ and $\ell(\ell+1)$ introduces a systematic bias in power spectrum analyses if the flat-sky approximation is used inappropriately for large-scale surveys [@problem_id:3502449].

### From Matter Density to Lensing Observables

The lensing potential $\psi$, and thus the convergence $\kappa$, are not arbitrary fields; they are sourced by the distribution of matter along the line of sight. The convergence at a given angular position $\boldsymbol{\theta}$ can be expressed as a weighted integral of the matter density contrast, $\delta(\chi\boldsymbol{\theta}, \chi) = (\rho - \bar{\rho})/\bar{\rho}$, along the comoving line-of-sight distance $\chi$:

$\kappa(\boldsymbol{\theta}) = \int_0^{\chi_H} d\chi \, W(\chi) \, \delta(\chi\boldsymbol{\theta}, \chi)$

Here, $\chi_H$ is the comoving distance to the horizon, and $W(\chi)$ is the **lensing efficiency kernel**. This kernel quantifies how effectively matter at a given distance $\chi$ lenses the background sources. Its derivation provides deep physical insight into the lensing mechanism [@problem_id:3502411].

Starting from the Poisson equation in comoving coordinates and relating it to the lensing potential, the kernel for a distribution of source galaxies with a normalized comoving distance distribution $n(\chi')$ is found to be:

$W(\chi) = \frac{3 H_0^2 \Omega_m}{2 c^2} \frac{\chi}{a(\chi)} \int_{\chi}^{\chi_H} d\chi' \, n(\chi') \frac{\chi' - \chi}{\chi'}$

Let us dissect this fundamental expression:
- The prefactor $\frac{3 H_0^2 \Omega_m}{2 c^2}$ combines fundamental constants ($G$, $c$) and cosmological parameters ($H_0$, $\Omega_m$). It arises directly from the coupling constant in the Poisson equation, $4\pi G$, and the expression for the mean matter density today in terms of the critical density.
- The factor $\frac{1}{a(\chi)}$, where $a(\chi)$ is the scale factor, accounts for the evolution of the physical matter density. Since physical density scales as $a^{-3}$, the source term in the comoving Poisson equation acquires this $1/a$ dependence, correctly reflecting that a given density contrast $\delta$ at higher redshift (smaller $a$) corresponds to a larger physical density and thus stronger lensing.
- The factor $\chi$ in front of the integral arises from the geometry of projection, specifically from converting angular derivatives on the sky to transverse derivatives in comoving space.
- The integral term $\int_{\chi}^{\chi_H} d\chi' \, n(\chi') \frac{\chi' - \chi}{\chi'}$ represents the geometrical efficiency, averaged over the entire population of source galaxies. The integration limit from $\chi$ to $\chi_H$ enforces causality: only matter in front of a source can lens it. The term $\frac{\chi'-\chi}{\chi'}$ is the geometric "lever arm" for a flat universe, representing the ratio of the comoving lens-source distance to the observer-source distance. Lensing is most efficient when the lens is halfway between the observer and the source.

While this integral expression is powerful for theoretical work, numerical simulations often adopt a more direct approach by performing **ray tracing**. This involves propagating individual light rays through a discretized 3D matter distribution, applying deflection "kicks" at multiple lens planes along the path. Such methods provide a non-perturbative way to solve for the light path and can capture effects beyond the Born approximation used in the integral formulation [@problem_id:3502405].

### Magnification and its Observational Consequences

Gravitational lensing conserves surface brightness, but it changes the apparent solid angle of a source. This leads to a change in the observed flux, an effect known as **magnification**, $\mu$. The magnification is given by the inverse of the determinant of the lensing Jacobian matrix:

$\mu = \frac{1}{\det \mathbf{A}} = \frac{1}{(1-\kappa)^2 - |\boldsymbol{\gamma}|^2}$

where $|\boldsymbol{\gamma}|^2 = \gamma_1^2 + \gamma_2^2$. In the weak lensing limit ($\kappa, |\boldsymbol{\gamma}| \ll 1$), this can be approximated as $\mu \approx 1 + 2\kappa$.

Magnification has two competing effects on the observed number counts of galaxies in a flux-limited survey [@problem_id:3502414]:
1.  **Solid-angle Dilation**: The lensing stretches the solid angle on the sky, diluting the number of sources per unit area by a factor of $1/\mu$.
2.  **Flux Amplification**: Fainter sources, which are intrinsically more numerous, are magnified above the survey's flux limit, increasing the number of observed sources.

The net effect is known as **magnification bias**. If the unlensed cumulative number counts as a function of apparent magnitude $m$ follow a power law $N_0(<m) \propto 10^{\alpha m}$, where $\alpha$ is the logarithmic slope, the net fractional change in observed number density $\delta_n/n$ is given by:

$\frac{\delta_n}{n} \approx 2(2.5\alpha - 1)\kappa$

This relationship shows that the observed galaxy density field is itself a (biased) tracer of the convergence field, providing another avenue to probe the mass distribution. The sign of the effect depends on whether $\alpha$ is greater or less than $0.4$.