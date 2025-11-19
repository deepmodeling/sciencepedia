## Introduction
Classical [continuum mechanics](@entry_id:155125), while remarkably successful at the macroscopic scale, encounters fundamental limitations when applied to phenomena at micro- and nano-scales. It predicts unphysical infinite stresses at [geometric singularities](@entry_id:186127) like crack tips and fails to capture the size-dependent material behaviors widely observed in [nanostructures](@entry_id:148157). To bridge this gap, [generalized continuum theories](@entry_id:193621) are required, and among the most influential is the theory of nonlocal elasticity. This framework introduces a characteristic internal length scale, postulating that the stress at a point is influenced not just by the local state of deformation, but by the strain throughout a surrounding neighborhood.

This article provides a graduate-level exploration of nonlocal elasticity, structured to build a comprehensive understanding from first principles to practical application.
*   In **Principles and Mechanisms**, we will delve into the mathematical heart of the theory, examining its integral and differential formulations, its connection to atomistic physics, and its thermodynamic and mathematical foundations.
*   The **Applications and Interdisciplinary Connections** chapter will demonstrate the theory's power by exploring how it resolves classical paradoxes in [fracture mechanics](@entry_id:141480), models the unique mechanical behavior of nanostructures, and enriches fundamental concepts like Saint-Venant's principle.
*   Finally, **Hands-On Practices** offers guided problems that translate theory into practice, tackling core challenges like deriving [wave dispersion](@entry_id:180230) and implementing efficient [numerical algorithms](@entry_id:752770) for nonlocal models.

By navigating these chapters, the reader will gain a robust understanding of nonlocal elasticity as a powerful extension of continuum mechanics, essential for modern materials science and engineering.

## Principles and Mechanisms

In this chapter, we transition from the conceptual motivations for nonlocal theories to the concrete mathematical framework of nonlocal elasticity. We will systematically construct the theory, starting from its fundamental constitutive postulate and exploring its physical origins, mathematical properties, and practical implications. The goal is to build a rigorous understanding of both the principles that govern [nonlocal mechanics](@entry_id:191075) and the mechanisms through which these principles manifest in material behavior.

### The Integral Formulation of Nonlocal Elasticity

The foundational axiom of classical, local elasticity is that the stress at a material point is determined exclusively by the strain at that same point. Eringen's theory of nonlocal elasticity departs from this axiom by postulating that the stress at a point is influenced by the state of strain throughout the body. This concept is formalized through an integral [constitutive relation](@entry_id:268485).

In this framework, the Cauchy stress tensor $\boldsymbol{\sigma}$ at a point $\mathbf{x}$ is not directly proportional to the [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}(\mathbf{x})$. Instead, it is computed as a weighted average of the local stress response, $\mathbb{C}:\boldsymbol{\varepsilon}$, over the entire domain $\Omega$ of the body. Here, $\mathbb{C}$ represents the standard [fourth-order elasticity tensor](@entry_id:188318). The mathematical expression of this principle is [@problem_id:2665383]:

$$
\boldsymbol{\sigma}(\mathbf{x}) = \int_{\Omega} \alpha(|\mathbf{x}-\mathbf{\xi}|, \ell) \, (\mathbb{C}:\boldsymbol{\varepsilon}(\mathbf{\xi})) \, \mathrm{d}V_{\xi}
$$

The function $\alpha$ is known as the **attenuation kernel** or **nonlocal kernel**. It encapsulates the physics of [long-range interactions](@entry_id:140725). For a homogeneous and isotropic material, this kernel depends on two key parameters: the distance $|\mathbf{x}-\mathbf{\xi}|$ between the source point $\mathbf{\xi}$ and the field point $\mathbf{x}$, and a characteristic **internal length scale** $\ell$. This length scale is a material property that quantifies the range of nonlocal interactions; it is a fundamental departure from classical theory, which contains no [intrinsic length scale](@entry_id:750789).

The kernel $\alpha$ must satisfy several crucial properties to form a physically and mathematically consistent theory:

1.  **Spatial Attenuation**: The kernel must decay as the distance $|\mathbf{x}-\mathbf{\xi}|$ increases, signifying that the influence of distant points is weaker than that of nearby points. The decay occurs over the length scale $\ell$.

2.  **Dimensionality**: For the integral equation to be dimensionally consistent, the units of the kernel $\alpha$ must be $[\text{length}]^{-n}$, where $n$ is the spatial dimension of the domain $\Omega$. This ensures that $\boldsymbol{\sigma}$ retains the correct units of stress (force per area).

3.  **Recovery of Local Elasticity**: A valid [nonlocal theory](@entry_id:752667) must converge to the classical local theory in the limit where the internal length scale vanishes, i.e., $\ell \to 0$. This requires the kernel to behave like the **Dirac delta distribution** $\delta(\mathbf{x}-\mathbf{\xi})$ as $\ell \to 0$. The [sifting property](@entry_id:265662) of the [delta function](@entry_id:273429), when applied to the constitutive integral, would then yield $\boldsymbol{\sigma}(\mathbf{x}) = \mathbb{C}:\boldsymbol{\varepsilon}(\mathbf{x})$. A necessary condition for this convergence is that the kernel must be **normalized** such that its integral over all space is unity:
    $$
    \int_{\mathbb{R}^n} \alpha(|\mathbf{r}|, \ell) \, \mathrm{d}V_r = 1
    $$
    This normalization also ensures that a uniform strain field $\boldsymbol{\varepsilon}_0$ applied to an infinite body produces the correct uniform local stress $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}_0$.

### Atomistic Foundations of Nonlocality

The integral form of nonlocal elasticity, while phenomenological, is deeply rooted in the physics of discrete materials. The long-range interactions between atoms or molecules in a crystal lattice provide a natural physical basis for a continuum theory where stress at one point depends on deformation at others.

Consider a simplified atomistic model of a crystal lattice where particles interact through a [pair potential](@entry_id:203104) $\phi(r)$, with $r$ being the interatomic distance. The total potential energy of the system is the sum of energies of all interacting pairs. By performing a coarse-graining procedure—effectively replacing discrete sums over atoms with continuous integrals over the volume—we can derive a continuum-level [constitutive law](@entry_id:167255). A schematic derivation shows that for long-range potentials, this procedure naturally leads to an Eringen-type integral law [@problem_id:2665435].

Crucially, this bottom-up approach reveals a direct relationship between the microscopic interaction potential and the macroscopic nonlocal kernel. The analysis shows that for a central [pair potential](@entry_id:203104) $\phi(r)$ that decays as a power law, $\phi(r) \sim r^{-p}$ for large $r$, the resulting nonlocal kernel $\alpha(r)$ is asymptotically proportional to $r^2 \phi''(r)$. This leads to a kernel that also decays as a power law, $\alpha(r) \sim r^{-p}$. This result is significant because it demonstrates that the phenomenological kernel is not an arbitrary choice; its mathematical form, particularly its long-range character, can be directly inherited from the underlying physics of interatomic forces. This contrasts with common assumptions that kernels must decay exponentially, which would arise from short-range (e.g., nearest-neighbor) interactions.

### The Structure of Nonlocal Continuum Theory

A common point of confusion when first encountering nonlocal elasticity is understanding which parts of the classical continuum mechanics framework are modified. The structure of continuum theory is often described as a triad of principles: [kinematics](@entry_id:173318), balance laws, and [constitutive relations](@entry_id:186508). When transitioning from local to [nonlocal theory](@entry_id:752667), only the last of these is altered [@problem_id:2665387].

-   **Kinematics**, the description of motion and deformation, remains unchanged. The [small-strain tensor](@entry_id:754968) $\boldsymbol{\varepsilon}$ is still defined as the symmetric part of the [displacement gradient](@entry_id:165352), $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$. This is a purely geometric definition, independent of material properties.

-   **Balance Laws**, which represent fundamental physical principles, also retain their form. The conservation of mass and the [balance of linear momentum](@entry_id:193575), $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \ddot{\mathbf{u}}$, are considered universal. The stress tensor $\boldsymbol{\sigma}$ appearing in the momentum balance is now the nonlocal stress, but the differential equation representing local [force balance](@entry_id:267186) is unchanged. For nonpolar media (those without internal [rotational degrees of freedom](@entry_id:141502)), the [balance of angular momentum](@entry_id:181848) continues to require the Cauchy stress tensor to be symmetric, $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$.

-   **Constitutive Relations**, which are material-specific, are the exclusive locus of modification. The local law $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$ is replaced by the integral relation discussed previously. It is this change alone that introduces nonlocality and its associated length scale into the model.

### The Differential Formulation: A Convenient and Equivalent Form

While the integral formulation is the most general and fundamental, its integro-differential nature can be cumbersome for analytical and numerical work. Under certain conditions, it is possible to convert the integral law into an equivalent, purely differential form. This equivalence holds exactly for an infinite, homogeneous medium, provided the attenuation kernel has a specific form.

This equivalence is most clearly demonstrated in Fourier space [@problem_id:2905431]. The nonlocal constitutive law is a convolution, $\boldsymbol{\sigma} = \alpha * (\mathbb{C}:\boldsymbol{\varepsilon})$. By the convolution theorem, its Fourier transform is an algebraic product:

$$
\widehat{\boldsymbol{\sigma}}(\mathbf{k}) = \widehat{\alpha}(\|\mathbf{k}\|) \, (\mathbb{C}:\widehat{\boldsymbol{\varepsilon}}(\mathbf{k}))
$$

where $\widehat{\cdot}$ denotes the Fourier transform and $\mathbf{k}$ is the wavevector. Now, consider a differential [constitutive relation](@entry_id:268485) of the Helmholtz type:

$$
(1 - \ell^2 \nabla^2) \boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}
$$

In Fourier space, the Laplacian operator $\nabla^2$ corresponds to multiplication by $-\|\mathbf{k}\|^2$. Thus, the differential relation transforms to:

$$
(1 + \ell^2 \|\mathbf{k}\|^2) \widehat{\boldsymbol{\sigma}}(\mathbf{k}) = \mathbb{C}:\widehat{\boldsymbol{\varepsilon}}(\mathbf{k}) \quad \implies \quad \widehat{\boldsymbol{\sigma}}(\mathbf{k}) = \frac{1}{1 + \ell^2 \|\mathbf{k}\|^2} (\mathbb{C}:\widehat{\boldsymbol{\varepsilon}}(\mathbf{k}))
$$

Comparing the two Fourier-space expressions, we see that the integral and differential models are identical if and only if the Fourier transform of the kernel is $\widehat{\alpha}(\|\mathbf{k}\|) = (1 + \ell^2 \|\mathbf{k}\|^2)^{-1}$. The [real-space](@entry_id:754128) kernel corresponding to this transform is the Green's function for the Helmholtz operator, $(1 - \ell^2 \nabla^2)$.

In one dimension, this specific kernel is the double [exponential function](@entry_id:161417), $\alpha(x) = \frac{1}{2\ell} \exp(-|x|/\ell)$ [@problem_id:2665354] [@problem_id:2905431]. In three dimensions, it is the Yukawa potential, $\alpha(r) = \frac{1}{4\pi\ell^2 r} \exp(-r/\ell)$. This differential form is widely used due to its relative simplicity, but its equivalence to the integral form is strictly valid only on infinite domains. On bounded domains, the two models diverge, particularly near boundaries.

### Mechanisms of Nonlocality: Regularization and Dispersion

One of the most powerful features of nonlocal elasticity is its ability to regularize the mechanical response at small length scales, curing certain pathologies of the classical local theory. This is often described as capturing **[size effects](@entry_id:153734)**. A paradigmatic example is the dispersion of [elastic waves](@entry_id:196203) [@problem_id:2665441].

In a classical elastic bar, the speed of [longitudinal waves](@entry_id:172335), $c_0 = \sqrt{E/\rho}$, is constant, independent of the wavelength. This leads to unphysical predictions at very short wavelengths (approaching the atomic scale). Let's analyze wave propagation using the 1D nonlocal model with the exponential kernel $\alpha(x) = \frac{1}{2\ell}\exp(-|x|/\ell)$. Substituting a plane-wave solution $u(x,t) = U \exp(i(kx - \omega t))$ into the governing equations yields the following **dispersion relation**:

$$
\rho \omega^2 = \frac{E k^2}{1 + (\ell k)^2}
$$

From this, we can find the [phase velocity](@entry_id:154045) $c_p = \omega/k$. In nondimensional form, where $\kappa = |k|\ell$ is the nondimensional [wavenumber](@entry_id:172452), the [phase velocity](@entry_id:154045) $\bar{c}_p = c_p/c_0$ is:

$$
\bar{c}_p(\kappa) = \frac{1}{\sqrt{1 + \kappa^2}}
$$

This result demonstrates a key mechanism of nonlocality. The phase velocity is no longer constant; it depends on the [wavenumber](@entry_id:172452).
-   For long wavelengths ($\kappa \ll 1$, i.e., wavelength $\lambda \gg \ell$), $\bar{c}_p \approx 1$, and we recover the classical wave speed $c_0$.
-   For short wavelengths ($\kappa \gg 1$, i.e., wavelength $\lambda \ll \ell$), $\bar{c}_p \to 0$. High-frequency waves travel slower and are attenuated.

The phase velocity is bounded above by $c_0$ for all frequencies, eliminating the unphysical behavior of discrete [lattice models](@entry_id:184345) where velocities can become infinite. This dispersive behavior is a hallmark of nonlocal models. The internal length scale $\ell$ naturally introduces a cutoff that separates macroscopic, local-like behavior from microscopic, nonlocal-dominated behavior. A characteristic cutoff wavenumber can be defined where nonlocal effects become significant, typically where $|k_c| \sim 1/\ell$ [@problem_id:2665441].

### Mathematical and Thermodynamic Foundations

For a theory to be physically viable, it must be consistent with the laws of thermodynamics and rest on a sound mathematical foundation.

For an elastic, rate-independent process, the material response is **conservative** or **hyperelastic**. This means that no energy is dissipated during a loading-unloading cycle. In the context of thermodynamics, this implies that the local dissipation, given by the Clausius-Duhem inequality, must be zero: $D = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi} = 0$, where $\psi$ is the Helmholtz free energy density [@problem_id:2665374]. This implies that the stress must be derivable from an energy potential. For a nonlocal system, the total free energy $\Psi$ is a quadratic functional of the strain field:

$$
\Psi[\boldsymbol{\varepsilon}] = \frac{1}{2} \int_{\Omega} \int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{x}) : \mathbb{K}(\mathbf{x} - \mathbf{\xi}) : \boldsymbol{\varepsilon}(\mathbf{\xi}) \, \mathrm{d}V_{\xi} \, \mathrm{d}V_x
$$

For the stress operator to be derivable from this potential, the kernel must satisfy a [major symmetry](@entry_id:198487) condition, $\mathbb{K}_{ijkl}(\mathbf{r}) = \mathbb{K}_{klij}(-\mathbf{r})$. This ensures the [nonlocal operator](@entry_id:752663) is **self-adjoint**. Furthermore, thermodynamic stability requires the free energy to be non-negative for any strain field, which translates to the condition that the Fourier transform of the kernel, $\widehat{\mathbb{K}}(\mathbf{k})$, must be a [positive semi-definite](@entry_id:262808) tensor for all $\mathbf{k}$.

These physical requirements have direct analogues in the functional-analytic properties of the nonlocal [integral operator](@entry_id:147512) $T_\alpha f = \int_\Omega \alpha(x-\xi) f(\xi) d\xi$ [@problem_id:2665405]. For the operator to be well-behaved on the Hilbert space $L^2(\Omega)$, it must be **bounded**, meaning it does not amplify functions infinitely. This is guaranteed if the kernel $\alpha$ is, for instance, in $L^1(\mathbb{R}^n)$ or $L^\infty(\mathbb{R}^n)$. The condition of self-adjointness, which ensures a real spectrum and the existence of an energy potential, requires that the kernel be an [even function](@entry_id:164802), $\alpha(\mathbf{z}) = \alpha(-\mathbf{z})$. This is a more stringent condition than the one for general [hyperelasticity](@entry_id:168357), and is typically assumed for [isotropic materials](@entry_id:170678).

### Challenges in Bounded Domains

The elegance of the nonlocal framework on infinite domains is challenged when applied to realistic, finite-sized bodies. Two major issues arise: boundary conditions and kernel truncation.

#### Boundary Conditions
A fundamental difference emerges between the integral and differential formulations when boundaries are present [@problem_id:2665442].
-   The **integral model** results in an integro-differential equation for the [displacement field](@entry_id:141476). The [integral operator](@entry_id:147512) does not increase the differential order of the governing equation. Consequently, a [weak formulation](@entry_id:142897) (via the [principle of virtual work](@entry_id:138749)) produces only the standard boundary terms, and the classical boundary conditions—prescribing displacements on $\Gamma_u$ and tractions on $\Gamma_t$—are sufficient for a [well-posed problem](@entry_id:268832).
-   The **differential model**, $(1 - \ell^2 \nabla^2)\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$, is a higher-order system of [partial differential equations](@entry_id:143134). The presence of the Laplacian term $\nabla^2\boldsymbol{\sigma}$ increases the differential order. Obtaining a [weak formulation](@entry_id:142897) for this system requires [integration by parts](@entry_id:136350) on the stress field, which introduces new, non-classical boundary terms involving gradients of stress (e.g., $\nabla \boldsymbol{\sigma} \cdot \mathbf{n}$). To ensure a [well-posed problem](@entry_id:268832), these terms must be controlled by specifying additional, non-classical boundary conditions for the stress field.

#### Kernel Truncation and Renormalization
For a point $\mathbf{x}$ near the boundary of a [finite domain](@entry_id:176950) $\Omega$, the integral $\int_\Omega \alpha(|\mathbf{x}-\mathbf{\xi}|)\dots \mathrm{d}V_\xi$ is truncated, as the kernel's support extends beyond $\Omega$. This simple truncation breaks the normalization property, since $\int_\Omega \alpha(|\mathbf{x}-\mathbf{\xi}|) \mathrm{d}V_\xi \lt 1$ for points near the boundary [@problem_id:2665409].

Using this unrenormalized truncated kernel leads to an unphysical **boundary softening**: under a uniform strain, the stress near the boundary is lower than in the bulk, as the material points "feel" fewer interacting neighbors.

To remedy this, a **renormalized kernel** $\widehat{\alpha}$ is often introduced:
$$
\widehat{\alpha}(\mathbf{x},\mathbf{\xi};\ell) = \frac{\alpha(|\mathbf{x}-\mathbf{\xi}|;\ell)}{I(\mathbf{x})} \quad \text{where} \quad I(\mathbf{x}) = \int_{\Omega} \alpha(|\mathbf{x}-\boldsymbol{\eta}|;\ell)\,\mathrm{d}\boldsymbol{\eta}
$$
By construction, this kernel integrates to one for every point $\mathbf{x} \in \Omega$, thereby restoring consistency under uniform strain. However, this fix comes at a cost. The normalization factor $I(\mathbf{x})$ depends on the position $\mathbf{x}$, which breaks the symmetry of the kernel, i.e., $\widehat{\alpha}(\mathbf{x},\mathbf{\xi}) \neq \widehat{\alpha}(\mathbf{\xi},\mathbf{x})$. This loss of symmetry implies that the [nonlocal operator](@entry_id:752663) is no longer self-adjoint, complicating the formulation of [variational principles](@entry_id:198028) and the development of symmetric stiffness matrices in numerical methods like the finite element method [@problem_id:2665409]. In the bulk of the material, far from the boundaries (at distances much greater than $\ell$), $I(\mathbf{x}) \to 1$, and the distinction between the renormalized and unrenormalized models vanishes.