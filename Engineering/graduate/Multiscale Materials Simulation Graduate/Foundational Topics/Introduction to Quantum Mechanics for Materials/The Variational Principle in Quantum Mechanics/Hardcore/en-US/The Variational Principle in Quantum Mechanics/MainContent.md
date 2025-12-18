## Introduction
The time-independent Schrödinger equation governs the [stationary states](@entry_id:137260) of quantum systems, but its exact analytical solution is possible for only the simplest cases. For the vast majority of systems relevant to chemistry, materials science, and condensed matter physics—from complex molecules to [crystalline solids](@entry_id:140223)—the interacting many-body problem is analytically intractable. The variational principle provides a powerful and elegant way forward, reformulating the differential eigenvalue problem as a more approachable minimization problem. It establishes that the energy of any approximate [trial wavefunction](@entry_id:142892) is a guaranteed upper bound to the true [ground-state energy](@entry_id:263704), thereby providing a clear path to systematically improving approximations: lower energy is always better.

This article provides a comprehensive graduate-level exploration of the [variational principle](@entry_id:145218), bridging its formal theory with its practical application in modern computational science. It is structured to guide the reader from fundamental concepts to advanced implementations.

The first chapter, **Principles and Mechanisms**, delves into the mathematical heart of the principle. It covers the Rayleigh-Ritz theorem for the ground state, its generalization to excited states through the [min-max principle](@entry_id:150229), and its ultimate expression in the form of Density Functional Theory.

The second chapter, **Applications and Interdisciplinary Connections**, showcases how these principles are put into practice. It explores the variational foundation of essential approximation methods like Hartree-Fock and Variational Monte Carlo, its role in calculating the electronic band structure of solids, and its utility in determining macroscopic material properties.

Finally, the **Hands-On Practices** chapter provides a set of targeted problems designed to solidify understanding of key computational challenges, such as basis set [ill-conditioning](@entry_id:138674), [k-point sampling](@entry_id:177715), and [preconditioning](@entry_id:141204), that arise when applying the variational principle in real-world simulations.

## Principles and Mechanisms

The [variational principle](@entry_id:145218) is a cornerstone of quantum mechanics, providing not only a profound conceptual framework but also a powerful practical tool for approximating solutions to the time-independent Schrödinger equation. It transforms the problem of solving a complex differential equation into a problem of minimization, a task for which a vast arsenal of mathematical techniques has been developed. This chapter elucidates the fundamental principles and mechanisms underpinning [variational methods](@entry_id:163656), from the foundational theorem for the ground state to its generalization for excited states and its central role in modern electronic structure theories like Density Functional Theory.

### The Ground-State Variational Principle

The [variational method](@entry_id:140454) begins with a simple but remarkably powerful statement concerning the ground-state energy of a quantum system.

#### The Rayleigh-Ritz Variational Principle

Consider a quantum system described by a self-adjoint (Hermitian) Hamiltonian operator, $\hat{H}$, which is bounded from below. Let its exact ground-state energy be $E_0$. The **ground-state [variational principle](@entry_id:145218)** states that for any normalized [trial wavefunction](@entry_id:142892) $|\psi\rangle$ that lies within the domain of $\hat{H}$, the [expectation value](@entry_id:150961) of the energy is an upper bound to the true [ground-state energy](@entry_id:263704) $E_0$.

$$
E[\psi] = \langle\psi|\hat{H}|\psi\rangle \ge E_0
$$

Equality holds if and only if $|\psi\rangle$ is an eigenstate of $\hat{H}$ corresponding to the ground-state energy $E_0$. For a non-normalized trial state, the principle is expressed using the **Rayleigh quotient**, $R[\psi]$, which is invariant to the normalization of the state:

$$
R[\psi] = \frac{\langle\psi|\hat{H}|\psi\rangle}{\langle\psi|\psi\rangle} \ge E_0
$$

This principle is fundamental because it provides a clear-cut objective: to find the [best approximation](@entry_id:268380) to the ground-state energy, one must search for the [trial wavefunction](@entry_id:142892) that minimizes the Rayleigh quotient. The lower the energy expectation value, the "better" the [trial wavefunction](@entry_id:142892), in a variational sense.

#### Mathematical Foundation

The proof of the [variational principle](@entry_id:145218) is straightforward and illustrative. According to the [spectral theorem](@entry_id:136620), since $\hat{H}$ is self-adjoint, it possesses a complete set of orthonormal [eigenstates](@entry_id:149904), which we denote as $|\phi_n\rangle$, with corresponding real eigenvalues $E_n$. Let us order these such that $E_0 \le E_1 \le E_2 \le \dots$.

$$
\hat{H}|\phi_n\rangle = E_n|\phi_n\rangle \quad \text{and} \quad \langle\phi_n|\phi_m\rangle = \delta_{nm}
$$

Any arbitrary trial state $|\psi\rangle$ from the domain of $\hat{H}$ can be expanded in this complete basis:

$$
|\psi\rangle = \sum_n c_n |\phi_n\rangle, \quad \text{where } c_n = \langle\phi_n|\psi\rangle
$$

Now, we evaluate the numerator and denominator of the Rayleigh quotient . The numerator is the energy expectation value:

$$
\langle\psi|\hat{H}|\psi\rangle = \left\langle \sum_m c_m \phi_m \right| \hat{H} \left| \sum_n c_n \phi_n \right\rangle = \sum_{m,n} c_m^* c_n \langle\phi_m|\hat{H}|\phi_n\rangle = \sum_{m,n} c_m^* c_n E_n \delta_{mn} = \sum_n |c_n|^2 E_n
$$

The denominator is the squared norm of the state:

$$
\langle\psi|\psi\rangle = \sum_{m,n} c_m^* c_n \langle\phi_m|\phi_n\rangle = \sum_{m,n} c_m^* c_n \delta_{mn} = \sum_n |c_n|^2
$$

The Rayleigh quotient is therefore a weighted average of the [energy eigenvalues](@entry_id:144381), where the weights $|c_n|^2$ represent the probability of measuring the energy $E_n$ in the state $|\psi\rangle$:

$$
R[\psi] = \frac{\sum_n |c_n|^2 E_n}{\sum_n |c_n|^2}
$$

Since $E_0$ is the lowest eigenvalue, $E_n \ge E_0$ for all $n$. We can thus establish a lower bound for the numerator:

$$
\sum_n |c_n|^2 E_n \ge \sum_n |c_n|^2 E_0 = E_0 \left( \sum_n |c_n|^2 \right)
$$

Dividing by the (positive) denominator $\sum_n |c_n|^2$ yields the [variational principle](@entry_id:145218): $R[\psi] \ge E_0$. Equality holds if and only if the expansion of $|\psi\rangle$ only contains terms for which $E_n = E_0$. This means $|\psi\rangle$ must be a [linear combination](@entry_id:155091) of the ground-state [eigenfunctions](@entry_id:154705)—that is, it must lie within the ground-state [eigenspace](@entry_id:150590).

#### Admissible Trial Wavefunctions

The power of the [variational principle](@entry_id:145218) lies in its application, but its validity rests on choosing **admissible trial wavefunctions**. A function is not admissible simply because it can be written down; it must satisfy fundamental physical and mathematical requirements . The search for the minimum energy is constrained to a specific subset of the Hilbert space.

1.  **Domain of the Hamiltonian**: The [trial wavefunction](@entry_id:142892) $\Psi$ must belong to the domain of the Hamiltonian. For a typical Hamiltonian of the form $\hat{H} = \hat{T} + \hat{V}$, this means the [expectation values](@entry_id:153208) of both kinetic and potential energy must be finite. A finite kinetic energy expectation, $\langle\Psi|\hat{T}|\Psi\rangle  \infty$, implies that the wavefunction must be sufficiently smooth (specifically, its first derivatives must be square-integrable). A discontinuous wavefunction, for instance, would have an infinite kinetic energy and is therefore not an admissible state.

2.  **Fermionic Antisymmetry**: For systems of identical fermions, such as electrons, the Pauli exclusion principle dictates that the total [many-body wavefunction](@entry_id:203043) $\Psi(\mathbf{x}_1, \dots, \mathbf{x}_N)$, where $\mathbf{x}_i = (\mathbf{r}_i, s_i)$ represents the combined space and spin coordinates of the $i$-th electron, must be **antisymmetric** with respect to the exchange of any two particles:
    $$
    \Psi(\dots, \mathbf{x}_i, \dots, \mathbf{x}_j, \dots) = - \Psi(\dots, \mathbf{x}_j, \dots, \mathbf{x}_i, \dots)
    $$
    A variational calculation for a fermionic ground state must be restricted to the subspace of antisymmetric functions. Minimizing the Rayleigh quotient over all functions, without this constraint, would yield the (unphysical) bosonic ground state. This [antisymmetry](@entry_id:261893) requirement is responsible for the **[nodal structure](@entry_id:151019)** of the wavefunction—the $(3N-1)$-dimensional surface in configuration space where $\Psi=0$. The topology of these nodes is a critical determinant of the kinetic energy.

3.  **Symmetry Constraints**: If the Hamiltonian possesses certain symmetries (e.g., translational, rotational, or spin symmetries), its [eigenfunctions](@entry_id:154705) can be classified according to the [irreducible representations](@entry_id:138184) of the corresponding symmetry group. To find the ground state within a specific symmetry sector (e.g., a state with a given [total spin](@entry_id:153335) $S$ or, in a crystal, a total [crystal momentum](@entry_id:136369) $\mathbf{k}$), the variational search must be restricted to trial wavefunctions that transform according to that [irreducible representation](@entry_id:142733). For a periodic solid, this means the [trial wavefunction](@entry_id:142892) must satisfy the many-body generalization of Bloch's theorem.

### Practical Implementation: The Rayleigh-Ritz Method

The [variational principle](@entry_id:145218) provides a target for approximation, but the full Hilbert space is infinite-dimensional. The **Rayleigh-Ritz method** makes the problem tractable by restricting the variational search to a finite-dimensional subspace $\mathcal{S}$ spanned by a set of pre-defined basis functions, $\{\phi_i\}_{i=1}^N$.

#### From Infinite to Finite Dimensions

A [trial wavefunction](@entry_id:142892) $|\psi\rangle$ within the subspace $\mathcal{S}$ is written as a [linear combination](@entry_id:155091) of the basis functions:

$$
|\psi\rangle = \sum_{i=1}^N c_i |\phi_i\rangle
$$

The variational parameters are now the coefficients $\{c_i\}$. The problem reduces to finding the set of coefficients that minimizes the Rayleigh quotient. This transforms the infinite-dimensional [functional minimization](@entry_id:184561) problem into a finite-dimensional algebraic problem.

#### The Generalized Eigenvalue Problem

In many practical applications, such as quantum chemistry (using atomic orbitals) or real-space methods like finite elements, the chosen basis functions $\{\phi_i\}$ are not orthonormal. This non-orthogonality must be properly handled . Let's substitute the [basis expansion](@entry_id:746689) into the Rayleigh quotient:

$$
R[\mathbf{c}] = \frac{\langle \sum_i c_i \phi_i | \hat{H} | \sum_j c_j \phi_j \rangle}{\langle \sum_i c_i \phi_i | \sum_j c_j \phi_j \rangle} = \frac{\sum_{i,j} c_i^* c_j \langle\phi_i|\hat{H}|\phi_j\rangle}{\sum_{i,j} c_i^* c_j \langle\phi_i|\phi_j\rangle}
$$

We define two matrices: the **Hamiltonian matrix** $H$ and the **[overlap matrix](@entry_id:268881)** $S$. Their elements are given by:

$$
H_{ij} = \langle\phi_i|\hat{H}|\phi_j\rangle
$$
$$
S_{ij} = \langle\phi_i|\phi_j\rangle
$$

Since $\hat{H}$ is Hermitian, the matrix $H$ is also Hermitian ($H_{ij} = H_{ji}^*$). Similarly, $S$ is a Hermitian matrix. If the basis functions are [linearly independent](@entry_id:148207), $S$ is also positive-definite. In matrix-vector notation, with $\mathbf{c}$ being the column vector of coefficients, the Rayleigh quotient becomes:

$$
E[\mathbf{c}] = \frac{\mathbf{c}^\dagger H \mathbf{c}}{\mathbf{c}^\dagger S \mathbf{c}}
$$

To find the coefficients that minimize this expression, we set the partial derivative with respect to each $c_k^*$ to zero, which leads to a system of linear equations. This system is elegantly expressed as the **[generalized eigenvalue problem](@entry_id:151614)**:

$$
H \mathbf{c} = E S \mathbf{c}
$$

Solving this equation yields a set of eigenvalues $\{E^{(m)}\}$ and corresponding eigenvectors $\{\mathbf{c}^{(m)}\}$. The lowest eigenvalue is the Rayleigh-Ritz approximation to the [ground-state energy](@entry_id:263704), and its corresponding eigenvector gives the coefficients for the approximate ground-state wavefunction.

#### Convergence and Basis Set Completeness

The accuracy of the Rayleigh-Ritz method depends entirely on the choice of the subspace $\mathcal{S}$. A key question is whether the approximation can be made arbitrarily accurate. The answer lies in the concept of **basis set completeness** .

A set of basis functions $\{\phi_j\}_{j=1}^\infty$ is said to be **complete** in the Hilbert space $\mathcal{H}$ if any function $|\psi\rangle \in \mathcal{H}$ can be approximated with arbitrary precision by a finite [linear combination](@entry_id:155091) of the basis functions. More formally, the linear span of the basis set is dense in $\mathcal{H}$.

In computational practice, one uses **systematic basis hierarchies**. These are sequences of nested, finite-dimensional subspaces, $\mathcal{S}_1 \subset \mathcal{S}_2 \subset \dots \subset \mathcal{S}_n \subset \dots$, whose union is dense in the Hilbert space. As the subspace is enlarged, the variational flexibility increases. Since the search space at step $n+1$ contains the search space at step $n$, the minimized energy can only decrease or stay the same: $E_{n+1} \le E_n$. This guarantees **monotonic convergence** of the energy from above. If the basis is complete, this sequence of approximate energies is guaranteed to converge to the exact [ground-state energy](@entry_id:263704) in the limit of an infinitely large basis.

Examples of such hierarchies include:
-   **Plane waves**: Used for periodic systems, parameterized by a [kinetic energy cutoff](@entry_id:186065) $E_{\text{cut}}$. Increasing $E_{\text{cut}}$ systematically adds more basis functions, forming a nested sequence that is complete for [periodic functions](@entry_id:139337).
-   **Gaussian-type orbitals (GTOs)**: Used in quantum chemistry, organized in hierarchies (e.g., correlation-consistent sets cc-pVDZ, cc-pVTZ, etc.) that systematically add functions to better describe electron correlation and polarization.
-   **Finite elements**: Used in real-space methods, where the hierarchy is created by refining the mesh (decreasing element size $h$) or increasing the polynomial order $p$ of the [shape functions](@entry_id:141015).

### Variational Principles for Excited States

The [variational principle](@entry_id:145218) is not limited to the ground state. It can be extended to characterize the entire [energy spectrum](@entry_id:181780) of the Hamiltonian.

#### Sequential Minimization

A straightforward way to find the energy of the first excited state, $E_1$, is to minimize the Rayleigh quotient over a restricted set of [trial functions](@entry_id:756165): those that are orthogonal to the true ground-state [eigenfunction](@entry_id:149030) $|\phi_0\rangle$ .

$$
E_1 = \min_{\psi \perp \phi_0, \psi \ne 0} R[\psi]
$$

This can be generalized. The $k$-th eigenvalue $E_k$ can be found by minimizing the Rayleigh quotient over all [trial functions](@entry_id:756165) that are orthogonal to the entire subspace spanned by the first $k$ eigenfunctions, $\{\phi_0, \phi_1, \dots, \phi_{k-1}\}$.

$$
E_k = \min_{\psi \perp \text{span}\{\phi_0, \dots, \phi_{k-1}\}, \psi \ne 0} R[\psi]
$$

In a practical Rayleigh-Ritz calculation, one can find approximate excited states by first solving $H\mathbf{c}=ES\mathbf{c}$ to get an approximate ground state $|\psi_0\rangle$, and then solving the same problem in the subspace of functions orthogonal to $|\psi_0\rangle$. If an eigenvalue $E_k$ is $m$-fold degenerate ($E_k = E_{k+1} = \dots = E_{k+m-1}$), this procedure will yield the same minimum energy $E_k$ for $m$ successive steps, and any [orthonormal set](@entry_id:271094) of the resulting eigenvectors will form a basis for the degenerate [eigenspace](@entry_id:150590).

#### The Min-Max Principle

The sequential minimization approach has a practical limitation: it requires knowing the exact lower-energy [eigenfunctions](@entry_id:154705). A more powerful and elegant formulation that bypasses this requirement is the **Courant-Fischer-Weyl [min-max principle](@entry_id:150229)**  . It characterizes the $n$-th eigenvalue ($E_{n-1}$ with index starting from 0, or $E_n$ with index from 1) directly as:

$$
E_n = \min_{\substack{S \subset \mathcal{H} \\ \dim S = n+1}} \left( \max_{\substack{\psi \in S \\ \psi \ne 0}} R[\psi] \right)
$$

In words, the $(n+1)$-th eigenvalue is found by considering all $(n+1)$-dimensional subspaces $S$ of the Hilbert space. For each subspace, we find the maximum possible value of the Rayleigh quotient. The eigenvalue $E_n$ is the minimum of these maximums. There is also a dual **max-min principle**:

$$
E_n = \max_{\substack{T \subset \mathcal{H} \\ \dim T = n}} \left( \min_{\substack{\psi \perp T \\ \psi \ne 0}} R[\psi] \right)
$$

#### Properties of Ritz Eigenvalues for Excited States

The [min-max principle](@entry_id:150229) is not just a theoretical curiosity; it is the key to understanding the behavior of approximate eigenvalues obtained from the Rayleigh-Ritz method. When we restrict the search to a finite-dimensional subspace $\mathcal{S}_m$, the approximate eigenvalues, called **Ritz values** $\lambda_k^{(m)}$, are given by the [min-max principle](@entry_id:150229) restricted to that subspace.

From this, two crucial properties follow, collectively known as the **Hylleraas-Undheim-MacDonald theorem** :

1.  **Upper-Bound Property**: The $k$-th Ritz value is an upper bound to the $k$-th exact eigenvalue: $\lambda_k^{(m)} \ge E_k$. This is because the minimization in the min-max formula for $\lambda_k^{(m)}$ is over a smaller set of subspaces (those contained within $\mathcal{S}_m$) than for the exact $E_k$.

2.  **Monotonic Convergence**: For a sequence of nested subspaces $\mathcal{S}_m \subset \mathcal{S}_{m+1}$, the Ritz eigenvalues are monotonically non-increasing: $\lambda_k^{(m+1)} \le \lambda_k^{(m)}$. This is because the minimization for $\lambda_k^{(m+1)}$ is over a larger set of trial subspaces than for $\lambda_k^{(m)}$.

Together, these properties guarantee that as we systematically improve our basis set, each approximate eigenvalue converges monotonically from above towards its exact counterpart. A stronger result, the **Cauchy Interlacing Theorem**, states that for nested subspaces $\mathcal{S}_m \subset \mathcal{S}_{m+1}$ with $\dim \mathcal{S}_{m+1} = \dim \mathcal{S}_m + 1$, the old and new Ritz values are interlaced: $\lambda_k^{(m+1)} \le \lambda_k^{(m)} \le \lambda_{k+1}^{(m+1)}$ .

### Advanced Application: The Variational Principle in Density Functional Theory

Perhaps the most impactful application of the variational principle in modern [materials simulation](@entry_id:176516) is **Density Functional Theory (DFT)**. DFT reframes the entire [quantum many-body problem](@entry_id:146763), shifting the focus from the complex [many-body wavefunction](@entry_id:203043) to the much simpler electron density, $n(\mathbf{r})$. This conceptual leap is founded on two variational theorems.

#### The Hohenberg-Kohn Theorems

The formal foundation of DFT is provided by the two **Hohenberg-Kohn (HK) theorems** . For a system of interacting electrons in an external potential $v_{\text{ext}}(\mathbf{r})$:

1.  **First HK Theorem**: The external potential $v_{\text{ext}}(\mathbf{r})$ is determined, up to an additive constant, by the ground-state electron density $n_0(\mathbf{r})$. Since $v_{\text{ext}}(\mathbf{r})$ determines the Hamiltonian, and the Hamiltonian determines all properties of the system, it follows that the ground-state density is the fundamental variable containing all information about the ground state.

2.  **Second HK Theorem**: A universal energy functional of the density, $E[n]$, can be defined. The exact ground-state energy of the system is the global minimum of this functional over the set of all physically realizable densities (so-called $N$-representable densities). The density that minimizes this functional is the true ground-state density, $n_0(\mathbf{r})$.

The second theorem is a powerful restatement of the [variational principle](@entry_id:145218). Instead of minimizing $\langle\Psi|\hat{H}|\Psi\rangle$ over trial wavefunctions, we now minimize an [energy functional](@entry_id:170311) $E[n]$ over trial densities.

#### The Energy Functional and its Minimization

In practice, for example in **orbital-free DFT**, the total [energy functional](@entry_id:170311) is written as a sum of components :

$$
E[n] = T_s[n] + E_{\text{H}}[n] + E_{\text{xc}}[n] + \int v_{\text{ext}}(\mathbf{r}) n(\mathbf{r}) d\mathbf{r}
$$

Here, $T_s[n]$ is the kinetic energy functional of a non-interacting reference system, $E_{\text{H}}[n]$ is the classical electrostatic (Hartree) energy, $E_{\text{xc}}[n]$ is the [exchange-correlation functional](@entry_id:142042) containing all the complex many-body effects, and the final term is the interaction with the external potential.

The variational problem is to minimize $E[n]$ subject to the constraint that the total number of electrons is conserved: $\int n(\mathbf{r}) d\mathbf{r} = N$. Using the method of Lagrange multipliers, this constrained minimization leads to an **Euler-Lagrange equation**:

$$
\frac{\delta E[n]}{\delta n(\mathbf{r})} = \mu
$$

where $\mu$ is the Lagrange multiplier, which is physically interpreted as the **chemical potential** of the electron system. Expanding the functional derivative gives the central equation of DFT:

$$
\frac{\delta T_s[n]}{\delta n(\mathbf{r})} + v_{\text{H}}(\mathbf{r}) + v_{\text{xc}}(\mathbf{r}) + v_{\text{ext}}(\mathbf{r}) = \mu
$$

where $v_{\text{H}}(\mathbf{r}) = \delta E_{\text{H}}[n]/\delta n(\mathbf{r})$ and $v_{\text{xc}}(\mathbf{r}) = \delta E_{\text{xc}}[n]/\delta n(\mathbf{r})$ are the Hartree and exchange-correlation potentials, respectively.

#### The Mathematical Foundation: Convexity

The existence of a minimizing density and the validity of the Euler-Lagrange equation rest on deep mathematical properties of the [universal functional](@entry_id:140176). The modern, rigorous formulation of DFT, pioneered by Elliott Lieb, employs tools from convex analysis .

In this framework, the [universal functional](@entry_id:140176) $F[n] = T_s[n] + E_{\text{H}}[n] + E_{\text{xc}}[n]$ is proven to be a **convex** and **lower semicontinuous** functional on the space of $N$-representable densities.

-   **Convexity** ($F[\lambda n_1 + (1-\lambda)n_2] \le \lambda F[n_1] + (1-\lambda)F[n_2]$) is a crucial property. It ensures that any [local minimum](@entry_id:143537) of the total [energy functional](@entry_id:170311) is also the [global minimum](@entry_id:165977), which dramatically simplifies the minimization problem.
-   **Lower semicontinuity**, together with [convexity](@entry_id:138568) and a property called coercivity, guarantees (by the direct method of the [calculus of variations](@entry_id:142234)) that a minimizing density exists. The variational problem is well-posed.

A key insight from convex analysis is the concept of the **[subdifferential](@entry_id:175641)**, denoted $\partial F[n]$. The [subdifferential](@entry_id:175641) is a generalization of the derivative for functionals that may not be differentiable everywhere. For a convex functional, a minimum is characterized by a [subdifferential](@entry_id:175641) inclusion. The Euler-Lagrange equation is more rigorously written as:

$$
0 \in \partial F[n] + v_{\text{ext}} - \mu \quad \text{or} \quad -(v_{\text{ext}}(\mathbf{r}) - \mu) \in \partial F[n]
$$

This states that the negative of the effective potential, $-(v_{\text{ext}} - \mu)$, must be an element of the set of "subgradients" of $F$ at the ground-state density $n$. If $F[n]$ happens to be differentiable at $n$, the [subdifferential](@entry_id:175641) contains only one element, the standard functional derivative $\delta F/\delta n$, and we recover the familiar Euler-Lagrange equality. This rigorous mathematical structure ensures that the [variational principle](@entry_id:145218) of DFT is not just a formal prescription but a well-defined and solvable problem, providing the solid foundation upon which much of modern computational materials science is built.