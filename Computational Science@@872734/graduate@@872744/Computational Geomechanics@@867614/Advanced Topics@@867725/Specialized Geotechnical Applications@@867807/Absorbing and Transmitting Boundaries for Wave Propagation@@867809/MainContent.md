## Introduction
Simulating wave propagation in unbounded domains, such as those encountered in [seismology](@entry_id:203510) and geotechnical engineering, presents a fundamental challenge for numerical methods that operate on finite computational grids. The need to truncate a physically infinite or semi-infinite medium with an artificial boundary introduces a critical problem: unless handled correctly, this boundary will act like a rigid wall, causing outgoing waves to reflect back into the domain of interest. These spurious reflections contaminate the numerical solution, rendering it physically meaningless. The development of effective absorbing and [transmitting boundaries](@entry_id:756128)—numerical conditions that mimic an infinite medium by allowing [wave energy](@entry_id:164626) to pass out of the computational domain without reflection—is therefore essential for accurate dynamic analysis.

This article provides a comprehensive exploration of the theory and practice behind these non-[reflecting boundaries](@entry_id:199812). It addresses the critical knowledge gap between the physical necessity of an energy-[absorbing boundary](@entry_id:201489) and its correct numerical implementation. By delving into the underlying principles, from energetic requirements to [impedance matching](@entry_id:151450), the reader will gain a robust theoretical foundation. The following chapters are structured to build upon this foundation, guiding the reader from core concepts to advanced, practical applications.

*   **Principles and Mechanisms** will establish the theoretical groundwork, exploring the energetic imperative for non-[reflecting boundaries](@entry_id:199812), the role of radiation conditions, and the mechanical principles behind local viscous boundaries and more sophisticated approaches like the Perfectly Matched Layer (PML).

*   **Applications and Interdisciplinary Connections** will demonstrate how these principles are extended to solve complex, real-world problems in geomechanics and geophysics, including their use in heterogeneous, anisotropic, and nonlinear media, as well as multi-physics contexts like [poroelasticity](@entry_id:174851).

*   **Hands-On Practices** will provide a series of targeted problems designed to solidify the reader's understanding of key concepts, from deriving [reflection coefficients](@entry_id:194350) to designing a high-performance absorbing layer.

By progressing through these sections, the reader will acquire the knowledge necessary to select, implement, and critically evaluate [absorbing boundary conditions](@entry_id:164672) for a wide range of wave propagation problems in [computational geomechanics](@entry_id:747617).

## Principles and Mechanisms

In [computational geomechanics](@entry_id:747617), the simulation of [wave propagation](@entry_id:144063) phenomena, such as those arising from earthquakes or dynamic [soil-structure interaction](@entry_id:755022), frequently involves domains that are, for practical purposes, unbounded. Numerical methods like the finite element or finite difference method, however, are inherently restricted to finite computational domains. This dichotomy necessitates the introduction of an **artificial boundary** to truncate the physical domain to a manageable size. The treatment of this artificial boundary is a critical aspect of the modeling process, as an improper condition can lead to spurious, non-physical wave reflections that contaminate the solution within the region of interest. This chapter elucidates the fundamental principles governing the design of non-[reflecting boundaries](@entry_id:199812) and explores the mechanisms of the most prominent techniques used to implement them.

### The Energetic Imperative for Non-Reflecting Boundaries

The fundamental purpose of an artificial boundary is to allow wave energy generated within the computational domain, $\Omega_R$, to pass out of it as if the domain were truly infinite. Let us consider the mechanical energy balance for a linear elastic solid. In the absence of [body forces](@entry_id:174230), the rate of change of the total mechanical energy—the sum of the kinetic energy, $K(t)$, and the [elastic strain energy](@entry_id:202243), $U(t)$—within a volume $\Omega_R$ is equal to the power supplied by the tractions acting on its boundary, $\Gamma_R$. This is expressed by the identity:

$$
\frac{\mathrm{d}}{\mathrm{d}t} \left[ K(t) + U(t) \right] = \int_{\Gamma_R} \boldsymbol{t} \cdot \boldsymbol{v} \, \mathrm{d}\Gamma
$$

where $\boldsymbol{t}$ is the traction vector on the boundary and $\boldsymbol{v}$ is the particle velocity.

If the artificial boundary $\Gamma_R$ were, for example, a fixed boundary ($\boldsymbol{v} = \boldsymbol{0}$) or a [traction-free boundary](@entry_id:197683) ($\boldsymbol{t} = \boldsymbol{0}$), the power [flux integral](@entry_id:138365) would be zero. In such cases, no energy can leave the domain. Wave energy propagating outwards would be perfectly reflected back into $\Omega_R$, leading to an unphysical accumulation of energy and a solution that fails to represent the physics of an unbounded medium.

To prevent such spurious reflections, the boundary must be an **energy sink** for outgoing waves. That is, the power flux term $\int_{\Gamma_R} \boldsymbol{t} \cdot \boldsymbol{v} \, \mathrm{d}\Gamma$ must be negative, signifying that energy is continuously being extracted from the domain. A general way to ensure this is to impose a relationship between traction and velocity of the form $\boldsymbol{t} = - \boldsymbol{Z} \boldsymbol{v}$, where $\boldsymbol{Z}$ is a positive-semidefinite impedance operator. This results in a power flux that is always non-positive, effectively drawing energy out of the domain [@problem_id:3498877]. The challenge, then, lies in designing an operator $\boldsymbol{Z}$ that not only absorbs energy but does so in a way that mimics the response of an infinite medium, thereby minimizing reflections.

### The Role of Radiation Conditions

The physical requirement that waves generated by a bounded source must carry energy away from the source and not return from infinity is formalized by a **radiation condition**. In the frequency domain, for a time-harmonic scalar wave field $u(\boldsymbol{x})$ with time dependence $\mathrm{e}^{-\mathrm{i}\omega t}$ governed by the Helmholtz equation, $\nabla^2 u + k^2 u = 0$, the requirement for purely outgoing waves is encapsulated by the **Sommerfeld radiation condition** [@problem_id:3498911]:

$$
\lim_{r\to\infty} r\left(\frac{\partial u}{\partial r} - \mathrm{i} k u\right) = 0
$$

where $r = |\boldsymbol{x}|$ is the radial distance from the source and $k$ is the [wavenumber](@entry_id:172452). This condition ensures that in the far field, the solution behaves like an [outgoing spherical wave](@entry_id:201591) of the form $\frac{f(\theta, \phi)}{r} \mathrm{e}^{\mathrm{i} k r}$, effectively filtering out incoming waves. The sign in the expression is critical and is coupled to the choice of time-harmonic convention; a convention of $\mathrm{e}^{+\mathrm{i}\omega t}$ would require replacing the minus sign with a plus sign.

In linear [elastodynamics](@entry_id:175818), the situation is more complex because the medium supports two distinct types of body waves: compressional (P) waves, which are irrotational, and shear (S) waves, which are solenoidal. These waves propagate at different speeds, $c_p = \sqrt{(\lambda+2\mu)/\rho}$ and $c_s = \sqrt{\mu/\rho}$ respectively, and thus have different wavenumbers, $k_p = \omega/c_p$ and $k_s = \omega/c_s$. A radiation condition for the vector [displacement field](@entry_id:141476) $\boldsymbol{u}$ must account for both wave types. The **Kupradze-Sommerfeld radiation conditions** achieve this by decomposing the far-field displacement into its P-wave (longitudinal) and S-wave (transverse) components and applying a Sommerfeld-type condition to each [@problem_id:3498911]:

$$
\lim_{r\to\infty} r\left(\frac{\partial \boldsymbol{u}_p}{\partial r} - \mathrm{i} k_p \boldsymbol{u}_p\right) = \boldsymbol{0} \quad \text{and} \quad \lim_{r\to\infty} r\left(\frac{\partial \boldsymbol{u}_s}{\partial r} - \mathrm{i} k_s \boldsymbol{u}_s\right) = \boldsymbol{0}
$$

These conditions are essential not only for physical realism but also for mathematical well-posedness. For exterior [boundary value problems](@entry_id:137204), such as scattering of waves off an object, the radiation condition guarantees the uniqueness of the solution [@problem_id:3498877]. Any numerical boundary treatment on a finite truncation boundary can be viewed as an approximation of these fundamental radiation conditions.

### The Principle of Mechanical Impedance Matching

The most direct way to construct an approximate radiation condition is through the principle of **[mechanical impedance](@entry_id:193172) matching**. Mechanical impedance, in the context of [wave propagation](@entry_id:144063), is the ratio of a force-like quantity (traction) to a velocity-like quantity (particle velocity).

Consider a simple one-dimensional scenario where two semi-infinite elastic media are in welded contact at an interface. When a [plane wave](@entry_id:263752) traveling in medium 1 is normally incident on the interface, part of its energy is reflected and part is transmitted into medium 2. The amplitudes of the reflected and transmitted waves are determined by the impedance contrast between the two media. For a P-wave, the specific [mechanical impedance](@entry_id:193172) is $Z_p = \rho c_p$, and for an S-wave, it is $Z_s = \rho c_s$. The [reflection coefficient](@entry_id:141473) for particle velocity, for instance, is given by the ratio $(Z_1 - Z_2) / (Z_1 + Z_2)$, where $Z_1$ and $Z_2$ are the impedances of the respective media [@problem_id:3498846].

From this, two key insights emerge:
1.  Reflection is caused by an **impedance mismatch** ($Z_1 \neq Z_2$).
2.  Reflection is completely eliminated if the impedances are perfectly matched ($Z_1 = Z_2$).

This principle is the cornerstone of local [absorbing boundary conditions](@entry_id:164672). To make an artificial boundary non-reflecting, we must ensure that the boundary condition enforces a traction-velocity relationship that endows the boundary with the same [mechanical impedance](@entry_id:193172) as the medium it replaces. For an outgoing plane wave traveling in the positive $x$-direction, the relationship between traction and particle velocity is $t = -Z v$. A [non-reflecting boundary condition](@entry_id:752602) at $x=L$ must therefore apply a traction $t(L,t) = -Z v(L,t)$, where $Z$ is the impedance of the physical medium [@problem_id:3498846, @problem_id:3498936]. The negative sign confirms that the boundary does negative work on the domain, extracting energy as required.

### Local Absorbing Boundaries: The Viscous Dashpot Model

The simplest and most widely used [non-reflecting boundary condition](@entry_id:752602) is derived by applying the [impedance matching](@entry_id:151450) principle under the assumption of **normally incident plane waves**. This leads to the **Lysmer-Kuhlemeyer viscous boundary**.

Let's consider an artificial planar boundary with outward unit normal $\boldsymbol{n}$. We analyze the [normal and tangential components](@entry_id:166204) of motion separately.
-   An outgoing P-wave propagating along $\boldsymbol{n}$ has particle motion parallel to $\boldsymbol{n}$. The exact relationship between the normal traction $t_n$ and normal velocity $v_n$ for this wave is $t_n = -\rho c_p v_n$ [@problem_id:3498936].
-   An outgoing S-wave propagating along $\boldsymbol{n}$ has particle motion tangential to the boundary. The relationship between the tangential traction vector $\boldsymbol{t}_t$ and tangential velocity vector $\boldsymbol{v}_t$ is $\boldsymbol{t}_t = -\rho c_s \boldsymbol{v}_t$ [@problem_id:3498945].

The Lysmer-Kuhlemeyer boundary condition imposes these two decoupled relations simultaneously on the artificial boundary:
$$
t_n = -\rho c_p v_n \quad \text{and} \quad \boldsymbol{t}_t = -\rho c_s \boldsymbol{v}_t
$$
These conditions are implemented in [finite element analysis](@entry_id:138109) by attaching "viscous dashpots" to the boundary nodes. The force exerted by a dashpot is proportional to the nodal velocity. To convert the impedance (which has units of stress per velocity) to a nodal dashpot coefficient (units of force per velocity), it must be multiplied by the nodal tributary area, $A$. The dashpot coefficients for motion normal ($c_n$) and tangential ($c_t$) to the boundary are therefore [@problem_id:3498864]:
$$
c_n = \rho c_p A \quad \text{and} \quad c_t = \rho c_s A
$$

While elegant and simple, the effectiveness of this approach is limited by its underlying assumptions [@problem_id:3498864, @problem_id:3498919]:
1.  **Normal Incidence:** The derivation is exact only for P- and S-waves striking the boundary at a normal angle ($0^\circ$ incidence).
2.  **Body Waves Only:** The derivation does not account for surface-[guided waves](@entry_id:269489), such as Rayleigh or Love waves, which have different phase velocities and coupled particle motions.
3.  **Local Homogeneity:** The material properties $\rho$, $c_p$, and $c_s$ are assumed to be constant at the boundary.

For body waves arriving at oblique angles, the simple dashpots generate spurious reflections. The [reflection coefficient](@entry_id:141473) for an obliquely incident SH wave, for example, can be shown to increase from zero at [normal incidence](@entry_id:260681) to one (total reflection) at grazing incidence ($\theta \to 90^\circ$) [@problem_id:3498919]. For [surface waves](@entry_id:755682), which involve complex, elliptically polarized particle motion and have a phase velocity different from $c_p$ or $c_s$, the uncoupled dashpots represent a severe impedance mismatch and are largely ineffective.

### A Hierarchy of Advanced Boundary Treatments

To overcome the limitations of local dashpots, a hierarchy of more sophisticated and accurate methods has been developed. These can be broadly classified into nonlocal boundary conditions and absorbing layers [@problem_id:3498851]. A key distinction also arises between **[absorbing boundaries](@entry_id:746195)**, designed solely to let outgoing waves pass with minimal reflection, and **[transmitting boundaries](@entry_id:756128)**, which correctly model the exterior impedance to allow both the passage of outgoing waves and the correct entry of incoming waves from the far field.

#### Nonlocal Boundary Conditions: The Dirichlet-to-Neumann Map

The theoretically exact [non-reflecting boundary condition](@entry_id:752602) for a given frequency is known as the **Dirichlet-to-Neumann (DtN) map**. It is a mathematical operator, $\mathcal{T}$, that maps the displacement field on the boundary, $u|_{\Gamma_R}$, to the traction field, $t|_{\Gamma_R}$, that would be generated by the unique, physically correct (outgoing) wave solution in the infinite exterior domain [@problem_id:3498913]. Imposing the condition $t = \mathcal{T}u$ on the artificial boundary makes it perfectly transparent to all outgoing waves at that frequency.

The DtN map possesses several key characteristics:
-   **Exactness:** For a given frequency and geometry, it is reflection-free.
-   **Nonlocality:** The traction at a point on the boundary generally depends on the displacement over the entire boundary. In the time domain, this translates to a convolution with the history of the boundary motion.
-   **Frequency Dependence:** The operator itself depends on the frequency $\omega$.
-   **Geometric Dependence:** The explicit form of the operator depends on the shape of the artificial boundary.

While a [closed-form expression](@entry_id:267458) for the DtN map is unavailable for arbitrarily shaped boundaries, it can be constructed analytically for separable geometries like spheres and cylinders. The construction involves expanding the wave field in a basis of vector harmonics and using outgoing Hankel functions to satisfy the radiation condition. The DtN map then becomes a diagonal (or block-diagonal) operator in the [spectral domain](@entry_id:755169) [@problem_id:3498913]. The existence of the DtN map demonstrates that exact non-[reflecting boundaries](@entry_id:199812) are theoretically possible and provides the "gold standard" against which approximate methods are measured. The need for a coupled, frequency-dependent operator, as embodied by the DtN map, is essential for accurately absorbing complex surface waves like Rayleigh waves [@problem_id:3498919].

#### Absorbing Layers: The Perfectly Matched Layer (PML)

A fundamentally different and powerful approach is the **Perfectly Matched Layer (PML)**. Instead of defining a condition *on* the boundary, the PML method surrounds the computational domain with an artificial layer of material designed to absorb incoming waves without reflection [@problem_id:3498851].

The PML works by a mathematical transformation known as **[complex coordinate stretching](@entry_id:162960)**. In the frequency domain, a coordinate such as $x$ is replaced by a complex-valued coordinate $\tilde{x}(x)$. This transformation has two profound effects:
1.  At the interface between the physical domain and the PML, the layer is perfectly impedance-matched to the physical medium. At the continuous level, this ensures that waves enter the layer without any reflection, regardless of their type, frequency, or [angle of incidence](@entry_id:192705).
2.  Within the layer, the complex coordinate causes propagating wave solutions to decay exponentially. The wave energy is smoothly attenuated as it travels through the layer.

The PML is a remarkably robust and versatile technique, capable of effectively absorbing both body waves and surface waves over a wide range of frequencies and incidence angles.

### Advanced Topics and Practical Considerations

#### Pathologies of PMLs and Modern Solutions

Despite their power, standard PML formulations can suffer from instabilities in certain challenging scenarios, manifesting as late-time exponential growth of the solution. These failures are particularly prominent under two conditions [@problem_id:3498866]:
1.  **Grazing Incidence and Evanescent Waves:** The damping in a standard PML is proportional to the component of the [wavevector](@entry_id:178620) normal to the layer. For waves at grazing incidence or for [evanescent waves](@entry_id:156713) (which have an imaginary normal [wavenumber](@entry_id:172452)), this damping effect vanishes, leading to instabilities.
2.  **Low-Frequency Content:** The standard PML formulation is singular at zero frequency ($\omega=0$), making it unable to damp static or very low-frequency components, which can accumulate over long transient simulations. This issue is particularly acute in [nearly incompressible materials](@entry_id:752388) (Poisson's ratio $\nu \to 0.5$), where the P-[wave speed](@entry_id:186208) becomes much larger than the S-wave speed, creating a very broad spectrum of wavelengths to absorb.

To remedy these pathologies, advanced PML formulations have been developed:
-   **Multi-Axial PML (MPML):** This method applies complex stretching along both normal and tangential directions to the layer, ensuring that waves at any angle (including grazing) are damped.
-   **Complex Frequency Shift (CFS) PML:** This introduces a frequency shift parameter into the stretching function, which removes the singularity at $\omega=0$. This makes the PML effective at damping low-frequency and [evanescent waves](@entry_id:156713), thereby curing the late-time instabilities.

These modern variants, often implemented using stable [auxiliary differential equation](@entry_id:746594) (ADE) formulations, have made the PML a highly reliable tool for a vast range of wave propagation problems.

#### Computational Cost and Selection Criteria

In practice, the choice between an advanced ABC (like a time-domain DtN map) and a PML involves trade-offs in computational cost, memory usage, and implementation complexity [@problem_id:3498867]. For transient simulations of duration $T = N_t \Delta t$ on a boundary with $N_b$ degrees of freedom:

-   **PML:** The primary cost is the addition of the PML domain itself. This adds a number of unknowns, $N_{\text{pml}}$, proportional to the layer thickness. The total computational work scales as $O(N_{\text{pml}} N_t)$, and the memory footprint is constant at $O(N_{\text{pml}})$.
-   **Time-Domain Nonlocal ABC:** A direct convolution with the entire time history is prohibitively expensive, with work scaling as $O(N_b N_t^2)$. A practical implementation uses **[recursive convolution](@entry_id:754162)**, where the boundary kernel is approximated by a sum of $M$ exponential functions (a Prony series). This reduces the total work to $O(N_b M N_t)$ and requires a constant memory of $O(N_b M)$.

The selection criteria can be summarized as follows:
-   For very long simulations (large $N_t$), direct convolution is not viable.
-   **Recursive ABCs** are computationally cheaper than PMLs if the cost per step is lower, i.e., when $N_b M \ll N_{\text{pml}}$. This is often the case when the exterior is a simple homogeneous half-space, and its response kernel can be accurately fitted with a small number of exponential terms ($M$).
-   **PMLs** are generally preferred when the material near the boundary is heterogeneous or complex, as the PML naturally handles this complexity. They are also superior when the time-domain kernel is difficult to approximate with a small $M$, which occurs with slowly decaying responses found in [poroelasticity](@entry_id:174851) or at very low frequencies.

Ultimately, the optimal choice depends on a balance between the desired accuracy, the geometric and material complexity of the problem, and the available computational resources.