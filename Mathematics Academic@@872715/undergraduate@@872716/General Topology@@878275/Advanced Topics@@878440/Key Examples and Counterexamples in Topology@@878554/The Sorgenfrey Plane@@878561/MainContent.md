## Introduction
In the study of [general topology](@entry_id:152375), understanding the precise limits of theorems is as crucial as knowing the theorems themselves. While familiar spaces like the Euclidean plane provide our core intuition, more exotic constructions are needed to test the boundaries of [topological properties](@entry_id:154666). The Sorgenfrey plane, denoted $\mathbb{R}_l^2$, stands out as one of the most important and instructive of these constructions, serving as a rich source of counterexamples that sharpen our understanding of the axioms.

## Principles and Mechanisms

We now undertake a systematic investigation of the topological structure of the Sorgenfrey plane. This space, denoted as $\mathbb{R}_l^2$, is a cornerstone of [general topology](@entry_id:152375), primarily for its role as a rich source of counterexamples that delineate the boundaries of key theorems. By dissecting its properties, we gain a deeper appreciation for the subtleties of topological axioms and their interrelationships. Our inquiry will proceed from foundational definitions to the more complex properties that establish the Sorgenfrey plane's unique character.

### The Basic Topology of the Sorgenfrey Plane

The Sorgenfrey plane is constructed as the Cartesian product of two Sorgenfrey lines, $\mathbb{R}_l \times \mathbb{R}_l$. The **Sorgenfrey line**, $\mathbb{R}_l$, is the set of real numbers $\mathbb{R}$ endowed with the **[lower-limit topology](@entry_id:155881)**. The basis for this topology is the collection of all half-open intervals of the form $[a, b)$, where $a  b$ are real numbers.

The topology on the Sorgenfrey plane, $\mathbb{R}_l^2$, is the standard **product topology**. A basis for this topology is therefore formed by all possible products of basis elements from each factor space. This results in a basis consisting of all rectangular sets of the form:
$$
B = [a, b) \times [c, d) = \{ (x, y) \in \mathbb{R}^2 \mid a \le x  b, c \le y  d \}
$$
for real numbers $a, b, c, d$ with $a  b$ and $c  d$. Visually, these basis elements are rectangles in the Cartesian plane that include their left and bottom boundaries but exclude their right and top boundaries. This seemingly minor modification of the standard Euclidean open rectangles leads to profound topological consequences.

### Comparison with the Standard Euclidean Topology

A natural first step in understanding any new topology on $\mathbb{R}^2$ is to compare it with the familiar **standard Euclidean topology**, which we denote $\mathcal{T}_E$. The basis for $\mathcal{T}_E$ consists of open rectangles $(a, b) \times (c, d)$. Let $\mathcal{T}_S$ denote the Sorgenfrey plane topology.

The Sorgenfrey topology $\mathcal{T}_S$ is **strictly finer** than the Euclidean topology $\mathcal{T}_E$. This means that every open set in $\mathcal{T}_E$ is also an open set in $\mathcal{T}_S$, but the converse is not true.

To establish the first part of this claim, we need only show that every basis element of $\mathcal{T}_E$ is an open set in $\mathcal{T}_S$. Consider an arbitrary Euclidean open rectangle $(a, b) \times (c, d)$. We can express this set as a union of Sorgenfrey basis elements:
$$
(a, b) \times (c, d) = \bigcup_{x \in (a, b), y \in (c, d)} [x, b) \times [y, d)
$$
Since the union of open sets is open, it follows that any Euclidean open rectangle is open in $\mathcal{T}_S$. By extension, any arbitrary Euclidean open set (which is a union of such rectangles) is also open in the Sorgenfrey topology. For instance, the Euclidean open disk $S = \{ (x, y) \mid x^2 + y^2  4 \}$ is an open set in the Sorgenfrey plane [@problem_id:1565775] [@problem_id:1586867].

To show the "strict" part of the relationship, we must present a set that is open in $\mathcal{T}_S$ but not in $\mathcal{T}_E$. The most straightforward example is any Sorgenfrey basis element itself, such as $B = [0, 1) \times [0, 1)$. This set is not open in the Euclidean topology. Consider the point $(0, 0) \in B$. Any Euclidean basis neighborhood of $(0, 0)$ is a rectangle of the form $(-\epsilon, \epsilon) \times (-\delta, \delta)$ for $\epsilon, \delta > 0$. Such a neighborhood will always contain points with negative coordinates, which are not in $B$. Therefore, no Euclidean neighborhood of $(0, 0)$ is contained within $B$, proving that $B$ is not open in $\mathcal{T}_E$ [@problem_id:1586867].

This finer topology endows the Sorgenfrey plane with more open sets, which allows for finer distinctions between points but also complicates certain large-scale properties, as we will see. For example, while the Euclidean open disk $S$ is open in $\mathbb{R}_l^2$, it is no longer closed. Its complement $S^c = \{ (x, y) \mid x^2 + y^2 \ge 4 \}$ is not open because any basic Sorgenfrey neighborhood of a boundary point like $(-2, 0)$, say $[-2, -2+\epsilon) \times [0, \delta)$, will contain points with $x > -2$ and $y \ge 0$ that are arbitrarily close to $(-2,0)$ and thus lie inside the disk $S$ [@problem_id:1565775].

### Fundamental Separation and Countability Properties

The Sorgenfrey plane satisfies several of the desirable "niceness" [axioms of topology](@entry_id:153192), which confirms it is a well-behaved space in many respects.

#### Separation Axioms

The Sorgenfrey plane is a **Hausdorff** (or $T_2$) space. This means that for any two distinct points $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$, there exist disjoint open sets $U_1$ and $U_2$ such that $P_1 \in U_1$ and $P_2 \in U_2$. This property is inherited from the Sorgenfrey line $\mathbb{R}_l$, which is itself Hausdorff. The proof is constructive. If $x_1 \neq x_2$, say $x_1  x_2$, then $U_1 = [x_1, x_2) \times \mathbb{R}$ and $U_2 = [x_2, x_2+1) \times \mathbb{R}$ are [disjoint open sets](@entry_id:150704) separating the points. If $x_1 = x_2$, then $y_1 \neq y_2$. Say $y_1  y_2$. We can then choose $U_1 = \mathbb{R} \times [y_1, y_2)$ and $U_2 = \mathbb{R} \times [y_2, y_2+1)$. For a concrete example, the points $P = (2, 5)$ and $Q = (2, 3)$ are separated by the disjoint Sorgenfrey [basis sets](@entry_id:164015) $U = [2, 3) \times [5, 6)$ and $V = [2, 3) \times [3, 4)$ [@problem_id:1586882].

More powerfully, the Sorgenfrey plane is a **regular** space. A space is regular if it is $T_1$ (which is weaker than Hausdorff) and for any closed set $C$ and a point $p \notin C$, there exist disjoint open sets $U$ and $V$ such that $p \in U$ and $C \subseteq V$. The proof of regularity for $\mathbb{R}_l^2$ stems from a remarkable property of its basis. The basis elements $[a, b)$ of the Sorgenfrey line are not just open; they are also closed, making them **clopen** sets. A set is closed if its complement is open. The complement of $[a, b)$ is $(-\infty, a) \cup [b, \infty)$, which is a union of two open sets in $\mathbb{R}_l$ and is therefore open. Consequently, the basis elements $[a, b) \times [c, d)$ of the Sorgenfrey plane are also clopen. Any $T_1$ space with a basis of [clopen sets](@entry_id:156588) is necessarily regular. Given $p \notin C$, there is a basis element $B$ such that $p \in B \subseteq X \setminus C$. We can then choose $U = B$ and $V = X \setminus B$. Both are open, disjoint, and separate the point from the closed set. Thus, the Sorgenfrey plane is regular [@problem_id:1570365].

#### Countability Properties

The status of the Sorgenfrey plane with respect to [countability axioms](@entry_id:152407) is more nuanced and is a primary source of its utility as a [counterexample](@entry_id:148660).

*   **First-Countable**: The Sorgenfrey plane **is** first-countable. A space is first-countable if every point has a countable [local basis](@entry_id:151573). For any point $x \in \mathbb{R}_l$, the collection $\{[x, x + \frac{1}{n}) \mid n \in \mathbb{N}\}$ forms a countable [local basis](@entry_id:151573). Since the product of two first-countable spaces is first-countable, the Sorgenfrey plane inherits this property. A countable [local basis](@entry_id:151573) for any point $(x, y) \in \mathbb{R}_l^2$ is given by the collection $\{[x, x + \frac{1}{n}) \times [y, y + \frac{1}{m}) \mid n, m \in \mathbb{N}\}$ [@problem_id:1586859].

*   **Separable**: The Sorgenfrey plane **is** separable. A space is separable if it contains a [countable dense subset](@entry_id:147670). The set $\mathbb{Q} \times \mathbb{Q}$ of points with rational coordinates is a countable set. It is also dense in $\mathbb{R}_l^2$. To see this, consider any non-empty basis element $[a, b) \times [c, d)$. By the density of the rationals in the reals, there exist $q_1, q_2 \in \mathbb{Q}$ such that $a \le q_1  b$ and $c \le q_2  d$. The point $(q_1, q_2)$ is therefore an element of $\mathbb{Q} \times \mathbb{Q}$ that lies within the given basis element. This confirms that $\mathbb{Q} \times \mathbb{Q}$ is dense [@problem_id:1586873] [@problem_id:1586879].

*   **Second-Countable**: The Sorgenfrey plane is **not** second-countable. A space is second-countable if its topology has a [countable basis](@entry_id:155278). This is a stronger condition than being first-countable or separable. The fact that the Sorgenfrey plane is separable but not second-countable is a significant result. We will demonstrate the failure of second-countability in the next section, as it is a direct consequence of the strange behavior of the anti-diagonal.

An important related property is the **[countable chain condition](@entry_id:154445) (ccc)**, which states that any collection of pairwise disjoint, non-empty open sets must be countable. Since the Sorgenfrey plane is separable, it must be ccc. If there were an uncountable collection of [disjoint open sets](@entry_id:150704), the [dense set](@entry_id:142889) $\mathbb{Q} \times \mathbb{Q}$ would have to supply a distinct rational point to each, which is impossible as $\mathbb{Q} \times \mathbb{Q}$ is countable. Therefore, there can be no uncountable collection of pairwise [disjoint open sets](@entry_id:150704) in the Sorgenfrey plane [@problem_id:1586879].

### The Anti-Diagonal: The Locus of Pathological Behavior

Many of the Sorgenfrey plane's most famous properties—particularly its failures—are revealed by examining the subspace known as the **anti-diagonal**, defined as $L = \{ (x, -x) \mid x \in \mathbb{R} \}$.

The central mechanism underlying the behavior of $L$ is the ability to isolate each of its points using a Sorgenfrey basis element. For any point $p = (x_0, -x_0) \in L$, consider the open set $U_{x_0} = [x_0, x_0 + \epsilon) \times [-x_0, -x_0 + \delta)$ for some $\epsilon, \delta > 0$. Let's determine the intersection of this open set with the line $L$. A point $(t, -t)$ is in $U_{x_0} \cap L$ if and only if:
1.  $x_0 \le t  x_0 + \epsilon$
2.  $-x_0 \le -t  -x_0 + \delta$, which is equivalent to $x_0 - \delta  t \le x_0$

Combining these two conditions, we find that the only possibility is $t = x_0$. This means that $U_{x_0} \cap L = \{ (x_0, -x_0) \} = \{p\}$ [@problem_id:1586817]. Since we can find an open set in $\mathbb{R}_l^2$ whose intersection with $L$ is just a single point, that singleton set is open in the subspace topology on $L$. This holds for every point in $L$.

This has immediate and profound consequences:

1.  **$L$ is an Uncountable Discrete Subspace**: Since every singleton subset of $L$ is open in its subspace topology, the subspace $L$ has the **[discrete topology](@entry_id:152622)**. As there is a bijection between $L$ and the [uncountable set](@entry_id:153749) $\mathbb{R}$, $L$ is an uncountable discrete space [@problem_id:1586879].

2.  **Failure of Second-Countability**: A [second-countable space](@entry_id:141954) must have a [countable basis](@entry_id:155278). If $\mathbb{R}_l^2$ were second-countable, every subspace of it, including $L$, would also have to be second-countable. However, an uncountable [discrete space](@entry_id:155685) is not second-countable. In a [discrete space](@entry_id:155685), the collection of all singleton sets forms a basis. For $L$, this is an uncountable collection. Therefore, the Sorgenfrey plane cannot be second-countable.

3.  **Failure of the Lindelöf Property**: A space is **Lindelöf** if every open cover has a countable [subcover](@entry_id:151408). The Sorgenfrey line $\mathbb{R}_l$ is Lindelöf, but the Sorgenfrey plane provides the classic [counterexample](@entry_id:148660) that the product of two Lindelöf spaces need not be Lindelöf. To prove this, we construct an [open cover](@entry_id:140020) of $\mathbb{R}_l^2$ with no countable [subcover](@entry_id:151408). Consider the collection of sets $\mathcal{A} = \{ [x, x+1) \times [-x, -x+1) \mid x \in \mathbb{R} \}$, and let $U = \mathbb{R}_l^2 \setminus L$. The collection $\mathcal{C} = \mathcal{A} \cup \{U\}$ is an [open cover](@entry_id:140020) for the entire plane. The set $U$ covers everything *except* the anti-diagonal $L$. As we showed, each set $A_x = [x, x+1) \times [-x, -x+1)$ from the collection $\mathcal{A}$ covers exactly one point of $L$, namely $(x, -x)$. To cover all of the uncountable points in $L$, any [subcover](@entry_id:151408) of $\mathcal{C}$ must include an uncountable number of sets from $\mathcal{A}$. Therefore, no countable [subcover](@entry_id:151408) exists, and the Sorgenfrey plane is not Lindelöf [@problem_id:1586845].

4.  **Failure of Normality**: The most celebrated property of the Sorgenfrey plane is that it is regular but **not normal**. A space is **normal** if it is $T_1$ and for any two [disjoint closed sets](@entry_id:152178), $C_1$ and $C_2$, there exist [disjoint open sets](@entry_id:150704) $U_1$ and $U_2$ that contain them. The anti-diagonal $L$ once again provides the stage for this [counterexample](@entry_id:148660). Let's partition $L$ into two sets:
    *   $A = \{ (x, -x) \mid x \in \mathbb{Q} \}$ (points on $L$ with rational coordinates)
    *   $B = \{ (x, -x) \mid x \in \mathbb{R} \setminus \mathbb{Q} \}$ (points on $L$ with irrational coordinates)
    These two sets are disjoint, and it can be shown that they are both [closed sets](@entry_id:137168) in the Sorgenfrey plane topology. The [non-normality](@entry_id:752585) of $\mathbb{R}_l^2$ stems from the fact that it is impossible to find disjoint open sets $U_A$ and $U_B$ such that $A \subseteq U_A$ and $B \subseteq U_B$. While the full proof is beyond the scope of this section, it relies on the "northeast-pointing" nature of the Sorgenfrey basis elements and the density of both rational and [irrational numbers](@entry_id:158320). Any open set covering the [dense set](@entry_id:142889) $A$ will inevitably intersect any open set covering $B$. The existence of this pair of inseparable disjoint closed sets definitively shows that the Sorgenfrey plane fails the normality axiom [@problem_id:1586825] [@problem_id:1570365].

### Summary: A Repository of Counterexamples

The Sorgenfrey plane is an indispensable tool for the working topologist. Its properties, both positive and negative, serve to sharpen our understanding of the hierarchy of topological axioms. Let us summarize its key features:

**Properties the Sorgenfrey Plane Possesses:**
*   Hausdorff ($T_2$) and Regular ($T_3$)
*   First-Countable
*   Separable
*   Countable Chain Condition (ccc)

**Properties the Sorgenfrey Plane Lacks:**
*   Second-Countable
*   Lindelöf
*   Normal ($T_4$)
*   Metrizable (since it is separable but not second-countable)

This profile makes $\mathbb{R}_l^2$ the canonical [counterexample](@entry_id:148660) for several important implications that do not hold in [general topology](@entry_id:152375):
*   **Regularity does not imply Normality.**
*   **The product of two Lindelöf spaces is not necessarily Lindelöf.**
*   **A [separable space](@entry_id:149917) is not necessarily second-countable or Lindelöf.**

By studying the mechanisms behind these properties, particularly the unique geometry of its basis and the resulting behavior of the anti-diagonal, we develop a more robust and nuanced intuition for the topological landscape.