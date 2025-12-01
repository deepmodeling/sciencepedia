## Introduction
Electrical Impedance Tomography (EIT) is a [non-invasive imaging](@entry_id:166153) modality that offers a unique window into the electrical properties of a body, providing functional information without the use of [ionizing radiation](@entry_id:149143). Its ability to monitor dynamic processes in real-time has made it particularly significant in fields like clinical medicine for tracking physiological changes. However, appreciating the power and limitations of EIT requires a deep understanding that bridges fundamental physics, complex mathematics, and practical application—a gap this article aims to fill. This text will guide you through the foundational concepts of EIT. We will begin with the "Principles and Mechanisms," where we derive the governing equations from first principles, explore realistic electrode models, and define the challenging inverse problem of [image reconstruction](@entry_id:166790). Following this, the "Applications and Interdisciplinary Connections" section will showcase EIT's versatility, from bedside respiratory monitoring to industrial process control and its role as a canonical problem in applied mathematics. Finally, the "Hands-On Practices" section provides a set of problems designed to solidify your understanding of the practical and theoretical challenges in EIT measurement and modeling.

## Principles and Mechanisms

This section delves into the fundamental principles and mechanisms that govern Electrical Impedance Tomography (EIT). We will derive the governing mathematical models from first physical principles, explore the intricacies of the electrode-tissue interface, and define the [forward problem](@entry_id:749531). Subsequently, we will formulate the inverse problem of image reconstruction, analyze its inherent mathematical challenges, and discuss practical strategies, such as time-difference and multifrequency imaging, that have enabled EIT to become a valuable monitoring tool.

### The Governing Equations of Electrostatics

The physical basis of EIT lies in the behavior of electric currents in a conductive medium at low frequencies. In this quasi-static regime, the time-varying components of the electromagnetic fields are negligible, allowing us to simplify Maxwell's equations. The foundational principles are the conservation of electric charge and Ohm's law.

In a steady state or quasi-static condition, where there is no net accumulation or depletion of charge at any point within the conductive body, the divergence of the current density vector $\mathbf{J}$ must be zero. This is the law of charge conservation:

$$ \nabla \cdot \mathbf{J} = 0 $$

This equation holds throughout the conductive domain, which we will denote as $\Omega$. The current density $\mathbf{J}$ itself is related to the electric field $\mathbf{E}$ via Ohm's law. For a simple [isotropic material](@entry_id:204616), this relationship is linear, characterized by a scalar conductivity $\gamma$:

$$ \mathbf{J} = \gamma \mathbf{E} $$

The conductivity $\gamma$, measured in Siemens per meter (S/m), is a property of the tissue that we aim to map.

The [quasi-static approximation](@entry_id:167818) also implies that the electric field is irrotational, i.e., its curl is zero ($\nabla \times \mathbf{E} = \mathbf{0}$). This property allows the electric field to be expressed as the negative gradient of a scalar electric potential, $u$:

$$ \mathbf{E} = -\nabla u $$

By combining these three fundamental relationships, we can derive a single governing partial differential equation (PDE) for the electric potential $u$ within the domain $\Omega$. Substituting the potential definition into Ohm's law gives $\mathbf{J} = -\gamma \nabla u$. Inserting this into the [charge conservation](@entry_id:151839) equation yields:

$$ \nabla \cdot (\gamma \nabla u) = 0 $$

This second-order elliptic partial differential equation is the cornerstone of the EIT [forward problem](@entry_id:749531). Given a known conductivity distribution $\gamma(\mathbf{x})$ and a set of applied currents on the boundary $\partial\Omega$, solving this equation provides the electric potential field $u(\mathbf{x})$ throughout the body [@problem_id:4881450].

The problem is completed by specifying boundary conditions. In the simplest conceptualization, known as the continuum model, one prescribes the normal component of the current density, $q$, on the parts of the boundary where electrodes are attached, $\Gamma_{e,k}$. On the insulating parts of the boundary, $\Gamma_n$, no current can flow, so the normal component of the current density is zero. This leads to mixed (Neumann-type) boundary conditions:

$$ \gamma \frac{\partial u}{\partial \mathbf{n}} = q \quad \text{on } \Gamma_{e,k} $$
$$ \frac{\partial u}{\partial \mathbf{n}} = 0 \quad \text{on } \Gamma_{n} $$

Here, $\frac{\partial u}{\partial \mathbf{n}}$ denotes the outward [normal derivative](@entry_id:169511) of the potential. For a solution to exist, the total current injected into the body must equal the total current withdrawn, which is a physical manifestation of overall charge conservation: $\int_{\partial\Omega} q \, ds = 0$. Under these pure Neumann conditions, the potential $u$ is only determined up to an arbitrary additive constant. A unique solution is obtained by imposing an additional constraint, such as setting the potential at one point to zero or enforcing a zero average potential over the boundary [@problem_id:4881450].

### Modeling the Electrode-Tissue Interface: The Complete Electrode Model

While the continuum model is instructive, it fails to capture two critical real-world phenomena: the finite size of electrodes and the electrochemical effects at the electrode-skin or electrode-tissue interface. This interface forms a thin layer with its own impedance, known as **contact impedance**, which can be significantly large and can cause a substantial potential drop between the electrode and the tissue.

A more accurate and widely used model is the **Complete Electrode Model (CEM)**, which explicitly accounts for these effects. The CEM replaces the continuum boundary conditions with a more sophisticated set that applies to discrete electrode regions $\{E_\ell\}_{\ell=1}^L$ [@problem_id:4881505].

1.  **Equipotential Electrodes and Contact Impedance:** Metallic electrodes are excellent conductors. It is therefore assumed that each electrode is an [equipotential surface](@entry_id:263718), having a constant potential $U_\ell$. The potential drop across the contact impedance layer between the electrode and the tissue is modeled as being proportional to the normal current density flowing through it. This gives rise to a Robin-type boundary condition on each electrode surface $E_\ell$:
    $$ u + z_\ell \gamma \frac{\partial u}{\partial \mathbf{n}} = U_\ell \quad \text{on } E_\ell $$
    Here, $z_\ell$ is the **specific contact impedance** (units of $\Omega \cdot \text{m}^2$) of the $\ell$-th electrode. This equation elegantly links the tissue potential $u$ at the boundary, the normal current density flowing into the tissue ($\gamma \frac{\partial u}{\partial \mathbf{n}}$), and the constant [electrode potential](@entry_id:158928) $U_\ell$.

2.  **Insulating Boundary:** On the portions of the boundary between electrodes, the surface is assumed to be electrically insulating. As in the simpler model, this means no current can pass through, leading to a homogeneous Neumann condition:
    $$ \gamma \frac{\partial u}{\partial \mathbf{n}} = 0 \quad \text{on } \partial\Omega \setminus \bigcup_{\ell=1}^L E_\ell $$

3.  **Current Enforcement:** The known applied currents, $I_\ell$, are enforced as integral constraints. The total current injected into the domain through electrode $E_\ell$ must be equal to the integral of the normal current density over the electrode's surface:
    $$ \int_{E_\ell} \gamma \frac{\partial u}{\partial \mathbf{n}} \, ds = I_\ell $$
    As before, global [charge conservation](@entry_id:151839) requires that the sum of all applied currents is zero: $\sum_{\ell=1}^L I_\ell = 0$.

4.  **Grounding:** The full system of equations in the CEM still determines the potentials only up to an additive constant. To ensure a unique solution, a reference, or "ground," must be established. This is typically done by setting one of the electrode potentials to zero (e.g., $U_L = 0$) or by requiring the sum of all electrode potentials to be zero ($\sum_{\ell=1}^L U_\ell = 0$) [@problem_id:4881505]. The CEM provides a robust and physically realistic [forward model](@entry_id:148443) that is the foundation of modern EIT systems.

### Generalizations of the Conductivity Model

The scalar, frequency-independent conductivity model $\gamma(\mathbf{x})$ is a simplification. Biological tissues exhibit more complex electrical properties, motivating extensions to the model.

#### Anisotropic Conductivity

Many biological tissues, such as skeletal muscle, heart muscle, and white matter in the brain, have a fibrous structure. Electrical current flows more easily along these fibers than across them. This property is known as **anisotropy**. To model this, the scalar conductivity $\gamma$ is replaced by a **[conductivity tensor](@entry_id:155827)**, a $3 \times 3$ [symmetric positive definite](@entry_id:139466) (SPD) matrix $\boldsymbol{\sigma}(\mathbf{x})$ [@problem_id:4881457].

Ohm's law becomes a [matrix-vector product](@entry_id:151002):

$$ \mathbf{J} = -\boldsymbol{\sigma} \nabla u $$

And the governing PDE is modified to:

$$ \nabla \cdot (\boldsymbol{\sigma} \nabla u) = 0 $$

A key physical consequence of anisotropy is that the current density vector $\mathbf{J}$ is generally **not** parallel to the electric field vector $\mathbf{E} = -\nabla u$. The conductivity tensor $\boldsymbol{\sigma}$ rotates the electric field vector to produce the current density vector, directing current preferentially along the directions of highest conductivity (the principal axes of the tensor) [@problem_id:4881457]. Accounting for anisotropy is crucial for accurate modeling in certain applications, though it significantly complicates the inverse problem as one must recover a tensor field instead of a scalar field.

#### Frequency-Dependent Admittivity

Biological tissues are not pure resistors; they also have capacitive properties due to cell membranes and other structures. This means their impedance changes with the frequency of the applied current. This effect is captured by modeling the conductivity as a complex-valued, frequency-dependent **admittivity**, $\gamma(\mathbf{x}, \omega)$. A common model is:

$$ \gamma(\mathbf{x}, \omega) = \sigma(\mathbf{x}) + i\omega \epsilon(\mathbf{x}) $$

Here, $\sigma(\mathbf{x})$ is the static conductivity, $\epsilon(\mathbf{x})$ is the electrical permittivity, $\omega$ is the angular frequency of the applied current, and $i$ is the imaginary unit. With this model, the electric potential $u$ and the measured voltages become complex-valued. This technique, known as **multifrequency EIT** or **electrical [impedance spectroscopy](@entry_id:195498) (EIS)**, allows for the separation of conductivity and permittivity effects, providing richer information about tissue composition and physiological state [@problem_id:4881462].

### The Inverse Problem and Linearization

The ultimate goal of EIT is to solve the **inverse problem**: to reconstruct the [spatial distribution](@entry_id:188271) of conductivity $\gamma(\mathbf{x})$ (or $\boldsymbol{\sigma}(\mathbf{x})$, or the pair $(\sigma(\mathbf{x}), \epsilon(\mathbf{x}))$) from measurements of currents and voltages made on the boundary.

The relationship, or **forward map**, between the interior conductivity and the boundary voltages is non-linear. The conductivity $\gamma$ multiplies the term $\nabla u$ in the governing PDE, meaning the solution $u$ (and thus the measured voltages) depends on $\gamma$ in a complex, non-linear way. Solving the full non-linear inverse problem is computationally demanding and often unstable.

A more common approach is to **linearize** the problem. This is particularly effective when imaging small changes in conductivity relative to a known or assumed baseline. This is the foundation for most dynamic EIT applications, such as lung function monitoring, where one images the change in conductivity due to breathing against the relatively static background of the torso.

Let's assume the true conductivity $\gamma$ is a small perturbation $\delta\gamma$ from a known background conductivity $\gamma_0$: $\gamma = \gamma_0 + \delta\gamma$. The resulting voltage measurements $\mathbf{U}$ will be a small perturbation $\delta\mathbf{U}$ from the baseline voltages $\mathbf{U}_0$. The linearized relationship is given by:

$$ \delta\mathbf{U} \approx \mathbf{J} \delta\boldsymbol{\gamma} $$

Here, $\delta\boldsymbol{\gamma}$ is a vector representing the discretized conductivity change over a grid of pixels or voxels, and $\mathbf{J}$ is the **Jacobian** or **sensitivity matrix** [@problem_id:4881507]. The entry $J_{\ell n}$ of this matrix quantifies how much the $\ell$-th voltage measurement changes in response to a small change in conductivity in the $n$-th pixel of the image.

The entries of the sensitivity matrix can be derived using perturbation theory and [adjoint methods](@entry_id:182748). The sensitivity of a measurement to a conductivity change in a region is proportional to the interaction of the electric fields that would be generated by the applied current pattern and the "adjoint" current pattern corresponding to the voltage measurement itself. Specifically, for a change $\delta\gamma$ in a small region $\Delta_n$, the change in the $\ell$-th voltage measurement is given by:

$$ \delta U_\ell \approx - \int_{\Delta_n} \nabla u^0_{\text{f},\ell} \cdot \nabla u^0_{\text{a},\ell} \, \delta\gamma(\mathbf{x}) \, d\mathbf{x} $$

Here, $u^0_{\text{f},\ell}$ is the background potential field produced by the current pattern used for the measurement, and $u^0_{\text{a},\ell}$ is the background potential field produced by applying a "reciprocal" current pattern corresponding to the voltage measurement leads. The sensitivity is thus highest in regions where both the driving and measuring electric fields are strong and aligned [@problem_id:4881507] [@problem_id:4881511]. For [anisotropic media](@entry_id:260774), this generalizes to an expression involving the tensor perturbation $\delta\boldsymbol{\sigma}$: $\delta Z_{12} \propto \int_V (\nabla u_1)^T \delta\boldsymbol{\sigma} (\nabla u_2) \, dV$ [@problem_id:4881457].

### The Ill-Posed Nature of EIT

The inverse problem of EIT is notoriously **ill-posed**. This means that the solution is highly sensitive to noise and errors in the measurements; a very small change in the measured voltages can lead to a very large, unphysical change in the reconstructed conductivity image.

This ill-posedness is a direct consequence of the physics. The governing elliptic PDE, $\nabla \cdot (\gamma \nabla u) = 0$, is a smoothing operator. Current injected at the boundary spreads out within the body, and the resulting potential distribution on the boundary is a smoothed-out representation of the interior conductivity. Fine details and high-spatial-frequency variations in conductivity deep inside the body have a very weak, almost imperceptible effect on the boundary measurements [@problem_id:4881518]. Reversing this process—trying to recover fine details from smooth boundary data—is inherently unstable.

In the context of the linearized problem $\delta\mathbf{U} = \mathbf{J} \delta\boldsymbol{\gamma}$, this [ill-posedness](@entry_id:635673) manifests in the properties of the Jacobian matrix $\mathbf{J}$:

1.  **Dense Matrix:** A change in conductivity in any single pixel within the body affects the global potential field, and thus influences *all* voltage measurements on the boundary. Consequently, the Jacobian matrix $\mathbf{J}$ is **dense**, with no zero entries [@problem_id:4881511].

2.  **Ill-Conditioning:** The singular values of $\mathbf{J}$, which represent the amplification factors from conductivity changes to voltage changes, decay to zero very rapidly. This means that conductivity variations corresponding to the smaller singular values (typically high-frequency spatial variations) are extremely difficult to detect. The condition number of the matrix (the ratio of the largest to the smallest [singular value](@entry_id:171660)) is enormous, making direct inversion impossible.

3.  **Logarithmic Stability:** The [ill-posedness](@entry_id:635673) is so severe that the best-available stability estimates for the full non-linear problem are of a **logarithmic type**. This means that the error in the reconstructed image decreases only as a negative power of the logarithm of the data [signal-to-noise ratio](@entry_id:271196). In practice, to halve the error in the image, one might need to reduce the measurement noise by many orders of magnitude. This is in stark contrast to mildly [ill-posed problems](@entry_id:182873) (like X-ray CT) which enjoy better, algebraic stability [@problem_id:4881486]. For a discrete system, this translates to the number of reliably recoverable features growing only as $\log(1/\epsilon)$, where $\epsilon$ is the noise level [@problem_id:4881486].

The number of electrodes, $L$, and the number of independent current patterns, $M$, influence the quality of the data. Increasing $L$ and $M$ (up to its maximum of $L-1$) provides more independent measurements and increases the rank of the Jacobian. However, it does not change the fundamental physics of smoothing, and thus the rapid decay of the singular values persists. The problem remains severely ill-posed, although resolution, particularly near the boundary, can be improved [@problem_id:4881518]. Similarly, using current patterns that penetrate deeper into the object, such as an "opposite" drive pattern (current injected and withdrawn at opposite electrodes) rather than an "adjacent" pattern, can improve the conditioning of the Jacobian and provide better sensitivity to central regions [@problem_id:4881484] [@problem_id:4881511].

### Practical Approaches: Difference and Multifrequency Imaging

Given the severe ill-posedness of the absolute imaging problem, practical EIT has relied heavily on clever strategies that reframe the problem to be more tractable.

#### Time-Difference EIT

The most successful clinical application of EIT is for continuous monitoring of physiological processes, such as lung ventilation or gastric emptying. This is accomplished through **time-difference EIT**. Instead of trying to reconstruct the absolute conductivity distribution $\gamma(\mathbf{x})$, one reconstructs the *change* in conductivity, $\delta\gamma(\mathbf{x}, t)$, over time relative to a baseline measurement.

The power of this approach is its remarkable ability to mitigate modeling errors. In a real-world setting, there are always mismatches between the computational model and the physical subject, such as uncertainties in the exact shape of the torso, the precise location of the electrodes, and the values of the contact impedances. These static, time-invariant errors can create enormous artifacts in an absolute image.

In difference imaging, we work with the difference in voltage measurements over time: $\delta\mathbf{U}(t) = \mathbf{U}(t) - \mathbf{U}_0$. A Taylor [series expansion](@entry_id:142878) of the forward map shows that the contributions of time-invariant modeling errors to the voltage measurements cancel out to first order when this subtraction is performed. The dominant error terms in an absolute reconstruction are eliminated, leaving behind only much smaller, second-order error terms [@problem_id:4881510]. The resulting linearized problem, $\delta\mathbf{U}(t) \approx \mathbf{J} \delta\boldsymbol{\gamma}(t)$, becomes much more robust and accurately relates the measured voltage changes to the underlying conductivity changes, enabling reliable imaging of dynamic processes [@problem_id:4881510].

#### Multifrequency EIT

Building upon the framework of linearization and difference imaging, multifrequency EIT leverages the frequency-dependent nature of tissue admittivity, $\gamma(\omega) = \sigma + i\omega\epsilon$. By taking measurements at multiple frequencies, we can aim to separate changes in conductivity $\delta\sigma$ from changes in permittivity $\delta\epsilon$.

The linearized problem at a single frequency $\omega$ relates the complex voltage change $\delta v(\omega)$ to the perturbations $\delta\sigma$ and $\delta\epsilon$:

$$ \delta v(\omega) \approx J_\gamma(\omega) (\delta\sigma + i\omega\delta\epsilon) $$

where $J_\gamma(\omega)$ is the complex-valued Jacobian. By separating this equation into its real and imaginary parts, we can construct a real-valued linear system that relates the real and imaginary parts of the voltage measurements to the unknown real-valued changes in conductivity and permittivity. Stacking these systems for multiple frequencies $\omega_1, \dots, \omega_M$ creates a larger, more constrained inverse problem [@problem_id:4881462]. Although still ill-posed, this approach allows for the reconstruction of spectroscopic information, which can be used to differentiate tissue types or characterize their physiological state in greater detail. Solving this system requires regularization, such as Tikhonov regularization, which balances fitting the data with maintaining a plausible, smooth solution.