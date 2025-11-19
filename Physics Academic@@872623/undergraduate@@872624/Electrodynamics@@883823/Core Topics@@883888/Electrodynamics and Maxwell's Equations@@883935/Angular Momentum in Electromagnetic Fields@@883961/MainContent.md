## Introduction
In physics, angular momentum is typically associated with the rotation of massive objects. However, a deeper exploration of Maxwell's equations reveals a startling and profound concept: the electromagnetic field itself can carry angular momentum. This idea challenges the classical intuition that fields are merely a static backdrop for particle interactions, recasting them as dynamic entities that store and transport mechanical properties. This article addresses the conceptual gap between mechanical and field-based angular momentum, providing a unified view essential for modern physics. The following chapters will guide you from the fundamental principles and mechanisms governing [field angular momentum](@entry_id:268053), through its diverse applications and interdisciplinary connections in areas like optics and quantum mechanics, to a series of hands-on problems that solidify these abstract concepts. We begin by examining the core definitions and conservation laws that form the bedrock of this fascinating topic.

## Principles and Mechanisms

In our study of electromagnetism, we have grown accustomed to associating momentum and angular momentum with massive particles in motion. However, one of the most profound consequences of Maxwell's theory is that the electromagnetic field itself can be a repository for these mechanical quantities. The field is not merely a static stage upon which charges and currents interact; it is a dynamic entity that can carry energy, momentum, and angular momentum. This chapter explores the principles governing the angular momentum stored in [electromagnetic fields](@entry_id:272866) and the mechanisms by which it is generated and exchanged with matter.

### Momentum and Angular Momentum of the Field

The concept of momentum in the electromagnetic field is inextricably linked to the flow of energy. The Poynting vector, $\vec{S} = \frac{1}{\mu_0} (\vec{E} \times \vec{B})$, describes the energy flux density—the rate of [energy flow](@entry_id:142770) per unit area—at a point in space. It is a remarkable insight that this energy flow is accompanied by a momentum density. The [electromagnetic momentum](@entry_id:268129) density, denoted by $\vec{g}$, is given by:

$$
\vec{g} = \frac{\vec{S}}{c^2} = \epsilon_0 (\vec{E} \times \vec{B})
$$

where $\epsilon_0$ is the [permittivity of free space](@entry_id:272823) and $c = 1/\sqrt{\epsilon_0 \mu_0}$ is the speed of light. This equation tells us that wherever non-parallel electric and magnetic fields coexist, there is momentum stored in the field itself.

Just as the mechanical [angular momentum of a particle](@entry_id:178745) with momentum $\vec{p}$ at a position $\vec{r}$ is $\vec{L} = \vec{r} \times \vec{p}$, we can define an **electromagnetic angular [momentum density](@entry_id:271360)**, $\vec{\mathcal{L}}$, associated with the momentum density $\vec{g}$:

$$
\vec{\mathcal{L}} = \vec{r} \times \vec{g} = \vec{r} \times \left( \epsilon_0 (\vec{E} \times \vec{B}) \right)
$$

The total angular momentum stored in the electromagnetic field, $\vec{L}_{em}$, is then the integral of this density over all space:

$$
\vec{L}_{em} = \int_{\text{all space}} \vec{\mathcal{L}} \, dV = \epsilon_0 \int_{\text{all space}} \vec{r} \times (\vec{E} \times \vec{B}) \, dV
$$

These definitions form the foundation of our entire discussion. They imply that even a static configuration of charges and currents can possess a non-zero angular momentum, a concept often referred to as "[hidden momentum](@entry_id:266575)."

### Angular Momentum in Static Fields: The Hidden Momentum

It may seem counter-intuitive that static fields, which do not radiate energy, can store angular momentum. Yet, the expression for $\vec{\mathcal{L}}$ places no requirement that the fields be time-varying. Let us explore this fascinating idea through a series of examples.

The simplest, albeit hypothetical, system that stores [field angular momentum](@entry_id:268053) consists of a single electric [point charge](@entry_id:274116) $q$ and a magnetic monopole with magnetic charge $g$. The electric field of the point charge is radial, $\vec{E} \propto \frac{q}{r^2} \hat{r}$, while the magnetic field of the monopole is also radial, $\vec{B} \propto \frac{g}{r^2} \hat{r}$. If the charge and monopole are separated, their fields are not collinear everywhere, leading to a non-zero [cross product](@entry_id:156749) $\vec{E} \times \vec{B}$ and thus a non-zero momentum density. It can be shown that this configuration stores a total angular momentum directed along the line connecting the two particles. By applying the principle of superposition, we can extend this to find the angular momentum stored by a [continuous distribution](@entry_id:261698) of charge in the presence of a monopole, such as a uniformly charged hemispherical shell [@problem_id:1565309].

While magnetic monopoles remain hypothetical, we can construct realistic [static systems](@entry_id:272358) that exhibit the same phenomenon. Consider a long, thin wire with a uniform line charge density $\lambda$ placed along the central axis of a finite [solenoid](@entry_id:261182) carrying a steady current $I$ [@problem_id:1565310]. The wire produces a [radial electric field](@entry_id:194700), $\vec{E} \propto (\lambda/s) \hat{s}$, where $s$ is the radial distance from the axis. The [solenoid](@entry_id:261182) produces an approximately uniform axial magnetic field inside it, $\vec{B} \approx B_z \hat{z}$. The momentum density inside the solenoid is:

$$
\vec{g} = \epsilon_0 (\vec{E} \times \vec{B}) \propto \frac{\lambda B_z}{s} (\hat{s} \times \hat{z}) = -\frac{\lambda B_z}{s} \hat{\phi}
$$

This momentum density circulates azimuthally around the central axis. The corresponding angular [momentum density](@entry_id:271360) at a position $\vec{r} = s\hat{s} + z\hat{z}$ is:

$$
\vec{\mathcal{L}} = \vec{r} \times \vec{g} \propto (s\hat{s} + z\hat{z}) \times (-\frac{1}{s}\hat{\phi}) = -\hat{z} + \frac{z}{s}\hat{s}
$$

When integrated over a volume symmetric about the $z=0$ plane, the radial component vanishes, leaving a net angular momentum directed along the axis. This demonstrates explicitly how static, perpendicular $\vec{E}$ and $\vec{B}$ fields create a "hidden" angular momentum.

Calculating the total angular momentum by integrating $\vec{r} \times (\vec{E} \times \vec{B})$ over all space can be cumbersome. For static fields, an alternative and often more elegant method exists. The total angular momentum can be expressed in terms of the charge density $\rho(\vec{r})$ and the magnetic vector potential $\vec{A}(\vec{r})$ (where $\vec{B} = \nabla \times \vec{A}$):

$$
\vec{L}_{em} = \int \rho(\vec{r}) \, (\vec{r} \times \vec{A}(\vec{r})) \, dV
$$

This formulation is particularly powerful when the [charge distribution](@entry_id:144400) is localized. For example, consider a system composed of a charged ring and a long coaxial solenoid [@problem_id:1565298]. The magnetic vector potential $\vec{A}$ outside an ideal solenoid is purely azimuthal, $\vec{A} = (\Phi / 2\pi s) \hat{\phi}$, where $\Phi$ is the magnetic flux within the solenoid. For a charge element $dq$ on the ring at radius $R$, the contribution to the angular momentum is $dq \, (\vec{R} \times \vec{A}(\vec{R}))$. Since $\vec{R} = R\hat{s}$ (in local cylindrical coordinates), we find $\vec{R} \times \vec{A} \propto \hat{s} \times \hat{\phi} = \hat{z}$, a constant vector. The [total angular momentum](@entry_id:155748) is then simply this constant vector multiplied by the total charge $Q$ of the ring. This method elegantly circumvents the need to integrate over all space where both $\vec{E}$ and $\vec{B}$ might exist. This principle also extends to more complex static interactions, such as that between a static electric dipole and a static magnetic dipole [@problem_id:1565317].

### The Conservation of Total Angular Momentum

The existence of electromagnetic angular momentum is not merely a mathematical curiosity; it is essential for upholding one of physics' most fundamental laws: the [conservation of angular momentum](@entry_id:153076). For any isolated system, the total angular momentum—the sum of the mechanical angular momentum of all its parts ($\vec{L}_{mech}$) and the angular momentum stored in its electromagnetic fields ($\vec{L}_{em}$)—must remain constant.

$$
\frac{d}{dt} (\vec{L}_{mech} + \vec{L}_{em}) = 0
$$

This principle becomes physically manifest in situations where angular momentum is transferred between matter and fields. A classic illustration is a variation of "Feynman's disk paradox." Consider a system of two concentric conducting spherical shells, initially at rest, holding charges $+Q$ and $-Q$. This [spherical capacitor](@entry_id:203255) produces a [radial electric field](@entry_id:194700) in the region between the shells. If this setup is immersed in a uniform external magnetic field $\vec{B}_0$, the crossed $\vec{E}$ and $\vec{B}$ fields store an initial amount of angular momentum $\vec{L}_{em, i}$ [@problem_id:1565314]. The initial mechanical angular momentum is zero, $\vec{L}_{mech, i} = 0$.

Now, suppose the two shells are connected by a wire, allowing the charges to neutralize. The electric field collapses to zero, and consequently, the final [field angular momentum](@entry_id:268053) is also zero, $\vec{L}_{em, f} = 0$. To conserve the total angular momentum of the [isolated system](@entry_id:142067), the shells must begin to rotate with a final mechanical angular momentum $\vec{L}_{mech, f}$ such that:

$$
\vec{L}_{mech, i} + \vec{L}_{em, i} = \vec{L}_{mech, f} + \vec{L}_{em, f} \quad \implies \quad \vec{L}_{mech, f} = \vec{L}_{em, i}
$$

The angular momentum that was "hidden" in the static fields is converted into observable mechanical rotation. A similar phenomenon occurs if a charged [parallel-plate capacitor](@entry_id:266922) at rest in a uniform magnetic field is discharged; it too will begin to rotate as the [field angular momentum](@entry_id:268053) is converted to mechanical angular momentum [@problem_id:1565287].

Another mechanism for transferring angular momentum involves Faraday's Law of Induction. Imagine a small bar magnet falling along the axis of a fixed, non-conducting ring that carries a uniform static charge [@problem_id:1565284]. As the magnet falls, the magnetic flux $\Phi_B$ through the ring changes with time. According to Faraday's Law, this changing flux induces a non-conservative, tangential electric field $E_{\phi}$ around the ring:

$$
\oint \vec{E} \cdot d\vec{l} = 2\pi R E_{\phi} = -\frac{d\Phi_B}{dt}
$$

This [induced electric field](@entry_id:267314) exerts a torque $\vec{\tau}$ on the static charges of the ring. The time integral of this torque equals the [total angular momentum](@entry_id:155748) imparted to the ring. The calculation reveals that the final angular momentum acquired by the ring is directly proportional to the change in magnetic flux passing through it. This provides a dynamic link between Maxwell's equations and the transfer of angular momentum to a mechanical system.

### Self-Field Angular Momentum

An object can also store angular momentum in the fields generated by its own motion. Consider a non-conducting spherical shell with a uniform [surface charge](@entry_id:160539) $Q$. If this shell is at rest, it produces only a [radial electric field](@entry_id:194700). Now, let the shell spin with a constant angular velocity $\vec{\omega}$ [@problem_id:1565302]. The moving charges constitute a [surface current](@entry_id:261791), which in turn generates a magnetic field. Outside the shell, this field is that of a magnetic dipole with moment $\vec{m} \propto Q R^2 \vec{\omega}$.

The interaction of the sphere's own [radial electric field](@entry_id:194700) with its self-generated magnetic field creates a non-zero [momentum density](@entry_id:271360) $\vec{g} = \epsilon_0 (\vec{E} \times \vec{B})$ in the space surrounding it. Integrating the angular [momentum density](@entry_id:271360) $\vec{\mathcal{L}} = \vec{r} \times \vec{g}$ over all space reveals a net [field angular momentum](@entry_id:268053) $\vec{L}_{em}$ that is aligned with the [axis of rotation](@entry_id:187094) $\vec{\omega}$. This means the [total angular momentum](@entry_id:155748) of the spinning charged sphere is not simply its mechanical moment of inertia times $\vec{\omega}$, but includes this additional electromagnetic contribution.

### Symmetry Constraints on Field Angular Momentum

Beyond direct calculation, we can often deduce properties of the electromagnetic angular momentum vector by leveraging the power of symmetry. The key is to understand how vectors and pseudovectors transform under [symmetry operations](@entry_id:143398).

A quantity like position $\vec{r}$ or electric field $\vec{E}$ is a **[polar vector](@entry_id:184542)**. Under a spatial inversion ($\vec{r} \rightarrow -\vec{r}$), a [polar vector](@entry_id:184542) flips its sign. A quantity like mechanical angular momentum $\vec{L} = \vec{r} \times \vec{p}$ or magnetic field $\vec{B}$ is a **[pseudovector](@entry_id:196296)** (or [axial vector](@entry_id:191829)). Under inversion, a [pseudovector](@entry_id:196296) does not change its sign. The electromagnetic angular momentum $\vec{L}_{em}$ is also a [pseudovector](@entry_id:196296).

The transformation rule for a [pseudovector](@entry_id:196296) $\vec{A}$ under a reflection through a plane (e.g., the $xy$-plane) is that components parallel to the plane flip their sign, while the component perpendicular to the plane remains unchanged: $(A_x, A_y, A_z) \rightarrow (-A_x, -A_y, A_z)$.

Now, consider a static system of charges and currents whose physical arrangement is invariant under certain symmetry operations [@problem_id:1565319]. Any physical observable of this system, including its total [field angular momentum](@entry_id:268053) $\vec{L}_{em}$, must also be invariant under these same operations.

Suppose the system has a reflection symmetry through the $xy$-plane. For $\vec{L}_{em}$ to be invariant under this reflection, it must be equal to its transformed version:

$$
(L_x, L_y, L_z) = (-L_x, -L_y, L_z)
$$

This equality can only hold if $L_x = -L_x$ and $L_y = -L_y$, which forces $L_x = 0$ and $L_y = 0$. Thus, symmetry with respect to the $xy$-plane demands that the angular momentum vector can only have a $z$-component.

If the system has additional symmetries, the constraints become even stronger. For instance, if the system is also symmetric under reflection through the $xz$-plane, the transformation rule for the [pseudovector](@entry_id:196296) $\vec{L}_{em}$ is $(L_x, L_y, L_z) \rightarrow (-L_x, L_y, -L_z)$. Invariance then requires $L_x = 0$ and $L_z = 0$.

Combining the constraints from both reflection symmetries, we are forced to conclude that $L_x = 0$, $L_y = 0$, and $L_z = 0$. The [total angular momentum](@entry_id:155748) must be identically zero. This powerful result, derived without calculating a single field, highlights how fundamental principles of symmetry can provide profound physical insight. It shows that for highly symmetric charge and current distributions, such as those belonging to the $D_{2h}$ point group, the total stored electromagnetic angular momentum must vanish.