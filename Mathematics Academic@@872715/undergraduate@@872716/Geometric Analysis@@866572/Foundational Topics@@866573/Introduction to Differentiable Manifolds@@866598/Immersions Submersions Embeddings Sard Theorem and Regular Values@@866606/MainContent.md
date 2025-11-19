## Introduction
In [differential topology](@entry_id:157662), the study of [smooth maps between manifolds](@entry_id:190665) is of central importance. These maps are the structure-preserving functions of the smooth world, but their behavior can be complex, producing images and preimages with rich geometric features. A fundamental challenge lies in classifying this behavior and understanding the structure of the objects they create. How can we predict whether a map locally resembles an inclusion, a projection, or something more complicated? When is the [solution set](@entry_id:154326) to a system of equations a smooth manifold?

This article provides a comprehensive framework for answering these questions. It navigates through the essential tools used to analyze [smooth maps](@entry_id:203730), structured across three distinct chapters. In **Principles and Mechanisms**, we will lay the groundwork by defining the [differential of a map](@entry_id:269524) and using its rank to classify maps as immersions or [submersions](@entry_id:159709). This chapter will also introduce the crucial concepts of [regular values](@entry_id:161151) and critical values, leading to two cornerstone results: the Regular Value Theorem, which describes the structure of preimages, and Sard's Theorem, which reveals that well-behaved preimages are the norm, not the exception. Following this theoretical foundation, **Applications and Interdisciplinary Connections** will showcase the power of these ideas, demonstrating how to define manifolds implicitly as [level sets](@entry_id:151155), how [submersions](@entry_id:159709) give rise to [fiber bundles](@entry_id:154670) like the Hopf fibration, and how these concepts connect to deeper topological invariants. Finally, **Hands-On Practices** provides a set of targeted problems designed to solidify understanding through direct computation and analysis of concrete examples. By the end of this exploration, you will gain a robust understanding of how the local, linear properties of a map dictate its global geometric consequences.

## Principles and Mechanisms

The behavior of a [smooth map](@entry_id:160364) between manifolds is fundamentally determined by its local properties. By examining the map's [linear approximation](@entry_id:146101) at each point—the differential—we can classify its geometric character and understand the structure of its image and preimages. This chapter delineates the core principles governing this classification, focusing on immersions, [submersions](@entry_id:159709), [regular values](@entry_id:161151), and embeddings.

### The Differential as a Local Linearization

A [smooth map](@entry_id:160364) $f: M \to N$ between manifolds $M$ and $N$ can be approximated near any point $p \in M$ by a linear map between their tangent spaces. This linear map is the **differential** of $f$ at $p$, denoted $df_p: T_pM \to T_{f(p)}N$. Before we can analyze the consequences of this linearization, we must recall its precise definition.

Let $M$ be a [smooth manifold](@entry_id:156564) of dimension $n$. The **[tangent space](@entry_id:141028)** $T_pM$ at a point $p \in M$ can be rigorously defined as the space of all **derivations** at $p$. A derivation is an $\mathbb{R}$-linear map $D: C^\infty(M) \to \mathbb{R}$ that satisfies the Leibniz rule for products of [smooth functions](@entry_id:138942):
$$
D(\phi\psi) = D(\phi)\psi(p) + \phi(p)D(\psi)
$$
for all $\phi, \psi \in C^\infty(M)$. A crucial property of derivations is that they are local operators; the value $D(\phi)$ depends only on the behavior of the function $\phi$ in an arbitrarily small neighborhood of $p$.

Given a [smooth map](@entry_id:160364) $f: M \to N$, it induces a linear map $df_p: T_pM \to T_{f(p)}N$ between the respective tangent spaces. For a [tangent vector](@entry_id:264836) $X \in T_pM$ (which is a derivation on $C^\infty(M)$), the differential $df_p(X)$ is defined as the tangent vector at $f(p) \in N$ whose action on any [smooth function](@entry_id:158037) $\psi \in C^\infty(N)$ is given by composition:
$$
(df_p(X))(\psi) = X(\psi \circ f)
$$
This definition is well-posed because the composition $\psi \circ f$ is a smooth function on $M$, which is the domain for the derivation $X$. The map $df_p(X)$ can be shown to satisfy the properties of a derivation at $f(p)$, and the mapping $X \mapsto df_p(X)$ is linear. Thus, the differential provides a canonical way to translate tangent vectors from the domain manifold to the [codomain](@entry_id:139336) manifold [@problem_id:3052900]. The properties of this linear map, particularly its rank, form the basis for classifying the local structure of $f$.

### Local Classification via Rank: Immersions and Submersions

Let the dimensions of $M$ and $N$ be $m$ and $n$, respectively. At each point $p \in M$, the differential $df_p$ is a linear map between [vector spaces](@entry_id:136837) of dimension $m$ and $n$. The rank of $df_p$ can vary from point to point, but when it is constant, the map exhibits a remarkably uniform local structure. Two cases of constant maximal rank are of paramount importance.

#### Immersions: Local Embeddings

An **immersion** is a [smooth map](@entry_id:160364) $f: M^m \to N^n$ whose differential $df_p$ is injective at every point $p \in M$. From linear algebra, a linear map between [finite-dimensional vector spaces](@entry_id:265491) can be injective only if the dimension of the domain is less than or equal to the dimension of the codomain. Therefore, for an immersion to exist, we must have $m \le n$. Injectivity of $df_p$ is equivalent to its rank being equal to the dimension of the domain, so for an immersion, $\operatorname{rank}(df_p) = m$ for all $p \in M$.

Since the rank is constant, the **Constant Rank Theorem** applies. This powerful theorem dictates the local form of such maps. For an immersion, it specializes to the **Immersion Theorem**, which states that for any point $p \in M$, there exist smooth [coordinate charts](@entry_id:262338) around $p$ and $f(p)$ such that $f$ is locally represented by the canonical inclusion of $\mathbb{R}^m$ into $\mathbb{R}^n$:
$$
(x_1, \dots, x_m) \mapsto (x_1, \dots, x_m, 0, \dots, 0)
$$
This local form reveals the essential geometric nature of an immersion: it locally "implants" the manifold $M$ into $N$ as a smooth, uncreased [submanifold](@entry_id:262388) [@problem_id:3052901] [@problem_id:3052939].

Several key consequences follow from this local picture. First, since the canonical inclusion is locally injective, every immersion is *locally injective*. This means that for any point $p \in M$, there exists a neighborhood $U$ of $p$ on which the restriction $f|_U$ is injective. Furthermore, on a sufficiently small neighborhood $U$, the map $f|_U$ is a homeomorphism onto its image $f(U)$. An immersion that is a homeomorphism onto its image is, by definition, an **embedding**. Thus, every immersion is locally an embedding [@problem_id:3052901]. The image $f(U)$ of such a local neighborhood is itself an $m$-dimensional [embedded submanifold](@entry_id:273162) of a neighborhood of $f(p)$ in $N$ [@problem_id:3052901].

It is critical to distinguish between local and global properties. While an immersion is locally injective, it need not be globally injective. A classic example is the map $f: \mathbb{R} \to \mathbb{R}^2$ given by $f(t) = (\cos(t), \sin(t))$. Its differential is everywhere injective, so it is an immersion, but the map is clearly not globally injective as $f(t) = f(t+2\pi)$ [@problem_id:3052939]. The image is the unit circle, which wraps around and intersects itself from the perspective of the domain.

#### Submersions: Local Projections

A **submersion** is a [smooth map](@entry_id:160364) $f: M^m \to N^n$ whose differential $df_p$ is surjective at every point $p \in M$ [@problem_id:3052879]. For a [linear map](@entry_id:201112) to be surjective, the dimension of its domain must be greater than or equal to the dimension of its [codomain](@entry_id:139336). Thus, a submersion requires $m \ge n$. Surjectivity of $df_p$ is equivalent to its rank being equal to the dimension of the [codomain](@entry_id:139336), so for a submersion, $\operatorname{rank}(df_p) = n$ for all $p \in M$ [@problem_id:3052879].

Again, the Constant Rank Theorem applies, yielding the **Submersion Theorem**. This theorem asserts that for any point $p \in M$, there exist smooth [coordinate charts](@entry_id:262338) around $p$ and $f(p)$ in which the map $f$ takes the form of the canonical projection from $\mathbb{R}^m$ to $\mathbb{R}^n$:
$$
(x_1, \dots, x_m) \mapsto (x_1, \dots, x_n)
$$
Geometrically, a [submersion](@entry_id:161795) locally behaves like projecting a higher-dimensional space onto a lower-dimensional one, smoothly "flattening" the [extra dimensions](@entry_id:160819) [@problem_id:3052879] [@problem_id:3052939].

An immediate consequence of this local form is that [submersions](@entry_id:159709) are **open maps**: they map open sets in $M$ to open sets in $N$. However, this does not imply that a [submersion](@entry_id:161795) is globally surjective. For example, the inclusion of an open ball into Euclidean space is a [submersion](@entry_id:161795) (with $m=n$), but it is not surjective [@problem_id:3052879].

### The Structure of Level Sets and Regular Values

We now shift our perspective from the local behavior of the map itself to the geometric structure of its **level sets**, or **preimages**, of the form $f^{-1}(y) = \{p \in M \mid f(p) = y\}$ for some $y \in N$. The key to understanding this structure lies in the concepts of regular and critical values.

#### Regular Values and Critical Values

A point $p \in M$ is a **regular point** of $f$ if the differential $df_p$ is surjective. If $df_p$ is not surjective, $p$ is a **critical point**.

The classification is then extended to the codomain $N$. A point $y \in N$ is a **[regular value](@entry_id:188218)** if every point $p$ in its [preimage](@entry_id:150899) $f^{-1}(y)$ is a regular point. If there is even one point $p \in f^{-1}(y)$ that is a critical point, then $y$ is a **critical value**. It is essential to note that the definition of a [regular value](@entry_id:188218) is a universal quantification over the preimage set. If the [preimage](@entry_id:150899) $f^{-1}(y)$ is empty, the condition is vacuously satisfied, and $y$ is automatically a [regular value](@entry_id:188218) [@problem_id:3052936] [@problem_id:3052895].

This seemingly pedantic point has profound consequences. For instance, if $m  n$, the differential $df_p$ can never be surjective, so every point in $M$ is a critical point. Therefore, a value $y \in N$ can be a [regular value](@entry_id:188218) only if its [preimage](@entry_id:150899) is empty [@problem_id:3052895] [@problem_id:3052888].

#### Sard's Theorem: The Abundance of Regular Values

One might wonder how common [regular values](@entry_id:161151) are. Are they exceptional, or are critical values the exception? **Sard's Theorem** provides a definitive answer: for a sufficiently [smooth map](@entry_id:160364), the set of [regular values](@entry_id:161151) is "most" of the codomain.

More precisely, if $f: M^m \to N^n$ is a map of class $C^k$ with $k > \max\{m-n, 0\}$, then the set of its critical values has measure zero in $N$. The concept of a measure-zero set is well-defined on a manifold, independent of the choice of [coordinate charts](@entry_id:262338), because diffeomorphisms (like transition maps) preserve [sets of measure zero](@entry_id:157694) [@problem_id:3052923].

The implication of Sard's Theorem is powerful: the set of [regular values](@entry_id:161151) is not only non-empty but dense and has full measure in $N$ [@problem_id:3052923]. This means that for almost any point $y$ we pick in the [codomain](@entry_id:139336), its [preimage](@entry_id:150899) will consist entirely of regular points (or be empty). This allows us to study the "generic" structure of preimages by focusing on those of [regular values](@entry_id:161151).

#### The Regular Value Theorem and the Implicit Function Theorem

The central result concerning the structure of preimages is the **Regular Value Theorem** (or **Preimage Theorem**). It states that if $y \in N$ is a [regular value](@entry_id:188218) of a [smooth map](@entry_id:160364) $f: M^m \to N^n$, then the preimage $f^{-1}(y)$ is a properly [embedded submanifold](@entry_id:273162) of $M$ of dimension $m-n$ [@problem_id:3052879].

The proof of this theorem is a beautiful application of the Submersion Theorem. The condition that $y$ is a [regular value](@entry_id:188218) means that $f$ is a [submersion](@entry_id:161795) at every point of the preimage $f^{-1}(y)$. At each such point $p$, we can find [local coordinates](@entry_id:181200) $(u_1, \dots, u_m)$ for $M$ and coordinates for $N$ such that $f$ is the projection $(u_1, \dots, u_m) \mapsto (u_1, \dots, u_n)$. The preimage of $y$ (which corresponds to the origin in the [local coordinates](@entry_id:181200) for $N$) is then locally defined by the equations $u_1 = \dots = u_n = 0$. This is precisely the definition of a local coordinate slice for an $(m-n)$-dimensional [submanifold](@entry_id:262388) [@problem_id:3052895].

This theorem should feel familiar, as it is a vast generalization of the **Implicit Function Theorem** from [multivariable calculus](@entry_id:147547). Consider a [smooth function](@entry_id:158037) $F: \mathbb{R}^{m+n} \to \mathbb{R}^n$ and the level set $F^{-1}(0)$. The Implicit Function Theorem states that if at a point $(x_0, y_0) \in F^{-1}(0)$ the partial derivative matrix $D_y F$ with respect to the last $n$ variables is invertible, we can locally write $y$ as a [smooth function](@entry_id:158037) of $x$, i.e., $y=g(x)$. This means the level set is locally the [graph of a function](@entry_id:159270).

From the manifold perspective, the invertibility of the $n \times n$ matrix $D_y F$ guarantees that the full $(m+n) \times n$ Jacobian matrix $DF = [D_x F \mid D_y F]$ has rank $n$, meaning it is surjective. This is exactly the condition for $(x_0, y_0)$ to be a regular point of $F$. If this holds for all points in the [level set](@entry_id:637056), then $0$ is a [regular value](@entry_id:188218). The Regular Value Theorem then asserts that $F^{-1}(0)$ is a smooth submanifold of dimension $(m+n) - n = m$. The Implicit Function Theorem provides the more explicit description that this $m$-dimensional manifold can be locally parameterized by the first $m$ coordinates, i.e., it is a graph [@problem_id:3052918].

#### A Unifying View: Transversality

The concept of a [regular value](@entry_id:188218) is a special case of a more general and unifying idea: **[transversality](@entry_id:158669)**. A [smooth map](@entry_id:160364) $f: M \to N$ is said to be transverse to an [embedded submanifold](@entry_id:273162) $S \subset N$ if for every point $p \in f^{-1}(S)$, the tangent spaces of the image of $f$ and of $S$ span the [tangent space](@entry_id:141028) of $N$:
$$
\text{im}(df_p) + T_{f(p)}S = T_{f(p)}N
$$
If we consider the case where the [submanifold](@entry_id:262388) $S$ is just a single point, $S = \{y\}$, then $S$ is a 0-dimensional submanifold and its [tangent space](@entry_id:141028) $T_yS$ is the [zero vector](@entry_id:156189) space $\{0\}$. The [transversality condition](@entry_id:261118) then simplifies to $\text{im}(df_p) = T_yN$. This is precisely the definition of [surjectivity](@entry_id:148931) for $df_p$. Therefore, a map $f$ is transverse to the point-submanifold $\{y\}$ if and only if $y$ is a [regular value](@entry_id:188218) of $f$ [@problem_id:3052888]. This perspective shows that the Regular Value Theorem is the foundational instance of the more general Transversality Theorem, which describes the structure of the preimage $f^{-1}(S)$ for any [submanifold](@entry_id:262388) $S$ to which $f$ is transverse.

### Global Geometry: Embeddings and Proper Maps

While immersions and [submersions](@entry_id:159709) are defined by local conditions, an **embedding** is a global concept. A [smooth map](@entry_id:160364) $f: M \to N$ is an embedding if it is both an immersion and a [homeomorphism](@entry_id:146933) onto its image. This means it is globally injective and faithfully represents the topology of $M$ as a subspace of $N$.

A canonical way to construct [embeddings](@entry_id:158103) is through the [graph of a function](@entry_id:159270). For any [smooth function](@entry_id:158037) $f: \mathbb{R} \to \mathbb{R}$, the associated graph map $F: \mathbb{R} \to \mathbb{R}^2$ given by $F(x) = (x, f(x))$ is always a [smooth embedding](@entry_id:637480). It is an immersion because its differential, represented by the vector $(1, f'(x))$, is never the zero vector. It is a homeomorphism onto its image because it is a [continuous bijection](@entry_id:198258) whose inverse, $(x, f(x)) \mapsto x$, is the restriction of a continuous projection map [@problem_id:3052928].

An important property for ensuring good global behavior is **properness**. A map $F: M \to N$ is **proper** if the preimage of every compact set in $N$ is a [compact set](@entry_id:136957) in $M$. A key topological fact is that a [proper map](@entry_id:158587) between locally compact Hausdorff spaces (such as [smooth manifolds](@entry_id:160799)) is a **[closed map](@entry_id:150357)**, meaning the image of any closed set is a [closed set](@entry_id:136446).

An embedding that is also a [proper map](@entry_id:158587) is called a **proper embedding**. The image of a proper embedding is always a closed submanifold of the [codomain](@entry_id:139336). This provides a powerful tool for constructing closed submanifolds. For instance, if a [smooth function](@entry_id:158037) $f: \mathbb{R} \to \mathbb{R}$ is proper (which is equivalent to $|f(x)| \to \infty$ as $|x| \to \infty$), then its graph map $F(x)=(x,f(x))$ is a [proper map](@entry_id:158587). As a [proper map](@entry_id:158587), $F$ is a [closed map](@entry_id:150357), and thus its image $F(\mathbb{R})$—the graph itself—is a closed subset of $\mathbb{R}^2$ [@problem_id:3052928]. An example is $f(x)=x^3+x$, which is proper, yielding a [closed graph](@entry_id:154162) in $\mathbb{R}^2$. In contrast, $g(x) = \arctan(x)$ is not a proper function. While its graph is also a [closed set](@entry_id:136446) in $\mathbb{R}^2$, this cannot be concluded from the properness of the map, underscoring that properness is a sufficient, but not always necessary, condition for the image to be a [closed set](@entry_id:136446) [@problem_id:3052928]. Finally, it is worth noting that for any smooth $f$, the graph map $F$ is not only an embedding but also a [diffeomorphism](@entry_id:147249) from $\mathbb{R}$ to its image, the graph $F(\mathbb{R})$. Since the domain and codomain have the same dimension (one), this also means $F$ is a submersion onto its image [@problem_id:3052928].