## Introduction
The discovery of superconductivity presented a profound challenge to classical physics, revealing materials with [zero electrical resistance](@entry_id:151583) and the mystifying ability to expel magnetic fields—the Meissner effect. The first successful theoretical step towards explaining these phenomena was the [phenomenological model](@entry_id:273816) developed by Fritz and Heinz London in 1935. The London equations provide a powerful and intuitive electrodynamic description of the superconducting state, bridging the gap between experimental observation and a deeper quantum understanding. This article provides a comprehensive exploration of this cornerstone theory. The first chapter, "Principles and Mechanisms," derives the two London equations and introduces the key concept of the [penetration depth](@entry_id:136478). Building on this foundation, "Applications and Interdisciplinary Connections" explores the far-reaching consequences of the theory, from [magnetic levitation](@entry_id:275771) and quantum computing components to a surprising link with the Higgs mechanism in particle physics. Finally, "Hands-On Practices" will allow you to apply these principles to solve practical problems in superconductivity. We begin our journey by examining the fundamental principles that govern the [frictionless flow](@entry_id:195983) of a supercurrent.

## Principles and Mechanisms

Following our introduction to the remarkable phenomena of superconductivity, we now develop a theoretical framework to describe its electromagnetic properties. The London equations, formulated by brothers Fritz and Heinz London in 1935, provide a powerful phenomenological description that successfully captures the two defining characteristics of superconductors: [zero electrical resistance](@entry_id:151583) and the Meissner effect. This chapter will derive these equations from fundamental principles, explore their profound consequences, and define their limits of applicability.

### The First London Equation and Perfect Conductivity

Let us first consider the property of zero DC electrical resistance, or **perfect conductivity**. In a normal conductor, the flow of electrons is impeded by scattering from [lattice vibrations](@entry_id:145169) (phonons) and impurities. This opposition to current flow is quantified by electrical resistivity, $\rho$. An applied electric field, $\mathbf{E}$, drives a [current density](@entry_id:190690), $\mathbf{J}$, that quickly reaches a steady state where the accelerating force of the field is balanced by this dissipative drag. This leads to Ohm's law, $\mathbf{J} = \mathbf{E}/\rho$.

In a superconductor, a fraction of electrons condense into a macroscopic quantum state, forming a frictionless superfluid of **Cooper pairs**. These charge carriers move without scattering or energy loss. To model the dynamics of this supercurrent, we can apply Newton's second law directly to a superconducting charge carrier of mass $m^*$ and charge $q$. The only force acting on it in the presence of an electric field $\mathbf{E}$ is the [electric force](@entry_id:264587), $\mathbf{F} = q\mathbf{E}$. Therefore, its acceleration, $\frac{d\mathbf{v}_s}{dt}$, is given by:

$m^* \frac{d\mathbf{v}_s}{dt} = q\mathbf{E}$

The supercurrent density, $\mathbf{J}_s$, is defined as the product of the number density of superconducting carriers, $n_s$, their charge, $q$, and their [average velocity](@entry_id:267649), $\mathbf{v}_s$. Thus, $\mathbf{J}_s = n_s q \mathbf{v}_s$. To find the relationship between the current and the electric field, we can differentiate this expression with respect to time. Assuming $n_s$ is constant, we obtain:

$\frac{\partial \mathbf{J}_s}{\partial t} = n_s q \frac{\partial \mathbf{v}_s}{\partial t}$

Substituting the expression for the acceleration from Newton's law yields a profound result [@problem_id:3001688]:

$\frac{\partial \mathbf{J}_s}{\partial t} = \frac{n_s q^2}{m^*} \mathbf{E}$

This is the **First London Equation**. It reveals a fundamentally different electrodynamic response compared to a normal conductor. An electric field in a superconductor does not sustain a constant current; instead, it causes the supercurrent to accelerate indefinitely. The carriers exhibit a purely inertial response, free from any [dissipative forces](@entry_id:166970).

A direct and crucial consequence of this equation is the phenomenon of perfect conductivity. If a steady, time-independent (DC) supercurrent is flowing, then $\frac{\partial \mathbf{J}_s}{\partial t} = 0$. Since the prefactor $\frac{n_s q^2}{m^*}$ is non-zero, the First London Equation immediately requires that the static electric field inside the superconductor must be zero [@problem_id:1821281]:

$\mathbf{E} = \mathbf{0}$

This confirms that a superconductor can sustain a persistent DC current with no internal electric field and, consequently, no [energy dissipation](@entry_id:147406) ($P = \mathbf{J}_s \cdot \mathbf{E} = 0$). Once established, a supercurrent will flow forever without any driving voltage, a defining feature of the superconducting state [@problem_id:3001688].

### The Meissner Effect and the Second London Equation

While the First London Equation successfully describes perfect conductivity, it is insufficient to explain the complete electrodynamics of a superconductor. A "[perfect conductor](@entry_id:273420)" described solely by this equation would behave differently from an actual superconductor when cooled in the presence of a magnetic field.

To understand why, let us combine the First London Equation with Faraday's law of induction, $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$. Taking the curl of the first London equation gives:

$\nabla \times \left( \frac{\partial \mathbf{J}_s}{\partial t} \right) = \nabla \times \left( \frac{n_s q^2}{m^*} \mathbf{E} \right) = \frac{n_s q^2}{m^*} (\nabla \times \mathbf{E})$

Assuming spatial and temporal derivatives can be interchanged, and substituting Faraday's law, we get:

$\frac{\partial}{\partial t} \left( \nabla \times \mathbf{J}_s \right) = - \frac{n_s q^2}{m^*} \frac{\partial \mathbf{B}}{\partial t}$

This can be integrated with respect to time to show that the quantity $\left( \frac{m^*}{n_s q^2} \nabla \times \mathbf{J}_s + \mathbf{B} \right)$ must be constant in time.

Now, consider a thought experiment [@problem_id:58079]. A material is placed in a uniform magnetic field $\mathbf{B}_{ext}$ while it is in its normal state ($T > T_c$). Inside the normal material, the field is $\mathbf{B}_{ext}$ and there is no supercurrent, so $\mathbf{J}_s = 0$. The material is then cooled below its critical temperature $T_c$. According to the logic of perfect conductivity alone, the time-constant quantity we just derived must retain its initial value. Since $\mathbf{J}_s$ was initially zero, the expression $\frac{m^*}{n_s q^2} \nabla \times \mathbf{J}_s$ is zero. Therefore, the magnetic field $\mathbf{B}$ inside the material must remain constant throughout the cooling process. The final state would be a superconductor with the initial magnetic field $\mathbf{B}_{ext}$ trapped inside.

However, experiments show the opposite. A superconductor actively expels magnetic fields from its interior as it cools through $T_c$. This phenomenon is the **Meissner effect**. This implies that the final state must be $\mathbf{B} = 0$ inside the bulk, regardless of the field history. Perfect conductivity alone cannot account for this; an additional physical principle is required.

The London brothers postulated this principle as their second equation. To ensure that the magnetic field is always expelled in the superconducting state, they required that the time-invariant quantity be not just a constant, but zero. This leads to the **Second London Equation**:

$\nabla \times \mathbf{J}_s = - \frac{n_s q^2}{m^*} \mathbf{B}$

This equation is a new [constitutive relation](@entry_id:268485) for a superconductor, independent of the first. It links the spatial variation of the supercurrent directly to the local magnetic field. It imposes the Meissner effect as an intrinsic property of the superconducting state.

A more direct form of this equation relates the supercurrent to the magnetic vector potential, $\mathbf{A}$ (where $\mathbf{B} = \nabla \times \mathbf{A}$). By choosing a specific gauge, the **London gauge**, defined by $\nabla \cdot \mathbf{A} = 0$, the Second London Equation simplifies to a local relationship [@problem_id:1818570]:

$\mathbf{J}_s = - \frac{n_s q^2}{m^*} \mathbf{A}$

This choice is particularly convenient because it expresses the supercurrent as a simple, direct response to the [vector potential](@entry_id:153642) itself, greatly simplifying calculations.

### The London Penetration Depth

The Second London Equation predicts not just that the magnetic field is expelled, but it also quantifies *how* it is expelled. Combining this new law with Maxwell's equations reveals the spatial profile of the magnetic field at the boundary of a superconductor. We begin with the static form of Ampere's law, which relates the magnetic field to the supercurrent it generates:

$\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$

Here, $\mu_0$ is the [permeability of free space](@entry_id:276113). To obtain an equation solely for the magnetic field, we take the curl of this expression [@problem_id:1818587]:

$\nabla \times (\nabla \times \mathbf{B}) = \mu_0 (\nabla \times \mathbf{J}_s)$

Using the vector identity $\nabla \times (\nabla \times \mathbf{V}) = \nabla(\nabla \cdot \mathbf{V}) - \nabla^2 \mathbf{V}$ and the fundamental law $\nabla \cdot \mathbf{B} = 0$, the left side becomes $-\nabla^2 \mathbf{B}$. Substituting the Second London Equation for $\nabla \times \mathbf{J}_s$ on the right side gives:

$-\nabla^2 \mathbf{B} = \mu_0 \left( - \frac{n_s q^2}{m^*} \mathbf{B} \right)$

Rearranging this gives a Helmholtz-type equation for the magnetic field:

$\nabla^2 \mathbf{B} = \frac{\mu_0 n_s q^2}{m^*} \mathbf{B}$

This equation shows that the magnetic field inside a superconductor does not obey Laplace's equation ($\nabla^2 \mathbf{B} = 0$) as it would in a vacuum. The equation is conventionally written as:

$\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}$

where we have defined a characteristic length scale, the **London [penetration depth](@entry_id:136478)**, $\lambda_L$:

$$ \lambda_L = \sqrt{\frac{m^*}{\mu_0 n_s q^2}} $$

For the purposes of this conventional formula, the charge carriers are often treated as individual electrons, so $q = -e$ and $m^* = m_e$, where $n_s$ is then the density of superconducting electrons.

To understand the physical significance of $\lambda_L$, consider a simple geometry: a superconductor occupying the half-space $z > 0$, with a [uniform magnetic field](@entry_id:263817) $B_s \hat{\mathbf{x}}$ applied parallel to the surface at $z=0$ [@problem_id:1821269]. The governing equation simplifies to $\frac{d^2 B_x}{dz^2} = \frac{1}{\lambda_L^2} B_x$. The solution that decays to zero deep inside the superconductor ($z \to \infty$) is:

$B(z) = B_s \exp(-z/\lambda_L)$

This result demonstrates the Meissner effect in action: the magnetic field does not abruptly stop at the surface but penetrates a short distance, decaying exponentially. The London penetration depth $\lambda_L$ is the [characteristic length](@entry_id:265857) of this decay. At a depth of one [penetration depth](@entry_id:136478), $z = \lambda_L$, the magnetic field strength has fallen to $\exp(-1) \approx 0.368$ of its value at the surface [@problem_id:1818541]. For typical superconductors, $\lambda_L$ is on the order of tens to hundreds of nanometers.

The expression for $\lambda_L$ shows that it is inversely proportional to the square root of the superconducting [carrier density](@entry_id:199230), $\lambda_L \propto 1/\sqrt{n_s}$. Since $n_s$ decreases as the temperature $T$ approaches the critical temperature $T_c$, the penetration depth must increase with temperature. For instance, using the empirical Gorter-Casimir model, where $n_s(T) \propto [1 - (T/T_c)^4]$, the penetration depth diverges as $T \to T_c$, signifying the breakdown of the superconducting state [@problem_id:1818560].

### Screening Currents

The expulsion of the magnetic field from the bulk of a superconductor is not magic; it is an active electrodynamic process. The changing magnetic flux during cooldown induces electric fields, which, according to the First London Equation, drive the acceleration of supercurrents. These currents arrange themselves near the surface to generate a magnetic field that precisely cancels the external field in the interior.

These **screening currents** are confined to a layer of thickness on the order of $\lambda_L$. We can find their spatial distribution from Ampere's law, $\mathbf{J}_s = \frac{1}{\mu_0} \nabla \times \mathbf{B}$. For our one-dimensional example with $\mathbf{B}(z) = B_s \exp(-z/\lambda_L) \hat{\mathbf{x}}$, the [current density](@entry_id:190690) is [@problem_id:1821269]:

$\mathbf{J}_s(z) = \frac{1}{\mu_0} \left( -\frac{\partial B_x}{\partial z} \right) \hat{\mathbf{y}} = \frac{B_s}{\mu_0 \lambda_L} \exp(-z/\lambda_L) \hat{\mathbf{y}}$

This shows a sheet of current flowing perpendicular to the magnetic field, localized near the surface and decaying into the bulk with the same characteristic length $\lambda_L$. It is this layer of supercurrent that actively shields the superconductor's interior from the external magnetic field.

### Beyond the London Model: Quantum Effects and Limitations

The London theory is a brilliant phenomenological success, but it is fundamentally a classical model. The true nature of superconductivity is quantum mechanical. The charge carriers, **Cooper pairs**, are bound pairs of electrons with charge $q = -2e$ and effective mass $m^* \approx 2m_e$. One of the most striking macroscopic manifestations of this quantum origin is **[flux quantization](@entry_id:144492)**. In a ring-shaped superconductor, the requirement that the macroscopic [quantum wavefunction](@entry_id:261184) of the Cooper pairs be single-valued upon traversing the ring leads to a remarkable constraint: the total magnetic flux $\Phi$ trapped in the hole of the ring can only take on integer multiples of a fundamental constant, the **[magnetic flux quantum](@entry_id:136429)** $\Phi_0$ [@problem_id:1821297]:

$\Phi = n \Phi_0, \quad \text{where } n \in \mathbb{Z} \text{ and } \Phi_0 = \frac{h}{2e}$

The appearance of Planck's constant $h$ and the charge $2e$ is direct evidence of the underlying quantum pairing mechanism, something beyond the scope of the classical London equations.

Furthermore, the London theory has inherent limitations. It is a **local theory**, meaning the current at a point $\mathbf{r}$ depends only on the fields at that same point. It also assumes the density of superconducting carriers, $n_s$, is constant throughout the material. This approximation breaks down in situations where the superconducting properties themselves vary rapidly in space.

A prime example is the core of an Abrikosov vortex in a Type-II superconductor. The London model predicts a magnetic field that diverges logarithmically at the vortex center. This is unphysical. A more advanced description, the **Ginzburg-Landau theory**, introduces another fundamental length scale: the **[coherence length](@entry_id:140689)**, $\xi$. This length scale characterizes the distance over which the superconducting order parameter (related to $n_s$) can vary. The London equations are only valid on scales much larger than $\xi$. Inside the [vortex core](@entry_id:159858), for radial distances $r \lesssim \xi$, the density of superelectrons $n_s$ is suppressed, going to zero at the very center. The London model, by assuming a constant $n_s$, fails to capture this crucial physics and breaks down precisely in this region [@problem_id:1818563]. These limitations pave the way for the more comprehensive quantum theories of superconductivity that will be explored in subsequent chapters.