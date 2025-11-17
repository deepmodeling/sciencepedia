## Introduction
In the study of [quantum many-body physics](@entry_id:141705), a central challenge lies in understanding the collective behavior of strongly interacting particles. How do the static, structural correlations in a system's ground state govern its dynamic response to perturbations? The Bijl-Feynman theory offers a brilliantly intuitive and powerful answer to this question, providing a foundational framework for the [elementary excitations](@entry_id:140859) in [quantum liquids](@entry_id:157479) like superfluid Helium-4. It elegantly bridges the gap between static structure, measurable in scattering experiments, and the energy spectrum of collective modes.

This article provides a comprehensive exploration of this cornerstone theory. In the first chapter, **Principles and Mechanisms**, we will derive the theory from a variational ansatz, culminating in the celebrated Feynman formula that connects excitation energy to the [static structure factor](@entry_id:141682). The second chapter, **Applications and Interdisciplinary Connections**, will showcase the theory's remarkable predictive power, from explaining the famous [roton minimum](@entry_id:138478) in helium to describing [plasmons](@entry_id:146184) in electron gases and anisotropic modes in [ultracold atoms](@entry_id:137057). Finally, the **Hands-On Practices** chapter will solidify your understanding by guiding you through key calculations that test the theory's consistency and apply it to predict physical phenomena.

## Principles and Mechanisms

The Bijl-Feynman theory provides a foundational and remarkably insightful framework for understanding the [elementary excitations](@entry_id:140859) in [quantum many-body systems](@entry_id:141221), particularly [quantum liquids](@entry_id:157479) like superfluid Helium-4. It establishes a profound connection between the dynamic properties of a system (its [excitation spectrum](@entry_id:139562)) and its static, structural properties in the ground state (its [correlation functions](@entry_id:146839)). This chapter will elucidate the core principles of the theory, beginning with the construction of the [variational wavefunction](@entry_id:144043) and culminating in the celebrated formula for the excitation energy.

### The Feynman Variational Ansatz

The central idea proposed by Richard Feynman, building upon earlier work by A. Bijl, is to construct a [trial wavefunction](@entry_id:142892) for an elementary excitation by introducing a small, collective density fluctuation into the system's exact ground state. Let us consider a system of $N$ identical spinless bosons, each of mass $m$, described by a translationally invariant Hamiltonian $\hat{H}$. The exact, normalized ground state of this system is denoted by $|\Psi_0\rangle$, which has an energy $E_0$ and a total momentum of zero.

To create an excitation carrying a well-defined momentum $\hbar\mathbf{k}$, we act on the ground state with the **density fluctuation operator**, $\hat{\rho}_{\mathbf{k}}$, defined as the Fourier component of the particle [density operator](@entry_id:138151):
$$
\hat{\rho}_{\mathbf{k}} = \sum_{j=1}^N e^{-i\mathbf{k} \cdot \mathbf{r}_j}
$$
The Hermitian conjugate of this operator is $\hat{\rho}_{\mathbf{k}}^{\dagger} = \hat{\rho}_{-\mathbf{k}}$. The unnormalized Feynman [trial wavefunction](@entry_id:142892) for an excitation of [wavevector](@entry_id:178620) $\mathbf{k}$ is thus given by:
$$
|\Psi_{\mathbf{k}}\rangle_{unnorm} = \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle
$$
This state has a clear physical interpretation: it represents a plane-wave density [modulation](@entry_id:260640) of [wavevector](@entry_id:178620) $\mathbf{k}$ superimposed upon the intricate, correlated structure of the many-body ground state. Because $\hat{\rho}_{\mathbf{k}}$ is constructed as a sum of single-particle operators, it changes the total momentum of the state from zero to $\hbar\mathbf{k}$, correctly identifying it as an excited state.

To be a useful variational state, we must normalize it. The squared norm is given by the ground-state [expectation value](@entry_id:150961):
$$
\langle\Psi_{\mathbf{k}}|\Psi_{\mathbf{k}}\rangle_{unnorm} = \langle\Psi_0| \hat{\rho}_{\mathbf{k}}^{\dagger} \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle = \langle\Psi_0| \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle
$$
This quantity is of central importance and is directly related to the **[static structure factor](@entry_id:141682)**, $S(\mathbf{k})$, a function measurable in elastic neutron or X-ray scattering experiments. It is defined as:
$$
S(\mathbf{k}) = \frac{1}{N} \langle\Psi_0| \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle
$$
$S(\mathbf{k})$ encapsulates information about the two-particle correlations in the ground state. Using this definition, the normalized Feynman state is:
$$
|\Psi_{\mathbf{k}}\rangle = \frac{1}{\sqrt{N S(\mathbf{k})}} \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle
$$
These Feynman states form a remarkably well-behaved basis. For two distinct wavevectors, $\mathbf{k} \neq \mathbf{k}'$, the states are orthogonal, i.e., $\langle \Psi_{\mathbf{k}'} | \Psi_{\mathbf{k}} \rangle = 0$ [@problem_id:1098949]. This orthogonality arises from the [translational invariance](@entry_id:195885) of the ground state. Furthermore, the Hamiltonian has no off-[diagonal matrix](@entry_id:637782) elements between these states: $\langle \Psi_{\mathbf{k}'} | \hat{H} | \Psi_{\mathbf{k}} \rangle = 0$ for $\mathbf{k} \neq \mathbf{k}'$ [@problem_id:1099000]. This implies that, to a first approximation, the Feynman states represent a set of non-interacting [elementary excitations](@entry_id:140859), making them an excellent starting point for a perturbation theory of the excited-state spectrum.

### The Bijl-Feynman Excitation Spectrum

The [variational principle](@entry_id:145218) allows us to estimate the energy of the excitation, $\epsilon(\mathbf{k})$, by calculating the expectation value of the energy increase in the trial state:
$$
\epsilon(\mathbf{k}) = \frac{\langle \Psi_{\mathbf{k}} | \hat{H} | \Psi_{\mathbf{k}} \rangle}{\langle \Psi_{\mathbf{k}} | \Psi_{\mathbf{k}} \rangle} - E_0 = \frac{\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{H} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle}{\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle} - E_0
$$
Since $|\Psi_0\rangle$ is an [eigenstate](@entry_id:202009) of $\hat{H}$, we can write $\hat{H} \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle = (\hat{\rho}_{\mathbf{k}} \hat{H} + [\hat{H}, \hat{\rho}_{\mathbf{k}}]) |\Psi_0\rangle = E_0 \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle + [\hat{H}, \hat{\rho}_{\mathbf{k}}] |\Psi_0\rangle$. Substituting this into the numerator gives:
$$
\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} (E_0 \hat{\rho}_{\mathbf{k}} + [\hat{H}, \hat{\rho}_{\mathbf{k}}]) | \Psi_0 \rangle = E_0 \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle + \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} [\hat{H}, \hat{\rho}_{\mathbf{k}}] | \Psi_0 \rangle
$$
The excitation energy thus simplifies to:
$$
\epsilon(\mathbf{k}) = \frac{\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} [\hat{H}, \hat{\rho}_{\mathbf{k}}] | \Psi_0 \rangle}{N S(\mathbf{k})}
$$
The numerator can be related to the [expectation value](@entry_id:150961) of the double commutator $[[\hat{H}, \hat{\rho}_{\mathbf{k}}], \hat{\rho}_{-\mathbf{k}}]$ and is connected to the [f-sum rule](@entry_id:147775), as explored in the hands-on practices.