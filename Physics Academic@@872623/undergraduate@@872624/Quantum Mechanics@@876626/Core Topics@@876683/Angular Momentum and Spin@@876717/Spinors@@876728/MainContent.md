## Introduction
The quantum world is home to properties with no classical counterpart, chief among them being intrinsic angular momentum, or "spin." For particles like electrons, this property is quantized into just two possible states—"up" or "down"—a reality that cannot be described by familiar vectors or wavefunctions. This creates a fundamental need for a new mathematical language to articulate the physics of these [two-level systems](@entry_id:196082). This article introduces the spinor, the essential tool for describing spin. In the chapters that follow, you will first master the foundational "Principles and Mechanisms" of the spinor formalism, from Pauli matrices to the algebra of [spin operators](@entry_id:155419). Next, we will explore the far-reaching "Applications and Interdisciplinary Connections" of spinors, showing how they are crucial to technologies like MRI, the structure of matter, and even theories of relativity. Finally, the "Hands-On Practices" section will provide an opportunity to solidify your understanding by actively solving problems related to these core concepts.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of intrinsic angular momentum, or **spin**, as a fundamental property of quantum particles. Unlike classical angular momentum, spin is not associated with the spatial motion or rotation of a body but is an inherent quantum attribute. For a spin-1/2 particle, such as an electron, the projection of its [spin angular momentum](@entry_id:149719) onto any given axis is quantized, yielding only two possible values: $+\hbar/2$ or $-\hbar/2$. To describe the state of such a [two-level system](@entry_id:138452), we require a new mathematical object: the **spinor**. This chapter delves into the principles governing spinors, their relationship to physical observables, and the mechanisms of their evolution.

### The Spinor as a Quantum State Vector

The state of a spin-1/2 particle is described by a two-component column vector with complex entries, known as a **[spinor](@entry_id:154461)**. It is an element of a two-dimensional [complex vector space](@entry_id:153448), $\mathbb{C}^2$. We can represent a general spinor, denoted by $|\chi\rangle$, as:
$$
|\chi\rangle = \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix} = c_{\uparrow} \begin{pmatrix} 1 \\ 0 \end{pmatrix} + c_{\downarrow} \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
Here, the basis vectors $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$ and $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$ represent the spin-up and spin-down states along a conventionally chosen axis, usually the z-axis. The complex coefficients $c_{\uparrow}$ and $c_{\downarrow}$ are the **probability amplitudes**. According to the [postulates of quantum mechanics](@entry_id:265847), the probability of measuring the particle's spin to be "up" ($+\hbar/2$) is $|c_{\uparrow}|^2$, and the probability of measuring it to be "down" ($-\hbar/2$) is $|c_{\downarrow}|^2$.

Since the particle must be found in one of these two states, the total probability must be unity. This leads to the **[normalization condition](@entry_id:156486)**:
$$
|c_{\uparrow}|^2 + |c_{\downarrow}|^2 = 1
$$
This condition can be expressed more compactly using the **Hermitian conjugate** (or adjoint) of the [spinor](@entry_id:154461), denoted by $\langle\chi|$. The Hermitian conjugate is found by taking the transpose of the spinor and then the complex conjugate of its elements. For our general [spinor](@entry_id:154461) $|\chi\rangle$, its adjoint is the row vector $\langle\chi| = \begin{pmatrix} c_{\uparrow}^*  c_{\downarrow}^* \end{pmatrix}$. The [normalization condition](@entry_id:156486) is then written as the inner product of the [spinor](@entry_id:154461) with itself:
$$
\langle\chi|\chi\rangle = \begin{pmatrix} c_{\uparrow}^*  c_{\downarrow}^* \end{pmatrix} \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix} = c_{\uparrow}^*c_{\uparrow} + c_{\downarrow}^*c_{\downarrow} = |c_{\uparrow}|^2 + |c_{\downarrow}|^2 = 1
$$

In practice, we often encounter unnormalized state vectors that result from theoretical calculations. To render them physically meaningful, we must normalize them. For instance, consider a particle in a state described by the unnormalized spinor $|\chi'\rangle = \begin{pmatrix} 1-i \\ 2 \end{pmatrix}$. To normalize this, we introduce a positive real constant $N$, such that $|\chi\rangle = N|\chi'\rangle$ satisfies the [normalization condition](@entry_id:156486). The calculation proceeds as follows [@problem_id:2122894]:
$$
\langle\chi|\chi\rangle = N^2 \begin{pmatrix} (1-i)^*  2^* \end{pmatrix} \begin{pmatrix} 1-i \\ 2 \end{pmatrix} = N^2 \begin{pmatrix} 1+i  2 \end{pmatrix} \begin{pmatrix} 1-i \\ 2 \end{pmatrix} = N^2((1+i)(1-i) + (2)(2)) = N^2(2+4) = 6N^2
$$
Setting $6N^2 = 1$ gives $N = 1/\sqrt{6}$. The normalized [spinor](@entry_id:154461) is therefore $|\chi\rangle = \frac{1}{\sqrt{6}} \begin{pmatrix} 1-i \\ 2 \end{pmatrix}$.

### Spin Operators and Eigenstates

Physical [observables in quantum mechanics](@entry_id:152184) are represented by Hermitian operators. The operators corresponding to the components of the spin angular momentum vector $\vec{S} = (S_x, S_y, S_z)$ are given by:
$$
S_k = \frac{\hbar}{2} \sigma_k, \quad \text{for } k \in \{x, y, z\}
$$
where $\hbar$ is the reduced Planck constant and $\sigma_k$ are the three **Pauli matrices**:
$$
\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
The only possible outcomes of a measurement of an observable are the **eigenvalues** of its corresponding operator. A state is an **eigenstate** of an operator if the action of the operator on the state simply multiplies the state by a scalar (the eigenvalue). Let's find the [eigenstates and eigenvalues](@entry_id:156160) for the z-component of spin, $S_z$ [@problem_id:1398689]. The eigenvalue equation is $S_z |\chi\rangle = \lambda |\chi\rangle$, where $\lambda$ is the eigenvalue. In matrix form:
$$
\frac{\hbar}{2} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix} = \lambda \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix} \implies \frac{\hbar}{2} \begin{pmatrix} c_{\uparrow} \\ -c_{\downarrow} \end{pmatrix} = \begin{pmatrix} \lambda c_{\uparrow} \\ \lambda c_{\downarrow} \end{pmatrix}
$$
This gives two equations: $\frac{\hbar}{2} c_{\uparrow} = \lambda c_{\uparrow}$ and $-\frac{\hbar}{2} c_{\downarrow} = \lambda c_{\downarrow}$.
If $c_{\uparrow} \neq 0$, then $\lambda = +\hbar/2$, which forces $c_{\downarrow} = 0$. The normalized eigenstate is $|\uparrow_z\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$.
If $c_{\downarrow} \neq 0$, then $\lambda = -\hbar/2$, which forces $c_{\uparrow} = 0$. The normalized eigenstate is $|\downarrow_z\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$.
These two states, often called "spin-up" and "spin-down" along z, form the **standard basis** (or z-basis). Any [spinor](@entry_id:154461) proportional to these, such as $\begin{pmatrix} 3 \\ 0 \end{pmatrix}$ or $\begin{pmatrix} 0 \\ -2i \end{pmatrix}$, is also an eigenstate of $S_z$ with the respective eigenvalue. A state like $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$, however, is not an [eigenstate](@entry_id:202009) of $S_z$ because applying the $S_z$ operator does not return a multiple of the original vector.

The choice of the z-axis is arbitrary. We can equally well find the [eigenstates](@entry_id:149904) of spin along other axes. For example, let's find the spin-up [eigenstate](@entry_id:202009) of $S_y$, which we denote $|{\uparrow_y}\rangle$ [@problem_id:2122908]. We must solve the eigenvalue equation $S_y |{\uparrow_y}\rangle = +\frac{\hbar}{2} |{\uparrow_y}\rangle$:
$$
\frac{\hbar}{2} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix} = +\frac{\hbar}{2} \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix} \implies \begin{pmatrix} -i c_{\downarrow} \\ i c_{\uparrow} \end{pmatrix} = \begin{pmatrix} c_{\uparrow} \\ c_{\downarrow} \end{pmatrix}
$$
This yields the condition $c_{\downarrow} = i c_{\uparrow}$. Applying the [normalization condition](@entry_id:156486) $|c_{\uparrow}|^2 + |i c_{\uparrow}|^2 = 2|c_{\uparrow}|^2 = 1$ gives $|c_{\uparrow}| = 1/\sqrt{2}$. By convention, we can choose the phase to make the first component real and positive, so $c_{\uparrow} = 1/\sqrt{2}$ and $c_{\downarrow} = i/\sqrt{2}$. Thus, the normalized spin-up state along the y-axis is:
$$
|\uparrow_y\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ i \end{pmatrix} = \frac{1}{\sqrt{2}}|\uparrow_z\rangle + \frac{i}{\sqrt{2}}|\downarrow_z\rangle
$$
This result is profound. A state that has a definite spin value along the y-axis is a **superposition** of states with definite spin along the z-axis. It is impossible for a spin-1/2 particle to have a definite spin value along two different axes simultaneously.

### Spinors and Spatial Direction

We can generalize this procedure to find the spinor corresponding to a spin oriented along an arbitrary direction in 3D space, defined by a unit vector $\boldsymbol{n} = (\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$, where $\theta$ and $\phi$ are the polar and azimuthal angles. This spinor is the [eigenstate](@entry_id:202009) of the operator $\boldsymbol{n} \cdot \boldsymbol{S}$ with eigenvalue $+\hbar/2$ [@problem_id:1398679]. The operator is $\boldsymbol{n} \cdot \boldsymbol{S} = \frac{\hbar}{2}(\boldsymbol{n} \cdot \boldsymbol{\sigma})$, where:
$$
\boldsymbol{n} \cdot \boldsymbol{\sigma} = \sin\theta\cos\phi\,\sigma_x + \sin\theta\sin\phi\,\sigma_y + \cos\theta\,\sigma_z = \begin{pmatrix} \cos\theta & \sin\theta\,\exp(-i\phi) \\ \sin\theta\,\exp(i\phi) & -\cos\theta \end{pmatrix}
$$
Solving the [eigenvalue equation](@entry_id:272921) $(\boldsymbol{n} \cdot \boldsymbol{\sigma})|\chi\rangle = |\chi\rangle$ leads, after some algebra involving trigonometric half-angle identities, to the normalized spinor:
$$
|\chi(\theta, \phi)\rangle = \begin{pmatrix} \cos(\theta/2) \\ \exp(i\phi)\sin(\theta/2) \end{pmatrix}
$$
This remarkable formula connects the abstract algebraic [spinor](@entry_id:154461) to a concrete geometric direction. The appearance of half-angles ($\theta/2$) is a signature feature of spinors. It implies that a full spatial rotation of $2\pi$ causes the spinor to acquire a factor of -1. The [spinor](@entry_id:154461) is not restored to its original value; only its sign is flipped. To return the spinor to its original state, a rotation of $4\pi$ is required. This $4\pi$-[periodicity](@entry_id:152486) is a unique property of fermions, including electrons, and has observable consequences in interference experiments.

### The Algebra of Spin: Non-Commutation and Uncertainty

The fact that a definite spin state along one axis is a [superposition of states](@entry_id:273993) along another is a direct consequence of the [non-commutation](@entry_id:136599) of the [spin operators](@entry_id:155419). To investigate this, we compute the **commutator** of $S_x$ and $S_y$, defined as $[S_x, S_y] = S_x S_y - S_y S_x$. Using the Pauli [matrix representations](@entry_id:146025) [@problem_id:2122913]:
$$
S_x S_y = \left(\frac{\hbar}{2}\right)^2 \sigma_x \sigma_y = \frac{\hbar^2}{4} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} = \frac{\hbar^2}{4} \begin{pmatrix} i  0 \\ 0  -i \end{pmatrix} = i\frac{\hbar^2}{4} \sigma_z = i\frac{\hbar}{2} S_z
$$
$$
S_y S_x = \left(\frac{\hbar}{2}\right)^2 \sigma_y \sigma_x = \frac{\hbar^2}{4} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} = \frac{\hbar^2}{4} \begin{pmatrix} -i  0 \\ 0  i \end{pmatrix} = -i\frac{\hbar^2}{4} \sigma_z = -i\frac{\hbar}{2} S_z
$$
Subtracting these gives the fundamental **spin commutation relation**:
$$
[S_x, S_y] = i\hbar S_z
$$
The relations for other pairs can be found by cyclic permutation: $[S_y, S_z] = i\hbar S_x$ and $[S_z, S_x] = i\hbar S_y$. The fact that these commutators are non-zero is the mathematical statement that the corresponding observables are **incompatible**—they cannot be simultaneously measured to arbitrary precision.

This incompatibility is quantified by the **Heisenberg Uncertainty Principle**. For any two [observables](@entry_id:267133) $A$ and $B$, the product of their standard deviations (uncertainties) in any state $|\psi\rangle$ is bounded by:
$$
(\Delta A)(\Delta B) \ge \frac{1}{2} |\langle\psi| [A, B] |\psi\rangle|
$$
Applying this to $S_x$ and $S_y$, we have:
$$
(\Delta S_x)(\Delta S_y) \ge \frac{1}{2} |\langle [S_x, S_y] \rangle| = \frac{1}{2} |\langle i\hbar S_z \rangle| = \frac{\hbar}{2} |\langle S_z \rangle|
$$
Let's verify this for a particle prepared in the spin-down state along the z-axis, $|\psi\rangle = |\downarrow_z\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ [@problem_id:2122931]. In this state, the value of $S_z$ is definite ($-\hbar/2$), so $\langle S_z \rangle = -\hbar/2$. The uncertainty principle predicts $(\Delta S_x)(\Delta S_y) \ge \frac{\hbar}{2} |-\hbar/2| = \frac{\hbar^2}{4}$. An explicit calculation of the uncertainties confirms this. The expectation values of $S_x$ and $S_y$ are zero, and $\langle S_x^2 \rangle = \langle S_y^2 \rangle = \hbar^2/4$. The variances are $(\Delta S_x)^2 = \langle S_x^2 \rangle - \langle S_x \rangle^2 = \hbar^2/4$ and $(\Delta S_y)^2 = \langle S_y^2 \rangle - \langle S_y \rangle^2 = \hbar^2/4$. The product of the standard deviations is thus $(\Delta S_x)(\Delta S_y) = (\hbar/2)(\hbar/2) = \hbar^2/4$. The state saturates the uncertainty bound, making it a [minimum uncertainty state](@entry_id:193251) for $S_x$ and $S_y$.

### Spin Dynamics: Rotations

The evolution of a quantum state is governed by the Schrödinger equation. For spin states, this evolution often corresponds to a rotation of the spin vector. Such rotations are implemented by [unitary operators](@entry_id:151194). The operator for a rotation by an angle $\theta$ about an axis defined by the unit vector $\boldsymbol{n}$ is:
$$
U_{\boldsymbol{n}}(\theta) = \exp\left(-\frac{i\theta}{\hbar} \boldsymbol{n} \cdot \boldsymbol{S}\right) = \exp\left(-\frac{i\theta}{2} \boldsymbol{n} \cdot \boldsymbol{\sigma}\right)
$$
A key property of the Pauli matrices is that for any [unit vector](@entry_id:150575) $\boldsymbol{n}$, $(\boldsymbol{n} \cdot \boldsymbol{\sigma})^2 = I$, where $I$ is the $2 \times 2$ identity matrix. Using the Taylor series expansion of the exponential, this property leads to a simplified form of the [rotation operator](@entry_id:136702):
$$
U_{\boldsymbol{n}}(\theta) = I \cos(\theta/2) - i (\boldsymbol{n} \cdot \boldsymbol{\sigma}) \sin(\theta/2)
$$
As an example, let's determine the final state of a qubit initially in the spin-down state $|\downarrow_z\rangle$ after a rotation by an angle $\theta$ about the x-axis [@problem_id:1398685]. Here, $\boldsymbol{n} = (1, 0, 0)$ and the operator is $U_x(\theta) = I \cos(\theta/2) - i \sigma_x \sin(\theta/2)$. Applying this to $|\downarrow_z\rangle$:
$$
|\psi_f\rangle = U_x(\theta) \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \left(\cos(\theta/2) \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} - i \sin(\theta/2) \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}\right) \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
$$
|\psi_f\rangle = \cos(\theta/2) \begin{pmatrix} 0 \\ 1 \end{pmatrix} - i \sin(\theta/2) \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} -i \sin(\theta/2) \\ \cos(\theta/2) \end{pmatrix}
$$
This demonstrates how a precisely controlled interaction, modeled as a rotation, can coherently transform one spin state into another.

These rotation operators are the link between [state preparation](@entry_id:152204), evolution, and measurement. Consider a particle prepared in the spin-up state, $|\psi_i\rangle = |\uparrow_z\rangle$. It is subjected to a rotation by $\theta = \pi/3$ about the y-axis. What is the probability that a subsequent measurement of $S_x$ yields $+\hbar/2$? [@problem_id:1398656].
First, we find the state after rotation, $|\psi_f\rangle = U_y(\pi/3)|\uparrow_z\rangle$. The [rotation operator](@entry_id:136702) is $U_y(\theta) = I\cos(\theta/2) - i\sigma_y\sin(\theta/2)$. The final state is $|\psi_f\rangle = \begin{pmatrix} \cos(\theta/2) \\ \sin(\theta/2) \end{pmatrix}$.
The state corresponding to a measurement outcome of $+\hbar/2$ for $S_x$ is its spin-up eigenstate, $|{\uparrow_x}\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$.
The probability is the squared magnitude of the projection of the final state onto the measurement state: $P(+S_x) = |\langle {\uparrow_x} | \psi_f \rangle|^2$.
$$
\langle {\uparrow_x} | \psi_f \rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 1  1 \end{pmatrix} \begin{pmatrix} \cos(\theta/2) \\ \sin(\theta/2) \end{pmatrix} = \frac{1}{\sqrt{2}} (\cos(\theta/2) + \sin(\theta/2))
$$
The probability is $P(+S_x) = \frac{1}{2}(\cos(\theta/2) + \sin(\theta/2))^2 = \frac{1+\sin\theta}{2}$. For $\theta = \pi/3$, this gives $P = \frac{1+\sqrt{3}/2}{2} = \frac{2+\sqrt{3}}{4}$.

### Multi-Spin Systems

The formalism of spinors extends naturally to systems of multiple particles. The state space for a system of two spin-1/2 particles is the **tensor product** of their individual two-dimensional spaces, resulting in a four-dimensional space. The basis for this space can be formed from the product of the individual particle basis states:
$$
|\uparrow\uparrow\rangle \equiv |\uparrow\rangle_1 \otimes |\uparrow\rangle_2, \quad |\uparrow\downarrow\rangle \equiv |\uparrow\rangle_1 \otimes |\downarrow\rangle_2, \quad |\downarrow\uparrow\rangle \equiv |\downarrow\rangle_1 \otimes |\uparrow\rangle_2, \quad |\downarrow\downarrow\rangle \equiv |\downarrow\rangle_1 \otimes |\downarrow\rangle_2
$$
An operator acting on a single particle, like $S_{1z}$, is understood to act as $S_{1z} \otimes I_2$ on the combined space, where $I_2$ is the [identity operator](@entry_id:204623) for particle 2. For [non-interacting particles](@entry_id:152322), the Hamiltonian is simply the sum of individual Hamiltonians. For example, if two particles with gyromagnetic ratios $\gamma_1, \gamma_2$ are in z-oriented magnetic fields $B_1, B_2$, the Hamiltonian is $H = -\gamma_1 B_1 S_{1z} - \gamma_2 B_2 S_{2z}$. If the system is in the state $|\psi\rangle = |\downarrow_1\rangle|\uparrow_2\rangle$, its energy is found by applying the Hamiltonian [@problem_id:2122912]:
$$
H|\psi\rangle = (-\gamma_1 B_1 S_{1z})|\downarrow_1\rangle|\uparrow_2\rangle - \gamma_2 B_2 |\downarrow_1\rangle(S_{2z}|\uparrow_2\rangle) = -\gamma_1 B_1 (-\hbar/2)|\psi\rangle - \gamma_2 B_2 (+\hbar/2)|\psi\rangle = \frac{\hbar}{2}(\gamma_1 B_1 - \gamma_2 B_2)|\psi\rangle
$$
The energy is thus $E = \frac{\hbar}{2}(\gamma_1 B_1 - \gamma_2 B_2)$.

More interesting phenomena arise when spins interact. A common model for [spin-spin interaction](@entry_id:173966) is the **Heisenberg Hamiltonian**, $H_{int} = \frac{K}{\hbar^2} (\vec{S}_1 \cdot \vec{S}_2)$, where $K$ is a coupling constant. This interaction couples the spins, leading to **[entangled states](@entry_id:152310)** that cannot be written as a simple product of individual states. One such crucial entangled state is the triplet state $|\psi\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle)$. To find the interaction energy for this state, it is useful to rewrite the dot product using the total [spin operator](@entry_id:149715) $\vec{S} = \vec{S}_1 + \vec{S}_2$. From $\vec{S}^2 = (\vec{S}_1 + \vec{S}_2) \cdot (\vec{S}_1 + \vec{S}_2) = \vec{S}_1^2 + \vec{S}_2^2 + 2\vec{S}_1 \cdot \vec{S}_2$, we get $\vec{S}_1 \cdot \vec{S}_2 = \frac{1}{2}(\vec{S}^2 - \vec{S}_1^2 - \vec{S}_2^2)$.
The state $|\psi\rangle$ is an [eigenstate](@entry_id:202009) of total spin with quantum numbers $S=1$ and $M_S=0$. For any single spin-1/2 particle, the eigenvalue of $\vec{S}_i^2$ is $s(s+1)\hbar^2 = \frac{1}{2}(\frac{1}{2}+1)\hbar^2 = \frac{3}{4}\hbar^2$. For the [total spin](@entry_id:153335) state with $S=1$, the eigenvalue of $\vec{S}^2$ is $S(S+1)\hbar^2 = 1(1+1)\hbar^2 = 2\hbar^2$.
The [expectation value](@entry_id:150961) of the dot product is therefore [@problem_id:2122925]:
$$
\langle \vec{S}_1 \cdot \vec{S}_2 \rangle = \frac{1}{2} (\langle\vec{S}^2\rangle - \langle\vec{S}_1^2\rangle - \langle\vec{S}_2^2\rangle) = \frac{1}{2} (2\hbar^2 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2) = \frac{\hbar^2}{4}
$$
The interaction energy for this state is $\langle H_{int} \rangle = \frac{K}{\hbar^2}\langle \vec{S}_1 \cdot \vec{S}_2 \rangle = \frac{K}{\hbar^2} \frac{\hbar^2}{4} = \frac{K}{4}$. This example illustrates how the spinor formalism provides the foundation for understanding the complex and rich behavior of interacting, entangled quantum systems.