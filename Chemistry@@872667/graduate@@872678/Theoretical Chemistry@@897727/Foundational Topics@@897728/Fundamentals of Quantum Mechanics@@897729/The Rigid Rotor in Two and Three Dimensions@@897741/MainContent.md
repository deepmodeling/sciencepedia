## Introduction
The rotation of molecules is a fundamental motion that governs their interaction with light, their thermodynamic properties, and their reactivity. While classical mechanics can describe rotation, a full understanding requires the lens of quantum mechanics. The rigid rotor, a simple yet powerful model representing a molecule with a fixed structure rotating in space, provides the essential quantum framework. This article bridges the gap between the abstract mathematical formulation of the rigid rotor and its profound implications across chemistry and physics.

In the chapters that follow, we will embark on a comprehensive exploration of this cornerstone model. The first chapter, "Principles and Mechanisms," delves into the quantum mechanics of the 2D and 3D rigid rotor, deriving its quantized energy levels and wavefunctions, and exploring the deep connection between symmetry, degeneracy, and the fundamental laws of angular momentum. Subsequently, "Applications and Interdisciplinary Connections" demonstrates the model's predictive power, showing how it underpins [molecular spectroscopy](@entry_id:148164), statistical mechanics, and the theory of [chemical reaction rates](@entry_id:147315). Finally, "Hands-On Practices" will provide opportunities to apply these concepts to solve tangible problems in spectroscopy and thermodynamics, solidifying your understanding of the [rigid rotor](@entry_id:156317)'s role in modern physical chemistry.

## Principles and Mechanisms

### The Three-Dimensional Rigid Rotor: The Diatomic Molecule

The simplest realistic model for the [rotational motion](@entry_id:172639) of a diatomic molecule is the **rigid rotor**, where two point masses, $m_1$ and $m_2$, are separated by a fixed distance, $R$. This system is free to rotate in three-dimensional space, and its potential energy $V$ is taken to be zero. The quantum mechanical description of this system provides the foundation for understanding [rotational spectroscopy](@entry_id:152769).

#### The Quantum Mechanical Hamiltonian

The [two-body problem](@entry_id:158716) of masses $m_1$ and $m_2$ can be reduced to an [equivalent one-body problem](@entry_id:173512) by separating the [center-of-mass motion](@entry_id:747201) from the [relative motion](@entry_id:169798). The [relative motion](@entry_id:169798) is described by a single particle of **reduced mass** $\mu = \frac{m_1 m_2}{m_1 + m_2}$ moving at a distance $r$ from the origin. The classical kinetic energy for this effective particle is $T = \frac{p^2}{2\mu}$. In quantum mechanics, we replace the classical momentum $p$ with the [momentum operator](@entry_id:151743) $\hat{p} = -i\hbar\nabla$, yielding the kinetic energy operator $\hat{T} = -\frac{\hbar^2}{2\mu}\nabla^2$, where $\nabla^2$ is the Laplacian operator.

For the [rigid rotor](@entry_id:156317), the radial distance is constrained to be a constant, $r=R$. This constraint eliminates any radial motion, meaning the wavefunction $\Psi$ depends only on the angular coordinates, $\theta$ and $\phi$. To formulate the Hamiltonian, we express the Laplacian operator in [spherical polar coordinates](@entry_id:274003):
$$
\nabla^2 = \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial}{\partial r}\right) + \frac{1}{r^2\sin\theta}\frac{\partial}{\partial\theta}\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{r^2\sin^2\theta}\frac{\partial^2}{\partial\phi^2}
$$
Since the wavefunction does not depend on $r$, any terms involving $\frac{\partial}{\partial r}$ will vanish when applied to $\Psi(\theta, \phi)$. We can therefore discard the radial part of the Laplacian and set $r=R$ in the remaining angular part. With $V=0$, the Hamiltonian operator $\hat{H}$ is purely kinetic, and the time-independent Schrödinger equation, $\hat{H}\Psi = E\Psi$, becomes [@problem_id:2961169]:
$$
-\frac{\hbar^2}{2\mu R^2}\left[ \frac{1}{\sin\theta}\frac{\partial}{\partial\theta}\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\phi^2} \right] \Psi(\theta, \phi) = E\Psi(\theta, \phi)
$$
The quantity $I = \mu R^2$ is the **moment of inertia** of the molecule. The operator within the brackets is the angular part of the Laplacian, often denoted $\nabla_\Omega^2$. This operator is fundamentally related to the square of the orbital [angular momentum operator](@entry_id:155961), $\hat{L}^2$, by the identity $\hat{L}^2 = -\hbar^2 \nabla_\Omega^2$. This allows us to write the Hamiltonian in a more compact and physically insightful form:
$$
\hat{H} = \frac{\hat{L}^2}{2I}
$$
The Schrödinger equation is thus an eigenvalue equation for the squared [angular momentum operator](@entry_id:155961): $\frac{\hat{L}^2}{2I}\Psi(\theta, \phi) = E\Psi(\theta, \phi)$.

#### Eigenstates and Energy Levels

The solutions to the angular momentum eigenvalue equation are a well-known family of special functions called the **[spherical harmonics](@entry_id:156424)**, denoted $Y_{\ell}^{m}(\theta, \phi)$ [@problem_id:2038351]. These functions are the simultaneous eigenfunctions of both the squared [angular momentum operator](@entry_id:155961) $\hat{L}^2$ and its projection onto a chosen axis, conventionally the $z$-axis, $\hat{L}_z$. Their eigenvalues are given by:
$$
\hat{L}^2 Y_{\ell}^{m}(\theta, \phi) = \hbar^2 \ell(\ell+1) Y_{\ell}^{m}(\theta, \phi)
$$
$$
\hat{L}_z Y_{\ell}^{m}(\theta, \phi) = \hbar m Y_{\ell}^{m}(\theta, \phi)
$$
Here, $\ell$ is the **[orbital angular momentum quantum number](@entry_id:167573)** (or rotational [quantum number](@entry_id:148529), often denoted $J$ in [molecular spectroscopy](@entry_id:148164)), and $m$ is the **magnetic quantum number**.

By substituting the eigenvalue of $\hat{L}^2$ into the Schrödinger equation, we obtain the [quantized energy levels](@entry_id:140911) for the [rigid rotor](@entry_id:156317):
$$
E_\ell = \frac{\hbar^2}{2I}\ell(\ell+1)
$$
The [quantum number](@entry_id:148529) $\ell$ can take any non-negative integer value, $\ell = 0, 1, 2, \dots$. For each value of $\ell$, the [magnetic quantum number](@entry_id:145584) $m$ can take on $2\ell+1$ integer values from $-\ell$ to $+\ell$.

#### The Origin of Quantization Rules

The integer nature of the quantum numbers $\ell$ and $m$ is not an ad hoc assumption but a direct consequence of the fundamental physical requirement that the wavefunction $\psi(\theta, \phi)$ be a single-valued, continuous, and finite function over the entire surface of the sphere. This can be understood by considering the solution via separation of variables, where we write $\psi(\theta, \phi) = \Theta(\theta)\Phi(\phi)$ [@problem_id:2912465].

1.  **Quantization of $m$**: The equation for the azimuthal part, $\Phi(\phi)$, is $\frac{d^2\Phi}{d\phi^2} = -m^2\Phi$. The general solution is $\Phi(\phi) \propto \exp(im\phi)$. Because the points $(\theta, \phi)$ and $(\theta, \phi+2\pi)$ are physically identical, the wavefunction must be single-valued, meaning $\Phi(\phi) = \Phi(\phi+2\pi)$. This [periodic boundary condition](@entry_id:271298) implies $\exp(im2\pi) = 1$, which is only satisfied if $m$ is an integer ($m \in \mathbb{Z}$).

2.  **Quantization of $\ell$**: The equation for the polar part, $\Theta(\theta)$, is the associated Legendre differential equation. For the total wavefunction to be well-behaved, the solution $\Theta(\theta)$ must remain finite at the poles of the sphere, i.e., at $\theta=0$ and $\theta=\pi$. This boundary condition is only met if $\ell$ is a non-negative integer and if its value is greater than or equal to the absolute value of $m$, i.e., $\ell \ge |m|$. Solutions where $\ell$ is not an integer or where $|m| > \ell$ diverge at one or both poles and are therefore physically unacceptable.

From a more advanced group-theoretic perspective, the space of square-integrable scalar functions on the sphere, $L^2(S^2)$, carries a unitary representation of the [rotation group](@entry_id:204412) $\mathrm{SO}(3)$. The decomposition of this representation into its [irreducible components](@entry_id:153033) yields only those with integer total angular momentum labels $\ell$. Half-integer representations, which correspond to spin, are representations of the double-cover group $\mathrm{SU}(2)$ and do not describe single-valued scalar functions on the sphere [@problem_id:2912465].

#### The Nature of the Ground State

The lowest possible energy state, or **ground state**, corresponds to the smallest value of $\ell$, which is $\ell=0$. Substituting into the energy formula gives:
$$
E_0 = \frac{\hbar^2}{2I}(0)(0+1) = 0
$$
This result is profound because it contrasts sharply with other canonical quantum systems, such as the [particle in a box](@entry_id:140940) or the [quantum harmonic oscillator](@entry_id:140678), which both possess a non-zero **zero-point energy**. The reason for this difference lies in the **Heisenberg Uncertainty Principle (HUP)** [@problem_id:2018789] [@problem_id:2018783].

For a particle in a box, the position $x$ and linear momentum $p_x$ are [conjugate variables](@entry_id:147843), with the uncertainty relation $\Delta x \Delta p_x \ge \hbar/2$. If the energy were zero, the momentum would be precisely zero ($\Delta p_x = 0$), implying an infinite uncertainty in position ($\Delta x \to \infty$). This contradicts the fact that the particle is confined to a finite box. Thus, the particle must have a non-zero ground state momentum and energy.

For the [rigid rotor](@entry_id:156317), the analogous [conjugate variables](@entry_id:147843) are the [angular position](@entry_id:174053) $\phi$ and the angular momentum component $L_z$, with the relation $\Delta \phi \Delta L_z \ge \hbar/2$. In the $\ell=0$ ground state, the [total angular momentum](@entry_id:155748) is exactly zero. Consequently, all its components are zero, so $L_z = 0$ and the uncertainty $\Delta L_z = 0$. The HUP then requires that the uncertainty in [angular position](@entry_id:174053), $\Delta \phi$, be infinite. For a freely rotating molecule, this is physically permissible: it simply means that the orientation of the molecule in space is completely random and unknowable. All orientations are equally probable. Since this complete [delocalization](@entry_id:183327) of [angular position](@entry_id:174053) does not violate any physical constraint of the system, a ground state with precisely zero angular momentum and zero kinetic energy is allowed.

### Symmetry, Observables, and Degeneracy

The structure of the rigid rotor eigenstates is deeply connected to the symmetries of the system. This connection is formalized through the language of [commuting operators](@entry_id:149529).

#### Complete Sets of Commuting Observables (CSCO)

A set of [observables](@entry_id:267133) is a **Complete Set of Commuting Observables (CSCO)** if the operators corresponding to them all commute with one another, and their simultaneous eigenvalues are sufficient to uniquely specify the quantum state (up to an overall phase).

For the free [rigid rotor](@entry_id:156317), the Hamiltonian is $\hat{H} = \hat{L}^2 / (2I)$. Let's consider the set of operators $\{\hat{H}, \hat{L}^2, \hat{L}_z\}$.
1.  $[\hat{H}, \hat{L}^2] = [\frac{\hat{L}^2}{2I}, \hat{L}^2] = 0$, since any operator commutes with a function of itself.
2.  It is a fundamental result of [angular momentum algebra](@entry_id:178952) that $[\hat{L}^2, \hat{L}_z] = 0$.
3.  From the first two results, it follows that $[\hat{H}, \hat{L}_z] = [\frac{\hat{L}^2}{2I}, \hat{L}_z] = \frac{1}{2I}[\hat{L}^2, \hat{L}_z] = 0$.

All three operators commute. The simultaneous eigenfunctions are the spherical harmonics $\lvert\ell, m\rangle$, and the pair of [quantum numbers](@entry_id:145558) $(\ell, m)$ uniquely specifies the state. Therefore, $\{\hat{H}, \hat{L}^2, \hat{L}_z\}$ constitutes a CSCO for the [rigid rotor](@entry_id:156317) [@problem_id:2880020]. Note that the set is technically redundant, as the eigenvalue of $\hat{H}$ is determined by $\ell$, but it satisfies the definition. In contrast, the set $\{\hat{H}, \hat{L}^2\}$ is *not* a CSCO, because for any $\ell > 0$, there are $2\ell+1$ distinct states (corresponding to different values of $m$) that share the same eigenvalues of $\hat{H}$ and $\hat{L}^2$. This degeneracy means the eigenvalues do not uniquely label the state.

#### Rotational Symmetry and Degeneracy

The energy of a rigid rotor state, $E_\ell$, depends only on the [quantum number](@entry_id:148529) $\ell$, not on $m$. This means that for any given $\ell > 0$, all $2\ell+1$ states corresponding to $m = -\ell, -\ell+1, \dots, \ell$ have the same energy. This is a **degeneracy** that arises from the symmetry of the system. The Hamiltonian $\hat{H}=\hat{L}^2/(2I)$ is spherically symmetric; it is invariant under any rotation in three-dimensional space. This $\mathrm{SO}(3)$ symmetry is expressed by the fact that the Hamiltonian commutes with all three components of the [angular momentum operator](@entry_id:155961): $[\hat{H}, \hat{L}_i] = 0$ for $i=x, y, z$.

Because there is no preferred direction in space for a free rotor, the choice of the $z$-axis for quantization is purely a convention. We could have chosen any other axis, defined by a [unit vector](@entry_id:150575) $\hat{\boldsymbol n}$, and used the operator $\hat{\boldsymbol n}\cdot\hat{\boldsymbol L}$ to resolve the degeneracy. The set $\{\hat{H}, \hat{L}^2, \hat{\boldsymbol n}\cdot\hat{\boldsymbol L}\}$ would form an equally valid CSCO [@problem_id:2880020]. It is crucial, however, not to confuse the commutation of $\hat{H}$ with all $\hat{L}_i$ with the commutation relations among the components themselves. The components of angular momentum famously do *not* commute with each other, e.g., $[\hat{L}_x, \hat{L}_y] = i\hbar \hat{L}_z$, which means that we can only know the value of one component at a time with arbitrary precision.

#### Symmetry Breaking by External Fields

The degeneracy associated with spherical symmetry can be lifted by applying an external field that introduces a preferred direction in space. For example, consider a molecule with a [permanent electric dipole moment](@entry_id:178322) $\mu$ placed in a weak, uniform electric field $\vec{E}$ directed along the $z$-axis. The interaction potential adds a term to the Hamiltonian: $\hat{V} = -\vec{\mu} \cdot \vec{E} = -\mu E \cos\theta$. The new Hamiltonian is $\hat{H}' = \frac{\hat{L}^2}{2I} - \mu E \cos\theta$.

We now re-examine the commutation relations [@problem_id:2880020]:
*   **Commutator with $\hat{L}_z$**: The operator $\hat{L}_z = -i\hbar\frac{\partial}{\partial\phi}$ commutes with any function that, like $\cos\theta$, is independent of $\phi$. Therefore, $[\hat{V}, \hat{L}_z]=0$, and since $[\hat{L}^2, \hat{L}_z]=0$, we have $[\hat{H}', \hat{L}_z]=0$. The system still possesses rotational symmetry about the $z$-axis, and $m$ remains a [good quantum number](@entry_id:263156).
*   **Commutator with $\hat{L}^2$**: The potential term $\cos\theta$ does *not* commute with $\hat{L}^2$. An operator that mixes states of different $\ell$ cannot commute with $\hat{L}^2$. The perturbation $\hat{V}$ has non-zero [matrix elements](@entry_id:186505) between states $\lvert\ell, m\rangle$ and $\lvert\ell \pm 1, m\rangle$. Consequently, $[\hat{V}, \hat{L}^2] \neq 0$, and thus $[\hat{H}', \hat{L}^2] \neq 0$.

The external field breaks the full [spherical symmetry](@entry_id:272852). As a result, $\ell$ is no longer a "good" [quantum number](@entry_id:148529) (the eigenstates of $\hat{H}'$ are mixtures of different $\ell$ states), and the energy levels, which now depend on both the original $\ell$ value and $m$, are no longer $(2\ell+1)$-fold degenerate. The field lifts the degeneracy in $m$. This phenomenon is known as the **Stark effect**.

### The Two-Dimensional Rigid Rotor: The Planar Model

A simpler but instructive model is the **planar [rigid rotor](@entry_id:156317)**, which describes a particle of moment of inertia $I$ constrained to move on a circle ($S^1$). This model is useful for describing internal rotations in molecules or as a simplified system for studying quantum principles.

#### The Hamiltonian and Eigenstates

The motion is described by a single angle $\phi$. The only relevant component of angular momentum is the one perpendicular to the plane of rotation, $\hat{L}_z$. The Hamiltonian is simply [@problem_id:2821487]:
$$
\hat{H}_0 = \frac{\hat{L}_z^2}{2I} = -\frac{\hbar^2}{2I}\frac{d^2}{d\phi^2}
$$
The eigenstates must satisfy the same [periodic boundary condition](@entry_id:271298) as in the 3D case: $\Psi(\phi) = \Psi(\phi+2\pi)$. This immediately leads to normalized [eigenfunctions](@entry_id:154705) of the form:
$$
\Psi_m(\phi) = \frac{1}{\sqrt{2\pi}}\exp(im\phi), \quad m \in \mathbb{Z}
$$
The corresponding [energy eigenvalues](@entry_id:144381) are:
$$
E_m = \frac{\hbar^2 m^2}{2I}
$$

#### Degeneracy in the Planar Rotor

The energy depends on $m^2$. This means that for any non-zero integer $m$, the states $\Psi_m$ and $\Psi_{-m}$ have the same energy. This two-fold degeneracy is a consequence of **[time-reversal symmetry](@entry_id:138094)**. The state $\exp(im\phi)$ corresponds to rotation in one direction, while $\exp(-im\phi)$ corresponds to rotation in the opposite direction; in the absence of external fields that could distinguish these directions, they must have the same energy [@problem_id:2912427].

#### Perturbation of the Planar Rotor

The planar rotor is an excellent system for applying perturbation theory. Consider a hindering potential that breaks the continuous rotational symmetry. For example, a weak electric field in the plane introduces a potential $V(\phi) = -\mu E \cos\phi$. We can calculate the correction to the non-degenerate ground state ($m=0$, $E_0^{(0)}=0$) using [second-order perturbation theory](@entry_id:192858) [@problem_id:2821487]:
$$
E_0^{(2)} = \sum_{m\neq 0} \frac{|\langle m | \hat{V} | 0 \rangle|^2}{E_0^{(0)} - E_m^{(0)}}
$$
The matrix elements of the perturbation are $\langle m | -\mu E \cos\phi | 0 \rangle$. Using $\cos\phi = \frac{1}{2}(\exp(i\phi) + \exp(-i\phi))$, we find that the only non-zero [matrix elements](@entry_id:186505) are for $m=\pm 1$, where $\langle \pm 1 | \hat{V} | 0 \rangle = -\frac{\mu E}{2}$. The energy denominator is $E_0^{(0)} - E_{\pm 1}^{(0)} = 0 - \frac{\hbar^2}{2I}$. The [second-order energy correction](@entry_id:136486) is then:
$$
E_0^{(2)} = \frac{|\langle 1 | \hat{V} | 0 \rangle|^2}{E_0^{(0)} - E_1^{(0)}} + \frac{|\langle -1 | \hat{V} | 0 \rangle|^2}{E_0^{(0)} - E_{-1}^{(0)}} = 2 \times \frac{(-\mu E/2)^2}{-\hbar^2/(2I)} = -\frac{I\mu^2E^2}{\hbar^2}
$$
This result, the quadratic Stark effect for the planar rotor, shows that the ground state energy is lowered by the perturbation.

This can be generalized to any hindering potential that can be expressed as a Fourier series, $\hat{V}(\phi) = \sum_{n=1}^{\infty} V_n \cos(n\phi)$. Following a similar procedure, the [second-order correction](@entry_id:155751) to the ground state energy is found to be [@problem_id:2821486]:
$$
E_0^{(2)} = -\frac{I}{\hbar^2} \sum_{n=1}^{\infty} \frac{V_n^2}{n^2}
$$
In the presence of such potentials, which are not uniform in $\phi$, the Hamiltonian no longer commutes with $\hat{L}_z$, and $m$ ceases to be a [good quantum number](@entry_id:263156) [@problem_id:2912427]. The perturbation mixes states with different $m$ values, and the degeneracies are generally lifted.

#### Relating the 2D and 3D Models

There is a direct mathematical connection between the 2D and 3D rotor models. The eigenfunctions of the 3D rotor, $Y_{\ell m}(\theta, \phi) \propto P_\ell^m(\cos\theta)\exp(im\phi)$, when evaluated at the equator ($\theta = \pi/2$), have the same azimuthal dependence, $\exp(im\phi)$, as the 2D rotor [eigenfunctions](@entry_id:154705). However, not all 3D eigenfunctions are non-zero at the equator. The associated Legendre functions $P_\ell^m(x)$ evaluated at $x=0$ are non-zero only if the sum $\ell+|m|$ is an even integer. If $\ell+|m|$ is odd, $P_\ell^m(0)=0$. This means that for a fixed $m$, the [spherical harmonics](@entry_id:156424) $Y_{\ell m}(\pi/2, \phi)$ vanish for alternating values of $\ell$ (starting from $\ell=|m|$) [@problem_id:2912427]. This [parity selection rule](@entry_id:155458) highlights a fundamental difference in the allowed states, and it is incorrect to simply identify a 2D rotor state with a specific 3D state; their Hamiltonians ($\hat{L}_z^2/2I$ vs. $\hat{L}^2/2I$) and energy spectra are fundamentally different.

### Extension to General Rigid Bodies: Molecular Tops

While the diatomic rigid rotor is a powerful model, most molecules are not linear. The rotational motion of a general, non-linear rigid body is described by its rotation about three orthogonal **principal axes** ($a, b, c$). The [rotational dynamics](@entry_id:267911) depend on the three corresponding **[principal moments of inertia](@entry_id:150889)**, $I_a, I_b, I_c$.

#### The Rotational Hamiltonian for Asymmetric Tops

The classical [rotational kinetic energy](@entry_id:177668) of a rigid body is $E_{rot} = \frac{J_a^2}{2I_a} + \frac{J_b^2}{2I_b} + \frac{J_c^2}{2I_c}$, where $J_a, J_b, J_c$ are the components of the angular momentum along the principal axes. The quantum mechanical Hamiltonian is obtained by replacing the classical quantities with their operator analogues:
$$
\hat{H}_{rot} = \frac{\hat{J}_a^2}{2I_a} + \frac{\hat{J}_b^2}{2I_b} + \frac{\hat{J}_c^2}{2I_c}
$$
Here, $\hat{J}_a, \hat{J}_b, \hat{J}_c$ are the operators for the components of angular momentum in the molecule's body-fixed frame.

#### Rotational Constants and Classification of Tops

In [molecular spectroscopy](@entry_id:148164), it is conventional to rewrite the Hamiltonian in terms of **[rotational constants](@entry_id:191788)**. By convention, the principal axes are labeled such that $I_a \le I_b \le I_c$. The [rotational constants](@entry_id:191788) $A, B, C$ are defined in inverse proportion to these [moments of inertia](@entry_id:174259) [@problem_id:2912437].

In energy units (e.g., Joules), they are defined as:
$$
A = \frac{\hbar^2}{2I_a}, \quad B = \frac{\hbar^2}{2I_b}, \quad C = \frac{\hbar^2}{2I_c}
$$
From the axis convention $I_a \le I_b \le I_c$, it follows that $A \ge B \ge C$.

In spectroscopy, these are more often expressed in frequency units (Hz, by dividing by $h$) or [wavenumber](@entry_id:172452) units ($\mathrm{cm}^{-1}$, by dividing by $hc$). In [wavenumber](@entry_id:172452) units, the definitions become:
$$
A = \frac{h}{8\pi^2 c I_a}, \quad B = \frac{h}{8\pi^2 c I_b}, \quad C = \frac{h}{8\pi^2 c I_c}
$$
The classification of molecular rotors ("tops") is based on the relationships between the moments of inertia [@problem_id:2912437]:

*   **Spherical Top**: All three moments of inertia are equal: $I_a = I_b = I_c$. This implies $A=B=C$. Examples include methane ($\text{CH}_4$) and sulfur hexafluoride ($\text{SF}_6$). Their energy levels follow the same simple formula as the linear rotor.
*   **Symmetric Top**: Two of the three moments of inertia are equal.
    *   **Prolate Symmetric Top**: The molecule is elongated, like a cigar (e.g., methyl chloride, $\text{CH}_3\text{Cl}$). The moment of inertia about the unique axis is the smallest. According to the convention, this means $I_a  I_b = I_c$. The corresponding [rotational constants](@entry_id:191788) are $A > B = C$.
    *   **Oblate Symmetric Top**: The molecule is flattened, like a disc (e.g., benzene, $\text{C}_6\text{H}_6$). The moment of inertia about the unique axis is the largest. According to the convention, this means $I_a = I_b  I_c$. The corresponding [rotational constants](@entry_id:191788) are $A = B > C$.
*   **Asymmetric Top**: All three moments of inertia are different: $I_a  I_b  I_c$. This implies $A > B > C$. Most molecules (e.g., water, $\text{H}_2\text{O}$) fall into this category, and their [rotational spectra](@entry_id:163636) are considerably more complex.

This classification is the starting point for analyzing the rich and detailed rotational [spectra of polyatomic molecules](@entry_id:182590).