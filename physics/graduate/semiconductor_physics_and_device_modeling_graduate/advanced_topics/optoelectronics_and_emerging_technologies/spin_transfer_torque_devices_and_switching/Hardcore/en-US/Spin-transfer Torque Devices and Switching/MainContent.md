## Introduction
In the quest for next-generation electronics, spintronics has emerged as a revolutionary field by leveraging the electron's intrinsic spin in addition to its charge. A central breakthrough in spintronics is the discovery of [spin-transfer torque](@entry_id:146992) (STT), a phenomenon that allows an electrical current to directly control the magnetic orientation of a nanoscale magnet. This capability addresses a fundamental knowledge gap, offering a scalable and efficient alternative to magnetic-field-based switching, and paving the way for high-performance, [non-volatile memory](@entry_id:159710) and novel computing architectures that challenge the limits of conventional CMOS technology.

This article provides a comprehensive exploration of [spin-transfer torque](@entry_id:146992) devices and their switching dynamics. The reader will be guided through the core theoretical framework, its practical application, and hands-on modeling. In the first chapter, **"Principles and Mechanisms"**, we will deconstruct the fundamental physics, from the generation of a [spin-polarized current](@entry_id:271736) to its interaction with a magnetic moment via the augmented Landau-Lifshitz-Gilbert equation. Following this, the **"Applications and Interdisciplinary Connections"** chapter will examine the primary application of STT in MRAM, discussing its engineering challenges, its relation to materials science and circuit design, and its place in the landscape of emerging technologies. Finally, the **"Hands-On Practices"** section will provide opportunities to apply these concepts by building computational models to simulate the behavior of STT devices. We begin by examining the foundational principles that enable a flow of electrons to control the state of a magnet.

## Principles and Mechanisms

The operation of [spin-transfer torque](@entry_id:146992) devices is predicated on a series of interconnected physical principles, ranging from the quantum mechanical nature of [electron spin](@entry_id:137016) to the classical dynamics of macroscopic magnetic moments. This chapter elucidates these core principles and mechanisms, building a theoretical framework that connects microscopic [spin transport](@entry_id:1132190) to the macroscopic switching of a [magnetic memory](@entry_id:263319) element. We will begin by defining the concept of a [spin-polarized current](@entry_id:271736), then describe the [equation of motion](@entry_id:264286) governing a magnetic moment, and finally introduce the [spin-transfer torque](@entry_id:146992) as the coupling mechanism that allows this current to manipulate the magnetic state.

### From Charge Current to Spin Current

In conventional electronics, information is encoded and processed through the flow of [electrical charge](@entry_id:274596). Spintronics introduces a new degree of freedom: the electron's intrinsic [spin angular momentum](@entry_id:149719). When an electrical current passes through a non-magnetic material, the spins of the charge carriers are typically randomly oriented, resulting in no net transport of [spin angular momentum](@entry_id:149719). However, in a [ferromagnetic material](@entry_id:271936), the inherent spin asymmetry in the electronic band structure leads to a **[spin-polarized current](@entry_id:271736)**.

To formalize this, we distinguish between the conventional **charge current density**, $J_c$, which measures the flow of charge per unit area per unit time, and the **vector spin current density**, $\mathbf{J}_s$, which measures the flow of [spin angular momentum](@entry_id:149719) per unit area per unit time. The spin current is a vector quantity because angular momentum has a direction.

Within the **[two-current model](@entry_id:146959)**, we consider the total charge current to be composed of two independent channels: one for electrons with spin aligned parallel to the ferromagnet's quantization axis (spin-up) and another for electrons with spin anti-parallel (spin-down). Let the spin-resolved charge current densities for these channels be $J_{\uparrow}$ and $J_{\downarrow}$, respectively. The total charge current density is simply their sum: $J_c = J_{\uparrow} + J_{\downarrow}$.

The degree of spin polarization of the current, denoted by $P$, is defined as the normalized difference between the two spin channel currents:
$$
P \equiv \frac{J_{\uparrow}-J_{\downarrow}}{J_{\uparrow}+J_{\downarrow}}
$$
This dimensionless quantity ranges from $P=-1$ (fully spin-down polarized) to $P=+1$ (fully spin-up polarized), with $P=0$ representing an unpolarized current.

The connection between the macroscopic charge current and the [spin current](@entry_id:142607) can be established from first principles . Each electron carries a fundamental charge of $-e$ (where $e$ is the elementary positive charge) and a [spin angular momentum](@entry_id:149719) of magnitude $\frac{\hbar}{2}$. If the current is polarized along a direction specified by the unit vector $\hat{\mathbf{p}}$, the [spin angular momentum](@entry_id:149719) carried by spin-up electrons is $+\frac{\hbar}{2}\hat{\mathbf{p}}$ and by spin-down electrons is $-\frac{\hbar}{2}\hat{\mathbf{p}}$. The spin current density $\mathbf{J}_s$ is the net flux of this angular momentum. By relating the particle current density in each channel to the charge current density ($j_{n, \uparrow \downarrow} = J_{\uparrow \downarrow}/e$), the total vector [spin current](@entry_id:142607) density can be expressed as:
$$
\mathbf{J}_s = \left(\frac{J_{\uparrow}}{e} - \frac{J_{\downarrow}}{e}\right) \frac{\hbar}{2} \hat{\mathbf{p}} = \frac{J_{\uparrow} - J_{\downarrow}}{J_{\uparrow} + J_{\downarrow}} \frac{\hbar}{2e} (J_{\uparrow} + J_{\downarrow}) \hat{\mathbf{p}}
$$
This simplifies to the fundamental constitutive relation connecting spin current to charge current:
$$
\mathbf{J}_s = P \frac{\hbar}{2e} J_c \hat{\mathbf{p}}
$$
This equation is a cornerstone of spintronics, showing that a charge current $J_c$ can carry a net flux of [spin angular momentum](@entry_id:149719), with its magnitude proportional to the polarization $P$ and its direction aligned with the spin [polarization vector](@entry_id:269389) $\hat{\mathbf{p}}$.

### Origin of Spin Polarization: The Mott Two-Current Model

The existence of a non-zero current polarization $P$ is rooted in the spin-dependent electronic structure and scattering mechanisms within a [ferromagnetic material](@entry_id:271936). The **Mott [two-current model](@entry_id:146959)** provides a simple yet powerful picture for understanding this phenomenon in diffusive metals . This model treats the spin-up and spin-down electron populations as two parallel, independent channels for conduction.

The validity of this model rests on several key assumptions:
1.  **Independent Spin Channels:** Spin-flip scattering events are assumed to be infrequent compared to momentum-scattering events. This means an electron's spin state is preserved over many scattering events, allowing the spin-up and spin-down currents to be treated separately. This holds when the spin-diffusion length is much longer than the mean free path.
2.  **Collinear Magnetization:** The material is a uniform, collinear ferromagnet, providing a global quantization axis for spin.
3.  **Weak Spin-Orbit Coupling:** Spin-orbit interactions, which can mix [spin states](@entry_id:149436) and lead to transverse currents (like the anomalous Hall effect), are considered negligible. The spin-conductivity tensor is therefore diagonal in the spin basis aligned with the magnetization.
4.  **Single Driving Field:** In steady-state, bulk diffusive transport, both spin channels are assumed to be driven by the same electric field, $E$.

Under these conditions, Ohm's law can be applied to each channel independently: $J_{\uparrow} = \sigma_{\uparrow} E$ and $J_{\downarrow} = \sigma_{\downarrow} E$, where $\sigma_{\uparrow}$ and $\sigma_{\downarrow}$ are the spin-resolved conductivities. The difference in these conductivities arises from the spin-split density of states at the Fermi level in a ferromagnet. Substituting these expressions into the definition of $P$ yields a direct relation to the material's intrinsic transport properties:
$$
P = \frac{\sigma_{\uparrow} E - \sigma_{\downarrow} E}{\sigma_{\uparrow} E + \sigma_{\downarrow} E} = \frac{\sigma_{\uparrow} - \sigma_{\downarrow}}{\sigma_{\uparrow} + \sigma_{\downarrow}}
$$
This result demonstrates that the ability of a ferromagnet to polarize a current is fundamentally determined by the asymmetry in its conductivity for majority and minority spin electrons.

### The Dynamics of Magnetization: The LLG Equation

To understand how a spin current can manipulate a magnet, we first need an equation of motion for the magnetization itself. For a single-domain ferromagnet, where the magnetization $\mathbf{M}$ can be treated as a single macroscopic vector of constant magnitude $M_s$ (the [saturation magnetization](@entry_id:143313)), its dynamics are described by the **Landau-Lifshitz-Gilbert (LLG) equation**. The vector is often represented as $\mathbf{M}(t) = M_s \mathbf{m}(t)$, where $\mathbf{m}(t)$ is a [unit vector](@entry_id:150575) describing the direction of magnetization.

The LLG equation can be derived from the fundamental relationship between a magnetic moment and its angular momentum . A magnetic field exerts a torque on a magnetic moment, causing it to precess. For electrons, the magnetic moment $\mathbf{M}$ and angular [momentum density](@entry_id:271360) are anti-parallel, related by a negative [gyromagnetic ratio](@entry_id:149290). Conventionally, a positive constant $\gamma$ (the [gyromagnetic ratio](@entry_id:149290)) is used, leading to the precessional dynamics:
$$
\frac{d\mathbf{m}}{dt} = -\gamma \mu_0 \mathbf{m} \times \mathbf{H}_{\mathrm{eff}}
$$
Here, $\mu_0$ is the [vacuum permeability](@entry_id:186031) and $\mathbf{H}_{\mathrm{eff}}$ is the **effective magnetic field**. This field is a fictitious field that represents the net torque arising from all energy contributions to the system, including external applied fields, [magnetocrystalline anisotropy](@entry_id:144488), and magnetostatic (demagnetizing) fields. It is formally defined as the variational derivative of the magnetic free energy density $\mathcal{F}$ with respect to the magnetization:
$$
\mathbf{H}_{\mathrm{eff}} = -\frac{1}{\mu_0} \frac{\delta \mathcal{F}}{\delta \mathbf{M}}
$$

This precessional motion is conservative; it does not allow the magnetization to relax towards an energy minimum. To account for energy dissipation, a phenomenological damping term is added. In the Gilbert formulation, this term is proportional to the time derivative of the magnetization itself, constructed to be orthogonal to $\mathbf{m}$ to preserve its unit length:
$$
\boldsymbol{\tau}_{\mathrm{damping}} = \alpha \mathbf{m} \times \frac{d\mathbf{m}}{dt}
$$
Here, $\alpha$ is the dimensionless **Gilbert damping constant**, which quantifies the strength of the dissipative processes. Combining the precessional and damping terms gives the full LLG equation in its implicit Gilbert form:
$$
\frac{d\mathbf{m}}{dt} = -\gamma \mu_0 \mathbf{m} \times \mathbf{H}_{\mathrm{eff}} + \alpha \mathbf{m} \times \frac{d\mathbf{m}}{dt}
$$
This equation describes how the [magnetization vector](@entry_id:180304) $\mathbf{m}$ precesses around the effective field while gradually spiraling in towards the direction of the field, eventually reaching an energy minimum.

### The Core Mechanism: Spin-Transfer Torque

The LLG equation describes the behavior of a magnet in response to effective fields and intrinsic damping. Spin-transfer torque is the mechanism that allows a [spin-polarized current](@entry_id:271736) to act as an additional, non-conservative torque, directly influencing the magnetization dynamics. When a spin-polarized current, with spin polarization $\mathbf{p}$, is injected into a second ferromagnetic layer (the "free layer") with magnetization $\mathbf{m}$, the electrons' spins are forced to align with $\mathbf{m}$. By [conservation of angular momentum](@entry_id:153076), the angular momentum lost by the electron spins is transferred to the magnetic lattice of the free layer, exerting a torque. This is the **[spin-transfer torque](@entry_id:146992) (STT)**.

The LLG equation is augmented with an STT term, $\boldsymbol{\tau}_{\mathrm{STT}}$:
$$
\frac{d\mathbf{m}}{dt} = -\gamma \mu_0 \mathbf{m} \times \mathbf{H}_{\mathrm{eff}} + \alpha \mathbf{m} \times \frac{d\mathbf{m}}{dt} + \boldsymbol{\tau}_{\mathrm{STT}}
$$

#### Damping-Like and Field-Like Torques: Phenomenology

The [spin-transfer torque](@entry_id:146992) $\boldsymbol{\tau}_{\mathrm{STT}}$ is not a single, simple term. It can be decomposed into two orthogonal components with distinct symmetries and physical effects :

1.  **Damping-Like (or Slonczewski) Torque ($\boldsymbol{\tau}_{\mathrm{DL}}$):** This component lies in the plane defined by $\mathbf{m}$ and $\mathbf{p}$ and is proportional to $\mathbf{m} \times (\mathbf{m} \times \mathbf{p})$. It is called "damping-like" because its mathematical form is similar to the Gilbert damping term. It directly opposes or enhances the natural damping, driving the [magnetization vector](@entry_id:180304) $\mathbf{m}$ either toward or away from the [polarization vector](@entry_id:269389) $\mathbf{p}$. This is the primary component responsible for switching the magnetization. An important property is that this torque changes the angle $\theta$ between $\mathbf{m}$ and $\mathbf{p}$, as $\frac{d(\mathbf{m} \cdot \mathbf{p})}{dt}$ is generally non-zero.

2.  **Field-Like (or Perpendicular) Torque ($\boldsymbol{\tau}_{\mathrm{FL}}$):** This component is perpendicular to the plane of $\mathbf{m}$ and $\mathbf{p}$, with a vector form proportional to $\mathbf{m} \times \mathbf{p}$. It acts like the torque from an [effective magnetic field](@entry_id:139861) oriented along the direction of the spin polarization $\mathbf{p}$. It primarily causes additional precession of $\mathbf{m}$ around $\mathbf{p}$ and does not, by itself, cause switching, as it conserves the angle between $\mathbf{m}$ and $\mathbf{p}$.

The total STT is a [linear combination](@entry_id:155091) of these two terms, with coefficients that depend on the current, device materials, and the angle $\theta = \arccos(\mathbf{m} \cdot \mathbf{p})$:
$$
\boldsymbol{\tau}_{\mathrm{STT}} = a_{\mathrm{DL}}(I, \theta) [\mathbf{m} \times (\mathbf{m} \times \mathbf{p})] + a_{\mathrm{FL}}(I, \theta) [\mathbf{m} \times \mathbf{p}]
$$
In the [linear response](@entry_id:146180) regime (small angles), the [field-like torque](@entry_id:146079) effectively modifies the precession frequency (and thus the FMR frequency), while the [damping-like torque](@entry_id:143548) modifies the effective damping (and thus the FMR [linewidth](@entry_id:199028)) .

#### Derivation of the Slonczewski (Damping-Like) Torque

The expression for the dominant [damping-like torque](@entry_id:143548) can be derived from the principle of [angular momentum conservation](@entry_id:156798) at the interface between the non-magnetic spacer and the free layer  . The incoming spin current carries [spin angular momentum](@entry_id:149719) polarized along $\mathbf{p}$. As the electrons pass into the free layer, the transverse component of their spin (relative to $\mathbf{m}$) is absorbed, and the longitudinal component is transmitted. The absorbed flux of [spin angular momentum](@entry_id:149719) is equal to the torque exerted on the layer.

The total torque $\boldsymbol{\mathcal{T}}$ on the free layer of thickness $t_F$ and area $A$ is proportional to the incident charge current $I$, the reduced Planck constant $\hbar$, the electron charge $e$, and a dimensionless angular efficiency factor $\eta(\theta)$ that encapsulates material- and angle-dependent transmission properties. A rigorous derivation shows that the torque term in the LLG equation, which has units of frequency, is given by:
$$
\boldsymbol{\tau}_{\mathrm{DL}} = \frac{\gamma \hbar}{2e M_s t_F} \frac{I}{A} \eta(\theta) [\mathbf{m} \times (\mathbf{m} \times \mathbf{p})]
$$
This is the celebrated Slonczewski torque. The factor of $1/t_F$ highlights that for a given current, the torque has a greater effect on thinner magnetic layers, as they possess less [total angular momentum](@entry_id:155748). The vector structure $\mathbf{m} \times (\mathbf{m} \times \mathbf{p})$ ensures the torque vanishes when $\mathbf{m}$ and $\mathbf{p}$ are collinear, and that it acts to drive $\mathbf{m}$ towards or away from $\mathbf{p}$, depending on the direction of the current $I$. By comparing this with the phenomenological form, we identify the amplitude $a_{\mathrm{DL}}$. A direct calculation based on the absorbed [spin current](@entry_id:142607) flux $J_s$ relates the torque amplitude to material parameters as $a_{\mathrm{STT}} = -\frac{\gamma J_s}{M_s t_F}$ (the sign depends on the convention relating spin current to charge current and the definition of $\gamma$) .

#### Microscopic Origin: Spin-Mixing Conductance

While the phenomenological model is powerful, a deeper understanding of the origins of the two torque components requires a quantum mechanical treatment of [electron scattering](@entry_id:159023) at the interface between the non-magnetic spacer and the free ferromagnet. In this picture, the torque arises from the spin-dependent [reflection and transmission](@entry_id:156002) of electrons at the interface.

The transport properties of the interface are encapsulated in a complex quantity known as the **spin-mixing conductance**, $g^{\uparrow\downarrow}$ . This conductance relates the transverse [spin current](@entry_id:142607) absorbed by the ferromagnet to the transverse [spin accumulation](@entry_id:1132188) $\boldsymbol{\mu}_s$ that builds up in the non-magnetic layer at the interface. It can be calculated from the spin-dependent reflection amplitudes ($r_{nm}^{\uparrow}$, $r_{nm}^{\downarrow}$) for electrons scattering between different electronic modes ($n, m$) at the interface:
$$
g^{\uparrow\downarrow} = \sum_{n, m} \left(\delta_{nm} - r_{nm}^{\uparrow} r_{nm}^{\downarrow*}\right)
$$
The crucial insight from this theory is that the two components of the [spin-transfer torque](@entry_id:146992) are directly related to the real and imaginary parts of the spin-mixing conductance:
*   The **real part**, $\operatorname{Re}(g^{\uparrow\downarrow})$, governs the dissipative part of the [spin transport](@entry_id:1132190) and is proportional to the amplitude of the **[damping-like torque](@entry_id:143548)**, $\boldsymbol{\tau}_{\mathrm{DL}} \propto \operatorname{Re}(g^{\uparrow\downarrow}) [\mathbf{m} \times (\mathbf{m} \times \boldsymbol{\mu}_s)]$.
*   The **imaginary part**, $\operatorname{Im}(g^{\uparrow\downarrow})$, governs the reactive part of the [spin transport](@entry_id:1132190) and is proportional to the amplitude of the **[field-like torque](@entry_id:146079)**, $\boldsymbol{\tau}_{\mathrm{FL}} \propto \operatorname{Im}(g^{\uparrow\downarrow}) [\mathbf{m} \times \boldsymbol{\mu}_s]$.

This formalism provides a rigorous foundation for the existence of both torque components and connects their relative magnitudes to the fundamental quantum scattering properties of the specific materials at the interface.

### STT in Devices: Transport, Stability, and Switching

Applying these principles to a functional device requires considering the entire structure and the influence of temperature.

#### Spin Transport and Diffusion

In a typical STT device, such as a [magnetic tunnel junction](@entry_id:145304) (MTJ), the free and fixed ferromagnetic layers are separated by a non-magnetic spacer (either a metal or an insulator). The [spin-polarized current](@entry_id:271736) generated by the fixed layer must traverse this spacer to reach the free layer. During this transit, spin information can be lost due to spin-flip scattering events.

The transport of a non-equilibrium [spin population](@entry_id:188184) in a non-magnetic metal is governed by the **[spin diffusion](@entry_id:160343)-relaxation equation** . For the vector spin accumulation $\boldsymbol{\mu}_s(\mathbf{r}, t)$, which represents the local splitting of the chemical potential for different spin directions, this equation is:
$$
\frac{\partial \boldsymbol{\mu}_{s}}{\partial t} = D \nabla^2 \boldsymbol{\mu}_{s} - \frac{\boldsymbol{\mu}_{s}}{\tau_{\mathrm{sf}}}
$$
Here, $D$ is the [spin diffusion](@entry_id:160343) coefficient and $\tau_{\mathrm{sf}}$ is the spin-flip relaxation time. The equation describes how spin accumulation spreads via diffusion ($D \nabla^2 \boldsymbol{\mu}_{s}$) and decays over time due to spin-flips ($-\boldsymbol{\mu}_{s}/\tau_{\mathrm{sf}}$).

In the steady state ($\partial \boldsymbol{\mu}_{s}/\partial t = 0$), this equation dictates the spatial profile of the [spin accumulation](@entry_id:1132188). The solution reveals a characteristic length scale over which spin polarization decays exponentially, known as the **[spin diffusion length](@entry_id:136942)**, $\lambda$:
$$
\lambda = \sqrt{D \tau_{\mathrm{sf}}}
$$
For a one-dimensional system, a [spin accumulation](@entry_id:1132188) $\boldsymbol{\mu}_0$ injected at an interface at $x=0$ will decay into the non-magnetic material as $\boldsymbol{\mu}_s(x) = \boldsymbol{\mu}_0 \exp(-x/\lambda)$. For an STT device to be efficient, the spacer layer thickness must be significantly smaller than the [spin diffusion length](@entry_id:136942), ensuring that the [spin-polarized current](@entry_id:271736) reaches the free layer with minimal loss of polarization.

#### Magnetic Anisotropy and Thermal Stability

For a ferromagnetic layer to function as a memory element, it must possess at least two stable magnetic states, separated by an energy barrier. This stability is provided by **[magnetic anisotropy](@entry_id:138218)**. Modern STT-MRAM cells often utilize **[perpendicular magnetic anisotropy](@entry_id:146658) (PMA)**, where the magnetization preferentially aligns perpendicular to the plane of the film.

PMA arises from a competition between two main energy contributions :
1.  **Magnetocrystalline Anisotropy:** Often originating from interfacial effects in [thin films](@entry_id:145310), this is described by an anisotropy constant $K_u$. For PMA, it favors out-of-plane alignment. Its energy density is $f_u = K_u \sin^2\theta$, where $\theta$ is the angle from the perpendicular axis.
2.  **Shape Anisotropy (Magnetostatic Energy):** Arising from the magnetic fields generated by the magnet itself, this energy favors keeping the magnetization in the plane of the film to minimize surface magnetic poles. For a thin film, its energy density is approximately $f_d = \frac{1}{2}\mu_0 M_s^2 \cos^2\theta$.

For the out-of-plane orientation to be stable, the [magnetocrystalline anisotropy](@entry_id:144488) must overcome the [shape anisotropy](@entry_id:144115). This leads to the stability condition:
$$
K_u > \frac{1}{2} \mu_0 M_s^2
$$
When this condition is met, the total energy has minima at $\theta=0$ and $\theta=\pi$ (up and down states) and a maximum in the plane at $\theta=\pi/2$. The **energy barrier**, $\Delta E$, separating the two stable states is the energy difference between the maximum and the minimum:
$$
\Delta E = \left( K_u - \frac{1}{2} \mu_0 M_s^2 \right) V
$$
where $V$ is the volume of the magnet. This energy barrier is of paramount importance: it must be large enough to prevent spontaneous thermal fluctuations from flipping the bit, thus ensuring long-term [data retention](@entry_id:174352).

#### Thermally Assisted Switching

At any non-zero temperature, the magnetization is subject to random thermal fluctuations, which are equivalent to a stochastic magnetic field. These fluctuations can cause the magnetization to escape from a stable energy well, even if the applied current is below the zero-temperature [critical switching current](@entry_id:1123212). This process of thermally activated switching is described by the **Néel-Brown model**.

The rate of switching, $\Gamma$, follows an Arrhenius-like law :
$$
\Gamma = f_0 \exp\left[-\frac{\Delta E(I)}{k_B T}\right]
$$
where $k_B$ is the Boltzmann constant and $T$ is the temperature. The term $\Delta E(I)$ is the energy barrier, which is now dependent on the current $I$ because the [spin-transfer torque](@entry_id:146992) effectively tilts the energy landscape, reducing the barrier for escape.

The [pre-exponential factor](@entry_id:145277), $f_0$, is the **attempt frequency**. It represents the characteristic rate at which the magnetization "attempts" to cross the energy barrier. Its value is determined by the intrinsic properties of the magnet, including the [gyromagnetic ratio](@entry_id:149290) $\gamma$, the damping constant $\alpha$, the anisotropy field $H_k = 2K_u/(\mu_0 M_s)$, and any external field $H_z$. A well-established approximation for the attempt frequency derived from the Kramers-Langer escape-[rate theory](@entry_id:1130588) is:
$$
f_0 = \frac{\alpha \gamma}{1+\alpha^2} \frac{1}{2\pi} \sqrt{H_k^2 - H_z^2}
$$
This expression encapsulates the essential physics: the switching attempt rate is proportional to the damping (as switching is a dissipative process) and depends on the curvature of the energy landscape at the minimum and saddle point, which is influenced by the applied and anisotropy fields. The [thermal stability factor](@entry_id:755897), $\Delta E / (k_B T)$, determines the probability of a successful attempt, governing the reliability and retention time of an STT memory cell.