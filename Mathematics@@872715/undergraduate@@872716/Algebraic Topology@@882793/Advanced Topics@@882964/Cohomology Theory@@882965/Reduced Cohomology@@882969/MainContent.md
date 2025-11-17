## Introduction
In the vast landscape of algebraic topology, [cohomology theory](@entry_id:270863) stands as a pillar, offering a set of powerful algebraic invariants to classify and distinguish topological spaces. While ordinary [singular cohomology](@entry_id:271229) is the standard tool, it carries a feature that can be an algebraic inconvenience: even the simplest topological object, a single point, has a non-trivial cohomology group. This prompts the question: can we refine the theory to 'normalize' this behavior? Reduced cohomology is the answer—a modification specifically designed to ensure that a point, and by extension any contractible space, has trivial cohomology in all degrees. This seemingly minor adjustment unlocks a world of cleaner formulations, streamlined computations, and deeper insights.

This article provides a thorough introduction to reduced cohomology, structured to build your understanding from the ground up. In the "Principles and Mechanisms" chapter, we will formally define reduced cohomology, explore its fundamental relationship with the ordinary theory, and see how it simplifies the algebraic picture for contractible spaces. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate the theory's power in action, showing how it provides elegant statements for foundational theorems and serves as a workhorse for computing the invariants of complex spaces. Finally, the "Hands-On Practices" section will offer you the opportunity to solidify your knowledge by working through concrete computational problems. Together, these sections will equip you with a robust understanding of why reduced cohomology is not just a theoretical curiosity, but an indispensable tool in the modern topologist's toolkit.

## Principles and Mechanisms

In the study of algebraic topology, [cohomology theory](@entry_id:270863) provides a powerful suite of invariants for distinguishing [topological spaces](@entry_id:155056). While ordinary [singular cohomology](@entry_id:271229) is foundational, it possesses a feature that can be cumbersome in certain contexts: a single-point space, the topologically simplest object, has non-trivial cohomology in degree zero. Reduced cohomology is a refinement of the ordinary theory, designed specifically to "normalize" this behavior, ensuring that a point—and by extension, any contractible space—has trivial cohomology in all degrees. This seemingly small adjustment leads to cleaner formulations of major theorems and simplifies numerous calculations.

### Definition and the Fundamental Splitting

The construction of reduced cohomology begins at the chain level, with the **augmented singular [chain complex](@entry_id:150246)**. For a non-empty space $X$ and coefficient group $G$ (which we will often take to be $\mathbb{Z}$ for clarity), the ordinary singular [chain complex](@entry_id:150246) is:
$$
\dots \xrightarrow{\partial_3} C_2(X) \xrightarrow{\partial_2} C_1(X) \xrightarrow{\partial_1} C_0(X) \to 0
$$
Here, $C_n(X)$ is the free [abelian group](@entry_id:139381) on the set of singular $n$-simplices in $X$. The augmentation is achieved by adding a map $\epsilon: C_0(X) \to \mathbb{Z}$ to the end of this sequence. The **[augmentation map](@entry_id:272732)** $\epsilon$ acts on a formal sum of 0-simplices (points) $\sum n_i \sigma_i$ by summing their coefficients: $\epsilon(\sum n_i \sigma_i) = \sum n_i$. Since the boundary of any 1-[simplex](@entry_id:270623) $\tau: \Delta^1 \to X$ is of the form $\sigma_1 - \sigma_0$, we have $\epsilon(\partial_1 \tau) = 1 - 1 = 0$, confirming that $\epsilon \circ \partial_1 = 0$. This gives the augmented [chain complex](@entry_id:150246):
$$
\dots \xrightarrow{\partial_2} C_1(X) \xrightarrow{\partial_1} C_0(X) \xrightarrow{\epsilon} \mathbb{Z} \to 0
$$
This sequence is exact, and its homology groups are the **reduced [singular homology](@entry_id:158380) groups** of $X$.

To define **reduced cohomology**, we apply the contravariant functor $\text{Hom}(-, G)$ to this augmented [chain complex](@entry_id:150246). This process reverses the arrows and yields the **reduced [cochain](@entry_id:275805) complex**:
$$
0 \to \text{Hom}(\mathbb{Z}, G) \xrightarrow{\epsilon^*} \text{Hom}(C_0(X), G) \xrightarrow{\delta^0} \text{Hom}(C_1(X), G) \xrightarrow{\delta^1} \dots
$$
where $\delta^{n-1} = \partial_n^*$. Recognizing that $\text{Hom}(C_n(X), G)$ is precisely the group of $n$-[cochains](@entry_id:159583) $C^n(X; G)$, and that $\text{Hom}(\mathbb{Z}, G) \cong G$, we can write this complex as:
$$
0 \to G \xrightarrow{\epsilon^*} C^0(X; G) \xrightarrow{\delta^0} C^1(X; G) \xrightarrow{\delta^1} C^2(X; G) \to \dots
$$
The cohomology groups of this complex are the **reduced [singular cohomology](@entry_id:271229) groups** of $X$, denoted $\tilde{H}^n(X; G)$.

The structure of this new complex is nearly identical to the ordinary [cochain](@entry_id:275805) complex, except for the initial map $\epsilon^*$ in degree 0. This modification only affects the 0-th cohomology group. The relationship between ordinary and reduced cohomology can be made precise by considering the [short exact sequence](@entry_id:137930) of chain complexes that defines the reduced [chain complex](@entry_id:150246), $\tilde{C}_*(X) = \ker(\epsilon)$. For a non-empty space $X$, this sequence $0 \to \tilde{C}_*(X) \to C_*(X) \to \mathbb{Z} \to 0$ splits. Applying the $\text{Hom}(-,G)$ [functor](@entry_id:260898) gives a [short exact sequence](@entry_id:137930) of [cochain](@entry_id:275805) complexes, which in turn induces a [long exact sequence in cohomology](@entry_id:266961).

This [long exact sequence](@entry_id:153438) reveals the fundamental connection between $H^n(X; G)$ and $\tilde{H}^n(X; G)$ [@problem_id:1668504].
For $n \ge 1$, the relevant portion of the [long exact sequence](@entry_id:153438) is
$$ \dots \to H^n(\text{pt}; G) \to H^n(X; G) \to \tilde{H}^n(X; G) \to H^{n+1}(\text{pt}; G) \to \dots $$
Since the cohomology of a point, $H^k(\text{pt}; G)$, is trivial for $k \ge 1$, the terms surrounding $\tilde{H}^n(X; G)$ and $H^n(X; G)$ are zero. Exactness then implies a direct [isomorphism](@entry_id:137127):
$$ H^n(X; G) \cong \tilde{H}^n(X; G) \quad \text{for all } n \ge 1. $$
The difference appears only in degree 0. The [long exact sequence](@entry_id:153438) begins:
$$ 0 \to H^0(\text{pt}; G) \to H^0(X; G) \to \tilde{H}^0(X; G) \to H^1(\text{pt}; G) \to \dots $$
Knowing $H^0(\text{pt}; G) \cong G$ and $H^1(\text{pt}; G) = 0$, this truncates to a [short exact sequence](@entry_id:137930):
$$ 0 \to G \to H^0(X; G) \to \tilde{H}^0(X; G) \to 0 $$
Because the original chain sequence splits, this sequence of cohomology groups also splits. This yields the crucial splitting relationship for any non-empty space $X$:
$$ H^0(X; G) \cong \tilde{H}^0(X; G) \oplus G. $$

In summary, reduced cohomology is identical to ordinary cohomology in all positive degrees, while in degree zero, it is a [direct summand](@entry_id:150541) of the ordinary theory, having "factored out" a copy of the coefficient group $G$.

### A Key Simplification: The Cohomology of Contractible Spaces

The primary motivation for introducing reduced cohomology is its behavior on contractible spaces. A space is **contractible** if it is homotopy equivalent to a single point. By the homotopy invariance of cohomology, a contractible space $X$ has the same cohomology groups as a point, denoted $*$. Let's compute these for a point. The ordinary cohomology is:
$$ H^n(*; G) = \begin{cases} G  \text{if } n=0 \\ 0  \text{if } n > 0 \end{cases} $$
The non-[trivial group](@entry_id:151996) in degree 0 can be an algebraic inconvenience. Applying the fundamental splitting relation, we can find the reduced cohomology of a point:
For $n \ge 1$, $\tilde{H}^n(*; G) \cong H^n(*; G) = 0$.
For $n = 0$, $H^0(*; G) \cong \tilde{H}^0(*; G) \oplus G$. Since $H^0(*; G) \cong G$, this implies $\tilde{H}^0(*; G)$ must be the [trivial group](@entry_id:151996), 0.

Thus, for a single-point space, we have the elegant result:
$$ \tilde{H}^n(*; G) = 0 \quad \text{for all } n \ge 0. $$
By homotopy invariance, this result extends immediately to all non-empty contractible spaces [@problem_id:1668473]. For any such space $X$, for instance Euclidean space $\mathbb{R}^k$ or the cone $CX$ over any space $X$, we have:
$$ \tilde{H}^n(X; G) = 0 \quad \text{for all } n \ge 0 \quad \text{(if X is contractible)}. $$
This is a significant simplification. Theorems and formulas involving sums over all [cohomology groups](@entry_id:142450) of a space become simpler when applied to contractible spaces, as all terms simply vanish [@problem_id:1668510].

### Geometric Interpretation of Zeroth Reduced Cohomology

The relationship $H^0(X; G) \cong \tilde{H}^0(X; G) \oplus G$ allows us to develop a clear geometric intuition for the 0-th reduced group. Recall that for any space $X$, $H^0(X; G)$ is isomorphic to the group of all locally constant functions from $X$ to $G$. If $X$ has $k$ path components, say $X_1, \dots, X_k$, then any such function is determined by its constant value on each component. Therefore, $H^0(X; G) \cong \prod_{i=1}^k G = G^k$.

For a **path-connected** non-empty space, $k=1$, so $H^0(X; G) \cong G$. The splitting formula $G \cong \tilde{H}^0(X; G) \oplus G$ immediately forces $\tilde{H}^0(X; G)$ to be the trivial group [@problem_id:1668514].

What if $X$ is not path-connected? Consider a space with $k$ path components. With integer coefficients, $H^0(X; \mathbb{Z}) \cong \mathbb{Z}^k$. The splitting formula gives $\mathbb{Z}^k \cong \tilde{H}^0(X; \mathbb{Z}) \oplus \mathbb{Z}$, which implies:
$$ \tilde{H}^0(X; \mathbb{Z}) \cong \mathbb{Z}^{k-1} $$
This gives a beautiful interpretation: the rank of the 0-th reduced cohomology group counts the number of path components, minus one. It measures the extent to which the space is disconnected [@problem_id:1668483].

We can understand this from the definition as well. $\tilde{H}^0(X; G)$ is the quotient of all 0-[cocycles](@entry_id:160556) (locally constant functions) by the subgroup of *constant* 0-[cocycles](@entry_id:160556). Let's make this concrete with a simple example: a space $X$ consisting of two discrete points, $X=\{p, q\}$ [@problem_id:1668516]. The 0-[cochains](@entry_id:159583) with integer coefficients are functions from $\{p, q\}$ to $\mathbb{Z}$, so $C^0(X; \mathbb{Z}) \cong \mathbb{Z} \oplus \mathbb{Z}$. Since there are no 1-[simplices](@entry_id:264881) connecting the points, all 0-[cochains](@entry_id:159583) are 0-[cocycles](@entry_id:160556), so $H^0(X; \mathbb{Z}) \cong \mathbb{Z} \oplus \mathbb{Z}$. A cochain is identified by the pair of values $(\phi(\sigma_p), \phi(\sigma_q))$. The subgroup of *constant* [cochains](@entry_id:159583), which is the image of $\epsilon^*$, consists of all pairs of the form $(m, m)$ for $m \in \mathbb{Z}$. The 0-th reduced cohomology group is the quotient:
$$ \tilde{H}^0(X; \mathbb{Z}) = \frac{H^0(X; \mathbb{Z})}{\text{im}(\epsilon^*)} \cong \frac{\mathbb{Z} \oplus \mathbb{Z}}{\{(m, m) \mid m \in \mathbb{Z}\}} $$
This quotient group is isomorphic to $\mathbb{Z}$. A generator for this group is the equivalence class of a [cochain](@entry_id:275805) that is non-zero on one component and zero on the other, for instance, the one represented by the pair $(1, 0)$. This corresponds to the general result $\mathbb{Z}^{2-1} = \mathbb{Z}$.

### The Power of Reduced Cohomology in Exact Sequences

The true utility of reduced cohomology becomes most apparent when working with the fundamental long [exact sequences](@entry_id:151503) of algebraic topology. The fact that $\tilde{H}^n(\text{pt})=0$ for all $n$ cleans up the statements of several key theorems.

#### The Suspension Isomorphism

The **suspension** of a [pointed space](@entry_id:265918) $X$, denoted $SX$ or $\Sigma X$, is the space obtained by taking the cylinder $X \times [0,1]$ and collapsing the top ($X \times \{1\}$) to a point and the bottom ($X \times \{0\}$) to another point. A related construction is the **cone** $CX$, where only the top $X \times \{1\}$ is collapsed. The suspension can be seen as the quotient of the cone, $SX \cong CX/X$.

This structure gives rise to a [long exact sequence](@entry_id:153438) in reduced cohomology for the pair $(CX, X)$:
$$ \dots \to \tilde{H}^k(CX, X) \to \tilde{H}^k(CX) \to \tilde{H}^k(X) \xrightarrow{\delta} \tilde{H}^{k+1}(CX, X) \to \tilde{H}^{k+1}(CX) \to \dots $$
As established earlier, the cone $CX$ is contractible, so all its reduced [cohomology groups](@entry_id:142450) are trivial: $\tilde{H}^k(CX) = 0$ for all $k$. The [long exact sequence](@entry_id:153438) therefore breaks apart into a collection of short [exact sequences](@entry_id:151503) of the form:
$$ 0 \to \tilde{H}^k(X) \xrightarrow{\delta} \tilde{H}^{k+1}(CX, X) \to 0 $$
This means the [connecting homomorphism](@entry_id:160713) $\delta$ is an isomorphism for all $k \ge 0$. Furthermore, for a "good pair" $(CX, X)$, the [relative cohomology](@entry_id:272456) of the pair is isomorphic to the reduced cohomology of the [quotient space](@entry_id:148218), $\tilde{H}^{k+1}(CX, X) \cong \tilde{H}^{k+1}(CX/X) = \tilde{H}^{k+1}(SX)$. Combining these isomorphisms gives the celebrated **Suspension Isomorphism**:
$$ \tilde{H}^k(X; G) \cong \tilde{H}^{k+1}(SX; G) \quad \text{for all } k \ge 0. $$
This theorem provides a powerful, "dimension-shifting" tool for computation [@problem_id:1661656]. For example, the suspension of a [pointed space](@entry_id:265918) $X$ is homeomorphic to the [smash product](@entry_id:266214) $X \wedge S^1$. Using this, we can compute the cohomology of $S^2 \wedge S^1 \cong \Sigma S^2$. Given that the only non-trivial reduced cohomology of the 2-sphere is $\tilde{H}^2(S^2; \mathbb{Z}) \cong \mathbb{Z}$, the [suspension isomorphism](@entry_id:156388) immediately implies that the only non-trivial reduced cohomology of $\Sigma S^2$ is:
$$ \tilde{H}^3(\Sigma S^2; \mathbb{Z}) \cong \tilde{H}^2(S^2; \mathbb{Z}) \cong \mathbb{Z}. $$
All other reduced [cohomology groups](@entry_id:142450) are trivial [@problem_id:1668460]. Writing this theorem using ordinary cohomology would require separate, messier statements for low degrees.

#### The Cofiber Sequence and Collapsing Subspaces

For a well-behaved pair of spaces $(X, A)$ (such as a CW pair, where $A$ is a [subcomplex](@entry_id:264130) of $X$), there is a [long exact sequence](@entry_id:153438) in reduced cohomology associated to the cofiber sequence $A \to X \to X/A$:
$$ \dots \to \tilde{H}^n(X/A; G) \xrightarrow{q^*} \tilde{H}^n(X; G) \xrightarrow{i^*} \tilde{H}^n(A; G) \xrightarrow{\delta} \tilde{H}^{n+1}(X/A; G) \to \dots $$
This sequence is a fundamental computational tool. A particularly useful consequence arises when the subspace $A$ is contractible [@problem_id:1668499]. If $A$ is non-empty and contractible, then $\tilde{H}^n(A; G) = 0$ for all $n$. The [long exact sequence](@entry_id:153438) then decomposes into short [exact sequences](@entry_id:151503):
$$ 0 \to \tilde{H}^n(X/A; G) \xrightarrow{q^*} \tilde{H}^n(X; G) \to 0 $$
This implies that the map $q^*: \tilde{H}^n(X/A; G) \to \tilde{H}^n(X; G)$, induced by the [quotient map](@entry_id:140877) $q: X \to X/A$, is an [isomorphism](@entry_id:137127) for all $n$. In other words, collapsing a contractible subspace does not change the reduced cohomology of a space.

This exact sequence is also invaluable for probing the algebraic structure of the maps involved. For instance, consider a CW pair $(X, A)$ where $A \cong S^1$, the quotient $X/A \cong S^2$, and we are given $\tilde{H}^1(X; \mathbb{Z})=0$ and $\tilde{H}^2(X; \mathbb{Z}) \cong \mathbb{Z}_7$. We can use the [long exact sequence](@entry_id:153438) to determine the nature of the [connecting homomorphism](@entry_id:160713) $\delta: \tilde{H}^1(A; \mathbb{Z}) \to \tilde{H}^2(X/A; \mathbb{Z})$ [@problem_id:1668501]. Plugging the known groups into the sequence around these terms yields:
$$ \dots \to \tilde{H}^1(X; \mathbb{Z}) \to \tilde{H}^1(S^1; \mathbb{Z}) \xrightarrow{\delta} \tilde{H}^2(S^2; \mathbb{Z}) \to \tilde{H}^2(X; \mathbb{Z}) \to \tilde{H}^2(S^1; \mathbb{Z}) \to \dots $$
Substituting the group structures, this becomes:
$$ \dots \to 0 \to \mathbb{Z} \xrightarrow{\delta} \mathbb{Z} \to \mathbb{Z}_7 \to 0 \to \dots $$
From the [exactness](@entry_id:268999) of $\mathbb{Z} \xrightarrow{\delta} \mathbb{Z} \to \mathbb{Z}_7 \to 0$, we deduce that $\text{coker}(\delta) \cong \mathbb{Z}_7$. The map $\delta$ is an endomorphism of $\mathbb{Z}$, so it must be multiplication by some integer $k$. Its cokernel is $\mathbb{Z}/k\mathbb{Z}$. For $\mathbb{Z}/k\mathbb{Z} \cong \mathbb{Z}_7$, we must have $|k|=7$. By choosing an appropriate generator, we find that the map $\delta$ is, algebraically, multiplication by 7. This demonstrates how the rigid structure of the long exact sequence allows us to translate topological information into precise algebraic statements.