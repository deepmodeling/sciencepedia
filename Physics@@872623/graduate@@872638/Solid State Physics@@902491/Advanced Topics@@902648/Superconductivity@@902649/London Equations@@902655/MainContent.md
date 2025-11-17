## Introduction
Superconductivity, the remarkable phenomenon of [zero electrical resistance](@entry_id:151583) and the expulsion of magnetic fields, challenged physicists for decades. While early models could account for perfect conductivity, they failed to explain the active field expulsion known as the Meissner effect, a defining feature of the superconducting state. The London equations, developed by brothers Fritz and Heinz London, provided the first successful phenomenological framework to unify these two properties. This article explores this foundational theory, offering a graduate-level understanding of the [electrodynamics](@entry_id:158759) of superconductors.

In the following chapters, we will embark on a structured journey through this pivotal theory. The **Principles and Mechanisms** chapter will derive the two London equations from first principles, revealing how they describe the inertia of the superconducting fluid and lead directly to the concept of a finite [magnetic penetration depth](@entry_id:140378). Building on this foundation, the **Applications and Interdisciplinary Connections** chapter will explore the far-reaching utility of the London model, from explaining current distribution in superconducting wires and magnetic levitation to its connections with fundamental mechanics and materials science. Finally, the **Hands-On Practices** section will offer a series of guided problems to reinforce these concepts and develop practical problem-solving skills.

## Principles and Mechanisms

The phenomenological theory of superconductivity developed by Fritz and Heinz London provides a remarkably successful description of the macroscopic electrodynamic properties of superconductors. This framework is built upon two fundamental equations that, when combined with Maxwell's equations, encapsulate the two defining characteristics of the superconducting state: [zero electrical resistance](@entry_id:151583) and the expulsion of magnetic fields, known as the Meissner effect. This chapter will derive these equations from first principles, explore their physical interpretations, and examine their profound consequences.

### The First London Equation: The Inertia of the Superfluid

The defining feature of a superconductor is the unimpeded flow of charge. To model this, we consider the charge carriers in the superconducting state—the **superfluid** composed of Cooper pairs—as a charged fluid that experiences no scattering or frictional forces. The motion of an individual superconducting charge carrier, with charge $q$ and effective mass $m$, in the presence of an electric field $\mathbf{E}$ is therefore governed by Newton's second law in its purest form: the rate of change of momentum is equal to the applied force.

$$ m \frac{d\mathbf{v}_s}{dt} = q\mathbf{E} $$

Here, $\mathbf{v}_s$ is the drift velocity of the superfluid. This equation describes a purely inertial response: the carriers accelerate as long as an electric field is present. This stands in stark contrast to a normal conductor, where scattering leads to a terminal drift velocity proportional to the field, as described by Ohm's law.

The supercurrent density, $\mathbf{J}_s$, is related to the number density of superconducting carriers, $n_s$, and their velocity by the standard definition:

$$ \mathbf{J}_s = n_s q \mathbf{v}_s $$

By convention, even though the charge carriers are Cooper pairs (with charge $q=-2e$ and mass $m_p \approx 2m_e$), it is standard to express the London equations in terms of the properties of individual electrons. We therefore let $n_s$ represent the number density of *superconducting electrons*, and use the electron charge $q=-e$ and effective mass $m$. Taking the time derivative of the [current density](@entry_id:190690) equation (assuming $n_s$ is constant in time) yields:

$$ \frac{\partial \mathbf{J}_s}{\partial t} = n_s q \frac{\partial \mathbf{v}_s}{\partial t} $$

Substituting the acceleration from Newton's law gives:

$$ \frac{\partial \mathbf{J}_s}{\partial t} = n_s q \left( \frac{q\mathbf{E}}{m} \right) = \frac{n_s q^2}{m} \mathbf{E} $$

Using $q=-e$, the equation takes its final form, known as the **first London equation**:

$$ \frac{\partial \mathbf{J}_s}{\partial t} = \frac{n_s e^2}{m} \mathbf{E} $$

This equation is a formal statement of perfect conductivity. It implies that any non-zero electric field will cause the supercurrent to increase linearly with time. Conversely, and perhaps more importantly, in the absence of an electric field ($\mathbf{E}=0$), the supercurrent does not change: $\frac{\partial \mathbf{J}_s}{\partial t} = 0$. This is the origin of **[persistent currents](@entry_id:146997)**. Once a current is established in a superconducting loop, it will flow indefinitely without any driving voltage, as there are no dissipative mechanisms to slow the charge carriers down [@problem_id:3001688].

The inertia of the charge carriers, which causes this resistance to changes in current, can be quantified as an electrical property known as **[kinetic inductance](@entry_id:141594)**. For a conductor of length $l$ and cross-sectional area $A$, the voltage drop is $V = El$. The total current is $I_s = J_s A$. The first London equation can be rewritten as $E = \frac{m}{n_s e^2} \frac{\partial J_s}{\partial t}$. Substituting these relations, we find:

$$ V = \left( \frac{ml}{n_s e^2 A} \right) \frac{dI_s}{dt} $$

This is precisely the form of the voltage-current relation for an inductor, $V = L_k \frac{dI}{dt}$, where the [kinetic inductance](@entry_id:141594) per unit length is $\frac{L_k}{l} = \frac{m}{n_s e^2 A}$. This [inductance](@entry_id:276031) is an intrinsic property of the superconductor, arising not from magnetic fields but from the kinetic energy of the accelerating superfluid. For a non-uniform conductor, such as a tapered wire, the total [kinetic inductance](@entry_id:141594) can be found by integrating this quantity over the length of the wire [@problem_id:144605].

### The Second London Equation and the Meissner Effect

While the first London equation successfully describes perfect conductivity, it is insufficient on its own to explain the Meissner effect—the active expulsion of magnetic fields from the interior of a superconductor. To understand why, consider what the first London equation implies when combined with Faraday's law of induction, $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$. The condition for a static supercurrent, $\frac{\partial \mathbf{J}_s}{\partial t} = 0$, implies from the first London equation that $\mathbf{E}=0$ inside the superconductor. Substituting this into Faraday's law gives:

$$ \frac{\partial \mathbf{B}}{\partial t} = 0 $$

This equation describes a "perfect conductor" but not a superconductor. It predicts that the magnetic field inside the material cannot change with time. If a material in its normal state is placed in a magnetic field and then cooled below its critical temperature (a process known as field-cooling), this model predicts that the initial magnetic flux would be trapped within the material. This directly contradicts experimental observations of the Meissner effect, where the flux is actively expelled during the transition [@problem_id:58079] [@problem_id:3001691].

The Meissner effect is therefore a distinct thermodynamic property of the superconducting ground state, not merely a consequence of perfect conductivity. To incorporate it into the theory, the Londons proposed a second, independent constraint. This second equation can be elegantly derived by taking the curl of the first London equation:

$$ \nabla \times \left( \frac{\partial \mathbf{J}_s}{\partial t} \right) = \nabla \times \left( \frac{n_s e^2}{m} \mathbf{E} \right) $$

Assuming a homogeneous superconductor where $n_s$ is spatially constant, and interchanging the time and space derivatives, we get:

$$ \frac{\partial}{\partial t} \left( \nabla \times \mathbf{J}_s \right) = \frac{n_s e^2}{m} (\nabla \times \mathbf{E}) $$

Using Faraday's law, $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$:

$$ \frac{\partial}{\partial t} \left( \nabla \times \mathbf{J}_s \right) = -\frac{n_s e^2}{m} \frac{\partial \mathbf{B}}{\partial t} \quad \implies \quad \frac{\partial}{\partial t} \left( \nabla \times \mathbf{J}_s + \frac{n_s e^2}{m} \mathbf{B} \right) = 0 $$

This shows that the quantity $\left( \nabla \times \mathbf{J}_s + \frac{n_s e^2}{m} \mathbf{B} \right)$ must be constant in time. The crucial physical insight of the London theory is to postulate that this constant of integration is identically zero. This can be justified by considering that when the material is in its normal state ($T > T_c$), there is no supercurrent ($\mathbf{J}_s=0$) and if it is cooled in zero magnetic field ($\mathbf{B}=0$), the constant must be zero. The postulate is that this relationship holds true for the superconducting state regardless of its history. This yields the **second London equation**:

$$ \nabla \times \mathbf{J}_s = -\frac{n_s e^2}{m} \mathbf{B} $$

This local equation relates the curl of the supercurrent density at a point directly to the magnetic field at that same point. It is a manifestly **gauge-invariant** relation, as both $\mathbf{J}_s$ and $\mathbf{B}$ are physically observable quantities that are independent of the choice of electromagnetic gauge [@problem_id:3001730]. An alternative, but less fundamental, formulation is sometimes given as $\mathbf{J}_s = -\frac{n_s e^2}{m}\mathbf{A}$, where $\mathbf{A}$ is the magnetic vector potential ($\mathbf{B} = \nabla \times \mathbf{A}$). While this relation correctly yields the second London equation upon taking the curl, it is not gauge-invariant and is only valid in a specific gauge choice (the London gauge, where $\nabla \cdot \mathbf{A} = 0$) [@problem_id:1818587].

### Consequences: Field Expulsion and the Penetration Depth

The second London equation is the key to describing the Meissner effect. By combining it with the static form of Ampere's law, $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$ (assuming non-magnetic material), we can derive the governing equation for the magnetic field inside a superconductor. Taking the curl of Ampere's law:

$$ \nabla \times (\nabla \times \mathbf{B}) = \mu_0 (\nabla \times \mathbf{J}_s) $$

Using the vector identity $\nabla \times (\nabla \times \mathbf{B}) = \nabla(\nabla \cdot \mathbf{B}) - \nabla^2 \mathbf{B}$ and Maxwell's equation $\nabla \cdot \mathbf{B} = 0$, the left side becomes $-\nabla^2 \mathbf{B}$. Substituting the second London equation into the right side gives:

$$ -\nabla^2 \mathbf{B} = \mu_0 \left( -\frac{n_s e^2}{m} \mathbf{B} \right) $$

This simplifies to the fundamental field equation for a London superconductor:

$$ \nabla^2 \mathbf{B} = \left( \frac{\mu_0 n_s e^2}{m} \right) \mathbf{B} $$

This equation predicts that the magnetic field cannot remain uniform inside a superconductor. It must have a non-zero second spatial derivative, meaning it must curve. We can identify a characteristic length scale from this equation, the **London [penetration depth](@entry_id:136478)**, $\lambda_L$, defined by:

$$ \lambda_L^2 = \frac{m}{\mu_0 n_s e^2} $$

The field equation then takes the elegant form $\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}$. For a simple geometry, such as a superconductor occupying the half-space $z > 0$ with a [uniform magnetic field](@entry_id:263817) $B_s$ applied parallel to the surface at $z=0$, this equation becomes $\frac{d^2B}{dz^2} = \frac{B}{\lambda_L^2}$. The physically valid solution, which decays into the bulk of the material, is an exponential:

$$ B(z) = B_s \exp\left(-\frac{z}{\lambda_L}\right) $$

This result is the mathematical expression of the Meissner effect. It shows that the magnetic field is expelled from the bulk of the superconductor, penetrating only a thin surface layer. The London [penetration depth](@entry_id:136478) $\lambda_L$ is precisely the distance over which the magnetic field strength decays to $1/e$ (approximately $0.368$) of its value at the surface [@problem_id:1818541]. For a typical superconductor like tin, with $n_s \approx 1.30 \times 10^{28} \text{ m}^{-3}$, the [penetration depth](@entry_id:136478) is on the order of tens of nanometers, for example, $\lambda_L \approx 46.6$ nm [@problem_id:1818587].

The expression for $\lambda_L$ reveals its dependence on the material's intrinsic properties: $\lambda_L \propto \sqrt{m/n_s}$. Materials with a lower density of superconducting carriers ($n_s$) or carriers with a higher effective mass ($m$) are less effective at screening magnetic fields and thus have a larger [penetration depth](@entry_id:136478) [@problem_id:3001692]. The screening mechanism itself can be understood as an [energy balance](@entry_id:150831): the system minimizes its total free energy by allowing the field to penetrate a short distance, incurring some [magnetic field energy](@entry_id:268850), in order to avoid the high kinetic energy cost of generating an infinitely sharp surface current that would be required for [perfect field](@entry_id:156337) expulsion [@problem_id:3001691].

### Advanced Applications and Limitations

The London formalism can be extended to more complex scenarios, revealing rich physics.

#### Multiply Connected Geometries: Flux Trapping

Consider a superconductor with a hole, such as a ring. We can define a closed loop $C$ deep within the bulk of the ring where, due to the Meissner effect, the supercurrent density $\mathbf{J}_s$ is effectively zero. Integrating the first London equation along this loop gives:

$$ \oint_C \mathbf{E} \cdot d\mathbf{l} = \oint_C \frac{m}{n_s e^2} \frac{\partial \mathbf{J}_s}{\partial t} \cdot d\mathbf{l} \approx 0 $$

From Faraday's law, the left-hand side is the negative time derivative of the total magnetic flux $\Phi$ passing through the loop, $-\frac{d\Phi}{dt}$. Therefore, we find that $\frac{d\Phi}{dt} = 0$. This implies that the total magnetic flux enclosed by the superconducting ring must remain constant. If the ring is cooled below its critical temperature while in a magnetic field, the flux from that field becomes trapped. If the external field is then removed, a [persistent supercurrent](@entry_id:276122) will be induced to maintain this trapped flux. This phenomenon is known as **[flux trapping](@entry_id:196395)** [@problem_id:1818545].

#### Inhomogeneous Superconductors

The local nature of the London equations allows them to be applied even when material properties, such as the [superfluid density](@entry_id:142018) $n_s$, vary in space. In such a case, the penetration depth becomes a position-dependent function, $\lambda_L(\mathbf{r})$. The governing field equation, $\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2(\mathbf{r})} \mathbf{B}$, remains valid. Solving this equation for a specific profile of $n_s(\mathbf{r})$ can lead to more complex field distributions, such as those described by modified Bessel functions, but the fundamental principle of field screening remains [@problem_id:144470].

#### Limitations of the London Model

The London theory, being linear and local, has its limits. It implicitly assumes that the [superfluid density](@entry_id:142018) $n_s$ is constant and does not respond to the magnetic field itself. This approximation breaks down when the fields or currents cause the superconducting properties to vary rapidly over short distances. The [characteristic length](@entry_id:265857) scale for variations in the superconducting state is the **Ginzburg-Landau [coherence length](@entry_id:140689)**, $\xi$. The London model is generally valid only for distances much larger than $\xi$.

A prime example of this breakdown is the core of an **Abrikosov vortex** in a Type-II superconductor. A vortex is a filament of normal (non-superconducting) material, with a radius on the order of $\xi$, that carries a single quantum of magnetic flux. The London model, when applied to a vortex, incorrectly predicts a magnetic field that diverges logarithmically as one approaches the center ($r \to 0$). This is unphysical. The more advanced Ginzburg-Landau theory shows that the superconducting order parameter is suppressed to zero within the core, and the magnetic field is capped at a value known as the [upper critical field](@entry_id:139431), $B_{c2} = \frac{\Phi_0}{2\pi \xi^2}$. By comparing the diverging London prediction with this physical limit, one can define a critical radius below which the London model fails, marking the boundary of the [vortex core](@entry_id:159858) [@problem_id:1818563]. This highlights that while powerful, the London equations represent a macroscopic approximation of a more complex microscopic reality.