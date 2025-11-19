## Introduction
The [propagation of sound](@entry_id:194493) is fundamentally governed by the wave equation, a powerful but often complex mathematical description. Solving this equation directly can be computationally intensive and may obscure the intuitive physical behavior of sound, especially at high frequencies. Geometrical acoustics emerges as an elegant and powerful approximation in this high-frequency regime, simplifying the intricate patterns of wave fronts into the more tangible concept of sound energy traveling along well-defined paths, or 'rays'. This approach not only makes complex problems tractable but also provides deep physical insight into how sound interacts with its environment.

This article provides a comprehensive introduction to the theory and application of [geometrical acoustics](@entry_id:188385). We will begin in the first chapter, **Principles and Mechanisms**, by deriving the foundational eikonal and [transport equations](@entry_id:756133) directly from the wave equation, establishing the mathematical basis for [ray tracing](@entry_id:172511). We will also explore the sophisticated Hamiltonian formulation, which offers a universal framework for analyzing ray behavior in [complex media](@entry_id:190482). Following this, the second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the theory's practical power by exploring its use in explaining phenomena like acoustic lensing, sound channels in the ocean, and [noise propagation](@entry_id:266175) in moving fluids, while also highlighting surprising links to fields like geophysics and general relativity. Finally, the **Hands-On Practices** section will offer opportunities to solidify your understanding by applying these principles to solve canonical problems in [ray tracing](@entry_id:172511) and scattering.

## Principles and Mechanisms

Geometrical acoustics represents the high-frequency limit of wave theory, where the wavelength of sound is assumed to be much smaller than any [characteristic length](@entry_id:265857) scale of the medium or its boundaries. In this regime, the complex, wave-like behavior of sound can be simplified to a more intuitive picture of energy propagating along well-defined paths, or **rays**. This chapter elucidates the fundamental principles governing this approximation, from the derivation of the core equations describing ray paths and amplitudes to the exploration of their behavior in [complex media](@entry_id:190482) and the limitations of the theory itself.

### The Eikonal Equation: From Waves to Rays

The foundation of [geometrical acoustics](@entry_id:188385) is built upon a simplification of the full wave equation. For a homogeneous, quiescent medium with sound speed $c$, the propagation of the scalar [velocity potential](@entry_id:262992) $\phi(\mathbf{x}, t)$ is described by:
$$
\nabla^2 \phi - \frac{1}{c^2} \frac{\partial^2 \phi}{\partial t^2} = 0
$$
In the high-frequency limit, we anticipate that the solution will be characterized by a rapidly oscillating phase and a slowly varying amplitude. This motivates seeking a monochromatic solution of the form:
$$
\phi(\mathbf{x}, t) = A(\mathbf{x}) \exp\left[ i\omega \left(T(\mathbf{x}) - t\right) \right]
$$
where $A(\mathbf{x})$ is the slowly varying [complex amplitude](@entry_id:164138), $\omega$ is the large angular frequency, and $T(\mathbf{x})$ is the **eikonal**, a real function representing the travel time of the wave. The surfaces of constant phase, where $T(\mathbf{x})$ is constant, are known as **wavefronts**.

Substituting this ansatz into the wave equation and performing the derivatives, we find that the dominant terms are those with the highest powers of $\omega$. The Laplacian yields $\nabla^2\phi \approx -\omega^2 A (\nabla T)^2 \exp[i\omega(T-t)]$, while the time derivative gives $\partial^2\phi/\partial t^2 = -\omega^2 \phi$. In the limit $\omega \to \infty$, terms involving lower powers of $\omega$ (such as those containing $\nabla A$ or $\nabla^2 A$) become negligible. Collecting the leading-order terms ($\propto \omega^2$), the wave equation reduces to:
$$
\left[ -(\nabla T)^2 + \frac{1}{c^2} \right] A \omega^2 \exp[i\omega(T-t)] = 0
$$
For a non-[trivial solution](@entry_id:155162) ($A \neq 0$), we must have:
$$
(\nabla T)^2 = \frac{1}{c(\mathbf{x})^2}
$$
This is the celebrated **[eikonal equation](@entry_id:143913)**. It is a first-order, non-linear [partial differential equation](@entry_id:141332) that governs the spatial structure of the phase fronts. This derivation shows how the ray concept emerges directly from the wave equation in the high-frequency limit [@problem_id:547733].

It is often convenient to work with a dimensionless phase function, or eikonal, $S(\mathbf{x})$, by introducing a reference sound speed $c_0$ and defining $S = c_0 T$. In this case, the [eikonal equation](@entry_id:143913) takes the form:
$$
(\nabla S)^2 = \frac{c_0^2}{c(\mathbf{x})^2} = n^2(\mathbf{x})
$$
where $n(\mathbf{x})$ is the **refractive index** of the medium.

### The Kinematics of Rays and Wavefronts

The [eikonal equation](@entry_id:143913) provides the geometric foundation for tracing sound. A **ray** is defined as an [integral curve](@entry_id:276251) of the gradient of the eikonal, representing the path of [energy propagation](@entry_id:202589). The [unit tangent vector](@entry_id:262985) to a ray, $\mathbf{t}_r$, is therefore parallel to $\nabla S$. By definition, the [gradient of a scalar field](@entry_id:270765) is everywhere normal to the [level surfaces](@entry_id:196027) of that field. Since wavefronts are surfaces of constant $S$, it follows that **acoustic rays are everywhere orthogonal to the wavefronts** [@problem_id:547679].

This [orthogonality principle](@entry_id:195179) provides deep insight into [wave propagation](@entry_id:144063). For instance, when a wave encounters an interface between two different media, the continuity of the wavefront across the interface dictates the law of refraction. At an interface, the temporal frequency $\omega$ and the component of the [wavevector](@entry_id:178620) tangential to the boundary must be continuous. This "[phase matching](@entry_id:161268)" condition leads directly to Snell's law. In a more complex scenario, such as an interface between two fluids in uniform motion, this principle can be generalized. If a plane wave in a fluid with sound speed $c_1$ and flow velocity $\mathbf{U}_1$ is incident at an angle $\theta_i$ on a second fluid with properties $c_2$ and $\mathbf{U}_2$, the angle of refraction $\theta_r$ is governed by a modified Snell's Law derived from the continuity requirements on the Doppler-shifted dispersion relation $\omega = c|\mathbf{k}| + \mathbf{k} \cdot \mathbf{U}$. This leads to the relation [@problem_id:547721]:
$$
\sin(\theta_r) = \frac{c_2 \sin(\theta_i)}{c_1 + (U_{1, \parallel} - U_{2, \parallel}) \sin(\theta_i)}
$$
where $U_\parallel$ represents the component of fluid velocity parallel to the interface and in the plane of incidence.

### The Dynamics of Amplitude: The Transport Equation

While the [eikonal equation](@entry_id:143913) describes the *shape* of the sound field, it says nothing about its *strength*. To determine the wave amplitude, we must consider the conservation of energy. For a steady-state sound field in a non-dissipative fluid, the time-averaged acoustic [energy flux](@entry_id:266056), or intensity $\mathbf{I} = \langle p \mathbf{v} \rangle$, must have zero divergence:
$$
\nabla \cdot \mathbf{I} = 0
$$
where $p$ is the acoustic pressure and $\mathbf{v}$ is the particle velocity. Using the high-frequency approximations for $p \approx \text{Re}\{i\omega\rho_0 \phi\}$ and $\mathbf{v} \approx \text{Re}\{i\omega (\nabla T) \phi\}$, the time-averaged intensity for a real amplitude $A$ is found to be $\mathbf{I} \propto A^2 \nabla T$. Substituting this into the [energy conservation](@entry_id:146975) law yields the **transport equation**:
$$
\nabla \cdot (A^2 \nabla T) = 0 \quad \text{or equivalently} \quad \nabla \cdot (A^2 \nabla S) = 0
$$
where the amplitude $A$ and eikonal $S$ are now linked [@problem_id:547698]. This equation can be interpreted physically: the quantity $A^2 n$ is conserved along a "ray tube," a bundle of adjacent rays. As the ray tube expands or contracts, the amplitude must decrease or increase, respectively, to conserve energy flux.

This change in amplitude due to ray tube area is known as **geometrical spreading**. For a wave propagating a distance $s$ along a ray in a homogeneous medium, the amplitude varies as $A(s) = A(0) / \mathcal{J}(s)$, where $\mathcal{J}(s)$ is the geometrical spreading factor. This factor is determined by the initial curvature of the [wavefront](@entry_id:197956). If the initial principal radii of curvature are $R_1$ and $R_2$, the spreading factor is given by:
$$
\mathcal{J}(s) = \sqrt{\left(1 + \frac{s}{R_1}\right) \left(1 + \frac{s}{R_2}\right)}
$$

### The Hamiltonian Formulation of Geometrical Acoustics

A particularly powerful and general framework for describing ray propagation is provided by Hamiltonian mechanics. In this formalism, the state of a ray at any point is described by its position vector $\mathbf{x}$ and its **slowness vector** $\mathbf{p} = \nabla T$ (or, up to a constant, the wavevector $\mathbf{k} = \nabla S$). The physics of the medium is encapsulated in a **Hamiltonian** function, $H(\mathbf{x}, \mathbf{p})$, which is derived from the [dispersion relation](@entry_id:138513) of the waves. For sound in a moving, inhomogeneous medium, the Hamiltonian (which corresponds to the frequency $\omega$) is:
$$
H(\mathbf{x}, \mathbf{k}) = c(\mathbf{x})|\mathbf{k}| + \mathbf{v}(\mathbf{x}) \cdot \mathbf{k}
$$
The evolution of a ray is then governed by **Hamilton's equations**, with time $t$ or another path parameter serving as the [independent variable](@entry_id:146806):
$$
\frac{d\mathbf{x}}{dt} = \nabla_{\mathbf{k}} H, \quad \frac{d\mathbf{k}}{dt} = -\nabla_{\mathbf{x}} H
$$
The first equation defines the **group velocity** $\mathbf{c}_g = d\mathbf{x}/dt$, which is the velocity of [energy propagation](@entry_id:202589) and thus the true ray velocity. For a fluid with uniform flow $\mathbf{U}$ and sound speed $c_0$, the group velocity is found to be [@problem_id:547766]:
$$
\mathbf{c}_g = \mathbf{U} + c_0 \frac{\mathbf{k}}{|\mathbf{k}|}
$$
This shows that energy propagates with the sound speed $c_0$ relative to the moving fluid, in the direction of the wavevector $\mathbf{k}$. The second of Hamilton's equations describes how the wavevector itself evolves as it travels through an inhomogeneous medium.

The Hamiltonian framework is exceptionally useful for identifying [conserved quantities](@entry_id:148503). If the Hamiltonian does not depend on a particular coordinate (a "cyclic" coordinate), the corresponding [canonical momentum](@entry_id:155151) is conserved. For example, in a medium with [axial symmetry](@entry_id:173333) about the $x_3$-axis, the Hamiltonian is independent of the [azimuthal angle](@entry_id:164011). This symmetry implies the conservation of the axial component of angular momentum, $L_z = x_1 p_2 - x_2 p_1$, along any ray path [@problem_id:547747]. Similarly, for sound in a fluid undergoing [solid-body rotation](@entry_id:191086) $\mathbf{v} = \mathbf{\Omega} \times \mathbf{r}$ with constant sound speed $c_0$, the Hamiltonian is independent of the absolute position $\mathbf{r}$ (only depending on it through the cross product). Hamilton's equations show that $d\mathbf{k}/dt = \mathbf{\Omega} \times \mathbf{k}$. This means the wavevector $\mathbf{k}$ precesses around the rotation axis $\mathbf{\Omega}$, but its magnitude $|\mathbf{k}|$ remains constant along the ray [@problem_id:547706].

### The Domain of Validity and Key Extensions

Geometrical acoustics is a powerful approximation, but it is essential to understand its limitations.

**Caustics:** The theory breaks down at **[caustics](@entry_id:158966)**, which are surfaces or lines onto which rays focus. At a [caustic](@entry_id:164959), the cross-sectional area of a ray tube shrinks to zero, and the transport equation predicts an unphysical infinite amplitude. A classic example is the envelope of rays reflected from the inside of a circle, which forms a nephroid or [cardioid](@entry_id:162600)-shaped caustic depending on the source location [@problem_id:547693]. These are regions where a more complete wave theory, which accounts for diffraction, is required to find the true finite pressure field.

**Diffraction:** Geometrical [acoustics](@entry_id:265335) neglects diffraction, the phenomenon of waves bending around obstacles. This approximation is valid only when the wavelength is much smaller than the size of any obstacles or the scale of variations in the medium. When these scales become comparable, diffraction effects become significant and must be included.

**Attenuation:** The [ideal theory](@entry_id:184127) assumes a lossless medium. In any real fluid, dissipative effects such as viscosity and [thermal conduction](@entry_id:147831) will cause the wave amplitude to decay with distance, a process known as **attenuation**. This can be incorporated into the framework by allowing the wavenumber to be a complex quantity, $k = k_R + i\alpha$, where $\alpha$ is the attenuation coefficient. For a plane wave, the amplitude decays as $\exp(-\alpha x)$. By starting from the linearized Navier-Stokes and energy equations, and assuming dissipation is weak, one can derive the attenuation coefficient. To leading order, it is given by [@problem_id:547697]:
$$
\alpha = \frac{\omega^2}{2\rho_0c_0^3}\left( \frac{4}{3}\mu + \mu_b + \kappa\left(\frac{1}{C_v} - \frac{1}{C_p}\right) \right)
$$
where $\mu$ and $\mu_b$ are the shear and bulk viscosities, $\kappa$ is the thermal conductivity, and $C_v, C_p$ are the specific heats. This result shows that attenuation is strongly frequency-dependent (proportional to $\omega^2$) and is caused by a combination of viscous and thermal loss mechanisms.

In summary, [geometrical acoustics](@entry_id:188385) provides a robust and intuitive framework for understanding high-frequency sound propagation. It replaces the complexity of the wave equation with the simpler, more tractable problem of tracing rays. By understanding its core principles—the eikonal and [transport equations](@entry_id:756133)—and its powerful Hamiltonian formulation, one can analyze sound propagation in a vast range of complex environments, while also recognizing the boundaries where this elegant approximation must give way to a full wave treatment.