## Introduction
Forced vibrations are a ubiquitous phenomenon in engineering and science, governing the behavior of everything from bridges swaying in the wind to atoms vibrating in a crystal lattice. Understanding and predicting how a system will behave under sustained, periodic loading is critical for designing safe, reliable, and efficient structures. Harmonic response analysis is the primary analytical tool for this task, providing a powerful framework to determine the steady-state oscillatory response of a system to sinusoidal excitation. The core challenge lies in applying this theory to complex, real-world structures, which often possess intricate geometries and millions of degrees of freedom. This is the gap that the Finite Element Method (FEM) so effectively bridges, translating the continuous problem of [structural dynamics](@entry_id:172684) into a discrete, solvable mathematical model.

This article offers a comprehensive journey through the theory, application, and practice of [harmonic response analysis](@entry_id:170620). It is designed to equip you with a deep, graduate-level understanding of this essential topic. We will navigate through three distinct chapters, each building upon the last:

*   The first chapter, **Principles and Mechanisms**, establishes the theoretical bedrock. We will derive the governing equations in the frequency domain, explore the physical meaning of complex-valued results, and examine advanced concepts like [modal analysis](@entry_id:163921), non-proportional damping, and the fundamental assumptions of linearity that define the method's scope.
*   Next, in **Applications and Interdisciplinary Connections**, we will witness the theory in action. This chapter demonstrates the method's versatility by exploring its application in diverse and advanced fields, including [rotordynamics](@entry_id:163706), vibroacoustics, [fluid-structure interaction](@entry_id:171183), and even the quantum mechanical analysis of molecular and lattice vibrations.
*   Finally, the **Hands-On Practices** section provides an opportunity to solidify your knowledge through targeted computational exercises, connecting the abstract mathematical formulations to concrete numerical results.

By progressing through these sections, you will gain not only the ability to perform harmonic analysis but also the insight to interpret its results and appreciate its profound connections across multiple scientific disciplines.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the [harmonic response analysis](@entry_id:170620) of structures modeled by the Finite Element Method (FEM). We will systematically derive the governing equations in the frequency domain, explore methods of their solution, and examine the physical interpretation of the key mathematical constructs. The discussion will proceed from the foundational equations to advanced solution techniques for complex systems, culminating in a critical appraisal of the assumptions that bound the applicability of this linear analysis framework.

### The Frequency-Domain Equation of Motion

The dynamic behavior of a structural system, discretized using the Finite Element Method, is described by a system of second-order ordinary differential equations known as the semi-discrete [equations of motion](@entry_id:170720). For a linear system, this is expressed in matrix form as:

$$
\mathbf{M}\ddot{\mathbf{q}}(t) + \mathbf{C}\dot{\mathbf{q}}(t) + \mathbf{K}\mathbf{q}(t) = \mathbf{f}(t)
$$

Here, $\mathbf{q}(t)$ is the vector of nodal [generalized coordinates](@entry_id:156576) (displacements and rotations), and the superimposed dots denote differentiation with respect to time $t$. The system matrices $\mathbf{M}$, $\mathbf{C}$, and $\mathbf{K}$ represent the inertial, dissipative, and elastic properties of the structure, respectively, while $\mathbf{f}(t)$ is the vector of externally applied nodal forces.

These matrices are not arbitrary but arise systematically from the application of the [principle of virtual work](@entry_id:138749) to the underlying continuum, combined with the finite element [spatial discretization](@entry_id:172158). In this process, the continuous [displacement field](@entry_id:141476) $\mathbf{u}(\mathbf{x}, t)$ within each element is approximated by a set of shape functions $\mathbf{N}(\mathbf{x})$ and nodal coordinates $\mathbf{q}(t)$, as $\mathbf{u}(\mathbf{x}, t) \approx \mathbf{N}(\mathbf{x})\mathbf{q}(t)$. The key system matrices and the force vector are assembled from element-level contributions [@problem_id:2563517]:

- The **global [consistent mass matrix](@entry_id:174630)**, $\mathbf{M}$, represents the kinetic energy of the system. It is assembled from element matrices $\mathbf{M}^{e} = \int_{\Omega^{e}} \rho \mathbf{N}^{\mathsf{T}}\mathbf{N} \, \mathrm{d}\Omega$, where $\rho$ is the material density and $\Omega^e$ is the element volume.

- The **[global stiffness matrix](@entry_id:138630)**, $\mathbf{K}$, represents the [strain energy](@entry_id:162699) stored in the structure due to elastic deformation. It is assembled from element contributions $\mathbf{K}^{e} = \int_{\Omega^{e}} \mathbf{B}^{\mathsf{T}}\mathbf{D}\mathbf{B} \, \mathrm{d}\Omega$, where $\mathbf{D}$ is the material's elasticity tensor and $\mathbf{B}$ is the [strain-displacement matrix](@entry_id:163451) that relates strains to nodal displacements.

- The **global damping matrix**, $\mathbf{C}$, models [energy dissipation](@entry_id:147406) mechanisms. Unlike mass and stiffness, damping is often modeled phenomenologically rather than derived from first principles. It can be assembled from element-level models representing material viscosity or, more commonly, constructed at the global level. A widely used form is **proportional (Rayleigh) damping**, where $\mathbf{C}$ is assumed to be a linear combination of the [mass and stiffness matrices](@entry_id:751703): $\mathbf{C} = \alpha\mathbf{M} + \beta\mathbf{K}$, with $\alpha, \beta \ge 0$.

- The **global external force vector**, $\mathbf{f}(t)$, represents the work-equivalent nodal forces resulting from distributed body forces $\mathbf{b}(t)$ and [surface tractions](@entry_id:169207) $\bar{\mathbf{t}}(t)$. It is assembled via integrals of the form $\int_{\Omega^{e}} \mathbf{N}^{\mathsf{T}}\mathbf{b}(t) \, \mathrm{d}\Omega$ and $\int_{\Gamma_{t}^{e}} \mathbf{N}^{\mathsf{T}}\bar{\mathbf{t}}(t) \, \mathrm{d}\Gamma$.

For [harmonic response analysis](@entry_id:170620), we consider the specific case where the external forcing is sinusoidal with a single angular frequency $\omega$. It is mathematically convenient to represent such a force using complex exponential notation, $\mathbf{f}(t) = \Re\{\hat{\mathbf{f}} e^{i\omega t}\}$, where $\hat{\mathbf{f}}$ is the [complex amplitude](@entry_id:164138) (phasor) of the force vector. Due to the linearity of the system, the long-term, [steady-state response](@entry_id:173787) will also be harmonic at the same frequency, which we can write as $\mathbf{q}(t) = \Re\{\hat{\mathbf{q}} e^{i\omega t}\}$. The complex vector $\hat{\mathbf{q}}$ represents the amplitudes and phase shifts of the nodal responses relative to the force.

Substituting these complex forms into the equation of motion, we find that the time derivatives are transformed into algebraic multiplications: $\dot{\mathbf{q}}(t) \to i\omega \hat{\mathbf{q}}e^{i\omega t}$ and $\ddot{\mathbf{q}}(t) \to -\omega^2 \hat{\mathbf{q}}e^{i\omega t}$. This allows us to eliminate the time-dependent term $e^{i\omega t}$ and convert the [system of differential equations](@entry_id:262944) into a system of complex linear algebraic equations [@problem_id:2563517]:

$$
(-\omega^2 \mathbf{M} + i\omega \mathbf{C} + \mathbf{K}) \hat{\mathbf{q}} = \hat{\mathbf{f}}
$$

This equation is the cornerstone of frequency-domain [harmonic response analysis](@entry_id:170620). It allows us to solve for the [steady-state response](@entry_id:173787) amplitude $\hat{\mathbf{q}}$ at any given frequency $\omega$ by solving a single matrix system.

### Mathematical Representation of Harmonic Motion

The use of complex numbers is a powerful convenience, not a physical necessity. It is essential to understand the precise mapping between the complex formalism and the physical, real-valued motion of the structure. A general [harmonic motion](@entry_id:171819) can be expressed as a combination of cosine and sine functions, $\mathbf{u}(t) = \mathbf{A} \cos(\omega t) + \mathbf{B} \sin(\omega t)$, where $\mathbf{A}$ and $\mathbf{B}$ are real-valued amplitude vectors.

The complex exponential representation $\mathbf{u}(t) = \Re\{\hat{\mathbf{u}} e^{i\omega t}\}$ provides an equivalent description. By writing the [complex amplitude](@entry_id:164138) vector $\hat{\mathbf{u}}$ in terms of its real and imaginary parts, $\hat{\mathbf{u}} = \mathbf{u}_R + i \mathbf{u}_I$, and using Euler's identity $e^{i\omega t} = \cos(\omega t) + i\sin(\omega t)$, we can expand the expression [@problem_id:2563532]:

$$
\mathbf{u}(t) = \Re\{(\mathbf{u}_R + i \mathbf{u}_I)(\cos(\omega t) + i\sin(\omega t))\} = \Re\{(\mathbf{u}_R \cos(\omega t) - \mathbf{u}_I \sin(\omega t)) + i(...) \}
$$

$$
\mathbf{u}(t) = \mathbf{u}_R \cos(\omega t) - \mathbf{u}_I \sin(\omega t)
$$

By comparing this with the cosine-sine form, we find the direct relationship between the components of the complex phasor and the real-valued amplitudes:

$$
\mathbf{A} = \mathbf{u}_R = \Re\{\hat{\mathbf{u}}\} \quad \text{and} \quad \mathbf{B} = -\mathbf{u}_I = -\Im\{\hat{\mathbf{u}}\}
$$

This shows that the real part of the [complex amplitude](@entry_id:164138), $\Re\{\hat{\mathbf{u}}\}$, corresponds to the component of the response that is in-phase with a pure cosine force, while the imaginary part, $\Im\{\hat{\mathbf{u}}\}$, corresponds to the out-of-phase (quadrature) component. Note that the sign convention depends on the choice of the time-harmonic term; if $e^{-i\omega t}$ were used, the relation for $\mathbf{B}$ would become $\mathbf{B} = \Im\{\hat{\mathbf{u}}\}$.

Alternatively, each component of the [complex amplitude](@entry_id:164138) $\hat{u}_j$ can be expressed in [polar form](@entry_id:168412), $\hat{u}_j = |\hat{u}_j| e^{i\theta_j}$. The physical meaning becomes immediately apparent [@problem_id:2563532]:

$$
u_j(t) = \Re\{|\hat{u}_j| e^{i\theta_j} e^{i\omega t}\} = \Re\{|\hat{u}_j| e^{i(\omega t + \theta_j)}\} = |\hat{u}_j| \cos(\omega t + \theta_j)
$$

Thus, the **magnitude** $|\hat{u}_j|$ is the physical amplitude of the oscillation for the $j$-th degree of freedom, and the **argument** $\theta_j$ is the [phase angle](@entry_id:274491), representing the lead or lag of the displacement relative to the reference cosine function.

### Dynamic Stiffness and Frequency Response Functions

The algebraic system derived previously can be written more compactly as:

$$
\mathbf{Z}(\omega) \hat{\mathbf{q}} = \hat{\mathbf{f}}
$$

where the matrix $\mathbf{Z}(\omega) = \mathbf{K} + i\omega\mathbf{C} - \omega^2\mathbf{M}$ is known as the **[dynamic stiffness](@entry_id:163760) matrix** [@problem_id:2563500]. It is a complex-valued, frequency-dependent matrix that encapsulates the entire linear dynamic character of the structure at a given frequency $\omega$. Its real part, $\mathbf{K} - \omega^2\mathbf{M}$, represents the conservative elastic and [inertial forces](@entry_id:169104), while its imaginary part, $\omega\mathbf{C}$, represents the [dissipative forces](@entry_id:166970). For systems with symmetric $\mathbf{M}$, $\mathbf{C}$, and $\mathbf{K}$ matrices, the [dynamic stiffness](@entry_id:163760) matrix $\mathbf{Z}(\omega)$ is also symmetric, which has important consequences for reciprocity.

The inverse of the [dynamic stiffness](@entry_id:163760) matrix, $\mathbf{H}(\omega) = \mathbf{Z}(\omega)^{-1}$, is arguably even more important in practice. This matrix is known as the **receptance matrix** or **dynamic [compliance matrix](@entry_id:185679)**, and it directly relates the displacement response to the applied force: $\hat{\mathbf{q}} = \mathbf{H}(\omega) \hat{\mathbf{f}}$. The entries $H_{jk}(\omega)$ of this matrix are scalar **Frequency Response Functions (FRFs)** that give the displacement amplitude at degree of freedom $j$ due to a unit harmonic force applied at degree of freedom $k$.

Depending on the motion quantity of interest (displacement, velocity, or acceleration), different types of FRFs are defined [@problem_id:2563541]:

- **Receptance** ($H_{uu}(\omega)$): The complex ratio of displacement to force, $\hat{u} = H_{uu}(\omega) \hat{f}$. Its SI units are $\mathrm{m/N}$. It is most sensitive to [system dynamics](@entry_id:136288) near the natural frequencies.

- **Mobility** ($H_{uv}(\omega)$): The complex ratio of velocity to force, $\hat{v} = H_{uv}(\omega) \hat{f}$. Since $\hat{v} = i\omega \hat{u}$, it follows directly that $H_{uv}(\omega) = i\omega H_{uu}(\omega)$. Its SI units are $\mathrm{m/(N \cdot s)}$. Mobility plots are often used in experimental [modal analysis](@entry_id:163921) as they tend to balance the contributions of different modes across the [frequency spectrum](@entry_id:276824).

- **Accelerance** or **Inertance** ($H_{ua}(\omega)$): The complex ratio of acceleration to force, $\hat{a} = H_{ua}(\omega) \hat{f}$. Since $\hat{a} = -\omega^2 \hat{u}$, it follows that $H_{ua}(\omega) = -\omega^2 H_{uu}(\omega)$. Its SI units are $\mathrm{m/(N \cdot s^2)}$.

The behavior of these FRFs as a function of frequency reveals the system's character. At very low frequencies ($\omega \to 0$), the response is dominated by stiffness, and the receptance matrix approaches the inverse of the static [stiffness matrix](@entry_id:178659), $\mathbf{H}(\omega) \approx \mathbf{K}^{-1}$. Conversely, at very high frequencies ($\omega \to \infty$), the response is dominated by inertia. The [dynamic stiffness](@entry_id:163760) matrix is asymptotically dominated by the mass term, $\mathbf{Z}(\omega) \sim -\omega^2\mathbf{M}$, and the receptance behaves as $\mathbf{H}(\omega) \sim -\omega^{-2}\mathbf{M}^{-1}$ [@problem_id:2563500]. Near the system's [natural frequencies](@entry_id:174472), the magnitude of the receptance exhibits sharp peaks, a phenomenon known as resonance, where a small force can produce a large response.

### Modal Analysis for Decoupling the Response

Solving the full $n \times n$ complex algebraic system at many frequency points can be computationally expensive for large models. **Modal analysis** provides a powerful and insightful alternative by transforming the problem into a smaller, simpler basis. The foundation of this method is the undamped free-vibration eigenvalue problem [@problem_id:2563545]:

$$
\mathbf{K}\boldsymbol{\phi}_r = \omega_r^2 \mathbf{M}\boldsymbol{\phi}_r
$$

The solutions to this problem are a set of $n$ eigenvalues $\omega_r^2$ and corresponding eigenvectors $\boldsymbol{\phi}_r$. The square roots $\omega_r$ are the **natural frequencies** of the system, and the eigenvectors $\boldsymbol{\phi}_r$ are the **[mode shapes](@entry_id:179030)**, representing the characteristic patterns of vibration. These mode shapes form a basis that possesses a crucial [orthogonality property](@entry_id:268007) with respect to both the [mass and stiffness matrices](@entry_id:751703). By scaling each [mode shape](@entry_id:168080) appropriately (a process called **mass-normalization**), we can achieve the following elegant relationships:

$$
\boldsymbol{\phi}_r^{\mathsf{T}}\mathbf{M}\boldsymbol{\phi}_s = \delta_{rs} \quad (\text{mass orthogonality})
$$

$$
\boldsymbol{\phi}_r^{\mathsf{T}}\mathbf{K}\boldsymbol{\phi}_s = \omega_r^2 \delta_{rs} \quad (\text{stiffness orthogonality})
$$

where $\delta_{rs}$ is the Kronecker delta (1 if $r=s$, 0 otherwise).

We can express the physical [displacement vector](@entry_id:262782) $\hat{\mathbf{q}}$ as a [linear combination](@entry_id:155091) of these [mode shapes](@entry_id:179030), $\hat{\mathbf{q}} = \sum_{r=1}^n \hat{\eta}_r \boldsymbol{\phi}_r$, where $\hat{\eta}_r$ are the complex modal coordinates. If the damping matrix $\mathbf{C}$ is proportional (i.e., of the form $\mathbf{C} = \alpha\mathbf{M} + \beta\mathbf{K}$), it shares the same [orthogonality property](@entry_id:268007): $\boldsymbol{\phi}_r^{\mathsf{T}}\mathbf{C}\boldsymbol{\phi}_s = ( \alpha + \beta\omega_r^2 ) \delta_{rs} = 2\zeta_r\omega_r\delta_{rs}$, where $\zeta_r$ is the [modal damping ratio](@entry_id:162799) for mode $r$.

Under this condition of proportional damping, substituting the modal expansion into the frequency-domain [equation of motion](@entry_id:264286) and pre-multiplying by a [mode shape](@entry_id:168080) $\boldsymbol{\phi}_r^{\mathsf{T}}$ causes all terms with $s \neq r$ to vanish. The large, coupled system of $n$ equations reduces to $n$ independent scalar equations, one for each mode [@problem_id:2563545]:

$$
(\omega_r^2 - \omega^2 + i 2\zeta_r\omega_r\omega) \hat{\eta}_r = \boldsymbol{\phi}_r^{\mathsf{T}}\hat{\mathbf{f}}
$$

The term on the right-hand side, $\Gamma_r = \boldsymbol{\phi}_r^{\mathsf{T}}\hat{\mathbf{f}}$, is the **modal force** [@problem_id:2563552]. It represents the [generalized force](@entry_id:175048) for mode $r$ and quantifies how effectively the spatial distribution of the applied force vector $\hat{\mathbf{f}}$ excites that particular [mode shape](@entry_id:168080). If the force distribution is orthogonal to a [mode shape](@entry_id:168080) ($\Gamma_r = 0$), that mode will not participate in the response, regardless of how close the driving frequency is to its natural frequency. The amplitude of each modal coordinate can be solved for trivially:

$$
\hat{\eta}_r = \frac{\Gamma_r}{\omega_r^2 - \omega^2 + i 2\zeta_r\omega_r\omega}
$$

The final physical response is then reconstructed by summing the contributions from each mode: $\hat{\mathbf{q}} = \sum_{r=1}^n \hat{\eta}_r \boldsymbol{\phi}_r$. This [modal superposition](@entry_id:175774) method is not only computationally efficient (especially when the response is dominated by a few modes) but also provides profound physical insight into how the structure responds as a combination of its fundamental vibration patterns.

### The Challenge of Non-Proportional Damping and the State-Space Formulation

The elegant [decoupling](@entry_id:160890) achieved through classical [modal analysis](@entry_id:163921) hinges on the assumption that the damping matrix $\mathbf{C}$ is simultaneously diagonalized by the undamped [mode shapes](@entry_id:179030). This is true for proportional damping but fails for a general, **non-proportionally damped** system, where damping might arise from localized dashpots or interactions between materials with different dissipative properties. In such cases, the transformed modal damping matrix $\boldsymbol{\Phi}^{\mathsf{T}}\mathbf{C}\boldsymbol{\Phi}$ is not diagonal, and the modal equations remain coupled, defeating the purpose of the transformation [@problem_id:2563524].

To properly decouple a non-proportionally damped system, a more general approach is required. This is achieved by recasting the [second-order system](@entry_id:262182) into a first-order **[state-space representation](@entry_id:147149)**. We define a [state vector](@entry_id:154607) of size $2n$ that includes both displacements and velocities: $\mathbf{z}(t) = \begin{pmatrix} \mathbf{q}(t) \\ \dot{\mathbf{q}}(t) \end{pmatrix}$. The governing equation then becomes:

$$
\dot{\mathbf{z}}(t) = \mathbf{A}\mathbf{z}(t) + \mathbf{F}(t) \quad \text{where} \quad \mathbf{A} = \begin{bmatrix} \mathbf{0} & \mathbf{I} \\ -\mathbf{M}^{-1}\mathbf{K} & -\mathbf{M}^{-1}\mathbf{C} \end{bmatrix}
$$

The dynamics are now governed by the properties of the $2n \times 2n$ state matrix $\mathbf{A}$, which is generally real but non-symmetric. Its eigenvalue problem, $\mathbf{A}\mathbf{v}_j = s_j\mathbf{v}_j$, yields $2n$ [complex eigenvalues](@entry_id:156384) $s_j$ and $2n$ [complex eigenvectors](@entry_id:155846) $\mathbf{v}_j$. These [eigenvalues and eigenvectors](@entry_id:138808) completely characterize the system's damped behavior.

This [state-space](@entry_id:177074) eigenproblem provides the basis for a true [decoupling](@entry_id:160890). The set of right eigenvectors $\mathbf{V}$ and a corresponding set of left eigenvectors $\mathbf{W}$ can be used to transform the [state vector](@entry_id:154607), $\mathbf{z}(t) = \mathbf{V}\boldsymbol{\eta}(t)$, leading to a fully decoupled set of $2n$ first-order scalar equations for the [state-space](@entry_id:177074) modal coordinates $\eta_j(t)$. The harmonic response can then be computed for each state-space mode independently and superimposed to find the final physical response. This method is universally applicable to any [linear time-invariant system](@entry_id:271030), albeit at the cost of solving a larger, complex-valued eigenproblem.

### Advanced Damping Models and Solution Characteristics

While [viscous damping](@entry_id:168972) is mathematically convenient, other models may better represent the physical reality of [energy dissipation](@entry_id:147406) in structures. One common alternative is **[hysteretic damping](@entry_id:750492)**, also known as structural damping. This model posits that the energy loss per cycle of vibration is independent of frequency, a behavior observed in many built-up structures. In the frequency domain, this is modeled by introducing a complex [stiffness matrix](@entry_id:178659) [@problem_id:2563534]:

$$
\tilde{\mathbf{K}} = \mathbf{K}(1 + i\eta)
$$

Here, $\eta$ is the **hysteretic loss factor**, which is directly related to the fraction of energy dissipated per cycle. The governing equation becomes $(\mathbf{K}(1+i\eta) - \omega^2\mathbf{M})\hat{\mathbf{q}} = \hat{\mathbf{f}}$. This can be seen as equivalent to a [viscous damping](@entry_id:168972) model where the damping matrix is frequency-dependent: $\mathbf{C}_{eq}(\omega) = (\eta/\omega)\mathbf{K}$. A key feature of [hysteretic damping](@entry_id:750492) is that the peak of the response amplitude occurs exactly at the [undamped natural frequency](@entry_id:261839), unlike [viscous damping](@entry_id:168972) which shifts the peak slightly.

Finally, it is crucial to distinguish between the two components of a [forced vibration](@entry_id:167113) solution: the transient response and the [steady-state response](@entry_id:173787). The full solution to the equation of motion is a sum of the [homogeneous solution](@entry_id:274365) (the transient part, which depends on [initial conditions](@entry_id:152863)) and a [particular solution](@entry_id:149080) (the steady-state part, which depends on the forcing). In any physical system with [energy dissipation](@entry_id:147406) ($\mathbf{C} \succeq \mathbf{0}$ and other conditions ensuring all modes are damped), the total mechanical energy of the free system is a non-increasing function of time, as its rate of change is $\dot{E} = -\dot{\mathbf{q}}^{\mathsf{T}}\mathbf{C}\dot{\mathbf{q}} \le 0$ [@problem_id:2563519]. This ensures that the transient response decays to zero over time, leaving only the persistent, [steady-state response](@entry_id:173787) that oscillates at the driving frequency $\omega$. The algebraic frequency-domain method, by its construction, is designed to find only this steady-state particular solution and implicitly assumes that sufficient time has passed for the transient effects to become negligible.

### The Domain of Validity for Linear Harmonic Analysis

The entire framework of linear [harmonic response analysis](@entry_id:170620) rests upon a set of critical assumptions that simplify the general, nonlinear [equations of motion](@entry_id:170720) into the constant-coefficient, linear time-invariant (LTI) form. It is essential for the analyst to be aware of these assumptions and the physical situations where they are violated [@problem_id:2563514].

The LTI model is valid under the following conditions:
1.  **Small Deformations**: Displacements and, more importantly, rotations must be small enough that the geometry of the structure does not change significantly. This linearizes the [strain-displacement relations](@entry_id:173321) and allows the stiffness matrix $\mathbf{K}$ to be treated as constant. If rotations are large, **[geometric nonlinearity](@entry_id:169896)** occurs, making $\mathbf{K}$ a function of the displacement $\mathbf{q}$.
2.  **Linear Elastic Material**: The material's stress-strain relationship must be linear (obeying Hooke's Law), and its properties must not change with deformation or time.
3.  **Linear Damping**: All dissipative effects must be adequately represented by a constant, linear damping matrix $\mathbf{C}$.
4.  **Time-Invariant Boundary Conditions and Loads**: The supports must be fixed, and the direction of applied forces must not depend on the structure's deformation. Loads like wind or pressure that act normal to a surface and rotate with it are known as **[follower forces](@entry_id:174748)** and introduce displacement-dependent terms that invalidate the LTI model.

Situations that violate these assumptions and require more advanced, [nonlinear analysis](@entry_id:168236) methods include:
-   **Large Rotations or Strains**: Common in flexible structures like cables, membranes, or slender beams under significant load.
-   **Contact and Friction**: The opening and closing of gaps (**[unilateral contact](@entry_id:756326)**) or the [stick-slip behavior](@entry_id:755445) of frictional interfaces introduces abrupt, highly nonlinear changes to the system's stiffness. A [harmonic response analysis](@entry_id:170620) cannot capture these phenomena.
-   **Nonlinear Materials**: Materials exhibiting plasticity, damage, or [hyperelasticity](@entry_id:168357) have a state-dependent stiffness that renders the system nonlinear.

Therefore, while [harmonic response analysis](@entry_id:170620) is a powerful and efficient tool, its application must be guided by a careful assessment of the physical problem to ensure that the idealizations of linearity and time-invariance provide a sufficiently accurate representation of reality.