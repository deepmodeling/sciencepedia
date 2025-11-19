## Introduction
In the study of topology, the [separation axioms](@entry_id:154482) provide a hierarchical system for [classifying spaces](@entry_id:148422) based on their ability to distinguish points and [closed sets](@entry_id:137168). Building upon the foundation of normal ($T_4$) spaces, which can separate disjoint closed sets, we encounter a stronger and more refined property: complete normality. This concept addresses a key shortcoming of normality—its failure to be inherited by subspaces—by extending separation to a more general pair of sets.

This article provides a comprehensive exploration of completely [normal spaces](@entry_id:154073), also known as $T_5$ or [hereditarily normal spaces](@entry_id:149845). It bridges the gap between the definition of normality and the need for a hereditary version, showing how these two perspectives converge into a single, powerful property. Over the next three chapters, you will gain a deep understanding of this essential topological concept.

The first chapter, **Principles and Mechanisms**, introduces the foundational concept of "[separated sets](@entry_id:152848)" and uses it to define complete normality. It culminates in a rigorous proof that a space is completely normal if and only if it is hereditarily normal. The second chapter, **Applications and Interdisciplinary Connections**, explores the vast classes of spaces that are completely normal, including all metric spaces, and investigates the property's behavior under various topological constructions. Finally, the **Hands-On Practices** section offers a set of curated problems to test and solidify your understanding of how to identify and work with these spaces.

## Principles and Mechanisms

In our exploration of topological spaces, the [separation axioms](@entry_id:154482) provide a crucial framework for [classifying spaces](@entry_id:148422) based on their ability to distinguish points and sets. Having previously examined [normal spaces](@entry_id:154073) ($T_4$), which guarantee that any two disjoint closed sets can be enclosed in disjoint open neighborhoods, we now turn our attention to a stronger and more subtle condition: **complete normality**. This property, also known as hereditary normality or $T_5$ (when combined with the $T_1$ axiom), extends the principle of separation from [closed sets](@entry_id:137168) to a more general class of sets known as "[separated sets](@entry_id:152848)".

### Separated Sets: A Refined Notion of Disjointness

Before defining complete normality, we must first understand the concept of [separated sets](@entry_id:152848). While [disjoint sets](@entry_id:154341) simply have no points in common, [separated sets](@entry_id:152848) satisfy a stricter condition related to their closures.

**Definition:** Two subsets, $A$ and $B$, of a topological space $X$ are said to be **separated** if the closure of each is disjoint from the other. Formally, this means both of the following conditions must hold:
$$
\overline{A} \cap B = \emptyset \quad \text{and} \quad A \cap \overline{B} = \emptyset
$$

It is important to note the subtleties of this definition. If two sets are separated, they are necessarily disjoint, since $A \cap B \subseteq \overline{A} \cap B = \emptyset$. However, the converse is not true; two [disjoint sets](@entry_id:154341) are not necessarily separated. Moreover, [separated sets](@entry_id:152848) need not be closed. Their [closures](@entry_id:747387), $\overline{A}$ and $\overline{B}$, may even intersect.

Consider a few illustrative examples in the space of real numbers $\mathbb{R}$ with its usual topology.

-   Let $A = (0, 1)$ and $B = (1, 2)$. These sets are disjoint. The [closures](@entry_id:747387) are $\overline{A} = [0, 1]$ and $\overline{B} = [1, 2]$. We see that $\overline{A} \cap B = [0, 1] \cap (1, 2) = \emptyset$ and $A \cap \overline{B} = (0, 1) \cap [1, 2] = \emptyset$. Thus, $A$ and $B$ are separated. Notice, however, that their closures are not disjoint: $\overline{A} \cap \overline{B} = \{1\}$.

-   Let's modify this slightly. Consider $A = \{1\}$ and $B = (1, 2)$. These sets are disjoint. The closures are $\overline{A} = \{1\}$ and $\overline{B} = [1, 2]$. We check the separation conditions: $\overline{A} \cap B = \{1\} \cap (1, 2) = \emptyset$. However, $A \cap \overline{B} = \{1\} \cap [1, 2] = \{1\} \neq \emptyset$. Therefore, these sets are *not* separated. The point in $A$ is a [limit point](@entry_id:136272) of $B$. [@problem_id:1539891]

-   Another illuminating example involves a sequence converging to a point. Let $A = \{0\}$ and $B = \{\frac{1}{n} \mid n \in \mathbb{Z}, n > 0\}$. These sets are clearly disjoint. Their [closures](@entry_id:747387) are $\overline{A} = \{0\}$ and $\overline{B} = B \cup \{0\}$, since 0 is the unique limit point of $B$. Checking the conditions: $\overline{A} \cap B = \{0\} \cap B = \emptyset$. But $A \cap \overline{B} = \{0\} \cap (B \cup \{0\}) = \{0\} \neq \emptyset$. Again, these sets are not separated. [@problem_id:1539891]

These simple examples highlight that the notion of "separated" is asymmetric. The failure of separation occurs when a point in one set is also a limit point of the other. A more complex example is found in $\mathbb{R}^2$ with the standard topology. Let $S_1$ be the non-positive x-axis, $S_1 = \{(x, 0) \mid x \leq 0\}$, and let $S_2$ be the graph of $y = \sin(1/x)$ for $x>0$, often called the [topologist's sine curve](@entry_id:142923). [@problem_id:1539879]
The set $S_1$ is closed, so $\overline{S_1} = S_1$. Since points in $S_1$ have non-positive $x$-coordinates and points in $S_2$ have positive $x$-coordinates, the sets are disjoint, and $\overline{S_1} \cap S_2 = \emptyset$.
The closure of $S_2$, however, is more interesting. As $x$ approaches $0$ from the right, the values of $\sin(1/x)$ oscillate infinitely between $-1$ and $1$. Consequently, the closure of $S_2$ includes the vertical line segment from $(0, -1)$ to $(0, 1)$. That is, $\overline{S_2} = S_2 \cup (\{0\} \times [-1, 1])$. The set $S_1$ contains the point $(0,0)$, which is also in this vertical segment. Therefore, $S_1 \cap \overline{S_2}$ is non-empty (it contains the origin), and the sets $S_1$ and $S_2$ are not separated.

### Complete Normality and its Equivalence to Hereditary Normality

With a firm grasp of [separated sets](@entry_id:152848), we can now define completely [normal spaces](@entry_id:154073). The definition extends the logic of [normal spaces](@entry_id:154073) from [disjoint closed sets](@entry_id:152178) to the more general case of [separated sets](@entry_id:152848).

**Definition:** A [topological space](@entry_id:149165) $X$ is **completely normal** if for any two [separated sets](@entry_id:152848) $A$ and $B$ in $X$, there exist disjoint open sets $U$ and $V$ such that $A \subseteq U$ and $B \subseteq V$.

A related concept is that of a [hereditary property](@entry_id:151340). A [topological property](@entry_id:141605) is **hereditary** if, whenever a space $X$ has the property, every subspace of $X$ also has it. For instance, the $T_1$ and $T_2$ (Hausdorff) properties are hereditary, but normality is famously not. This motivates the following definition.

**Definition:** A space $X$ is **hereditarily normal** if every subspace of $X$ is a [normal space](@entry_id:154487).

It turns out that these two seemingly different concepts are, in fact, one and the same. This equivalence is a cornerstone theorem in the study of [separation axioms](@entry_id:154482).

**Theorem:** A [topological space](@entry_id:149165) $X$ is completely normal if and only if it is hereditarily normal. [@problem_id:1663441] [@problem_id:1539904]

**Proof:**

($\implies$) Assume $X$ is completely normal. We want to show it is hereditarily normal. Let $Y$ be any subspace of $X$. To show $Y$ is normal, let $C$ and $D$ be any two [disjoint closed sets](@entry_id:152178) in $Y$. Since they are closed in $Y$, we have $\overline{C}^Y = C$ and $\overline{D}^Y = D$. The closure in the subspace is given by $\overline{C}^Y = \overline{C}^X \cap Y$. Since $D \subseteq Y$, we have $\overline{C}^X \cap D = (\overline{C}^X \cap Y) \cap D = \overline{C}^Y \cap D = C \cap D = \emptyset$. Similarly, $C \cap \overline{D}^X = \emptyset$. Thus, $C$ and $D$ are [separated sets](@entry_id:152848) in the parent space $X$. By the complete normality of $X$, there exist [disjoint open sets](@entry_id:150704) $U, V \subseteq X$ such that $C \subseteq U$ and $D \subseteq V$. The sets $U_Y = U \cap Y$ and $V_Y = V \cap Y$ are then [disjoint open sets](@entry_id:150704) in the subspace $Y$ containing $C$ and $D$, respectively. This proves that $Y$ is normal. Since $Y$ was an arbitrary subspace, $X$ is hereditarily normal.

($\impliedby$) Assume $X$ is hereditarily normal. We want to show it is completely normal. Let $A$ and $B$ be any two [separated sets](@entry_id:152848) in $X$. This means $\overline{A} \cap B = \emptyset$ and $A \cap \overline{B} = \emptyset$.
Let's consider the subspace $Y = X \setminus (\overline{A} \cap \overline{B})$. Since $\overline{A}$ and $\overline{B}$ are closed in $X$, their intersection is closed, and thus $Y$ is an open subspace of $X$.
Let $A' = A$ and $B' = B$. Both are subsets of $Y$. Let's examine their [closures](@entry_id:747387) *in the subspace Y*.
The closure of $A'$ in $Y$ is $\overline{A'}^Y = \overline{A}^X \cap Y = \overline{A}^X \cap (X \setminus (\overline{A}^X \cap \overline{B}^X)) = \overline{A}^X \setminus \overline{B}^X$.
Similarly, the closure of $B'$ in $Y$ is $\overline{B'}^Y = \overline{B}^X \setminus \overline{A}^X$.
These two sets, $\overline{A'}^Y$ and $\overline{B'}^Y$, are disjoint. They are also closed in $Y$ by definition of subspace closure.
Since $X$ is hereditarily normal, the subspace $Y$ is normal. Because $\overline{A'}^Y$ and $\overline{B'}^Y$ are disjoint closed sets in $Y$, there exist disjoint open sets $U_Y, V_Y$ in $Y$ such that $\overline{A'}^Y \subseteq U_Y$ and $\overline{B'}^Y \subseteq V_Y$.
Since $Y$ is open in $X$, any set open in $Y$ is also open in $X$. Thus, $U_Y$ and $V_Y$ are [disjoint open sets](@entry_id:150704) in $X$.
We have $A = A' \subseteq \overline{A'}^Y \subseteq U_Y$ and $B = B' \subseteq \overline{B'}^Y \subseteq V_Y$. We have found our desired [disjoint open sets](@entry_id:150704) in $X$ that separate $A$ and $B$. Therefore, $X$ is completely normal. $\square$

This theorem provides two powerful perspectives on the same property. It also directly implies that **complete normality is a [hereditary property](@entry_id:151340)**. If $Y$ is a subspace of a completely normal (and thus hereditarily normal) space $X$, then any subspace of $Y$ is also a subspace of $X$ and is therefore normal. This makes $Y$ hereditarily normal, which in turn means $Y$ is completely normal. [@problem_id:1539921]

### Properties and Characterizations

Complete normality is a strong condition, and spaces that possess it have a rich structure. If we add the $T_1$ axiom (that singletons are closed), a [completely normal space](@entry_id:153577) is called a **$T_5$ space**.

#### The Hierarchy of Separation

The $T_5$ property fits neatly at the top of the main chain of [separation axioms](@entry_id:154482). We have the following series of implications:
$$
T_5 \implies T_4 \implies T_3 \implies T_2 \implies T_1
$$
-   **$T_5 \implies T_4$ (Completely Normal $\implies$ Normal):** If a space is completely normal and $T_1$, we can show it is normal ($T_4$). Let $A$ and $B$ be two disjoint closed sets. Since they are closed, $\overline{A}=A$ and $\overline{B}=B$. The condition that they are separated, $\overline{A} \cap B = \emptyset$ and $A \cap \overline{B} = \emptyset$, reduces to $A \cap B = \emptyset$, which is true by assumption. So, any two disjoint closed sets are separated. In a [completely normal space](@entry_id:153577), they can be placed in disjoint open neighborhoods. Thus, the space is normal. [@problem_id:1539920]

-   **$T_4 \implies T_3 \implies T_2$:** As established in the study of [normal spaces](@entry_id:154073), a normal $T_1$ space ($T_4$) is always regular and $T_1$ ($T_3$), and a regular $T_1$ space ($T_3$) is always Hausdorff ($T_2$). The proof for $T_4 \implies T_3$ involves taking a [closed set](@entry_id:136446) $F$ and a point $x \notin F$. Since the space is $T_1$, $\{x\}$ is a closed set disjoint from $F$. Normality provides the [disjoint open sets](@entry_id:150704) required for regularity. The proof for $T_3 \implies T_2$ is similar. [@problem_id:1539899] [@problem_id:1539920]

#### Urysohn-Type Characterizations

Just as [normal spaces](@entry_id:154073) are characterized by Urysohn's Lemma, which guarantees the existence of a continuous function separating two disjoint closed sets, completely [normal spaces](@entry_id:154073) admit a more general version for [separated sets](@entry_id:152848).

**Theorem (Urysohn-type Lemma for Separated Sets):** A $T_1$ space $X$ is completely normal if and only if for any two [separated sets](@entry_id:152848) $A$ and $B$, there exists a continuous function $f: X \to [0, 1]$ such that $f(x)=0$ for all $x \in A$ and $f(x)=1$ for all $x \in B$.

This theorem is immensely powerful. For instance, it allows us to prove an even stronger separation property: in a [completely normal space](@entry_id:153577), any two [separated sets](@entry_id:152848) $A$ and $B$ can be contained in open neighborhoods $U$ and $V$ whose **[closures](@entry_id:747387) are also disjoint**. [@problem_id:153889] To see this, we take the continuous function $f$ from the theorem above. The sets $U = f^{-1}([0, 1/3))$ and $V = f^{-1}((2/3, 1])$ are [disjoint open sets](@entry_id:150704) containing $A$ and $B$, respectively. By the properties of continuous functions, their closures are contained within $f^{-1}([0, 1/3])$ and $f^{-1}([2/3, 1])$, which are disjoint. Thus, $\overline{U} \cap \overline{V} = \emptyset$.

This functional separation can be creatively applied. Suppose we have three pairwise [separated sets](@entry_id:152848), $A_1, A_2, A_3$, in a completely normal $T_1$ space $X$. Can we find a continuous function that assigns them to distinct values, say $0, 1/2, 1$? [@problem_id:1539902]

The answer is yes. The key is to note that if $A_i$ and $A_j$ are separated for $i \neq j$, then the set $A_1$ is separated from the union $A_2 \cup A_3$. Likewise, $A_3$ is separated from $A_1 \cup A_2$.
Using the Urysohn-type lemma, we can construct two continuous functions:
1.  A function $f_1: X \to [0, 1]$ such that $f_1(A_1) = \{0\}$ and $f_1(A_2 \cup A_3) = \{1\}$.
2.  A function $f_3: X \to [0, 1]$ such that $f_3(A_1 \cup A_2) = \{0\}$ and $f_3(A_3) = \{1\}$.

Now, we can combine these to define a new continuous function $h: X \to [0, 1]$ by $h(x) = \frac{1}{2}(f_1(x) + f_3(x))$. Let's check its values on our sets:
-   For $x \in A_1$, $h(x) = \frac{1}{2}(0 + 0) = 0$.
-   For $x \in A_2$, $h(x) = \frac{1}{2}(1 + 0) = 1/2$.
-   For $x \in A_3$, $h(x) = \frac{1}{2}(1 + 1) = 1$.

We have successfully constructed the desired function. This construction also reveals a deep connection to the property of [connectedness](@entry_id:142066). If $X$ were a [connected space](@entry_id:153144), could it be that $X = A_1 \cup A_2 \cup A_3$? The existence of our function $h$ says no. If $X$ were this union, then the image $h(X)$ would be the set $\{0, 1/2, 1\}$. But this set is disconnected, while the continuous image of a [connected space](@entry_id:153144) must be connected. This is a contradiction. Therefore, if $X$ is connected, the remainder set $X \setminus (A_1 \cup A_2 \cup A_3)$ must be non-empty. [@problem_id:1539902]

In summary, complete normality represents a significant strengthening of the normality condition. Its equivalence with hereditary normality and its powerful functional separation properties make it a natural and robust concept in the classification of [topological spaces](@entry_id:155056).