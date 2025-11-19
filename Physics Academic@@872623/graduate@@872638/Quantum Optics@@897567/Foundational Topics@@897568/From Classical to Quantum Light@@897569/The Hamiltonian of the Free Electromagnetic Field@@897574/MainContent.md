## Introduction
The [quantization of the electromagnetic field](@entry_id:155376) is a foundational pillar of quantum optics, providing the essential bridge between the classical [wave theory of light](@entry_id:173307) and its observed particle-like nature. The central challenge lies in transitioning from a continuous field description to a quantum theory of discrete energy packets, or photons. The most systematic path for this transition is the Hamiltonian formalism, which reformulates the field's energy in a way that is ripe for quantization. This article provides a comprehensive exploration of this process, establishing the Hamiltonian of the free electromagnetic field as a cornerstone of modern physics.

Across the following chapters, you will embark on a journey from first principles to practical applications. The first chapter, **Principles and Mechanisms**, meticulously derives the classical Hamiltonian and uses it to perform [canonical quantization](@entry_id:148501), revealing the profound insight that each field mode behaves as an independent [harmonic oscillator](@entry_id:155622). Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, showcases the remarkable utility of this Hamiltonian in explaining real-world phenomena like the Casimir effect and as a crucial tool in fields ranging from [condensed matter](@entry_id:747660) to cosmology. Finally, the **Hands-On Practices** section offers an opportunity to actively engage with the material, solidifying your understanding by applying the Hamiltonian to solve concrete quantum optical problems.

## Principles and Mechanisms

To understand the [quantum nature of light](@entry_id:270825), we must first establish a rigorous framework for describing the energy of the classical electromagnetic field. The transition from a classical to a quantum theory is most systematically achieved through the Hamiltonian formalism, which identifies the independent degrees of freedom of a system and its total energy. This chapter will first construct the classical Hamiltonian for the free electromagnetic field and then use it as a foundation for quantization, revealing the field's particle-like excitations—photons—and exploring the properties of the resulting quantum Hamiltonian.

### The Classical Hamiltonian of the Electromagnetic Field

The dynamics of a classical field can be described by a **Lagrangian density**, $\mathcal{L}$. For the free electromagnetic field in a vacuum, a convenient starting point is to describe the field using the [magnetic vector potential](@entry_id:141246) $\mathbf{A}(t, \mathbf{r})$ and the scalar potential $\phi(t, \mathbf{r})$. By choosing the **Coulomb gauge**, defined by the condition $\nabla \cdot \mathbf{A} = 0$, the dynamics in the absence of sources are simplified considerably. In this gauge, the [scalar potential](@entry_id:276177) can be set to zero ($\phi=0$), and the field's behavior is entirely captured by the vector potential $\mathbf{A}$. The electric and magnetic fields are then given by:

$$
\mathbf{E} = -\frac{\partial \mathbf{A}}{\partial t} \quad \text{and} \quad \mathbf{B} = \nabla \times \mathbf{A}
$$

The Lagrangian density, which is the kinetic energy density minus the potential energy density, can be expressed in terms of $\mathbf{A}$ as [@problem_id:2086079]:

$$
\mathcal{L} = \frac{\epsilon_0}{2} \left(\frac{\partial \mathbf{A}}{\partial t}\right)^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2
$$

Here, $\epsilon_0$ is the [permittivity](@entry_id:268350) and $\mu_0$ is the [permeability of free space](@entry_id:276113). The first term resembles a kinetic energy density, as it depends on the time derivative of $\mathbf{A}$, while the second term, depending on spatial derivatives, acts as a potential energy density.

To transition to the Hamiltonian formulation, we treat the components of the vector potential, $A_i(\mathbf{r})$, as the generalized field coordinates. The **canonical momentum density** $\mathbf{\Pi}$, conjugate to $\mathbf{A}$, is defined as the partial derivative of the Lagrangian density with respect to the "generalized velocity" $\dot{\mathbf{A}} = \partial \mathbf{A} / \partial t$. For each component $\pi_i$:

$$
\pi_i = \frac{\partial \mathcal{L}}{\partial \dot{A}_i} = \frac{\partial}{\partial \dot{A}_i} \left[ \frac{\epsilon_0}{2} \sum_j (\dot{A}_j)^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2 \right] = \epsilon_0 \dot{A}_i
$$

In vector form, $\mathbf{\Pi} = \epsilon_0 \dot{\mathbf{A}}$. We immediately see a direct physical meaning for the [canonical momentum](@entry_id:155151): it is proportional to the electric field, $\mathbf{\Pi} = -\epsilon_0 \mathbf{E}$.

The **Hamiltonian density** $\mathcal{H}$ is obtained via a Legendre transform of $\mathcal{L}$:

$$
\mathcal{H} = \mathbf{\Pi} \cdot \dot{\mathbf{A}} - \mathcal{L}
$$

Substituting the expressions for $\mathbf{\Pi}$ and $\mathcal{L}$ into this definition, we find:

$$
\mathcal{H} = (\epsilon_0 \dot{\mathbf{A}}) \cdot \dot{\mathbf{A}} - \left[ \frac{\epsilon_0}{2} \dot{\mathbf{A}}^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2 \right] = \frac{\epsilon_0}{2} \dot{\mathbf{A}}^2 + \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2
$$

Finally, by expressing this result in terms of the physical electric and magnetic fields using $\dot{\mathbf{A}} = -\mathbf{E}$ and $\nabla \times \mathbf{A} = \mathbf{B}$, we arrive at a celebrated result [@problem_id:2086079] [@problem_id:2071097]:

$$
\mathcal{H} = \frac{\epsilon_0}{2} \mathbf{E}^2 + \frac{1}{2\mu_0} \mathbf{B}^2
$$

This is precisely the well-known expression for the energy density of the electromagnetic field. The total Hamiltonian $H$, representing the total energy of the field in a given volume, is the integral of this density over that volume:

$$
H = \int \mathcal{H} \, d^3\mathbf{r} = \int \left( \frac{\epsilon_0}{2} \mathbf{E}^2 + \frac{1}{2\mu_0} \mathbf{B}^2 \right) d^3\mathbf{r}
$$

It is important to note that this fundamental expression for energy density is independent of the specific gauge or formulation used to derive it. For example, starting from the manifestly Lorentz-invariant Lagrangian density $\mathcal{L} = -\frac{1}{4} F_{\mu\nu} F^{\mu\nu}$, where $F_{\mu\nu}$ is the [electromagnetic field strength tensor](@entry_id:267409), and working in the temporal gauge ($A_0 = 0$), the same canonical procedure yields the identical Hamiltonian density, demonstrating the robustness of this physical result [@problem_id:66994].

### From Field Modes to Harmonic Oscillators

The Hamiltonian $H$ describes the total energy of the field, but for quantization, we need to identify the fundamental, independent degrees of freedom. The field $\mathbf{A}(\mathbf{r}, t)$ at each point in space cannot serve this role, as the fields at neighboring points are coupled through Maxwell's equations. The proper degrees of freedom are the **[normal modes](@entry_id:139640)** of the field. These modes represent collective oscillations of the entire field that evolve independently of one another. In free space, these modes are [plane waves](@entry_id:189798), each characterized by a [wavevector](@entry_id:178620) $\mathbf{k}$ and a polarization state $\lambda$.

To make this crucial connection explicit, let's consider a simplified model: a single electromagnetic mode in a one-dimensional cavity of length $L$ with perfectly conducting walls [@problem_id:756264]. The vector potential for the fundamental standing wave mode can be written as:

$$
\mathbf{A}(x, t) = \hat{y} \mathcal{N} \sin(kx) q(t)
$$

where $k = \pi/L$, $\mathcal{N}$ is a [normalization constant](@entry_id:190182), and $\hat{y}$ is a unit vector for the transverse polarization. Here, the entire spatial dependence is fixed by the mode function $\sin(kx)$, and the entire time dependence is encapsulated in a single generalized coordinate, $q(t)$.

The corresponding electric and magnetic fields are:

$$
\mathbf{E}(x,t) = -\frac{\partial \mathbf{A}}{\partial t} = -\hat{y} \mathcal{N} \sin(kx) \dot{q}(t)
$$
$$
\mathbf{B}(x,t) = \nabla \times \mathbf{A} = \hat{z} \mathcal{N} k \cos(kx) q(t)
$$

Now, we can calculate the total Hamiltonian by integrating the energy density over the volume of the cavity $V=SL$, where $S$ is the cross-sectional area:

$$
H = \int_0^L S \left[ \frac{\epsilon_0}{2} E_y^2 + \frac{1}{2\mu_0} B_z^2 \right] dx
$$
$$
H = S \int_0^L \left[ \frac{\epsilon_0}{2} \mathcal{N}^2 \sin^2(kx) \dot{q}(t)^2 + \frac{1}{2\mu_0} \mathcal{N}^2 k^2 \cos^2(kx) q(t)^2 \right] dx
$$

The integrals over the spatial coordinate are standard: $\int_0^L \sin^2(\frac{\pi x}{L}) dx = \int_0^L \cos^2(\frac{\pi x}{L}) dx = L/2$. Performing the integration, we find:

$$
H = \left( \frac{\epsilon_0 S \mathcal{N}^2 L}{4} \right) \dot{q}^2 + \left( \frac{\mathcal{N}^2 k^2 S L}{4\mu_0} \right) q^2
$$

Using the relation $c^2 = 1/(\epsilon_0 \mu_0)$, we can rewrite the coefficient of the $q^2$ term. If we let $\omega = ck = c\pi/L$ be the angular frequency of the mode, the expression simplifies to:

$$
H = \left( \frac{\epsilon_0 S \mathcal{N}^2 L}{4} \right) \dot{q}^2 + \left( \frac{\epsilon_0 S \mathcal{N}^2 L}{4} \right) \omega^2 q^2
$$

This expression has the unmistakable form of the Hamiltonian for a **mechanical harmonic oscillator**, $H = \frac{1}{2}m_{eff} \dot{q}^2 + \frac{1}{2}m_{eff} \omega^2 q^2$, where $m_{eff} = \epsilon_0 S \mathcal{N}^2 L / 2$ is an effective mass. This profound result is the cornerstone of quantum optics: **each independent mode of the electromagnetic field is dynamically equivalent to a simple harmonic oscillator**.

### The Quantum Hamiltonian: Photons as Excitations

The equivalence between [field modes](@entry_id:189270) and harmonic oscillators provides a clear path to quantization. We promote the generalized coordinate $q$ and its [conjugate momentum](@entry_id:172203) $p = \partial L / \partial \dot{q} = m_{eff} \dot{q}$ to [quantum operators](@entry_id:137703), $\hat{q}$ and $\hat{p}$, which obey the [canonical commutation relation](@entry_id:150454) $[\hat{q}, \hat{p}] = i\hbar$.

It is more convenient to work with the **annihilation** and **[creation operators](@entry_id:191512)**, defined for each oscillator (mode) as:

$$
\hat{a} = \sqrt{\frac{m_{eff}\omega}{2\hbar}}(\hat{q} + \frac{i}{m_{eff}\omega}\hat{p}) \quad \text{and} \quad \hat{a}^\dagger = \sqrt{\frac{m_{eff}\omega}{2\hbar}}(\hat{q} - \frac{i}{m_{eff}\omega}\hat{p})
$$

These operators satisfy the commutation relation $[\hat{a}, \hat{a}^\dagger] = 1$. The Hamiltonian for a single mode, in terms of these operators, becomes:

$$
\hat{H}_{\text{mode}} = \hbar\omega \left(\hat{a}^\dagger \hat{a} + \frac{1}{2}\right)
$$

Generalizing from our simple 1D cavity to the free field in three-dimensional space, each mode, identified by its wavevector $\mathbf{k}$ and polarization $\lambda$, is an independent harmonic oscillator. The total Hamiltonian of the free quantum electromagnetic field is the sum of the Hamiltonians for all these independent modes [@problem_id:717275]:

$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right)
$$

Here, $\omega_k = c|\mathbf{k}|$ is the mode frequency, and the operators $\hat{a}_{\mathbf{k}, \lambda}$ and $\hat{a}_{\mathbf{k}, \lambda}^\dagger$ annihilate and create excitations in the mode $(\mathbf{k}, \lambda)$. They satisfy the commutation relations appropriate for a continuous basis of modes (or a discrete basis if the field is confined to a finite volume).

The operator $\hat{N}_{\mathbf{k}, \lambda} = \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda}$ is the **[number operator](@entry_id:153568)**. Its eigenvalues are non-negative integers ($0, 1, 2, ...$) that count the number of [energy quanta](@entry_id:145536) in the mode $(\mathbf{k}, \lambda)$. These quanta of the electromagnetic field are what we call **photons**.

The ground state of the quantum field is the **vacuum state** $|0\rangle$, which is defined as the state containing no photons in any mode: $\hat{a}_{\mathbf{k}, \lambda}|0\rangle = 0$ for all $(\mathbf{k}, \lambda)$. The energy of the vacuum is found by applying the Hamiltonian:

$$
\hat{H}|0\rangle = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right) |0\rangle = \left( \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar \omega_k \right) |0\rangle
$$

The energy of the vacuum state, $E_{vac} = \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar \omega_k$, is the sum of the **zero-point energies** of all the field oscillators. This sum diverges, an issue we will return to shortly.

A single-photon state with wavevector $\mathbf{k}_0$ and polarization $\lambda_0$ is created by acting on the vacuum with the corresponding [creation operator](@entry_id:264870): $|\psi_{\mathbf{k}_0, \lambda_0}\rangle = \hat{a}_{\mathbf{k}_0, \lambda_0}^\dagger |0\rangle$. Let's find its energy [@problem_id:717275]:

$$
\hat{H} |\psi_{\mathbf{k}_0, \lambda_0}\rangle = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right) \hat{a}_{\mathbf{k}_0, \lambda_0}^\dagger |0\rangle
$$

Using the commutation relation to move $\hat{a}_{\mathbf{k}, \lambda}$ to the right, we have $\hat{a}_{\mathbf{k}, \lambda} \hat{a}_{\mathbf{k}_0, \lambda_0}^\dagger = \hat{a}_{\mathbf{k}_0, \lambda_0}^\dagger \hat{a}_{\mathbf{k}, \lambda} + \delta_{\mathbf{k}, \mathbf{k}_0}\delta_{\lambda, \lambda_0}$. The term with $\hat{a}_{\mathbf{k}, \lambda}$ on the right annihilates the vacuum. The only non-zero contribution comes from the commutator when $(\mathbf{k}, \lambda) = (\mathbf{k}_0, \lambda_0)$. This gives:

$$
\hat{H} |\psi_{\mathbf{k}_0, \lambda_0}\rangle = \left( \hbar\omega_{k_0} + \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar \omega_k \right) |\psi_{\mathbf{k}_0, \lambda_0}\rangle = (\hbar\omega_{k_0} + E_{vac}) |\psi_{\mathbf{k}_0, \lambda_0}\rangle
$$

The energy of the single-photon state is $E_{\psi} = E_{vac} + \hbar\omega_{k_0}$. The energy of the photon itself, relative to the vacuum, is $\Delta E = E_{\psi} - E_{vac} = \hbar\omega_{k_0} = \hbar c |\mathbf{k}_0|$. This confirms our interpretation: the Hamiltonian describes a collection of particles (photons), each carrying an energy proportional to its frequency.

### Properties of the Quantized Field

#### Zero-Point Energy and Normal Ordering

The infinite energy of the vacuum state, $E_{vac}$, is a pervasive feature of quantum field theory. In many applications, this infinite constant energy is unobservable because physical measurements typically detect energy *differences*. As we saw above, the energy of a photon is a well-defined finite quantity relative to the vacuum.

A common formal procedure to handle this infinity is **[normal ordering](@entry_id:145434)**, denoted by colons $: \dots :$. This operation prescribes that in any product of [creation and annihilation operators](@entry_id:147121), all [creation operators](@entry_id:191512) are to be moved to the left of all [annihilation operators](@entry_id:180957). For example, $: \hat{a}\hat{a}^\dagger : = \hat{a}^\dagger \hat{a}$. Applying this to the Hamiltonian effectively discards the commutator that gives rise to the zero-point energy term:

$$
:\hat{H}: \; = \sum_{\mathbf{k}, \lambda} \hbar \omega_k :\left( \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right): \; = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda}
$$

This normally ordered Hamiltonian, often used as the definition of the field's energy, has a [vacuum expectation value](@entry_id:146340) of zero by construction. This redefines the zero of energy to be the [vacuum energy](@entry_id:155067).

While often dismissed, the [zero-point energy](@entry_id:142176) is believed to have real physical consequences, such as the Casimir effect and its potential contribution to the [cosmological constant](@entry_id:159297). To explore this, one can employ a **regularization** scheme that renders the sum finite. For example, one can introduce a cutoff factor that suppresses high-frequency modes [@problem_id:756347]. Replacing the sum over modes with an integral in the large-volume limit ($\sum_{\mathbf{k}} \to V/(2\pi)^3 \int d^3k$), the regularized zero-point energy density $\mathcal{E}_0^{\text{reg}}$ in a medium with refractive index $n$ and with an exponential cutoff at frequency $\Omega$ can be calculated as:

$$
\mathcal{E}_0^{\text{reg}} = \frac{E_0^{\text{reg}}}{V} = \frac{2}{V} \sum_{\mathbf{k}} \frac{1}{2}\hbar\omega_k e^{-\omega_k/\Omega} = \frac{\hbar}{(2\pi)^3} \int_0^\infty 4\pi k^2 \left(\frac{c}{n}k\right) e^{-ck/(n\Omega)} dk = \frac{3\hbar n^3\Omega^4}{\pi^2c^3}
$$

The result depends on the arbitrary cutoff $\Omega$, but it shows how a finite energy density arises from the vacuum fluctuations. Different hypothetical modifications to physics at high energy would lead to different regularized values [@problem_id:327317].

#### Field Dynamics and Symmetries

In the Heisenberg picture, operators evolve in time according to the [equation of motion](@entry_id:264286) $i\hbar \frac{d\hat{O}}{dt} = [\hat{O}, \hat{H}]$. For an [annihilation operator](@entry_id:149476) of a specific mode $(\mathbf{k}', \lambda')$, the commutator is:

$$
[\hat{a}_{\mathbf{k}', \lambda'}, \hat{H}] = \left[\hat{a}_{\mathbf{k}', \lambda'}, \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda}\right] = \hbar \omega_{k'} \hat{a}_{\mathbf{k}', \lambda'}
$$

This leads to the [equation of motion](@entry_id:264286) $i\hbar \frac{d\hat{a}_{\mathbf{k}', \lambda'}}{dt} = \hbar \omega_{k'} \hat{a}_{\mathbf{k}', \lambda'}$, whose solution is a simple oscillation:

$$
\hat{a}_{\mathbf{k}', \lambda'}(t) = \hat{a}_{\mathbf{k}', \lambda'}(0) e^{-i\omega_{k'}t}
$$

This shows that the fundamental modes of the quantum field oscillate harmonically in time, just as their classical counterparts do. This simple [time evolution](@entry_id:153943) allows for the straightforward calculation of field correlation functions, which are central to describing the statistical properties of light [@problem_id:756323].

The Hamiltonian also determines the conservation laws of the system. The total momentum of the free field can be expressed as an operator by summing the momentum $\hbar\mathbf{k}$ of each photon, weighted by the number of photons in that mode [@problem_id:756384]:

$$
\mathbf{\hat{P}} = \sum_{\mathbf{k}, \lambda} \hbar \mathbf{k} \, \hat{a}^\dagger_{\mathbf{k}, \lambda} \hat{a}_{\mathbf{k}, \lambda}
$$

A direct calculation shows that the number operators for all modes commute with each other, $[ \hat{N}_{\mathbf{k},\lambda}, \hat{N}_{\mathbf{k}',\lambda'} ]=0$. Since both $\hat{H}$ and $\mathbf{\hat{P}}$ are constructed as sums of number operators (with different weighting factors), they must commute with each other:

$$
[\hat{H}, \mathbf{\hat{P}}] = 0
$$

This means that the total momentum of the free electromagnetic field is a conserved quantity. This conservation law is a direct consequence of the [translational symmetry](@entry_id:171614) of free space.

### Connecting the Field and Particle Pictures

We have two pictures of the quantum field: a collection of photons described by $\hat{a}$ and $\hat{a}^\dagger$, and the quantum electric and magnetic [field operators](@entry_id:140269), $\hat{\mathbf{E}}(\mathbf{r})$ and $\hat{\mathbf{B}}(\mathbf{r})$. These pictures are unified by expressing the [field operators](@entry_id:140269) as a superposition of all their modes, where the amplitude of each mode is determined by its [creation and annihilation operators](@entry_id:147121) [@problem_id:711806]. For the free field in a vacuum, these expansions are:

$$
\hat{\mathbf{E}}(\mathbf{r}) = i \sum_{\mathbf{k},\lambda} \sqrt{\frac{\hbar\omega_k}{2\epsilon_0 V}} \left( \mathbf{e}_{\mathbf{k}\lambda} \hat{a}_{\mathbf{k}\lambda} e^{i\mathbf{k}\cdot\mathbf{r}} - \mathbf{e}_{\mathbf{k}\lambda}^* \hat{a}_{\mathbf{k}\lambda}^\dagger e^{-i\mathbf{k}\cdot\mathbf{r}} \right)
$$
$$
\hat{\mathbf{B}}(\mathbf{r}) = i \sum_{\mathbf{k},\lambda} \sqrt{\frac{\hbar}{2\epsilon_0 \omega_k V}} \left( (\mathbf{k}\times\mathbf{e}_{\mathbf{k}\lambda}) \hat{a}_{\mathbf{k}\lambda} e^{i\mathbf{k}\cdot\mathbf{r}} - (\mathbf{k}\times\mathbf{e}_{\mathbf{k}\lambda}^*) \hat{a}_{\mathbf{k}\lambda}^\dagger e^{-i\mathbf{k}\cdot\mathbf{r}} \right)
$$
(Here written for a finite quantization volume $V$; the continuum version involves integrals over $\mathbf{k}$.)

These expressions show that the physical field at a point in space is a sum over all photon modes. Even in the vacuum state $|0\rangle$, where the expectation value of the fields is zero, their variance is not. This gives rise to **[vacuum fluctuations](@entry_id:154889)**—fleeting, virtual electromagnetic fields that exist even in the complete absence of photons, a purely quantum mechanical phenomenon [@problem_id:756264].

The final consistency check is to substitute these operator expansions back into the classical energy density expression and apply [normal ordering](@entry_id:145434). This procedure connects the field and particle representations of the energy. Calculating the normally ordered Hamiltonian $\hat{H} = \frac{1}{2}\int d^3\mathbf{r} :\!\left( \epsilon_0 \hat{\mathbf{E}}^2(\mathbf{r}) + \frac{1}{\mu_0} \hat{\mathbf{B}}^2(\mathbf{r}) \right)\!:$ leads, after significant algebra involving the orthogonality of the modes, back to the [diagonal form](@entry_id:264850) [@problem_id:711806]:

$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda}
$$

This result provides a beautiful and complete synthesis: the energy of the quantum electromagnetic field can be understood equivalently as the integrated energy density of the quantum [field operators](@entry_id:140269) or as the sum of the energies of its constituent photons. It is this dual nature, captured perfectly by the Hamiltonian, that lies at the heart of [quantum optics](@entry_id:140582).

Finally, it is worth noting that this entire quantization procedure applies to the **transverse** components of the electromagnetic field—the components that constitute radiation. In a more [complete theory](@entry_id:155100) including charges, the field's canonical momentum can be separated into transverse ($\nabla \cdot \mathbf{\Pi}_{\perp} = 0$) and longitudinal ($\nabla \times \mathbf{\Pi}_{\|} = 0$) parts. The Hamiltonian for the [transverse field](@entry_id:266489) gives rise to photons, while the energy associated with the longitudinal part, $\int \frac{1}{2\epsilon_0} \mathbf{\Pi}_{\|}^2 d^3\mathbf{r}$, can be shown to represent the instantaneous Coulomb interaction energy between the charges in the system [@problem_id:756413]. This formal separation clarifies that photons are the quanta of the radiating, transverse electromagnetic field.