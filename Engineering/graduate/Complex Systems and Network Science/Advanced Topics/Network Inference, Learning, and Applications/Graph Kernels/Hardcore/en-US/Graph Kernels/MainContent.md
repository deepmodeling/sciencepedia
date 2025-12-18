## Introduction
In an era dominated by network data, from molecular structures in drug discovery to social networks and brain connectomes, the ability to analyze and compare entire graphs is of paramount importance. Traditional machine learning algorithms, such as Support Vector Machines (SVMs), are designed for data represented as fixed-length vectors, creating a fundamental gap when faced with the complex, non-Euclidean nature of graphs. Graph kernels provide a powerful and theoretically elegant solution to this problem, acting as a bridge by defining a similarity function between pairs of graphs. This allows us to leverage the full power of kernel-based learning methods directly on graph-[structured data](@entry_id:914605). This article offers a comprehensive exploration of graph kernels. We will begin in "Principles and Mechanisms" by delving into the mathematical foundations and design patterns that make these methods work. Next, in "Applications and Interdisciplinary Connections," we will survey the broad utility of graph kernels across diverse machine learning tasks and scientific fields. Finally, "Hands-On Practices" will provide practical exercises to solidify your understanding of how to implement and interpret these powerful tools.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms that underpin graph kernels. We will begin by establishing the mathematical definition of a kernel and its connection to feature spaces, before exploring the crucial principle of [isomorphism](@entry_id:137127) invariance. We will then survey a general framework for designing kernels on graphs, the R-convolution, and examine several major families of graph kernels, including Random Walk, Shortest-Path, and Weisfeiler-Lehman kernels. Finally, we will discuss the theoretical concepts of [expressivity](@entry_id:271569) and universality, which characterize the power and limitations of these methods.

### Defining Graph Kernels: The Mathematical Foundation

At its most intuitive level, a **graph kernel** $k(G, H)$ is a function that measures the similarity between two graphs, $G$ and $H$. However, for a function to be a valid kernel in the context of [kernel methods](@entry_id:276706) (such as Support Vector Machines), it must satisfy specific mathematical properties. The central property is that of being **positive semidefinite (PSD)**.

A function $k: \mathcal{G} \times \mathcal{G} \to \mathbb{R}$ on a collection of graphs $\mathcal{G}$ is a valid kernel if it is **symmetric**, meaning $k(G, H) = k(H, G)$ for all graphs $G, H \in \mathcal{G}$, and **positive semidefinite**. The PSD property is defined with respect to any finite sample of graphs $\{G_1, G_2, \dots, G_n\} \subset \mathcal{G}$. For such a sample, we can construct a **Gram matrix** $K \in \mathbb{R}^{n \times n}$, where each entry is given by $K_{ij} = k(G_i, G_j)$. The function $k$ is PSD if and only if the Gram matrix $K$ is positive semidefinite for any such sample.

A symmetric matrix $K$ is positive semidefinite if for any non-[zero vector](@entry_id:156189) $c \in \mathbb{R}^n$, the [quadratic form](@entry_id:153497) $c^\top K c = \sum_{i=1}^n \sum_{j=1}^n c_i c_j K_{ij}$ is non-negative ($c^\top K c \ge 0$). An equivalent and often more intuitive condition is that all eigenvalues of the Gram matrix $K$ must be non-negative. 

A stricter condition is that a kernel be **strictly positive definite (PD)**. This requires the Gram matrix $K$ to be strictly positive definite for any sample of *pairwise distinct* graphs. This means that for any non-zero vector $c$, the quadratic form $c^\top K c$ is strictly positive ($c^\top K c > 0$), or equivalently, all eigenvalues of $K$ are strictly positive. The restriction to distinct graphs is critical; if a sample contains duplicate graphs, say $G_i = G_j$ for $i \neq j$, the $i$-th and $j$-th rows of the Gram matrix will be identical. Such a matrix is singular, must have at least one zero eigenvalue, and therefore cannot be strictly [positive definite](@entry_id:149459). 

An alternative and powerful perspective defines a kernel through a **[feature map](@entry_id:634540)**. A function $k(G, H)$ is a PSD kernel if and only if there exists a mapping $\phi$ from the space of graphs $\mathcal{G}$ to an [inner product space](@entry_id:138414) (a Hilbert space) $\mathcal{H}$ such that the kernel value is the inner product of the feature representations:

$k(G, H) = \langle \phi(G), \phi(H) \rangle_{\mathcal{H}}$

This is a profoundly important equivalence. It guarantees that any function constructed as an inner product of feature vectors is a valid PSD kernel. This "kernel trick" is the basis for most practical kernel designs: one focuses on engineering a meaningful [feature map](@entry_id:634540) $\phi(G)$, and the PSD property of the resulting kernel $k$ follows automatically.

This modern definition of a PSD kernel is underpinned by the **Moore-Aronszajn theorem**. This theorem states that for any non-[empty set](@entry_id:261946) $\mathcal{G}$ and any symmetric, positive semidefinite function $k$ on $\mathcal{G} \times \mathcal{G}$, there exists a unique **Reproducing Kernel Hilbert Space (RKHS)** $\mathcal{H}_k$ of functions on $\mathcal{G}$ for which $k$ is the [reproducing kernel](@entry_id:262515). This theorem is extremely general and requires no assumptions about the structure of the domain $\mathcal{G}$ (such as compactness) or the continuity of the kernel. This is why it provides the theoretical justification for most graph kernels used in practice, which operate on the infinite, [discrete space](@entry_id:155685) of all finite graphs. This stands in contrast to the more famous **Mercer's theorem**, which provides a [spectral decomposition](@entry_id:148809) for kernels but requires strong assumptions, namely that the domain is compact and the kernel is continuous—conditions that are rarely met in the context of graph machine learning. 

### The Invariance Principle: Kernels on Unlabeled Graphs

In many scientific applications, graphs represent entities where the specific identities (or labels) of the nodes are arbitrary. For instance, in comparing the structures of two molecules, we care about the pattern of atomic bonds, not the arbitrary indices assigned to the atoms in a data file. Two graphs that are structurally identical but have different node labelings are called **isomorphic**.

A graph property is considered an **[isomorphism](@entry_id:137127) invariant** if its value is the same for all graphs in an [isomorphism](@entry_id:137127) class. Examples of simple invariants include the number of vertices, the number of edges, and the [degree sequence](@entry_id:267850). For a graph kernel to be a meaningful measure of structural similarity on unlabeled graphs, it must also be an [isomorphism](@entry_id:137127) invariant. That is, if $G \cong G'$ and $H \cong H'$, a well-defined kernel must satisfy $k(G, H) = k(G', H')$. If this condition were not met, the kernel's value would depend on the arbitrary labeling of the nodes, not the intrinsic structure of the graphs. This means the kernel must be a function of the [isomorphism classes](@entry_id:147854) of the graphs, not the specific labeled instances. 

The most common strategy to ensure a kernel is [isomorphism](@entry_id:137127)-invariant is to design an **invariant [feature map](@entry_id:634540)** $\phi$. If the [feature map](@entry_id:634540) assigns the same vector to all [isomorphic graphs](@entry_id:271870), i.e., $G \cong G' \implies \phi(G) = \phi(G')$, then the resulting kernel $k(G, H) = \langle \phi(G), \phi(H) \rangle$ will automatically be isomorphism-invariant. 

There are two primary mechanisms for achieving this:
1.  **Aggregation of Local Features:** A powerful and general approach is to first compute features for local substructures within the graph (e.g., for each node and its neighborhood) and then aggregate these features using a permutation-invariant operator, such as a sum or by constructing a histogram. Since an isomorphism only permutes the nodes, the *multiset* of local features is itself an invariant. The aggregation step converts this multiset into a single, fixed-size [feature vector](@entry_id:920515) for the entire graph. 
2.  **Use of Canonical Invariants:** One can directly use features that are known to be [isomorphism invariants](@entry_id:141089). A classic example is the **[graph spectrum](@entry_id:261508)**, which is the multiset of eigenvalues of the graph's adjacency or Laplacian matrix. Isomorphic graphs have identical adjacency matrices up to a permutation of rows and columns ($A_2 = P^\top A_1 P$), which implies they are [similar matrices](@entry_id:155833) and thus have the same eigenvalues. A feature vector consisting of the sorted [eigenvalues of a graph](@entry_id:275622) is therefore an isomorphism invariant. A kernel defined as the inner product of such spectral feature vectors is guaranteed to be both PSD and isomorphism-invariant. 

### A General Recipe: R-Convolution Kernels

Haussler's **R-[convolution kernel](@entry_id:1123051)** framework provides a general and elegant recipe for constructing kernels on discrete, composite objects like graphs. The core idea is to define the similarity between two whole objects by summing up similarities over all pairs of their constituent parts. 

The construction proceeds in three steps:
1.  **Decomposition:** A relation $R$ decomposes each graph $G$ into a multiset of its "parts," denoted $R(G)$. These parts can be simple (nodes, edges) or complex (walks, paths, subtrees, [graphlets](@entry_id:1125733)).
2.  **Base Kernel:** A PSD kernel $k_{\text{part}}$ is defined on the space of parts. This base kernel measures the similarity between two individual parts.
3.  **Convolution:** The final kernel on two graphs, $G$ and $H$, is computed by summing the similarities over all pairs of parts, one from each graph's decomposition:
    $k(G, H) = \sum_{p \in R(G)} \sum_{p' \in R(H)} k_{\text{part}}(p, p')$

This construction is guaranteed to produce a valid PSD kernel. If the base kernel $k_{\text{part}}$ has a [feature map](@entry_id:634540) $\phi_{\text{part}}$ such that $k_{\text{part}}(p, p') = \langle \phi_{\text{part}}(p), \phi_{\text{part}}(p') \rangle$, then the R-[convolution kernel](@entry_id:1123051) $k$ has an aggregate [feature map](@entry_id:634540) for the whole graph given by $\Phi(G) = \sum_{p \in R(G)} \phi_{\text{part}}(p)$. The kernel $k(G,H)$ is simply the inner product $\langle \Phi(G), \Phi(H) \rangle$.

Often, the parts themselves are composite, such as a walk which is a sequence of nodes and edges. In this case, the base kernel on the parts can be further constructed using a product rule. If a part $p$ is a tuple $(p_1, \dots, p_m)$ and we have PSD base kernels $k_i$ for each component, then a valid kernel on the tuples is $k_{\text{tuple}}(p, p') = \prod_{i=1}^m k_i(p_i, p'_i)$. This corresponds to a [feature map](@entry_id:634540) in the **[tensor product](@entry_id:140694)** of the component Hilbert spaces. 

### Major Families of Graph Kernels

The R-convolution principle gives rise to several important families of graph kernels. We will examine three major examples.

#### Random Walk Kernels

Random walk kernels measure similarity by counting the number of "matched" [random walks](@entry_id:159635) in two graphs. They are a canonical example of the R-convolution framework where the "parts" are walks.

The core machinery for this kernel is the **[direct product](@entry_id:143046) graph**, denoted $G \times H$. The vertex set of this graph is the Cartesian product of the original vertex sets, $V(G) \times V(H)$. An edge exists between a pair of vertices $(u, x)$ and $(v, y)$ in $G \times H$ if and only if there is an edge $(u, v)$ in $G$ *and* an edge $(x, y)$ in $H$. This represents a simultaneous step in both graphs. The [adjacency matrix](@entry_id:151010) of this product graph, $A_{\times}$, is given by the **Kronecker product** of the individual adjacency matrices: $A_{\times} = A_G \otimes A_H$. 

A walk of length $t$ in the [direct product](@entry_id:143046) graph corresponds to a matched walk of length $t$ in the original graphs. The number of such walks is given by the entries of the matrix $(A_G \otimes A_H)^t$. The [random walk kernel](@entry_id:1130563) aggregates these counts over all possible walk lengths, weighted by a decay factor $\lambda$ to ensure longer walks contribute less and that the sum converges. The kernel is defined as:

$k_{\text{RW}}(G, H) = \sum_{t=0}^{\infty} \lambda^t \mathbf{1}^\top (A_G \otimes A_H)^t \mathbf{1}$

where $\mathbf{1}$ is the all-ones vector, effectively summing over all possible start and end points. More general versions can use arbitrary start and end distributions. This infinite [geometric series](@entry_id:158490) converges if the spectral radius of the matrix $\lambda(A_G \otimes A_H)$ is less than 1. This leads to the convergence condition $|\lambda|  1 / \rho(A_G \otimes A_H)$, where $\rho(\cdot)$ is the spectral radius. Using the property $\rho(A \otimes B) = \rho(A)\rho(B)$, the condition becomes $|\lambda|  1 / (\rho(A_G) \rho(A_H))$. When this condition holds, the kernel can be computed efficiently in [closed form](@entry_id:271343) using the [matrix inverse](@entry_id:140380):

$k_{\text{RW}}(G, H) = \mathbf{1}^\top (I - \lambda(A_G \otimes A_H))^{-1} \mathbf{1}$



#### Shortest-Path Kernels

This family of kernels compares graphs by examining the distributions of their shortest-path distances. The set of [all-pairs shortest paths](@entry_id:636377) provides a global, metric-aware signature of a graph's structure.

Following the R-convolution principle, we can define a shortest-path kernel by decomposing each graph into the multiset of its shortest-path lengths $\{d_G(u,v) | (u,v) \in V_G \times V_G\}$. We then choose a PSD base kernel $\kappa$ on non-negative real numbers to compare these lengths. The final graph kernel is the sum over all pairs of shortest paths, one from each graph:

$K(G,H) = \sum_{(u,v)\in V_G \times V_G} \sum_{(x,y)\in V_H \times V_H} \kappa\big(d_G(u,v), d_H(x,y)\big)$

This construction is guaranteed to be PSD. If $\kappa(\ell, \ell') = \langle \phi(\ell), \phi(\ell') \rangle$, then the [feature map](@entry_id:634540) for the graph $G$ is $\Psi(G) = \sum_{(u,v)} \phi(d_G(u,v))$, and the kernel is the inner product of these aggregate feature vectors. 

Different choices for the base kernel $\kappa$ lead to different shortest-path kernels:
*   **Histogram Kernel:** If we choose $\kappa(\ell, \ell') = \mathbf{1}[\ell = \ell']$ (a Dirac kernel), the graph kernel simply becomes the inner product of the shortest-path length histograms of the two graphs. This compares the frequency of each path length. 
*   **Gaussian Kernel:** A common choice for $\kappa$ on continuous values is the Gaussian RBF kernel, $\kappa(\ell, \ell') = \exp(-\gamma (\ell - \ell')^2)$, which allows for soft matching of similar but not identical path lengths.
*   **Kernel Mean Embedding:** A more sophisticated approach compares the distributions of path lengths using a metric like the Maximum Mean Discrepancy (MMD). This can be formulated as a kernel $K(G,H) = \exp(-\gamma \|\mu_{P_G} - \mu_{P_H}\|^2_{\mathcal{H}_\kappa})$, where $\mu_{P_G}$ is the embedding of the path length distribution of $G$ into the RKHS of the base kernel $\kappa$. This is also a valid PSD kernel. 

#### Weisfeiler-Lehman Subtree Kernels

The Weisfeiler-Lehman (WL) kernel is one of the most powerful and widely used graph kernels. Its [expressivity](@entry_id:271569) is tied to the **Weisfeiler-Lehman test of isomorphism**, an iterative [vertex coloring](@entry_id:267488) algorithm.

The 1-WL algorithm (also known as [color refinement](@entry_id:1122664)) proceeds as follows:
1.  **Initialization:** All vertices in a graph are assigned the same initial color (e.g., based on their degree).
2.  **Iterative Refinement:** In each iteration, a vertex's color is updated based on its own current color and the multiset of its neighbors' colors. This process is repeated until the set of colors in the graph stabilizes.

The WL subtree kernel leverages this process by constructing a [feature vector](@entry_id:920515) from the color counts at each iteration. For a graph $G$, the [feature vector](@entry_id:920515) $\phi_{\text{WL},h}(G)$ is a [concatenation](@entry_id:137354) of histograms of the colors that appear at each iteration $t=0, 1, \dots, h$. The kernel is then the inner product of these feature vectors: $k_{\text{WL},h}(G,H) = \langle \phi_{\text{WL},h}(G), \phi_{\text{WL},h}(H) \rangle$.

The crucial insight is that the discriminative power of the WL subtree kernel is **identical** to that of the 1-WL test itself. Two graphs $G$ and $H$ are indistinguishable by the 1-WL test if, at every iteration, the multiset of colors in $G$ is the same as the multiset of colors in $H$. If this is the case, their feature vectors $\phi_{\text{WL},h}(G)$ and $\phi_{\text{WL},h}(H)$ will be identical for any $h$. Consequently, the kernel cannot distinguish them.  

This reveals a fundamental limitation. The 1-WL test is known not to be a complete [isomorphism](@entry_id:137127) test. For example, any two non-isomorphic regular graphs of the same size and degree are indistinguishable by 1-WL. A classic example is the [cycle graph](@entry_id:273723) $C_6$ and the disjoint union of two triangles $K_3 \cup K_3$. More powerful counterexamples exist, such as pairs of non-isomorphic **[strongly regular graphs](@entry_id:269473)** with the same parameters (e.g., the Shrikhande graph and the $4 \times 4$ rook's graph), which the 1-WL test, and therefore the WL subtree kernel, cannot distinguish. 

### Expressivity, Invariance, and Universality

The design of a graph kernel always involves a trade-off between **invariance** and **[expressivity](@entry_id:271569)**. A highly invariant kernel (e.g., one based only on the degree distribution) is robust to small structural changes but may fail to distinguish between graphs with very different structures. Conversely, a highly expressive kernel can capture fine-grained structural details but may be more sensitive to noise and computationally expensive.

For example, consider two 3-regular graphs on 6 vertices: the complete [bipartite graph](@entry_id:153947) $K_{3,3}$ and the triangular prism graph $C_3 \square K_2$. A simple degree-distribution kernel cannot distinguish them, as they have identical degree distributions. However, $K_{3,3}$ is triangle-free, while the prism has two triangles. An augmented kernel that includes a feature for triangle counts can easily distinguish them. This demonstrates how adding higher-order structural features increases [expressivity](@entry_id:271569), allowing the kernel to separate graphs that simpler invariants cannot. 

A key theoretical concept related to [expressivity](@entry_id:271569) is **universality**. A kernel $k$ on the space of graphs $\mathcal{G}$ is said to be universal if its RKHS, $\mathcal{H}_k$, is dense in the space of all continuous functions on $\mathcal{G}$. Intuitively, this means a learning algorithm using a universal kernel can approximate any continuous target function on graphs to arbitrary accuracy, given enough data.

However, most practical graph kernels, including the families discussed above, are **not universal**. The reason lies in the nature of their [feature maps](@entry_id:637719). These kernels typically rely on counting a [finite set](@entry_id:152247) of substructures or running an algorithm for a finite number of steps. This results in a [feature map](@entry_id:634540) $\phi: \mathcal{G} \to \mathbb{R}^m$ that is either finite-dimensional or, more fundamentally, **non-injective**. A non-[injective map](@entry_id:262763) means there exist non-[isomorphic graphs](@entry_id:271870) $G \neq H$ that are mapped to the same feature vector, $\phi(G) = \phi(H)$. As we saw with the WL kernel, this is a common occurrence. If two distinct graphs have the same feature vector, then any function $f \in \mathcal{H}_k$ must assign them the same value, since $f(G) = \langle w, \phi(G) \rangle = \langle w, \phi(H) \rangle = f(H)$. It is therefore impossible for the RKHS to approximate a continuous function that separates $G$ and $H$. This fundamental limitation prevents the RKHS from being dense in the space of all continuous functions, thus precluding universality. 