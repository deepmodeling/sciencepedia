## Introduction
In quantum mechanics and many areas of physics, the central task is often to solve an [eigenvalue problem](@entry_id:143898), such as the time-independent Schrödinger equation. While exact solutions exist for idealized models like the hydrogen atom, real-world systems are typically too complex to be solved analytically. This creates a critical gap between our simple models and the intricate reality we wish to describe. Perturbation theory provides a powerful and systematic framework to bridge this gap. It allows us to calculate approximate solutions for a complex system by treating the difficult parts of its governing operator as a small "perturbation" to a simpler, solvable problem.

This article offers a comprehensive exploration of this essential method. In the first chapter, "Principles and Mechanisms," we will derive the fundamental formulas of Rayleigh-Schrödinger [perturbation theory](@entry_id:138766) for both non-degenerate and degenerate cases, and discuss the mathematical foundations that ensure its validity. The second chapter, "Applications and Interdisciplinary Connections," will showcase the theory's vast utility by examining its role in explaining phenomena across atomic physics, [condensed matter](@entry_id:747660), and beyond. Finally, "Hands-On Practices" provides an opportunity to apply these concepts to concrete problems, solidifying your understanding of this indispensable tool.

## Principles and Mechanisms

The time-independent Schrödinger equation, $H|\Psi\rangle = E|\Psi\rangle$, forms the bedrock of quantum mechanics, describing the [stationary states](@entry_id:137260) of a system. While this [eigenvalue equation](@entry_id:272921) is exactly solvable for a small number of idealized systems (e.g., the hydrogen atom, the quantum harmonic oscillator), the vast majority of physical and chemical systems of interest possess Hamiltonians of such complexity that exact solutions are unattainable. Perturbation theory provides a powerful and systematic method for obtaining approximate solutions by starting from a simpler, solvable problem and treating the difference as a small "perturbation." This chapter will develop the principles and mechanisms of Rayleigh-Schrödinger perturbation theory, which expresses the energies and eigenstates of the complex system as a power series in the strength of the perturbation.

### The General Framework of Perturbation Theory

The core strategy of perturbation theory is to partition the full Hamiltonian $H$ of the system into two parts: an unperturbed Hamiltonian $H_0$, for which the eigenvalue problem is known and solvable, and a perturbation $V$, which represents the difference between the true Hamiltonian and the simplified model.

$$ H = H_0 + V $$

We assume that the complete set of orthonormal [eigenfunctions](@entry_id:154705) $|\Psi_n^{(0)}\rangle$ and corresponding eigenvalues $E_n^{(0)}$ of the unperturbed Hamiltonian $H_0$ are known:

$$ H_0 |\Psi_n^{(0)}\rangle = E_n^{(0)} |\Psi_n^{(0)}\rangle $$

The set $\{|\Psi_n^{(0)}\rangle\}$ forms a complete basis for the Hilbert space of the system. Our goal is to find the eigenvalues $E$ and [eigenfunctions](@entry_id:154705) $|\Psi\rangle$ of the full Hamiltonian $H$.

To systematically track the effect of the perturbation, we introduce a fictitious, dimensionless parameter $\lambda \in [0, 1]$ and define a continuous family of Hamiltonians $H(\lambda)$:

$$ H(\lambda) = H_0 + \lambda V $$

This construction smoothly connects the unperturbed system ($\lambda=0$) to the full, physical system ($\lambda=1$). We now seek solutions to the [eigenvalue problem](@entry_id:143898) for $H(\lambda)$:

$$ (H_0 + \lambda V) |\Psi(\lambda)\rangle = E(\lambda) |\Psi(\lambda)\rangle $$

The fundamental assumption of Rayleigh-Schrödinger [perturbation theory](@entry_id:138766) is that the energy $E(\lambda)$ and [eigenfunction](@entry_id:149030) $|\Psi(\lambda)\rangle$ are **analytic functions** of $\lambda$ in a neighborhood of $\lambda=0$. This allows us to expand them as [power series](@entry_id:146836) in $\lambda$:

$$ E(\lambda) = E^{(0)} + \lambda E^{(1)} + \lambda^2 E^{(2)} + \dots = \sum_{k=0}^{\infty} \lambda^k E^{(k)} $$
$$ |\Psi(\lambda)\rangle = |\Psi^{(0)}\rangle + \lambda |\Psi^{(1)}\rangle + \lambda^2 |\Psi^{(2)}\rangle + \dots = \sum_{k=0}^{\infty} \lambda^k |\Psi^{(k)}\rangle $$

As $\lambda \to 0$, the perturbed solutions must smoothly reduce to the unperturbed ones. For a specific state, say the $n$-th state, this provides the crucial boundary condition: $E_n(0) = E_n^{(0)}$ and $|\Psi_n(0)\rangle = |\Psi_n^{(0)}\rangle$. This immediately identifies the zeroth-order terms in the series.

To fully specify the problem, we must impose a [normalization condition](@entry_id:156486) on $|\Psi(\lambda)\rangle$. While the physical requirement is $\langle\Psi(\lambda)|\Psi(\lambda)\rangle = 1$, this leads to algebraically complex equations. A more convenient and widely used convention is **[intermediate normalization](@entry_id:196388)** [@problem_id:2653593]. In this scheme, we demand that the projection of the perturbed state onto the unperturbed reference state remains unity for all $\lambda$:

$$ \langle\Psi_n^{(0)}|\Psi_n(\lambda)\rangle = 1 $$

Substituting the [series expansion](@entry_id:142878) for $|\Psi_n(\lambda)\rangle$ yields:
$$ \langle\Psi_n^{(0)}| (|\Psi_n^{(0)}\rangle + \lambda |\Psi_n^{(1)}\rangle + \lambda^2 |\Psi_n^{(2)}\rangle + \dots) = 1 $$
$$ \langle\Psi_n^{(0)}|\Psi_n^{(0)}\rangle + \lambda \langle\Psi_n^{(0)}|\Psi_n^{(1)}\rangle + \lambda^2 \langle\Psi_n^{(0)}|\Psi_n^{(2)}\rangle + \dots = 1 $$

Since $\langle\Psi_n^{(0)}|\Psi_n^{(0)}\rangle = 1$, for this equation to hold for all values of $\lambda$, the coefficient of each power of $\lambda$ must be zero. This provides a powerful constraint on the correction terms for the wavefunction:

$$ \langle\Psi_n^{(0)}|\Psi_n^{(k)}\rangle = 0 \quad \text{for all } k \ge 1 $$

This means that all higher-order corrections to the wavefunction are orthogonal to the zeroth-order state. This convention uniquely fixes the phase and amplitude of the wavefunction at each order, greatly simplifying the derivation of the correction formulas.

### Perturbation Theory for Non-Degenerate States

We first consider the simplest case where the eigenvalue $E_n^{(0)}$ of interest is **non-degenerate**, meaning it is unique in the spectrum of $H_0$. By substituting the power series for $E_n(\lambda)$ and $|\Psi_n(\lambda)\rangle$ into the Schrödinger equation and collecting terms with the same power of $\lambda$, we can derive expressions for the corrections $E_n^{(k)}$ and $|\Psi_n^{(k)}\rangle$.

#### First-Order Corrections

Equating the terms of order $\lambda^1$ yields the first-order equation:
$$ H_0 |\Psi_n^{(1)}\rangle + V |\Psi_n^{(0)}\rangle = E_n^{(0)} |\Psi_n^{(1)}\rangle + E_n^{(1)} |\Psi_n^{(0)}\rangle $$

To find the **[first-order energy correction](@entry_id:143593)**, $E_n^{(1)}$, we project this equation onto the unperturbed state $\langle\Psi_n^{(0)}|$:
$$ \langle\Psi_n^{(0)}|H_0|\Psi_n^{(1)}\rangle + \langle\Psi_n^{(0)}|V|\Psi_n^{(0)}\rangle = E_n^{(0)}\langle\Psi_n^{(0)}|\Psi_n^{(1)}\rangle + E_n^{(1)}\langle\Psi_n^{(0)}|\Psi_n^{(0)}\rangle $$

Since $H_0$ is Hermitian, $\langle\Psi_n^{(0)}|H_0 = E_n^{(0)}\langle\Psi_n^{(0)}|$. The first term on the left becomes $E_n^{(0)}\langle\Psi_n^{(0)}|\Psi_n^{(1)}\rangle$. From [intermediate normalization](@entry_id:196388), we know $\langle\Psi_n^{(0)}|\Psi_n^{(1)}\rangle=0$. Since $\langle\Psi_n^{(0)}|\Psi_n^{(0)}\rangle=1$, the equation simplifies dramatically to:

$$ E_n^{(1)} = \langle\Psi_n^{(0)}|V|\Psi_n^{(0)}\rangle $$

This elegant result states that the [first-order correction](@entry_id:155896) to the energy is simply the [expectation value](@entry_id:150961) of the perturbation calculated with respect to the unperturbed state. To first order, the total energy is $E_n \approx E_n^{(0)} + \langle\Psi_n^{(0)}|V|\Psi_n^{(0)}\rangle$.

A canonical example is the **[anharmonic oscillator](@entry_id:142760)**, described by the Hamiltonian $H = -\frac{d^2}{dx^2} + x^2 + \lambda x^4$ [@problem_id:740786]. The unperturbed part $H_0 = -\frac{d^2}{dx^2} + x^2$ is the [quantum harmonic oscillator](@entry_id:140678), and the perturbation is $V = x^4$. The unperturbed ground state energy is $E_0^{(0)}=1$ and its wavefunction is $\psi_0^{(0)}(x) = \pi^{-1/4} \exp(-x^2/2)$. The [first-order energy correction](@entry_id:143593) is:

$$ E_0^{(1)} = \langle\psi_0^{(0)}|x^4|\psi_0^{(0)}\rangle = \int_{-\infty}^{\infty} (\pi^{-1/4} e^{-x^2/2})^* x^4 (\pi^{-1/4} e^{-x^2/2}) dx = \frac{1}{\sqrt{\pi}} \int_{-\infty}^{\infty} x^4 e^{-x^2} dx $$

This standard Gaussian integral evaluates to $\frac{3\sqrt{\pi}}{4}$, yielding $E_0^{(1)} = \frac{3}{4}$. The [ground state energy](@entry_id:146823), correct to first order in $\lambda$, is thus $E_0(\lambda) \approx 1 + \frac{3}{4}\lambda$.

An important related result is the **Hellmann-Feynman theorem**. It states that if a Hamiltonian $H(a)$ depends on a parameter $a$, then the derivative of an eigenvalue with respect to that parameter is equal to the expectation value of the derivative of the Hamiltonian:
$$ \frac{dE_n(a)}{da} = \left\langle\Psi_n(a)\left|\frac{\partial H(a)}{\partial a}\right|\Psi_n(a)\right\rangle $$
If we consider a perturbation of the form $H = H_0 + \lambda V$, where $V = \frac{\partial H}{\partial \lambda}|_{\lambda=0}$, the theorem implies $\frac{dE_n}{d\lambda}|_{\lambda=0} = \langle\Psi_n^{(0)}|V|\Psi_n^{(0)}\rangle$, which is exactly the expression for $E_n^{(1)}$. This provides a powerful alternative method for calculating first-order energy shifts when the perturbation corresponds to a change in a parameter within the Hamiltonian itself [@problem_id:740815].

#### Second-Order Corrections

To find the **[first-order wavefunction correction](@entry_id:275651)**, $|\Psi_n^{(1)}\rangle$, we expand it in the complete basis of unperturbed states: $|\Psi_n^{(1)}\rangle = \sum_{m} c_m |\Psi_m^{(0)}\rangle$. The [intermediate normalization](@entry_id:196388) condition $\langle\Psi_n^{(0)}|\Psi_n^{(1)}\rangle=0$ implies that the coefficient $c_n=0$. Substituting this expansion into the first-order equation and projecting onto a different state $\langle\Psi_k^{(0)}|$ (with $k \ne n$) gives the coefficients:

$$ c_k = \frac{\langle\Psi_k^{(0)}|V|\Psi_n^{(0)}\rangle}{E_n^{(0)} - E_k^{(0)}} \quad (k \ne n) $$

Thus, the first-order correction to the wavefunction is:

$$ |\Psi_n^{(1)}\rangle = \sum_{m \ne n} \frac{\langle\Psi_m^{(0)}|V|\Psi_n^{(0)}\rangle}{E_n^{(0)} - E_m^{(0)}} |\Psi_m^{(0)}\rangle $$

This shows that the perturbation "mixes" the unperturbed state $|\Psi_n^{(0)}\rangle$ with other unperturbed states $|\Psi_m^{(0)}\rangle$. The extent of mixing is proportional to the [coupling matrix](@entry_id:191757) element $\langle\Psi_m^{(0)}|V|\Psi_n^{(0)}\rangle$ and inversely proportional to the energy difference between the states.

Using this result for $|\Psi_n^{(1)}\rangle$, one can proceed to the second-order equation and project onto $\langle\Psi_n^{(0)}|$ to find the **[second-order energy correction](@entry_id:136486)**, $E_n^{(2)}$:

$$ E_n^{(2)} = \sum_{m \ne n} \frac{|\langle\Psi_m^{(0)}|V|\Psi_n^{(0)}\rangle|^2}{E_n^{(0)} - E_m^{(0)}} $$

This expression is central to many applications of [perturbation theory](@entry_id:138766). It can be interpreted as the result of the system making "virtual" transitions from the initial state $|\Psi_n^{(0)}\rangle$ to all other states $|\Psi_m^{(0)}\rangle$ and back. The energy of the state $|\Psi_n^{(0)}\rangle$ is "pushed down" by states with higher energy ($E_m^{(0)} > E_n^{(0)}$) and "pushed up" by states with lower energy ($E_m^{(0)} < E_n^{(0)}$).

For example, consider a [harmonic oscillator](@entry_id:155622) perturbed by a linear term, $H = H_0 + \lambda x$ [@problem_id:740935]. Let's find the [second-order correction](@entry_id:155751) to the first excited state ($n=1$). The unperturbed energies are $E_m^{(0)} = 2m+1$ (in appropriate units). The perturbation is $V=x$. The [matrix elements](@entry_id:186505) of $x$ have a strict selection rule: $\langle m|x|n \rangle$ is non-zero only if $m=n\pm1$. For the first excited state ($n=1$), the only non-zero [matrix elements](@entry_id:186505) are $\langle0|x|1\rangle$ and $\langle2|x|1\rangle$. The [second-order energy correction](@entry_id:136486) is therefore:

$$ E_1^{(2)} = \frac{|\langle0|x|1\rangle|^2}{E_1^{(0)}-E_0^{(0)}} + \frac{|\langle2|x|1\rangle|^2}{E_1^{(0)}-E_2^{(0)}} = \frac{|\langle0|x|1\rangle|^2}{(3)-(1)} + \frac{|\langle2|x|1\rangle|^2}{(3)-(5)} $$
Using the standard results for the harmonic oscillator, $|\langle0|x|1\rangle|^2=1/2$ and $|\langle2|x|1\rangle|^2=1$, we find:
$$ E_1^{(2)} = \frac{1/2}{2} + \frac{1}{-2} = \frac{1}{4} - \frac{1}{2} = -\frac{1}{4} $$
The total energy of the first excited state to second order is $E_1(\lambda) \approx 3 - \frac{\lambda^2}{4}$ (since $E_1^{(1)}=\langle1|x|1\rangle=0$).

### Perturbation Theory for Degenerate States

The formulas for the second-order energy and first-order wavefunction corrections contain denominators of the form $E_n^{(0)} - E_m^{(0)}$. If the unperturbed energy level $E_n^{(0)}$ is **degenerate**, meaning there are other states $|\Psi_m^{(0)}\rangle$ with the exact same energy, then these denominators become zero and the non-degenerate theory breaks down. This mathematical divergence signals a physical reality: for a set of degenerate states, even an infinitesimal perturbation can cause a strong mixing between them, and the original unperturbed eigenstates may no longer be a good starting point.

The correct procedure, known as **[degenerate perturbation theory](@entry_id:143587)**, is to find the "correct" zeroth-order wavefunctions that are stable under the perturbation. These are specific [linear combinations](@entry_id:154743) of the original degenerate states. The method is as follows [@problem_id:2767591]:

1.  **Identify the Degenerate Subspace:** For a given unperturbed energy $E^{(0)}$ with a $g$-fold degeneracy, identify the set of $g$ orthonormal [eigenstates](@entry_id:149904) $\{|\psi_1^{(0)}\rangle, |\psi_2^{(0)}\rangle, \dots, |\psi_g^{(0)}\rangle\}$ that span the degenerate [eigenspace](@entry_id:150590).

2.  **Construct the Perturbation Matrix:** Form a $g \times g$ matrix, $W$, whose elements are the [matrix elements](@entry_id:186505) of the perturbation $V$ within the degenerate subspace:
    $$ W_{ij} = \langle\psi_i^{(0)}|V|\psi_j^{(0)}\rangle $$

3.  **Diagonalize the Perturbation Matrix:** Find the eigenvalues $E_k^{(1)}$ and corresponding eigenvectors of the matrix $W$. The eigenvalues $E_k^{(1)}$ (for $k=1, \dots, g$) are the first-order energy corrections. The degeneracy is lifted (or partially lifted) by the perturbation, and the degenerate level $E^{(0)}$ splits into a set of new levels $E^{(0)} + \lambda E_k^{(1)}$.

4.  **Find the Correct Zeroth-Order States:** The eigenvectors of $W$ provide the coefficients for the "correct" zeroth-order states $|\phi_k^{(0)}\rangle$, which are the linear combinations of the original basis states that diagonalize the perturbation: $|\phi_k^{(0)}\rangle = \sum_{j=1}^g c_{kj} |\psi_j^{(0)}\rangle$. These are the states that smoothly connect to the perturbed eigenstates as $\lambda \to 0$.

Consider a simple [three-level system](@entry_id:147049) with a degenerate unperturbed Hamiltonian [@problem_id:740813]:
$$ H_0 = \begin{pmatrix} 3  & 0  & 0 \\ 0  & 3  & 0 \\ 0  & 0  & 5 \end{pmatrix}, \quad V = \begin{pmatrix} 0  & \epsilon  & 0 \\ \epsilon  & 0  & \epsilon \\ 0  & \epsilon  & 0 \end{pmatrix} $$
The eigenvalue $E^{(0)}=3$ is doubly degenerate, spanned by $|\psi_1^{(0)}\rangle = (1,0,0)^T$ and $|\psi_2^{(0)}\rangle = (0,1,0)^T$. The perturbation matrix $W$ in this subspace is:
$$ W = \begin{pmatrix} \langle\psi_1^{(0)}|V|\psi_1^{(0)}\rangle  & \langle\psi_1^{(0)}|V|\psi_2^{(0)}\rangle \\ \langle\psi_2^{(0)}|V|\psi_1^{(0)}\rangle  & \langle\psi_2^{(0)}|V|\psi_2^{(0)}\rangle \end{pmatrix} = \begin{pmatrix} 0  & \epsilon \\ \epsilon  & 0 \end{pmatrix} $$
The eigenvalues of this matrix are found by solving the [secular equation](@entry_id:265849) $\det(W - E^{(1)}I) = 0$, which gives $(E^{(1)})^2 - \epsilon^2 = 0$. The eigenvalues are $E^{(1)} = \pm\epsilon$. Thus, the perturbation lifts the degeneracy, and the original level at $E=3$ splits into two levels with energies $3 + \lambda\epsilon$ and $3 - \lambda\epsilon$ to first order.

A more physical example is a particle in a three-dimensional cubic box of side length $L$, perturbed by a potential $H' = \lambda xyz$ [@problem_id:740860]. The first excited state is triply degenerate, corresponding to the quantum numbers $(n_x,n_y,n_z)$ being $(2,1,1)$, $(1,2,1)$, and $(1,1,2)$. We must construct the $3 \times 3$ matrix of $H'$ in this basis and find its eigenvalues, which will give the splitting of the energy level.

### Mathematical Foundations and Convergence

The formal power series we have derived are not always guaranteed to be useful approximations. Their validity rests on firm mathematical foundations related to the spectral properties of the operators $H_0$ and $V$.

#### Conditions for Validity

For the Rayleigh-Schrödinger [perturbation series](@entry_id:266790) to be well-behaved, certain conditions must be met [@problem_id:2933747] [@problem_id:2767591]. These are rigorously established by the Kato-Rellich theorem and related results in analytic perturbation theory.
1.  **Self-Adjointness:** The Hamiltonians $H_0$ and $H$ must be [self-adjoint operators](@entry_id:152188) on a dense domain in the Hilbert space. This ensures real [energy eigenvalues](@entry_id:144381) and [unitary time evolution](@entry_id:192535).
2.  **Spectral Isolation and Finite Multiplicity:** The unperturbed eigenvalue of interest, $E_n^{(0)}$, must be an **[isolated point](@entry_id:146695)** in the spectrum of $H_0$. This means there exists a **[spectral gap](@entry_id:144877)** $\Delta_n = \min_{m \ne n} |E_m^{(0)} - E_n^{(0)}| > 0$, separating it from all other eigenvalues. Furthermore, if the level is degenerate, its multiplicity must be finite.
3.  **Relative Boundedness of V:** The perturbation $V$ must be "small" relative to $H_0$ in a precise operator-theoretic sense. A [sufficient condition](@entry_id:276242) is that $V$ is **$H_0$-bounded** with a relative bound less than 1. This ensures that the total Hamiltonian $H(\lambda)$ remains self-adjoint and its spectrum is stable against the perturbation for sufficiently small $\lambda$.

Under these conditions, the eigenvalues and eigenprojections of $H(\lambda)$ are guaranteed to be analytic functions of $\lambda$ near $\lambda=0$.

#### The Role of the Spectral Gap

The [spectral gap](@entry_id:144877) $\Delta_n$ is not just a formal requirement; it quantitatively controls the magnitude of the perturbative corrections [@problem_id:2683544]. A "small" perturbation is one whose strength is small *relative* to the [energy level spacing](@entry_id:181168) of the unperturbed system.
Looking at the formulas for the corrections, we see that the denominators involve energy differences. The smallest possible denominator magnitude is precisely the [spectral gap](@entry_id:144877) $\Delta_n$. This allows us to place rigorous bounds on the size of the corrections. For a bounded perturbation $V$ with operator norm $\|V\|$:

- The norm of the [first-order correction](@entry_id:155896) to the state vector is bounded by:
$$ \|\Psi_n^{(1)}\| \le \frac{\|V\|}{\Delta_n} $$
- The magnitude of the [second-order energy correction](@entry_id:136486) is bounded by:
$$ |E_n^{(2)}| \le \frac{\|V\|^2}{\Delta_n} $$

These bounds show that the [perturbation series](@entry_id:266790) will converge rapidly if the perturbation strength (as measured by $\|V\|$) is small compared to the [spectral gap](@entry_id:144877) $\Delta_n$. Conversely, if energy levels are closely packed (small $\Delta_n$), the corrections can be large, and the [perturbation series](@entry_id:266790) may converge slowly or not at all. The dimensionless ratio $\|\lambda V\|/\Delta_n$ is the true parameter governing the convergence behavior.

#### Radius of Convergence

The [perturbation series](@entry_id:266790) for the energy, $E_n(\lambda) = \sum_k \lambda^k E_n^{(k)}$, is a [power series](@entry_id:146836) in the parameter $\lambda$. Standard complex analysis tells us that this series converges inside a disk in the complex $\lambda$-plane, $| \lambda | < R$, where $R$ is the **radius of convergence**. The radius is determined by the distance from the origin to the nearest singularity of the function $E_n(\lambda)$.

A remarkable result from [operator theory](@entry_id:139990) is that these singularities occur at values of $\lambda$ where the eigenvalues of $H(\lambda)$ become degenerate—that is, where two or more energy levels cross [@problem_id:740723]. These points of degeneracy are **[branch points](@entry_id:166575)** of the eigenvalues as multi-valued analytic functions of $\lambda$. Therefore, the [radius of convergence](@entry_id:143138) for the [perturbation series](@entry_id:266790) of a given level is the absolute value of the smallest $\lambda$ (real or complex) for which that level crosses another.

For matrix Hamiltonians, this can be calculated explicitly. The eigenvalues are the roots of the [characteristic polynomial](@entry_id:150909) $\det(H(\lambda) - E I) = 0$. Eigenvalue degeneracy occurs when this polynomial has a multiple root for $E$, which happens if and only if its [discriminant](@entry_id:152620) vanishes. By finding the values of $\lambda$ that make the discriminant zero, we can identify the [branch points](@entry_id:166575) and thus the [radius of convergence](@entry_id:143138). For example, for the Hamiltonian $H(\lambda) = \begin{pmatrix} 0 & \lambda & 0 \\ \lambda & 2 & \sqrt{3}\,\lambda \\ 0 & \sqrt{3}\,\lambda & 8 \end{pmatrix}$, solving for the values of $\lambda$ where the characteristic polynomial has a double root yields $\lambda = \pm i\sqrt{3}$ and $\lambda = \pm 2i$. The branch points closest to the origin are at $\pm i\sqrt{3}$, so the radius of convergence for the [perturbation series](@entry_id:266790) of any of its eigenvalues is $R = |\pm i\sqrt{3}| = \sqrt{3}$. This provides a precise limit on the applicability of the [series expansion](@entry_id:142878).