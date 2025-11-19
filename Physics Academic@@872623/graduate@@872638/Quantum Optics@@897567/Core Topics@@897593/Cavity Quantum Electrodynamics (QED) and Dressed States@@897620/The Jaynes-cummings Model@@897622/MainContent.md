## Introduction
The interaction between a single quantum emitter and a single mode of light represents one of the most fundamental processes in quantum mechanics. Describing this [light-matter coupling](@entry_id:196079) with full quantum rigor is a complex challenge, yet it is essential for understanding phenomena ranging from spontaneous emission to the operation of quantum computers. The Jaynes-Cummings (JC) model addresses this by providing an elegant and exactly solvable framework that, despite its simplifying assumptions, captures the essential physics with remarkable accuracy. It has evolved from a theoretical curiosity into a foundational paradigm that drives innovation in quantum science and technology.

This article offers a graduate-level exploration of the Jaynes-Cummings model, designed to build a deep conceptual and practical understanding. Across three chapters, you will gain a comprehensive view of this pivotal model.
*   The first chapter, **Principles and Mechanisms**, deconstructs the Jaynes-Cummings Hamiltonian, explains the critical role of the Rotating Wave Approximation, and derives the "dressed state" picture that is central to its dynamics.
*   The second chapter, **Applications and Interdisciplinary Connections**, showcases how the model's predictions manifest in experimental cavity QED, serve as a blueprint for quantum technologies like circuit QED, and provide a unifying language that connects to condensed matter physics, chemistry, and even cosmology.
*   Finally, the **Hands-On Practices** chapter provides a series of targeted problems to solidify your grasp of the model's mathematical formalism and its connection to [physical observables](@entry_id:154692).

We will begin by deriving the model from first principles, establishing the Hamiltonian that governs this canonical quantum system.

## Principles and Mechanisms

The interaction between a single [two-level quantum system](@entry_id:190799) (an "atom") and a single mode of a quantized electromagnetic field provides one of the most fundamental paradigms in quantum optics. The Jaynes-Cummings model, which describes this system under specific, yet widely applicable, approximations, offers an exactly solvable framework that reveals profound quantum phenomena. This chapter elucidates the core principles and mechanisms of the Jaynes-Cummings model, from the construction of its Hamiltonian to the physical consequences of the interaction.

### The Jaynes-Cummings Hamiltonian

The starting point for describing a two-level atom interacting with a single cavity mode is the quantum Rabi Hamiltonian. However, in many experimental regimes, a simplified version, the Jaynes-Cummings (JC) Hamiltonian, is sufficient and offers much greater analytical tractability. The total Hamiltonian $H_{JC}$ for the system is composed of three distinct parts: the Hamiltonian of the free atom $H_A$, the Hamiltonian of the free cavity field $H_F$, and the interaction Hamiltonian $H_I$.

$$
H_{JC} = H_A + H_F + H_I
$$

Let us examine each component in detail [@problem_id:2134455].

The atom is modeled as a two-level system with a ground state $|g\rangle$ and an excited state $|e\rangle$, separated by an energy $\hbar \omega_a$, where $\omega_a$ is the atomic transition frequency. The free atomic Hamiltonian, $H_A$, can be expressed using the Pauli operator $\sigma_z = |e\rangle\langle e| - |g\rangle\langle g|$:

$$
H_A = \frac{1}{2}\hbar\omega_a \sigma_z
$$

This term describes the internal energy of the isolated atom. Its eigenvalues are $+\frac{1}{2}\hbar\omega_a$ for the excited state $|e\rangle$ and $-\frac{1}{2}\hbar\omega_a$ for the ground state $|g\rangle$, establishing the energy splitting of $\hbar\omega_a$.

The single mode of the quantized electromagnetic field within the cavity is modeled as a quantum harmonic oscillator with frequency $\omega_c$. Its Hamiltonian, $H_F$, is given by:

$$
H_F = \hbar\omega_c \left(a^\dagger a + \frac{1}{2}\right)
$$

Here, $a^\dagger$ and $a$ are the bosonic [creation and annihilation operators](@entry_id:147121) for photons in the cavity mode, satisfying the commutation relation $[a, a^\dagger] = 1$. The operator $N_{photon} = a^\dagger a$ is the photon [number operator](@entry_id:153568), whose eigenvalues are the non-negative integers $n=0, 1, 2, \dots$. The term $\frac{1}{2}\hbar\omega_c$ represents the zero-point energy of the cavity field, the minimum possible energy of the mode even in the absence of any photons.

The third component, $H_I$, describes the interaction between the atom and the field. In the Jaynes-Cummings model, this interaction is characterized by a [coupling constant](@entry_id:160679) $g$ and takes the form:

$$
H_I = \hbar g \left(\sigma_+ a + \sigma_- a^\dagger\right)
$$

The operators $\sigma_+ = |e\rangle\langle g|$ and $\sigma_- = |g\rangle\langle e|$ are the atomic [raising and lowering operators](@entry_id:153228), respectively. This interaction Hamiltonian encapsulates the fundamental processes of energy exchange. The term $\hbar g \sigma_+ a$ describes the atom transitioning from its ground state to its excited state while annihilating a photon from the cavity ($|g, n\rangle \rightarrow |e, n-1\rangle$). Conversely, the term $\hbar g \sigma_- a^\dagger$ describes the atom de-exciting from $|e\rangle$ to $|g\rangle$ while creating a photon in the cavity ($|e, n\rangle \rightarrow |g, n+1\rangle$) [@problem_id:2134495]. Crucially, both processes conserve the total number of excitations in the system, a feature we will explore in detail later. This form of the interaction is a direct result of a critical simplification known as the Rotating Wave Approximation.

### The Rotating Wave Approximation

The elegantly simple form of the Jaynes-Cummings interaction Hamiltonian is not fundamental; it is derived from a more general [light-matter interaction](@entry_id:142166) Hamiltonian by applying the **Rotating Wave Approximation (RWA)**. The full [dipole interaction](@entry_id:193339) between the atom and the field includes terms that correspond to all possible combinations of atomic and field operations. In [the interaction picture](@entry_id:198213) with respect to the free Hamiltonians of the atom and field, the interaction Hamiltonian $H'_I(t)$ is:

$$
H'_I(t) = \hbar g (\sigma_+ e^{i\omega_a t} + \sigma_- e^{-i\omega_a t})(a e^{-i\omega_c t} + a^\dagger e^{i\omega_c t})
$$

Expanding this expression reveals four distinct terms [@problem_id:2134470]:

$$
H'_I(t) = \hbar g \left[ \sigma_+ a e^{i(\omega_a - \omega_c)t} + \sigma_- a^\dagger e^{-i(\omega_a - \omega_c)t} + \sigma_+ a^\dagger e^{i(\omega_a + \omega_c)t} + \sigma_- a e^{-i(\omega_a + \omega_c)t} \right]
$$

The RWA is valid under the condition that the atom and cavity are near resonance, meaning the detuning $\Delta = \omega_a - \omega_c$ is small, and the coupling strength $g$ is much weaker than the transition frequencies themselves, i.e., $g \ll \omega_a, \omega_c$ [@problem_id:2134446]. Under these conditions, the terms containing the rapidly oscillating factors $e^{\pm i(\omega_a + \omega_c)t}$ average to nearly zero over the characteristic timescale of the system's evolution, which is governed by $g$ and $\Delta$. These rapidly oscillating terms are known as **[counter-rotating terms](@entry_id:153937)**. They correspond to highly non-energy-conserving processes: $\sigma_+ a^\dagger$ describes the simultaneous excitation of the atom and creation of a photon, while $\sigma_- a$ describes the simultaneous de-excitation of the atom and [annihilation](@entry_id:159364) of a photon.

The RWA consists of neglecting these [counter-rotating terms](@entry_id:153937). The remaining two terms, containing the slowly oscillating factor $e^{\pm i(\omega_a - \omega_c)t}$, are the **rotating terms**. When one transforms back to the Schrödinger picture, these terms give rise to the familiar interaction Hamiltonian $H_I = \hbar g (\sigma_+ a + \sigma_- a^\dagger)$. The RWA is thus an energy-conservation argument at its core, retaining only the processes that facilitate a resonant or near-resonant exchange of energy between the atom and the field.

### Conservation of Excitation Number and the Hilbert Space Structure

A profound consequence of the RWA is that the resulting Jaynes-Cummings Hamiltonian possesses a conserved quantity, which is not conserved by the full Rabi Hamiltonian. This conserved quantity is represented by the **total excitation [number operator](@entry_id:153568)**, defined as:

$$
N_{ex} = a^\dagger a + \sigma_+ \sigma_- = N_{photon} + |e\rangle\langle e|
$$

This operator simply counts the number of photons in the cavity and adds one if the atom is in its excited state. To demonstrate that $N_{ex}$ represents a conserved quantity, one must show that it commutes with the full Jaynes-Cummings Hamiltonian, $[H_{JC}, N_{ex}] = 0$ [@problem_id:2083516] [@problem_id:2134443]. The free parts, $H_A$ and $H_F$, naturally commute with $N_{ex}$ (at least when $\omega_a = \omega_c$; a slightly more careful calculation shows it holds generally). The crucial part is the commutator with the [interaction term](@entry_id:166280):

$$
[H_I, N_{ex}] = \hbar g [(\sigma_+ a + \sigma_- a^\dagger), (a^\dagger a + \sigma_+ \sigma_-)]
$$

Using the fundamental [commutation relations](@entry_id:136780), one can show that $[\sigma_+ a, N_{ex}] = 0$ and $[\sigma_- a^\dagger, N_{ex}] = 0$ individually. For instance, $[\sigma_- a^\dagger, a^\dagger a] = \sigma_- [a^\dagger, a^\dagger a] = - \sigma_- a^\dagger$, while $[\sigma_- a^\dagger, \sigma_+ \sigma_-] = a^\dagger [\sigma_-, \sigma_+ \sigma_-] = + a^\dagger \sigma_-$. The sum is zero. A similar cancellation occurs for the $\sigma_+ a$ term.

The conservation of the total excitation number, $[H_{JC}, N_{ex}] = 0$, has a powerful implication: the Hamiltonian does not induce transitions between states with different total excitation numbers. This means that the full, infinite-dimensional Hilbert space of the combined system, which is the tensor product of the atomic and field Hilbert spaces, decomposes into a [direct sum](@entry_id:156782) of much smaller, dynamically independent subspaces, each labeled by a specific eigenvalue $N$ of $N_{ex}$.

For $N=0$, the subspace is one-dimensional, containing only the absolute ground state of the system, $|g, 0\rangle$. This state has zero excitations (zero photons, atom in ground state) and is an [eigenstate](@entry_id:202009) of $H_{JC}$ with energy $E_{g,0} = -\frac{1}{2}\hbar\omega_a$.

For any integer $N \ge 1$, the subspace is two-dimensional, spanned by the pair of **bare states** $\{|e, N-1\rangle, |g, N\rangle\}$. Both of these states have a total of $N$ excitations. The dynamics of the Jaynes-Cummings model are entirely contained within this series of disjoint [two-level systems](@entry_id:196082), which greatly simplifies the task of finding the system's [eigenstates and eigenvalues](@entry_id:156160).

### Dressed States and the Jaynes-Cummings Ladder

Within each two-dimensional subspace of constant excitation number $N \ge 1$, the [interaction term](@entry_id:166280) of the Hamiltonian couples the two bare states. The [eigenstates](@entry_id:149904) of the full Hamiltonian are no longer the bare states but are superpositions of them. These new eigenstates are known as **dressed states**, as the interaction "dresses" the atom with the properties of the field, and vice versa.

To find the energies of these dressed states, we can write the Hamiltonian as a $2 \times 2$ matrix within the basis $\{|e, N-1\rangle, |g, N\rangle\}$. Let's consider the general case with detuning $\Delta = \omega_a - \omega_c$. The matrix representation of $H_{JC}$ in this subspace is:
$$
H_N = \begin{pmatrix} \langle e, N-1 | H_{JC} | e, N-1 \rangle  \langle e, N-1 | H_{JC} | g, N \rangle \\ \langle g, N | H_{JC} | e, N-1 \rangle  \langle g, N | H_{JC} | g, N \rangle \end{pmatrix}
$$

Calculating the [matrix elements](@entry_id:186505) yields:
$$
H_N = \begin{pmatrix} \hbar\omega_c(N-1) + \frac{1}{2}\hbar\omega_a  \hbar g\sqrt{N} \\ \hbar g\sqrt{N}  \hbar\omega_c N - \frac{1}{2}\hbar\omega_a \end{pmatrix}
$$

The eigenvalues of this matrix are the energies of the dressed states, denoted $E_{N,+}$ and $E_{N,-}$:
$$
E_{N, \pm} = \hbar\omega_c\left(N-\frac{1}{2}\right) \pm \frac{1}{2}\hbar\sqrt{\Delta^2 + 4g^2 N}
$$
The quantity $\Omega_N = 2g\sqrt{N}$ is known as the generalized Rabi frequency for the $N$-excitation manifold.

This result reveals a characteristic energy level structure known as the **Jaynes-Cummings ladder**. The single ground state $|g, 0\rangle$ stands alone. For each $N \ge 1$, the degeneracy (or [near-degeneracy](@entry_id:172107)) of the bare states $|e, N-1\rangle$ and $|g, N\rangle$ is lifted by the interaction, creating a doublet of dressed states $|N, +\rangle$ and $|N, -\rangle$ separated in energy by $\hbar\sqrt{\Delta^2 + (2g\sqrt{N})^2}$.

A particularly important case arises for $N=1$ at exact resonance ($\Delta=0$) [@problem_id:1105511]. The bare states $|e, 0\rangle$ (excited atom, no photons) and $|g, 1\rangle$ (ground-state atom, one photon) are degenerate in energy. The interaction splits them into a doublet of dressed states, $|1, \pm\rangle = \frac{1}{\sqrt{2}}(|g, 1\rangle \pm |e, 0\rangle)$, with an energy separation of:
$$
\Delta E_1 = E_{1,+} - E_{1,-} = 2\hbar g
$$
This splitting is known as the **vacuum Rabi splitting**. The name arises because the splitting occurs even for a single quantum of excitation, which can be viewed as the atom interacting with the vacuum fluctuations of the cavity field. Observing this splitting is a definitive sign of the **[strong coupling regime](@entry_id:143581)** of cavity QED, where the coherent energy exchange rate $g$ is faster than the decoherence rates of the system. This phenomenon is readily observed in modern experiments, such as circuit QED systems where a superconducting qubit interacts with a [microwave resonator](@entry_id:189295), leading to a measurable frequency separation of $2g/(2\pi)$ [@problem_id:2134469]. The splitting for higher manifolds increases as $\sqrt{N}$, as demonstrated for the $N=2$ manifold spanned by $\{|e,1\rangle, |g,2\rangle\}$, where the splitting is $2\hbar g\sqrt{2}$ at resonance [@problem_id:2134478].

### Beyond the Rotating Wave Approximation: The Bloch-Siegert Shift

While the RWA and the resulting Jaynes-Cummings model are remarkably successful, the neglected [counter-rotating terms](@entry_id:153937) do have a physical effect, especially as the [coupling strength](@entry_id:275517) $g$ becomes a significant fraction of the [resonant frequency](@entry_id:265742) $\omega_0$ (the [ultrastrong coupling](@entry_id:196561) regime). The influence of the [counter-rotating terms](@entry_id:153937) can be calculated using [perturbation theory](@entry_id:138766), treating $H_{CRT} = \hbar g(a\sigma_- + a^\dagger\sigma_+)$ as a perturbation on the exactly solvable Jaynes-Cummings Hamiltonian [@problem_id:2134494].

The [counter-rotating terms](@entry_id:153937) connect states that differ by two excitations, for example coupling the $N$-th manifold to the $(N+2)$-th and $(N-2)$-th manifolds. Consequently, the [first-order energy correction](@entry_id:143593), which is the expectation value of the perturbation in the unperturbed (dressed) states, is zero.
$$
\Delta E^{(1)} = \langle N, \pm | H_{CRT} | N, \pm \rangle = 0
$$

The leading correction comes from [second-order perturbation theory](@entry_id:192858). For a dressed state $|N, \pm\rangle$, the energy shift is given by summing over all other states $|M, \pm'\rangle$:
$$
\Delta E_{N, \pm}^{(2)} = \sum_{M, \pm' \neq N, \pm} \frac{|\langle M, \pm' | H_{CRT} | N, \pm \rangle|^2}{E_{N, \pm}^{(0)} - E_{M, \pm'}^{(0)}}
$$
The dominant contributions come from the states to which $|N, \pm\rangle$ is coupled, i.e., states in the $N\pm2$ manifolds. The energy denominators in this expression are approximately $\pm 2\hbar\omega_0$, since the manifolds are separated by a large energy. A detailed calculation for a state in any manifold, performed in the weak-coupling limit $g \ll \omega_0$, reveals a small, [negative energy](@entry_id:161542) shift. For the resonant case, this shift is:
$$
\Delta E^{(2)} \approx -\frac{\hbar g^2}{2\omega_0}
$$
This correction is known as the **Bloch-Siegert shift**. It represents a small lowering of the dressed state energies, or equivalently, a small increase in the effective transition frequency required to drive the system, caused by the virtual processes mediated by the [counter-rotating terms](@entry_id:153937). While often negligible, the Bloch-Siegert shift is a fundamental correction that becomes important in precision measurements and in the burgeoning field of ultrastrong-coupling cavity QED.