## Introduction
The field of [nuclear reactor simulation](@entry_id:1128946) is undergoing a computational revolution, driven by the integration of machine learning (ML) and neural networks. Traditionally, high-fidelity simulations, while accurate, are burdened by immense computational costs, creating a significant bottleneck for complex tasks like design optimization, real-time control, and comprehensive uncertainty analysis. This article addresses this challenge by exploring how ML provides a new class of powerful and efficient tools tailored for nuclear engineering.

This article provides a comprehensive journey through the application of ML in [nuclear reactor simulation](@entry_id:1128946). The journey begins with the **Principles and Mechanisms** chapter, which lays the theoretical groundwork, explaining how ML models from data-driven surrogates to Physics-Informed Neural Networks are built upon and constrained by the laws of physics. Next, the **Applications and Interdisciplinary Connections** chapter showcases these methods in action, demonstrating their utility in solving real-world problems from inverse field reconstruction to creating digital twins for autonomous control. Finally, the **Hands-On Practices** section offers practical exercises, allowing you to apply these concepts and build your own physics-constrained models. By the end, you will have a deep understanding of how to leverage machine learning to solve some of the most pressing problems in nuclear science and engineering.

## Principles and Mechanisms

The integration of machine learning (ML) and neural networks into [nuclear reactor simulation](@entry_id:1128946) is not merely an application of generic data-fitting algorithms to a new domain. Instead, it represents a paradigm shift where the principles of machine learning are fused with the foundational laws of physics to create novel, powerful, and efficient computational tools. This chapter delineates the core principles and mechanisms underpinning these applications, moving from data-driven surrogates that accelerate existing simulations to [physics-informed models](@entry_id:753434) that directly solve the governing equations of reactor physics. We will explore how neural architectures can be tailored to respect physical symmetries and conservation laws, and how these models are rigorously integrated into engineering workflows for uncertainty quantification and validation.

### Surrogate Modeling for Simulation Acceleration

A primary driver for adopting ML in nuclear engineering is the formidable computational cost of high-fidelity simulations. Methods such as Monte Carlo [neutron transport](@entry_id:159564) provide high accuracy but may require hours or days of supercomputing time for a single core state evaluation. This cost is prohibitive for applications requiring many thousands or millions of queries, such as core design optimization, uncertainty quantification, or real-time control. ML-based surrogate models, trained on a limited set of high-fidelity data, can provide near-instantaneous predictions, serving as powerful accelerators.

#### Data-Driven Reduced-Order Modeling: From PCA to Autoencoders

The state of a nuclear reactor, often described by fields like the neutron flux or temperature distribution over a discretized mesh, can be represented as a very high-dimensional vector. For instance, a 3D flux map with millions of mesh points corresponds to a vector in $\mathbb{R}^n$ where $n$ is in the millions. However, the physically realizable states of the system typically do not populate this entire space. Instead, they lie on or near a much lower-dimensional manifold, governed by the underlying physics. The goal of [reduced-order modeling](@entry_id:177038) is to find a compact representation of this manifold.

The classical linear approach to this problem is **Principal Component Analysis (PCA)**. Given a collection of simulation snapshots (e.g., flux fluctuation fields) $\{x_i\}$, organized into a data matrix, PCA identifies an optimal [orthogonal basis](@entry_id:264024) for the data. This basis consists of the eigenvectors of the data's covariance matrix, $C = \mathbb{E}[xx^T]$ (assuming zero-mean data). The eigenvectors, or principal components, corresponding to the largest eigenvalues capture the directions of greatest variance in the data. By projecting the data onto the subspace spanned by the top $k$ principal components, we can achieve the best possible linear dimensionality reduction for a given reconstruction error.

**Autoencoders** provide a powerful nonlinear generalization of PCA. An autoencoder is a neural network architecture composed of two parts: an **encoder**, which maps the high-dimensional input $x$ to a low-dimensional latent representation $z$, and a **decoder**, which attempts to reconstruct the original input $\hat{x}$ from $z$. The network is trained to minimize the reconstruction error, typically the mean squared error $\mathbb{E}[\|x - \hat{x}\|_2^2]$.

The connection between autoencoders and PCA becomes explicit when we consider a simple linear autoencoder without nonlinear [activation functions](@entry_id:141784). In this case, the encoder and decoder perform [linear transformations](@entry_id:149133). The optimal linear autoencoder, which minimizes the reconstruction error for a latent dimension $k$, learns to perform a projection onto the subspace spanned by the first $k$ principal components of the data. The minimum achievable reconstruction error is precisely the sum of the "[unexplained variance](@entry_id:756309)"—that is, the sum of the eigenvalues of the covariance matrix corresponding to the dimensions that were discarded .

Let the eigenvalues of the covariance matrix $C$ be sorted in descending order, $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_n$. The total variance in the data is given by the trace of the covariance matrix, $\operatorname{tr}(C) = \sum_{i=1}^n \lambda_i = \mathbb{E}[\|x\|_2^2]$. If we use an optimal linear autoencoder (or PCA) with a $k$-dimensional latent space, the expected squared reconstruction error is the sum of the smallest $n-k$ eigenvalues:
$$
\mathbb{E}[\|x - \hat{x}\|_2^2]_{opt} = \sum_{i=k+1}^n \lambda_i
$$
This provides a direct, quantitative way to select the latent dimension $k$. For example, if we require the relative reconstruction error to be less than 5%, we must choose the smallest $k$ such that the sum of the tail-end eigenvalues is less than 0.05 of the total sum of eigenvalues . While nonlinear autoencoders can potentially discover more complex, curved manifolds and achieve lower error for the same latent dimension, this linear analysis provides a fundamental baseline and a powerful intuition for how these networks capture the essential features of physical fields.

#### Operator Learning: Mapping Between Function Spaces

While autoencoders excel at compressing and reconstructing states, a more general and powerful task is **[operator learning](@entry_id:752958)**. Here, the goal is not to represent a single field, but to learn the mapping, or operator, that transforms one function into another. In reactor physics, we are often interested in the **parameter-to-solution map**, which relates input functions, such as material property fields, to output solution functions, like the neutron flux.

For instance, consider the steady-state neutron diffusion equation on a domain $\Omega$:
$$
-\nabla \cdot \big(D(x)\,\nabla \phi(x)\big) + \Sigma_a(x)\,\phi(x) = S(x)
$$
The solution operator $\mathcal{G}$ for this equation maps the triplet of input functions $(D(x), \Sigma_a(x), S(x))$ to the unique solution function $\phi(x)$. Formally, we write $\phi = \mathcal{G}(D, \Sigma_a, S)$. A [neural operator](@entry_id:1128605) is an ML architecture designed to learn such mappings between infinite-dimensional [function spaces](@entry_id:143478) .

For such learning to be feasible, the underlying physical operator $\mathcal{G}$ must possess certain mathematical properties. Most critically, the operator should be stable or **Lipschitz continuous** on the space of admissible input functions. This means that small changes in the input functions (e.g., small perturbations in the diffusion coefficient field $D(x)$) should lead to correspondingly small changes in the output solution $\phi(x)$ . Without this continuity, any learned approximation would fail to generalize, as imperceptibly different inputs could produce wildly different outputs.

The well-posedness of the governing PDE is the foundation upon which this continuity rests. For second-order elliptic equations like the diffusion equation, the **Lax-Milgram theorem** guarantees the existence, uniqueness, and stability of a solution under specific conditions on the input [function spaces](@entry_id:143478). For example, the diffusion tensor $D(x)$ must be in $L^\infty$ and be uniformly elliptic (bounded away from zero), the absorption cross section $\Sigma_a(x)$ must be in $L^\infty$ and non-negative, and the source $S(x)$ must be in $L^2(\Omega)$. Under these physically realistic conditions, the solution operator is well-defined and continuous, mapping from a suitable space of input coefficients to a Sobolev space of solutions, such as $H^1_0(\Omega)$ for vacuum boundary conditions . This mathematical bedrock is what makes [operator learning](@entry_id:752958) a principled and viable approach for physics simulation.

#### A Case Study: The Fourier Neural Operator (FNO)

The **Fourier Neural Operator (FNO)** is a particularly effective architecture for learning solution operators, especially for problems defined on [periodic domains](@entry_id:753347). Its design is motivated by the properties of linear, constant-coefficient PDEs. An FNO layer operates by:
1. Transforming the input function to the frequency domain using a Fast Fourier Transform (FFT).
2. Applying a learned filter by performing element-wise multiplication with a complex-valued weight tensor in the Fourier domain. This step is typically restricted to a finite number of low-frequency modes.
3. Transforming the result back to the spatial domain using an inverse FFT.
These [spectral convolution](@entry_id:755163) layers are typically interleaved with simple, pointwise neural networks that apply nonlinearities.

The theoretical justification for the FNO's success lies in the spectral properties of the solution operator it aims to learn. For the diffusion equation with constant coefficients $D$ and $\Sigma_a$ on a periodic domain, the solution operator is a **Fourier multiplier**. This means it has a very simple action in the frequency domain: it multiplies the $k$-th Fourier coefficient of the source term, $\hat{s}_k$, by a factor $\lambda_k = (D|k|^2 + \Sigma_a)^{-1}$ to yield the $k$-th Fourier coefficient of the solution, $\hat{\phi}_k$ .

Critically, because this multiplier $\lambda_k$ decays to zero as the frequency $|k| \to \infty$, the solution operator is a **[compact operator](@entry_id:158224)**. A fundamental result from [functional analysis](@entry_id:146220) states that any [compact operator](@entry_id:158224) can be approximated arbitrarily well by a [finite-rank operator](@entry_id:143413). In this context, a finite-rank approximation corresponds to truncating the Fourier series to a finite number of modes and applying the exact multiplier to them. The FNO architecture is essentially a parameterized version of such a finite-rank spectral operator. By learning the weights in the Fourier domain, the FNO learns to emulate the action of the solution operator. The universal approximation property of FNOs, which guarantees their ability to approximate the solution operator uniformly on [compact sets](@entry_id:147575) of input functions, is a direct consequence of the compactness of the underlying physical operator and the FNO's ability to approximate the associated Fourier multipliers .

### Physics-Informed Neural Networks (PINNs): Solving Governing Equations

While [surrogate models](@entry_id:145436) learn from data generated by existing solvers, **Physics-Informed Neural Networks (PINNs)** represent a different paradigm: they learn to solve the governing differential equations directly. This is typically achieved without any labeled solution data, by training the network to satisfy the physical laws themselves.

#### The Core Principle: Residual-Based Loss

The central mechanism of a PINN is the formulation of a loss function based on the PDE **residual**. A neural network, $\phi_\theta(x)$, is constructed to represent the solution, taking coordinates (e.g., position $x$) as input and outputting the field value. The network's parameters, $\theta$, are the trainable [weights and biases](@entry_id:635088).

The residual, $r(x)$, is defined as the value obtained when the neural network's output is plugged into the governing differential equation. For the 1D [steady-state diffusion](@entry_id:154663) equation, $-D \phi'' + \Sigma_a \phi = Q$, the residual is:
$$
r(x) = -D \frac{d^2 \phi_\theta}{dx^2} + \Sigma_a \phi_\theta(x) - Q
$$
The key innovation enabling this is **automatic differentiation (AD)**, a computational technique implemented in all modern deep learning frameworks. AD allows for the exact and efficient computation of derivatives of the network's output with respect to its inputs (e.g., $\phi'_\theta$ and $\phi''_\theta$), which are themselves neural networks.

The training objective is to minimize the squared $L^2$-norm of this residual over the entire domain, often supplemented by terms that enforce boundary conditions. The loss function for the PDE is:
$$
\mathcal{L}_{PDE} = \int_{\Omega} r(x)^2 \, dx
$$
By driving this loss to zero, the optimizer forces the neural network $\phi_\theta(x)$ to become a close approximation of the true solution to the PDE. The integral is typically approximated by summing the squared residual over a large set of randomly sampled "collocation points" within the domain. For very simple [trial functions](@entry_id:756165), this optimization problem can even be solved analytically, providing clear insight into how minimizing the residual finds the best-fit parameters .

#### Extending to Complex Physics: The Boltzmann Transport Equation

The PINN methodology is highly flexible and extends naturally to more complex and fundamental physical models, such as the **linear Boltzmann transport equation**. This equation provides a more detailed description of particle behavior than the diffusion approximation. In one-dimensional slab geometry, the steady-state equation for the angular flux $\psi(x, \mu)$ is an integro-differential equation:
$$
\mu \frac{\partial \psi(x, \mu)}{\partial x} + \Sigma_t \psi(x, \mu) = \frac{\Sigma_s}{2} \int_{-1}^1 \psi(x, \mu') \, d\mu' + q(x)
$$
Here, $\psi$ is a function of both position $x$ and the [direction cosine](@entry_id:154300) $\mu$. A PINN, $\psi_\theta(x, \mu)$, can be trained to solve this equation by constructing a residual that incorporates all terms :
- The **streaming term** $\mu \frac{\partial \psi}{\partial x}$ is handled by applying automatic differentiation to the network's output with respect to the spatial input $x$.
- The **collision term** $\Sigma_t \psi$ is a straightforward multiplication.
- The **scattering source term**, which contains an integral over the angular variable $\mu'$, is approximated using [numerical quadrature](@entry_id:136578). At each spatial collocation point $x$, the network is evaluated at a set of quadrature angles $\{\mu_k\}$ with corresponding weights $\{w_k\}$, and the integral is computed as a weighted sum: $\int \psi_\theta(x, \mu') d\mu' \approx \sum_k w_k \psi_\theta(x, \mu_k)$.

Boundary conditions, such as vacuum conditions where there is no incoming flux ($\psi(0, \mu) = 0$ for $\mu > 0$), are enforced by adding a separate boundary loss term to the total training objective. This term penalizes non-zero values of the network's output at the boundaries for the relevant incoming directions . This demonstrates the power of the PINN framework to incorporate diverse mathematical structures—derivatives, integrals, and boundary constraints—into a unified optimization problem.

### Graph Neural Networks for Spatially Discrete Systems

Many systems in nuclear engineering, particularly the reactor core itself, possess a natural, discrete, graph-like structure. A reactor core is a lattice of fuel assemblies, where each assembly interacts primarily with its immediate neighbors. **Graph Neural Networks (GNNs)** are a class of neural networks specifically designed to operate on data with an underlying graph structure, making them a natural choice for modeling core-wide physics.

#### Constructing Physics-Informed Graphs

A crucial first step in applying GNNs is to define the [graph representation](@entry_id:274556) of the physical system. This is not an arbitrary choice but a critical modeling decision that should be guided by physical principles. For a reactor core, the graph is typically defined as follows :
- **Nodes**: Each fuel assembly is a node in the graph. The state of each node is represented by a feature vector, which can include physical properties like [uranium enrichment](@entry_id:146426), burnup, control rod insertion, and coolant conditions.
- **Edges**: Edges represent physical interactions between assemblies. The principle of **locality** dictates that edges should only connect physically adjacent assemblies, as direct interactions (e.g., [neutron leakage](@entry_id:1128700), heat transfer) occur across their shared faces. This results in a sparse adjacency matrix that mirrors the core's geometry.
- **Edge Weights**: The weights on the edges should quantify the strength of the interaction. For processes that are reciprocal, such as conduction or diffusion, the graph should be undirected, with symmetric edge weights ($w_{ij} = w_{ji}$). Furthermore, the weights should be physically meaningful. For example, when modeling inter-assembly thermal coupling, a well-chosen weight could be a dimensionless number representing the ratio of [thermal conductance](@entry_id:189019) between assemblies to the convective heat removal capacity within an assembly. This embeds physical scaling laws directly into the graph structure itself .

#### Physics-Consistent Message Passing

Once the graph is defined, the GNN learns to predict nodal quantities by passing "messages" between connected nodes. The architecture of this message-passing process can also be designed to be consistent with physical laws. Rather than using a generic GNN layer (e.g., from a standard graph convolutional network), one can derive an update rule that mimics a numerical solver for the governing PDE.

Consider the discretized [neutron diffusion equation](@entry_id:1128691) for an assembly $i$. The neutron balance requires that the net effect of leakage to/from neighbors, local absorption, and local fission sources sums to zero in a steady state. An [iterative solver](@entry_id:140727) for this system often takes the form of an update that drives this residual to zero. Such an update can be directly interpreted as a GNN [message-passing](@entry_id:751915) layer . For instance, a physically consistent update rule for the flux $\phi_i$ at node $i$ would be:
$$
\phi_i^{(t+1)} = \phi_i^{(t)} - \Delta t \left[ \sum_{j \in \mathcal{N}(i)} \text{Leakage}_{j \to i} + \text{Absorption}_i - \text{FissionSource}_i \right]
$$
In this formulation, the "message" from a neighbor $j$ to node $i$ is directly related to the physical quantity of [neutron leakage](@entry_id:1128700) between them, which is a function of their flux difference $(\phi_j^{(t)} - \phi_i^{(t)})$ and the diffusion coefficient $D_{ij}$. The central node then aggregates these leakage messages and updates its own state based on local physics (absorption and fission). This approach embeds the discretized PDE directly into the [network architecture](@entry_id:268981), creating a powerful [inductive bias](@entry_id:137419) that facilitates learning and improves generalization.

### ML in Advanced Simulation and Engineering Workflows

Beyond serving as standalone solvers or accelerators, ML models are increasingly being integrated as components within larger, more complex engineering and safety analysis workflows. This requires a rigorous understanding of their performance, limitations, and uncertainties.

#### Multi-Fidelity Modeling and Uncertainty Quantification

Quantifying the impact of uncertainties in model inputs (e.g., [nuclear cross sections](@entry_id:1128920)) on simulation outputs is critical for safety assessment. However, propagating uncertainties using high-fidelity Monte Carlo methods can be prohibitively expensive. The **Multi-Level Monte Carlo (MLMC)** method is a powerful variance-reduction technique that addresses this challenge by leveraging a hierarchy of models with varying fidelity and cost .

The MLMC estimator for an expected quantity $\mathbb{E}[Q_L]$ is built as a telescoping sum of differences between model levels:
$$
\mathbb{E}[Q_L] = \mathbb{E}[Q_0] + \sum_{\ell=1}^L \mathbb{E}[Q_\ell - Q_{\ell-1}]
$$
where level $L$ is the highest fidelity. Each term in the sum is estimated with an independent Monte Carlo simulation. The key insight is that the variance of the difference, $\mathbb{V}[Q_\ell - Q_{\ell-1}]$, decreases as the fidelity of levels $\ell$ and $\ell-1$ increases. Therefore, the expensive high-fidelity levels require far fewer samples to estimate the small correction term accurately.

ML surrogates are ideal candidates for the low-fidelity levels ($Q_0, Q_1, \dots$) in this hierarchy. Their rapid execution speed makes them extremely cheap ($C_\ell$ is small), allowing for a vast number of samples to be drawn to accurately estimate the mean of the cheapest model, $\mathbb{E}[Q_0]$. The [optimal allocation](@entry_id:635142) of computational effort across the levels to achieve a target total variance $\epsilon^2$ at minimum cost involves choosing the number of samples $N_\ell$ at each level such that:
$$
N_\ell \propto \sqrt{\frac{V_\ell}{C_\ell}}
$$
where $V_\ell = \mathbb{V}[Q_\ell - Q_{\ell-1}]$. This strategy demonstrates how to intelligently combine the speed of ML models with the accuracy of physics-based solvers to perform UQ tasks that would be intractable with either method alone .

#### Verification, Validation, and Uncertainty Quantification (VVUQ)

For ML models to be used in high-consequence applications like nuclear [reactor safety analysis](@entry_id:1130678), they must be subjected to the same rigorous **Verification, Validation, and Uncertainty Quantification (VVUQ)** framework as traditional physics models. This framework systematically assesses all sources of error and uncertainty .

- **Verification** addresses the question, "Are we solving the model equations correctly?" It focuses on quantifying [numerical errors](@entry_id:635587) arising from discretization and iterative solvers. For a simulation incorporating an ML model, this includes the error of the larger multiphysics solver into which the surrogate is embedded.

- **Validation** addresses the question, "Are we solving the right equations?" It involves comparing model predictions to real-world experimental data to quantify the **[model discrepancy](@entry_id:198101)** or **model form error**. When an ML surrogate is used, its inherent prediction error is a major component of this discrepancy. This is an **epistemic uncertainty** (due to lack of knowledge, reducible with more data or a better model) and must be carefully quantified, often resulting in a posterior distribution for the [model bias](@entry_id:184783).

- **Uncertainty Quantification (UQ)** involves propagating all known sources of uncertainty through the model to the final quantity of interest. A complete UQ budget must include:
    1.  **Aleatoric Uncertainty**: Inherent randomness in the system or data that the ML model may be trained to predict (e.g., from unresolved physics).
    2.  **Epistemic Uncertainty**: Includes the [model discrepancy](@entry_id:198101) of the ML surrogate, inferred during validation.
    3.  **Numerical Error**: The residual error from the solver, estimated during verification.
    4.  **Parameter and Scenario Uncertainty**: Uncertainties in model inputs and operating conditions.

By combining these independent sources of uncertainty, typically using the law of total variance, one can construct a final posterior predictive distribution for a key safety metric, such as the peak cladding temperature. This provides not just a single point prediction but a full probabilistic assessment, including [confidence intervals](@entry_id:142297), which is essential for robust engineering design and safety analysis . This holistic framework ensures that ML models are not treated as black boxes but as transparent, quantifiable components of a predictive engineering toolkit.