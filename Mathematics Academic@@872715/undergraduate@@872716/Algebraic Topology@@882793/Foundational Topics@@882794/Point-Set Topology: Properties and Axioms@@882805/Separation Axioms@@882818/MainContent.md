## Introduction
In the vast landscape of topological spaces, not all are created equal. Some exhibit pathological behaviors that defy the intuitions we carry from analysis, such as sequences converging to multiple points at once. To bring order to this universe and identify spaces that are "well-behaved," mathematicians have introduced a series of conditions known as the **separation axioms**. These axioms provide a foundational framework for [classifying spaces](@entry_id:148422) based on their power to distinguish points and sets from one another, forming a ladder of increasing "niceness." This article addresses the fundamental need for such a classification, exploring the hierarchy of axioms that guarantees the [structural integrity](@entry_id:165319) required for much of modern mathematics.

This article is structured to build your understanding from the ground up. In **Principles and Mechanisms**, we will define each of the major separation axioms—from $T_0$ to $T_4$—and explore their core properties and interrelationships. Following this, **Applications and Interdisciplinary Connections** will demonstrate why these abstract definitions matter, showcasing their crucial role in [general topology](@entry_id:152375), algebraic geometry, and the mechanics of algebraic topology itself. Finally, **Hands-On Practices** will allow you to solidify your knowledge by working through concrete problems that test your understanding of these essential concepts.

## Principles and Mechanisms

In the study of topological spaces, it is often necessary to impose conditions that guarantee a certain "reasonableness" of behavior, particularly when concepts from analysis, such as [limits of sequences](@entry_id:159667), are involved. These conditions, known as the **separation axioms**, form a hierarchy that classifies spaces based on the degree to which points and closed sets can be distinguished by open sets. This chapter delineates the principal separation axioms, explores their fundamental characterizations, and illustrates their significance through key theorems and examples.

### The Lower Axioms: Distinguishing Points

The most fundamental axioms, designated $T_0, T_1$, and $T_2$, address the distinguishability of individual points. They form a strict hierarchy, with each successive axiom imposing a stronger condition than the last.

#### $T_0$ (Kolmogorov) Spaces

The weakest of the separation axioms is the $T_0$ axiom, which ensures that any two distinct points are at least topologically distinguishable.

**Definition ($T_0$ Space):** A [topological space](@entry_id:149165) $(X, \tau)$ is a **$T_0$ space**, or **Kolmogorov space**, if for every pair of distinct points $x, y \in X$, there exists an open set $U \in \tau$ that contains one of the points but not the other. That is, either ($x \in U$ and $y \notin U$) or ($y \in U$ and $x \notin U$).

This axiom asserts that the topology is rich enough to discern a difference between any two points. However, it does not demand this discernibility to be symmetric.

Consider, for example, a two-point set $X = \{p, q\}$ with the topology $\tau = \{\emptyset, \{p\}, \{p,q\}\}$. This space is often called the Sierpiński space. To check the $T_0$ condition, we only need to examine the pair of distinct points $(p, q)$. The open set $U = \{p\}$ contains $p$ but not $q$. Therefore, the condition is met, and $(X, \tau)$ is a $T_0$ space [@problem_id:1672438]. Note the asymmetry: there is no open set that contains $q$ but not $p$.

#### $T_1$ (Fréchet) Spaces

The $T_1$ axiom strengthens the $T_0$ condition by requiring the separation to be possible in both directions for any pair of distinct points.

**Definition ($T_1$ Space):** A [topological space](@entry_id:149165) $(X, \tau)$ is a **$T_1$ space**, or **Fréchet space**, if for every pair of distinct points $x, y \in X$, there exists an open set $U$ containing $x$ but not $y$, and an open set $V$ containing $y$ but not $x$.

Clearly, any $T_1$ space is also a $T_0$ space. The converse, however, is not true. The Sierpiński space discussed above is $T_0$ but not $T_1$, as no open set contains $q$ without also containing $p$ [@problem_id:1672438].

The $T_1$ property has a remarkably simple and powerful equivalent characterization concerning [closed sets](@entry_id:137168).

**Theorem:** A [topological space](@entry_id:149165) $X$ is a $T_1$ space if and only if every singleton set $\{x\}$ is closed for all $x \in X$.

**Proof:**
($\Rightarrow$) Assume $X$ is a $T_1$ space. To show that $\{x\}$ is closed for some $x \in X$, we must show that its complement, $X \setminus \{x\}$, is open. For any point $y \in X \setminus \{x\}$, we have $y \neq x$. By the $T_1$ definition, there exists an open set $V_y$ such that $y \in V_y$ and $x \notin V_y$. This implies $V_y \subseteq X \setminus \{x\}$. Since this is true for every $y \in X \setminus \{x\}$, we can write $X \setminus \{x\} = \bigcup_{y \in X \setminus \{x\}} V_y$. As a union of open sets, $X \setminus \{x\}$ is open.

($\Leftarrow$) Assume every singleton set $\{x\}$ is closed. Let $x, y$ be distinct points in $X$. Then $\{y\}$ is a [closed set](@entry_id:136446), so its complement $U = X \setminus \{y\}$ is open. By construction, $x \in U$ and $y \notin U$. Similarly, since $\{x\}$ is closed, $V = X \setminus \{x\}$ is an open set such that $y \in V$ and $x \notin V$. This satisfies the definition of a $T_1$ space.

Since a finite union of closed sets is closed, an immediate corollary is that in a $T_1$ space, every finite subset is closed [@problem_id:1672463].

A canonical example of a space that is $T_1$ but not $T_2$ (Hausdorff, defined next) is an infinite set $X$ endowed with the **[cofinite topology](@entry_id:138582)**. In this topology, a set is open if it is empty or its complement is finite. Let $x, y$ be distinct points in $X$. The set $U = X \setminus \{y\}$ is open because its complement, $\{y\}$, is finite. We have $x \in U$ and $y \notin U$. Symmetrically, $V = X \setminus \{x\}$ is an open set containing $y$ but not $x$. Thus, the space is $T_1$ [@problem_id:1672428].

### $T_2$ (Hausdorff) Spaces: A Foundation for Analysis

While the $T_1$ axiom ensures that points are topologically separate, the Hausdorff condition is the cornerstone for most of analysis, guaranteeing that points can be placed in completely disjoint open "bubbles".

**Definition ($T_2$ Space):** A topological space $(X, \tau)$ is a **$T_2$ space**, or **Hausdorff space**, if for any two distinct points $x, y \in X$, there exist disjoint open sets $U, V \in \tau$ (i.e., $U \cap V = \emptyset$) such that $x \in U$ and $y \in V$.

The Hausdorff property implies the $T_1$ property, since if $x \in U$ and $y \in V$ with $U \cap V = \emptyset$, then $U$ is an open set containing $x$ but not $y$, and vice versa. The [cofinite topology](@entry_id:138582) on an infinite set demonstrates that the converse is false. In that space, any two non-empty open sets $U$ and $V$ have finite complements. The complement of their intersection, $X \setminus (U \cap V) = (X \setminus U) \cup (X \setminus V)$, is a finite union of [finite sets](@entry_id:145527), and thus finite. Since $X$ is infinite, this means $U \cap V$ must be non-empty. Therefore, no two distinct points can be separated by [disjoint open sets](@entry_id:150704), and the space is not Hausdorff [@problem_id:1672428].

The crucial role of the Hausdorff condition is underscored by its relationship with the convergence of sequences. In spaces that feel familiar, like the real line, a convergent sequence has only one possible limit. This property is guaranteed by the $T_2$ axiom.

**Theorem:** In a Hausdorff space, every convergent sequence has a unique limit.

**Proof:** Let $X$ be a Hausdorff space and let $(x_n)$ be a sequence in $X$. Suppose $(x_n)$ converges to two distinct points, $L_1$ and $L_2$. Since $X$ is Hausdorff and $L_1 \neq L_2$, there exist [disjoint open sets](@entry_id:150704) $U_1$ and $U_2$ with $L_1 \in U_1$ and $L_2 \in U_2$. By the definition of convergence, since $(x_n) \to L_1$, there exists an integer $N_1$ such that for all $n > N_1$, $x_n \in U_1$. Similarly, since $(x_n) \to L_2$, there exists an integer $N_2$ such that for all $n > N_2$, $x_n \in U_2$. Let $N = \max(N_1, N_2)$. Then for any $n > N$, we must have $x_n \in U_1$ and $x_n \in U_2$, which means $x_n \in U_1 \cap U_2$. But this is a contradiction, as $U_1 \cap U_2 = \emptyset$. Therefore, the limit must be unique.

The contrapositive of this theorem provides a powerful test for non-Hausdorff spaces. Consider a three-point set $X = \{x_1, x_2, x_3\}$ with the topology $\tau = \{\emptyset, \{x_1\}, \{x_1, x_2\}, X\}$. The constant sequence $a_n = x_1$ for all $n$ converges to $x_1$, as every neighborhood of $x_1$ contains all terms of the sequence. However, it also converges to $x_2$, since the open neighborhoods of $x_2$ are $\{x_1, x_2\}$ and $X$, both of which contain $x_1$. It even converges to $x_3$, whose only neighborhood is $X$. Since this sequence has multiple limits, the space cannot be Hausdorff [@problem_id:1672459].

Another fundamental characterization of Hausdorff spaces involves the [product topology](@entry_id:154786). The **diagonal** of a set $X$ is the subset $\Delta = \{(x,x) \mid x \in X\}$ of the Cartesian product $X \times X$.

**Theorem:** A [topological space](@entry_id:149165) $X$ is Hausdorff if and only if the diagonal $\Delta$ is a closed subset of $X \times X$ (with the product topology).

**Proof:**
($\Rightarrow$) Assume $X$ is Hausdorff. To show $\Delta$ is closed, we show its complement $(X \times X) \setminus \Delta$ is open. A point $(x,y)$ is in the complement if and only if $x \neq y$. Since $X$ is Hausdorff, there exist disjoint open sets $U, V \subset X$ with $x \in U$ and $y \in V$. The set $U \times V$ is an [open neighborhood](@entry_id:268496) of $(x,y)$ in the [product topology](@entry_id:154786). For any point $(u,v) \in U \times V$, we have $u \in U$ and $v \in V$. Since $U \cap V = \emptyset$, $u \neq v$, so $(u,v) \notin \Delta$. Thus, $U \times V \subseteq (X \times X) \setminus \Delta$. Since every point in the complement has such an [open neighborhood](@entry_id:268496) contained within the complement, the complement is open.

($\Leftarrow$) Assume $\Delta$ is closed in $X \times X$. Let $x, y$ be distinct points in $X$. Then $(x,y) \notin \Delta$, so $(x,y)$ is in the open set $(X \times X) \setminus \Delta$. By the definition of the product topology, there must exist a basic open set $U \times V$ such that $(x,y) \in U \times V$ and $U \times V \subseteq (X \times X) \setminus \Delta$. This means $x \in U$, $y \in V$, and for any $(u,v) \in U \times V$, we have $u \neq v$. This implies that $U \cap V = \emptyset$. Thus, we have found disjoint open neighborhoods for $x$ and $y$.

This property is illustrated clearly by considering a two-point set $S=\{0,1\}$ with different topologies [@problem_id:1672455]. If $S$ has the [trivial topology](@entry_id:154009), its product with itself is also trivial. The diagonal $\Delta = \{(0,0), (1,1)\}$ is not closed, reflecting that the space is not Hausdorff. If $S$ has the [discrete topology](@entry_id:152622), it is Hausdorff. The [product space](@entry_id:151533) is also discrete, meaning every subset, including $\Delta$, is closed.

### The Higher Axioms: Separating Points and Sets

The next level in the hierarchy, consisting of regular and [normal spaces](@entry_id:154073), moves beyond separating points to separating points from closed sets and [closed sets](@entry_id:137168) from one another. By convention, these properties are typically defined on $T_1$ spaces, leading to the definitions of $T_3$ and $T_4$ spaces.

#### $T_3$ (Regular) Spaces

A [regular space](@entry_id:155336) allows for the separation of a point from a closed set that does not contain it.

**Definition ($T_3$ Space):** A [topological space](@entry_id:149165) is **regular** if for any [closed set](@entry_id:136446) $C$ and any point $x \notin C$, there exist [disjoint open sets](@entry_id:150704) $U$ and $V$ such that $x \in U$ and $C \subseteq V$. A **$T_3$ space** is a regular $T_1$ space.

Every $T_3$ space is also a $T_2$ (Hausdorff) space. To see this, let $x, y$ be distinct points. Since the space is $T_1$, $\{y\}$ is a closed set. As $x \notin \{y\}$, we can apply the regularity condition to the point $x$ and the closed set $\{y\}$ to obtain [disjoint open sets](@entry_id:150704) separating them.

Regularity has a useful equivalent formulation in terms of neighborhoods.

**Theorem:** A $T_1$ space $X$ is regular if and only if for every point $x \in X$ and every [open neighborhood](@entry_id:268496) $U$ of $x$, there exists an open neighborhood $V$ of $x$ such that its closure, $\overline{V}$, is contained in $U$.

**Proof:**
($\Rightarrow$) Assume $X$ is regular. Let $x \in X$ and let $U$ be an open neighborhood of $x$. Then $C = X \setminus U$ is a closed set not containing $x$. By regularity, there exist disjoint open sets $V$ and $W$ such that $x \in V$ and $C \subseteq W$. Since $V$ and $W$ are disjoint, $V \subseteq X \setminus W$. Because $W$ is open, $X \setminus W$ is closed. Therefore, the closure of $V$ must be contained in this [closed set](@entry_id:136446): $\overline{V} \subseteq X \setminus W$. Finally, since $C \subseteq W$, we have $X \setminus W \subseteq X \setminus C = U$. Combining these inclusions, we get $\overline{V} \subseteq U$ [@problem_id:1672469].

($\Leftarrow$) Assume the neighborhood-closure condition holds. Let $C$ be a closed set and $x \notin C$. Then $U = X \setminus C$ is an [open neighborhood](@entry_id:268496) of $x$. By the condition, there exists an [open neighborhood](@entry_id:268496) $V$ of $x$ such that $\overline{V} \subseteq U$. Let $W = X \setminus \overline{V}$. Then $W$ is an open set, and since $\overline{V} \subseteq U = X \setminus C$, it follows that $C \subseteq X \setminus U \subseteq X \setminus \overline{V} = W$. Furthermore, $V$ and $W$ are disjoint by construction. Thus, the space is regular.

An important result states that adding [local compactness](@entry_id:272878) to the Hausdorff condition is sufficient to guarantee regularity.
**Theorem:** Every locally compact Hausdorff space is a $T_3$ (regular) space [@problem_id:1672451].

#### $T_4$ (Normal) Spaces

Normality is the next step up, allowing for the separation of any two disjoint closed sets.

**Definition ($T_4$ Space):** A [topological space](@entry_id:149165) is **normal** if for any two disjoint closed sets $C_1$ and $C_2$, there exist [disjoint open sets](@entry_id:150704) $U_1$ and $U_2$ such that $C_1 \subseteq U_1$ and $C_2 \subseteq U_2$. A **$T_4$ space** is a normal $T_1$ space.

A $T_4$ space is automatically a $T_3$ space. To see this, let $C$ be a closed set and $x \notin C$. In a $T_1$ space, $\{x\}$ is a closed set. We now have two disjoint closed sets, $\{x\}$ and $C$. By normality, we can find [disjoint open sets](@entry_id:150704) separating them, which is precisely the regularity condition.

The class of [normal spaces](@entry_id:154073) is extremely important, as it includes all metric spaces and all compact Hausdorff spaces. The proof that [metric spaces](@entry_id:138860) are normal provides a beautiful and constructive method that is central to [general topology](@entry_id:152375).

**Theorem:** Every [metric space](@entry_id:145912) $(X, d)$ is a $T_4$ (normal) space.

**Sketch of Proof:** Let $A$ and $B$ be two disjoint, non-empty, closed subsets of $X$. For any point $x \in X$, the distance from $x$ to a set $S$, defined as $d(x, S) = \inf_{s \in S} d(x, s)$, is a continuous function of $x$. Because $A$ and $B$ are closed and disjoint, for any $x \in X$, the denominator $d(x, A) + d(x, B)$ is never zero. We can then define the **Urysohn function**:
$$ f(x) = \frac{d(x, A)}{d(x, A) + d(x, B)} $$
This function $f: X \to [0, 1]$ is continuous. For any $a \in A$, $d(a, A) = 0$, so $f(a) = 0$. For any $b \in B$, $d(b, B) = 0$, so $f(b) = 1$. The sets $U = f^{-1}([0, 1/2))$ and $V = f^{-1}((1/2, 1])$ are then disjoint open sets (as preimages of open sets under a continuous function) with $A \subseteq U$ and $B \subseteq V$. This demonstrates normality. This construction is a specific instance of the more general **Urysohn's Lemma**, which states that a space is normal if and only if any two disjoint closed sets can be separated by a continuous function. The problem in [@problem_id:1672414] provides a concrete calculation of this function for two disjoint closed disks in $\mathbb{R}^2$.

### Subtleties and Important Counterexamples

While the axioms form a hierarchy ($T_4 \Rightarrow T_3 \Rightarrow T_2 \Rightarrow T_1 \Rightarrow T_0$), the reverse implications do not hold. We have already seen examples distinguishing $T_0$, $T_1$, and $T_2$. The distinctions between the higher axioms are more subtle and require more sophisticated counterexamples.

- **A [regular space](@entry_id:155336) that is not normal:** The hierarchy $T_4 \Rightarrow T_3$ is also strict. A famous counterexample is the **Sorgenfrey plane**, $S = \mathbb{R}_l \times \mathbb{R}_l$, where $\mathbb{R}_l$ is the real line with the [lower-limit topology](@entry_id:155881) (basis of intervals $[a,b)$). The Sorgenfrey plane is the product of two [regular spaces](@entry_id:154729) and is therefore regular. However, it can be shown that $S$ is not normal. The proof involves showing that $S$ is separable (contains a [countable dense subset](@entry_id:147670) like $\mathbb{Q} \times \mathbb{Q}$) but also contains an uncountable closed discrete subset (the "anti-diagonal" $D = \{(x, -x) \mid x \in \mathbb{R}\}$). In a normal [separable space](@entry_id:149917), every closed discrete subset must be countable. The existence of $D$ thus implies that the Sorgenfrey plane cannot be normal [@problem_id:1672443].

- **Normality is not Hereditary:** A property is called **hereditary** if every subspace of a space with that property also has the property. The properties $T_0, T_1, T_2$, and regularity are all hereditary. Normality, however, is not. This means a subspace of a normal space is not guaranteed to be normal. The classic [counterexample](@entry_id:148660) is the **Tychonoff plank**. Let $\Omega_1 = [0, \omega_1]$ be the set of [ordinals](@entry_id:150084) up to the [first uncountable ordinal](@entry_id:156023) $\omega_1$, and let $\Omega_0 = [0, \omega]$ be the set of ordinals up to the first infinite ordinal $\omega$. The [product space](@entry_id:151533) $X = \Omega_1 \times \Omega_0$ is compact and Hausdorff, and therefore normal. Now consider the subspace $Y = X \setminus \{(\omega_1, \omega)\}$, which is the full space with one "corner point" removed. Within this space $Y$, the sets $A = \{\omega_1\} \times [0, \omega)$ and $B = [0, \omega_1) \times \{\omega\}$ are disjoint and closed. However, it can be proven that any open set containing $A$ must intersect any open set containing $B$. Therefore, these two [closed sets](@entry_id:137168) cannot be separated by disjoint open sets, proving that the subspace $Y$ is not normal [@problem_id:1672466].

Understanding these axioms and their interrelations is fundamental to the study of topology, providing the necessary framework for constructing proofs and understanding the scope and limitations of major theorems.