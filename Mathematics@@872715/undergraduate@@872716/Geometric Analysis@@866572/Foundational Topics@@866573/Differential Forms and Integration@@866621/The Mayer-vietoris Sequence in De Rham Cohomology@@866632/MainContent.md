## Introduction
De Rham cohomology provides a powerful lens through which to study the underlying topological structure of [smooth manifolds](@entry_id:160799). However, computing the cohomology groups directly from their definition as a quotient of closed by [exact differential](@entry_id:138691) forms can be an intractable task for all but the simplest spaces. This presents a significant challenge: how can we calculate these crucial [topological invariants](@entry_id:138526) for [complex manifolds](@entry_id:159076)? The answer lies in a "[divide and conquer](@entry_id:139554)" strategy, and the most potent tool for this purpose is the Mayer-Vietoris sequence.

This article addresses the problem of computation by introducing the Mayer-Vietoris sequence, an algebraic machine that elegantly connects the cohomology of a manifold to the cohomology of its simpler, overlapping open subsets. By understanding this relationship, we can deconstruct complex spaces, compute the cohomology of the pieces, and then algebraically reassemble the information to deduce the cohomology of the whole.

Over the next three chapters, you will gain a comprehensive understanding of this essential technique. First, in "Principles and Mechanisms," we will build the sequence from the ground up, starting with differential forms and proving its existence and key properties. Then, in "Applications and Interdisciplinary Connections," we will put the theory into practice, using the sequence to perform classic computations for spheres and tori, and exploring its links to analysis and physics. Finally, "Hands-On Practices" will provide a chance to apply and solidify your knowledge through guided problems.

## Principles and Mechanisms

The preceding chapter introduced the de Rham cohomology groups $H^k_{\mathrm{dR}}(M)$ as topological invariants of a smooth manifold $M$. While their definition as the quotient of closed forms by [exact forms](@entry_id:269145) is elegant, direct computation from this definition can be formidable. A central challenge in algebraic topology is to develop tools that allow for the computation of these invariants for complex spaces by decomposing them into simpler, more manageable components. The Mayer-Vietoris sequence is arguably the most powerful such tool for de Rham cohomology. It provides an algebraic machine that precisely relates the cohomology of a manifold $M$ to the cohomologies of two open subsets $U$ and $V$ that cover it, and the cohomology of their intersection $U \cap V$. This chapter elucidates the principles and construction of this sequence.

### The Short Exact Sequence of de Rham Complexes

The foundation of the Mayer-Vietoris sequence lies not in cohomology itself, but one level deeper, in the algebraic structure of the [differential forms](@entry_id:146747) on the manifold and its subsets. This structure is a **[short exact sequence](@entry_id:137930) of [cochain](@entry_id:275805) complexes**. Let us construct it step by step.

Let $M$ be a [smooth manifold](@entry_id:156564), and let $U, V \subset M$ be two open subsets such that $M = U \cup V$. For any integer $k \ge 0$, we can consider the [vector spaces](@entry_id:136837) of smooth $k$-forms on these sets: $\Omega^k(M)$, $\Omega^k(U)$, $\Omega^k(V)$, and $\Omega^k(U \cap V)$.

#### The Restriction and Difference Maps

We can define two natural linear maps that connect these spaces. First, a map $i: \Omega^k(M) \to \Omega^k(U) \oplus \Omega^k(V)$ is given by restricting a global form on $M$ to the subsets $U$ and $V$. If $i_U: U \hookrightarrow M$ and $i_V: V \hookrightarrow M$ are the inclusion maps, this restriction is formally the pullback by these inclusions. We define $i$ as:
$$ i(\omega) = (i_U^*\omega, i_V^*\omega) = (\omega|_U, \omega|_V) $$
for any $\omega \in \Omega^k(M)$.

Second, a map $j: \Omega^k(U) \oplus \Omega^k(V) \to \Omega^k(U \cap V)$ takes a pair of forms, one on $U$ and one on $V$, and maps them to the difference of their restrictions on the overlap $U \cap V$. If $j_U: U \cap V \hookrightarrow U$ and $j_V: U \cap V \hookrightarrow V$ are the inclusions, we define $j$ as:
$$ j(\alpha, \beta) = j_U^*\alpha - j_V^*\beta = \alpha|_{U \cap V} - \beta|_{U \cap V} $$
for any $(\alpha, \beta) \in \Omega^k(U) \oplus \Omega^k(V)$.

These maps fit into a sequence for each degree $k$:
$$ 0 \longrightarrow \Omega^k(M) \xrightarrow{i} \Omega^k(U) \oplus \Omega^k(V) \xrightarrow{j} \Omega^k(U \cap V) \longrightarrow 0 $$
The term "[short exact sequence](@entry_id:137930)" means that at each position, the image of the incoming map is precisely the kernel of the outgoing map. Proving this exactness is a crucial step that relies on a fundamental tool of [analysis on manifolds](@entry_id:637756): the **partition of unity** [@problem_id:3072121].

#### The Gluing Lemma and Exactness

For a smooth [paracompact manifold](@entry_id:162090) $M$ (a condition satisfied by all Hausdorff, second-countable manifolds) and an [open cover](@entry_id:140020) $\{U, V\}$, there exists a **smooth [partition of unity](@entry_id:141893) subordinate to the cover**. This is a pair of smooth functions, $\varphi_U, \varphi_V: M \to [0,1]$, such that the support of $\varphi_U$ is contained in $U$, the support of $\varphi_V$ is contained in $V$, and $\varphi_U(x) + \varphi_V(x) = 1$ for all $x \in M$ [@problem_id:3072121].

Let us now prove that the sequence is exact.

1.  **Exactness at $\Omega^k(M)$**: The map $i$ is injective. If $i(\omega) = (0, 0)$, then $\omega|_U = 0$ and $\omega|_V = 0$. Since $U$ and $V$ cover $M$, a form that is zero on both sets must be zero everywhere. Thus, $\ker(i) = \{0\}$, which is the image of the map from the initial $0$.

2.  **Exactness at $\Omega^k(U) \oplus \Omega^k(V)$**: We must show $\operatorname{im}(i) = \ker(j)$.
    -   ($\subseteq$): If $(\alpha, \beta) \in \operatorname{im}(i)$, then $\alpha = \omega|_U$ and $\beta = \omega|_V$ for some global form $\omega$. Then $j(\alpha, \beta) = \omega|_{U \cap V} - \omega|_{U \cap V} = 0$. So $\operatorname{im}(i) \subseteq \ker(j)$.
    -   ($\supseteq$): This is the "gluing lemma" for forms. Suppose $(\alpha, \beta) \in \ker(j)$, meaning $\alpha \in \Omega^k(U)$, $\beta \in \Omega^k(V)$, and they are compatible on the overlap: $\alpha|_{U \cap V} = \beta|_{U \cap V}$. We can use a [partition of unity](@entry_id:141893) $\{\varphi_U, \varphi_V\}$ to "glue" them into a single global form $\omega$ on $M$. We define $\omega$ as the sum of two globally defined forms: one that is $\varphi_V \alpha$ on $U$ and zero elsewhere, and another that is $\varphi_U \beta$ on $V$ and zero elsewhere. More formally, if we define $\tilde{\alpha}$ on $M$ to be the extension of $\varphi_V \alpha$ by zero outside the support of $\varphi_V$, and $\tilde{\beta}$ on $M$ to be the extension of $\varphi_U \beta$ by zero outside the support of $\varphi_U$, then $\omega = \tilde{\alpha} + \tilde{\beta}$ is a well-defined global smooth form. One can check that this $\omega$ has the desired property: $\omega|_U = \alpha$ and $\omega|_V = \beta$. This shows that any compatible pair $(\alpha, \beta)$ comes from a global form, so $\ker(j) \subseteq \operatorname{im}(i)$ [@problem_id:3072088]. This demonstrates that compatibility on the overlap is the necessary and [sufficient condition](@entry_id:276242) for gluing local forms into a global one.

3.  **Exactness at $\Omega^k(U \cap V)$**: The map $j$ is surjective. For any form $\eta \in \Omega^k(U \cap V)$, we need to find a pair $(\alpha, \beta)$ such that $j(\alpha, \beta) = \eta$. Again, using a [partition of unity](@entry_id:141893) $\{\varphi_U, \varphi_V\}$, we can construct such a pair. Define $\alpha$ to be the form $\varphi_V \eta$ on $U \cap V$, extended by zero to all of $U$. Define $\beta$ to be the form $-\varphi_U \eta$ on $U \cap V$, extended by zero to all of $V$. These extensions are smooth. Then on $U \cap V$, their difference is $\alpha - \beta = \varphi_V \eta - (-\varphi_U \eta) = (\varphi_U + \varphi_V)\eta = \eta$. Thus, $j$ is surjective [@problem_id:3072112].

Since the [exterior derivative](@entry_id:161900) $d$ commutes with restriction, the maps $i$ and $j$ are **[chain maps](@entry_id:268209)**, meaning $d \circ i = (d \oplus d) \circ i$ and $d \circ j = j \circ (d \oplus d)$. Therefore, we have established the existence of a [short exact sequence](@entry_id:137930) of cochain complexes.

### The Long Exact Sequence in Cohomology

A fundamental theorem of [homological algebra](@entry_id:155139) states that any [short exact sequence](@entry_id:137930) of [cochain](@entry_id:275805) complexes gives rise to a **[long exact sequence in cohomology](@entry_id:266961)**. Applying this theorem to the sequence we just constructed yields the Mayer-Vietoris sequence for de Rham cohomology:
$$ \cdots \to H^k(M) \xrightarrow{i^*} H^k(U) \oplus H^k(V) \xrightarrow{j^*} H^k(U \cap V) \xrightarrow{\delta} H^{k+1}(M) \to \cdots $$
This sequence is the central computational tool. Its power comes from the properties of its maps, which we now describe in terms of their actions on cohomology classes [@problem_id:3072141].

#### The Induced Maps on Cohomology

-   **The Restriction Map $i^*$**: The map $i^*: H^k(M) \to H^k(U) \oplus H^k(V)$ is induced by the [cochain](@entry_id:275805) map $i$. It takes the [cohomology class](@entry_id:263961) of a closed form $\omega$ on $M$ and maps it to the pair of classes represented by the restrictions of $\omega$ to $U$ and $V$:
    $$ i^*([\omega]) = ([\omega|_U], [\omega|_V]) $$
    This is well-defined because the restriction of a closed form is closed, and the restriction of an exact form is exact.

-   **The Difference Map $j^*$**: Similarly, the map $j^*: H^k(U) \oplus H^k(V) \to H^k(U \cap V)$ is induced by $j$. It takes a pair of cohomology classes $([\alpha], [\beta])$ and maps them to the class of the difference of their representatives on the intersection:
    $$ j^*([\alpha], [\beta]) = [\alpha|_{U \cap V} - \beta|_{U \cap V}] $$

#### The Connecting Homomorphism

The most subtle and powerful map in the sequence is the **[connecting homomorphism](@entry_id:160713)**, $\delta: H^k(U \cap V) \to H^{k+1}(M)$. It increases the degree by one and is constructed via a procedure known as a "diagram chase" or the "snake lemma." Let's trace its construction [@problem_id:3072087] [@problem_id:3072108].

1.  **Start with a class**: Take a [cohomology class](@entry_id:263961) $[ \eta ] \in H^k(U \cap V)$. Let $\eta$ be a closed $k$-form on $U \cap V$ that represents this class, so $d\eta = 0$.

2.  **Lift to $U$ and $V$**: Since the cochain map $j: \Omega^k(U) \oplus \Omega^k(V) \to \Omega^k(U \cap V)$ is surjective, we can find a pair of $k$-forms $(\alpha, \beta)$ with $\alpha \in \Omega^k(U)$ and $\beta \in \Omega^k(V)$ such that $j(\alpha, \beta) = \eta$. That is, $\alpha|_{U \cap V} - \beta|_{U \cap V} = \eta$. Note that $\alpha$ and $\beta$ are generally not closed. A canonical choice for this lift uses a partition of unity $\{\varphi_U, \varphi_V\}$: we can define $\alpha$ as the smooth extension of $\varphi_V \eta$ from $U \cap V$ to $U$, and $\beta$ as the smooth extension of $-\varphi_U \eta$ from $U \cap V$ to $V$.

3.  **Apply the exterior derivative**: Now, apply the [exterior derivative](@entry_id:161900) $d$ to the pair $(\alpha, \beta)$ to get a pair of $(k+1)$-forms $(d\alpha, d\beta)$ on $U$ and $V$, respectively.

4.  **Find the global form**: Let's see what happens to this pair on the intersection. We apply the map $j$ to $(d\alpha, d\beta)$:
    $$ j(d\alpha, d\beta) = d\alpha|_{U \cap V} - d\beta|_{U \cap V} = d(\alpha|_{U \cap V} - \beta|_{U \cap V}) = d\eta = 0 $$
    This means the pair $(d\alpha, d\beta)$ is in the kernel of $j$. By the [exactness](@entry_id:268999) of the [cochain](@entry_id:275805) sequence, this implies that $(d\alpha, d\beta)$ must be in the image of $i$. Therefore, there exists a unique global $(k+1)$-form $\omega \in \Omega^{k+1}(M)$ such that $i(\omega) = (d\alpha, d\beta)$. In other words, $\omega$ is a global form whose restriction to $U$ is $d\alpha$ and to $V$ is $d\beta$.

5.  **Define the image class**: This global form $\omega$ is closed, because on $U$, $d\omega = d(d\alpha) = 0$, and on $V$, $d\omega = d(d\beta) = 0$. We define the image of $[\eta]$ under the [connecting homomorphism](@entry_id:160713) to be the [cohomology class](@entry_id:263961) of this form $\omega$:
    $$ \delta([\eta]) = [\omega] \in H^{k+1}(M) $$
    While the construction involves choices (the representative $\eta$ and the lift $(\alpha, \beta)$), the resulting [cohomology class](@entry_id:263961) $[\omega]$ is independent of these choices. Using the canonical lift from step 2, one can derive an explicit formula for a representative of $\delta([\eta])$: the global form $\omega$ is given by $\omega|_U = d(\varphi_V \eta) = d\varphi_V \wedge \eta$ and $\omega|_V = d(-\varphi_U \eta) = -d\varphi_U \wedge \eta$ [@problem_id:3072087].

### Interpreting the Sequence: A Dictionary for Computation

The power of the Mayer-Vietoris sequence lies in the meaning of [exactness](@entry_id:268999) at each term. The statement "the image of the incoming map equals the kernel of the outgoing map" translates into powerful computational criteria.

#### When do local classes come from a global class?

Consider a pair of cohomology classes, $[\alpha] \in H^k(U)$ and $[\beta] \in H^k(V)$. When can we say that these two classes are "compatible" in the sense that they are restrictions of a single global class $[\omega] \in H^k(M)$? This is equivalent to asking when $([\alpha], [\beta])$ is in the image of $i^*$. The sequence is:
$$ \cdots \to H^k(M) \xrightarrow{i^*} H^k(U) \oplus H^k(V) \xrightarrow{j^*} H^k(U \cap V) \to \cdots $$
By exactness at $H^k(U) \oplus H^k(V)$, we have $\operatorname{im}(i^*) = \ker(j^*)$. Thus, a pair of local classes $([\alpha], [\beta])$ arises from a global class if and only if it lies in the kernel of $j^*$, which means $j^*([\alpha], [\beta]) = [\alpha|_{U \cap V} - \beta|_{U \cap V}] = 0$. This gives us a concrete test: **local cohomology classes on $U$ and $V$ can be glued to a global class on $M$ if and only if their restrictions to the intersection $U \cap V$ define the same cohomology class.**

#### When can an intersection class be extended?

Consider a class $[\gamma] \in H^k(U \cap V)$. When can this class be "split" into a difference of classes, one from $U$ and one from $V$? That is, when does there exist $([\alpha], [\beta]) \in H^k(U) \oplus H^k(V)$ such that $[\gamma] = [\alpha|_{U \cap V} - \beta|_{U \cap V}]$? This is equivalent to asking when $[\gamma]$ is in the image of $j^*$. The sequence is:
$$ \cdots \to H^k(U) \oplus H^k(V) \xrightarrow{j^*} H^k(U \cap V) \xrightarrow{\delta} H^{k+1}(M) \to \cdots $$
By [exactness](@entry_id:268999) at $H^k(U \cap V)$, we have $\operatorname{im}(j^*) = \ker(\delta)$ [@problem_id:3072096]. This yields another powerful criterion: **a cohomology class on the intersection $U \cap V$ is the difference of restrictions of classes from $U$ and $V$ if and only if it is mapped to zero by the [connecting homomorphism](@entry_id:160713) $\delta$.**

This dictionary is key to many computations. For instance, consider a closed $k$-form $\omega$ on $M$ whose restrictions $\omega|_U$ and $\omega|_V$ are both exact. This means its class $[\omega]$ is in the kernel of $i^*$. By exactness, $[\omega]$ must be in the image of $\delta$ from the previous degree, i.e., $[\omega] = \delta([\eta])$ for some class $[\eta] \in H^{k-1}(U \cap V)$. If we can show that $H^{k-1}(U \cap V) = 0$, then $[\eta]$ must be zero, forcing $[\omega] = \delta(0) = 0$. This proves that $\omega$ must be globally exact [@problem_id:3072132].

### Naturality and Applications

A crucial feature of the Mayer-Vietoris sequence is its **[naturality](@entry_id:270302)**. This means that it behaves predictably with respect to [smooth maps between manifolds](@entry_id:190665).

#### The Principle of Naturality

Suppose we have two manifolds $M$ and $N$, each with an [open cover](@entry_id:140020) ($M = U \cup V$ and $N = U' \cup V'$). Let $f: M \to N$ be a [smooth map](@entry_id:160364) that respects these covers, meaning $f(U) \subseteq U'$ and $f(V) \subseteq V'$. The pullback map $f^*$ induces homomorphisms on cohomology, $f^*: H^k(N) \to H^k(M)$. Naturality asserts that these pullback maps commute with all the maps in the Mayer-Vietoris sequences of $M$ and $N$. This gives rise to a commutative "ladder" diagram [@problem_id:3072102]:

$$
\begin{array}{ccccccc}
\cdots \to  H^k(N)  \xrightarrow{i_N^*}  H^k(U')\oplus H^k(V')  \xrightarrow{j_N^*}  H^k(U'\cap V')  \xrightarrow{\delta_N}  H^{k+1}(N)  \to \cdots \\
 \downarrow f^*   \downarrow f_U^* \oplus f_V^*   \downarrow f_{U \cap V}^*   \downarrow f^*  \\
\cdots \to  H^k(M)  \xrightarrow{i_M^*}  H^k(U)\oplus H^k(V)  \xrightarrow{j_M^*}  H^k(U\cap V)  \xrightarrow{\delta_M}  H^{k+1}(M)  \to \cdots
\end{array}
$$

The commutativity of the square involving the [connecting homomorphism](@entry_id:160713), $f^* \circ \delta_N = \delta_M \circ f_{U \cap V}^*$, is a particularly deep and useful result.

#### Combining Mayer-Vietoris with Homotopy Invariance

The true computational power of the Mayer-Vietoris sequence is unleashed when combined with another fundamental principle: the **homotopy invariance of de Rham cohomology**. This principle states that if two manifolds are smoothly homotopy equivalent, their de Rham [cohomology groups](@entry_id:142450) are isomorphic, and the isomorphism is induced by the [pullback](@entry_id:160816) of the homotopy equivalence map.

Let's see how these principles work together in a classic example. Consider the [annulus](@entry_id:163678) $X = S^1 \times (0,1)$ and the circle $S^1$. The projection $p: X \to S^1$ is a homotopy equivalence. Therefore, the [pullback](@entry_id:160816) map $p^*: H^k(S^1) \to H^k(X)$ is an isomorphism for all $k$. This means that to compute the cohomology of the [annulus](@entry_id:163678) $X$, it suffices to compute the cohomology of the much simpler circle $S^1$ and then "transport" the result via the isomorphism $p^*$ [@problem_id:3072091].

We can compute $H^1(S^1)$ using the Mayer-Vietoris sequence. Let's cover $S^1$ with two overlapping open arcs, $I_1$ and $I_2$, such that their intersection $I_1 \cap I_2$ consists of two disjoint arcs. The relevant part of the Mayer-Vietoris sequence is:
$$ H^0(I_1) \oplus H^0(I_2) \xrightarrow{j_{S^1}^*} H^0(I_1 \cap I_2) \xrightarrow{\delta_{S^1}} H^1(S^1) \to H^1(I_1) \oplus H^1(I_2) $$
Since open arcs are contractible, $H^1(I_1) = H^1(I_2) = \{0\}$. Also, $H^0$ of a connected space is $\mathbb{R}$. So we have $H^0(I_1) \cong \mathbb{R}$, $H^0(I_2) \cong \mathbb{R}$, and since $I_1 \cap I_2$ has two components, $H^0(I_1 \cap I_2) \cong \mathbb{R} \oplus \mathbb{R}$. The map $j_{S^1}^*$ sends a pair of constants $(c_1, c_2)$ to a [constant function](@entry_id:152060) $c_2 - c_1$ on the intersection, which corresponds to the diagonal subspace $\{(d,d) \in \mathbb{R} \oplus \mathbb{R}\}$.
By [exactness](@entry_id:268999), $H^1(S^1) \cong \operatorname{coker}(j_{S^1}^*) \cong (\mathbb{R} \oplus \mathbb{R}) / \{(d,d)\} \cong \mathbb{R}$. A generator for $H^1(S^1)$ is, for example, the image of the class $(1,-1) \in H^0(I_1 \cap I_2)$ under $\delta_{S^1}$. Let's call this generator $[\omega_{S^1}]$.

Now, we can use [naturality](@entry_id:270302). We can lift the cover of $S^1$ to a cover of the [annulus](@entry_id:163678) $X$ by setting $U = p^{-1}(I_1)$ and $V = p^{-1}(I_2)$. The projection map $p: X \to S^1$ respects these covers. By [naturality](@entry_id:270302), we have the commutative square:
$$ p^* \circ \delta_{S^1} = \delta_X \circ (p|_{U \cap V})^* $$
Since $p^*$ is an [isomorphism](@entry_id:137127), it maps the generator $[\omega_{S^1}]$ of $H^1(S^1)$ to a generator of $H^1(X)$. Thus, $p^*([\omega_{S^1}])$ is a generator for $H^1(X)$, and we conclude that $H^1(X) \cong \mathbb{R}$ as well. This elegant argument, weaving together decomposition, [exactness](@entry_id:268999), [naturality](@entry_id:270302), and homotopy, exemplifies the profound utility of the Mayer-Vietoris sequence in geometric analysis.