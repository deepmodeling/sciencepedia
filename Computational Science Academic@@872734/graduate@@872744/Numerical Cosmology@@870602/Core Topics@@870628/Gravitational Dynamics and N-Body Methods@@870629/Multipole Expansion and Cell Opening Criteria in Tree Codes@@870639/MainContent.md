## Introduction
In the quest to understand the formation of cosmic structures, [numerical cosmology](@entry_id:752779) faces a fundamental challenge: the immense computational cost of the gravitational N-body problem. Directly calculating the force between every pair of particles in a simulation scales as $\mathcal{O}(N^2)$, a complexity that quickly becomes prohibitive for the millions or billions of particles required for realistic models. Hierarchical [tree codes](@entry_id:756159), a cornerstone of modern [computational astrophysics](@entry_id:145768), provide an elegant solution, reducing this complexity to a far more manageable $\mathcal{O}(N \log N)$.

However, this efficiency gain is not free; it relies on a sophisticated [approximation scheme](@entry_id:267451). This article addresses the crucial question of how [tree codes](@entry_id:756159) approximate gravitational forces accurately and efficiently. It demystifies the core mechanisms that balance computational speed with physical fidelity, providing a graduate-level deep dive into the theory and practice behind these essential algorithms.

Throughout this guide, you will gain a comprehensive understanding of this powerful technique. The first chapter, **Principles and Mechanisms**, delves into the mathematical foundation of the multipole expansion and the pivotal role of the cell opening criterion in controlling error. The second chapter, **Applications and Interdisciplinary Connections**, explores how these concepts are applied in [cosmological simulations](@entry_id:747925), adapted for [high-performance computing](@entry_id:169980), and generalized to other physical systems. Finally, the **Hands-On Practices** section provides concrete exercises to solidify these theoretical concepts. We begin by examining the fundamental principles that allow us to approximate the gravitational influence of distant matter and the criteria used to decide when this approximation is valid.

## Principles and Mechanisms

The accurate and efficient computation of gravitational forces is a cornerstone of [numerical cosmology](@entry_id:752779). While direct summation of all pairwise interactions offers perfect accuracy, its $\mathcal{O}(N^2)$ computational complexity renders it impractical for the large-scale simulations necessary to model [cosmic structure formation](@entry_id:137761). Hierarchical [tree codes](@entry_id:756159), such as the Barnes-Hut algorithm, reduce this complexity to a manageable $\mathcal{O}(N \log N)$ by approximating the gravitational influence of distant groups of particles. This chapter delves into the fundamental principles and mechanisms underpinning this approximation: the [multipole expansion](@entry_id:144850) of the [gravitational potential](@entry_id:160378) and the cell opening criteria that govern its application.

### The Multipole Expansion of the Gravitational Potential

The foundation of the tree-code approximation lies in the multipole expansion, a concept rooted in classical [potential theory](@entry_id:141424). The exact Newtonian gravitational potential $\Phi(\mathbf{r})$ at a field point $\mathbf{r}$ due to a collection of source masses $\{m_a\}$ at positions $\{\mathbf{x}_a\}$ is given by the sum of their individual potentials:

$$
\Phi(\mathbf{r}) = - G \sum_{a} \frac{m_a}{|\mathbf{r} - \mathbf{x}_a|}
$$

When the field point $\mathbf{r}$ is far from a localized group of sources contained within a tree cell, we can approximate this sum without treating each source individually. Let us choose an **expansion center** $\mathbf{x}_0$ for the cell (e.g., its geometric center or center of mass). We can then rewrite the distance term as $|\mathbf{R} - \mathbf{y}_a|$, where $\mathbf{R} \equiv \mathbf{r} - \mathbf{x}_0$ is the vector from the expansion center to the field point, and $\mathbf{y}_a \equiv \mathbf{x}_a - \mathbf{x}_0$ is the position of a source particle relative to the expansion center. For a distant field point, $|\mathbf{y}_a| \ll |\mathbf{R}|$. This allows us to perform a Taylor expansion of the Green's function $1/|\mathbf{R} - \mathbf{y}_a|$ in powers of the small ratio $|\mathbf{y}_a|/|\mathbf{R}|$.

The expansion up to the second order yields:

$$
\frac{1}{|\mathbf{R} - \mathbf{y}_a|} \approx \frac{1}{R} + \frac{\mathbf{R} \cdot \mathbf{y}_a}{R^3} + \frac{1}{2} \sum_{i,j} \frac{3 R_i R_j - \delta_{ij} R^2}{R^5} y_{a,i} y_{a,j}
$$

where $R = |\mathbf{R}|$, and the indices $i, j$ denote Cartesian components. Substituting this back into the potential sum and grouping terms by powers of $1/R$, we obtain the multipole expansion of the potential. The coefficients of this expansion are the **[multipole moments](@entry_id:191120)** of the mass distribution within the cell, computed with respect to the expansion center $\mathbf{x}_0$ [@problem_id:3480596].

The first three Cartesian moments are:

- **Monopole moment**: The total mass of the cell. This is a scalar.
  $$ M = \sum_a m_a $$
  The monopole term represents the potential of the entire cell as if it were a single point mass located at the expansion center.

- **Dipole moment**: A vector quantity that captures the first-order asymmetry of the [mass distribution](@entry_id:158451).
  $$ \mathbf{D} = \sum_a m_a (\mathbf{x}_a - \mathbf{x}_0) $$

- **Quadrupole moment**: A [symmetric tensor](@entry_id:144567) that describes the second-order shape of the [mass distribution](@entry_id:158451). It is often represented in its **traceless** form to simplify the potential expression:
  $$ Q_{ij} = \sum_a m_a \left( 3 (\mathbf{x}_a - \mathbf{x}_0)_i (\mathbf{x}_a - \mathbf{x}_0)_j - \delta_{ij} |\mathbf{x}_a - \mathbf{x}_0|^2 \right) $$

Using these moments, the potential can be approximated as a sum of terms corresponding to each multipole order:
$\Phi(\mathbf{r}) \approx \Phi_{\text{mono}} + \Phi_{\text{dipole}} + \Phi_{\text{quad}} + \dots$

This expansion is fundamentally a solution to **Laplace's equation**, $\nabla^2\Phi = 0$, which governs the gravitational potential in source-free space. The general solution in [spherical coordinates](@entry_id:146054) involves terms with radial dependence $r^{\ell}$ (**interior solution**) and $r^{-(\ell+1)}$ (**exterior solution**), each multiplied by spherical harmonics $Y_{\ell m}(\hat{\mathbf{r}})$ that describe the angular dependence. The [spherical harmonics](@entry_id:156424) form a complete [orthonormal basis](@entry_id:147779) on the unit sphere [@problem_id:3480557]. For a localized source distribution, the potential must vanish at infinity, which forces us to select only the exterior solution terms that decay with distance. The [multipole expansion](@entry_id:144850) is precisely this exterior solution, and its convergence is guaranteed only for points outside a sphere that encloses all the source mass.

### Error Analysis and Control

The utility of the [multipole expansion](@entry_id:144850) lies in its truncation. By keeping only a few terms (e.g., up to the quadrupole), we obtain a computationally cheap approximation. The accuracy of this approximation is determined by the magnitude of the first neglected term.

Let $s$ be a characteristic size of the source cell and $d = |\mathbf{r} - \mathbf{x}_0|$ be the distance to the field point. The potential contribution from the multipole of order $\ell$ scales as $\Phi_\ell \sim M s^\ell / d^{\ell+1}$. The corresponding force contribution, being the gradient of the potential, scales as $F_\ell \sim M s^\ell / d^{\ell+2}$. A crucial insight is that the **[relative error](@entry_id:147538)** from neglecting the $\ell$-th order term, compared to the dominant monopole force ($F_0 \sim M/d^2$), scales identically for both the potential and the force [@problem_id:3480541]:

$$
\frac{|\Phi_\ell|}{|\Phi_0|} \sim \left(\frac{s}{d}\right)^\ell \quad \text{and} \quad \frac{|F_\ell|}{|F_0|} \sim \left(\frac{s}{d}\right)^\ell
$$

The accuracy of a truncated expansion therefore depends critically on two factors: the order of truncation and the choice of expansion center.

A judicious choice of expansion center can make lower-order moments vanish, significantly improving accuracy for a given truncation level. If we choose the cell's **center of mass (COM)** as the expansion center $\mathbf{x}_0$, the dipole moment $\mathbf{D} = \sum_a m_a (\mathbf{x}_a - \mathbf{x}_{\text{COM}})$ becomes identically zero by definition [@problem_id:3480596]. In this "COM gauge", the first non-zero moment after the monopole is typically the quadrupole.

Let's consider the impact on a monopole-only approximation ($p=0$, where $p$ is the highest multipole order retained).
- If the expansion center is arbitrary, the leading error comes from the neglected dipole ($\ell=1$), and the relative force error scales as $\mathcal{O}(s/d)$.
- If the expansion center is the COM, the dipole vanishes. The leading error now comes from the neglected quadrupole ($\ell=2$), and the relative force error scales as $\mathcal{O}((s/d)^2)$ [@problem_id:3480541] [@problem_id:3480604].

This demonstrates the profound advantage of centering the expansion on the COM. A small, unintentional offset $\boldsymbol{\epsilon}$ from the COM will reintroduce a dipole-like error term that is linear in $\epsilon$ and dominates the intrinsic quadrupole error, significantly degrading accuracy [@problem_id:3480574]. For certain highly symmetric mass distributions, such as two equal masses placed symmetrically about the origin, the dipole moment is naturally zero. In these cases, the [quadrupole moment](@entry_id:157717) provides the leading correction to the monopole approximation, and the error is intrinsically of higher order [@problem_id:3480554].

If we truncate the expansion after the quadrupole term ($p=2$) in the COM gauge, the first neglected non-zero term is the octupole ($\ell=3$). The leading relative force error in this case scales as $\mathcal{O}((s/d)^3)$ [@problem_id:3480596].

### The Cell Opening Criterion: Bridging Theory and Practice

The [error analysis](@entry_id:142477) provides a clear prescription for controlling accuracy: the ratio $s/d$ must be kept small. Tree codes operationalize this principle through a **Multipole Acceptance Criterion (MAC)**, most commonly the Barnes-Hut **opening criterion**.

This criterion states that a cell's multipole approximation can be used if the cell is sufficiently far away relative to its size. This condition is expressed as:

$$
\frac{s}{d} \le \theta
$$

Here, $\theta$ is a user-defined dimensionless **opening parameter** or tolerance, typically in the range of $0.5$ to $1.0$. If the condition is met, the cell is considered to be in the "far-field," and its multipole contribution is added to the force calculation. If the condition is violated ($s/d > \theta$), the cell is too close or too large to be accurately represented by the truncated expansion. The algorithm then "opens" the cell and recursively applies the criterion to its children.

The parameter $\theta$ provides direct control over the [approximation error](@entry_id:138265). For instance, if the leading [relative error](@entry_id:147538) $\delta$ scales as $\delta \approx C(s/d)^2$ (as in a monopole approximation about the COM), then by using the opening criterion, we ensure that the maximum error incurred from any single cell is bounded by $\delta_{\text{max}} \approx C\theta^2$ [@problem_id:3480604]. A smaller value of $\theta$ forces the algorithm to open more cells and descend deeper into the tree, performing more direct calculations and improving accuracy at the cost of increased computation time. For example, changing $\theta$ from $0.8$ to $0.5$ requires that a cell be significantly farther away before it is accepted, and reduces the error at the acceptance threshold by a factor of $(0.5/0.8)^2 = 25/64$.

A subtle but crucial aspect of the MAC is the definition of the [cell size](@entry_id:139079) $s$. For the multipole approximation to be mathematically valid, the field point must lie outside the **sphere of convergence** of the expansion. This sphere is centered on the expansion origin $\mathbf{x}_0$ and must enclose all mass within the cell. Therefore, a scientifically rigorous definition for $s$ is the radius of this minimal enclosing sphere [@problem_id:3480576]:

$$
s = \max_{a} |\mathbf{x}_a - \mathbf{x}_0|
$$

In practice, since we only know that particles are within a [bounding box](@entry_id:635282), $s$ is taken as the distance from the expansion center to the farthest corner of the box. While simpler heuristics are sometimes used, such as setting $s$ to the longest side of the [bounding box](@entry_id:635282), they can lead to inconsistencies. For an elongated cell, for instance, the choice of definition for $s$ (e.g., "max-side" versus "circumscribed radius") can significantly alter the distance at which the cell is accepted, thereby affecting which interactions are approximated and which are computed directly [@problem_id:3480553].

### The Complete Tree Algorithm

The principles of multipole expansion and the cell opening criterion are integrated into a cohesive algorithm for calculating the [gravitational force](@entry_id:175476) on every particle in the simulation. For each target particle $i$, the algorithm performs a "tree walk" starting from the root of the [octree](@entry_id:144811). This walk partitions all other particles in the simulation into two sets: a **[near-field](@entry_id:269780)** and a **[far-field](@entry_id:269288)**.

The process is recursive [@problem_id:3480612]:
1.  Start with the root node of the tree.
2.  For the current node, compute its size $s$ and distance $d$ to the target particle $i$.
3.  Apply the MAC: Check if $s/d \le \theta$.
4.  If the criterion is met, the node is accepted. Its contribution to the force on particle $i$ is computed using its stored [multipole moments](@entry_id:191120) (e.g., monopole or monopole+quadrupole). This node is added to the **far-field interaction list**, $\mathcal{M}_i$, and the recursion down this branch of the tree terminates.
5.  If the criterion is not met, the node is opened. The algorithm is then called recursively on each of the node's children.
6.  If the [recursion](@entry_id:264696) reaches a leaf node (a node containing only one or a small number of particles), these individual particles are added to the **near-field interaction list**, $\mathcal{N}_i$.

This traversal ensures that every source particle in the simulation is accounted for exactly once, either as part of an aggregated multipole from the [far-field](@entry_id:269288) list or as an individual particle in the [near-field](@entry_id:269780) list. This avoids any [double counting](@entry_id:260790). The total acceleration on particle $i$ is the sum of contributions from both lists:

$$
\mathbf{a}_{i} = \sum_{j \in \mathcal{N}_{i}} \mathbf{a}^{\mathrm{PP}}_{ij} + \sum_{n \in \mathcal{M}_{i}} \mathbf{a}^{\mathrm{MP}}_{in}
$$

where $\mathbf{a}^{\mathrm{PP}}_{ij}$ is the force from a direct particle-particle (PP) calculation and $\mathbf{a}^{\mathrm{MP}}_{in}$ is the force from the multipole-particle (MP) approximation. This hybrid approach allows the algorithm to achieve an average computational complexity of $\mathcal{O}(N \log N)$, a dramatic improvement over the direct $\mathcal{O}(N^2)$ method.

### Extensions for Periodic Boundary Conditions

Cosmological simulations are typically performed in a cubic volume with **periodic boundary conditions (PBC)** to represent a statistically homogeneous patch of an infinite universe. This [periodicity](@entry_id:152486) fundamentally alters the nature of the gravitational interaction. The potential at any point is influenced not only by the particles in the primary simulation box but also by their infinite lattice of periodic images.

A pure [tree code](@entry_id:756158) based on the vacuum ($1/r$) [multipole expansion](@entry_id:144850) is not suitable for periodic simulations. The [direct sum](@entry_id:156782) of the $1/r$ potential over an infinite lattice is only conditionally convergent, and the periodic Green's function for the Poisson equation is fundamentally different from the vacuum kernel. A pure [tree code](@entry_id:756158) fails to capture the long-range (low-[wavenumber](@entry_id:172452), or small-$k$) component of the periodic gravitational field, leading to significant errors in large-scale dynamics [@problem_id:3480549].

To correctly handle gravity under PBC, [tree codes](@entry_id:756159) must be augmented with methods that properly account for the long-range [periodic potential](@entry_id:140652). Two standard approaches are:
- **Ewald Summation**: This technique splits the periodic sum into two rapidly converging parts: a short-range component calculated in real space (which can be handled by a tree) and a long-range component calculated in reciprocal (Fourier) space. The [reciprocal-space sum](@entry_id:754152) explicitly computes the contribution from the crucial low-$k$ modes.
- **Tree-Particle-Mesh (TreePM)**: This hybrid method splits the force calculation. A fast Fourier transform (FFT)-based Particle-Mesh (PM) solver is used on a grid to compute the long-range part of the force, correctly incorporating the periodic Green's function. The tree is then used to compute the remaining short-range force, where the vacuum approximation is accurate.

In both cases, the tree algorithm's efficiency in handling [short-range interactions](@entry_id:145678) is combined with a Fourier-space method that correctly models the long-range physics dictated by the periodic boundary conditions.