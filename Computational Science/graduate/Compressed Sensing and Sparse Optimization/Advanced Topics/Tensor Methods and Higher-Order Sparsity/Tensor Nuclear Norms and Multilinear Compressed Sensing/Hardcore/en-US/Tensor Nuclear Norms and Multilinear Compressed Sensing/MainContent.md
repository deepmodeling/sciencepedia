## Introduction

The challenge of reconstructing high-dimensional signals from incomplete information is a central theme in modern data science, with applications ranging from [medical imaging](@entry_id:269649) to video processing. While compressed sensing for vectors is well understood, extending these ideas to higher-order data arrays, or tensors, introduces significant new complexities. The core problem lies in the fact that, unlike matrices, tensors do not have a single, universal definition of rank. This ambiguity creates a knowledge gap, necessitating a richer framework to define, model, and recover "simple" or [low-rank tensor](@entry_id:751518) structures from limited measurements.

This article provides a comprehensive exploration of this advanced topic. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork by introducing key [low-rank tensor](@entry_id:751518) models—such as the CP, Tucker, and tubal rank decompositions—and their powerful convex surrogates, the [tensor nuclear norms](@entry_id:755857). We will investigate the mathematical guarantees, like the Tensor Restricted Isometry Property, that ensure reliable recovery. Subsequently, **Applications and Interdisciplinary Connections** will bridge theory and practice, demonstrating how selecting the appropriate tensor norm can solve complex problems in dynamic imaging and quantitative sensing by aligning the mathematical model with the data's physical structure. Finally, **Hands-On Practices** will offer guided problems to solidify your understanding and apply these concepts to practical design scenarios.

## Principles and Mechanisms

The recovery of structured signals from incomplete or corrupted measurements forms the cornerstone of modern signal processing and machine learning. While the principles of [compressed sensing](@entry_id:150278) for sparse vectors are well-established, their extension to higher-order data arrays, or tensors, introduces significant complexity and richness. The challenge lies in defining what constitutes a "simple" or "low-dimensional" tensor. Unlike matrices, for which rank provides a single, unambiguous measure of complexity, tensors possess multiple, non-equivalent notions of rank. This multiplicity gives rise to a diverse array of structural models, convex regularizers, and [recovery guarantees](@entry_id:754159), each tailored to a specific type of underlying tensor structure. This chapter delineates the fundamental principles and mechanisms governing [multilinear compressed sensing](@entry_id:752294), exploring the interplay between tensor decompositions, their corresponding convex surrogates, and the conditions that ensure reliable recovery.

### Models of Low-Rank Tensor Structure

The first step in any recovery problem is to posit a structural model for the signal of interest. For tensors, the primary models are based on low-rank decompositions, which express a high-dimensional object in terms of a smaller number of constituent components.

#### Canonical Polyadic Decomposition and CP-Rank

The most direct generalization of [matrix rank](@entry_id:153017) is the **Canonical Polyadic (CP) decomposition**. An $N$-way tensor $\mathcal{X} \in \mathbb{R}^{d_1 \times \cdots \times d_N}$ is a rank-1 tensor if it can be written as the outer product of $N$ vectors: $\mathcal{X} = u^{(1)} \otimes u^{(2)} \otimes \cdots \otimes u^{(N)}$, where $u^{(n)} \in \mathbb{R}^{d_n}$. The **CP-rank** of a general tensor $\mathcal{X}$, denoted $r_{\mathrm{CP}}(\mathcal{X})$, is the smallest integer $R$ such that $\mathcal{X}$ can be expressed as a sum of $R$ rank-1 tensors:
$$
\mathcal{X} = \sum_{i=1}^{R} \lambda_i \, u_i^{(1)} \otimes u_i^{(2)} \otimes \cdots \otimes u_i^{(N)}
$$
While conceptually simple, the CP-rank is NP-hard to compute in general, and the set of tensors with CP-rank at most $R$ is not closed. These properties make it a difficult constraint to handle directly in optimization problems.

#### Tucker Decomposition and Multilinear Rank

A more flexible and computationally tractable model is the **Tucker decomposition**. This represents a tensor $\mathcal{X}$ as a dense, smaller **core tensor** $\mathcal{G} \in \mathbb{R}^{r_1 \times \cdots \times r_N}$ that is transformed by a set of **factor matrices** $U^{(n)} \in \mathbb{R}^{d_n \times r_n}$ for $n=1, \dots, N$. The operation is expressed using the mode-$n$ product:
$$
\mathcal{X} = \mathcal{G} \times_1 U^{(1)} \times_2 U^{(2)} \cdots \times_N U^{(N)}
$$
The tuple $\mathbf{r} = (r_1, r_2, \ldots, r_N)$ is known as the **[multilinear rank](@entry_id:195814)** or Tucker rank of the tensor. Each $r_n$ corresponds to the rank of the mode-$n$ **unfolding** (or [matricization](@entry_id:751739)) of the tensor, $\mathcal{X}_{(n)}$, which is a matrix of size $d_n \times (\prod_{j \neq n} d_j)$. The factor matrices $U^{(n)}$ are typically chosen to have orthonormal columns, spanning the [dominant mode](@entry_id:263463)-$n$ subspaces of the tensor. This model is more general than the CP decomposition in the sense that a single tensor can have a low [multilinear rank](@entry_id:195814) but a high CP-rank.

#### Tubal Rank and the Tensor SVD (t-SVD)

For third-order tensors, a powerful algebraic framework has emerged based on a novel **t-product** operation. For tensors $\mathcal{X} \in \mathbb{R}^{n_1 \times n_2 \times n_3}$ and $\mathcal{Y} \in \mathbb{R}^{n_2 \times n_4 \times n_3}$, the t-product $\mathcal{Z} = \mathcal{X} \ast \mathcal{Y}$ is defined to be consistent with [circular convolution](@entry_id:147898) along the third mode (the "tubes"). This operation has a remarkable property: it becomes standard [matrix multiplication](@entry_id:156035) in the Fourier domain. If we apply the Discrete Fourier Transform (DFT) to each tube of the tensors, obtaining Fourier-domain tensors $\widehat{\mathcal{X}}$ and $\widehat{\mathcal{Y}}$, the t-product is equivalent to performing [matrix multiplication](@entry_id:156035) on each of the $n_3$ frontal slices :
$$
\widehat{\mathcal{Z}}(:,:,k) = \widehat{\mathcal{X}}(:,:,k) \widehat{\mathcal{Y}}(:,:,k) \quad \text{for } k=1, \ldots, n_3
$$
The result $\mathcal{Z}$ is then recovered via an inverse DFT along the tubes. This algebraic structure leads to the **Tensor Singular Value Decomposition (t-SVD)**, which factorizes a tensor $\mathcal{X}$ as $\mathcal{X} = \mathcal{U} \ast \mathcal{S} \ast \mathcal{V}^\top$. Here, $\mathcal{U}$ and $\mathcal{V}$ are orthogonal tensors (e.g., $\mathcal{U}^\top \ast \mathcal{U}$ is the identity tensor), and $\mathcal{S}$ is an **f-diagonal** tensor, meaning each of its frontal slices in the Fourier domain is a diagonal matrix . The number of non-zero [singular value](@entry_id:171660) tubes in $\mathcal{S}$ defines the **tubal rank** of the tensor. This framework effectively transforms the tensor problem into a collection of independent matrix problems in the Fourier domain.

### Convex Surrogates for Tensor Rank

The non-convexity and [computational hardness](@entry_id:272309) associated with [tensor rank](@entry_id:266558) motivate the use of convex surrogates, analogous to the matrix nuclear norm. The general strategy is to find a norm that acts as the tightest [convex relaxation](@entry_id:168116) of the rank function. The framework of **atomic norms** provides a systematic way to construct such surrogates.

An [atomic norm](@entry_id:746563) is defined with respect to a set of elementary "atoms" $\mathcal{A}$. The norm of a signal $\mathcal{X}$, denoted $\|\mathcal{X}\|_{\mathcal{A}}$, is the gauge of the [convex hull](@entry_id:262864) of the atomic set, which can be written as:
$$
\|\mathcal{X}\|_{\mathcal{A}} = \inf \left\{ \sum_{i} |c_i| : \mathcal{X} = \sum_{i} c_i a_i, \ a_i \in \mathcal{A} \right\}
$$
This finds the decomposition of $\mathcal{X}$ into atoms that has the minimum $\ell_1$ norm of coefficients. A key result from convex analysis is that the [atomic norm](@entry_id:746563) $\| \cdot \|_{\mathcal{A}}$ is the convex envelope of the corresponding rank function (which counts the minimum number of atoms to represent a signal) on the [unit ball](@entry_id:142558) of the [dual norm](@entry_id:263611), $\| \cdot \|_{\mathcal{A}}^\star$.

#### The Atomic Norm for CP-Rank

To promote low CP-rank, we define the atoms as the set of all rank-1 tensors with unit-norm factors. This leads to the [atomic norm](@entry_id:746563) for CP-rank, often simply called the **[tensor nuclear norm](@entry_id:755856)** in this context . Its [dual norm](@entry_id:263611), $\| \mathcal{X} \|_{\mathcal{A}}^\star = \sup_{a \in \mathcal{A}} \langle \mathcal{X}, a \rangle$, is the **multilinear spectral norm**, which measures the maximum output of the tensor when viewed as a multilinear form acting on unit-norm vectors. The [atomic norm](@entry_id:746563) $\| \mathcal{X} \|_{\mathcal{A}}$ is then the convex envelope of the CP-rank on the [unit ball](@entry_id:142558) of this multilinear [spectral norm](@entry_id:143091).

#### The Overlapped Nuclear Norm for Tucker Rank

To encourage low [multilinear rank](@entry_id:195814) $\mathbf{r} = (r_1, \ldots, r_N)$, a widely used regularizer is the sum of the matrix nuclear norms of the unfoldings:
$$
\|\mathcal{X}\|_{\text{sum-*}} = \sum_{n=1}^{N} \lambda_n \|\mathcal{X}_{(n)}\|_*
$$
where $\|\cdot\|_*$ is the matrix nuclear norm and $\lambda_n$ are positive weights. This norm, sometimes called the **overlapped [nuclear norm](@entry_id:195543)**, promotes low rank in all matricizations simultaneously. It is a powerful and flexible regularizer, though as we will see, its performance can depend heavily on the tensor's dimensions and the choice of weights.

#### The Tubal Tensor Nuclear Norm (t-TNN)

Within the t-SVD framework, the natural convex surrogate for tubal rank is the **Tubal Tensor Nuclear Norm (t-TNN)**. It is defined as the sum of the singular values of the tensor, which, thanks to the properties of the t-product, can be computed as the average of the matrix nuclear norms of the frontal slices in the Fourier domain :
$$
\|\mathcal{X}\|_{\text{t-TNN}} = \frac{1}{n_3} \sum_{k=1}^{n_3} \|\widehat{\mathcal{X}}(:,:,k)\|_*
$$
This regularizer leverages the decoupling property of the DFT, effectively regularizing a set of independent matrix problems.

### Guarantees for Tensor Recovery

With a convex surrogate $f(\mathcal{X})$ in hand, a common approach to recover a tensor $\mathcal{X}_\star$ from measurements $\mathbf{y} = \mathcal{A}(\mathcal{X}_\star) + \mathbf{w}$ is to solve a [constrained optimization](@entry_id:145264) problem, such as:
$$
\widehat{\mathcal{X}} = \arg\min_{\mathcal{X}} f(\mathcal{X}) \quad \text{subject to} \quad \|\mathcal{A}(\mathcal{X}) - \mathbf{y}\|_2 \le \epsilon
$$
where $\epsilon$ is a bound on the noise level. The central question is: under what conditions on the measurement operator $\mathcal{A}$ does the solution $\widehat{\mathcal{X}}$ accurately approximate $\mathcal{X}_\star$?

#### The Tensor Restricted Isometry Property and Stable Recovery

For generic linear operators $\mathcal{A}$ (e.g., with i.i.d. Gaussian entries), the key property is the **Tensor Restricted Isometry Property (TRIP)**. It generalizes the matrix RIP and asserts that the operator $\mathcal{A}$ approximately preserves the Frobenius norm of all tensors within a specific set of low-rank structures. For instance, for the set $\mathcal{M}_{\mathbf{r}}$ of tensors with [multilinear rank](@entry_id:195814) at most $\mathbf{r}$, the TRIP constant $\delta_{\mathbf{r}}$ is the smallest $\delta$ such that for all $\mathcal{X} \in \mathcal{M}_{\mathbf{r}}$ :
$$
(1 - \delta) \|\mathcal{X}\|_F^2 \le \|\mathcal{A}(\mathcal{X})\|_2^2 \le (1 + \delta) \|\mathcal{X}\|_F^2
$$
A crucial feature of this property is its invariance under multilinear orthogonal transformations. Since applying orthogonal factor matrices to a tensor preserves both its Frobenius norm and its [multilinear rank](@entry_id:195814), the TRIP of an operator $\mathcal{A}$ is identical to that of an operator $\mathcal{A} \circ \mathcal{Q}$, where $\mathcal{Q}$ is any such [orthogonal transformation](@entry_id:155650) .

If an operator satisfies a TRIP-like condition over the set of possible error vectors (the descent cone), we can establish robust [recovery guarantees](@entry_id:754159). Consider the recovery of a tensor $\mathcal{X}_\star$ using the overlapped nuclear norm in the presence of [adversarial noise](@entry_id:746323) $\|\mathbf{w}\|_2 \le \epsilon$. The error $\mathcal{H} = \widehat{\mathcal{X}} - \mathcal{X}_\star$ must lie in the descent cone of the norm at $\mathcal{X}_\star$. By combining the optimality condition with the feasibility of both $\widehat{\mathcal{X}}$ and $\mathcal{X}_\star$, we can bound $\|\mathcal{A}(\mathcal{H})\|_2 \le 2\epsilon$. If $\mathcal{A}$ satisfies a restricted [strong convexity](@entry_id:637898) condition, $(1-\delta)\|\mathcal{H}\|_F^2 \le \|\mathcal{A}(\mathcal{H})\|_2^2$, a direct chain of inequalities yields a powerful stability bound :
$$
\|\widehat{\mathcal{X}} - \mathcal{X}_\star\|_F \le \frac{2\epsilon}{\sqrt{1-\delta}}
$$
This result demonstrates that if the measurement operator is well-behaved on the set of low-rank tensors (i.e., $\delta$ is not too close to 1), then the reconstruction error is bounded proportionally to the noise level.

#### Incoherence and Random Sampling

In many practical applications, such as image completion or [recommender systems](@entry_id:172804), the measurement operator corresponds to sampling a small subset of the tensor's entries. In this scenario, the TRIP is not a suitable analytical tool. Instead, [recovery guarantees](@entry_id:754159) depend on the interplay between the tensor's structure and the sampling process. Two key properties emerge: **incoherence** and **spikiness**.

The **mode-wise incoherence**, $\mu_n$, measures how "spread out" the basis vectors of the mode-$n$ subspace (the columns of $U^{(n)}$ in a Tucker decomposition) are across the standard coordinate axes. For a factor matrix $U^{(n)} \in \mathbb{R}^{d_n \times r_n}$ with orthonormal columns, it is defined as :
$$
\mu_n \triangleq \frac{d_n}{r_n} \max_{i \in \{1,\dots,d_n\}} \| (U^{(n)})_{i,:} \|_2^2
$$
where $(U^{(n)})_{i,:}$ is the $i$-th row of $U^{(n)}$. This parameter ranges from $1$ (for a "flat" or maximally incoherent subspace) to $d_n/r_n$ (for a subspace aligned with a single coordinate). Low incoherence (small $\mu_n$) is desirable, as it ensures that all entries of the tensor carry a reasonable amount of information about the underlying subspace, making it easier to recover from random samples.

The **spikiness**, $\alpha$, measures how concentrated the tensor's energy is in a few entries. It is defined as the ratio of the tensor's maximum entry magnitude to its average entry magnitude :
$$
\alpha \triangleq \frac{\sqrt{d_1 \cdots d_N} \, \|\mathcal{X}\|_\infty}{\|\mathcal{X}\|_F}
$$
This parameter ranges from $1$ (for a "flat" tensor with equal-magnitude entries) to $\sqrt{d_1 \cdots d_N}$ (for a tensor with a single non-zero entry). Even if a tensor has very low rank, if it is extremely spiky, uniform random sampling will likely miss the few informative entries. Therefore, successful recovery requires not only low rank and low incoherence, but also that the tensor is not overly spiky (i.e., $\alpha$ is bounded by a moderate constant) .

### Quantitative Performance Analysis

The principles described above can be sharpened into precise, quantitative predictions about the performance of tensor recovery algorithms.

#### Fundamental Error Limits: A Minimax Perspective

A fundamental question is: what is the best possible recovery error achievable by *any* algorithm, given a certain number of measurements and noise level? For Gaussian measurement models, this minimax error can be calculated with high precision. For the canonical problem of recovering a rank-1 CP tensor $\mathcal{X}^\star \in \mathbb{R}^{d_1 \times d_2 \times d_3}$ from $m$ noisy measurements, the leading-order minimax [mean-squared error](@entry_id:175403) is given by :
$$
\inf_{\widehat{\mathcal{X}}} \sup_{\mathcal{X}^\star} \mathbb{E} \left[ \|\widehat{\mathcal{X}} - \mathcal{X}^\star\|_F^2 \right] \approx \frac{\sigma^2}{m} (d_1 + d_2 + d_3 - 2)
$$
This elegant result reveals that the error scales with the noise variance $\sigma^2$, inversely with the number of measurements $m$, and proportionally to the intrinsic degrees of freedom of a rank-1 tensor, which is $(d_1-1) + (d_2-1) + (d_3-1) + 1 = d_1 + d_2 + d_3 - 2$. This quantity, the dimension of the tangent space to the manifold of rank-1 tensors, serves as the [statistical dimension](@entry_id:755390) of the recovery problem.

#### Sample Complexity and the Geometry of Recovery

The number of measurements $m$ required for successful recovery—the [sample complexity](@entry_id:636538)—depends critically on the geometry of the chosen convex regularizer. Different norms trace different paths toward the low-rank solution, inducing descent cones with varying sizes. The [statistical dimension](@entry_id:755390) of the descent cone provides a sharp estimate for the [sample complexity](@entry_id:636538).

A compelling example arises when comparing the overlapped [nuclear norm](@entry_id:195543) and the t-TNN for recovering a cubic tensor $\mathcal{X} \in \mathbb{R}^{n \times n \times n}$ with [multilinear rank](@entry_id:195814) $(r,r,r)$ and tubal rank $r$. The overlapped norm operates on three highly unbalanced unfoldings of size $n \times n^2$. In contrast, the t-TNN, by virtue of the DFT, operates on $n$ independent, well-conditioned square matrix problems of size $n \times n$. Geometrically, the latter approach is far more efficient. The total [statistical dimension](@entry_id:755390) for the t-TNN is the sum of dimensions for the $n$ matrix problems, leading to a [sample complexity](@entry_id:636538) of roughly $m_{\text{t-TNN}} \approx n \cdot r(2n-r) \approx 2n^2r$. The overlapped norm induces a much broader descent cone, requiring significantly more measurements, with a [sample complexity](@entry_id:636538) scaling closer to $m_{\text{over}} \approx 3r(n^2+n) \approx 3n^2r$ . This illustrates a deep principle: aligning the convex regularizer with the true algebraic structure of the signal can lead to dramatic gains in [statistical efficiency](@entry_id:164796).

Finally, it is crucial to recognize the inherent **anisotropy** of tensor recovery. Unlike vectors or matrices, where permuting indices is often a trivial symmetry, permuting the modes of a tensor can fundamentally alter the recovery problem. Consider the [sample complexity](@entry_id:636538) of recovering a tensor with the weighted overlapped [nuclear norm](@entry_id:195543). A sufficient number of samples can be shown to scale with a term like $\sum_{k=1}^3 \lambda_k^2 \mu_k^{\text{eff}} r_k (d_k + d_{-k})$, where $d_{-k} = \prod_{j \neq k} d_j$ and $\mu_k^{\text{eff}}$ is an effective incoherence parameter for the $k$-th unfolding. Because the dimensions $d_k$, ranks $r_k$, and incoherences $\mu_k$ are specific to each mode, permuting the modes changes the alignment of these parameters with the weights $\lambda_k$, which can drastically change the overall [sample complexity](@entry_id:636538) . This highlights that a "one-size-fits-all" approach to tensor problems is insufficient; an effective strategy must be sensitive to the unique, anisotropic characteristics of each tensor mode.