## Introduction
In the study of [general topology](@entry_id:152375), certain examples stand out not for their simplicity, but for the profound clarity they bring to complex theoretical boundaries. The Niemytzki plane, also known as the Moore plane, is one such paramount example. While its construction seems straightforward, its properties challenge our intuition and provide definitive answers to questions about the hierarchy of topological axioms. It serves as the canonical counterexample that disentangles properties like regularity from normality, and separability from second-[countability](@entry_id:148500), which might otherwise seem inextricably linked. This article provides a comprehensive exploration of this fascinating space. In the first chapter, **Principles and Mechanisms**, we will deconstruct the definition of the Niemytzki topology and analyze its unique properties. Following this, the **Applications and Interdisciplinary Connections** chapter will situate the plane within the broader mathematical landscape, focusing on its crucial role as a repository of counterexamples. Finally, the **Hands-On Practices** chapter offers guided problems to solidify your understanding and engage directly with the plane's counter-intuitive characteristics.

## Principles and Mechanisms

The Niemytzki plane, also known as the Moore plane, stands as a cornerstone example in [general topology](@entry_id:152375). While its definition is deceptively simple, its properties provide profound insights and serve as critical counterexamples that delineate the boundaries between various topological concepts. This chapter will deconstruct the plane's definition, explore its local and global topological structure, and culminate in its most famous application: demonstrating that a [regular space](@entry_id:155336) need not be normal.

### Defining the Niemytzki Plane Topology

The underlying set for the Niemytzki plane is the closed [upper half-plane](@entry_id:199119) of the Euclidean plane, which we denote as $L$.
$$ L = \{(x, y) \in \mathbb{R}^2 \mid y \ge 0\} $$
The topology on $L$ is not the standard subspace topology inherited from $\mathbb{R}^2$. Instead, it is defined by specifying a [local basis](@entry_id:151573) for each point, with the nature of the basis elements depending on whether the point lies in the open [upper half-plane](@entry_id:199119) or on the x-axis.

Let $P = \{(x, y) \in L \mid y > 0\}$ be the open [upper half-plane](@entry_id:199119) and let $X = \{(x, 0) \in L \mid x \in \mathbb{R}\}$ be the x-axis. The basis for the Niemytzki topology is defined as follows:

1.  **For a point $p = (x, y) \in P$ (where $y > 0$):** The basis elements are the standard open Euclidean disks centered at $p$ with a radius $r$ that is small enough to ensure the disk remains within $P$. That is, for any $r$ such that $0  r \le y$, the set $B_r(p) = \{(x', y') \in L \mid (x'-x)^2 + (y'-y)^2  r^2\}$ is a basis element. In essence, the topology on $P$ is identical to its standard Euclidean topology.

2.  **For a point $p = (x, 0) \in X$ (on the x-axis):** The basis elements are sets of the form $\{p\} \cup D$, where $D$ is any open disk in the upper half-plane $P$ that is tangent to the x-axis at $p$. Specifically, for any $r > 0$, the set $U_r(p) = \{p\} \cup \{(u, v) \in \mathbb{R}^2 \mid (u-x)^2 + (v-r)^2  r^2\}$ is a basis element.

This hybrid definition is the source of all the plane's unique characteristics. While points in the [upper half-plane](@entry_id:199119) behave familiarly, points on the x-axis have "teardrop" or "raindrop" shaped neighborhoods that include the point itself plus a disk "hanging" from it into the upper plane.

### The Anatomy of Neighborhoods

The unusual nature of neighborhoods for points on the x-axis has immediate and non-intuitive consequences. A common misconception is to think of subsets of the x-axis in terms of their properties in the standard one-dimensional topology.

For example, consider a set which is an [open interval](@entry_id:144029) on the x-axis, such as $S = \{(x, 0) \mid a  x  b\}$ for some $a  b$. In the [standard topology](@entry_id:152252) on $\mathbb{R}$, this is an open set. However, in the Niemytzki plane, $S$ is **not** an open set. To be open, for any point $p \in S$, there must exist a basis element $B$ such that $p \in B \subseteq S$. But any basis element for $p = (x, 0) \in S$ is of the form $\{p\} \cup D$, where $D$ is a non-empty open disk in the [upper half-plane](@entry_id:199119) $P$. Such a basis element necessarily contains points with a positive $y$-coordinate, which are not in $S$. Therefore, no basis element around any point of $S$ is contained within $S$, proving $S$ is not open [@problem_id:1584907].

This same logic implies that for any point $p=(a,0)$ on the x-axis, its interior in the Niemytzki plane is the [empty set](@entry_id:261946). Any open set containing $p$ must also contain points not in the singleton set $\{p\}$ (specifically, points from the tangent disk), so no open set can be a subset of $\{p\}$ [@problem_id:1584855].

Understanding the geometry of these neighborhoods is crucial. A set $N$ is a neighborhood of a point $p_0=(x_0, 0)$ if and only if it fully contains some basis element $\{p_0\} \cup D_r$, where $D_r$ is a disk of radius $r>0$ centered at $(x_0, r)$. For instance, consider the origin $p_0 = (0,0)$. The parabolic region $S_C = \{(x,y) \mid y \ge x^2\}$ is a neighborhood of the origin because for a sufficiently small radius $r$ (e.g., $r \le 0.5$), the entire tangent disk $D_r$ is contained within the region defined by $y \ge x^2$. In contrast, the "V-shaped" region $S_D = \{(x,y) \mid y \le |x|\}$ is **not** a neighborhood of the origin. Any tangent disk $D_r$ contains its center, $(0,r)$. For this point, $y=r$ and $x=0$, so the condition $y \le |x|$ becomes $r \le 0$, which is false for any $r>0$. Since the center of the disk is not in $S_D$, the disk is not a subset of $S_D$, and thus no basis element around the origin is contained in $S_D$ [@problem_id:1584875].

### Topological Structure of Key Subspaces

The unusual neighborhood structure dramatically affects the topology of subspaces. The most important examples are horizontal lines.

Consider a horizontal line $Y = \{(x, c) \mid x \in \mathbb{R}\}$ for some fixed constant $c > 0$. A point $q = (a, c) \in Y$ is in the open [upper half-plane](@entry_id:199119) $P$. Its neighborhoods in the Niemytzki plane are standard Euclidean disks. The intersection of such a disk $B_r(q)$ (with $r \le c$) with the line $Y$ is the set $\{(x, c) \mid (x-a)^2  r^2\}$, which is an open interval on the line $Y$ centered at $a$. This demonstrates that the subspace topology on $Y$ is precisely the standard Euclidean topology on $\mathbb{R}$ [@problem_id:1584885].

The situation on the x-axis, $X = \{(x, 0) \mid x \in \mathbb{R}\}$, is strikingly different. Let $p = (a, 0)$ be any point in $X$. A basis element for $p$ in the Niemytzki plane is $B = \{p\} \cup D$, where $D$ is a tangent disk in $P$. When we intersect this with the subspace $X$, we get $B \cap X = (\{p\} \cup D) \cap X = \{p\}$. This means that for any point $p \in X$, the singleton set $\{p\}$ is open in the subspace topology on $X$. Since any subset of $X$ can be written as a union of its points (which are open sets), every subset of $X$ is open in the subspace topology. Therefore, the subspace topology on the x-axis is the **discrete topology** [@problem_id:1584877] [@problem_id:1584885].

This single result—that the x-axis is an uncountable discrete subspace—is the key to unlocking many of the Niemytzki plane's properties.

### A Survey of Topological Properties

With a firm grasp of the local structure, we can now classify the Niemytzki plane with respect to major topological properties. It serves as a classic [counterexample](@entry_id:148660) in many cases.

**Separability:** A space is **separable** if it contains a [countable dense subset](@entry_id:147670). The Niemytzki plane is separable. Consider the set $S = \{(p, q) \mid p, q \in \mathbb{Q}, q > 0\}$, which consists of all points in the open upper half-plane with rational coordinates. This set is countable. It is also dense in the Niemytzki plane because any basis element—whether a standard disk in $P$ or a tangent disk attached to $X$—is a non-empty open set in the Euclidean sense and must therefore contain a point with rational coordinates. Thus, $S$ intersects every basis element, making it a [countable dense subset](@entry_id:147670) [@problem_id:15905] [@problem_id:15915]. Another valid countable [dense set](@entry_id:142889) is $D = \{(p, q) \mid p, q \in \mathbb{Q}, q \ge 0\}$, as it is a superset of $S$ and also countable [@problem_id:15915].

**Countability Axioms:** A space is **first-countable** if every point has a countable [neighborhood basis](@entry_id:148053). It is **second-countable** if the topology has a [countable basis](@entry_id:155278). The Niemytzki plane is first-countable but not second-countable.
*   **First-Countable:** The Niemytzki plane is first-countable. For points in the open upper half-plane $P$, the set of open disks with rational radii forms a countable [local basis](@entry_id:151573). For a point $p$ on the x-axis, the set of basis neighborhoods $\{U_r(p) \mid r \in \mathbb{Q}, r>0\}$, where the tangent disk has a rational radius, is a countable [local basis](@entry_id:151573) for $p$.
*   **Not Second-Countable:** Second-countability is a [hereditary property](@entry_id:151340), meaning every subspace of a [second-countable space](@entry_id:141954) is second-countable. We know the x-axis $X$ is a subspace of the Niemytzki plane. However, $X$ has the discrete topology and is uncountable. A discrete space is second-countable if and only if it is countable (since a basis must contain all the singleton sets). As $X$ is uncountable, it is not second-countable. Therefore, the Niemytzki plane cannot be second-countable [@problem_id:1584877] [@problem_id:15905].

**The Lindelöf Property:** A space is **Lindelöf** if every [open cover](@entry_id:140020) has a countable [subcover](@entry_id:151408). The Niemytzki plane is not Lindelöf. A [closed subspace](@entry_id:267213) of a Lindelöf space must be Lindelöf. The x-axis $X$ is a closed set in the Niemytzki plane (since its complement, $P$, is open). However, $X$ is not Lindelöf. The collection of open sets $\{\{p\} \mid p \in X\}$ is an [open cover](@entry_id:140020) of the subspace $X$. Since $X$ is uncountable, this cover has no countable [subcover](@entry_id:151408). As $X$ is a closed, non-Lindelöf subspace, the entire Niemytzki plane cannot be Lindelöf [@problem_id:1584876].

**Metrizability:** A space is **metrizable** if its topology can be induced by a metric. The Niemytzki plane is not metrizable. One of the most powerful theorems connecting these properties states that a space is separable and metrizable if and only if it is second-countable. The Niemytzki plane is separable but not second-countable. This contradiction proves it cannot be metrizable [@problem_id:15905].

**Baire Space:** A space is a **Baire space** if the intersection of any countable collection of dense open sets is itself dense. Surprisingly, the Niemytzki plane **is** a Baire space. This can be shown elegantly by considering its subspaces. The open [upper half-plane](@entry_id:199119) $P$ is an open, [dense subspace](@entry_id:261392) of the Niemytzki plane. As an open subset of $\mathbb{R}^2$ (a complete [metric space](@entry_id:145912)), $P$ is a Baire space. A topological space that contains a dense open Baire subspace is itself a Baire space. Thus, the Niemytzki plane is a Baire space [@problem_id:15905].

### A Classic Counterexample: Regularity without Normality

The [separation axioms](@entry_id:154482) classify how well points and [closed sets](@entry_id:137168) can be distinguished by open sets. The Niemytzki plane is a **Tychonoff space** (also called completely regular or $T_{3\frac{1}{2}}$), which implies it is also **regular** ($T_3$). This means that for any closed set $F$ and any point $p \notin F$, there exist disjoint open sets $U$ and $V$ such that $p \in U$ and $F \subseteq V$.

The critical question is whether it is **normal** ($T_4$). A space is normal if any two [disjoint closed sets](@entry_id:152178) can be separated by [disjoint open sets](@entry_id:150704). The Niemytzki plane's fame comes from the fact that it is regular but **not normal**.

To prove this, we construct two disjoint closed sets that cannot be separated. Consider the partition of the x-axis into points with rational and irrational coordinates:
*   $A = \{(q, 0) \mid q \in \mathbb{Q}\}$
*   $B = \{(r, 0) \mid r \in \mathbb{R} \setminus \mathbb{Q}\}$

As established, the x-axis $X$ is a [closed subspace](@entry_id:267213) with the [discrete topology](@entry_id:152622). In a discrete space, every subset is closed. Thus, $A$ and $B$ are [closed sets](@entry_id:137168) within the subspace $X$. Since $X$ is itself closed in the Niemytzki plane, $A$ and $B$ are [closed sets](@entry_id:137168) in the entire plane. They are also clearly disjoint.

The central theorem is that any open set $U$ containing $A$ must intersect any open set $V$ containing $B$ [@problem_id:1584869]. The proof is a sophisticated argument by contradiction that beautifully combines the plane's topology with the properties of the real numbers.

Assume for contradiction that there exist disjoint open sets $U$ and $V$ with $A \subseteq U$ and $B \subseteq V$.
1.  For each point $p \in A$ (a rational point on the axis), because $U$ is open, it must contain a basis neighborhood of $p$. This neighborhood can be characterized by the radius $r_p > 0$ of its tangent disk, which lies entirely in $U$.
2.  Similarly, for each point in $B$, there is a tangent disk of some radius contained in $V$.
3.  The core of the argument involves analyzing the set of radii $\{r_p \mid p \in A\}$. We partition the set $A$ into a countable number of subsets. For each integer $n > 0$, define $A_n = \{ p \in A \mid r_p \ge 1/n \}$. Since every $p \in A$ has some positive radius $r_p$, we have $A = \bigcup_{n=1}^{\infty} A_n$.
4.  The argument now involves the Baire Category Theorem. Identifying $A$ with the set of rational numbers $\mathbb{Q}$, we have $\mathbb{Q} = \bigcup_{n=1}^{\infty} A_n$.
5.  A standard proof using the Baire Category Theorem shows that for at least one integer $N$, the closure of the set $A_N$ (in the [standard topology](@entry_id:152252) of $\mathbb{R}$) must contain a non-empty [open interval](@entry_id:144029), say $(a,b)$.
6.  This consequence is profound: within the interval $(a,b)$, there is a dense "thicket" of [rational points](@entry_id:195164) from $A_N$, and for all of these points, the tangent disks inside $U$ have a radius of at least $1/N$. The geometric configuration of these numerous, relatively "fat" disks pushing up from the x-axis makes it impossible for an open set $V$ to cover the irrational points in $(a,b)$ without intersecting one of these disks. This leads to the required contradiction that $U \cap V \neq \emptyset$.

This elegant proof solidifies the Niemytzki plane's status as a fundamental object of study, demonstrating with perfect clarity that the property of regularity does not imply normality.