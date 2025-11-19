## Introduction
In fields from signal processing to machine learning, data is increasingly represented not on regular grids but on complex, irregular networks or graphs. Processing signals defined on these structures—such as social network activity, brain functional data, or sensor network measurements—poses a fundamental challenge: how can we adapt powerful tools like the Fourier transform, which rely on notions of frequency and [shift-invariance](@entry_id:754776), to domains that lack this regular structure? Graph Signal Processing (GSP) emerges as the theoretical framework to address this gap, providing a comprehensive methodology for analyzing and manipulating data on graphs.

This article provides a graduate-level introduction to the core principles and applications of GSP. We will explore how a meaningful concept of "frequency" can be defined on any graph, leading to a direct analogue of the Fourier transform. Across three chapters, you will build a robust understanding of this modern field. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork by introducing the graph Laplacian, defining the Graph Fourier Transform (GFT), and developing the concepts of spectral filtering and localized [graph wavelets](@entry_id:750020). The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the power of these tools in solving real-world problems, from [signal recovery](@entry_id:185977) and [compressed sensing](@entry_id:150278) on networks to modeling [diffusion processes](@entry_id:170696) and designing advanced, multi-resolution filterbanks. Finally, the **"Hands-On Practices"** chapter offers a series of guided exercises to solidify your grasp of these abstract concepts through concrete calculations on [simple graphs](@entry_id:274882). By the end, you will be equipped with the foundational knowledge to apply GSP techniques to a wide range of problems involving structured data.

## Principles and Mechanisms

In the study of signals defined on regular domains, such as time-series or images on a grid, the Fourier transform provides a canonical tool for analyzing frequency content. This transform decomposes a signal into a basis of [complex exponentials](@entry_id:198168), which are the [eigenfunctions](@entry_id:154705) of the differentiation operator. The core question for [graph signal processing](@entry_id:184205) is whether a similar concept of "frequency" and an analogous Fourier transform can be developed for signals defined on the vertices of an arbitrary graph, whose structure is irregular and lacks a simple notion of [shift-invariance](@entry_id:754776). This chapter establishes the foundational principles that answer this question, leading to the development of the Graph Fourier Transform (GFT), spectral filtering, and [graph wavelets](@entry_id:750020).

### Graph Signals and the Notion of Total Variation

Let us consider a weighted, [undirected graph](@entry_id:263035) $G = (\mathcal{V}, \mathcal{E}, W)$, where $\mathcal{V}$ is a set of $N$ vertices, $\mathcal{E}$ is the set of edges, and $W$ is a symmetric weight matrix with non-negative entries $w_{ij}$ representing the strength of the connection between vertices $i$ and $j$. A **graph signal** is a function $x: \mathcal{V} \to \mathbb{R}$, which can be represented as a vector $x \in \mathbb{R}^{N}$, where the $i$-th component $x_i$ is the value of the signal at vertex $i$.

To define frequency on a graph, we must first quantify the concept of signal variation or smoothness with respect to the underlying graph structure. Intuitively, a signal is smooth, or of "low frequency," if its values do not change much across strongly connected vertices. Conversely, a signal is oscillatory, or of "high frequency," if its values fluctuate rapidly across edges with large weights.

The central operator for quantifying this variation is the **combinatorial graph Laplacian**, $L$, defined as:

$L = D - W$

where $D$ is the diagonal **degree matrix** with entries $D_{ii} = d_i = \sum_{j=1}^{N} w_{ij}$. The Laplacian operator acts on a signal $x$ to produce a new signal $(Lx)_i = d_i x_i - \sum_{j \sim i} w_{ij} x_j = \sum_{j \sim i} w_{ij} (x_i - x_j)$, where $j \sim i$ denotes that vertices $i$ and $j$ are connected. This local operation measures the weighted difference between a signal's value at a vertex and the values at its neighbors.

To obtain a global measure of variation, we use the [quadratic form](@entry_id:153497) associated with the Laplacian, known as the **Dirichlet energy**:

$E(x) = x^{\top} L x$

This scalar quantity represents the [total variation](@entry_id:140383) of the signal $x$ over the graph. A simple but crucial derivation reveals its intuitive meaning. By expanding the [quadratic form](@entry_id:153497), we can show the following identity [@problem_id:3448874]:

$x^{\top} L x = x^{\top}(D - W)x = \sum_{i=1}^{N} d_i x_i^2 - \sum_{i,j=1}^{N} w_{ij} x_i x_j = \frac{1}{2} \sum_{i=1}^{N} \sum_{j=1}^{N} w_{ij} (x_i - x_j)^2$

This form makes it clear that the Dirichlet energy is a weighted sum of the squared differences of the signal values across all edges. A signal that is perfectly constant ($x_i = c$ for all $i$) has $x_i - x_j = 0$ for all pairs, resulting in zero Dirichlet energy—the smoothest possible signal. Any variation in the signal across an edge contributes positively to the energy. Minimizing this [energy functional](@entry_id:170311) is a common principle for smoothing a signal on a graph.

### The Graph Fourier Transform

With the Dirichlet energy established as our measure of [total variation](@entry_id:140383), we seek a basis that elegantly represents this concept. In classical signal processing, the Fourier basis diagonalizes the differentiation operator. Analogously, we seek an orthonormal basis for graph signals that diagonalizes the graph Laplacian $L$.

Since the graph is undirected, the weight matrix $W$ is symmetric, and consequently, the graph Laplacian $L$ is a real, [symmetric matrix](@entry_id:143130). The [spectral theorem](@entry_id:136620) for real [symmetric matrices](@entry_id:156259) guarantees that $L$ has a full set of $N$ real eigenvalues, $\lambda_0, \lambda_1, \dots, \lambda_{N-1}$, and a corresponding [orthonormal basis of eigenvectors](@entry_id:180262), $u_0, u_1, \dots, u_{N-1}$. We can write this [eigendecomposition](@entry_id:181333) in matrix form as:

$L = U \Lambda U^{\top}$

where $U = [u_0, u_1, \dots, u_{N-1}]$ is an [orthonormal matrix](@entry_id:169220) ($U^{\top}U = UU^{\top} = I$) whose columns are the eigenvectors, and $\Lambda = \mathrm{diag}(\lambda_0, \lambda_1, \dots, \lambda_{N-1})$ is the diagonal matrix of corresponding eigenvalues. The eigenvalues of the Laplacian are non-negative ($0 \le \lambda_0 \le \dots \le \lambda_{N-1}$) and are interpreted as the **graph frequencies**. The corresponding eigenvectors $u_k$ are the **graph Fourier modes**.

This [eigenbasis](@entry_id:151409) is precisely the basis we seek. Any graph signal $x$ can be represented as a linear combination of these modes: $x = \sum_{k=0}^{N-1} \hat{x}_k u_k$. The coefficients $\hat{x}_k$ are found by projecting the signal onto the basis vectors: $\hat{x}_k = u_k^{\top} x$. This leads to the definition of the **Graph Fourier Transform (GFT)** and its inverse [@problem_id:3448866]:

- **Forward GFT:** $\hat{x} = U^{\top} x$
- **Inverse GFT:** $x = U \hat{x}$

The vector $\hat{x}$ is the [spectral representation](@entry_id:153219) of the signal $x$. The key property of this transform is that it diagonalizes the Dirichlet energy. By substituting $x = U \hat{x}$ into the energy expression, we get:

$E(x) = (U\hat{x})^{\top} L (U\hat{x}) = \hat{x}^{\top} (U^{\top} L U) \hat{x} = \hat{x}^{\top} \Lambda \hat{x} = \sum_{k=0}^{N-1} \lambda_k \hat{x}_k^2$

This relationship is the cornerstone of [graph signal processing](@entry_id:184205). It shows that the [total variation](@entry_id:140383) of a signal is the sum of the squared magnitudes of its spectral coefficients, weighted by the corresponding graph frequencies $\lambda_k$. A signal is smooth if its energy is concentrated in the components corresponding to small eigenvalues (low frequencies).

The [eigenvalues and eigenvectors](@entry_id:138808) are also the solutions to the minimization of the **Rayleigh quotient**, $R(u) = (u^{\top} L u) / (u^{\top} u)$. The smallest eigenvalue $\lambda_0$ is the minimum value of the Rayleigh quotient, achieved by the eigenvector $u_0$. For any graph, the constant vector $\mathbf{1}$ is an eigenvector of $L$ with eigenvalue 0, since $L\mathbf{1} = (D-W)\mathbf{1} = 0$. If the graph is connected, this is the only eigenvector with eigenvalue 0, so $\lambda_0 = 0$ is a simple eigenvalue and its eigenvector $u_0 = \frac{1}{\sqrt{N}}\mathbf{1}$ represents the "DC component" of the graph. If a graph has $c$ connected components, the multiplicity of the eigenvalue 0 is $c$, and the corresponding eigenspace is spanned by vectors that are piecewise-constant on these components [@problem_id:3448866].

### Variations and Generalizations

The GFT as defined above is not the only possible formulation. Different choices of the Laplacian operator or extensions to more complex graph structures lead to important variations.

#### Normalized Laplacians and Weighted Inner Products

The eigenvectors of the combinatorial Laplacian $L$ form an orthonormal basis with respect to the standard Euclidean inner product, $\langle x, y \rangle_2 = x^{\top}y$. A closely related operator is the **symmetrically normalized Laplacian**:

$L_{\mathrm{n}} = D^{-1/2} L D^{-1/2} = I - D^{-1/2} W D^{-1/2}$

This operator is also real and symmetric, and its eigenvalues, which are typically bounded in $[0, 2]$, are often preferred for analysis as they are less dependent on node degrees. The eigenvectors of $L_{\mathrm{n}}$ also form an [orthonormal basis](@entry_id:147779). An important connection exists between the eigen-systems of $L$ and $L_{\mathrm{n}}$ [@problem_id:3448879]. Specifically, if $v_k$ is an eigenvector of $L_{\mathrm{n}}$ with eigenvalue $\lambda_k$, the vector $u_k = D^{-1/2}v_k$ is a [generalized eigenvector](@entry_id:154062) for the pair $(L, D)$ with the same eigenvalue, satisfying $Lu_k = \lambda_k D u_k$. The basis of these [generalized eigenvectors](@entry_id:152349) is not orthonormal in the standard sense, but rather with respect to a $D$-[weighted inner product](@entry_id:163877): $u_j^{\top} D u_k = \delta_{jk}$. The transformation that connects a signal's representation between these bases is the operator $D^{1/2}$. This distinction is crucial for developing consistent theories of filtering and sampling on graphs.

#### Graph Fourier Transforms for Directed Graphs

Extending Fourier analysis to [directed graphs](@entry_id:272310) presents a significant challenge because the adjacency matrix $W$ is no longer symmetric. Consequently, the associated Laplacian operator is not symmetric and is not guaranteed to have real eigenvalues or an orthogonal [eigenbasis](@entry_id:151409). Two principled approaches address this [@problem_id:3448876]:

1.  **Hermitianization:** One can construct a related **Hermitian** operator whose spectral properties can be leveraged. An example is the **magnetic Laplacian**, which encodes edge directionality as complex phases in a new Hermitian matrix. By the spectral theorem, this Hermitian operator possesses a full set of real eigenvalues and a **unitary** [eigenbasis](@entry_id:151409) $U$ (where $U^*U = I$). A GFT defined by $\hat{x} = U^*x$ is well-behaved: it is perfectly invertible ($x = U\hat{x}$), its basis is complete and orthonormal, and it conserves Euclidean energy ($\|x\|_2^2 = \|\hat{x}\|_2^2$).

2.  **Jordan-based GFT:** A more direct approach is to use the **Jordan normal form** of the non-symmetric Laplacian, $L = V J V^{-1}$. The columns of the invertible matrix $V$ consist of *generalized* eigenvectors, which still form a complete basis for $\mathbb{C}^N$. However, this basis is generally **not orthogonal**. As a result, a GFT defined via $\hat{x} = V^{-1}x$ does not conserve Euclidean energy. While a Parseval-like identity can be recovered using a weighted norm, the lack of orthogonality complicates the interpretation and use of this transform in many signal processing applications.

For these reasons, approaches based on Hermitianization are often preferred for developing a practical GFT for [directed graphs](@entry_id:272310).

### Spectral Graph Filtering

One of the most powerful applications of the GFT is the ability to perform filtering directly in the graph [spectral domain](@entry_id:755169). Analogous to classical filtering, a **spectral graph filter** modifies a signal by amplifying or attenuating its frequency components. A filter is defined by a scalar function $g: [0, \infty) \to \mathbb{R}$, called the filter kernel or frequency response. Applying the filter to a signal $x$ is defined through [functional calculus](@entry_id:138358) on the Laplacian:

$y = g(L) x \triangleq U g(\Lambda) U^{\top} x$

where $g(\Lambda)$ is the [diagonal matrix](@entry_id:637782) with entries $g(\lambda_k)$. By transforming this equation into the GFT domain, we obtain the fundamental filtering principle [@problem_id:3448913]:

$\hat{y}_k = g(\lambda_k) \hat{x}_k$

This shows that spectral [graph filtering](@entry_id:193076) is simply a point-wise multiplication of the signal's graph Fourier coefficients by the filter's [frequency response](@entry_id:183149). For instance, a **low-pass filter** would have a kernel $g(\lambda)$ that is large for small $\lambda$ and small for large $\lambda$, thus attenuating the high-frequency components and resulting in a smoother output signal. The energy of the output signal is given by $\|y\|_2^2 = \sum_k |g(\lambda_k)|^2 |\hat{x}_k|^2$, explicitly showing how the filter reshapes the signal's energy distribution across the spectrum. A filter $g(L)$ is invertible if and only if its response $g(\lambda_k)$ is non-zero for all eigenvalues $\lambda_k$.

### Signal Priors for Regularization: Smoothness versus Sparsity

In many applications, such as [signal denoising](@entry_id:275354), compression, or reconstruction from partial samples, we must solve an inverse problem. These problems are often ill-posed and require a regularization term, or a **prior**, that encodes expected properties of the signal. The framework of [graph signal processing](@entry_id:184205) provides two powerful and widely used priors for graph signals [@problem_id:3448915].

1.  **Quadratic Smoothness Prior ($L_2$ Regularization):** The Dirichlet energy, $J_2(x) = x^{\top}L x$, serves as a natural prior for signals that are expected to be **globally smooth**. This prior penalizes all non-zero differences across edges, promoting solutions where neighboring vertices have similar values. From a Bayesian perspective, it corresponds to a Gaussian Markov Random Field (GMRF) model with a precision matrix proportional to $L$ [@problem_id:3448915]. This prior is highly effective for signals that are approximately **bandlimited** (i.e., their GFT coefficients are concentrated at low frequencies). However, its quadratic nature tends to heavily penalize and thus blur sharp discontinuities.

2.  **Graph Total Variation ($L_1$ Regularization):** An alternative prior is the **Graph Total Variation (GTV)**, which is the $\ell_1$-norm of the signal differences across edges:

    $J_1(x) = \mathrm{GTV}(x) = \sum_{(i,j) \in \mathcal{E}} w_{ij} |x_i - x_j| = \|Bx\|_{1,w}$

    where $B$ is the graph [incidence matrix](@entry_id:263683) [@problem_id:3448871]. The use of the $\ell_1$-norm promotes **sparsity** in the vector of edge differences. This means it encourages many differences $(x_i - x_j)$ to be exactly zero, while allowing a few large differences to exist with a penalty that grows linearly, not quadratically. This prior is therefore ideal for signals that are expected to be **piecewise-constant**, such as the indicator vectors of communities in a network. It excels at preserving sharp edges while enforcing smoothness within regions. The choice between the $L_2$ and $L_1$ smoothness priors is fundamental and depends entirely on the assumed model for the underlying signal.

### Localized Analysis: Graph Wavelets

The Fourier modes $u_k$ are [eigenfunctions](@entry_id:154705) of the global operator $L$ and are therefore typically supported across the entire graph. This makes the GFT unsuitable for analyzing signals whose frequency content varies locally. To achieve simultaneous localization in both the vertex and spectral domains, we can construct **[graph wavelets](@entry_id:750020)**.

Spectral [graph wavelets](@entry_id:750020) are designed as band-pass filters applied to a signal localized at a single vertex. A **wavelet atom** $\psi_{s,i}$ localized at vertex $i$ and at a scale $s$ is defined as [@problem_id:3448880]:

$\psi_{s,i} = h(sL) \delta_i$

where $\delta_i$ is the Kronecker delta signal (a value of 1 at vertex $i$ and 0 elsewhere) and $h$ is a [band-pass filter](@entry_id:271673) kernel. The **scale parameter** $s$ dilates the kernel in the frequency domain, tuning the wavelet to different frequency bands. This leads to the characteristic **graph uncertainty principle**:
-   **Small scales $s$** correspond to analysis at high frequencies. The [wavelet](@entry_id:204342) kernel $h(s\lambda)$ is wide in the spectrum, which corresponds to a [wavelet](@entry_id:204342) atom $\psi_{s,i}$ that is well-localized (concentrated) around vertex $i$.
-   **Large scales $s$** correspond to analysis at low frequencies. The kernel is narrow in the spectrum, leading to a [wavelet](@entry_id:204342) atom that is spread out across many vertices (poorly localized).

The structure of the graph itself mediates this trade-off. For some graphs, like the [star graph](@entry_id:271558), the distinction between vertex and spectral localization can become blurred. The **[mutual coherence](@entry_id:188177)** between the vertex basis and the GFT basis quantifies this relationship; a high coherence, as found in the [star graph](@entry_id:271558), implies a weak uncertainty principle, where it is possible for signals to be sparse in both domains simultaneously [@problem_id:3448919].

For a wavelet transform to be useful, it must be stably invertible. This is ensured if the collection of all wavelet atoms and a low-pass **scaling function** $\phi_i = g(L)\delta_i$ (which captures the DC and low-frequency content missed by the [wavelets](@entry_id:636492)) form a mathematical structure known as a **frame**. This requires the filter kernels $g$ and $h$ to "tile" the [graph spectrum](@entry_id:261508) appropriately, satisfying the frame condition for some constants $0  A \le B  \infty$ [@problem_id:3448880]:

$A \le |g(\lambda_k)|^2 + \sum_{m} |h(s_m \lambda_k)|^2 \le B \quad \text{for all } k$

The ratio of the frame bounds, $B/A$, is related to the condition number of the frame operator and controls the numerical stability of the transform and its robustness to noise. For a tight frame where $A=B$, the transform behaves like a [unitary operator](@entry_id:155165), offering perfect stability [@problem_id:3448911].