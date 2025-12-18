## Introduction
Full-Waveform Inversion (FWI) has revolutionized [seismic imaging](@entry_id:273056) by producing high-resolution models of the Earth's subsurface. However, conventional FWI often relies on an isotropic assumption, which is an oversimplification for many complex geological environments like sedimentary basins or fractured reservoirs. The true elastic properties of these regions are often anisotropic, meaning their seismic velocities vary with the direction of wave propagation. Ignoring this reality can lead to significant imaging artifacts and erroneous geological interpretations.

This article addresses this critical gap by providing a comprehensive overview of multiparameter and anisotropic Full-Waveform Inversion. We will move beyond the isotropic approximation to explore the methods required to characterize the Earth in its full complexity. Readers will gain a deep understanding of the advanced principles, practical challenges, and cutting-edge applications of this powerful imaging technique.

The journey begins in the **Principles and Mechanisms** chapter, where we will establish the physical and mathematical foundations of wave propagation in [anisotropic media](@entry_id:260774) and formulate the multiparameter [inverse problem](@entry_id:634767) using the [adjoint-state method](@entry_id:633964). Next, the **Applications and Interdisciplinary Connections** chapter explores advanced inversion strategies for real-world data, the importance of optimal survey design, and the broader impact of FWI concepts in fields like materials science. Finally, the **Hands-On Practices** section provides an opportunity to apply these theoretical concepts to concrete computational problems, solidifying the understanding of key challenges in anisotropic FWI.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms that underpin multiparameter and anisotropic [full-waveform inversion](@entry_id:749622) (FWI). We will first establish the physical and mathematical basis for modeling [wave propagation](@entry_id:144063) in complex [anisotropic media](@entry_id:260774). Subsequently, we will formulate the [inverse problem](@entry_id:634767), deriving the [objective function](@entry_id:267263) and the gradient necessary for [iterative optimization](@entry_id:178942). Finally, we will explore the key challenges inherent to multiparameter FWI, including [parameter sensitivity](@entry_id:274265), cross-talk, and the critical role of [model parameterization](@entry_id:752079) and resolution analysis.

### The Anisotropic Forward Problem: Modeling the Wavefield

Accurate FWI is predicated on a [forward modeling](@entry_id:749528) engine that can faithfully replicate the physics of wave propagation. In most geological settings, the assumption of [isotropy](@entry_id:159159) is an oversimplification. Therefore, we must begin with the [equations of motion](@entry_id:170720) in a generally anisotropic elastic solid.

#### The Anisotropic Elastic Wave Equation and the Stiffness Tensor

The propagation of [elastic waves](@entry_id:196203) in a source-free continuum is governed by the [conservation of linear momentum](@entry_id:165717). Combined with a linear [constitutive relation](@entry_id:268485) (Hooke's Law) and the definition of [infinitesimal strain](@entry_id:197162), we arrive at the anisotropic [elastic wave equation](@entry_id:748864). In [tensor notation](@entry_id:272140), these foundational relationships are expressed as:

1.  **Conservation of Momentum (Cauchy's First Law of Motion):**
    $ \rho \partial_t^2 u_i = \partial_j \sigma_{ij} $

2.  **Linear Elastic Constitutive Law (Generalized Hooke's Law):**
    $ \sigma_{ij} = C_{ijkl} \epsilon_{kl} $

3.  **Infinitesimal Strain-Displacement Relation:**
    $ \epsilon_{kl} = \frac{1}{2}(\partial_k u_l + \partial_l u_k) $

Here, $\rho$ is the density, $\mathbf{u}$ is the displacement vector, $\sigma_{ij}$ is the second-order stress tensor, $\epsilon_{kl}$ is the second-order strain tensor, and $C_{ijkl}$ is the fourth-order stiffness tensor that characterizes the elastic properties of the medium.

The stiffness tensor $C_{ijkl}$ is the centerpiece of anisotropic modeling. In three dimensions, it contains $3^4 = 81$ components. However, intrinsic symmetries significantly reduce the number of independent constants. The symmetry of the stress ($\sigma_{ij} = \sigma_{ji}$) and strain ($\epsilon_{kl} = \epsilon_{lk}$) tensors imposes minor symmetries on the stiffness tensor ($C_{ijkl} = C_{jikl} = C_{ijlk}$), reducing the independent components to 36. The existence of a [strain-energy density function](@entry_id:755490) further imposes a [major symmetry](@entry_id:198487) ($C_{ijkl} = C_{klij}$), which reduces the number of [independent elastic constants](@entry_id:203649) to 21 for the most general case of anisotropy, known as a **triclinic** medium .

The complexity of the FWI problem is directly related to the number of independent parameters in $C_{ijkl}$, which is determined by the material's symmetry. Key [symmetry classes](@entry_id:137548) relevant to [geophysics](@entry_id:147342) include:

*   **Orthorhombic:** Possesses three mutually orthogonal planes of symmetry. This reduces the number of independent constants to 9. Examples include fractured media with orthogonal fracture sets. In Voigt notation, the stiffness matrix is characterized by non-zero diagonal terms and off-diagonal coupling terms between normal stresses ($C_{12}, C_{13}, C_{23}$) .

*   **Transverse Isotropy (TI):** Has a single axis of rotational symmetry. If this axis is vertical, the medium is described as **Vertically Transverse Isotropy (VTI)**. This is a common approximation for sedimentary basins where layering is the dominant cause of anisotropy. A VTI medium is described by 5 [independent elastic constants](@entry_id:203649) .

*   **Isotropy:** Exhibits full [rotational invariance](@entry_id:137644), meaning its properties are the same in all directions. This is the simplest case, where the 5 constants of a TI medium are further constrained, leaving only 2 independent constants. These are typically chosen as the Lamé parameters, $\lambda$ and $\mu$. The isotropic [stiffness tensor](@entry_id:176588) is given by $C_{ijkl} = \lambda \delta_{ij}\delta_{kl} + \mu(\delta_{ik}\delta_{jl}+\delta_{il}\delta_{jk})$.

#### Plane Waves, Phase Velocity, and the Christoffel Equation

To understand how anisotropy affects wave propagation, we analyze the behavior of [plane waves](@entry_id:189798). By substituting a plane-wave [ansatz](@entry_id:184384), $\mathbf{u}(\mathbf{x}, t) = \mathbf{A} \exp(i(\omega t - \mathbf{k} \cdot \mathbf{x}))$, into the [elastic wave equation](@entry_id:748864), we obtain the **Christoffel equation**:

$ \Gamma_{il} A_l = \rho v^2 A_i $

where $\mathbf{A}$ is the polarization vector, $v = \omega / |\mathbf{k}|$ is the phase velocity, and $\Gamma_{il} = C_{ijkl} n_j n_k$ is the **Christoffel stiffness matrix**, with $\mathbf{n} = \mathbf{k} / |\mathbf{k}|$ being the [unit vector](@entry_id:150575) in the propagation direction.

This is an [eigenvalue problem](@entry_id:143898). For any given propagation direction $\mathbf{n}$, the three eigenvalues of the matrix $\mathbf{\Gamma}$ give the values of $\rho v^2$ for the three types of waves that can propagate in that direction. The corresponding eigenvectors give their polarization directions. In a general [anisotropic medium](@entry_id:187796), these modes are a quasi-compressional (qP) wave and two quasi-shear (qS1, qS2) waves, whose polarizations are mutually orthogonal but not necessarily purely parallel or perpendicular to the propagation direction.

Let's consider two important cases :

*   **Isotropic Medium:** The Christoffel matrix becomes $\Gamma_{il} = (\lambda + \mu) n_i n_l + \mu \delta_{il}$. Solving the eigenvalue problem yields two distinct phase velocities, independent of the propagation direction $\mathbf{n}$:
    *   Compressional (P-wave) speed: $v_p = \sqrt{(\lambda + 2\mu)/\rho}$, with polarization parallel to $\mathbf{n}$.
    *   Shear (S-wave) speed: $v_s = \sqrt{\mu/\rho}$, a degenerate eigenvalue for any polarization perpendicular to $\mathbf{n}$.

*   **VTI Medium:** The phase velocities now depend on the angle of propagation with respect to the symmetry axis. For propagation along the symmetry axis (e.g., vertical, $\mathbf{n} = (0,0,1)$), the speeds are $v_P^{\parallel} = \sqrt{C_{33}/\rho}$ and $v_S^{\parallel} = \sqrt{C_{44}/\rho}$. For propagation perpendicular to the axis (e.g., horizontal, $\mathbf{n} = (1,0,0)$), three distinct speeds emerge: $v_P^{\perp} = \sqrt{C_{11}/\rho}$, $v_{SV}^{\perp} = \sqrt{C_{44}/\rho}$, and $v_{SH}^{\perp} = \sqrt{C_{66}/\rho}$. The fact that $v_P^{\parallel} \neq v_P^{\perp}$ and $v_S^{\parallel} \neq v_{SH}^{\perp}$ is the defining characteristic of P-wave and SH-wave anisotropy, respectively. This direction-dependent velocity is the primary kinematic signature that FWI aims to exploit.

#### Practical Parameterizations of Anisotropy

While the stiffness coefficients $C_{ijkl}$ provide a complete description, they are often not intuitive and can be difficult to constrain in an inversion. Therefore, practical parameterizations are essential.

For VTI media, the most common is **Thomsen's [parameterization](@entry_id:265163)** . It recasts the 5 independent stiffnesses into a more physically meaningful set: the vertical P-wave speed ($v_{p0}$), the vertical S-[wave speed](@entry_id:186208) ($v_{s0}$), and three dimensionless anisotropy parameters ($\epsilon$, $\delta$, $\gamma$). These parameters are defined in terms of the stiffness coefficients (e.g., $\epsilon = (C_{11} - C_{33})/(2C_{33})$). In the limit of weak anisotropy, they have direct physical interpretations:
*   **$\epsilon$** approximates the fractional difference between horizontal and vertical P-wave velocities, i.e., $(v_P(\pi/2) - v_{p0})/v_{p0}$.
*   **$\gamma$** approximates the fractional difference between horizontal and vertical SH-wave velocities.
*   **$\delta$** is more subtle. It governs the P-wave velocity for near-vertical propagation and is the key parameter controlling the short-spread Normal Moveout (NMO) velocity.

Another important class of anisotropy is **Tilted Transverse Isotropy (TTI)**, which describes a medium that is locally VTI but whose symmetry axis is tilted. This is crucial for modeling areas with dipping sedimentary layers or tectonic deformation. A TTI medium is still described by 5 intrinsic [elastic constants](@entry_id:146207), but its orientation requires two additional parameters: a **tilt angle** (polar angle from the vertical) and an **azimuth angle** (angle in the horizontal plane) . To model [wave propagation](@entry_id:144063) in a global coordinate system, the local VTI [stiffness tensor](@entry_id:176588) $C^{\ell}_{ijkl}$ must be rotated into the global frame. This is a fourth-order [tensor transformation](@entry_id:161187):

$ C^{g}_{pqrs} = R_{pi}R_{qj}R_{rk}R_{sl} C^{\ell}_{ijkl} $

Here, $\mathbf{R}$ is the $3 \times 3$ rotation matrix constructed from the tilt and azimuth angles. This rotation mixes the components of the tensor, resulting in a much more densely populated stiffness matrix in the global frame, which correctly captures the complex wave behavior in TTI media.

### Formulating the Inverse Problem: Misfit and Gradients

FWI seeks to find an Earth model $\mathbf{m}$ that minimizes the difference between observed seismic data $\mathbf{d}_{\text{obs}}$ and synthetic data $\mathbf{p}(\mathbf{m})$ predicted by the [forward model](@entry_id:148443). This is formulated as an optimization problem.

#### The Waveform Misfit Functional

The core of FWI is the [objective function](@entry_id:267263), or [misfit functional](@entry_id:752011), which quantifies the data residual. For single-component data, a simple L2-norm is often used. However, for multicomponent anisotropic FWI, a more sophisticated formulation is required to handle vector-valued data and [correlated noise](@entry_id:137358).

Assuming the noise is zero-mean and Gaussian, the Maximum Likelihood principle leads to a generalized [least-squares](@entry_id:173916) [misfit functional](@entry_id:752011). For multicomponent data, this takes the form :

$ J(\mathbf{m}) = \frac{1}{2} \sum_{s} \sum_{r} \int \big[\mathbf{d}_{sr}(t) - \mathbf{p}_{sr}(t;\mathbf{m})\big]^{\top} \mathbf{\Sigma}_{sr}^{-1} \big[\mathbf{d}_{sr}(t) - \mathbf{p}_{sr}(t;\mathbf{m})\big] \mathrm{d}t $

where $\mathbf{d}_{sr}(t)$ and $\mathbf{p}_{sr}(t;\mathbf{m})$ are the vector-valued observed and predicted data for source $s$ and receiver $r$, and $\mathbf{\Sigma}_{sr}$ is the data noise covariance matrix. The [inverse covariance matrix](@entry_id:138450) $\mathbf{\Sigma}_{sr}^{-1}$ serves as a weighting operator that properly accounts for different noise levels on each component and, crucially, for any cross-correlations in the noise.

In practice, the absolute amplitudes of seismic data can be unreliable due to unknown source strength, uncertain receiver coupling, or unmodeled physical effects like attenuation. Instead of forcing the inversion to fit these incorrect amplitudes by introducing artifacts into the Earth model, it is common to augment the problem by introducing **[nuisance parameters](@entry_id:171802)**. These can include per-shot scaling factors or even a full frequency-dependent source [wavelet](@entry_id:204342) $\gamma_s(\omega)$, which are estimated jointly with the Earth model parameters. The [forward model](@entry_id:148443) is modified, for instance, to $\gamma_s(\omega) \mathbf{p}_{sr}(\omega; \mathbf{m})$, and the misfit is minimized with respect to both $\mathbf{m}$ and $\gamma_s(\omega)$ .

#### Gradient Computation via the Adjoint-State Method

Most FWI algorithms rely on local, [gradient-based optimization](@entry_id:169228) methods, such as steepest descent or quasi-Newton methods. These require the computation of the gradient of the [misfit functional](@entry_id:752011) $J$ with respect to the model parameters $\mathbf{m}$. Calculating this gradient efficiently is the central computational challenge of FWI. A brute-force approach, perturbing each model parameter individually, would require one forward simulation per parameter, which is computationally prohibitive for large models.

The **[adjoint-state method](@entry_id:633964)** provides an elegant and efficient solution. It allows the computation of the entire [gradient vector](@entry_id:141180) at the cost of only two simulations per source: one forward simulation to compute the predicted data and residuals, and one "adjoint" simulation to propagate information about the residuals backward.

The derivation involves defining a Lagrangian functional that incorporates the governing wave equation as a constraint. By setting the variation of the Lagrangian with respect to the forward field to zero, one derives the **[adjoint equation](@entry_id:746294)** and its corresponding **adjoint source**. For the general anisotropic [elastic wave equation](@entry_id:748864) and the multicomponent [misfit functional](@entry_id:752011) discussed above, the adjoint source term $\mathbf{s}^*(\mathbf{x}, t)$ that drives the adjoint wavefield $\mathbf{u}^*$ is found to be :

$ \mathbf{s}^{\ast}(\mathbf{x}, t) = - \sum_{r} \mathbf{Q}_{r}^{\top} \mathbf{W}_{r} \left( \mathbf{Q}_{r} \mathbf{u}(\mathbf{x}_{r},t) - \mathbf{d}_{r}(t) \right) \delta(\mathbf{x}-\mathbf{x}_r) $

Here, the data residual at each receiver $r$ is weighted by the (inverse-covariance) weight matrix $\mathbf{W}_r$ and projected back from the instrument's measurement space via $\mathbf{Q}_r^{\top}$. The result is injected as a time-reversed [body force](@entry_id:184443) at the receiver location, driving the adjoint simulation backward in time. The adjoint wave equation itself is self-adjoint, meaning it has the same form as the forward equation.

A key aspect of anisotropic FWI is the coupling between wavefield components. This coupling appears in the adjoint field through two mechanisms :
1.  **Measurement Coupling:** If the receiver instrument matrix $\mathbf{Q}_r$ or the weighting matrix $\mathbf{W}_r$ is non-diagonal, a residual on one measured component will generate an adjoint [source term](@entry_id:269111) for all three physical displacement components.
2.  **Propagation Coupling:** Even with a diagonal source, the anisotropic nature of the stiffness tensor $C_{ijkl}$ inherently couples the displacement components during propagation. A force in the $x$-direction will generate waves with displacement in all three directions as the adjoint field propagates.

Once the adjoint field $\mathbf{u}^*$ is computed, the gradient of the [misfit functional](@entry_id:752011) with respect to a specific model parameter (e.g., a stiffness coefficient $C_{pqrs}$) can be found by a zero-lag [cross-correlation](@entry_id:143353) of the forward and adjoint fields.

### Key Challenges in Multiparameter FWI

Moving from isotropic to anisotropic FWI significantly increases the number of parameters to be resolved, introducing profound challenges related to parameter trade-offs, non-uniqueness, and resolution.

#### Parameter Sensitivity and Cross-Talk

The success of FWI depends on the sensitivity of the seismic data to the model parameters. Different parameters influence the wavefield in distinct ways that vary with acquisition geometry (e.g., offset, azimuth, and angle). For example, consider the P-P reflection coefficient $R_{PP}(\theta)$ from a weak-contrast VTI interface. The linearized approximation shows that $R_{PP}$ is a weighted sum of contrasts in the anisotropy parameters $\Delta\epsilon$ and $\Delta\delta$, with weights that depend on the incidence angle $\theta$ :

$ R_{PP}(\theta) \approx A(\theta) \Delta\delta + B(\theta) \Delta\epsilon $

where the sensitivity kernels are approximately $A(\theta) \propto \sin^2\theta \cos^2\theta$ and $B(\theta) \propto \sin^4\theta$. The sensitivity to $\Delta\delta$ peaks at mid-range angles (around $45^\circ$), while the sensitivity to $\Delta\epsilon$ is strongest at the widest angles. This demonstrates that resolving both parameters requires data with a broad range of illumination angles. At an angle of $\theta = \pi/4$, the sensitivities have equal magnitude, highlighting a point of potential ambiguity if data were limited to this angle.

This leads to the concept of **parameter cross-talk**, where the effect of a perturbation in one parameter can be partially or fully compensated by a perturbation in another. This creates ambiguity and [ill-posedness](@entry_id:635673) in the [inverse problem](@entry_id:634767). A dangerous manifestation of cross-talk occurs when using an incomplete physical model. For instance, if one employs a "pseudo-acoustic" FWI algorithm that models P-wave anisotropy but ignores shear-wave physics, changes in the true shear velocity $v_{s0}$ can create angle-dependent travel-time changes. The inversion, lacking the ability to update $v_{s0}$ or its related parameters, may misattribute these effects to a spurious update in the P-wave velocity $v_{p0}$, leading to a biased and geologically incorrect model .

#### The Choice of Inversion Parameterization

The severity of cross-talk is intimately linked to the choice of inversion parameters. While Thomsen's parameters are physically intuitive, they can exhibit strong trade-offs. For example, in many acquisition geometries, the effects of changing $v_{p0}$ and $\delta$ can be very similar, leading to high correlation. An alternative is to invert directly for components of the [stiffness tensor](@entry_id:176588), such as $C_{11}$ and $C_{33}$.

The "orthogonality" of a [parameterization](@entry_id:265163) can be quantified by examining the gradients. If the gradients with respect to two parameters, $\nabla_a J$ and $\nabla_b J$, are nearly parallel, the parameters are highly coupled, as an update in the direction of one gradient is nearly identical to an update in the other. A measure of this is the cosine of the angle between the gradient vectors . A value near $\pm 1$ indicates strong coupling, while a value near 0 indicates orthogonality. By analyzing these gradient inner products for different parameterizations (e.g., Thomsen vs. stiffness coefficients) under a given survey geometry, one can select a set of parameters that is better conditioned for inversion, potentially improving convergence and reducing artifacts from cross-talk.

#### Resolution Analysis and the Hessian

A formal analysis of resolution and cross-talk requires examining the **Hessian matrix**, the matrix of second derivatives of the [misfit functional](@entry_id:752011), $\mathbf{H} = \nabla^2 J$. In the vicinity of the solution, the inverse of the Hessian, $\mathbf{H}^{-1}$, approximates the posterior model covariance matrix. Its diagonal elements relate to the uncertainty of each parameter, while its off-diagonal elements quantify the trade-offs between parameters.

In practice, the full Hessian is too expensive to compute. A common approximation is the **Gauss-Newton Hessian**, $\mathbf{H} \approx \mathbf{J}^\top \mathbf{J}$, where $\mathbf{J}$ is the Jacobian or sensitivity matrix. A powerful tool for analyzing the properties of the Hessian is the **Point-Spread Function (PSF)**. A PSF is a column of the inverse Hessian, $\mathbf{H}^{-1}$, and represents the model update that would result from a single, localized data impulse. Conceptually, it is the model image of a point diffractor in the subsurface .

The PSF provides invaluable insight into the inversion's capabilities:
*   **Spatial Resolution:** The spatial extent or "spread" of the PSF in its primary parameter block indicates the smallest feature that can be resolved. A narrow PSF implies high resolution.
*   **Parameter Cross-talk:** The "leakage" of energy from the PSF into the blocks corresponding to other model parameters directly visualizes cross-talk. For example, if we compute the PSF for an impulse in the $v_{p0}$ parameter, any significant energy appearing in the $\epsilon$ part of the resulting PSF vector reveals the degree to which $v_{p0}$ and $\epsilon$ are coupled by the survey.

Analysis using PSFs shows that wide angular illumination is critical for [decoupling](@entry_id:160890) anisotropic parameters. With limited-angle data, the PSFs for different parameters can look very similar, indicating low [resolving power](@entry_id:170585) and severe cross-talk. Adding more angles of illumination helps to differentiate the parameter sensitivities, leading to more focused PSFs with less leakage, and thus a better-posed [inverse problem](@entry_id:634767) .