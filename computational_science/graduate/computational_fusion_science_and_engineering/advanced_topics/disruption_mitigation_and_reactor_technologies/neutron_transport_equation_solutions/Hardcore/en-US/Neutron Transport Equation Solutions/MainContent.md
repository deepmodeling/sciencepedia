## Introduction
The behavior of neutrons in matter is a cornerstone of nuclear science, dictating the performance, safety, and feasibility of fission and fusion energy systems. Accurately predicting the distribution of neutrons—their density, energy, and direction of travel—is essential for designing components like a fusion reactor's breeding blanket or shielding. However, this predictive capability hinges on solving the Boltzmann transport equation, a complex integro-differential equation that poses significant mathematical and computational challenges. This article serves as a comprehensive guide to understanding and solving this pivotal equation. The following chapters will build your expertise from the ground up. First, in **Principles and Mechanisms**, we will dissect the transport equation itself, exploring its physical meaning and the foundational concepts of both deterministic and stochastic solution methods. Next, **Applications and Interdisciplinary Connections** will showcase how these solutions are used to calculate critical engineering parameters and solve problems in fields ranging from reactor analysis to plasma physics. Finally, the **Hands-On Practices** section provides concrete problems to translate theory into practical computational skill, solidifying your understanding of these powerful techniques.

## Principles and Mechanisms

The behavior of neutrons within a medium is governed by the principles of particle transport, which describe how particles stream through space and interact with matter. At its core, the study of neutron transport is an exercise in statistical mechanics, accounting for the collective behavior of a vast number of individual neutrons. This chapter elucidates the fundamental equation describing this behavior—the Boltzmann transport equation—and explores the principal mechanisms and methodologies for its solution, which are central to [computational fusion science](@entry_id:1122784).

### The Neutron Transport Equation: A Phase-Space Balance

The state of a neutron at any instant is fully described by its position $\vec{r}$, its direction of motion $\vec{\Omega}$ (a [unit vector](@entry_id:150575)), and its kinetic energy $E$. These three variables define a seven-dimensional continuous space known as **phase space**. The primary quantity of interest in [transport theory](@entry_id:143989) is the **[angular neutron flux](@entry_id:1121012)**, denoted $\psi(\vec{r}, \vec{\Omega}, E)$.

To understand the physical meaning of angular flux, we first consider the angular number density, $n(\vec{r}, \vec{\Omega}, E)$, which represents the number of neutrons per unit volume, per unit [solid angle](@entry_id:154756), and per unit energy. The angular flux is then defined as the product of the angular number density and the neutron speed, $v(E)$:

$$
\psi(\vec{r}, \vec{\Omega}, E) = v(E) n(\vec{r}, \vec{\Omega}, E)
$$

Physically, the angular flux $\psi(\vec{r}, \vec{\Omega}, E)$ represents the number of neutrons at position $\vec{r}$ with direction $\vec{\Omega}$ and energy $E$ that cross a unit area oriented perpendicular to $\vec{\Omega}$, per unit time, per unit [solid angle](@entry_id:154756), and per unit energy. Its standard units are $\mathrm{n} \cdot \mathrm{cm}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1} \cdot \mathrm{eV}^{-1}$ .

While the angular flux provides the most detailed description, it is often useful to work with its angular moments. The two most important moments are:

1.  The **scalar flux**, $\phi(\vec{r}, E)$, which is the integral of the angular flux over all directions. It represents the total flow rate of neutrons of energy $E$ passing through a point $\vec{r}$ from all directions. Equivalently, and perhaps more intuitively, it can be interpreted as the total path length traveled per unit time by all neutrons within a unit volume, per unit energy. Its units are $\mathrm{n} \cdot \mathrm{cm}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{eV}^{-1}$.
    $$
    \phi(\vec{r}, E) = \int_{4\pi} \psi(\vec{r}, \vec{\Omega}, E) \, d\vec{\Omega}
    $$

2.  The **[neutron current](@entry_id:1128689)**, $\vec{J}(\vec{r}, E)$, which is the first angular moment of the angular flux. It is a vector quantity representing the net flow rate of neutrons per unit area, per unit energy. The direction of $\vec{J}$ indicates the direction of net particle streaming. Its units are also $\mathrm{n} \cdot \mathrm{cm}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{eV}^{-1}$.
    $$
    \vec{J}(\vec{r}, E) = \int_{4\pi} \vec{\Omega} \, \psi(\vec{r}, \vec{\Omega}, E) \, d\vec{\Omega}
    $$

The governing equation for the angular flux is derived from a simple principle: particle conservation in an infinitesimal phase-space element $d\vec{r} \, d\vec{\Omega} \, dE$. Under steady-state conditions, the rate at which neutrons are lost from this element must exactly equal the rate at which they are gained.

The **loss mechanisms** are :
-   **Streaming (Leakage)**: Neutrons physically move out of the spatial [volume element](@entry_id:267802) $d\vec{r}$. This net outflow is described by a divergence term, $\vec{\Omega} \cdot \nabla \psi$.
-   **Collisions**: Neutrons within the element interact with nuclei in the medium and are either absorbed or scattered into a different direction or energy, thereby being removed from the state $(\vec{\Omega}, E)$. This removal rate is proportional to the flux and the **macroscopic total cross section**, $\Sigma_t(\vec{r}, E)$, which represents the probability of any interaction per unit path length. The collision loss term is $\Sigma_t(\vec{r}, E) \psi(\vec{r}, \vec{\Omega}, E)$.

The **gain mechanisms** are :
-   **In-scattering**: Neutrons from other directions $\vec{\Omega}'$ and energies $E'$ scatter into the state $(\vec{\Omega}, E)$. This is described by the **double-differential macroscopic [scattering cross section](@entry_id:150101)**, $\Sigma_s(\vec{r}, E' \to E, \vec{\Omega}' \cdot \vec{\Omega})$, integrated over all possible initial states.
-   **Fission**: In fissile materials, neutron-induced fission events create new neutrons. This source depends on the fission rate, which is proportional to the scalar flux $\phi(\vec{r}, E')$, the average number of neutrons per fission $\nu(E')$, and the macroscopic fission cross section $\Sigma_f(\vec{r}, E')$. The newly created neutrons are emitted with an energy spectrum $\chi(E)$ and are typically assumed to be isotropic in the [lab frame](@entry_id:181186).
-   **External Sources**: Independent sources, such as the D-T [fusion reaction](@entry_id:159555) in a plasma, can inject neutrons into the system. This is represented by a source term $Q(\vec{r}, \vec{\Omega}, E)$.

Equating the rate of loss to the rate of gain gives the steady-state Boltzmann neutron transport equation. For a general, spatially heterogeneous medium, this equation is :

$$
\vec{\Omega} \cdot \nabla \psi(\vec{r}, \vec{\Omega}, E) + \Sigma_t(\vec{r}, E) \psi(\vec{r}, \vec{\Omega}, E) = \int_0^\infty dE' \int_{4\pi} d\vec{\Omega}' \, \Sigma_s(\vec{r}, E' \to E, \vec{\Omega}' \cdot \vec{\Omega}) \psi(\vec{r}, \vec{\Omega}', E') + S_f(\vec{r}, E) + Q(\vec{r}, \vec{\Omega}, E)
$$

where the fission source $S_f$ is given by:

$$
S_f(\vec{r}, E) = \frac{\chi(E)}{4\pi} \int_0^\infty dE' \, \nu\Sigma_f(\vec{r}, E') \phi(\vec{r}, E')
$$

Every term in this equation has units of a source density: $\mathrm{n} \cdot \mathrm{cm}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1} \cdot \mathrm{eV}^{-1}$, ensuring the balance is dimensionally consistent.

### Interaction Physics: The Role of Cross Sections

The material-dependent coefficients in the transport equation, the macroscopic cross sections $\Sigma$, are the bridge between the physics of [neutron-nucleus interactions](@entry_id:1128684) and the macroscopic transport model. These are derived from **microscopic cross sections**, denoted $\sigma$, which represent the effective target area a single nucleus presents for a particular interaction.

The relationship between the macroscopic cross section $\Sigma_x$ for a reaction type $x$ and the microscopic cross section $\sigma_x$ in a material with atomic number density $N$ (atoms per unit volume) is simply:

$$
\Sigma_x(E) = N \sigma_x(E)
$$

For a [homogeneous mixture](@entry_id:146483) of different nuclides $i$, each with [number density](@entry_id:268986) $N_i$, the total [macroscopic cross section](@entry_id:1127564) is the sum of the contributions from each nuclide :

$$
\Sigma_x(E) = \sum_i N_i \sigma_{x,i}(E)
$$

The total cross section, $\Sigma_t$, is the sum of all possible reaction channels, which are broadly categorized into **absorption** ($\Sigma_a$) and **scattering** ($\Sigma_s$). Absorption includes reactions like radiative capture ($(n, \gamma)$) and fission ($(n,f)$) that eliminate the incident neutron. Scattering includes elastic and inelastic processes that change the neutron's energy and direction but conserve its number. Thus, $\Sigma_t = \Sigma_a + \Sigma_s$.

The scattering process requires a more detailed description, as it links different parts of the phase space. The **macroscopic scattering kernel**, $\Sigma_s(\vec{r}, E' \to E, \vec{\Omega}' \cdot \vec{\Omega})$, is constructed by summing the contributions from each nuclide in the material mixture. The probability distribution for the outgoing energy and angle, $p_i(E' \to E, \mu)$, where $\mu = \vec{\Omega}' \cdot \vec{\Omega}$, is provided by evaluated nuclear data files (e.g., ENDF). The full kernel is then :

$$
\Sigma_s(\vec{r}, E' \to E, \mu) = \sum_i N_i \sigma_{s,i}(E') p_i(E' \to E, \mu)
$$

This kernel, when integrated over all outgoing energies $E$ and solid angles $\vec{\Omega}$, must recover the total macroscopic scattering cross section at the incident energy $E'$, i.e., $\int_0^\infty dE \int_{4\pi} d\vec{\Omega} \, \Sigma_s(\vec{r}, E' \to E, \mu) = \Sigma_s(\vec{r}, E')$.

### Solving the Equation: Problem Formulation

The transport equation is a partial integro-differential equation, and to be well-posed, it requires a complete problem specification, including boundary conditions and a clear definition of the source terms.

#### Boundary Conditions

Boundary conditions must specify the angular flux for all *incoming* directions at the boundary of the computational domain. Let $\partial V$ be the boundary surface with an outward [unit normal vector](@entry_id:178851) $\vec{n}_b$. An incoming direction $\vec{\Omega}$ is one for which $\vec{\Omega} \cdot \vec{n}_b  0$. Common boundary conditions include :

-   **Vacuum**: No particles enter the domain from the outside.
    $$ \psi(\vec{r}_b, \vec{\Omega}, E) = 0 \quad \text{for} \quad \vec{\Omega} \cdot \vec{n}_b  0 $$

-   **Specular Reflection**: Particles hitting the boundary are reflected like light from a mirror, with the angle of incidence equal to the angle of reflection. The incoming flux in direction $\vec{\Omega}$ is equal to the outgoing flux in the reflected direction $\vec{\Omega}' = \vec{\Omega} - 2(\vec{\Omega} \cdot \vec{n}_b)\vec{n}_b$.
    $$ \psi(\vec{r}_b, \vec{\Omega}, E) = \psi(\vec{r}_b, \vec{\Omega} - 2(\vec{\Omega} \cdot \vec{n}_b)\vec{n}_b, E) \quad \text{for} \quad \vec{\Omega} \cdot \vec{n}_b  0 $$

-   **White (or Diffuse) Reflection**: All outgoing particles are reflected back into the domain with an isotropic [angular distribution](@entry_id:193827) (Lambertian). The magnitude is set by conserving the particle current.
    $$ \psi(\vec{r}_b, \vec{\Omega}, E) = \frac{1}{\pi} \int_{\vec{\Omega}' \cdot \vec{n}_b  0} \psi(\vec{r}_b, \vec{\Omega}', E) (\vec{\Omega}' \cdot \vec{n}_b) \, d\vec{\Omega}' \quad \text{for} \quad \vec{\Omega} \cdot \vec{n}_b  0 $$

-   **Periodic**: Used to model infinitely repeating geometries (e.g., a single fuel pin in a large reactor lattice). A particle leaving one boundary at $\vec{r}_b'$ with direction $\vec{\Omega}$ re-enters at a corresponding boundary point $\vec{r}_b$ with the same direction.
    $$ \psi(\vec{r}_b, \vec{\Omega}, E) = \psi(\vec{r}_b', \vec{\Omega}, E) \quad \text{for} \quad \vec{\Omega} \cdot \vec{n}_b  0 $$

-   **Albedo**: A simplified [diffuse reflection](@entry_id:173213) model where a fraction $a(E)$ of the outgoing current is reflected isotropically. It is a generalization of the white boundary, which has $a(E)=1$.
    $$ \psi(\vec{r}_b, \vec{\Omega}, E) = \frac{a(E)}{\pi} \int_{\vec{\Omega}' \cdot \vec{n}_b  0} \psi(\vec{r}_b, \vec{\Omega}', E) (\vec{\Omega}' \cdot \vec{n}_b) \, d\vec{\Omega}' \quad \text{for} \quad \vec{\Omega} \cdot \vec{n}_b  0 $$

#### Fixed-Source vs. Eigenvalue Problems

The mathematical character of the transport problem depends critically on the nature of its source terms. This leads to a fundamental distinction between problems relevant to fusion systems and those relevant to fission reactors .

In a **source-driven system**, such as a fusion reactor blanket, neutrons are produced by an external source (the D-T plasma) that is independent of the neutron flux itself. The fission term is absent or negligible ($\Sigma_f \approx 0$). The steady-state transport equation takes the form $L\psi = Q$, where $L$ is the net transport operator (streaming and collisions) and $Q$ is the known external source. This is a **linear [fixed-source problem](@entry_id:1125046)**. For a subcritical system (one that cannot sustain a chain reaction on its own), this equation has a unique, stable solution where the flux magnitude is directly proportional to the source strength.

In contrast, a **multiplying system**, like a fission reactor core, is defined by the fission source term, which depends on the flux itself: $S_f = F\psi$. To analyze the self-sustaining nature of such a system, we consider the case with no external source ($Q=0$). The equation becomes $L\psi = F\psi$. This is no longer a [fixed-source problem](@entry_id:1125046) but a [homogeneous equation](@entry_id:171435). Non-trivial solutions exist only under a special condition, which is formulated as a **[generalized eigenvalue problem](@entry_id:151614)**:

$$
L\psi = \frac{1}{k} F\psi
$$

Here, the eigenvalue $k$ (often denoted $k_{\text{eff}}$) represents the ratio of neutrons produced in one "generation" by fission to those lost in the preceding generation. A steady-state, self-sustaining chain reaction is possible only if production exactly balances loss, which corresponds to the **[criticality condition](@entry_id:201918)** $k_{\text{eff}} = 1$. The resulting flux solution is an [eigenfunction](@entry_id:149030), determined only up to a multiplicative constant (i.e., its shape is fixed, but its [absolute magnitude](@entry_id:157959), corresponding to the reactor power, is not). If $k_{\text{eff}}  1$ (supercritical), the neutron population will grow exponentially in time, whereas if $k_{\text{eff}}  1$ (subcritical), it will decay in the absence of an external source.

### Deterministic Solution Methods: The Discrete Ordinates ($S_N$) Approach

Deterministic methods solve the transport equation by discretizing the entire phase space and solving the resulting system of algebraic equations. The most prominent deterministic method is the **[discrete ordinates](@entry_id:1123828) ($S_N$) method**.

#### Angular Discretization

The core idea of the $S_N$ method is to replace the continuous angular variable $\vec{\Omega}$ with a finite set of $M$ discrete directions, or ordinates, $\{\vec{\Omega}_m\}$, each with an associated quadrature weight, $\{w_m\}$. The transport equation is then solved only for these specific directions. Any integral over solid angle is approximated by a weighted sum over the [discrete ordinates](@entry_id:1123828) :

$$
\int_{4\pi} f(\vec{\Omega}') \, d\vec{\Omega}' \approx \sum_{m'=1}^{M} w_{m'} f(\vec{\Omega}_{m'})
$$

Applying this to the multigroup transport equation (where energy is already discretized into $G$ groups) results in a system of $M \times G$ coupled partial differential equations for the semi-discrete unknowns $\psi_{g,m}(\vec{r}) \equiv \psi_g(\vec{r}, \vec{\Omega}_m)$. For each group $g$ and direction $m$, the equation becomes:

$$
\vec{\Omega}_m \cdot \nabla \psi_{g,m}(\vec{r}) + \Sigma_{t,g}(\vec{r}) \psi_{g,m}(\vec{r}) = \sum_{g'=1}^{G} \sum_{l=0}^{L} \frac{2l+1}{4\pi} \Sigma_{s,g' \to g,l}(\vec{r}) \sum_{m'=1}^{M} w_{m'} P_l(\vec{\Omega}_m \cdot \vec{\Omega}_{m'}) \psi_{g',m'}(\vec{r}) + Q_g(\vec{r}, \vec{\Omega}_m)
$$

Here, [anisotropic scattering](@entry_id:148372) has been represented using a Legendre polynomial ($P_l$) expansion up to order $L$.

#### Spatial Discretization

The semi-discrete $S_N$ equations must still be discretized in space. This is typically done using a finite volume or finite element approach, marching through the spatial grid along each discrete direction. The choice of spatial discretization scheme is critical for the accuracy and stability of the solution. Two classic schemes are the Diamond-Difference and Step-Characteristics methods .

-   The **Diamond-Difference (DD)** scheme assumes a linear variation of the angular flux across each spatial cell. For a 1D slab cell of width $\Delta x$ and optical thickness $\tau = \Sigma_t \Delta x / |\mu|$, the DD relation between the incoming flux ($\psi_{in}$) and outgoing flux ($\psi_{out}$) is:
    $$
    \psi_{out} = \frac{2 - \tau}{2 + \tau} \psi_{in} + \frac{Q \Delta x}{|\mu| + \Sigma_t \Delta x/2}
    $$
    The term $(2-\tau)/(2+\tau)$ is the transmission factor. If the optical thickness $\tau > 2$, this factor becomes negative. This means that for optically thick cells, a positive incoming flux can produce an unphysical negative outgoing flux, a significant drawback of the DD method.

-   The **Step-Characteristics (SC)** scheme assumes the source within the cell is constant and solves the transport equation analytically across the cell. This yields the update relation:
    $$
    \psi_{out} = \psi_{in} e^{-\tau} + \frac{Q}{\Sigma_t} (1 - e^{-\tau})
    $$
    In this formula, all terms are guaranteed to be non-negative for non-negative inputs ($\psi_{in} \ge 0, Q \ge 0$). The SC scheme is therefore unconditionally **positivity-preserving**, making it more robust than DD, although it is only first-order accurate, whereas DD is second-order accurate.

#### Numerical Artifacts: Ray Effects

A notorious limitation of the $S_N$ method is the **ray effect**, an artifact arising directly from angular discretization. Because transport is restricted to a finite number of directions, unphysical flux oscillations and depressions can appear in regions between the discrete rays. This is most pronounced in problems with localized sources and low scattering, such as a collimated beam in a void .

Consider a detector of radius $a$ at a distance $L$ from a source. If the source direction $\theta_0$ does not align with a discrete ordinate, the numerical solution will stream along the nearest direction, creating an angular misalignment $\varepsilon$. This results in a lateral offset $d = L \sin\varepsilon$ at the detector plane. The numerical beam will miss the detector if $d > a$. The quadrature is adequate only if the misalignment is less than the detector's acceptance half-angle, $\alpha = \arcsin(\min\{1, a/L\})$.

To guarantee adequacy for *any* source direction, the quadrature must be fine enough that the maximum possible misalignment, $\varepsilon_{\max} = \pi/N$ for a uniform quadrature of $N$ angles, is less than or equal to the acceptance angle. This provides a criterion for quadrature refinement:

$$
N \ge N_{\min} = \left\lceil \frac{\pi}{\alpha(L,a)} \right\rceil
$$

This illustrates that mitigating [ray effects](@entry_id:1130607) requires tailoring the [angular quadrature](@entry_id:1121013) to the specific problem geometry and physics.

### Stochastic Solution Methods: The Monte Carlo (MC) Approach

An entirely different paradigm for solving the transport equation is the **Monte Carlo (MC) method**. Instead of discretizing phase space and solving a large system of equations, the MC method performs a direct [statistical simulation](@entry_id:169458) of the physical lives of individual neutrons. By tracking a large number of these particle "histories" and averaging their behavior, one can obtain statistically robust estimates of macroscopic quantities like flux.

An **analog Monte Carlo** simulation aims to replicate the physical stochastic processes as closely as possible . The life of a single neutron history proceeds as follows:

1.  **Birth**: A neutron is "born" by sampling its initial position, direction, and energy from the distribution of the source $Q$. Its statistical weight is initialized to $w=1$.

2.  **Free Flight**: The distance $s$ the neutron travels to its next collision is a random variable governed by the exponential probability distribution $p(s) = \Sigma_t e^{-\Sigma_t s}$. This distance is sampled using the [inverse transform method](@entry_id:141695): $s = - \ln(\xi) / \Sigma_t$, where $\xi$ is a random number uniformly distributed in $(0, 1)$. The particle's position is then updated along its current direction.

3.  **Collision**: At the new position, a collision occurs. The type of interaction is chosen probabilistically. The probability of scattering is $\Sigma_s / \Sigma_t$, and the probability of absorption is $\Sigma_a / \Sigma_t$. Another random number is sampled to make this choice.
    -   If **absorption** is selected, the neutron is removed from the system, and its history is terminated.
    -   If **scattering** is selected, the neutron survives. A new direction and energy are sampled from the distribution defined by the scattering kernel $\Sigma_s(E' \to E, \mu)$. The simulation then returns to Step 2 to sample a new free-flight path.

This process is repeated until the neutron is absorbed or leaks from the system.

To estimate a macroscopic quantity like the scalar flux, we use **tallies**. The **track-length estimator** is a common and efficient method. The flux in a region is physically related to the total path length of particles within it. Therefore, for each straight-line path segment (track) a simulated neutron makes, we measure its length $\ell$ inside a designated tally volume $V$. The contribution of this track to the average scalar flux tally for that volume is $\ell/V$. To estimate the average angular flux in a specific solid angle bin $\Delta\Omega_k$, the contribution is $\ell / (V \Delta\Omega_k)$, and it is only scored if the particle's direction lies within that bin. After simulating millions or billions of histories, the law of large numbers ensures that the average of these tally contributions converges to the true physical quantity.

### Advanced Topic: Adjoint Transport

In many applications, we are not interested in the full flux distribution but in a specific integrated quantity, or **response**, such as a reaction rate in a small detector, a dose at a point, or the system's multiplication factor. The **[adjoint transport equation](@entry_id:1120823)** provides a powerful and elegant framework for calculating such responses efficiently.

The adjoint flux, $\psi^\dagger(\vec{r}, \vec{\Omega}, E)$, can be interpreted as the "importance" of a neutron at phase-space point $(\vec{r}, \vec{\Omega}, E)$ with respect to its contribution to the desired response. The [adjoint equation](@entry_id:746294) is derived from the forward equation by defining an inner product over phase space and find the formal adjoint of the transport operator, $L^\dagger$. The key property linking the forward and adjoint problems is the [reciprocity relation](@entry_id:198404) :

$$
\langle \psi^\dagger, L\psi \rangle = \langle L^\dagger \psi^\dagger, \psi \rangle
$$

This leads to the remarkable result that the response $R = \langle q^\dagger, \psi \rangle$ can also be calculated as $R = \langle \psi^\dagger, q \rangle$, where $q^\dagger$ is the "adjoint source" (the [response function](@entry_id:138845) itself) and $q$ is the forward source.

The [adjoint transport equation](@entry_id:1120823) is given by $L^\dagger \psi^\dagger = q^\dagger$, where the [adjoint operator](@entry_id:147736) $L^\dagger$ has the following form:
-   The streaming term reverses direction: $\vec{\Omega} \cdot \nabla \psi \to -\vec{\Omega} \cdot \nabla \psi^\dagger$. Adjoint particles effectively move backward in space.
-   The total cross section remains unchanged: $\Sigma_t^\dagger(\vec{r}, E) = \Sigma_t(\vec{r}, E)$.
-   The scattering operator transposes the initial and final energies: the adjoint scattering kernel for a transition from $E'$ to $E$ is the forward kernel for a transition from $E$ to $E'$. This means adjoint particles "up-scatter" in energy where forward particles would "down-scatter".
-   The adjoint source $q^\dagger$ is simply the cross section for the reaction of interest, defined over the region of interest. For example, to calculate a reaction rate $R_x$ in a detector volume $V_D$, the adjoint source is $q^\dagger(\vec{r}, E) = \Sigma_x(\vec{r}, E) \chi_D(\vec{r})$, where $\chi_D$ is the [characteristic function](@entry_id:141714) of the detector .
-   The adjoint boundary conditions are also reversed. For a forward vacuum boundary where no particles enter ($\psi=0$ for $\vec{\Omega}\cdot\vec{n}_b  0$), the adjoint boundary condition requires that no adjoint particles (no importance) leave the domain ($\psi^\dagger=0$ for $\vec{\Omega}\cdot\vec{n}_b  0$) .

The power of the adjoint method becomes apparent when one needs to calculate a single response for many different forward source distributions. Instead of running a computationally expensive forward transport simulation for each source, one can run a single adjoint simulation to find $\psi^\dagger$. The response for any forward source $q$ can then be found by the simple integration $R = \int \psi^\dagger q \, dV d\Omega dE$.