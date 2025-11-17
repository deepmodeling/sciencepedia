## Introduction
Classical algebraic topology offers a powerful lens for understanding the structure of spaces, with standard [cohomology theory](@entry_id:270863) providing deep insights, particularly for compact manifolds. The celebrated Poincaré [duality theorem](@entry_id:137804), for instance, reveals a beautiful symmetry in the algebraic invariants of these well-behaved spaces. However, when our investigation shifts to [non-compact spaces](@entry_id:273664)—such as Euclidean space, an open cylinder, or the complement of a knot—these classical tools lose much of their descriptive power. The ordinary cohomology of a contractible space like $\mathbb{R}^n$ is trivial, telling us nothing about its intrinsic n-dimensional nature. This limitation highlights a significant gap in our topological toolkit, creating the need for a new theory tailored to the unique challenges of non-compactness.

This article introduces **cohomology with compact supports**, the algebraic framework designed precisely to fill this gap. It captures the global, large-scale properties of [non-compact spaces](@entry_id:273664) and restores a powerful form of duality. Over the next three chapters, you will gain a comprehensive understanding of this essential theory.
- In **Principles and Mechanisms**, we will construct cohomology with compact supports from first principles, explore its fundamental properties, and prove the generalized Poincaré [duality theorem](@entry_id:137804) that forms its theoretical core.
- In **Applications and Interdisciplinary Connections**, we will see the theory in action, using it to compute invariants for key [non-compact spaces](@entry_id:273664) and exploring its deep connections to [differential geometry](@entry_id:145818), knot theory, and Lie groups.
- Finally, **Hands-On Practices** will provide opportunities to solidify your knowledge by working through guided problems that highlight the theory's computational power and subtleties.

We begin our journey by examining the motivations for this new theory and defining its fundamental building blocks.

## Principles and Mechanisms

In the study of compact manifolds, algebraic topology provides powerful tools that relate the geometric structure of a space to its algebraic invariants. Standard [cohomology theory](@entry_id:270863), for instance, culminates in the celebrated Poincaré [duality theorem](@entry_id:137804), which reveals a profound symmetry in the Betti numbers of a compact, [orientable manifold](@entry_id:276936). However, when we transition our focus to [non-compact spaces](@entry_id:273664), such as Euclidean space or surfaces with punctures, these familiar tools often lose their efficacy. The standard cohomology groups of a contractible space like $\mathbb{R}^n$, for example, are trivial in positive degrees, telling us little about its $n$-dimensional nature. This chapter introduces **cohomology with compact supports**, a modification of ordinary cohomology designed precisely to capture the large-scale topology of [non-compact spaces](@entry_id:273664) and to restore a version of Poincaré duality in this broader context.

### The Motivation: Failure of Standard Duality

For a compact, orientable $n$-manifold $M$, Poincaré duality establishes an isomorphism $H^k(M) \cong H_{n-k}(M)$. The failure of this classical result for [non-compact manifolds](@entry_id:262738) is the primary motivation for developing a new theory. Consider the simplest [non-compact manifold](@entry_id:636943), the real line $\mathbb{R}$. As a 1-manifold, a hypothetical Poincaré duality would relate $H^1(\mathbb{R})$ and $H_0(\mathbb{R})$. However, because $\mathbb{R}$ is path-connected, its 0-th homology group is $H_0(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$. On the other hand, since $\mathbb{R}$ is contractible, its first cohomology group is trivial, $H^1(\mathbb{R}; \mathbb{Z}) = 0$. Clearly, $\mathbb{Z} \not\cong 0$, so the duality fails [@problem_id:1666082].

From the perspective of de Rham cohomology, the failure is rooted in the very construction of the duality pairing. For a compact orientable $n$-manifold $M$, the non-degenerate pairing between cohomology classes is given by integration:
$$ \langle [\omega], [\eta] \rangle = \int_M \omega \wedge \eta $$
where $[\omega] \in H^k(M)$ and $[\eta] \in H^{n-k}(M)$. This pairing is well-defined because the integral of any smooth form over a [compact domain](@entry_id:139725) is finite. If we attempt to apply this definition to a [non-compact manifold](@entry_id:636943) like $\mathbb{R}^n$, we immediately face a problem: the integral of $\omega \wedge \eta$ over the non-[compact domain](@entry_id:139725) $\mathbb{R}^n$ is not guaranteed to converge [@problem_id:1529975]. To ensure convergence, we must impose stricter conditions on the differential forms we integrate—namely, that they vanish outside of some [compact set](@entry_id:136957). This key observation is the gateway to our new theory.

### Defining Cohomology with Compact Supports

The most direct way to construct a [cohomology theory](@entry_id:270863) that addresses the issue of non-compactness is to build it from [cochains](@entry_id:159583) that are non-zero only on a compact part of the space.

#### The Subcomplex of Compactly Supported Cochains

Let $X$ be a topological space and $C^k(X; G)$ be the group of singular $k$-[cochains](@entry_id:159583) with coefficients in an abelian group $G$. For a cochain $\phi \in C^k(X; G)$, its **support**, denoted $\text{supp}(\phi)$, is defined as the smallest closed subset $A \subseteq X$ such that $\phi$ vanishes on any singular $k$-chain whose image lies in the complement $X \setminus A$. A cochain $\phi$ is said to have **[compact support](@entry_id:276214)** if its support is a compact set.

The set of all $k$-[cochains](@entry_id:159583) with [compact support](@entry_id:276214) forms a subgroup of $C^k(X; G)$, which we denote by $C_c^k(X; G)$. For these groups to form a [cochain](@entry_id:275805) complex, the [coboundary operator](@entry_id:162168) $\delta: C^k(X; G) \to C^{k+1}(X; G)$ must restrict to a map $\delta: C_c^k(X; G) \to C_c^{k+1}(X; G)$. This is indeed the case. The support of a coboundary $\delta\phi$ is always a subset of the support of the original cochain $\phi$, i.e., $\text{supp}(\delta\phi) \subseteq \text{supp}(\phi)$. Consequently, if $\phi$ has [compact support](@entry_id:276214), so must $\delta\phi$.

For example, consider the 0-[cochain](@entry_id:275805) $\phi \in C^0(\mathbb{R}^n; \mathbb{Z})$ defined by the [characteristic function](@entry_id:141714) of the closed unit ball $D$: $\phi(p) = 1$ if $p \in D$ and $\phi(p) = 0$ otherwise. The support of $\phi$ is $D$, which is compact. The coboundary $\delta\phi$ is a 1-cochain whose value on a singular 1-[simplex](@entry_id:270623) $\sigma: \Delta^1 \to \mathbb{R}^n$ is $(\delta\phi)(\sigma) = \phi(\sigma(1)) - \phi(\sigma(0))$. This value can be non-zero only if one endpoint of the path $\sigma$ is inside $D$ and the other is outside, which requires the path to cross the boundary of the ball. It can be shown rigorously that the support of $\delta\phi$ is precisely the unit sphere $S^{n-1}$, which is also a compact set [@problem_id:1641331].

Since $(C_c^*(X; G), \delta)$ is a [subcomplex](@entry_id:264130) of the standard singular cochain complex, we can define the **$k$-th cohomology group with compact supports**, denoted $H_c^k(X; G)$, as the cohomology of this [subcomplex](@entry_id:264130):
$$ H_c^k(X; G) = \frac{\ker(\delta: C_c^k(X; G) \to C_c^{k+1}(X; G))}{\text{im}(\delta: C_c^{k-1}(X; G) \to C_c^k(X; G))} $$

#### The Direct Limit Definition

An alternative, and often more powerful, definition of cohomology with compact supports is given as a direct limit of [relative cohomology](@entry_id:272456) groups. For a locally compact Hausdorff space $X$, we define:
$$ H_c^k(X; G) = \varinjlim_{K} H^k(X, X \setminus K; G) $$
Here, the limit is taken over the [directed set](@entry_id:155049) of all compact subsets $K$ of $X$, ordered by inclusion. Intuitively, this definition captures cohomology classes that "live" on some compact subset $K$ and "vanish at infinity" (i.e., vanish on $X \setminus K$). As we take the limit over larger and larger [compact sets](@entry_id:147575) $K$ that exhaust $X$, we capture all possible such phenomena.

This definition provides immediate insight into the behavior of $H_c^*$ on [compact spaces](@entry_id:155073). If the space $X$ is itself compact, then $X$ can be chosen as one of the [compact sets](@entry_id:147575) $K$ in the directed system. In fact, it is the [maximal element](@entry_id:274677), or [terminal object](@entry_id:151050), of the [directed set](@entry_id:155049). A property of direct limits is that if the indexing set has a [terminal object](@entry_id:151050), the limit is isomorphic to the group at that object. Therefore, for compact $X$, the limit collapses:
$$ H_c^k(X; G) \cong H^k(X, X \setminus X; G) = H^k(X, \emptyset; G) \cong H^k(X; G) $$
This shows that for [compact spaces](@entry_id:155073), such as the torus $T^2$, cohomology with compact supports is naturally isomorphic to ordinary cohomology [@problem_id:1641386]. For [non-compact spaces](@entry_id:273664), however, the two theories diverge significantly.

### Fundamental Properties and Computations

The relationship between $H_c^*(X)$ and $H^*(X)$ is governed by the natural inclusion of [cochain](@entry_id:275805) complexes $i: C_c^*(X) \hookrightarrow C^*(X)$. This induces a homomorphism $i^*: H_c^k(X) \to H^k(X)$. A central question is to understand the nature of this map.

#### Distinction from Ordinary Cohomology

The map $i^*: H_c^k(X) \to H^k(X)$ is neither injective nor surjective in general. A cohomology class in $H_c^k(X)$ can become trivial in $H^k(X)$, and a class in $H^k(X)$ might not be representable by a cocycle with [compact support](@entry_id:276214).

A striking example illustrates this difference. Consider the 1-cochain $\phi$ on $\mathbb{R}$ defined by $\phi(\sigma) = \sigma(1) - \sigma(0)$ for any singular 1-simplex $\sigma$. This cochain is a coboundary in the standard theory, as $\phi = \delta f$ for the 0-[cochain](@entry_id:275805) $f(x)=x$. Thus, its class $[\phi]$ in $H^1(\mathbb{R}; \mathbb{R})$ is zero. However, $f(x)=x$ does not have [compact support](@entry_id:276214). Can we find a different 0-cochain $g$ with [compact support](@entry_id:276214) such that $\phi = \delta g$? Suppose such a $g$ exists, with its support contained in some interval $[-M, M]$. Let's take a simplex $\sigma$ with endpoints $a = -2M$ and $b = 2M$. Then $(\delta g)(\sigma) = g(b) - g(a) = 0 - 0 = 0$. But $\phi(\sigma) = b-a = 4M \neq 0$. This contradiction shows that $\phi$ cannot be the coboundary of any compactly supported 0-[cochain](@entry_id:275805). Therefore, its class $[\phi]_c$ in $H_c^1(\mathbb{R}; \mathbb{R})$ is non-zero [@problem_id:1641346]. This demonstrates that $H_c^1(\mathbb{R}) \not\cong H^1(\mathbb{R})$, and in fact, we have found a non-trivial element in $H_c^1(\mathbb{R})$.

#### Functoriality and Proper Maps

A key feature of ordinary cohomology is its [functoriality](@entry_id:150069): any continuous map $f: X \to Y$ induces a pullback homomorphism $f^*: H^k(Y) \to H^k(X)$. This property is more restricted for cohomology with compact supports. If $\psi \in C_c^k(Y)$ has [compact support](@entry_id:276214) $K \subset Y$, its pullback $f^*\psi$ on $X$ is supported within the [preimage](@entry_id:150899) $f^{-1}(K)$. For $f^*\psi$ to also have [compact support](@entry_id:276214), we require that $f^{-1}(K)$ be compact. This must hold for *any* compact $K \subset Y$.

This requirement defines a special class of functions. A [continuous map](@entry_id:153772) $f: X \to Y$ is called a **[proper map](@entry_id:158587)** if the [preimage](@entry_id:150899) of every compact set in $Y$ is a [compact set](@entry_id:136957) in $X$. The fundamental result on [functoriality](@entry_id:150069) is that a continuous map $f: X \to Y$ between locally compact Hausdorff spaces induces a well-defined homomorphism $f^*: H_c^k(Y) \to H_c^k(X)$ if and only if $f$ is a [proper map](@entry_id:158587).

For instance, the map $f: \mathbb{R} \to \mathbb{R}$ given by $f(x) = x^3 - x$ is proper. The limit of $|f(x)|$ as $|x| \to \infty$ is infinity, which ensures that the preimage of any bounded (hence compact) set in the [codomain](@entry_id:139336) must be a bounded (and closed, hence compact) set in the domain. Therefore, this map induces a valid homomorphism on cohomology with compact supports [@problem_id:1641375].

In contrast, consider the projection map $p: \mathbb{R}^2 \to \mathbb{R}$ given by $p(x, y) = x$. This map is not proper. The [preimage](@entry_id:150899) of the compact interval $K = [0, 1] \subset \mathbb{R}$ is the set $p^{-1}(K) = [0, 1] \times \mathbb{R}$, which is an infinite strip and not compact in $\mathbb{R}^2$. Because $p$ is not proper, it does not induce a canonical pullback homomorphism $p^*: H_c^k(\mathbb{R}) \to H_c^k(\mathbb{R}^2)$ [@problem_id:1641328].

#### The Long Exact Sequence of a Pair

One of the most powerful computational tools for cohomology with compact supports arises from considering a space $X$ decomposed into an open subset $U$ and its closed complement $F = X \setminus U$. For such a pair, there is a long exact sequence:
$$ \dots \to H_c^k(U; G) \to H_c^k(X; G) \to H_c^k(F; G) \to H_c^{k+1}(U; G) \to \dots $$
This sequence allows us to compute the cohomology of one space if we know it for the other two.

Let's use this sequence to compute the compactly supported Betti numbers of $Y = \mathbb{R} \setminus [0, 1]$. We choose $X = \mathbb{R}$, the open set $U = Y$, and the closed complement $F = [0, 1]$. We need the [cohomology groups](@entry_id:142450) for $X$ and $F$. We have previously seen that $H_c^1(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$ and all other groups are zero. For the [compact space](@entry_id:149800) $F = [0, 1]$, we have $H_c^k(F) \cong H^k(F)$. Since $[0, 1]$ is contractible, $H^0([0, 1]; \mathbb{Z}) \cong \mathbb{Z}$ and its higher cohomology groups are zero. Plugging these into the [long exact sequence](@entry_id:153438) [@problem_id:1641368]:
$$ \dots \to H_c^0(X) \to H_c^0(F) \to H_c^1(U) \to H_c^1(X) \to H_c^1(F) \to \dots $$
$$ \dots \to 0 \to \mathbb{Z} \to H_c^1(Y) \to \mathbb{Z} \to 0 \to \dots $$
This yields a [short exact sequence](@entry_id:137930) of abelian groups:
$$ 0 \to \mathbb{Z} \to H_c^1(Y; \mathbb{Z}) \to \mathbb{Z} \to 0 $$
From this sequence, we can deduce that the rank of $H_c^1(Y; \mathbb{Z})$ is $1+1=2$. Furthermore, a 0-[cocycle](@entry_id:200749) with [compact support](@entry_id:276214) on a non-compact, connected space must be zero. Since $Y$ consists of two non-compact components, $(-\infty, 0)$ and $(1, \infty)$, we have $H_c^0(Y; \mathbb{Z})=0$. Thus, the compactly supported Betti numbers for $Y$ are $h_c^0=0$ and $h_c^1=2$.

### Poincaré Duality for Non-Compact Manifolds

The primary triumph of cohomology with compact supports is that it provides the correct framework for extending Poincaré duality to [non-compact manifolds](@entry_id:262738).

**Theorem (Poincaré Duality for Non-Compact Manifolds):** If $M$ is a connected, orientable $n$-dimensional manifold, then for any integer $k$ and any coefficient group $G$, there is an isomorphism:
$$ H_c^k(M; G) \cong H_{n-k}(M; G) $$

Let's return to our motivating example, $M=\mathbb{R}$. This is a connected, orientable 1-manifold. The [duality theorem](@entry_id:137804) predicts an [isomorphism](@entry_id:137127) $H_c^1(\mathbb{R}; \mathbb{Z}) \cong H_{1-1}(\mathbb{R}; \mathbb{Z}) = H_0(\mathbb{R}; \mathbb{Z})$. Since $\mathbb{R}$ is path-connected, $H_0(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$. The theorem therefore implies $H_c^1(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$, which perfectly matches the result we derived from the definition of a coboundary with [compact support](@entry_id:276214) [@problem_id:1666082]. The theory is consistent.

A foundational calculation in the subject is determining the cohomology with compact supports for Euclidean space $\mathbb{R}^n$. Using the direct limit definition and excision, one can show that for $R>0$, $H^k(\mathbb{R}^n, \mathbb{R}^n \setminus \overline{B_R}) \cong \tilde{H}^{k-1}(S^{n-1})$. The direct limit of these groups as $R \to \infty$ stabilizes, yielding:
$$ H_c^k(\mathbb{R}^n; \mathbb{Z}) \cong \begin{cases} \mathbb{Z}  \text{if } k=n \\ 0  \text{if } k \neq n \end{cases} $$
This result [@problem_id:1641388] is profoundly satisfying: unlike ordinary cohomology, $H_c^*$ correctly identifies the dimension of Euclidean space, assigning it a single non-[trivial group](@entry_id:151996) in top dimension.

This result can also be seen through another important lens. For any locally compact Hausdorff space $X$, its cohomology with compact supports is isomorphic to the [reduced cohomology](@entry_id:268050) of its [one-point compactification](@entry_id:153786) $X^+$. The [one-point compactification](@entry_id:153786) of $\mathbb{R}^n$ is the $n$-sphere, $S^n$. Therefore,
$$ H_c^k(\mathbb{R}^n) \cong \tilde{H}^k((\mathbb{R}^n)^+) \cong \tilde{H}^k(S^n) $$
This immediately gives the same result, as the [reduced cohomology](@entry_id:268050) of $S^n$ is $\mathbb{Z}$ in degree $n$ and trivial otherwise.

As a final illustration of the theorem's power, let us compute the rank of the first [compactly supported cohomology](@entry_id:634085) group of $X_{g,m}$, an [orientable surface](@entry_id:274245) of genus $g$ with $m \ge 1$ points removed. As $X_{g,m}$ is a connected, orientable [2-manifold](@entry_id:152719), Poincaré duality gives us an [isomorphism](@entry_id:137127) $H_c^1(X_{g,m}; \mathbb{Z}) \cong H_{2-1}(X_{g,m}; \mathbb{Z}) = H_1(X_{g,m}; \mathbb{Z})$. We can find the rank of this homology group, $b_1$, using the Euler characteristic. The Euler characteristic of the closed surface $S_g$ is $2-2g$. Removing $m$ points gives $\chi(X_{g,m}) = 2-2g-m$. For a connected [2-manifold](@entry_id:152719), $\chi = b_0 - b_1 + b_2$. Since $X_{g,m}$ is connected, $b_0=1$. Since it is non-compact, its top homology $H_2$ is trivial, so $b_2=0$. This gives $2-2g-m = 1-b_1$, which implies that $b_1 = 2g+m-1$. By duality, this is also the rank of the first cohomology group with compact supports [@problem_id:1664185]. This calculation demonstrates how cohomology with compact supports provides a crucial bridge between the geometry of [non-compact manifolds](@entry_id:262738) and their fundamental algebraic invariants.