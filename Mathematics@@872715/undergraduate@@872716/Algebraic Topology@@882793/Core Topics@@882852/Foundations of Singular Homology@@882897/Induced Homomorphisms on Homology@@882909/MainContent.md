## Introduction
In the study of algebraic topology, we assign algebraic structures, such as homology groups, to topological spaces to understand their underlying properties. However, these structures would be of limited value if they existed in isolation. The crucial bridge between the geometric world of spaces and [continuous maps](@entry_id:153855) and the algebraic world of groups and homomorphisms is the concept of an **[induced homomorphism](@entry_id:149311)**. This mechanism translates continuous functions into algebraic ones, allowing us to compare the homology of different spaces and understand the deep effects of a map on a space's structure. This article addresses the fundamental question of how topology and algebra are formally connected, providing a comprehensive guide to this essential tool.

The following chapters will guide you through the theory and application of [induced homomorphisms](@entry_id:266478). In "Principles and Mechanisms," we will delve into the formal definition, exploring the foundational principles of [functoriality](@entry_id:150069) and homotopy invariance, and establish concrete methods for their computation. Next, "Applications and Interdisciplinary Connections" will showcase the power of these concepts by using them to define [geometric invariants](@entry_id:178611) like the [degree of a map](@entry_id:158493) and by revealing their surprising role in fields like dynamical systems and theoretical physics. Finally, "Hands-On Practices" will offer a set of targeted problems to help you master the computational techniques and solidify your understanding of the core ideas.

## Principles and Mechanisms

A [continuous map](@entry_id:153772) between [topological spaces](@entry_id:155056) provides a bridge, connecting the structure of one space to another. The algebraic invariants we assign to these spaces, such as homology groups, would be of limited use if they did not respect these bridges. The concept of an **[induced homomorphism](@entry_id:149311)** is the crucial mechanism that translates the geometric language of [continuous maps](@entry_id:153855) into the algebraic language of group homomorphisms, providing a powerful tool for comparing and understanding [topological spaces](@entry_id:155056). This chapter explores the fundamental principles governing these induced maps and the mechanisms by which they are calculated and applied.

### Functoriality: The Foundational Principle

At its core, [singular homology](@entry_id:158380) is a **functor** from the category of topological spaces to the category of graded [abelian groups](@entry_id:145145). This statement packs in two foundational properties that govern how maps between spaces translate to maps between homology groups.

Let $f: X \to Y$ be a continuous map. For any singular $k$-simplex, which is a map $\sigma: \Delta^k \to X$, the composition $f \circ \sigma: \Delta^k \to Y$ is a singular $k$-[simplex](@entry_id:270623) in $Y$. This defines a homomorphism between the chain groups, $f_\#: S_k(X) \to S_k(Y)$, by setting $f_\#(\sum n_i \sigma_i) = \sum n_i (f \circ \sigma_i)$. A key verification shows that this [chain map](@entry_id:266133) commutes with the [boundary operator](@entry_id:160216) $\partial$, meaning $\partial \circ f_\# = f_\# \circ \partial$. This compatibility ensures that $f_\#$ sends cycles to [cycles and boundaries](@entry_id:261701) to boundaries, thus descending to a well-defined homomorphism on the homology groups, denoted $f_*: H_k(X) \to H_k(Y)$ for each integer $k \ge 0$.

The functorial properties of this construction are:

1.  **Identity Preservation**: The identity map $\text{id}_X: X \to X$ induces the identity homomorphism on homology: $(\text{id}_X)_* = \text{id}: H_k(X) \to H_k(X)$ for all $k$.
2.  **Composition Preservation**: For a composition of [continuous maps](@entry_id:153855) $X \xrightarrow{f} Y \xrightarrow{g} Z$, the [induced homomorphism](@entry_id:149311) is the composition of the individual [induced homomorphisms](@entry_id:266478): $(g \circ f)_* = g_* \circ f_*$.

This second property is particularly powerful. It allows us to deduce properties of a complex map's [induced homomorphism](@entry_id:149311) by factoring the map through simpler intermediate spaces. A primary example is the constant map. Consider a map $f: X \to Y$ that sends every point in $X$ to a single point $y_0 \in Y$. This map can be factored as the composition $X \xrightarrow{c} \{y_0\} \xrightarrow{i} Y$, where $c$ is the map collapsing $X$ to a single-point space $\{y_0\}$, and $i$ is the inclusion of that point into $Y$.

By the composition property, $f_* = (i \circ c)_* = i_* \circ c_*$. To understand this map, we need the homology of a one-point space, which is a fundamental calculation: $H_k(\{y_0\}) = 0$ for all $k > 0$, and $H_0(\{y_0\}) \cong \mathbb{Z}$. For any dimension $k > 0$, the [codomain](@entry_id:139336) of the map $c_*: H_k(X) \to H_k(\{y_0\})$ is the [trivial group](@entry_id:151996) $\{0\}$. Therefore, $c_*$ must be the zero homomorphism, sending every element of $H_k(X)$ to $0$. Consequently, the full composite map $f_* = i_* \circ c_*$ must also be the zero homomorphism for all $k > 0$ [@problem_id:1658308].

### Homotopy Invariance: Deformations and Their Algebraic Trace

One of the central tenets of algebraic topology is that spaces that can be continuously deformed into one another should be considered "the same" from a topological perspective. The algebraic counterpart to this principle is **homotopy invariance**. It states that if two maps $f, g: X \to Y$ are homotopic (written $f \simeq g$), then they induce the same homomorphism on all homology groups:

$$f \simeq g \implies f_* = g_* : H_k(X) \to H_k(Y) \text{ for all } k \ge 0.$$

This theorem is proven by constructing an algebraic "homotopy between [chain maps](@entry_id:268209)," known as a [chain homotopy](@entry_id:158964), which relates $f_\#$ and $g_\#$. This algebraic object ensures that for any cycle $z$, the chains $f_\#(z)$ and $g_\#(z)$ differ by a boundary, meaning they represent the same homology class.

A direct and important consequence concerns **[nullhomotopic maps](@entry_id:268278)**. A map $f: X \to Y$ is [nullhomotopic](@entry_id:148739) if it is homotopic to a constant map $c: X \to Y$. By homotopy invariance, $f_* = c_*$. As we established in the previous section by factoring through a point, the [induced map](@entry_id:271712) $c_*$ is the zero map for all positive dimensions. Therefore, any [nullhomotopic](@entry_id:148739) map induces the zero homomorphism on all positive-dimensional homology groups [@problem_id:1658301]. This implies that the image of such a map, $\text{Im}(f_*)$, is the [trivial subgroup](@entry_id:141709) $\{0\}$, and its kernel, $\ker(f_*)$, is the entire domain $H_k(X)$.

An immediate corollary is that if two spaces $X$ and $Y$ are homotopy equivalent, then their homology groups are isomorphic, since the maps implementing the homotopy equivalence induce inverse isomorphisms on homology.

### From Geometry to Matrices: Concrete Computations

While the abstract properties of [induced homomorphisms](@entry_id:266478) are powerful, it is essential to be able to compute them in concrete situations. For finitely generated homology groups, which are common for spaces built from simple cells, [induced homomorphisms](@entry_id:266478) can be represented by matrices.

#### The Connection to the Fundamental Group

For a [path-connected space](@entry_id:156428) $X$, the [first homology group](@entry_id:145318) $H_1(X)$ is intimately related to the fundamental group $\pi_1(X, x_0)$. Specifically, $H_1(X)$ is the **[abelianization](@entry_id:140523)** of $\pi_1(X, x_0)$, the group obtained by quotienting $\pi_1$ by its [commutator subgroup](@entry_id:140057). The homomorphism from $\pi_1$ to $H_1$ simply "forgets" the non-commutative information.

This relationship is natural. For a map $f: (X, x_0) \to (Y, y_0)$, the [induced map](@entry_id:271712) on first homology, $f_*: H_1(X) \to H_1(Y)$, is precisely the abelianization of the [induced map](@entry_id:271712) on the fundamental groups, $f_\#: \pi_1(X, x_0) \to \pi_1(Y, y_0)$. This allows us to compute $f_*$ on $H_1$ if we know its action on $\pi_1$.

For example, let $X = S^1 \vee S^1$ (the wedge of two circles) and $Y = T^2 = S^1 \times S^1$. Their fundamental groups are $\pi_1(X) \cong \mathbb{Z} * \mathbb{Z}$, the [free group](@entry_id:143667) on two generators $\{a, b\}$, and $\pi_1(Y) \cong \mathbb{Z} \times \mathbb{Z}$, the free abelian group on two generators $\{u, v\}$. Correspondingly, their first homology groups are $H_1(X) \cong \mathbb{Z} \oplus \mathbb{Z}$ with basis $\{[a], [b]\}$ and $H_1(Y) \cong \mathbb{Z} \oplus \mathbb{Z}$ with basis $\{[u], [v]\}$. Suppose a map $f: X \to Y$ induces a map on fundamental groups given by $f_\#(a) = u^3 v^2$ and $f_\#(b) = u^{-1} v^4$. To find the [induced map](@entry_id:271712) $f_*$ on homology, we abelianize these expressions. In the additive notation of homology, this means:
$$f_*([a]) = 3[u] + 2[v]$$
$$f_*([b]) = -1[u] + 4[v]$$
With respect to the ordered bases $([a], [b])$ and $([u], [v])$, the homomorphism $f_*$ is represented by the matrix whose columns are the coordinate vectors of the images of the basis vectors. This gives the matrix $\begin{pmatrix} 3 & -1 \\ 2 & 4 \end{pmatrix}$ [@problem_id:1658281].

#### Composition and Matrix Multiplication

The functorial property $(g \circ f)_* = g_* \circ f_*$ elegantly translates into [matrix multiplication](@entry_id:156035). Consider maps between spaces whose homology groups are represented by free abelian groups. The [induced homomorphism](@entry_id:149311) for each map corresponds to a matrix, and the [induced homomorphism](@entry_id:149311) for the composite map corresponds to the product of those matrices.

Let's illustrate this with maps on the torus, $T^2 = S^1 \times S^1$. We identify $H_1(T^2, \mathbb{Z})$ with $\mathbb{Z} \oplus \mathbb{Z}$ via a basis $\{\beta_1, \beta_2\}$ corresponding to the two principal circles of the torus, and $H_1(S^1, \mathbb{Z})$ with $\mathbb{Z}$ via a generator $\alpha$. Consider a map $p: T^2 \to S^1$ given by $p(z_1, z_2) = z_1^2 z_2^4$ and a map $i: S^1 \to T^2$ given by $i(z) = (z^3, z^{-2})$. The composite map is $f = i \circ p: T^2 \to T^2$.
The map $p_*$ sends $\beta_1$ to the class of a loop of degree 2 in $S^1$ and $\beta_2$ to the class of a loop of degree 4. So, $p_*(\beta_1) = 2\alpha$ and $p_*(\beta_2) = 4\alpha$. As a map from $\mathbb{Z}^2$ to $\mathbb{Z}$, this is represented by the row matrix $\begin{pmatrix} 2 & 4 \end{pmatrix}$.
The map $i_*$ sends the generator $\alpha$ of $H_1(S^1)$ to the homology class represented by a loop that winds 3 times around the first circle of the torus and -2 times around the second. So, $i_*(\alpha) = 3\beta_1 - 2\beta_2$. As a map from $\mathbb{Z}$ to $\mathbb{Z}^2$, this is represented by the column matrix $\begin{pmatrix} 3 \\ -2 \end{pmatrix}$.
The [induced map](@entry_id:271712) of the composition, $f_* = i_* \circ p_*$, is represented by the product of these matrices:
$$ f_* \longleftrightarrow \begin{pmatrix} 3 \\ -2 \end{pmatrix} \begin{pmatrix} 2 & 4 \end{pmatrix} = \begin{pmatrix} 6 & 12 \\ -4 & -8 \end{pmatrix} $$
This matrix completely describes the action of the self-map $f$ on the first homology of the torus [@problem_id:1658298].

### Naturality and Exact Sequences

The true power of [induced homomorphisms](@entry_id:266478) is revealed when they are combined with the major structural theorems of homology theory, such as the long [exact sequences](@entry_id:151503) associated with pairs and unions of spaces. The key concept is **[naturality](@entry_id:270302)**, which asserts that [induced homomorphisms](@entry_id:266478) commute with the structural maps of these sequences.

#### The Long Exact Sequence of a Pair

A [continuous map](@entry_id:153772) $f: X \to Y$ that also maps a subspace $A \subseteq X$ into a subspace $B \subseteq Y$ is called a **map of pairs**, denoted $f: (X,A) \to (Y,B)$. Such a map induces homomorphisms not only on the absolute homology groups $H_k(X)$ and $H_k(A)$, but also on the [relative homology groups](@entry_id:159711) $H_k(X,A)$.

These induced maps arrange themselves into a "ladder diagram" connecting the long [exact sequences](@entry_id:151503) for the two pairs:
```
... --> H_k(A) --> H_k(X) --> H_k(X,A) --> H_{k-1}(A) --> ...
       |           |           |             |
     (f|A)_*     f_*         f_*           (f|A)_*
       |           |           |             |
       v           v           v             v
... --> H_k(B) --> H_k(Y) --> H_k(Y,B) --> H_{k-1}(B) --> ...
```
Naturality means that every square in this diagram commutes. The most useful of these [commutation relations](@entry_id:136780) is often the one involving the [connecting homomorphism](@entry_id:160713) $\partial$:
$$ \partial \circ f_* = (f|_A)_* \circ \partial $$
This equation allows us to relate the [induced map](@entry_id:271712) on [relative homology](@entry_id:159348) to the [induced map](@entry_id:271712) on the homology of the boundary subspace. Consider the pair $(D^n, S^{n-1})$ consisting of the $n$-disk and its boundary sphere. The long exact sequence for this pair shows that the [connecting homomorphism](@entry_id:160713) $\partial: H_n(D^n, S^{n-1}) \to H_{n-1}(S^{n-1})$ is an isomorphism for $n \ge 1$.
Now, let $f: (D^n, S^{n-1}) \to (D^n, S^{n-1})$ be a map of pairs. Let $g = f|_{S^{n-1}}: S^{n-1} \to S^{n-1}$ be its restriction to the boundary. The [induced map](@entry_id:271712) $g_*: H_{n-1}(S^{n-1}) \to H_{n-1}(S^{n-1})$ is multiplication by an integer, the degree of $g$, which we denote by $k$. Similarly, $f_*: H_n(D^n, S^{n-1}) \to H_n(D^n, S^{n-1})$ is multiplication by some integer $m$. The [commutativity](@entry_id:140240) relation $\partial \circ f_* = g_* \circ \partial$ becomes a statement about these integers. Since $\partial$ is an isomorphism, we can compose with its inverse to find that $f_* = \partial^{-1} \circ g_* \circ \partial$. This algebraic conjugation implies that the linear maps $f_*$ and $g_*$ must be multiplication by the same scalar. Therefore, $m = k$. The [induced map](@entry_id:271712) on [relative homology](@entry_id:159348) is completely determined by the degree of the map on the boundary [@problem_id:1658279] [@problem_id:1658265].

#### Mayer-Vietoris and Suspension Isomorphisms

This principle of [naturality](@entry_id:270302) extends to other fundamental sequences and isomorphisms.
- If a map $f: X \to Y$ respects decompositions of the spaces into open sets, say $X=U \cup V$ and $Y=A \cup B$ with $f(U) \subseteq A$ and $f(V) \subseteq B$, then $f$ induces a [chain map](@entry_id:266133) between the respective Mayer-Vietoris sequences. This allows for component-wise calculation of induced maps on subspaces, which can then be assembled to understand the global map [@problem_id:1658283].
- The **[suspension isomorphism](@entry_id:156388)**, $S: \tilde{H}_k(X) \stackrel{\cong}{\longrightarrow} \tilde{H}_{k+1}(\Sigma X)$, is also natural. For any map $f: X \to Y$, its suspension $\Sigma f: \Sigma X \to \Sigma Y$ satisfies $(\Sigma f)_* \circ S = S \circ f_*$. This simple [commutation relation](@entry_id:150292) has a profound consequence for maps on spheres. Let $f: S^n \to S^n$ be a map of degree $k$. Its suspension is a map $\Sigma f: S^{n+1} \to S^{n+1}$. The [naturality](@entry_id:270302) of the [suspension isomorphism](@entry_id:156388) immediately implies that $\deg(\Sigma f) = \deg(f) = k$. The [degree of a map](@entry_id:158493) on a sphere is invariant under suspension [@problem_id:1658302].

### Deeper Connections and Advanced Applications

The theory of [induced homomorphisms](@entry_id:266478) connects to nearly every aspect of algebraic topology, leading to sophisticated results and computational tools.

#### Degree, Determinants, and Coefficients

For a self-map $f: M \to M$ on a closed, connected, oriented $n$-manifold, the [induced map](@entry_id:271712) on the top homology group, $f_*: H_n(M) \to H_n(M)$, is multiplication by an integer called the **degree** of $f$. For the [2-torus](@entry_id:265991) $T^2$, the degree is related to the action on $H_1$. If the matrix for $f_*: H_1(T^2) \to H_1(T^2)$ is $A$, then the degree of $f$ is equal to $\det(A)$.

This relationship can be used to deduce non-obvious properties. Suppose we are told that for a map $f: T^2 \to T^2$, the [induced map on homology](@entry_id:265781) with coefficients in $\mathbb{Z}_p$ (for a prime $p$) is zero, i.e., $f_*: H_1(T^2; \mathbb{Z}_p) \to H_1(T^2; \mathbb{Z}_p)$ is the zero map. By the Universal Coefficient Theorem, this is equivalent to saying that the [integer matrix](@entry_id:151642) $A$ representing $f_*$ on $H_1(T^2; \mathbb{Z})$ becomes the [zero matrix](@entry_id:155836) when its entries are reduced modulo $p$. This means every entry of $A$ is divisible by $p$. We can write $A = pB$ for some [integer matrix](@entry_id:151642) $B$. The degree of $f$ is then:
$$ \deg(f) = \det(A) = \det(pB) = p^2 \det(B) $$
Therefore, the degree of $f$ must be divisible by $p^2$. This shows how knowledge of the [induced map](@entry_id:271712) with one set of coefficients can constrain its properties with another [@problem_id:1658259].

#### The Diagonal Map and the Cup Product

A map of central importance is the **diagonal map** $\Delta: X \to X \times X$, given by $\Delta(x) = (x,x)$. The [induced map](@entry_id:271712) $\Delta_*: H_k(X) \to H_k(X \times X)$ is fundamental because it relates the homology of $X$ to the homology of its product with itself. Using the Künneth formula (with field coefficients, for simplicity), we can decompose $H_k(X \times X)$ as $\bigoplus_{i+j=k} H_i(X) \otimes H_j(X)$. The map $\Delta_*$ is the homological encoding of how $X$ sits inside this product.

This map is dually related to the **[cup product](@entry_id:159554)** in cohomology. The [induced map](@entry_id:271712) $\Delta^*$ on cohomology pulls back cohomology classes from $X \times X$ to $X$. The cup product $\cup$ on $H^*(X)$ is defined precisely via this pullback: $\alpha \cup \beta = \Delta^*(\alpha \times \beta)$, where $\times$ is the cross product in cohomology. This duality allows us to compute $\Delta_*$ if we know the cup product structure of $H^*(X)$.

Let's consider $X = \mathbb{C}P^2$, complex projective 2-space, with rational coefficients. Its non-zero homology groups are $H_{2k}(\mathbb{C}P^2; \mathbb{Q}) \cong \mathbb{Q}$ for $k=0,1,2$. Let $\alpha_{2k}$ be a generator for $H_{2k}$. We want to compute $\Delta_*(\alpha_4) \in H_4(\mathbb{C}P^2 \times \mathbb{C}P^2)$. By the Künneth formula,
$$ H_4(\mathbb{C}P^2 \times \mathbb{C}P^2) \cong (H_4 \otimes H_0) \oplus (H_2 \otimes H_2) \oplus (H_0 \otimes H_4) $$
Let the basis for this space be $\{\alpha_4 \otimes \alpha_0, \alpha_2 \otimes \alpha_2, \alpha_0 \otimes \alpha_4\}$. We can write $\Delta_*(\alpha_4)$ as a linear combination $c_1(\alpha_4 \otimes \alpha_0) + c_2(\alpha_2 \otimes \alpha_2) + c_3(\alpha_0 \otimes \alpha_4)$.

To find the coefficients $c_i$, we pair this expression with basis elements from the dual cohomology group $H^4(\mathbb{C}P^2 \times \mathbb{C}P^2)$. Let $\beta^{2k}$ be the generator of $H^{2k}(\mathbb{C}P^2)$ dual to $\alpha_{2k}$. The basis for $H^4$ of the product is $\{\beta^4 \otimes \beta^0, \beta^2 \otimes \beta^2, \beta^0 \otimes \beta^4\}$. Using the Kronecker pairing $\langle \cdot, \cdot \rangle$, [naturality](@entry_id:270302) of $\Delta$, and the duality between $\Delta_*$ and the cup product, we have:
$$ \langle \beta^p \otimes \beta^q, \Delta_*(\alpha_4) \rangle = \langle \Delta^*(\beta^p \otimes \beta^q), \alpha_4 \rangle = \langle \beta^p \cup \beta^q, \alpha_4 \rangle $$
The [cohomology ring](@entry_id:160158) of $\mathbb{C}P^2$ is generated by $\beta^2$ with the relation $\beta^2 \cup \beta^2 = \beta^4$. Thus, for any pair $(p, q)$ with $p+q=4$, the [cup product](@entry_id:159554) $\beta^p \cup \beta^q$ is equal to $\beta^4$. Therefore, $\langle \beta^p \cup \beta^q, \alpha_4 \rangle = \langle \beta^4, \alpha_4 \rangle = 1$.
Evaluating the left side, we find that pairing with $\beta^4 \otimes \beta^0$ picks out $c_1$, pairing with $\beta^2 \otimes \beta^2$ picks out $c_2$, and pairing with $\beta^0 \otimes \beta^4$ picks out $c_3$. Since all these pairings must equal 1, we conclude that $c_1=c_2=c_3=1$. Thus:
$$ \Delta_*(\alpha_4) = (\alpha_4 \otimes \alpha_0) + (\alpha_2 \otimes \alpha_2) + (\alpha_0 \otimes \alpha_4) $$
This calculation [@problem_id:1658284] beautifully demonstrates the profound interplay between homology, cohomology, products of spaces, and the maps that connect them. It is a testament to the cohesive and predictive power of the functorial machinery in algebraic topology.