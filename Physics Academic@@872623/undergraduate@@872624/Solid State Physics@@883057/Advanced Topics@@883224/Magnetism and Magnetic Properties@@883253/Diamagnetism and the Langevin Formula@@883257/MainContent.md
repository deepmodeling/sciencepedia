## Introduction
Every material, from a simple gas to a complex solid, responds to the presence of a magnetic field. While some materials are strongly attracted or repelled, all matter exhibits a subtle, fundamental repulsion known as [diamagnetism](@entry_id:148741). This universal effect, originating from the quantum mechanical nature of atoms, can be surprisingly well-described by classical physics. The central challenge lies in moving from a qualitative understanding based on Lenz's law to a quantitative model that connects an atom's microscopic structure to a material's measurable magnetic properties. This article bridges that gap by systematically developing the classical theory of diamagnetism.

This article is structured to guide you from foundational concepts to practical applications. We will first uncover the inductive origin of diamagnetism, introduce the crucial concept of Larmor precession, and culminate in a detailed derivation of the Langevin formula. Next, we will demonstrate how this formula is used as a powerful tool in chemistry, materials science, and even astrophysics. Finally, the "Hands-On Practices" section will solidify your understanding through guided problem-solving, allowing you to apply the theory to concrete physical scenarios. We begin by exploring the core principles that govern this fascinating magnetic phenomenon.

## Principles and Mechanisms

Diamagnetism is a fundamental magnetic response present in all matter. It arises from the reaction of atomic [electron orbitals](@entry_id:157718) to an externally applied magnetic field. Unlike [paramagnetism](@entry_id:139883) or ferromagnetism, which depend on the existence of intrinsic [magnetic dipole moments](@entry_id:158175), [diamagnetism](@entry_id:148741) is an induced effect. This chapter elucidates the classical principles governing this phenomenon, culminating in the derivation and application of the Langevin formula, and concludes by exploring the limitations of this classical description.

### The Inductive Origin of Diamagnetism

The physical origin of [diamagnetism](@entry_id:148741) is best understood as a microscopic manifestation of Faraday's law of induction and **Lenz's law**. Consider a classical model of an atom where electrons move in [stable orbits](@entry_id:177079) around a nucleus. When an external magnetic field $\vec{B}$ is applied, the magnetic flux through the area of each electron orbit changes. According to Faraday's law, this change in flux induces an [electromotive force](@entry_id:203175) (EMF) and, consequently, a tangential electric field.

This [induced electric field](@entry_id:267314) exerts a torque on the orbiting electron, causing its angular velocity to change. By **Lenz's law**, the [induced current](@entry_id:270047) must generate a magnetic field that opposes the initial change in flux. This means that the change in the electron's [orbital magnetic moment](@entry_id:159585) is directed opposite to the applied external field. This creation of an opposing magnetic moment is the essence of **diamagnetism**.

This conclusion can also be reached through a powerful symmetry argument [@problem_id:1769896]. An isolated atom with a spherically symmetric electron cloud is isotropic; it has no preferred direction. When a uniform external magnetic field $\vec{B}$ is applied, the field itself introduces a unique axis of symmetry. Any response of the system, such as the [induced magnetic moment](@entry_id:184971) $\vec{m}$, must align with this unique axis for the combined system's symmetry to be preserved. Therefore, the induced moment $\vec{m}$ must be collinear with $\vec{B}$. The universal observation that the energy of the atom increases in the presence of the field, combined with Lenz's law, dictates that this response must be opposing, leading to the conclusion that $\vec{m}$ is anti-parallel to $\vec{B}$.

### Larmor's Theorem and Induced Precession

To quantify this induced effect, we move beyond qualitative arguments to a dynamical analysis of the electron's motion. The motion of an electron (charge $-e$, mass $m_e$) in a [central potential](@entry_id:148563) $V(r)$ and a uniform magnetic field $\vec{B}$ is governed by the Lorentz force law:
$$
m_e \ddot{\vec{r}} = -\nabla V(r) - e(\dot{\vec{r}} \times \vec{B})
$$
where $-\nabla V(r)$ represents the [central force](@entry_id:160395) $\vec{F}_0$ from the nucleus. The analysis of this equation is greatly simplified by a key insight known as **Larmor's theorem**.

**Larmor's theorem** states that, to first order in the magnetic field strength, the motion of a charged particle in a [central force](@entry_id:160395) field is equivalent to its motion in the absence of the field, as observed from a reference frame that rotates with a specific angular velocity. This special [angular velocity](@entry_id:192539) is known as the **Larmor frequency**, $\vec{\omega}_L$.

To demonstrate this, we transform the equation of motion to a frame rotating with an unknown angular velocity $\vec{\Omega}$. The equation of motion in this [rotating frame](@entry_id:155637) (primed coordinates) becomes:
$$
m_e \ddot{\vec{r}}' = \vec{F}_0 - e((\vec{v}' + \vec{\Omega} \times \vec{r}) \times \vec{B}) - 2m_e(\vec{\Omega} \times \vec{v}') - m_e(\vec{\Omega} \times (\vec{\Omega} \times \vec{r}))
$$
The crucial step is to choose $\vec{\Omega}$ to eliminate the first-order magnetic and Coriolis force terms. By setting the sum of the dominant velocity-dependent terms to zero, we find the required [angular velocity](@entry_id:192539):
$$
-e(\vec{v}' \times \vec{B}) - 2m_e(\vec{\Omega} \times \vec{v}') = 0 \implies (e\vec{B} - 2m_e\vec{\Omega}) \times \vec{v}' = 0
$$
This equation holds for any velocity $\vec{v}'$ if we choose:
$$
\vec{\Omega} = \frac{e\vec{B}}{2m_e}
$$
This is the Larmor frequency vector, $\vec{\omega}_L$. With this choice, and neglecting terms of order $B^2$, the equation of motion in the rotating frame simplifies remarkably:
$$
m_e \ddot{\vec{r}}' \approx \vec{F}_0
$$
This confirms that in the Larmor frame, the electron's motion appears as it would without any magnetic field. The effect of the magnetic field, therefore, is to superimpose a uniform precession of the entire electron orbit around the direction of $\vec{B}$ at the Larmor frequency. Importantly, this result is independent of the specific form of the central potential $V(r)$, making it a general principle for any bound electron system [@problem_id:2835252]. This induced [orbital motion](@entry_id:162856) is known as **Larmor precession**.

The magnitude of the Larmor frequency is $|\vec{\omega}_L| = \frac{eB}{2m_e}$. It is instructive to compare this to the **cyclotron frequency**, $\omega_c = \frac{eB}{m_e}$, which is the angular frequency of a *free* electron executing circular [motion in a magnetic field](@entry_id:195019). The Larmor frequency is exactly half the cyclotron frequency. This factor of one-half is a fundamental distinction between the induced response of a bound electron and the characteristic motion of a free one [@problem_id:1769897]. While a free electron's entire motion is dictated by the magnetic field, a bound electron's orbit is only perturbed, leading to a precessional response at a lower frequency.

### The Langevin Formula for Diamagnetic Susceptibility

The Larmor precession of the electron's orbit constitutes an additional electrical current, which in turn generates an induced [magnetic dipole moment](@entry_id:149826). We can now calculate this moment. The change in the electron's velocity due to the precession is $\Delta\vec{v} = \vec{\omega}_L \times \vec{r}$. The [induced magnetic moment](@entry_id:184971), $\Delta\vec{\mu}$, is given by the change in the current loop expression:
$$
\Delta\vec{\mu} = \frac{1}{2} \langle (-e)(\vec{r} \times \Delta\vec{v}) \rangle = -\frac{e}{2} \langle \vec{r} \times (\vec{\omega}_L \times \vec{r}) \rangle
$$
Substituting $\vec{\omega}_L = \frac{e\vec{B}}{2m_e}$ and applying the [vector triple product](@entry_id:162942) identity $\vec{a} \times (\vec{b} \times \vec{c}) = \vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})$, we get:
$$
\Delta\vec{\mu} = -\frac{e^2}{4m_e} \langle \vec{B}(\vec{r} \cdot \vec{r}) - \vec{r}(\vec{r} \cdot \vec{B}) \rangle
$$
For an isotropic system, such as a spherically symmetric atom, we can average over all orientations. If we align $\vec{B}$ with the $z$-axis, $\vec{B} = B\hat{z}$, the time-averaged off-diagonal terms like $\langle xz \rangle$ and $\langle yz \rangle$ are zero. The expression simplifies to:
$$
\Delta\vec{\mu} = -\frac{e^2 B}{4m_e} \langle x^2 + y^2 \rangle \hat{z} = -\frac{e^2}{4m_e} \langle \rho^2 \rangle \vec{B}
$$
where $\langle \rho^2 \rangle = \langle x^2 + y^2 \rangle$ is the mean-square radius of the electron orbit projected onto the plane perpendicular to the field. For a spherically [symmetric charge distribution](@entry_id:276636), statistical mechanics tells us that $\langle x^2 \rangle = \langle y^2 \rangle = \langle z^2 \rangle = \frac{1}{3}\langle r^2 \rangle$. Therefore, $\langle \rho^2 \rangle = \frac{2}{3}\langle r^2 \rangle$, where $\langle r^2 \rangle$ is the mean-square radius of the electron's orbit from the nucleus.

Substituting this into the expression for the induced moment for a single electron gives:
$$
\Delta\vec{\mu}_{\text{electron}} = -\frac{e^2 \langle r^2 \rangle}{6m_e} \vec{B}
$$
The induced moment is anti-parallel to the applied field and proportional to $e^2/m_e$ and the mean-square orbital radius [@problem_id:1769892].

An atom contains $Z$ electrons, and since [diamagnetism](@entry_id:148741) is an effect involving all electrons, we must sum their individual contributions. The total [induced magnetic moment](@entry_id:184971) per atom is:
$$
\vec{\mu}_{\text{atom}} = -\frac{e^2 \vec{B}}{6m_e} \sum_{i=1}^{Z} \langle r_i^2 \rangle
$$
The macroscopic magnetization $\vec{M}$ (magnetic moment per unit volume) is the atomic moment multiplied by the [number density](@entry_id:268986) of atoms, $n$.
$$
\vec{M} = n \vec{\mu}_{\text{atom}} = -\frac{n e^2 \vec{B}}{6m_e} \sum_{i=1}^{Z} \langle r_i^2 \rangle
$$
Finally, the [magnetic susceptibility](@entry_id:138219) $\chi$ is defined by the relation $\vec{M} = \chi \vec{H}$. In non-magnetic materials where magnetization is weak, we can approximate $\vec{B} \approx \mu_0 \vec{H}$. This yields the celebrated **Langevin formula for [diamagnetic susceptibility](@entry_id:136270)**:
$$
\chi = -\frac{\mu_0 n e^2}{6m_e} \sum_{i=1}^{Z} \langle r_i^2 \rangle
$$

### Interpreting and Applying the Langevin Formula

The Langevin formula provides a powerful framework for understanding the diamagnetic properties of materials.
- **Universality:** The negative sign confirms that the susceptibility is always negative, meaning the induced magnetization always opposes the applied field. This is a universal property of all atoms.
- **Dependence on Atomic Structure:** The susceptibility is directly proportional to the sum of the mean-square radii of all electron orbits, $\sum_{i} \langle r_i^2 \rangle$. This term is heavily weighted towards the outermost electrons. For example, in a potassium atom ($Z=19$, configuration $1s^2 2s^2 2p^6 3s^2 3p^6 4s^1$), the single valence electron in the N shell ($n=4$) has a mean radius so much larger than those of the inner-shell electrons that its contribution to the [diamagnetic susceptibility](@entry_id:136270) dominates, despite there being 18 other electrons [@problem_id:1769894]. Diamagnetism is fundamentally a measure of the spatial extent of the electron cloud.
- **Macroscopic Properties:** The formula connects microscopic atomic properties to measurable macroscopic quantities.
    - **Volume Susceptibility:** The formula gives the volume susceptibility, which depends on the [number density](@entry_id:268986) $n$. For an ideal gas where $n = P/(k_B T)$, the magnetization $M$ will vary with pressure and temperature, not because the atomic response changes, but because the number of atoms per unit volume changes [@problem_id:1769906]. The underlying atomic susceptibility is temperature-independent.
    - **Mass Susceptibility:** It is often useful to define the mass susceptibility, $\chi_{\text{mass}} = \chi / \rho$, where $\rho$ is the mass density. For a material composed of particles of mass $m_{\text{part}}$, this becomes $\chi_{\text{mass}} = \mu_{\text{atom}} / (m_{\text{part}} B)$. This quantity reflects the diamagnetic contribution per unit mass. For instance, comparing a helium atom (He, 2 electrons) and a doubly-ionized beryllium ion (Be$^{2+}$, also 2 electrons), if we assume their $\langle r^2 \rangle$ values are similar, their atomic susceptibilities are nearly identical. However, their mass susceptibilities will differ, scaling inversely with their respective particle masses [@problem_id:1769843].
- **Effect on Magnetic Fields:** A diamagnetic material, when placed in an external field, actively alters that field. Consider a long solenoid that produces a field $B_0 = \mu_0 n I$ in a vacuum. When filled with a diamagnetic liquid of susceptibility $\chi$, the material becomes magnetized with $M = \chi H = \chi nI$. The total field inside, $B_f$, is given by $B_f = \mu_0(H+M) = \mu_0(1+\chi)H$. The ratio of the final to initial field is thus $B_f/B_0 = 1+\chi$. Since $\chi$ is negative for a diamagnet, the field inside the material is reduced [@problem_id:1769893].

### The Limits of Classical Theory: The Bohr-van Leeuwen Theorem

The Langevin model, based on bound electrons, is remarkably successful in describing [diamagnetism](@entry_id:148741) in insulators and atoms. A natural question arises: how does this apply to the conduction electrons in a metal, which can be modeled as a [free electron gas](@entry_id:145649)?

If we attempt to apply classical statistical mechanics to a gas of free, non-interacting electrons, we encounter a profound failure. The **Bohr-van Leeuwen theorem** states that in a purely classical framework, any system of charges in thermal equilibrium can exhibit no [net magnetization](@entry_id:752443). The diamagnetic (and paramagnetic) susceptibility of a classical electron gas is predicted to be exactly zero.

The proof of this theorem involves analyzing the classical partition function, $Z$. The Hamiltonian for an electron in a magnetic field is $H = \frac{1}{2m_e}(\vec{p} + e\vec{A})^2$, where $\vec{p}$ is the [canonical momentum](@entry_id:155151) and $\vec{A}$ is the [vector potential](@entry_id:153642). The partition function involves an integral over all positions and momenta:
$$
Z \propto \iint \exp\left(-\frac{H}{k_B T}\right) d^3r \, d^3p = \iint \exp\left(-\frac{(\vec{p} + e\vec{A})^2}{2m_e k_B T}\right) d^3r \, d^3p
$$
The crucial step is to recognize that the momentum integral can be simplified by a shift of variable, $\vec{p}' = \vec{p} + e\vec{A}$. Since the integration is over all possible momenta from $-\infty$ to $+\infty$, this shift does not change the result of the integral. The partition function becomes independent of the vector potential $\vec{A}$, and therefore independent of the magnetic field $\vec{B}$.

Since the free energy $F = -k_B T \ln Z$ is independent of $B$, the magnetization $M = -\frac{1}{V} (\partial F / \partial B)$ must be zero. Consequently, the susceptibility $\chi = \partial M / \partial H$ is also zero [@problem_id:1769909].

This startling result shows that classical physics cannot account for the magnetic properties of free electrons. The orbiting paths at the boundary of the material, which are not cancelled by adjacent loops, are neglected in this simple picture. A correct description of the weak diamagnetism of conduction electrons (known as Landau diamagnetism) and their weak [paramagnetism](@entry_id:139883) (Pauli paramagnetism) requires a full quantum mechanical treatment, where the [quantization of energy](@entry_id:137825) levels (Landau levels) in a magnetic field becomes the central physical mechanism. The Langevin model, while powerful, is therefore fundamentally limited to systems of bound electrons.