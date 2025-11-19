## Introduction
Simulating wave propagation in unbounded domains, such as for seismic exploration or antenna design, presents a fundamental challenge in computational science: how to model an infinite space on a finite computer. Any artificial truncation of the simulation domain risks generating spurious reflections that contaminate the solution and render it useless. The Perfectly Matched Layer (PML) has emerged as the most powerful and theoretically elegant solution to this problem, providing a nearly reflection-free [absorbing boundary](@entry_id:201489) that has revolutionized wave-based modeling across numerous scientific disciplines.

This article offers a comprehensive exploration of the PML, designed to take the reader from foundational theory to advanced application. It addresses the need for a robust boundary condition by dissecting the unique mechanism that sets the PML apart from simpler methods. Across the following sections, you will gain a deep, practical understanding of this essential technique.

The journey begins in **Principles and Mechanisms**, where we will uncover the core concept of [complex coordinate stretching](@entry_id:162960) that enables the 'perfectly matched' property. We will explore how this frequency-domain idea is translated into efficient time-domain algorithms like the CPML and discuss the practical design considerations for creating a stable and effective layer. Next, **Applications and Interdisciplinary Connections** will broaden our scope, demonstrating the PML's remarkable versatility in complex physical systems such as [elastodynamics](@entry_id:175818), [poroelasticity](@entry_id:174851), and even general relativity. This section also highlights the PML's critical role as an enabling technology for advanced fields like [full-waveform inversion](@entry_id:749622) and [physics-informed machine learning](@entry_id:137926). Finally, **Hands-On Practices** will provide a set of targeted problems, allowing you to engage directly with the material and develop a practical intuition for PML design, stability analysis, and performance evaluation.

## Principles and Mechanisms

The accurate simulation of [wave propagation](@entry_id:144063) in unbounded domains is a central challenge in [computational geophysics](@entry_id:747618). Since computational resources are finite, the physical domain must be truncated by an artificial boundary. The design of this boundary is critical; an [ideal boundary](@entry_id:200849) would perfectly absorb all outgoing waves without generating spurious reflections, thus mimicking an infinitely extended medium. While various methods, such as **[absorbing boundary conditions](@entry_id:164672) (ABCs)** and **sponge layers**, have been developed, the **Perfectly Matched Layer (PML)** stands as the most effective and widely used technique for this purpose. This chapter elucidates the fundamental principles and mechanisms that endow the PML with its remarkable properties.

### The Foundational Principle: Complex Coordinate Stretching

The core idea of the PML, introduced by Bérenger in 1994 and later re-interpreted through the lens of complex analysis, is to surround the computational domain with a layer of artificial material that is perfectly impedance-matched to the physical domain at their interface but is highly dissipative within. This is achieved not by altering the physical parameters of the medium in a conventional sense, but by a more abstract and powerful concept: **[complex coordinate stretching](@entry_id:162960)**.

Let us consider a time-harmonic scalar acoustic wave governed by the Helmholtz equation, $\nabla^2 \hat{u} + k^2 \hat{u} = 0$, where $\hat{u}$ is the frequency-domain acoustic potential and $k = \omega/c$ is the [wavenumber](@entry_id:172452). To implement a PML in the region $x > L$, we introduce a complex "stretched" coordinate $\tilde{x}$ related to the physical coordinate $x$ by an analytic mapping:
$$
\tilde{x}(x) = \int_L^x s_x(\xi) \, d\xi
$$
Here, $s_x(x)$ is a complex-valued **stretch factor**. A common and illustrative choice for this factor is:
$$
s_x(x) = 1 + \frac{\sigma(x)}{i\omega}
$$
where $\sigma(x) \ge 0$ is a real-valued damping profile that is zero for $x \le L$ and positive for $x > L$. By the [chain rule](@entry_id:147422), a derivative with respect to the physical coordinate $x$ is transformed as follows:
$$
\frac{\partial}{\partial x} = \frac{\partial \tilde{x}}{\partial x} \frac{\partial}{\partial \tilde{x}} = s_x(x) \frac{\partial}{\partial \tilde{x}} \quad \implies \quad \frac{\partial}{\partial \tilde{x}} = \frac{1}{s_x(x)} \frac{\partial}{\partial x}
$$
The governing equation inside the PML, when expressed in terms of the physical coordinates, is obtained by replacing the derivative operator $\partial_x$ with its stretched counterpart $(1/s_x)\partial_x$. For a 2D problem with a PML only in the $x$-direction, the Helmholtz equation becomes:
$$
\frac{1}{s_x(x)} \frac{\partial}{\partial x} \left( \frac{1}{s_x(x)} \frac{\partial \hat{u}}{\partial x} \right) + \frac{\partial^2 \hat{u}}{\partial y^2} + k^2 \hat{u} = 0
$$
The effect of this transformation is profound. A plane wave propagating into the PML, with spatial dependence $\exp(ik_x x)$, is transformed into a wave that behaves as $\exp(ik_x \tilde{x})$. Substituting the definition of $\tilde{x}$ and $s_x$:
$$
\exp\left(ik_x \int_L^x \left(1 + \frac{\sigma(\xi)}{i\omega}\right) d\xi\right) = \exp(ik_x (x-L)) \exp\left(-\frac{k_x}{\omega} \int_L^x \sigma(\xi) d\xi\right)
$$
The complex part of the stretch factor transforms the oscillatory wave into a spatially decaying (evanescent) one, thus achieving absorption. The imaginary part of $s_x$ must be positive (or its real part if defined as $s_x = 1+i\sigma/\omega$) for decay to occur for waves propagating into the layer.

### The "Perfectly Matched" Property and Zero Reflection

The genius of the PML lies not just in its ability to absorb waves, but to do so without generating reflections at the interface between the physical domain and the layer. This "perfectly matched" property is a direct consequence of the complex stretching formulation in the continuous partial differential equation setting [@problem_id:3612645].

To demonstrate this, consider a [plane wave](@entry_id:263752) $\hat{u}_{\mathrm{inc}}(\mathbf{x}) = \exp(i(k_x x + k_y y))$ incident on a PML interface at $x=L$. The total field in the physical domain ($x \le L$) is the sum of the incident and a reflected wave, $\hat{u} = \exp(i(k_x x + k_y y)) + R \exp(i(-k_x x + k_y y))$, while the transmitted field in the PML ($x > L$) is $\hat{u} = T \exp(i(k_x \tilde{x} + k_y y))$.

The appropriate [interface conditions](@entry_id:750725), derived from the [weak formulation](@entry_id:142897) of the stretched wave equation, are the continuity of the field $\hat{u}$ and the continuity of the transformed normal flux, $(1/s_x)\partial_x \hat{u}$. At the interface $x=L$, the damping $\sigma(L)=0$, so $s_x(L)=1$. Applying these two conditions yields a system of two equations for the reflection coefficient $R$ and [transmission coefficient](@entry_id:142812) $T$:
1.  Continuity of $\hat{u}$: $1 + R = T$
2.  Continuity of $(1/s_x)\partial_x \hat{u}$: $i k_x (1 - R) = i k_x T$

Solving this simple system gives the remarkable result $R=0$ and $T=1$. This holds for any frequency $\omega$ and any [angle of incidence](@entry_id:192705) (any $k_y$), because the matching conditions are independent of these parameters. This is a stark contrast to conventional ABCs, which are typically exact only for a single angle of incidence, and sponge layers, which introduce an [impedance mismatch](@entry_id:261346) and always produce some reflection, no matter how gradual their damping profile is [@problem_id:3612645].

This perfect non-reflecting property can be understood more deeply through the lens of complex analysis [@problem_id:3612653]. If the coefficients of the wave equation are [analytic functions](@entry_id:139584) of the spatial coordinates, the solution itself is an analytic function. The [complex coordinate stretching](@entry_id:162960) can then be interpreted as a deformation of the domain's contour into the complex plane. According to Cauchy's integral theorem, this deformation does not alter the solution within the original, un-deformed domain, provided no singularities of the field are crossed. The PML is, in essence, a numerical realization of this [contour deformation](@entry_id:162827), which elegantly explains why it does not disturb the interior field and is perfectly non-reflecting at the continuous level.

### Time-Domain Implementations: From Split-Fields to Unsplit ADE

The theoretical formulation of PML is most natural in the frequency domain, where the stretch factor $s(\omega)$ is a simple multiplier. For time-domain numerical methods, which are prevalent in [geophysics](@entry_id:147342), implementing this frequency-dependent operation requires special techniques. The multiplication by $1/s_x(\omega)$ in the frequency domain corresponds to a convolution in the time domain, which is computationally expensive to evaluate directly.

The original approach by Bérenger was the **split-field PML** [@problem_id:3612657]. For a 2D acoustic system, the pressure field $p$ is split into two sub-fields, $p = p_x + p_y$. The governing equations are modified such that the damping associated with the $x$-direction acts only on the terms involving $p_x$, and similarly for the $y$-direction. For example, the first-order acoustic equations are modified to a system like:
$$
\partial_t p_x + \sigma_x(x) p_x = -\kappa \partial_x v_x
$$
$$
\partial_t p_y + \sigma_y(y) p_y = -\kappa \partial_y v_y
$$
$$
\rho(\partial_t v_x + \sigma_x(x) v_x) = -\partial_x (p_x+p_y)
$$
... and so on. This formulation, while doubling the number of fields to be stored, results in a system of local-in-time [partial differential equations](@entry_id:143134) that can be solved with standard [time-stepping schemes](@entry_id:755998). It can be rigorously shown that this split-field system is equivalent to the [complex coordinate stretching](@entry_id:162960) formulation and thus preserves the zero-reflection property [@problem_id:3612657].

A more modern and often more robust approach is the **unsplit formulation**, commonly known as the **Convolutional PML (CPML)** or **Auxiliary Differential Equation (ADE) PML** [@problem_id:3572761]. This method directly tackles the temporal convolution by introducing auxiliary memory variables that satisfy simple [ordinary differential equations](@entry_id:147024) (ODEs). For a typical stretch factor, the convolution kernel is exponential, allowing for a recursive update of the memory variables at each time step. This avoids both the costly history integral and the need to split physical fields, making it highly efficient and more easily extensible to complex physics, such as [anisotropic elasticity](@entry_id:186771), where field splitting can break essential symmetries and lead to instabilities [@problem_id:3612664] [@problem_id:3572761].

To enhance the performance of PMLs, particularly for broadband signals containing very low frequencies and for absorbing [evanescent waves](@entry_id:156713), the simple stretch factor is often replaced by a **complex-frequency-shifted (CFS)** form:
$$
s(\omega) = \kappa + \frac{d}{\alpha + i\omega}
$$
Here, $d$ is a [damping parameter](@entry_id:167312), $\kappa \ge 1$ is a real stretching factor that aids in absorbing [evanescent waves](@entry_id:156713), and $\alpha \ge 0$ is the frequency shift. The shift $\alpha$ improves absorption of low-frequency components and regularizes the temporal kernel, which mitigates late-time instabilities that can plague classical PML formulations [@problem_id:3572761].

### Generality and Application to Complex Media

The principle of [complex coordinate stretching](@entry_id:162960) is not limited to scalar [acoustic waves](@entry_id:174227). It can be systematically applied to any linear hyperbolic system, including the equations of isotropic and [anisotropic elasticity](@entry_id:186771). For a 2D isotropic elastic medium described by the velocity-stress [first-order system](@entry_id:274311), the PML is implemented by applying the same derivative transformations, $\partial_x \to (1/s_x)\partial_x$ and $\partial_z \to (1/s_z)\partial_z$, to all spatial derivatives in the momentum and [constitutive equations](@entry_id:138559).

Defining the [state vector](@entry_id:154607) as $\mathbf{q} = [v_x, v_z, \sigma_{xx}, \sigma_{zz}, \sigma_{xz}]^T$, the stretched system can be written in the [compact operator](@entry_id:158224) form $\partial_t \mathbf{q} = \mathcal{L}_s \mathbf{q}$, where $\mathcal{L}_s$ is the matrix of transformed [differential operators](@entry_id:275037) [@problem_id:3612701]:
$$
\mathcal{L}_s =
\begin{pmatrix}
0  & 0  & \frac{1}{\rho s_x}\frac{\partial}{\partial x}  & 0  & \frac{1}{\rho s_z}\frac{\partial}{\partial z} \\
0  & 0  & 0  & \frac{1}{\rho s_z}\frac{\partial}{\partial z}  & \frac{1}{\rho s_x}\frac{\partial}{\partial x} \\
\frac{\lambda+2\mu}{s_x}\frac{\partial}{\partial x}  & \frac{\lambda}{s_z}\frac{\partial}{\partial z}  & 0  & 0  & 0 \\
\frac{\lambda}{s_x}\frac{\partial}{\partial x}  & \frac{\lambda+2\mu}{s_z}\frac{\partial}{\partial z}  & 0  & 0  & 0 \\
\frac{\mu}{s_z}\frac{\partial}{\partial z}  & \frac{\mu}{s_x}\frac{\partial}{\partial x}  & 0  & 0  & 0
\end{pmatrix}
$$
This demonstrates the mechanical and general nature of applying the PML transformation to more complex physical systems.

### Practical Design and Advanced Considerations

While the PML is perfect in the continuous limit, its performance in a practical numerical simulation depends on several design choices and an awareness of potential pitfalls.

#### Damping Profile Design

The effectiveness of a PML of finite thickness $L$ depends on the choice of the damping profile $\sigma(x)$. A common choice is a polynomial profile, $\sigma(x) = \sigma_{\max} (x/L)^m$, which is zero at the interface and increases towards the outer boundary. The reflection from the back of the layer can be approximated by a two-way attenuation formula. For a target reflection amplitude $R_0$, the required peak damping $\sigma_{\max}$ can be derived analytically [@problem_id:3612686]:
$$
\sigma_{\max} = - \frac{c (m+1)}{2 L} \ln(R_{0})
$$
This formula provides a powerful tool for designing a PML to meet a specific performance requirement. A small value of $m$ (e.g., $m=1, 2$) provides a gradual turn-on of damping, which minimizes numerical reflections from the interface itself, while a larger $\sigma_{\max}$ and thickness $L$ reduce the reflection from the layer's termination.

#### The Role of Numerical Discretization

The "perfectly matched" property is fundamentally a property of the continuous PDEs. When implemented on a numerical grid, such as in the Finite-Difference Time-Domain (FDTD) method, this perfection is generally lost [@problem_id:3335215]. The reason is **numerical dispersion and anisotropy**. The FDTD grid supports waves whose phase velocity depends on frequency and propagation direction relative to the grid axes. The PML, designed based on the isotropic continuum equations, cannot perfectly match the anisotropic numerical impedance of the grid for all angles of incidence.

This mismatch results in small, non-zero reflections at the PML interface, particularly for waves at [oblique incidence](@entry_id:267188). The reflection tends to increase with frequency and as the angle of incidence approaches grazing. However, for waves at [normal incidence](@entry_id:260681) along a grid axis, the problem becomes effectively one-dimensional, and it is possible to construct a discrete PML that is numerically perfectly matched, yielding exactly zero reflection [@problem_id:3335215].

This leads to a critical design trade-off [@problem_id:3612722]. The total reflection from a numerical PML has two main components:
1.  **Back-wall reflection ($R_b$)**: Caused by the finite thickness of the layer. This is reduced by increasing the layer thickness $L$ and/or the total integrated damping.
2.  **Discrete interface reflection ($R_d$)**: Caused by the [numerical discretization](@entry_id:752782) and the abrupt (though smooth) turn-on of the damping profile. This is reduced by using a more gradual profile (lower polynomial order $m$) and finer grid spacing $\Delta x$.

Optimizing a PML involves balancing these competing effects within a given computational budget. For instance, given a maximum number of grid cells for the layer, one must choose the polynomial order $m$ and peak damping $\sigma_{\max}$ to minimize the sum of these two reflection contributions [@problem_id:3612722].

#### Stability in Corners and Anisotropic Media

Two notorious challenges in early PML implementations were instabilities in corners and in [anisotropic media](@entry_id:260774). Modern PML formulations based on coordinate stretching have elegantly solved these issues.

In a **corner region**, where damping profiles like $\sigma_x(x)$ and $\sigma_y(y)$ are active simultaneously, the resulting wave operator from a proper coordinate-stretching formulation is purely additive. The modified Helmholtz equation, for example, takes the form $\frac{1}{s_x^2}\partial_{xx}p + \frac{1}{s_y^2}\partial_{yy}p + \dots = 0$. Critically, no mixed-derivative terms (e.g., $\partial_{xy}p$) are generated. This additive structure ensures that the corner is stable [@problem_id:3612652]. Both split-field and ADE/CPML formulations naturally preserve this additive structure.

In **[anisotropic media](@entry_id:260774)**, a naive PML can be unstable. The instability arises when the material's property tensor (e.g., the [elasticity tensor](@entry_id:170728)) and the PML's stretching tensor do not commute. This can lead to modes with negative dissipation, which grow exponentially in time [@problem_id:3612664]. A robust solution is the **Multi-Axial PML (M-PML)**, which introduces a mixing of the damping profiles. For a 2D system, the effective damping profiles are set to $\sigma'_x = \sigma_x + \eta\sigma_y$ and $\sigma'_y = \sigma_y + \eta\sigma_x$. To guarantee stability for any material orientation, the [stretch tensor](@entry_id:193200) must be made scalar, i.e., $s_x = s_y$. This condition is satisfied for any choice of base profiles $\sigma_x$ and $\sigma_y$ if and only if the mixing parameter $\eta=1$. This choice makes the effective damping in both directions equal to $\sigma_x + \sigma_y$, restoring [commutativity](@entry_id:140240) and ensuring stability.

In summary, the Perfectly Matched Layer is a powerful and theoretically elegant construct. Its foundation in [complex coordinate stretching](@entry_id:162960) provides a mechanism for near-perfect [wave absorption](@entry_id:756645). While its implementation requires careful consideration of time-domain representation, [numerical dispersion](@entry_id:145368), and stability in [complex media](@entry_id:190482), the principles outlined in this chapter provide a robust framework for designing and deploying effective PMLs in a wide range of geophysical simulations.