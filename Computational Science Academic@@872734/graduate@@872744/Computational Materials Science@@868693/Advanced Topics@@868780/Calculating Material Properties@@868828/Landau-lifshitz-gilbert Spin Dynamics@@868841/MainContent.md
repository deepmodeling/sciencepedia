## Introduction
The behavior of magnetic materials is fundamentally governed by the collective dynamics of their internal magnetic moments. Understanding and predicting how magnetization evolves in time and space is a cornerstone of modern condensed matter physics and materials science, underpinning technologies from hard drives to next-generation spintronic memory. However, capturing this complex motion requires a robust theoretical framework that can account for both conservative precessional motion and dissipative [energy relaxation](@entry_id:136820). The Landau-Lifshitz-Gilbert (LLG) equation rises to this challenge, providing a powerful [phenomenological model](@entry_id:273816) that has become the standard for simulating micromagnetic phenomena. This article provides a graduate-level exploration of LLG [spin dynamics](@entry_id:146095), bridging fundamental theory with practical application.

First, in "Principles and Mechanisms," we will deconstruct the LLG equation from first principles, examining the physical origins of the precessional and damping torques and defining the crucial concept of the [effective magnetic field](@entry_id:139861) that drives the dynamics. Next, "Applications and Interdisciplinary Connections" will demonstrate the remarkable versatility of the LLG model, exploring its use in characterizing materials, explaining the motion of complex [magnetic textures](@entry_id:751636) like domain walls and skyrmions, and engineering advanced spintronic devices. Finally, "Hands-On Practices" will connect this theoretical knowledge to the world of computational science, addressing the key numerical challenges in solving the LLG equation for practical simulations.

## Principles and Mechanisms

The dynamics of magnetization at the continuum level are governed by a phenomenological equation of motion that captures the fundamental interplay between conservative torques and dissipative relaxation processes. This chapter delineates the principles underpinning the Landau-Lifshitz-Gilbert (LLG) equation, the primary tool for simulating [spin dynamics](@entry_id:146095) in magnetic materials. We will construct this equation from first principles, dissect its constituent terms, define the effective magnetic field that drives the motion, and explore its symmetries and modern extensions.

### The Equation of Motion: Precession and Damping

The foundation of [spin dynamics](@entry_id:146095) is the torque exerted on a magnetic moment by a magnetic field. For a macroscopic [magnetization vector](@entry_id:180304) field $\mathbf{M}(\mathbf{r}, t)$, subject to an [effective magnetic field](@entry_id:139861) $\mathbf{B}_\mathrm{eff}$, the torque results in a precessional motion. The relationship between the magnetic moment $\mathbf{M}$ and the underlying angular [momentum density](@entry_id:271360) $\mathbf{L}$ is given by $\mathbf{M} = \gamma \mathbf{L}$, where $\gamma$ is the **[gyromagnetic ratio](@entry_id:149290)**. The fundamental equation of motion for angular momentum is $\frac{d\mathbf{L}}{dt} = \boldsymbol{\tau}$, where the torque density is $\boldsymbol{\tau} = \mathbf{M} \times \mathbf{B}_\mathrm{eff}$. Combining these gives the equation for precession:

$$
\frac{d\mathbf{M}}{dt} = \gamma (\mathbf{M} \times \mathbf{B}_\mathrm{eff})
$$

A crucial aspect of [magnetism in materials](@entry_id:176681) is that it primarily originates from the spin angular momentum of electrons. For an electron, the [gyromagnetic ratio](@entry_id:149290) $\gamma$ is negative. This sign convention is of profound physical consequence. Let us consider a simplified scenario: a uniform magnetization $\mathbf{M}$ is initially aligned along the $+\hat{\mathbf{x}}$ axis, subject to a static effective field $\mathbf{B}_\mathrm{eff}$ along the $+\hat{\mathbf{z}}$ axis. The initial rate of change is given by $\frac{d\mathbf{M}}{dt} = \gamma (\mathbf{M} \times \mathbf{B}_\mathrm{eff})$. The [cross product](@entry_id:156749) $\mathbf{M} \times \mathbf{B}_\mathrm{eff}$ points in the $+\hat{\mathbf{y}}$ direction. Since $\gamma  0$, the resulting vector $\frac{d\mathbf{M}}{dt}$ points in the $-\hat{\mathbf{y}}$ direction. Therefore, the [magnetization vector](@entry_id:180304) begins to precess clockwise in the $xy$-plane when viewed from above (along $+\hat{\mathbf{z}}$) [@problem_id:3460247]. This is known as **Larmor precession**, and it follows a left-hand rule with respect to the field direction due to the negative [gyromagnetic ratio](@entry_id:149290) of the electron.

In micromagnetics, it is conventional to work with the normalized [magnetization vector](@entry_id:180304) $\mathbf{m} = \mathbf{M} / M_s$, where $M_s$ is the **[saturation magnetization](@entry_id:143313)** (the fixed magnitude of $\mathbf{M}$, with SI units of $\mathrm{A/m}$). We will consistently use an [effective magnetic field](@entry_id:139861), $\mathbf{B}_\mathrm{eff}$, in units of Tesla. The absolute value of the [gyromagnetic ratio](@entry_id:149290) for a free electron is $|\gamma_e| \approx 1.76 \times 10^{11} \, \mathrm{s^{-1}T^{-1}}$ (or $2\pi \times 28 \, \mathrm{GHz/T}$). To avoid ambiguity with the sign, many texts define a positive constant $\gamma$ and explicitly include the negative sign for electron [spin precession](@entry_id:149995). Following a common convention in LLG literature, we write the precession term as $-\gamma (\mathbf{m} \times \mathbf{B}_\mathrm{eff})$, where $\gamma$ is taken as a positive constant.

Pure precession does not describe how a magnetic system reaches equilibrium. A second, dissipative mechanism is required. Gilbert proposed a phenomenological damping term proportional to the time derivative of the magnetization, representing a viscous-like drag on the motion. To ensure that this torque does not change the magnitude of the magnetization (i.e., $| \mathbf{m} | = 1$ is preserved), it must be orthogonal to $\mathbf{m}$. This is achieved with a [cross product](@entry_id:156749) form. Combining the precessional and damping torques, we arrive at the **Landau-Lifshitz-Gilbert (LLG) equation** in its Gilbert form [@problem_id:3460180]:

$$
\frac{\partial \mathbf{m}}{\partial t} = -\gamma \, \mathbf{m} \times \mathbf{B}_\mathrm{eff} + \alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t}
$$

Here:
- The first term, $-\gamma \, \mathbf{m} \times \mathbf{B}_\mathrm{eff}$, is the **precessional torque**. As discussed, it causes $\mathbf{m}$ to precess around $\mathbf{B}_\mathrm{eff}$. The parameter $\gamma$ is the (positive) [gyromagnetic ratio](@entry_id:149290), with SI units of $\mathrm{s^{-1}T^{-1}}$.
- The second term, $\alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t}$, is the **Gilbert damping torque**. It drives the system towards an energy minimum by causing $\mathbf{m}$ to spiral in towards the direction of $\mathbf{B}_\mathrm{eff}$. The coefficient $\alpha$ is the dimensionless **Gilbert damping constant**, which quantifies the strength of this dissipation.
- $\mathbf{B}_\mathrm{eff}$ is the **effective magnetic field**, with SI units of Tesla (T). It is the net field experienced by the magnetization, arising from all energetic contributions, and acts as the driving force for the dynamics.

It is critical to note that both terms on the right-hand side are, by construction of the cross product, perpendicular to $\mathbf{m}$. Since $\frac{\partial \mathbf{m}}{\partial t}$ is a linear combination of these two terms, it too is perpendicular to $\mathbf{m}$. This guarantees that the magnitude of the magnetization is conserved during the dynamics: $\frac{d}{dt}(\mathbf{m} \cdot \mathbf{m}) = 2 \mathbf{m} \cdot \frac{d\mathbf{m}}{dt} = 0$.

### The Landau-Lifshitz Form and its Equivalence

The Gilbert form of the LLG equation is implicit because the time derivative $\frac{\partial \mathbf{m}}{\partial t}$ appears on both sides. An alternative, explicit form was originally proposed by Landau and Lifshitz. The **Landau-Lifshitz (LL) form** is written as:

$$
\frac{\partial \mathbf{m}}{\partial t} = -\gamma' \, \mathbf{m} \times \mathbf{B}_\mathrm{eff} - \lambda \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})
$$

Here, $\gamma'$ is a renormalized [gyromagnetic ratio](@entry_id:149290) and $\lambda$ is a [damping parameter](@entry_id:167312) with units of $\mathrm{s^{-1}T^{-1}}$. The damping term in the LL form, $-\lambda \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})$, has a clear physical interpretation. The [vector triple product](@entry_id:162942) $\mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})$ points in the direction that simultaneously lies in the plane defined by $\mathbf{m}$ and $\mathbf{B}_\mathrm{eff}$ and is perpendicular to $\mathbf{m}$. It is a torque that directly pushes $\mathbf{m}$ towards alignment with $\mathbf{B}_\mathrm{eff}$.

While appearing different, the Gilbert and Landau-Lifshitz forms are mathematically equivalent. We can demonstrate this by algebraically rearranging the Gilbert form to solve for $\frac{\partial \mathbf{m}}{\partial t}$ [@problem_id:3460189]. We begin with the Gilbert form:
$$
\frac{\partial \mathbf{m}}{\partial t} - \alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t} = -\gamma \, \mathbf{m} \times \mathbf{B}_\mathrm{eff}
$$
Taking the cross product of this equation with $\alpha \mathbf{m}$:
$$
\alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t} - \alpha^2 \, \mathbf{m} \times \left(\mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t}\right) = -\alpha \gamma \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})
$$
Using the [vector triple product](@entry_id:162942) identity $\mathbf{A} \times (\mathbf{B} \times \mathbf{C}) = \mathbf{B}(\mathbf{A}\cdot\mathbf{C}) - \mathbf{C}(\mathbf{A}\cdot\mathbf{B})$ and the properties $|\mathbf{m}|=1$ and $\mathbf{m} \cdot \frac{\partial \mathbf{m}}{\partial t} = 0$, we find that $\mathbf{m} \times (\mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t}) = -\frac{\partial \mathbf{m}}{\partial t}$. Substituting this gives:
$$
\alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t} + \alpha^2 \frac{\partial \mathbf{m}}{\partial t} = -\alpha \gamma \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})
$$
We can now substitute the expression for $\alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t}$ from the original Gilbert equation into this result, which yields:
$$
\left(\frac{\partial \mathbf{m}}{\partial t} + \gamma \, \mathbf{m} \times \mathbf{B}_\mathrm{eff}\right) + \alpha^2 \frac{\partial \mathbf{m}}{\partial t} = -\alpha \gamma \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})
$$
Solving for $\frac{\partial \mathbf{m}}{\partial t}$:
$$
(1+\alpha^2) \frac{\partial \mathbf{m}}{\partial t} = -\gamma \, \mathbf{m} \times \mathbf{B}_\mathrm{eff} - \alpha\gamma \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})
$$
$$
\frac{\partial \mathbf{m}}{\partial t} = -\frac{\gamma}{1+\alpha^2} \, \mathbf{m} \times \mathbf{B}_\mathrm{eff} - \frac{\alpha\gamma}{1+\alpha^2} \, \mathbf{m} \times (\mathbf{m} \times \mathbf{B}_\mathrm{eff})
$$
By comparing this directly with the LL form, we find the relations between the two sets of parameters:
$$
\gamma' = \frac{\gamma}{1+\alpha^2} \quad \text{and} \quad \lambda = \frac{\alpha\gamma}{1+\alpha^2}
$$
This equivalence shows that the dimensionless Gilbert damping $\alpha$ not only controls the magnitude of dissipation but also renormalizes the precession frequency. For typical metallic ferromagnets where $\alpha \ll 1$, we have $\gamma' \approx \gamma$ and $\lambda \approx \alpha\gamma$.

### The Driving Force: The Effective Field $B_{\text{eff}}$

The dynamics described by the LLG equation are entirely dictated by the **[effective magnetic field](@entry_id:139861)**, $\mathbf{B}_\mathrm{eff}$. This field is not merely an external applied field; it is a generalized [thermodynamic force](@entry_id:755913) that encompasses all interactions influencing the magnetization. It is derived from the total micromagnetic [free energy functional](@entry_id:184428) of the system, $E[\mathbf{m}]$. The relationship is defined through the **variational derivative** of the energy functional [@problem_id:3460194]:

$$
\mathbf{B}_\mathrm{eff} = - \frac{1}{M_s} \frac{\delta E}{\delta \mathbf{m}}
$$

The variational derivative, $\frac{\delta E}{\delta \mathbf{m}}$, is a vector field defined such that the [first variation](@entry_id:174697) of the energy, $\delta E$, can be written as $\delta E = \int \frac{\delta E}{\delta \mathbf{m}} \cdot \delta \mathbf{m} \, dV$, for an arbitrary, infinitesimal variation $\delta \mathbf{m}$. An important subtlety arises from the constraint $|\mathbf{m}|=1$, which implies that any admissible variation must satisfy $\delta\mathbf{m} \cdot \mathbf{m} = 0$. Because of this, any component of $\frac{\delta E}{\delta \mathbf{m}}$ that is parallel to $\mathbf{m}$ does not contribute to the energy variation. Consequently, any component of $\mathbf{B}_\mathrm{eff}$ parallel to $\mathbf{m}$ produces no torque ($\mathbf{m} \times (\lambda \mathbf{m}) = \mathbf{0}$) and is dynamically inert. We can therefore ignore such parallel components when deriving the physically relevant field [@problem_id:3460185].

The total energy $E$ is a sum of several contributions, each giving rise to a component of the effective field: $E = E_\mathrm{ex} + E_\mathrm{K} + E_\mathrm{Z} + E_\mathrm{D} + \dots$, and correspondingly $\mathbf{B}_\mathrm{eff} = \mathbf{B}_\mathrm{ex} + \mathbf{B}_\mathrm{K} + \mathbf{B}_\mathrm{Z} + \mathbf{B}_\mathrm{D} + \dots$.

#### Exchange Field
The **exchange interaction** favors parallel alignment of neighboring spins and is responsible for ferromagnetic order. It penalizes spatial variations in the magnetization direction. The [energy functional](@entry_id:170311) is:
$$
E_\mathrm{ex}[\mathbf{m}] = \int_{\Omega} A |\nabla \mathbf{m}|^2 \, dV
$$
where $A$ is the exchange stiffness constant. To find the corresponding field, we compute the [first variation](@entry_id:174697) $\delta E_\mathrm{ex}$ and use integration by parts [@problem_id:3460185]. This procedure yields a bulk term and a boundary term. The bulk contribution gives the variational derivative $\frac{\delta E_\mathrm{ex}}{\delta \mathbf{m}} = -2A \nabla^2 \mathbf{m}$, where $\nabla^2$ is the vector Laplacian. The **exchange field** is therefore:
$$
\mathbf{B}_\mathrm{ex} = \frac{2A}{M_s} \nabla^2 \mathbf{m}
$$
The boundary term in the variation, $\int_{\partial\Omega} 2A \frac{\partial \mathbf{m}}{\partial \mathbf{n}} \cdot \delta \mathbf{m} \, dS$, must vanish for a "free" boundary, leading to the **[natural boundary condition](@entry_id:172221)** $\frac{\partial \mathbf{m}}{\partial \mathbf{n}} = \mathbf{0}$, where $\frac{\partial}{\partial \mathbf{n}}$ is the normal derivative at the surface [@problem_id:3460185].

#### Anisotropy Field
Crystalline solids often have preferred ("easy") or disfavored ("hard") directions for magnetization due to spin-orbit coupling. This is described by **[magnetocrystalline anisotropy](@entry_id:144488)**. For a material with **uniaxial anisotropy** along a direction defined by the unit vector $\mathbf{e}_u$, a common form for the energy density is:
$$
w_K = -K_u (\mathbf{m} \cdot \mathbf{e}_u)^2
$$
where $K_u$ is the anisotropy constant. The variation of this energy density gives $\delta w_K = -2K_u (\mathbf{m} \cdot \mathbf{e}_u) (\delta\mathbf{m} \cdot \mathbf{e}_u) = (-2K_u (\mathbf{m} \cdot \mathbf{e}_u) \mathbf{e}_u) \cdot \delta\mathbf{m}$. The corresponding **anisotropy field** is [@problem_id:3460246]:
$$
\mathbf{B}_K = \frac{2K_u}{M_s} (\mathbf{m} \cdot \mathbf{e}_u) \mathbf{e}_u
$$
The sign of $K_u$ determines the nature of the anisotropy. If $K_u > 0$, the energy is minimized when $\mathbf{m}$ is parallel to $\mathbf{e}_u$ ($\theta=0$), creating an **easy axis**. If $K_u  0$, the energy is minimized when $\mathbf{m}$ is perpendicular to $\mathbf{e}_u$ ($\theta=\pi/2$), creating an **easy plane** [@problem_id:3460246].

#### Zeeman Field
An externally applied magnetic field $\mathbf{B}_\mathrm{ext}$ couples to the magnetization via the Zeeman energy:
$$
E_Z[\mathbf{m}] = -\int M_s \mathbf{B}_\mathrm{ext} \cdot \mathbf{m} \, dV
$$
The variation is straightforward, yielding the simplest contribution to the effective field, the **Zeeman field**, which is just the external field itself [@problem_id:3460194]:
$$
\mathbf{B}_Z = \mathbf{B}_\mathrm{ext}
$$

#### Demagnetizing Field
The magnetization itself is a source of a magnetic field, often called the **[demagnetizing field](@entry_id:265717)** or stray field, $\mathbf{H}_d$. In the absence of [free currents](@entry_id:191634), this field is governed by the magnetostatic Maxwell's equations: $\nabla \times \mathbf{H}_d = \mathbf{0}$ and $\nabla \cdot \mathbf{B} = \nabla \cdot (\mu_0(\mathbf{H}_d + \mathbf{M})) = 0$. The curl-free condition allows us to define a scalar potential, $\mathbf{H}_d = -\nabla\phi$, which turns the divergence equation into a Poisson equation for the potential: $\nabla^2\phi = \nabla \cdot \mathbf{M}$.

The [demagnetizing field](@entry_id:265717) is fundamentally a **nonlocal** interaction: the field at a point $\mathbf{r}$ depends on the magnetization distribution throughout the entire magnetic body. The energy associated with this field can be shown to be $E_d = -\frac{\mu_0}{2} \int \mathbf{M} \cdot \mathbf{H}_d \, dV$. The variation of this energy shows that the contribution to the effective B-field is $\mu_0$ times the [demagnetizing field](@entry_id:265717): $\mathbf{B}_\mathrm{eff}^{(d)} = \mu_0 \mathbf{H}_d$ [@problem_id:3460222].

In computational micromagnetics, especially with periodic boundary conditions, it is most efficient to calculate $\mathbf{H}_d$ in Fourier space. The Poisson equation becomes algebraic, and for any wavevector $\mathbf{k} \neq \mathbf{0}$, one finds [@problem_id:3460222]:
$$
\mathbf{H}_d(\mathbf{k}) = - \frac{\mathbf{k}(\mathbf{k} \cdot \mathbf{M}(\mathbf{k}))}{k^2} = - \left(\frac{\mathbf{k}\mathbf{k}^T}{k^2}\right) \mathbf{M}(\mathbf{k})
$$
The matrix $\frac{\mathbf{k}\mathbf{k}^T}{k^2}$ is a projection operator that projects the [magnetization vector](@entry_id:180304) $\mathbf{M}(\mathbf{k})$ onto the direction of $\mathbf{k}$. This shows that the [demagnetizing field](@entry_id:265717) is a [longitudinal field](@entry_id:264833). In real space, this Fourier-space product corresponds to a convolution with a tensor kernel, explicitly demonstrating the nonlocality [@problem_id:3460222].

#### Dzyaloshinskii-Moriya Field
In materials lacking inversion symmetry, the spin-orbit interaction can give rise to the **Dzyaloshinskii-Moriya interaction (DMI)**, an [antisymmetric exchange](@entry_id:138329) that favors non-collinear, chiral [spin structures](@entry_id:161662). The form of the DMI energy depends on the [crystal symmetry](@entry_id:138731). For a bulk material with T-type symmetry, the energy has the form $E_D = \int D \, \mathbf{m} \cdot (\nabla \times \mathbf{m}) \, dV$. The variation yields the **DMI field** [@problem_id:3460194]:
$$
\mathbf{B}_D^{\text{bulk}} = -\frac{2D}{M_s} (\nabla \times \mathbf{m})
$$
For a thin film with an interface normal to $\hat{\mathbf{z}}$, breaking inversion symmetry at the interface leads to a different energy form, such as $w_D = D[m_z (\nabla \cdot \mathbf{m}) - (\mathbf{m} \cdot \nabla)m_z]$. This leads to a distinct interfacial DMI field [@problem_id:3460201]:
$$
\mathbf{B}_D^{\text{interface}} = \frac{2D}{M_s} \left(\nabla m_z - (\nabla \cdot \mathbf{m})\hat{\mathbf{z}}\right)
$$
These terms are crucial for stabilizing chiral magnetic structures like skyrmions and [domain walls](@entry_id:144723).

### Symmetries and Conservation Laws

The LLG equation has fundamental properties related to energy and time symmetry.

#### Energy Dissipation
The total energy of the magnetic system changes over time due to the work done by the effective field. The rate of change is given by $\frac{dE}{dt} = \int \frac{\delta E}{\delta \mathbf{m}} \cdot \frac{\partial \mathbf{m}}{\partial t} \, dV = - M_s \int \mathbf{B}_\mathrm{eff} \cdot \frac{\partial \mathbf{m}}{\partial t} \, dV$. Using the explicit LL form for $\frac{\partial \mathbf{m}}{\partial t}$, we find that the dot product with $\mathbf{B}_\mathrm{eff}$ is:
$$
\mathbf{B}_\mathrm{eff} \cdot \frac{\partial \mathbf{m}}{\partial t} = \frac{\alpha\gamma}{1+\alpha^2} |\mathbf{m} \times \mathbf{B}_\mathrm{eff}|^2
$$
The precession term, being orthogonal to $\mathbf{B}_\mathrm{eff}$, does no work. The energy change is due solely to the damping term. The total rate of energy change is therefore [@problem_id:3460186]:
$$
\frac{dE}{dt} = - M_s \int \frac{\alpha\gamma}{1+\alpha^2} |\mathbf{m} \times \mathbf{B}_\mathrm{eff}|^2 \, dV \le 0
$$
Since $\alpha, \gamma > 0$, the energy of the system can only decrease or remain constant. Dissipation stops ($\frac{dE}{dt}=0$) only when the integrand is zero everywhere, which occurs when $\mathbf{m}$ is parallel to $\mathbf{B}_\mathrm{eff}$ throughout the system. This is the condition for a static equilibrium state. The Gilbert damping term thus ensures that the system relaxes towards a (local) energy minimum.

#### Time-Reversal Symmetry
A physical process is time-reversal invariant if its governing equations have the same form when time is run backwards. The time-reversal operation $T$ transforms time $t \to -t$. Since magnetization is related to spin (an [axial vector](@entry_id:191829) representing angular momentum), it is odd under time reversal: $\mathbf{m}(t) \to -\mathbf{m}(-t)$. Consequently, the time derivative $\dot{\mathbf{m}}$ is even, while the effective field $\mathbf{B}_\mathrm{eff}$ (which includes contributions like exchange and anisotropy, but also the external field which is odd under $T$) is odd. Analyzing the LLG terms under this transformation reveals [@problem_id:3460186]:
- The precession term $-\gamma (\mathbf{m} \times \mathbf{B}_\mathrm{eff})$ transforms into itself; it is **even** under time reversal.
- The Gilbert damping term $\alpha (\mathbf{m} \times \dot{\mathbf{m}})$ transforms into its negative; it is **odd** under [time reversal](@entry_id:159918).

Because the damping term changes sign, the LLG equation as a whole is **not time-reversal invariant** for any non-zero damping $\alpha > 0$. This broken symmetry is the hallmark of a dissipative process. The dynamics of a magnet "winding down" towards equilibrium looks different from a movie of that process played in reverse. Only in the ideal case of zero damping ($\alpha=0$) is the precessional dynamics time-reversal symmetric.

### Extension to Spintronics: Spin-Transfer Torques

In the field of [spintronics](@entry_id:141468), it is possible to manipulate magnetization not just with fields, but also with spin-polarized electrical currents. When a current of spin-polarized electrons passes through a region of non-uniform magnetization (like a [domain wall](@entry_id:156559)), the electrons transfer a portion of their spin angular momentum to the local magnetization, exerting a **[spin-transfer torque](@entry_id:146992) (STT)**. To model this, the LLG equation is augmented with additional torque terms [@problem_id:3460228]:

$$
\frac{\partial \mathbf{m}}{\partial t} = \left(-\gamma \, \mathbf{m} \times \mathbf{B}_\mathrm{eff} + \alpha \, \mathbf{m} \times \frac{\partial \mathbf{m}}{\partial t}\right) - (\mathbf{u} \cdot \nabla)\mathbf{m} + \beta \, \mathbf{m} \times (\mathbf{u} \cdot \nabla)\mathbf{m}
$$

The two new terms are the spin-transfer torques:
1.  **Adiabatic STT**: The term $-(\mathbf{u} \cdot \nabla)\mathbf{m}$ arises from the assumption that the spins of the transport electrons adiabatically follow the local magnetization direction. It acts as an effective torque that can drive [magnetic textures](@entry_id:751636), such as [domain walls](@entry_id:144723), into motion.
2.  **Non-adiabatic STT**: The term $\beta \, \mathbf{m} \times (\mathbf{u} \cdot \nabla)\mathbf{m}$ accounts for the fact that electron spins do not perfectly track the local magnetization due to their own spin-relaxation processes. This "mistracking" results in an additional torque component, whose strength is governed by the dimensionless **non-adiabaticity parameter** $\beta$.

The vector $\mathbf{u}$ represents an effective spin drift velocity, whose direction is parallel to the [electric current](@entry_id:261145) density $\mathbf{J}$ and whose magnitude is given by:
$$
\mathbf{u} = \frac{P \mu_B}{e M_s} \mathbf{J}
$$
where $P$ is the spin polarization of the current, $\mu_B$ is the Bohr magneton, and $e$ is the elementary charge.

It is crucial to distinguish the roles of the two [dimensionless parameters](@entry_id:180651), $\alpha$ and $\beta$. The Gilbert damping $\alpha$ describes an **[intrinsic property](@entry_id:273674) of the ferromagnet**: the relaxation of the collective magnetization by transferring energy to the lattice. In contrast, the non-adiabaticity parameter $\beta$ is a property related to the **spin transport electrons**: it quantifies the efficiency of the spin-transfer process arising from [spin relaxation](@entry_id:139462) in the current itself. While they can be related in some theoretical models, they represent physically distinct dissipative channels [@problem_id:3460228]. This augmented LLG equation is the foundation for modeling a vast range of modern spintronic devices.