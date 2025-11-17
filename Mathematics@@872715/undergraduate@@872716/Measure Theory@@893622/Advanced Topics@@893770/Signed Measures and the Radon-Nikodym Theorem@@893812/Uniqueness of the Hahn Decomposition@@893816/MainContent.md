## Introduction
The Hahn Decomposition Theorem is a cornerstone of measure theory, providing a fundamental way to understand the structure of spaces endowed with a [signed measure](@entry_id:160822). It asserts that any such space can be neatly partitioned into two regions: one where the measure behaves positively, and one where it behaves negatively. While the existence of this partition is powerful, its true utility and theoretical depth are unlocked by a more subtle property: its uniqueness. This article delves into this crucial aspect, addressing the question of *how* unique this decomposition truly is. Across the following chapters, we will first explore the principles and mechanisms behind the uniqueness proof, clarifying the concept of uniqueness "up to a [null set](@entry_id:145219)". We will then examine the far-reaching applications and interdisciplinary connections of this property in fields like functional analysis and probability theory. Finally, a series of hands-on practices will allow you to solidify your understanding by applying these concepts to concrete examples.

## Principles and Mechanisms

The Hahn Decomposition Theorem is a cornerstone of [measure theory](@entry_id:139744), asserting that any space with a [signed measure](@entry_id:160822) can be partitioned into two fundamental regions: one where the measure is non-negative and one where it is non-positive. While the existence of such a decomposition is powerful, its utility is profoundly enhanced by its uniqueness. This chapter delves into the principles governing this uniqueness, the mechanism of its proof, and its far-reaching consequences for related concepts like the Jordan decomposition.

### The Uniqueness of the Decomposition

The Hahn Decomposition Theorem guarantees that for any [signed measure](@entry_id:160822) $\nu$ on a [measurable space](@entry_id:147379) $(X, \mathcal{M})$, there exists a partition of $X$ into two disjoint measurable sets, $P$ and $N$, such that $P$ is a positive set for $\nu$ and $N$ is a negative set for $\nu$. That is, for any measurable subset $E \subseteq P$, $\nu(E) \ge 0$, and for any measurable subset $F \subseteq N$, $\nu(F) \le 0$.

The crucial second part of the theorem addresses uniqueness. It does not claim that the sets $P$ and $N$ are absolutely unique. Instead, it makes a more subtle and powerful statement: the decomposition is unique up to **$\nu$-[null sets](@entry_id:203073)**.

Formally, if $(P_1, N_1)$ and $(P_2, N_2)$ are two Hahn decompositions for the same [signed measure](@entry_id:160822) $\nu$, then the symmetric differences $P_1 \Delta P_2$ and $N_1 \Delta N_2$ are $\nu$-null. A set $Z \in \mathcal{M}$ is defined as a **$\nu$-[null set](@entry_id:145219)** if for every measurable subset $E \subseteq Z$, we have $\nu(E) = 0$. This implies not only that the set $Z$ itself may have zero measure, but that all its measurable parts do as well.

### The Proof of Uniqueness

The proof of this uniqueness is an elegant application of the very definitions of positive and negative sets. It demonstrates a fundamental structural constraint imposed by the [signed measure](@entry_id:160822) on the space.

Let $(P_1, N_1)$ and $(P_2, N_2)$ be two Hahn decompositions for $\nu$. Our goal is to show that their symmetric difference, $P_1 \Delta P_2 = (P_1 \setminus P_2) \cup (P_2 \setminus P_1)$, is a $\nu$-[null set](@entry_id:145219). We can analyze each part of this union separately.

Consider the set $P_1 \setminus P_2$. Since $(P_2, N_2)$ is a partition of $X$, we can write this set as an intersection: $P_1 \setminus P_2 = P_1 \cap N_2$. Now, consider any measurable subset $E \subseteq P_1 \cap N_2$.
1.  Since $E$ is a subset of $P_1$, which is a positive set, we must have $\nu(E) \ge 0$.
2.  Simultaneously, since $E$ is a subset of $N_2$, which is a negative set, we must have $\nu(E) \le 0$.

The only real number that is both non-negative and non-positive is zero. Therefore, for any measurable subset $E \subseteq P_1 \setminus P_2$, it must be that $\nu(E) = 0$. By definition, this means the set $P_1 \setminus P_2$ is a $\nu$-[null set](@entry_id:145219).

By a perfectly symmetrical argument, the set $P_2 \setminus P_1 = P_2 \cap N_1$ is also a $\nu$-[null set](@entry_id:145219). Any measurable subset of it is contained in the positive set $P_2$ and the negative set $N_1$, forcing its measure to be zero.

The [symmetric difference](@entry_id:156264) $P_1 \Delta P_2$ is the disjoint union of the two $\nu$-[null sets](@entry_id:203073) $P_1 \setminus P_2$ and $P_2 \setminus P_1$. Any measurable subset of this symmetric difference is itself a disjoint union of subsets from these two null components, and its measure will therefore be $0+0=0$. Consequently, $P_1 \Delta P_2$ is a $\nu$-[null set](@entry_id:145219), which completes the proof of uniqueness [@problem_id:1464517].

### Interpreting Uniqueness in Practice

The phrase "unique up to a [null set](@entry_id:145219)" can seem abstract, but concrete examples reveal its practical meaning. It tells us that while different valid Hahn decompositions can exist, they only differ on sets that are inconsequential from the perspective of the measure $\nu$.

#### The Case of the Zero Measure

Consider the trivial **zero measure**, $\mu_0$, defined by $\mu_0(E) = 0$ for every measurable set $E \in \mathcal{M}$. Let's find its Hahn decomposition. For any measurable set $A$, and any subset $E \subseteq A$, we have $\mu_0(E) = 0$. Since $0 \ge 0$ and $0 \le 0$, every measurable set in the space is simultaneously a positive set and a negative set for $\mu_0$. This has a surprising consequence: *any* measurable partition $(A, B)$ of the space $X$ is a valid Hahn decomposition. For instance, on the real line, both $((-\infty, 0], (0, \infty))$ and $(\mathbb{Q}, \mathbb{R}\setminus\mathbb{Q})$ are valid Hahn decompositions.

This appears to be a massive failure of uniqueness. However, the uniqueness theorem is not violated. To see why, we must ask: what is a $\mu_0$-[null set](@entry_id:145219)? A set $Z$ is $\mu_0$-null if for every measurable $E \subseteq Z$, $\mu_0(E)=0$. But this is true for *any* measurable set $E$ in the entire space. Therefore, for the zero measure, every measurable set is a $\mu_0$-[null set](@entry_id:145219).

If we take any two Hahn decompositions, $(P_1, N_1)$ and $(P_2, N_2)$, their symmetric difference $P_1 \Delta P_2$ is a [measurable set](@entry_id:263324). As such, it is automatically a $\mu_0$-[null set](@entry_id:145219). The uniqueness theorem holds perfectly; it is simply that the concept of a "[null set](@entry_id:145219)" is so expansive for the zero measure that it accommodates all possible decompositions [@problem_id:1464510].

#### Decompositions Defined by a Density Function

A more common scenario involves a [signed measure](@entry_id:160822) $\nu$ that is absolutely continuous with respect to a positive measure $\mu$, given by a density function $f$ via the Radon-Nikodym theorem:
$$ \nu(E) = \int_E f \,d\mu $$
In this case, the natural Hahn decomposition is given by the sets where the density function is non-negative and negative:
$P = \{x \in X \mid f(x) \ge 0\}$
$N = \{x \in X \mid f(x)  0\}$

Let's consider a specific example on $(\mathbb{R}, \mathcal{B}(\mathbb{R}))$ with $\mu$ being the Lebesgue measure. Define a [signed measure](@entry_id:160822) by $\nu(E) = \int_E (x^2-4)\exp(-x^2/2) \,d\mu(x)$. The density function is $f(x) = (x^2-4)\exp(-x^2/2)$.
This function is non-negative when $x^2 - 4 \ge 0$, which occurs for $x \in (-\infty, -2] \cup [2, \infty)$. So, a natural choice for the positive set is $P_1 = (-\infty, -2] \cup [2, \infty)$.

However, what if we chose a slightly different set, $P_2 = (-\infty, -2) \cup (2, \infty)$? This is also a valid positive set, as is its complement a valid negative set. The sets $P_1$ and $P_2$ are not identical. Their [symmetric difference](@entry_id:156264) is $P_1 \Delta P_2 = \{-2, 2\}$.
According to the uniqueness theorem, this set must be $\nu$-null. Let's verify this.
$$ \nu(\{-2, 2\}) = \int_{\{-2, 2\}} (x^2-4)\exp(-x^2/2) \,d\mu(x) $$
The set $\{-2, 2\}$ consists of two points and thus has a Lebesgue measure of zero. The integral of any function over a set of measure zero is zero. Therefore, $\nu(\{-2, 2\}) = 0$. Since the only non-empty measurable subset of $\{-2, 2\}$ is the set itself, this confirms that $P_1 \Delta P_2$ is a $\nu$-[null set](@entry_id:145219). The difference between the two decompositions is confined to the boundary where the density is zero, a set which is inconsequential to the measure $\nu$ [@problem_id:1436330].

### Consequences of Hahn Uniqueness

The essential uniqueness of the Hahn decomposition is not merely an elegant theoretical result; it is the foundation upon which the uniqueness of other critical constructions in [measure theory](@entry_id:139744) rests.

#### Uniqueness of the Jordan Decomposition

Every [signed measure](@entry_id:160822) $\nu$ can be decomposed into the difference of two mutually singular positive measures, $\nu = \nu^+ - \nu^-$. This is known as the **Jordan decomposition**. These measures, the **positive variation** $\nu^+$ and **negative variation** $\nu^-$, are directly constructed from a Hahn decomposition $(P, N)$:
$$ \nu^+(E) = \nu(E \cap P) \quad \text{and} \quad \nu^-(E) = -\nu(E \cap N) $$
The uniqueness of the Hahn decomposition directly implies the uniqueness of the Jordan decomposition. If $(P_1, N_1)$ and $(P_2, N_2)$ are two Hahn decompositions, they give rise to two potential Jordan decompositions, $(\nu_1^+, \nu_1^-)$ and $(\nu_2^+, \nu_2^-)$. However, we can show they are identical. For any [measurable set](@entry_id:263324) $E$:
$$ \nu_1^+(E) - \nu_2^+(E) = \nu(E \cap P_1) - \nu(E \cap P_2) = \nu(E \cap (P_1 \setminus P_2)) - \nu(E \cap (P_2 \setminus P_1)) $$
Since $P_1 \setminus P_2$ and $P_2 \setminus P_1$ are $\nu$-[null sets](@entry_id:203073), any measure of their subsets is zero. Thus, the difference is $0 - 0 = 0$. This shows $\nu_1^+ = \nu_2^+$, and a similar argument shows $\nu_1^- = \nu_2^-$. The Jordan decomposition is therefore unique, not just "up to [null sets](@entry_id:203073)," but absolutely unique. This uniqueness is critical for defining the [total variation measure](@entry_id:193822) $|\nu| = \nu^+ + \nu^-$ as a single, well-defined measure.

For instance, on a [discrete space](@entry_id:155685) $X = \{a, b, c\}$, if a [signed measure](@entry_id:160822) is given by $\nu(\{a\}) = 5$, $\nu(\{b\}) = -12$, and $\nu(\{c\}) = 4$, the Hahn decomposition is uniquely determined (up to [null sets](@entry_id:203073), of which there are none but $\emptyset$) as $P=\{a, c\}$ and $N=\{b\}$. This leads to a single, unambiguous Jordan decomposition where, for example, $\nu^+(\{a,b\}) = \nu(\{a,b\} \cap \{a,c\}) = \nu(\{a\}) = 5$ and $\nu^-(\{b,c\}) = -\nu(\{b,c\} \cap \{b\}) = -\nu(\{b\}) = 12$ [@problem_id:1464500].

#### Uniqueness of Separating Sets for Singular Measures

The Jordan measures $\nu^+$ and $\nu^-$ are **mutually singular**, denoted $\nu^+ \perp \nu^-$, because they are concentrated on the [disjoint sets](@entry_id:154341) $P$ and $N$, respectively. The uniqueness of the Hahn decomposition is a specific instance of a more general principle regarding [singular measures](@entry_id:191565).

Two positive measures $\mu_1$ and $\mu_2$ are mutually singular if there exists a partition $(A_1, A_2)$ of the space such that $\mu_1$ is concentrated on $A_1$ (i.e., $\mu_1(E) = \mu_1(E \cap A_1)$ for all $E$) and $\mu_2$ is concentrated on $A_2$. Is this pair of separating sets unique? The answer is the same as for the Hahn decomposition: yes, up to [null sets](@entry_id:203073).

If $(B_1, B_2)$ is another such pair of separating sets, we can show that $\mu_1(A_1 \Delta B_1) = 0$ and $\mu_2(A_2 \Delta B_2) = 0$. The reasoning mirrors the Hahn proof. Consider $\mu_1(A_1 \setminus B_1)$. Since $\mu_1$ is concentrated on $B_1$, its measure on any set disjoint from $B_1$ must be zero. Thus, $\mu_1(A_1 \setminus B_1) = \mu_1((A_1 \setminus B_1) \cap B_1^c) = 0$. By symmetry, since $\mu_1$ is also concentrated on $A_1$, $\mu_1(B_1 \setminus A_1) = 0$. It follows that $\mu_1(A_1 \Delta B_1) = \mu_1(A_1 \setminus B_1) + \mu_1(B_1 \setminus A_1) = 0+0=0$. This confirms that the geometric separation of [singular measures](@entry_id:191565) is essentially unique [@problem_id:1464508].

### Transformations of Signed Measures

The structural rigidity provided by the uniqueness theorem allows us to predict the decomposition of transformed measures.

For example, if $(P, N)$ is a Hahn decomposition for $\nu$, what is the decomposition for the [signed measure](@entry_id:160822) $\mu = -k\nu$ for some constant $k > 0$? A set $E \subseteq P$ has $\nu(E) \ge 0$, which implies $\mu(E) = -k\nu(E) \le 0$. Thus, $P$ becomes a negative set for $\mu$. Conversely, a set $F \subseteq N$ has $\nu(F) \le 0$, which implies $\mu(F) = -k\nu(F) \ge 0$, making $N$ a positive set for $\mu$. Therefore, the Hahn decomposition for $\mu = -k\nu$ is simply $(N, P)$ [@problem_id:1464511].

Similarly, if two [signed measures](@entry_id:198637) $\nu_1$ and $\nu_2$ happen to share a common Hahn decomposition $(P, N)$, this structure is preserved under addition. For the sum $\nu = \nu_1 + \nu_2$, any set $E \subseteq P$ will have $\nu(E) = \nu_1(E) + \nu_2(E) \ge 0+0=0$, so $P$ is positive for $\nu$. Likewise, $N$ is negative for $\nu$. Thus, $(P, N)$ is a Hahn decomposition for $\nu_1 + \nu_2$, and by the uniqueness theorem, it is the unique such decomposition up to $\nu$-[null sets](@entry_id:203073) [@problem_id:1464501].

In conclusion, the uniqueness of the Hahn decomposition, while nuanced, is a deep and stabilizing property of [signed measures](@entry_id:198637). It ensures that the fundamental split of a space into positive and negative domains is not arbitrary but is an intrinsic feature determined by the measure itself. This principle guarantees the coherence of related concepts and provides a solid foundation for the broader theory of integration and [signed measures](@entry_id:198637).