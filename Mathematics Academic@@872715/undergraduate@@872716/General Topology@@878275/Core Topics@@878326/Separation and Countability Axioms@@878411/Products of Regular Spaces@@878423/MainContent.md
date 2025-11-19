## Introduction
In the study of topology, a fundamental technique involves constructing new spaces from existing ones to expand our mathematical universe. The Cartesian [product of topological spaces](@entry_id:152598), endowed with the [product topology](@entry_id:154786), is one of the most important of these constructions. However, a crucial question arises: which properties of the original "factor" spaces are inherited by the new "product" space? This article delves into the [separation axiom](@entry_id:155057) of **regularity**, a property that exhibits exceptionally stable behavior under this operation. We will explore the pivotal theorem stating that a product space is regular if and only if each of its factors is regular.

This article is structured to guide you from theoretical foundations to practical applications. In **Principles and Mechanisms**, we will define regularity, dissect the proof of the main theorem, and highlight the critical role of the [product topology](@entry_id:154786). Next, **Applications and Interdisciplinary Connections** will demonstrate the theorem's power by applying it to spaces in geometry, [functional analysis](@entry_id:146220), and topological algebra, while contrasting regularity's behavior with other properties like normality. Finally, **Hands-On Practices** will provide targeted exercises to solidify your understanding of these concepts through concrete examples and counterexamples.

## Principles and Mechanisms

In our exploration of [topological spaces](@entry_id:155056), the construction of new spaces from existing ones is a central theme. The product topology provides a canonical way to endow a Cartesian [product of topological spaces](@entry_id:152598) with a topology that relates intimately to the topologies of its constituent factors. A fundamental question then arises: which topological properties are inherited by the [product space](@entry_id:151533) from its factors, and conversely, which properties of the product space are conferred upon its factors? This chapter focuses on the [separation axiom](@entry_id:155057) of **regularity**, a property that, as we shall see, behaves exceptionally well with respect to arbitrary products.

### The Essence of Regularity

Before delving into products, let us solidify our understanding of regularity. A [topological space](@entry_id:149165) is said to be **regular** if, for any [closed set](@entry_id:136446) $C$ and any point $p$ not in $C$, there exist [disjoint open sets](@entry_id:150704) $U$ and $V$ such that $p \in U$ and $C \subseteq V$. This definition captures the ability to separate points from closed sets with open "sleeves."

While this definition is geometrically intuitive, an equivalent formulation is often more powerful in proofs, particularly those involving products. A space $X$ is regular if and only if for every point $p \in X$ and every open set $W$ containing $p$, there exists another open set $U$ such that $p \in U$ and the closure of $U$, denoted $\overline{U}$, is a subset of $W$. This condition can be written compactly as:
$$ p \in U \subseteq \overline{U} \subseteq W $$
This property allows us to "shrink" an open neighborhood $W$ around a point $p$ to a smaller open neighborhood $U$ whose closure is still comfortably contained within $W$.

To make this tangible, consider the Euclidean plane $\mathbb{R}^2$. Let us verify its regularity in a specific instance. Suppose we have a point $P = (2, 2)$ and a closed line segment $C$ connecting $(-1, -1)$ and $(1, -1)$. We can construct an open set around $P$ using an open ball $U_r$ of radius $r$, and an open set "around" $C$ by taking the union of all [open balls](@entry_id:143668) of radius $r$ centered at each point in $C$, let's call this set $V_r$. The question of separation becomes: for which values of $r$ are $U_r$ and $V_r$ disjoint? Intuitively, the balls must be small enough that they do not touch. By the triangle inequality, if a point $X$ were in their intersection, then the distance $d(P, Q)$ for some $Q \in C$ would be less than $2r$. Thus, separation is guaranteed if $2r$ is no larger than the minimum distance from $P$ to $C$, which we denote $d(P, C)$. For this specific case, the closest point on segment $C$ to $P$ is $(1,-1)$, with a distance of $\sqrt{(2-1)^2 + (2-(-1))^2} = \sqrt{10}$. Therefore, $U_r$ and $V_r$ are disjoint if $r \le \frac{\sqrt{10}}{2}$. This quantitative exercise illustrates the concrete geometric meaning of separating a point from a [closed set](@entry_id:136446) [@problem_id:1569452].

Let's also illustrate the alternative neighborhood-shrinking definition. Consider the point $p = (0,0)$ in $\mathbb{R}^2$ and the open square neighborhood $W = (-1, 1) \times (-1, 1)$. Can we find an open set $U$ containing $p$ such that $\overline{U} \subseteq W$? Let's try $U = (-\frac{1}{2}, \frac{1}{2}) \times (-\frac{1}{2}, \frac{1}{2})$. This is an open set containing the origin. In the [standard topology](@entry_id:152252) of $\mathbb{R}^2$, the closure of a product is the product of closures, so $\overline{U} = [-\frac{1}{2}, \frac{1}{2}] \times [-\frac{1}{2}, \frac{1}{2}]$. Since $[-\frac{1}{2}, \frac{1}{2}] \subseteq (-1, 1)$, we have successfully found a neighborhood $U$ satisfying $p \in U \subseteq \overline{U} \subseteq W$, confirming the regularity condition in this instance [@problem_id:1569463]. This ability to insert a [closed neighborhood](@entry_id:276349) between a point and its open neighborhood is the key mechanism we will exploit in [product spaces](@entry_id:151693).

### The Main Theorem: Preservation of Regularity Under Products

We now arrive at a cornerstone result in [general topology](@entry_id:152375). It states that regularity is perfectly preserved under the product topology, regardless of the number of spaces being multiplied.

**Theorem:** Let $\{X_\alpha\}_{\alpha \in J}$ be a non-empty collection of topological spaces. The product space $X = \prod_{\alpha \in J} X_\alpha$ is regular if and only if each factor space $X_\alpha$ is regular.

This "if and only if" statement comprises two distinct claims, each with its own elegant proof.

#### From Product to Factors

Let us first prove that if the product space $X = \prod X_\alpha$ is regular, then each individual factor space $X_\alpha$ must also be regular.

The proof relies on two essential properties: regularity is a **[hereditary property](@entry_id:151340)** and a **[topological invariant](@entry_id:142028)**. A property is hereditary if every subspace of a space with that property also has that property. It is a topological invariant if it is preserved under [homeomorphism](@entry_id:146933).

First, let's establish that regularity is hereditary. Let $Z$ be a [regular space](@entry_id:155336) and $S$ be any subspace of $Z$. To show $S$ is regular, take any point $s \in S$ and a closed set $C_S \subseteq S$ with $s \notin C_S$. By the definition of the subspace topology, $C_S = S \cap C_Z$ for some closed set $C_Z$ in $Z$. Since $s \in S$ and $s \notin C_S$, it follows that $s \notin C_Z$. As $Z$ is regular, there exist disjoint open sets $U_Z$ and $V_Z$ in $Z$ such that $s \in U_Z$ and $C_Z \subseteq V_Z$. Now, consider the sets $U_S = S \cap U_Z$ and $V_S = S \cap V_Z$. These are open in the subspace $S$, they are disjoint because $U_Z$ and $V_Z$ are, $s \in U_S$, and $C_S = S \cap C_Z \subseteq S \cap V_Z = V_S$. Thus, $S$ is regular. This holds for any subspace, whether open, closed, or neither [@problem_id:1569431].

Now, to connect this to the product space, fix an index $\beta \in J$ and choose a point $p = (p_\alpha)_{\alpha \neq \beta}$ in the sub-product $\prod_{\alpha \neq \beta} X_\alpha$. Consider the "slice" subspace $S_\beta = \{x \in X \mid x_\alpha = p_\alpha \text{ for all } \alpha \neq \beta\}$. This subspace $S_\beta$ is homeomorphic to the factor space $X_\beta$ via the natural projection map. Since the full product space $X$ is assumed to be regular, its subspace $S_\beta$ must also be regular. Because $X_\beta$ is homeomorphic to the [regular space](@entry_id:155336) $S_\beta$, and regularity is a topological invariant, $X_\beta$ must be regular. This argument holds for every $\beta \in J$, completing the proof [@problem_id:1569457].

As a related consequence, if we assume the factor spaces are T1 (meaning singletons are closed), then a [regular space](@entry_id:155336) is also a Hausdorff (T2) space. The product of T1 spaces is T1, and the product of regular T1 spaces is therefore a regular T1 space, which in turn must be Hausdorff. Therefore, the product of [regular spaces](@entry_id:154729) is always Hausdorff (assuming T1, which is often included in the definition of regularity) [@problem_id:1569433].

#### From Factors to Product

The more substantial part of the theorem is proving that if each factor space $X_\alpha$ is regular, then the [product space](@entry_id:151533) $X = \prod X_\alpha$ is regular.

For simplicity, let's first consider the product of two [regular spaces](@entry_id:154729), $X$ and $Y$. We will use the neighborhood-shrinking definition of regularity. Let $p = (x_0, y_0)$ be an arbitrary point in $X \times Y$, and let $W$ be any open neighborhood of $p$. By the definition of the [product topology](@entry_id:154786), there must exist a basic open set $U \times V$ such that $p \in U \times V \subseteq W$, where $U$ is open in $X$ and $V$ is open in $Y$.

This is where the regularity of the factor spaces comes into play.
- Since $X$ is regular and $x_0 \in U$, there exists an open set $U_0$ in $X$ such that $x_0 \in U_0 \subseteq \overline{U_0} \subseteq U$.
- Since $Y$ is regular and $y_0 \in V$, there exists an open set $V_0$ in $Y$ such that $y_0 \in V_0 \subseteq \overline{V_0} \subseteq V$.

Now, form the product $U_0 \times V_0$. This is a basic open set in $X \times Y$ that contains the point $p = (x_0, y_0)$. The final, crucial step is to examine its closure. A key theorem of [product topology](@entry_id:154786) states that for any subsets $A \subseteq X$ and $B \subseteq Y$, the closure of their product is the product of their [closures](@entry_id:747387): $\overline{A \times B} = \overline{A} \times \overline{B}$. This identity is the bridge that connects the properties of the factors to the properties of the product [@problem_id:1569458].

Applying this identity, we have:
$$ \overline{U_0 \times V_0} = \overline{U_0} \times \overline{V_0} $$
From our construction, we know $\overline{U_0} \subseteq U$ and $\overline{V_0} \subseteq V$. Therefore,
$$ \overline{U_0 \times V_0} \subseteq U \times V $$
And since we chose $U \times V$ to be a subset of $W$, we have the full chain of inclusions:
$$ p \in U_0 \times V_0 \subseteq \overline{U_0 \times V_0} \subseteq W $$
This demonstrates that $X \times Y$ is regular.

This argument extends directly to an arbitrary product $X = \prod_{\alpha \in J} X_\alpha$. For any point $p=(p_\alpha)$ and any open neighborhood $W$, we can find a basic [open neighborhood](@entry_id:268496) $\prod U_\alpha \subseteq W$, where $U_\alpha$ is open in $X_\alpha$ for all $\alpha$, and the set of indices $F = \{\alpha \in J \mid U_\alpha \neq X_\alpha\}$ is finite. For each $\alpha \in F$, we use the regularity of $X_\alpha$ to find an open set $V_\alpha$ such that $p_\alpha \in V_\alpha \subseteq \overline{V_\alpha} \subseteq U_\alpha$. For $\alpha \notin F$, we simply let $V_\alpha = X_\alpha$. The open set $\prod V_\alpha$ is a neighborhood of $p$ whose closure, $\prod \overline{V_\alpha}$, is contained within $\prod U_\alpha$ and thus within $W$.

### Applications and the Power of the Theorem

The theorem's strength lies in its universality. It applies to products of any size, from finite to uncountably infinite.

- **Euclidean and Function Spaces:** Since the real line $\mathbb{R}$ with its standard topology is a [metric space](@entry_id:145912) and thus regular, our theorem immediately implies that any finite product $\mathbb{R}^n$ is regular. More profoundly, it means that the space of all real sequences, $\mathbb{R}^\mathbb{N}$, endowed with the product topology, is a [regular space](@entry_id:155336). The same holds for any [function space](@entry_id:136890) $Y^S$ (the set of all functions from a set $S$ to a space $Y$) with the [product topology](@entry_id:154786); if $Y$ is regular, so is $Y^S$ [@problem_id:1569450], [@problem_id:1569497]. Even a product with a trivial one-point space, say $X \times \{p\}$, is regular if $X$ is, as this product is simply homeomorphic to $X$ itself [@problem_id:1569492].

- **Subspace Products:** Combining the main theorem with the fact that regularity is a [hereditary property](@entry_id:151340) yields further results. If $X$ and $Y$ are [regular spaces](@entry_id:154729) and $A$ is any subspace of $X$, the product space $A \times Y$ is guaranteed to be regular. This is because $A$, as a subspace of a [regular space](@entry_id:155336), is regular, and $Y$ is regular by assumption. Their product is therefore a product of two [regular spaces](@entry_id:154729), which must be regular [@problem_id:1569431].

### A Critical Caveat: The Role of the Topology

It is imperative to recognize that this elegant theorem is entirely contingent on the use of the **[product topology](@entry_id:154786)**. If we equip the Cartesian product with a different topology, the result may no longer hold. The most famous example is the **[box topology](@entry_id:148414)**, where the basis of open sets consists of all arbitrary products $\prod U_\alpha$ where each $U_\alpha$ is open, without the restriction that only finitely many can differ from the whole space.

Consider the space $\mathbb{R}^\mathbb{N}$ with the box topology. This space, despite being a product of [regular spaces](@entry_id:154729), is **not regular**. To see why, one can construct a point and a closed set that cannot be separated. Let $p = (0, 0, \dots)$ be the origin and let $C = \{x \in \mathbb{R}^\mathbb{N} \mid x_n \ge 1/n \text{ for all } n\}$. The set $C$ is closed in the box topology, and $p \notin C$. Any basic open neighborhood of $p$ is of the form $U = \prod (-\epsilon_n, \epsilon_n)$ for some sequence of positive numbers $(\epsilon_n)$. Any open neighborhood of $C$ must contain a basic open set $V$ that covers $C$. One can show that for any such $U$ and $V$, their intersection is non-empty. For instance, a point $y = (y_n)$ can be constructed such that $y_n$ is simultaneously close to $0$ (to be in $U$) and close to a point in $C$ (to be in $V$). The failure of separation stems from the immense "freedom" in the box topology; a neighborhood can be made arbitrarily "thin" in every coordinate simultaneously, a property that the [product topology](@entry_id:154786) prevents [@problem_id:1569455]. This counterexample powerfully illustrates that the finiteness condition in the definition of the [product topology](@entry_id:154786) basis is precisely what allows the regularity of factors to propagate to the product.

### Context and Comparison

The preservation of regularity under arbitrary products is a truly remarkable result, setting it apart from many other important topological properties.

- **Normality:** A space is normal if any two [disjoint closed sets](@entry_id:152178) can be separated by [disjoint open sets](@entry_id:150704). Products of [normal spaces](@entry_id:154073) are not necessarily normal. The Sorgenfrey plane, a product of two [normal spaces](@entry_id:154073), is a classic [counterexample](@entry_id:148660).
- **Lindelöf Property:** A space is Lindelöf if every open cover has a countable [subcover](@entry_id:151408). The product of two Lindelöf spaces need not be Lindelöf.
- **Second-Countability:** A product of [second-countable spaces](@entry_id:151268) is second-countable only if the number of non-trivial factors is countable. An uncountable product of copies of $\mathbb{R}$ is not second-countable.

In this landscape, regularity stands out. Its stable and predictable behavior under the product construction is one of the primary reasons it, along with the related Hausdorff property, occupies a central place in the study of topology and its applications in analysis and geometry [@problem_id:1569497].