## Introduction
Superconductivity stands as one of the most remarkable quantum phenomena observable on a macroscopic scale, defined by its signature properties of [zero electrical resistance](@entry_id:151583) and the active expulsion of magnetic fields, known as the Meissner effect. While these empirical observations are fascinating, a deeper understanding requires a theoretical framework that can describe the underlying [electrodynamics](@entry_id:158759). The London equations, developed by brothers Fritz and Heinz London in 1935, represent the first successful phenomenological theory to explain these behaviors, providing a cornerstone for the physics of superconductors. This article addresses the need for a coherent model that connects the microscopic behavior of superconducting electrons to macroscopic electromagnetic properties.

This article is structured to guide you from fundamental principles to practical applications. The first chapter, **Principles and Mechanisms**, will derive the two London equations from a simple [two-fluid model](@entry_id:139846), explain how they lead to the Meissner effect, and introduce the crucial concept of the [magnetic penetration depth](@entry_id:140378). We will also explore advanced topics, including the effects of anisotropy and the limitations of this local theory. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of the London framework by applying it to classify type-I and type-II superconductors, analyze the properties of [quantum vortices](@entry_id:147375), and understand the principles behind modern experimental probes and electronic devices. Finally, the **Hands-On Practices** chapter will provide a set of guided problems designed to solidify your theoretical understanding and build practical calculation skills.

## Principles and Mechanisms

The electromagnetic properties of superconductors are profoundly different from those of ordinary metals. While the introductory chapter highlighted the empirical phenomena of zero resistance and [perfect diamagnetism](@entry_id:203008) (the Meissner effect), this chapter delves into the theoretical framework that describes these behaviors. The London equations, developed by Fritz and Heinz London in 1935, provide a phenomenological yet remarkably successful description of the [electrodynamics](@entry_id:158759) of the superconducting state. They serve as the cornerstone for understanding how superconductors interact with electric and magnetic fields.

### The Electrodynamics of the Superconducting State: The London Equations

At the heart of the London theory is the two-fluid model, which posits that below the critical temperature $T_c$, the conduction electrons can be conceptually divided into two interpenetrating components: a normal fluid of electrons that behave like those in a conventional metal, and a superfluid of electrons that are condensed into a macroscopic quantum state. This superfluid component moves without any dissipation, carrying what is known as the **supercurrent**. The London equations describe the behavior of this idealized, frictionless charged fluid.

#### The First London Equation: Perfect Conductivity and Inertial Response

Let us consider the dynamics of the charge carriers in the superfluid component. We denote the number density of these superconducting carriers as $n_s$, their charge as $q$ (which is $-e$ for electrons), and their [inertial mass](@entry_id:267233) as $m$. In an ideal superconductor, these carriers experience no scattering. Therefore, when subjected to an electric field $\mathbf{E}$, they accelerate unimpeded according to Newton's second law. The force on a single carrier is $\mathbf{F} = q\mathbf{E}$, and its acceleration is $\frac{d\mathbf{v}_s}{dt}$, where $\mathbf{v}_s$ is the average drift velocity of the superfluid. Newton's law thus reads:

$m \frac{d\mathbf{v}_s}{dt} = q\mathbf{E}$

This equation describes a purely **inertial response**: the velocity of the superfluid changes as long as an electric field is present. This is in stark contrast to a normal conductor, where scattering leads to a frictional drag force and a steady-state velocity proportional to the field (Ohm's law).

The supercurrent density, $\mathbf{J}_s$, is defined by the flow of these carriers: $\mathbf{J}_s = n_s q \mathbf{v}_s$. By taking the time derivative of this expression and substituting the equation of motion, we arrive at the **first London equation** [@problem_id:3001688]:

$\frac{\partial \mathbf{J}_s}{\partial t} = n_s q \frac{\partial \mathbf{v}_s}{\partial t} = n_s q \left( \frac{q\mathbf{E}}{m} \right) = \frac{n_s q^2}{m} \mathbf{E}$

Using the electron charge $q=-e$, the equation takes its standard form:

$\frac{\partial \mathbf{J}_s}{\partial t} = \frac{n_s e^2}{m} \mathbf{E}$

This equation encapsulates the property of perfect conductivity. If a constant electric field $\mathbf{E}_0$ were applied to a superconductor, the supercurrent would grow linearly with time, $\mathbf{J}_s(t) = \left(\frac{n_s e^2}{m} t\right) \mathbf{E}_0$, without bound. This implies an infinite direct current (DC) conductivity. Conversely, in the absence of an electric field ($\mathbf{E}=0$), the equation dictates that $\frac{\partial \mathbf{J}_s}{\partial t} = 0$. This means that any existing supercurrent will flow indefinitely without decay, providing a theoretical basis for the phenomenon of **[persistent currents](@entry_id:146997)** [@problem_id:3001720].

#### The Second London Equation: Perfect Diamagnetism and the Meissner Effect

The first London equation alone is insufficient to explain the Meissner effect. It describes perfect conductivity, but not [perfect diamagnetism](@entry_id:203008). To derive the second, crucial part of the theory, we combine the first London equation with Maxwell's-Faraday's law of induction, $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$. Taking the curl of the first London equation gives:

$\nabla \times \left(\frac{\partial \mathbf{J}_s}{\partial t}\right) = \frac{\partial}{\partial t}(\nabla \times \mathbf{J}_s) = \frac{n_s e^2}{m} (\nabla \times \mathbf{E})$

Substituting Faraday's law yields:

$\frac{\partial}{\partial t}(\nabla \times \mathbf{J}_s) = -\frac{n_s e^2}{m} \frac{\partial \mathbf{B}}{\partial t}$

This can be rearranged into the form $\frac{\partial}{\partial t} \left( \nabla \times \mathbf{J}_s + \frac{n_s e^2}{m} \mathbf{B} \right) = \mathbf{0}$. This implies that the quantity in parentheses is constant in time. The Londons made a profound physical leap by postulating that this constant of integration is not just constant, but is identically zero. This postulate elevates the theory beyond that of a simple [perfect conductor](@entry_id:273420) and is the key to describing the Meissner effect. With this postulate, we arrive at the **second London equation** [@problem_id:3001730]:

$\nabla \times \mathbf{J}_s = - \frac{n_s e^2}{m} \mathbf{B}$

This equation provides a direct, local relationship between the supercurrent and the magnetic field $\mathbf{B}$ at the same point in space. It asserts that a static magnetic field inside a superconductor is necessarily accompanied by spatially varying screening currents. Note that both $\mathbf{J}_s$ and $\mathbf{B}$ are physically observable and gauge-invariant quantities, making this equation manifestly gauge-invariant.

#### Superconductors vs. Perfect Conductors: The Essence of the Meissner Effect

The two London equations together define the electromagnetic response of a superconductor. It is instructive to contrast this with the behavior of a hypothetical "[perfect conductor](@entry_id:273420)," defined as a material with zero resistivity ($\rho=0$) but without the constraint of the second London equation.

For a perfect conductor, Ohm's law, $\mathbf{E} = \rho \mathbf{J}$, implies that for any finite current, the electric field inside must be zero, $\mathbf{E}=0$. From Faraday's law, $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$, this immediately leads to $\frac{\partial \mathbf{B}}{\partial t} = \mathbf{0}$. This means the magnetic field inside a perfect conductor can never change.

This simple law leads to a **history-dependent** magnetic response. If a material is cooled to its perfectly conducting state in the presence of a magnetic field, that field becomes trapped inside. If the material is first cooled in zero field and then a field is applied, the conductor will generate surface currents to prevent the field from entering, keeping the interior field at zero [@problem_id:3001691].

A superconductor behaves differently. The second London equation is a [constitutive relation](@entry_id:268485) that must hold in the final [thermodynamic state](@entry_id:200783), regardless of how that state was reached. It demands that any static magnetic field be screened by supercurrents. This leads to the active expulsion of magnetic flux—the Meissner effect—which is not predicted for a [perfect conductor](@entry_id:273420). Thus, the Meissner effect is a distinct thermodynamic property of the superconducting state, not merely a consequence of perfect conductivity [@problem_id:3001720].

### Magnetic Field Penetration and the Screening Current

The second London equation predicts that magnetic fields will be screened by supercurrents. We can now quantify this [screening effect](@entry_id:143615) and introduce one of the most important [characteristic length scales](@entry_id:266383) in superconductivity.

#### The London Penetration Depth

Let's combine the second London equation with the magnetostatic form of Ampère's law, $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$, where $\mu_0$ is the [permeability of free space](@entry_id:276113). Taking the curl of Ampère's law gives:

$\nabla \times (\nabla \times \mathbf{B}) = \mu_0 (\nabla \times \mathbf{J}_s)$

Using the vector identity $\nabla \times (\nabla \times \mathbf{V}) = \nabla(\nabla \cdot \mathbf{V}) - \nabla^2 \mathbf{V}$ and the fundamental law $\nabla \cdot \mathbf{B} = 0$, the left-hand side simplifies to $-\nabla^2 \mathbf{B}$. Substituting the second London equation on the right-hand side yields:

$-\nabla^2 \mathbf{B} = \mu_0 \left( - \frac{n_s e^2}{m} \mathbf{B} \right)$

This gives the governing differential equation for the magnetic field inside a superconductor:

$\nabla^2 \mathbf{B} = \frac{\mu_0 n_s e^2}{m} \mathbf{B}$

This equation shows that the magnetic field does not abruptly drop to zero at the surface but rather decays in a characteristic manner. We can define a parameter with units of length, the **London [penetration depth](@entry_id:136478)** $\lambda_L$, such that:

$\lambda_L^2 = \frac{m}{\mu_0 n_s e^2}$

The field equation then becomes a standard Helmholtz-type equation:

$\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}$

To see the physical meaning of $\lambda_L$, consider a superconductor occupying the half-space $x>0$ with a magnetic field $\mathbf{B}_0$ applied parallel to the surface. The solution to the one-dimensional equation $\frac{d^2 B}{dx^2} = \frac{B}{\lambda_L^2}$ that decays into the bulk is an [exponential function](@entry_id:161417) [@problem_id:3001692] [@problem_id:3001730]:

$\mathbf{B}(x) = \mathbf{B}_0 \exp(-x/\lambda_L)$

This result demonstrates that the magnetic field is expelled from the interior of the superconductor, penetrating only a thin surface layer of characteristic thickness $\lambda_L$. Typical values for $\lambda_L$ in [conventional superconductors](@entry_id:275247) are in the range of 50-500 nanometers.

The expression for $\lambda_L$ reveals its dependence on the material's properties. The [penetration depth](@entry_id:136478) increases with the carrier mass ($ \lambda_L \propto \sqrt{m} $) and decreases with the [superfluid density](@entry_id:142018) ($ \lambda_L \propto 1/\sqrt{n_s} $). A "heavier" or less dense superfluid is less effective at screening fields, allowing them to penetrate further [@problem_id:3001692].

#### The Energetics of Screening

The expulsion of a magnetic field is not without cost. The supercurrents required for screening carry kinetic energy. The total free energy of the system must balance the [magnetic field energy](@entry_id:268850) with this kinetic energy.

The kinetic energy density of the supercurrent can be written as $f_k = \frac{1}{2} n_s m v_s^2$. Using the relations $\mathbf{J}_s = n_s e \mathbf{v}_s$ and the result from Ampere's law for the half-space geometry, $|\mathbf{J}_s| = \frac{1}{\mu_0} |\frac{d\mathbf{B}}{dx}| = \frac{|\mathbf{B}|}{\mu_0 \lambda_L}$, one can derive a remarkable local relationship [@problem_id:3001721]:

$f_k(x) = \frac{1}{2} n_s m \left( \frac{|\mathbf{J}_s|}{n_s e} \right)^2 = \frac{m}{2 n_s e^2} |\mathbf{J}_s|^2 = \frac{m}{2 n_s e^2} \left( \frac{|\mathbf{B}(x)|}{\mu_0 \lambda_L} \right)^2$

Substituting the definition $\lambda_L^2 = \frac{m}{\mu_0 n_s e^2}$, we find:

$f_k(x) = \frac{\mu_0 \lambda_L^2}{2} \left( \frac{|\mathbf{B}(x)|}{\mu_0 \lambda_L} \right)^2 = \frac{|\mathbf{B}(x)|^2}{2\mu_0}$

This reveals that the kinetic energy density of the screening current at any point is exactly equal to the [magnetic energy density](@entry_id:193006) at that same point. The exponential decay profile is the precise configuration that minimizes the total free energy, representing the optimal compromise between lowering the magnetic energy inside the superconductor and paying the kinetic energy cost to do so [@problem_id:3001691].

From a thermodynamic perspective, the superconducting state is stable because the energy gained by the electrons forming Cooper pairs, known as the **[condensation energy](@entry_id:195476)**, outweighs the energy costs associated with field expulsion. This competition defines the thermodynamic [critical field](@entry_id:143575), $H_c$. If an external applied field $H_a$ exceeds $H_c$, the [magnetic energy](@entry_id:265074) cost becomes too high, and it is more favorable for the material to revert to the normal, non-superconducting state. For a bulk sample, the superconducting state is stable when $H_a  H_c$ [@problem_id:3001711].

### Beyond the Isotropic Model: Advanced Topics

The simple London model is powerful, but real materials introduce complexities such as crystalline anisotropy and [many-body interactions](@entry_id:751663). These effects can be incorporated by refining the parameters of the London theory.

#### Anisotropy and the Effective Mass Tensor

Many superconducting materials, particularly high-temperature superconductors, have [crystal structures](@entry_id:151229) that are highly anisotropic. In such materials, the mobility of an electron depends on its direction of motion. This is captured by replacing the scalar effective mass $m$ with an **[effective mass tensor](@entry_id:147018)** $\hat{m}$. In a coordinate system aligned with the principal crystal axes, this tensor is diagonal: $\hat{m} = \mathrm{diag}(m_a, m_b, m_c)$.

The inertial response to an electric field becomes anisotropic, and the first London equation generalizes to a tensor relation. This carries through to the second London equation, which in the London gauge ($\mathbf{J}_s = -\hat{\Lambda}\mathbf{A}$) is expressed with a diagonal superfluid rigidity tensor $\hat{\Lambda}$ [@problem_id:3001705]:

$\mathbf{J}_s = - \begin{pmatrix} n_s e^2/m_a   0  0 \\ 0  n_s e^2/m_b  0 \\ 0  0  n_s e^2/m_c \end{pmatrix} \mathbf{A}$

This leads to three distinct penetration depths, one for screening currents flowing in each principal plane, which screen fields oriented along the corresponding axis:

$\lambda_i = \sqrt{\frac{m_i}{\mu_0 n_s e^2}}$, for $i \in \{a, b, c\}$

A larger effective mass along a certain axis implies a larger [penetration depth](@entry_id:136478) for fields oriented perpendicular to that axis, as the heavier carriers are less effective at establishing screening currents.

#### Renormalization of the Penetration Depth

The mass $m$ appearing in the formula for $\lambda_L$ is the *[inertial mass](@entry_id:267233)* of the superconducting carriers. Identifying its correct physical value requires going beyond the [phenomenological model](@entry_id:273816). In a real solid, the mass is modified by two primary effects: the crystal lattice and [many-body interactions](@entry_id:751663).

In a crystal, electrons move in a [periodic potential](@entry_id:140652), and their response to external forces is governed by their **band effective mass** $m_b$, which can be very different from the free electron mass. Furthermore, interactions between electrons (e.g., via exchange of [lattice vibrations](@entry_id:145169), or phonons) "dress" the electrons, turning them into quasiparticles with a renormalized **[quasiparticle effective mass](@entry_id:140437)** $m^*$.

A crucial distinction arises depending on the system's underlying symmetries. In a hypothetical Galilean-invariant system (like a [uniform electron gas](@entry_id:163911)), a principle from Landau's Fermi-liquid theory shows that the effects of [mass renormalization](@entry_id:139777) on the total current are exactly cancelled by "backflow" currents in the interacting liquid. As a result, the current response depends only on the bare carrier mass, not the enhanced $m^*$ [@problem_id:3001722].

However, a real crystal lattice breaks Galilean invariance. The lattice itself can absorb momentum. In this case, the backflow cancellation is incomplete, and the [inertial mass](@entry_id:267233) that governs the supercurrent response is indeed the renormalized quasiparticle mass $m^*$. Since interactions typically increase the effective mass ($m^* > m_b$), stronger coupling (e.g., strong [electron-phonon interaction](@entry_id:140708)) leads to a larger [inertial mass](@entry_id:267233). Consequently, [strong-coupling superconductors](@entry_id:140567) are expected to have a *larger* penetration depth than predicted from their [band structure](@entry_id:139379) alone [@problem_id:3001722]. This is a key insight connecting microscopic [many-body physics](@entry_id:144526) to a macroscopic, measurable quantity.

#### The Limits of Locality: Nonlocal Electrodynamics

The London model is a **local theory**: it assumes the supercurrent $\mathbf{J}_s(\mathbf{r})$ at a point $\mathbf{r}$ is determined solely by the fields at that same point. This assumption is valid only if the [characteristic length](@entry_id:265857) scale of field variations, $\lambda_L$, is much larger than the intrinsic size of the Cooper pairs, described by the **coherence length** $\xi$. Superconductors where $\lambda_L \gg \xi$ are called **London superconductors**.

In many materials, especially very clean ones, the opposite is true: $\lambda_L \ll \xi$. These are **Pippard superconductors**. In this **nonlocal regime**, a Cooper pair "sees" the [electromagnetic potential](@entry_id:264816) averaged over its size $\xi$. The current at point $\mathbf{r}$ then depends on the vector potential $\mathbf{A}(\mathbf{r}')$ in a whole neighborhood around $\mathbf{r}$. The [constitutive relation](@entry_id:268485) becomes an integral:

$\mathbf{J}_s(\mathbf{r}) = -\int K(\mathbf{r}-\mathbf{r}') \mathbf{A}(\mathbf{r}') d^3r'$

Here, $K(\mathbf{r}-\mathbf{r}')$ is the nonlocal electromagnetic response kernel, which decays over the length scale $\xi$.

Nonlocality has observable consequences, particularly in the low-temperature behavior of the penetration depth. For [unconventional superconductors](@entry_id:141195) with nodes (zeros) in their energy gap, such as $d$-wave superconductors, the local theory predicts that the change in penetration depth at low temperatures is linear: $\Delta\lambda(T) = \lambda(T) - \lambda(0) \propto T$. However, in clean samples at very low temperatures, the response becomes nonlocal. This leads to a crossover to a different temperature dependence, $\Delta\lambda(T) \propto T^2$. The observation of this crossover is a powerful experimental tool for probing the nonlocal nature of electrodynamics and the [nodal structure](@entry_id:151019) of the superconducting gap. Furthermore, because the response is wavevector-dependent, measurements of $\lambda(T)$ can become sensitive to the experimental geometry and probe, another hallmark of nonlocality [@problem_id:3001662].