## Introduction
Understanding how cells transition between states is a central question in biology, fundamental to development, regeneration, and disease. Modern single-cell technologies provide high-resolution snapshots of cell populations at different time points, but these static pictures leave a critical knowledge gap: how did the cells in the initial state transform into the cells of the final state? Inferring these dynamic processes from static data is a major challenge in [computational systems biology](@entry_id:747636). Optimal Transport (OT) offers a powerful and principled mathematical framework to address this challenge. By representing cell populations as distributions, OT allows us to compute the most 'efficient' or plausible mapping that transforms one distribution into another, revealing the underlying dynamics of cellular transitions.

This article provides a comprehensive exploration of optimal transport models in the context of [cell biology](@entry_id:143618). In the first chapter, "Principles and Mechanisms," we will build the mathematical foundations from the ground up, defining how cell populations are represented and exploring the core concepts of the Monge and Kantorovich problems, the role of the cost function, and key extensions like [entropic regularization](@entry_id:749012) and unbalanced transport. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the power of this framework by exploring its use in defining biologically informed costs, integrating multi-omic and spatial data, and even making predictive and counterfactual statements about cell fate. Finally, the "Hands-On Practices" chapter offers a set of focused problems designed to solidify your theoretical understanding through practical application.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mathematical mechanisms that underpin the application of optimal transport (OT) to the study of [cell state transitions](@entry_id:747193). We will build the framework from the ground up, starting with the representation of cell populations as mathematical objects and progressing to the advanced formulations of OT that enable robust and biologically realistic modeling.

### Representing Cell Populations as Probability Measures

To apply a rigorous mathematical framework to cell populations, we must first formalize their representation. A population of cells, characterized by their gene expression profiles, can be conceptualized as a distribution of points in a high-dimensional state space, $\mathcal{X} = \mathbb{R}^d$, where $d$ is the number of genes measured. At any given time $t$, we can define a **population-level probability measure**, $\mu_t$, on this space. This measure captures the distribution of cell states across the entire [biological population](@entry_id:200266). Formally, for any region (Borel set) $B \subset \mathbb{R}^d$, $\mu_t(B)$ gives the probability that a cell drawn uniformly at random from the population at time $t$ will have a gene expression profile falling within $B$ [@problem_id:3335602].

In practice, we do not have access to the true population measure $\mu_t$. Instead, single-cell technologies like scRNA-seq provide us with a finite sample of cell profiles at discrete time points, $\{X_i^{(t)}\}_{i=1}^{N_t}$. To connect this data to the underlying measure, we make a critical modeling assumption: that the experimental sampling process is **state-independent**. This assumption posits that the likelihood of capturing and sequencing a cell does not depend on its transcriptomic state. Under this condition, the observed cell profiles can be treated as **[independent and identically distributed](@entry_id:169067) (i.i.d.)** samples drawn from the true population measure $\mu_t$ [@problem_id:3335602].

Given a set of $N$ i.i.d. samples $\{x_i\}_{i=1}^N$ from a population, we construct an **[empirical measure](@entry_id:181007)**, $\hat{\mu}$, which serves as a discrete approximation of the true continuous measure $\mu$. The [empirical measure](@entry_id:181007) is defined as a sum of Dirac masses, where each observed cell is an atom of the distribution, weighted equally:

$$
\hat{\mu} = \frac{1}{N} \sum_{i=1}^{N} \delta_{x_i}
$$

Here, $\delta_{x_i}$ is a Dirac measure that places all of its mass (in this case, a mass of $1/N$) at the single point $x_i$. The Law of Large Numbers guarantees that as the sample size $N$ increases, the [empirical measure](@entry_id:181007) $\hat{\mu}$ converges to the true underlying measure $\mu$. In OT-based modeling, we work directly with these empirical measures constructed from experimental data.

The raw data from sequencing experiments often requires preprocessing, such as library size normalization, which can significantly impact the geometry of the state space. For instance, a common normalization technique transforms a raw count vector $x_i$ by dividing it by its total sum, $y_i = x_i / (\mathbf{1}^\top x_i)$. This operation, when applied to all cells, is a transformation on the support of the [empirical measure](@entry_id:181007). Mathematically, the new [empirical measure](@entry_id:181007) on the normalized data, $\hat{\nu} = \frac{1}{N}\sum \delta_{y_i}$, is a **pushforward** of the original [empirical measure](@entry_id:181007) $\hat{\mu}$ by the normalization map. This particular transformation projects all [cell state](@entry_id:634999) vectors onto the probability [simplex](@entry_id:270623), fundamentally altering the geometric relationships between them, which in turn affects the subsequent OT calculations [@problem_id:3335641].

### The Core Problem of Optimal Transport: From Monge to Kantorovich

With cell populations at two time points, $t_0$ and $t_1$, represented by probability measures $\mu_0$ and $\mu_1$, the central question becomes: what is the most plausible or "efficient" way that the initial population transformed into the final one? Optimal transport provides a framework to answer this by finding a "transport plan" that minimizes a total cost.

The earliest formulation of this problem is attributed to Gaspard Monge. The **Monge problem** seeks a deterministic **transport map**, $T: \mathcal{X} \to \mathcal{X}$, that pushes the initial measure $\mu_0$ onto the final measure $\mu_1$ (denoted $T_\# \mu_0 = \mu_1$) while minimizing the total transport cost:

$$
\inf_{T: T_\# \mu_0 = \mu_1} \int_{\mathcal{X}} c(x, T(x)) \,d\mu_0(x)
$$

Here, $c(x, y)$ is a [cost function](@entry_id:138681) that quantifies the effort required to move a cell from state $x$ to state $y$. The Monge formulation is intuitive, suggesting that each cell at $t_0$ has a unique descendant state at $t_1$. However, this formulation is often too restrictive. For instance, it forbids a single [cell state](@entry_id:634999) from giving rise to multiple distinct descendant states (mass splitting) or multiple initial states from converging to a single final state (mass merging). Consequently, a solution to the Monge problem may not exist, especially for discrete empirical measures derived from single-cell data [@problem_id:3335652].

To overcome these limitations, Leonid Kantorovich proposed a more general formulation. The **Kantorovich problem** relaxes the requirement of a deterministic map. Instead of a map, it seeks a **transport plan** or **coupling**, which is a joint probability measure $\pi$ on the product space $\mathcal{X} \times \mathcal{X}$. The value $\pi(A, B)$ can be interpreted as the amount of mass that is transported from a source region $A$ to a target region $B$. A valid coupling must have $\mu_0$ and $\mu_1$ as its marginals. The set of all such valid couplings is denoted $\Pi(\mu_0, \mu_1)$. The Kantorovich primal problem is then to find the coupling that minimizes the expected transport cost:

$$
\inf_{\pi \in \Pi(\mu_0, \mu_1)} \int_{\mathcal{X} \times \mathcal{X}} c(x, y) \,d\pi(x, y)
$$

This formulation allows for both mass splitting and merging and, crucially, is guaranteed to have a solution for any pair of probability measures $\mu_0$ and $\mu_1$ on a reasonably well-behaved space. Every Monge map corresponds to a specific type of Kantorovich coupling, but not vice-versa, making the Kantorovich formulation a powerful and general relaxation [@problem_id:3335652].

When applied to discrete empirical measures $\mu_0 = \sum_{i=1}^n a_i \delta_{x_i}$ and $\mu_1 = \sum_{j=1}^m b_j \delta_{y_j}$, the Kantorovich problem becomes a **linear program**. The coupling $\pi$ becomes a matrix of flows $\pi_{ij} \ge 0$, where $\pi_{ij}$ is the amount of mass moving from source cell $i$ to target cell $j$. The cost becomes a matrix $C_{ij} = c(x_i, y_j)$. The objective is to find the matrix $\pi$ that minimizes the total cost, $\sum_{i,j} C_{ij} \pi_{ij}$, subject to the marginal constraints:

- $\sum_{j=1}^m \pi_{ij} = a_i$ for each source cell $i=1, \dots, n$.
- $\sum_{i=1}^n \pi_{ij} = b_j$ for each target cell $j=1, \dots, m$.

These constraints enforce that the total mass flowing out of each initial state matches its observed abundance, and the total mass flowing into each final state matches its abundance. This models the aggregate flow of the cell population, not the fate of individual cells [@problem_id:3335583]. A prerequisite for this "balanced" OT problem is that the total mass must be conserved, i.e., $\sum a_i = \sum b_j$. Biologically, this assumes that processes like [cell proliferation](@entry_id:268372) and death are negligible between the two time points [@problem_id:3335602].

### Defining the Geometry: The Role of the Cost Function

The choice of the [cost function](@entry_id:138681) $c(x, y)$ is a critical modeling decision, as it defines the geometry of the transport problem and encodes our biological assumptions about the "effort" of a state transition.

A ubiquitous choice is the **squared Euclidean cost**, $c(x, y) = \|x - y\|_2^2$. This cost has several desirable mathematical properties. It is invariant to joint translations and rotations of the state space. For instance, applying a Principal Component Analysis (PCA) rotation to the data will not change the transport cost between any two points. A profound result, **Brenier's theorem**, states that for the squared Euclidean cost (and an absolutely continuous source measure), the optimal Kantorovich plan is, in fact, concentrated on the graph of a unique Monge map $T$. Furthermore, this map has a special structure: it is the gradient of a convex function, $T(x) = \nabla\phi(x)$. This connects the general Kantorovich theory back to a deterministic map and provides a powerful structural characterization of the inferred cellular flows as a [conservative vector field](@entry_id:265036) in gene expression space [@problem_id:3335652] [@problem_id:3335596] [@problem_id:3335596]. Displacement interpolation under this cost follows straight lines, aligning the model with a physical interpretation of minimum kinetic energy [@problem_id:3335596].

Another common choice, particularly relevant for gene expression data, is the **cosine dissimilarity**, $c(x, y) = 1 - \frac{x \cdot y}{\|x\|_2 \|y\|_2}$. This [cost function](@entry_id:138681) measures the angle between two state vectors. Its key property is invariance to positive rescaling of the vectors. This means it only considers the relative expression program of a cell, ignoring differences in total mRNA content (or library size). Two cells with proportional gene expression vectors will have zero cost between them. However, unlike the squared Euclidean cost, cosine dissimilarity is not a true metric (it violates the identity of indiscernibles and the [triangle inequality](@entry_id:143750)) and does not benefit from the elegant structural results of Brenier's theorem [@problem_id:3335596].

The selection of a cost function must be guided by the biological question and the nature of the data. Both squared Euclidean and cosine costs are invariant under a common orthonormal change of basis (e.g., PCA), but their differing sensitivities to vector magnitude versus direction lead to distinct transport geometries and biological interpretations [@problem_id:3335596].

### Deeper Insights from Duality and Dynamic Formulations

Beyond the primal problem of finding the [optimal coupling](@entry_id:264340), OT offers deeper perspectives through its dual and dynamic formulations.

The **Kantorovich [dual problem](@entry_id:177454)** provides an alternative, and often highly informative, view. The [dual problem](@entry_id:177454) is a maximization over a pair of functions $(\phi, \psi)$, known as **potentials**, defined on the source and target spaces, respectively:

$$
\sup_{\phi, \psi} \left\{ \int \phi \,d\mu_0 + \int \psi \,d\mu_1 \right\} \quad \text{subject to} \quad \phi(x) + \psi(y) \le c(x, y)
$$

The value of the [dual problem](@entry_id:177454) is equal to the primal OT cost. The optimal potentials $(\phi^*, \psi^*)$ have a powerful interpretation. They decompose the transition cost $c(x,y)$ into source-specific ($\phi^*(x)$) and target-specific ($\psi^*(y)$) contributions. A fundamental result states that the [optimal transport](@entry_id:196008) plan $\pi^*$ only moves mass between pairs $(x,y)$ where the dual constraint is active, i.e., $\phi^*(x) + \psi^*(y) = c(x,y)$. In a [cell biology](@entry_id:143618) context, a high potential $\phi^*(x)$ might indicate an unstable or "poised" state that is likely to transition, while a low potential $\psi^*(y)$ could represent a stable state or a developmental endpoint that is an attractive fate. The potentials thus help to reveal the underlying energy landscape, including transition barriers and affinities, that drives [cell state transitions](@entry_id:747193) [@problem_id:3335649].

An entirely different but equivalent perspective on OT (for the squared Euclidean cost) is provided by the **Benamou-Brenier dynamic formulation**. This formulation recasts the static [matching problem](@entry_id:262218) into a dynamic, fluid mechanics problem. It seeks a path of probability densities $\{\rho_t\}_{t \in [0,1]}$ and a time-dependent [velocity field](@entry_id:271461) $\{v_t\}_{t \in [0,1]}$ that evolves the initial distribution $\mu_0$ to the final distribution $\mu_1$. The evolution is governed by the **[continuity equation](@entry_id:145242)**, which enforces mass conservation:

$$
\partial_t \rho_t + \nabla \cdot (\rho_t v_t) = 0
$$

Among all paths satisfying this constraint and the boundary conditions $\rho_0 = \mu_0$ and $\rho_1 = \mu_1$, the one that corresponds to the [optimal transport](@entry_id:196008) plan is the one that minimizes the total kinetic energy of the flow:

$$
\inf_{\rho_t, v_t} \int_0^1 \int_{\mathcal{X}} \rho_t(x) \|v_t(x)\|^2 \,dx \,dt
$$

This value is exactly the squared Wasserstein-2 distance. In this view, $\rho_t$ is the distribution of the cell population at an intermediate time $t$, and $v_t(x)$ represents the average velocity of cells in gene expression space at state $x$. This provides a compelling, intuitive picture of the entire population "flowing" through the state space along the most energy-efficient path from the initial to the final configuration [@problem_id:3335613].

### Practical Extensions for Biological Realism and Computational Efficiency

The classical OT framework, while powerful, has limitations. Modern applications leverage several key extensions to enhance computational feasibility and biological relevance.

#### Entropic Regularization for Computation and Uncertainty

Solving the discrete OT problem as a linear program can be computationally expensive for large numbers of cells. Furthermore, the [optimal coupling](@entry_id:264340) is often sparse and highly sensitive to small perturbations in the data. **Entropic regularization** addresses both issues by adding a penalty term to the [objective function](@entry_id:267263) that favors "smoother" transport plans:

$$
\min_{\pi \in \Pi(\mu_0, \mu_1)} \left( \sum_{i,j} C_{ij} \pi_{ij} + \varepsilon \sum_{i,j} \pi_{ij} (\log \pi_{ij} - 1) \right)
$$

The parameter $\varepsilon > 0$ controls the strength of the regularization. This new objective is strictly convex, guaranteeing a unique [optimal coupling](@entry_id:264340) $\pi^\varepsilon$ [@problem_id:3335595]. This unique solution has a characteristic multiplicative structure: $\pi^\varepsilon_{ij} = u_i v_j \exp(-C_{ij}/\varepsilon)$, where $u_i$ and $v_j$ are scaling factors found efficiently using the **Sinkhorn-Knopp algorithm**.

The effect of $\varepsilon$ is analogous to temperature:
- As $\varepsilon \to 0^+$, the solution converges to a solution of the unregularized OT problem, typically a sparse coupling.
- As $\varepsilon$ increases, the coupling becomes denser and less sensitive to the [cost matrix](@entry_id:634848) $C$. Mass is spread more broadly, reflecting greater uncertainty in the transition paths. In the limit $\varepsilon \to \infty$, the coupling ignores the cost entirely and becomes the product of the marginals, $\pi_{ij} = a_i b_j$.

Biologically, this regularization can be interpreted as modeling diffusive or stochastic effects in [cell fate decisions](@entry_id:185088), while computationally it provides a fast, robust, and scalable algorithm for estimating transport plans [@problem_id:3335595].

#### Unbalanced Optimal Transport for Modeling Growth and Death

A major limitation of classical OT is the strict enforcement of [mass conservation](@entry_id:204015). Cell populations, however, are dynamic systems with ongoing proliferation and apoptosis. **Unbalanced Optimal Transport (UOT)** extends the framework to account for such changes in total mass.

Instead of enforcing the marginal constraints strictly, UOT relaxes them by introducing penalty terms into the [objective function](@entry_id:267263). A common approach uses a divergence, such as the Kullback-Leibler (KL) divergence, to penalize deviations of the coupling's marginals from the observed distributions:

$$
\min_{\pi \ge 0} \left( \langle \pi, C \rangle + \tau D_{\mathrm{KL}}(\pi \mathbf{1} \,\|\, \mu_0) + \tau D_{\mathrm{KL}}(\pi^{\top} \mathbf{1} \,\|\, \mu_1) \right)
$$

Here, $\pi\mathbf{1}$ and $\pi^\top\mathbf{1}$ are the row and column sums (the marginals) of the coupling $\pi$, and $\tau > 0$ is a parameter controlling how strictly the marginals are enforced. This formulation allows the optimization to find a transport plan where the total mass flowing out of a source state or into a target state may not match the observed data, if doing so significantly reduces the overall cost. The resulting deviations of the coupling's marginals from $\mu_0$ and $\mu_1$ can be interpreted as local mass creation (proliferation) or destruction (apoptosis), thus providing a principled way to infer state-specific growth and death rates directly from snapshot data [@problem_id:3335593].

#### The Gromov-Wasserstein Discrepancy for Cross-Modality Alignment

A growing challenge in [systems biology](@entry_id:148549) is the integration of data from different measurement modalities, such as scRNA-seq (transcriptome) and scATAC-seq ([epigenome](@entry_id:272005)), which are often measured on different sets of cells. In this scenario, the two cell populations live in entirely different feature spaces, $X$ and $Y$, making it impossible to define a meaningful cross-domain cost function $c(x,y)$.

The **Gromov-Wasserstein (GW) discrepancy** provides a solution by reformulating the transport problem. Instead of minimizing the cost of moving points, GW seeks to find a coupling that best preserves the *internal geometry* of the two spaces. It assumes we can compute intra-domain distance matrices, $D_X$ and $D_Y$, but not inter-domain ones. The GW objective finds a coupling $\pi$ that minimizes the discrepancy between the distances of paired points. For a quadratic loss function $L$, the objective is:

$$
\min_{\pi \in \Pi(\mu_0, \mu_1)} \sum_{i,k=1}^n \sum_{j,l=1}^m |D_X(x_i, x_k) - D_Y(y_j, y_l)|^2 \pi_{ij} \pi_{kl}
$$

This objective is quadratic in the transport plan $\pi$. Intuitively, it seeks a matching such that if two cells $x_i$ and $x_k$ are close in the first modality, their matched counterparts $y_j$ and $y_l$ should also be close in the second modality. The GW framework thus enables the comparison and alignment of distributions based on their intrinsic "shape," without requiring them to live in the same space, making it an indispensable tool for multi-omic [data integration](@entry_id:748204) [@problem_id:3335633].