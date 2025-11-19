## Introduction
While Bloch's theorem is fundamental to understanding the [energy band structure](@entry_id:264545) of crystals, the Bloch wavefunctions themselves contain a deeper layer of information. Beyond defining the [energy spectrum](@entry_id:181780), the periodic part of the Bloch function, $|u_{n\mathbf{k}}\rangle$, encodes a rich "[quantum geometry](@entry_id:147695)" that governs a wide array of profound physical phenomena. This geometric structure, often overlooked in introductory treatments, is the key to understanding modern concepts like [topological materials](@entry_id:142123) and quantized transport. This article bridges that conceptual gap, providing a comprehensive exploration of the Berry phase and Berry curvature of Bloch states. The journey begins in the **Principles and Mechanisms** section, which lays the theoretical groundwork by introducing the general concept of a geometric phase and defining the Berry [connection and curvature](@entry_id:158520) in the momentum space of crystals. The **Applications and Interdisciplinary Connections** section demonstrates the far-reaching impact of this geometry, exploring its role in topological insulators, Weyl [semimetals](@entry_id:152277), and its connections to fields like optics and quantum chemistry. Finally, **Hands-On Practices** provides a set of guided problems to solidify the reader's understanding of these crucial concepts. We begin by examining the core principles that underpin the [quantum geometry](@entry_id:147695) of electron bands.

## Principles and Mechanisms

In the framework of Bloch's theorem, which describes the band structure of crystalline solids, the Bloch [eigenstates](@entry_id:149904) $|\psi_{n\mathbf{k}}\rangle = e^{i\mathbf{k}\cdot\mathbf{r}} |u_{n\mathbf{k}}\rangle$ are primarily treated as stationary states that determine the [energy spectrum](@entry_id:181780) $E_n(\mathbf{k})$. However, the periodic part of the Bloch function, $|u_{n\mathbf{k}}\rangle$, contains profound geometric information that governs a wide array of physical phenomena, from electrical polarization to quantized transport. This section delves into the principles and mechanisms of this "[quantum geometry](@entry_id:147695)" of electron bands, focusing on the concepts of the Berry phase, Berry connection, and Berry curvature.

### The Geometric Phase in Adiabatic Evolution

The story begins not in solids, but in the general framework of quantum mechanics. Consider a quantum system described by a Hamiltonian $H(\mathbf{R})$ that depends on a set of external parameters $\mathbf{R}(t)$. If these parameters are varied slowly in time, the **[adiabatic theorem](@entry_id:142116)** states that if the system starts in an eigenstate $|n(\mathbf{R}(0))\rangle$, it will remain in the instantaneous eigenstate $|n(\mathbf{R}(t))\rangle$ at a later time $t$, up to a phase factor. The total phase accumulated is $\exp(i\phi_{total})$.

This phase has two components. The first is the familiar **dynamic phase**, $\phi_{dyn} = -\frac{1}{\hbar}\int_0^T E_n(t') dt'$, which depends on the energy of the [eigenstate](@entry_id:202009). The second, more subtle component is the **geometric phase**, discovered by Michael Berry. This phase, also known as the Berry phase, depends not on the duration of the evolution but on the geometric path traced by the parameters $\mathbf{R}(t)$ in parameter space. For a cyclic evolution where $\mathbf{R}(T) = \mathbf{R}(0)$, the Berry phase is given by:
$$
\gamma_n = i \oint_{\mathcal{C}} \langle u_n(\mathbf{R}) | \nabla_{\mathbf{R}} | u_n(\mathbf{R}) \rangle \cdot d\mathbf{R}
$$
where $\mathcal{C}$ is the closed loop in [parameter space](@entry_id:178581).

A particularly intuitive example arises in a simple [two-level system](@entry_id:138452), such as a spin-1/2 particle in a magnetic field, described by a Hamiltonian $H = \mathbf{d} \cdot \boldsymbol{\sigma}$, where $\boldsymbol{\sigma}$ is the vector of Pauli matrices. Here, the vector $\mathbf{d}$ acts as the parameter vector. The [energy eigenvalues](@entry_id:144381) are $E_{\pm} = \pm |\mathbf{d}|$. If the direction of the vector $\mathbf{d}$ is varied adiabatically, tracing a closed loop on a sphere, the ground state acquires a Berry phase. This phase is elegantly related to the geometry of the path: $\gamma_{-} = \frac{1}{2}\Omega$, where $\Omega$ is the [solid angle](@entry_id:154756) subtended by the path of the normalized vector $\hat{\mathbf{d}} = \mathbf{d}/|\mathbf{d}|$ on the unit sphere, known as the Bloch sphere [@problem_id:1097470]. For example, if we consider a Hamiltonian where the vector $\mathbf{d}$ traces a circle of constant polar angle $\theta$ as another parameter $\phi$ goes from $0$ to $2\pi$, the [solid angle](@entry_id:154756) enclosed is $\Omega = 2\pi(1 - \cos\theta)$. The Berry phase acquired by the ground state is therefore $\gamma = \pi(1 - \cos\theta)$ [@problem_id:1097470]. This result beautifully illustrates that quantum phase can encode the geometry of the system's [parameter space](@entry_id:178581).

### The Berry Connection and Curvature in Momentum Space

In a crystalline solid, the crystal momentum $\mathbf{k}$ is a natural set of parameters for the Bloch Hamiltonian $H(\mathbf{k})$. The Brillouin zone, the space of all unique crystal momenta, becomes the parameter space over which the geometry of the [eigenstates](@entry_id:149904) $|u_{n\mathbf{k}}\rangle$ is defined.

Following the analogy with the general Berry phase, we define a vector field for each band $n$ within the Brillouin zone, known as the **Berry connection**:
$$
\mathbf{A}_n(\mathbf{k}) = i \langle u_{n\mathbf{k}} | \nabla_{\mathbf{k}} | u_{n\mathbf{k}} \rangle
$$
Here, $|u_{n\mathbf{k}}\rangle$ is the cell-periodic part of the Bloch function, assumed to be normalized, $\langle u_{n\mathbf{k}} | u_{n\mathbf{k}} \rangle = 1$. The Berry connection is a momentum-space analogue of the vector potential in electromagnetism.

A crucial subtlety arises from the fact that the phase of the Bloch eigenstate is not unique. At each point $\mathbf{k}$, we can choose a different phase for our eigenstate without changing any physical observable. This corresponds to a **U(1) gauge transformation**:
$$
|u'_{n\mathbf{k}}\rangle = e^{i\phi_n(\mathbf{k})} |u_{n\mathbf{k}}\rangle
$$
where $\phi_n(\mathbf{k})$ is a smooth, real scalar function of momentum. Under this transformation, the Berry connection is not invariant. A straightforward calculation shows that the new connection $\mathbf{A}'_n(\mathbf{k})$ is related to the old one by [@problem_id:1097422] [@problem_id:2955790]:
$$
\mathbf{A}'_n(\mathbf{k}) = \mathbf{A}_n(\mathbf{k}) - \nabla_{\mathbf{k}} \phi_n(\mathbf{k})
$$
This is precisely the gauge transformation law for a vector potential in electromagnetism. Since the Berry connection itself is gauge-dependent, it is not a direct physical observable.

However, just as in electromagnetism, we can construct a gauge-invariant quantity from the connection. This is the **Berry curvature**, defined as the "curl" of the Berry connection in [momentum space](@entry_id:148936):
$$
\boldsymbol{\Omega}_n(\mathbf{k}) = \nabla_{\mathbf{k}} \times \mathbf{A}_n(\mathbf{k})
$$
In two dimensions, the Berry curvature is a [pseudoscalar](@entry_id:196696) quantity $\Omega_n(\mathbf{k}) \equiv (\boldsymbol{\Omega}_n(\mathbf{k}))_z = \partial_{k_x} A_{n,y}(\mathbf{k}) - \partial_{k_y} A_{n,x}(\mathbf{k})$. Applying the gauge transformation to the curvature, we find that the extra term vanishes because the [curl of a gradient](@entry_id:274168) is identically zero: $\nabla_{\mathbf{k}} \times (\nabla_{\mathbf{k}} \phi_n) = 0$. Therefore, the Berry curvature is **gauge invariant**:
$$
\boldsymbol{\Omega}'_n(\mathbf{k}) = \boldsymbol{\Omega}_n(\mathbf{k})
$$
The Berry curvature is the analogue of the magnetic field in momentum space. It is a local, intrinsic, and physically meaningful geometric property of the band structure. The Berry phase $\gamma_n[\mathcal{C}]$ acquired by traversing a closed loop $\mathcal{C}$ in the Brillouin zone is, by Stokes' theorem, the flux of the Berry curvature through the surface enclosed by the loop:
$$
\gamma_n[\mathcal{C}] = \oint_{\mathcal{C}} \mathbf{A}_n(\mathbf{k}) \cdot d\mathbf{k} = \int_{\mathcal{S}} \boldsymbol{\Omega}_n(\mathbf{k}) \cdot d\mathbf{S}
$$
While the Berry phase around a general loop can change by multiples of $2\pi$ under certain "large" [gauge transformations](@entry_id:176521), the physical phase factor $e^{i\gamma_n[\mathcal{C}]}$ is strictly gauge invariant [@problem_id:2955790].

### Calculating the Berry Curvature: The Two-Band Model

The general formula for Berry curvature can be cumbersome. For the common and instructive case of a two-band model, described by a Hamiltonian of the form $H(\mathbf{k}) = \mathbf{d}(\mathbf{k}) \cdot \boldsymbol{\sigma}$, the formula for the ground state Berry curvature simplifies considerably. It can be expressed directly in terms of the vector function $\mathbf{d}(\mathbf{k})$ and its derivatives:
$$
\boldsymbol{\Omega}_-(\mathbf{k}) = \frac{1}{2d^3} \mathbf{d} \cdot \left( \frac{\partial \mathbf{d}}{\partial k_x} \times \frac{\partial \mathbf{d}}{\partial k_y} \right) \hat{\mathbf{z}}
$$
where $d = |\mathbf{d}(\mathbf{k})|$, and we denote the component as $\mathcal{F}_{xy}(\mathbf{k}) = (\boldsymbol{\Omega}_-(\mathbf{k}))_z$. This formula reveals that the curvature is large in regions of momentum space where the direction of the vector $\mathbf{d}$ changes rapidly.

Let's apply this to a concrete model [@problem_id:1097488]. Consider a 2D [tight-binding](@entry_id:142573) Hamiltonian on a square lattice given by $H(\mathbf{k}) = \mathbf{d}(\mathbf{k})\cdot\boldsymbol{\sigma}$ with
$$
\mathbf{d}(\mathbf{k}) = \begin{pmatrix} \alpha \sin(k_x a) \\ \beta \sin(k_y a) \\ M - \gamma(\cos(k_x a) + \cos(k_y a)) \end{pmatrix}
$$
To calculate the Berry curvature at the $\Gamma$-point, $\mathbf{k}=(0,0)$, we first evaluate the vector and its derivatives. At $\mathbf{k}=(0,0)$, we have $d_x = d_y = 0$ and $d_z = M - 2\gamma$. Assuming $M>2\gamma$, the vector is $\mathbf{d}(0,0) = (0, 0, M-2\gamma)$. The [partial derivatives](@entry_id:146280) at this point are $\partial_{k_x}\mathbf{d} = (\alpha a, 0, 0)$ and $\partial_{k_y}\mathbf{d} = (0, \beta a, 0)$. The [cross product](@entry_id:156749) is $(\partial_{k_x}\mathbf{d} \times \partial_{k_y}\mathbf{d}) = (0, 0, \alpha\beta a^2)$. The [scalar triple product](@entry_id:152997) is then $\mathbf{d} \cdot (\partial_{k_x}\mathbf{d} \times \partial_{k_y}\mathbf{d}) = (M-2\gamma)(\alpha\beta a^2)$. With $d = M-2\gamma$, the Berry curvature at the $\Gamma$-point is:
$$
\mathcal{F}_{xy}(0,0) = \frac{1}{2(M-2\gamma)^3} (M-2\gamma)(\alpha\beta a^2) = \frac{\alpha\beta a^2}{2(M-2\gamma)^2}
$$
This example [@problem_id:1097488], along with similar calculations [@problem_id:1097389], demonstrates that the Berry curvature is a well-defined local property of the band structure that can be computed directly from the Hamiltonian.

### Symmetry Constraints on Berry Curvature

Symmetries of the crystal and Hamiltonian impose powerful constraints on the form of the Berry curvature, which in turn dictates the possibility of various topological phenomena.

**Time-Reversal Symmetry (TRS):** The time-reversal operator $\mathcal{T}$ is an [anti-unitary operator](@entry_id:149378) that reverses momentum, $\mathcal{T}: \mathbf{k} \to -\mathbf{k}$. For a system with TRS, the Berry curvature of a non-degenerate band must be an [odd function](@entry_id:175940) of momentum:
$$
\boldsymbol{\Omega}_n(-\mathbf{k}) = -\boldsymbol{\Omega}_n(\mathbf{k})
$$
This can be demonstrated by analyzing the transformation properties of the Bloch states and the definition of the Berry connection [@problem_id:1097401]. An immediate consequence is that the integral of the Berry curvature over the entire Brillouin zone, which is symmetric under $\mathbf{k} \to -\mathbf{k}$, must vanish for any system possessing TRS.

**Inversion Symmetry (IS):** The inversion operator $\mathcal{P}$ also maps $\mathbf{k} \to -\mathbf{k}$. For a system with IS, the Berry curvature is an [even function](@entry_id:164802) of momentum:
$$
\boldsymbol{\Omega}_n(-\mathbf{k}) = \boldsymbol{\Omega}_n(\mathbf{k})
$$

**Combined TRS and IS:** If a system possesses both time-reversal and [inversion symmetry](@entry_id:269948), the two constraints must hold simultaneously. This implies $\boldsymbol{\Omega}_n(\mathbf{k}) = \boldsymbol{\Omega}_n(-\mathbf{k}) = -\boldsymbol{\Omega}_n(\mathbf{k})$, which can only be satisfied if the Berry curvature is identically zero everywhere in the Brillouin zone: $\boldsymbol{\Omega}_n(\mathbf{k}) \equiv 0$ [@problem_id:1097409]. Such systems cannot exhibit phenomena like the anomalous Hall effect, which rely on non-zero Berry curvature. Similar constraints arise from other symmetries, such as the combination of a two-fold rotation and time reversal, $\mathcal{S} = C_2\mathcal{T}$ [@problem_id:1097498].

**Chiral Symmetry:** A Hamiltonian has chiral symmetry if there exists a [unitary operator](@entry_id:155165) $\mathcal{C}$ such that $\mathcal{C}H(\mathbf{k})\mathcal{C}^\dagger = -H(\mathbf{k})$. This symmetry relates eigenstates with energy $E_n$ to eigenstates with energy $-E_n$. It can be shown that the Berry curvature of these partner bands are equal: $\boldsymbol{\Omega}_{n}(\mathbf{k}) = \boldsymbol{\Omega}_{-n}(\mathbf{k})$. For a gapped insulator, this implies that the total Berry curvature flux of the occupied (negative energy) bands is equal to that of the unoccupied (positive energy) bands. Since the sum over all bands must be zero, this forces the total flux for the occupied bands to be zero [@problem_id:1097469].

### Topological Invariants: The Chern Number

While the Berry curvature is a local property, its global integral over the entire Brillouin zone reveals a profound topological property. For a two-dimensional system, the integral of the Berry curvature for a given band $n$, when normalized, yields an integer known as the **first Chern number** or simply the **Chern number**, $C_n$:
$$
C_n = \frac{1}{2\pi} \int_{\text{BZ}} \Omega_n(\mathbf{k}) \, d^2k
$$
This number is a **[topological invariant](@entry_id:142028)**. It is robust against any smooth deformation of the Hamiltonian (e.g., changing hopping parameters) as long as the energy gap to other bands remains open [@problem_id:2955790]. The Chern number can only change its integer value when a band gap closes, which corresponds to a [topological phase transition](@entry_id:137214).

A powerful way to conceptualize the origin of the Chern number is to imagine the map $\mathbf{d}(\mathbf{k})$ from the 2D Brillouin zone (which has the [topology of a torus](@entry_id:271267)) to the space of the $\mathbf{d}$-vector (which, for its direction, is a sphere). The Chern [number counts](@entry_id:160205) how many times the vector $\mathbf{d}(\mathbf{k})$ wraps around the origin as $\mathbf{k}$ covers the entire Brillouin zone.

Furthermore, we can understand the change in Chern number by considering an extended parameter space, for instance by including a mass parameter $m$ in the Hamiltonian, $H(\mathbf{k}, m)$. The points $(\mathbf{k}_0, m_0)$ where the gap closes, $\mathbf{d}(\mathbf{k}_0, m_0)=0$, act as sources or sinks of Berry curvature flux. These points can be viewed as fictitious **magnetic monopoles** in the three-dimensional $(\mathbf{k}, m)$ parameter space [@problem_id:1097395]. The Chern number of the system for a given mass $m$ is then simply the sum of the charges of all monopoles with mass parameter less than $m$. The charge of each monopole is quantized to be a half-integer, typically $\pm 1/2$. For a model with vector $\mathbf{d}(\mathbf{k}, m) = (t_1\sin(k_x a), t_1\sin(k_y a), m - t_2(\cos(k_x a) + \cos(k_y a)))$, one can find four such monopoles in the full [parameter space](@entry_id:178581), located at specific values of $\mathbf{k}$ and $m$. The sum of the [absolute values](@entry_id:197463) of their charges is $\sum|Q_M| = 4 \times |\pm 1/2| = 2$ [@problem_id:1097395].

### Physical Manifestations of Berry Curvature

The abstract geometry of Bloch bands has tangible consequences in a variety of physical phenomena.

#### Anomalous Velocity and the Anomalous Hall Effect
The [semiclassical equations of motion](@entry_id:138500) for an electron wavepacket are modified by the Berry curvature. In addition to the standard [group velocity](@entry_id:147686), $\mathbf{v}_g = \frac{1}{\hbar}\nabla_{\mathbf{k}} E_n$, there is an **[anomalous velocity](@entry_id:146502)** term that is perpendicular to any applied external force $\mathbf{F}_{\text{ext}} = \hbar \dot{\mathbf{k}}$:
$$
\dot{\mathbf{r}} = \frac{1}{\hbar} \frac{\partial E_n}{\partial \mathbf{k}} + \dot{\mathbf{k}} \times \boldsymbol{\Omega}_n(\mathbf{k})
$$
The second term, $\mathbf{v}_{\text{an}} = \dot{\mathbf{k}} \times \boldsymbol{\Omega}_n(\mathbf{k})$, is the [anomalous velocity](@entry_id:146502) [@problem_id:1097495]. If an electric field $\mathbf{E}$ is applied, it exerts a force $\mathbf{F}_{\text{ext}}=-e\mathbf{E}$, causing $\mathbf{k}$ to change. The [anomalous velocity](@entry_id:146502) term generates a current transverse to the applied field, even in the absence of a magnetic field. This is the intrinsic **anomalous Hall effect**. At zero temperature, the total contribution from all filled bands results in a Hall conductivity $\sigma_{xy}$ that is directly proportional to the total Chern number of the occupied bands, $C_{occ}$:
$$
\sigma_{xy} = \frac{e^2}{h} C_{occ}
$$
This stunning result connects a [bulk transport](@entry_id:142158) measurement to a quantized topological invariant of the ground state [@problem_id:1097455]. A non-zero Chern number, and thus a quantized Hall conductivity, is the defining characteristic of a Chern insulator.

#### Adiabatic Pumping
The concept of a Chern number can be extended to pumping cycles. Consider a one-dimensional system whose Hamiltonian depends on a parameter that is varied cyclically and adiabatically in time. The extended [parameter space](@entry_id:178581), consisting of momentum $k$ and time $t$, forms a 2D torus. The integral of the Berry curvature over this synthetic torus is also a quantized Chern number. Thouless showed that this integer corresponds to the number of electrons pumped through the system in one cycle. The Rice-Mele model is the canonical example, where a cyclic variation of hopping amplitudes and on-site potentials can pump exactly one electron charge $e$ across the chain if the path in [parameter space](@entry_id:178581) encloses a topological transition point [@problem_id:1097427].

#### Modern Theory of Electric Polarization
The Berry phase formalism also provides the foundation for the [modern theory of electric polarization](@entry_id:147035). The classical expression for polarization is ill-defined in a periodic solid. The modern theory redefines the electronic contribution to polarization $\mathbf{P}_e$ as an integral of the Berry connection (not curvature) over the Brillouin zone:
$$
\mathbf{P}_e = -\frac{e}{(2\pi)^3} \sum_{n \in \text{occ}} \int_{\text{BZ}} \mathbf{A}_n(\mathbf{k}) \, d^3k
$$
Because the Berry connection is gauge-dependent, the absolute value of polarization is not unique. It is only defined up to a **quantum of polarization**, $\mathbf{P}_q = e\mathbf{R}/\Omega$, where $\mathbf{R}$ is a lattice vector and $\Omega$ is the unit cell volume [@problem_id:2989541]. This ambiguity is a fundamental feature, not a flaw, and reflects the freedom to shift the electronic charge center by a full lattice vector without changing the bulk physics. However, *changes* in polarization are uniquely defined and correspond to physically measurable quantities like surface charge.

#### The Quantum Hall Effect
In the integer quantum Hall effect, a strong perpendicular magnetic field $B$ modifies the band structure into a set of flat Landau levels. The Streda formula provides a deep connection between transport and thermodynamics, relating the Hall conductivity to the derivative of the electron density $n$ with respect to the magnetic field at a fixed chemical potential $\mu$: $\sigma_{xy} = e (\partial n / \partial B)_\mu$. The topology of the magnetic bands is captured by the Diophantine equation, which relates the band index to the Chern numbers of the magnetic sub-bands. This framework allows for the calculation of the quantized Hall plateaus from fundamental principles [@problem_id:1097474].

### Generalizations: Quantum Metric and Non-Abelian Curvature

The geometric description of Bloch bands can be extended in two important directions.

First, the Berry curvature is only part of a larger structure. The full **quantum geometric tensor** is defined as $Q_{ij}^{(n)} = \langle \partial_i u_n | (1 - |u_n\rangle\langle u_n|) | \partial_j u_n \rangle$. Its imaginary part is proportional to the Berry curvature, $\text{Im}(Q_{ij}) = \frac{1}{2}\Omega_{ij}$. Its real part is the **[quantum metric](@entry_id:139548) tensor**, $g_{ij} = \text{Re}(Q_{ij})$, which defines a metric, or a notion of distance, on the manifold of quantum states parameterized by $\mathbf{k}$. For a two-band model, the trace of the [quantum metric](@entry_id:139548) for the lower band is given by $\text{tr}[g] = \frac{1}{4d^2} [ \sum_{i,j}(\partial_i d_j)^2 - \sum_i(\partial_i d)^2 ]$ [@problem_id:1097400]. There exists a fundamental inequality $\sqrt{\det g} \ge |\Omega|/2$, relating the [volume element](@entry_id:267802) of the metric to the curvature. In certain idealized models, this inequality is saturated, and the total "volume" of the Brillouin zone, as measured by the [quantum metric](@entry_id:139548), is directly proportional to the Chern number [@problem_id:1097391].

Second, when two or more bands are degenerate, the concepts of Berry [connection and curvature](@entry_id:158520) must be generalized. The eigenstates form a vector space, and the [connection and curvature](@entry_id:158520) become $N \times N$ matrices, where $N$ is the number of degenerate bands. This is the realm of **non-Abelian Berry curvature**, analogous to Yang-Mills fields in particle physics. The non-Abelian Berry curvature is defined as:
$$
\Omega_{ij}(\mathbf{k}) = \partial_i A_j - \partial_j A_i - i [A_i, A_j]
$$
The new commutator term is necessary because the matrix-valued connections $A_i$ do not, in general, commute. Under a gauge transformation (a change of basis within the degenerate subspace) by a [unitary matrix](@entry_id:138978) $U(\mathbf{k})$, the curvature transforms covariantly: $\Omega'_{ij} = U \Omega_{ij} U^\dagger$ [@problem_id:1097478]. Because of this, the trace of a single curvature matrix is not gauge invariant. However, traces of products, such as $\text{Tr}[\Omega_{ij}\Omega_{kl}]$, are gauge invariant and form the basis for constructing higher-order topological invariants [@problem_id:1097478]. This non-Abelian framework is essential for describing [topological phases](@entry_id:141674) in systems with protected degeneracies, such as those arising from spatial symmetries [@problem_id:1097453], and can be probed using tools like the non-Abelian Wilson loop [@problem_id:1097457].

In summary, the geometry of Bloch wavefunctions, encoded in the Berry phase, connection, and curvature, is a rich and powerful concept. It provides a unifying language for describing a vast range of phenomena, from the polarization of insulators to the [quantized conductance](@entry_id:138407) of [topological materials](@entry_id:142123), and offers a beautiful bridge between the microscopic quantum world and macroscopic observable effects.