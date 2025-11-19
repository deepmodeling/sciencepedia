## Introduction
In the study of abstract algebra, understanding the intricate structure of a group is a primary objective. While a group's definition is simple, its internal architecture can be complex. A powerful method for dissecting this structure is to examine it through the lens of one of its subgroups. This leads to the concept of a **[coset](@entry_id:149651)**, a construction that partitions an entire group into smaller, more manageable pieces, each a "shifted" version of the subgroup. By understanding [cosets](@entry_id:147145), we can uncover deep properties of the group and establish foundational results, like the celebrated Lagrange's Theorem.

This article will guide you through the theory and application of cosets. In the first chapter, **Principles and Mechanisms**, we will formally define [cosets](@entry_id:147145) as equivalence classes, explore their essential properties, and prove their connection to the size of the group. Following this, the **Applications and Interdisciplinary Connections** chapter will reveal the practical power of [cosets](@entry_id:147145), demonstrating their role in geometry, number theory, and the physical sciences. Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding of these critical algebraic tools.

## Principles and Mechanisms

Having established the fundamental concepts of groups and subgroups, we now explore a powerful construction that allows us to understand the internal structure of a group by using one of its subgroups. This construction, known as a **coset**, partitions the entire group into disjoint subsets, each of which is a "shifted" copy of the subgroup. This partitioning provides profound insights into the group's properties and leads to one of the most fundamental results in [finite group theory](@entry_id:146601), Lagrange's Theorem.

### Cosets as Equivalence Classes

The most rigorous way to understand how a subgroup partitions a group is by defining an [equivalence relation](@entry_id:144135). Given a group $G$ and a subgroup $H$, we can define a relation $\sim$ on the elements of $G$ that connects two elements if they are "equivalent" relative to $H$.

Let $a$ and $b$ be any two elements in a group $G$, and let $H$ be a subgroup of $G$. We define the relation $a \sim b$ if and only if $a^{-1}b \in H$. Let us verify that this is indeed an [equivalence relation](@entry_id:144135). [@problem_id:1785193]

1.  **Reflexivity:** For any element $a \in G$, we must show $a \sim a$. The product $a^{-1}a$ is the [identity element](@entry_id:139321) $e$. Since $H$ is a subgroup, it must contain the identity, so $a^{-1}a = e \in H$. Therefore, $a \sim a$.

2.  **Symmetry:** If $a \sim b$, we must show $b \sim a$. The condition $a \sim b$ means $a^{-1}b \in H$. Because $H$ is a subgroup, it is closed under taking inverses. Thus, the inverse of $a^{-1}b$, which is $(a^{-1}b)^{-1} = b^{-1}(a^{-1})^{-1} = b^{-1}a$, must also be in $H$. The condition $b^{-1}a \in H$ is precisely the definition of $b \sim a$.

3.  **Transitivity:** If $a \sim b$ and $b \sim c$, we must show $a \sim c$. The given conditions mean that $a^{-1}b \in H$ and $b^{-1}c \in H$. Since $H$ is closed under the group operation, the product of these two elements must also be in $H$. So, $(a^{-1}b)(b^{-1}c) = a^{-1}(bb^{-1})c = a^{-1}ec = a^{-1}c \in H$. This is the definition of $a \sim c$.

Having established that $\sim$ is an equivalence relation, we know it partitions the group $G$ into disjoint equivalence classes. What do these classes look like? The [equivalence class](@entry_id:140585) of an element $g \in G$, denoted $[g]$, is the set of all elements $x \in G$ such that $g \sim x$.
$$[g] = \{x \in G \mid g \sim x\} = \{x \in G \mid g^{-1}x \in H\}$$
Let $h = g^{-1}x$. Since $h$ can be any element of $H$, we can write $x = gh$. This means the equivalence class of $g$ is the set of all elements formed by multiplying $g$ on the left by every element of $H$. This leads us to a formal definition.

For a group $G$ and a subgroup $H$, the **left coset** of $H$ with respect to an element $g \in G$ is the set:
$$gH = \{gh \mid h \in H\}$$
Thus, the equivalence classes of the relation $a^{-1}b \in H$ are precisely the left [cosets](@entry_id:147145) of $H$ in $G$.

Similarly, we could have defined a relation $a \approx b$ if and only if $ab^{-1} \in H$. This is also an equivalence relation, and its equivalence classes define the **[right cosets](@entry_id:136335)** of $H$:
$$Hg = \{hg \mid h \in H\}$$

### Core Properties of Cosets

The view of cosets as equivalence classes immediately bestows upon them several [critical properties](@entry_id:260687).

#### Conditions for Coset Equality

A common task is to determine if two elements generate the same coset. For instance, given $g_1, g_2 \in G$, when is $g_1H = g_2H$? Since cosets are [equivalence classes](@entry_id:156032), this equality holds if and only if $g_1$ and $g_2$ are in the same class, i.e., $g_1 \sim g_2$. Unpacking this definition, we arrive at the fundamental criterion:
$$g_1H = g_2H \iff g_2^{-1}g_1 \in H$$
A symmetric argument for [right cosets](@entry_id:136335) shows that $Hg_1 = Hg_2 \iff g_1g_2^{-1} \in H$. [@problem_id:1785200]

This criterion is not just theoretical; it is a practical tool for checking [coset](@entry_id:149651) equality. For example, consider the symmetric group $S_3 = \{e, (12), (13), (23), (123), (132)\}$ and its subgroup $H = \{e, (12)\}$. Let's test if the cosets $(123)H$ and $(13)H$ are equal. We set $g_1 = (123)$ and $g_2 = (13)$. We must check if $g_2^{-1}g_1 \in H$. The inverse of the [transposition](@entry_id:155345) $(13)$ is itself, so we compute $(13)^{-1}(123) = (13)(123)$. This composition yields $(12)$, which is an element of $H$. Therefore, we can conclude that $(123)H = (13)H$. [@problem_id:1785204]

An important corollary is that any element of a coset can serve as its **representative**. If $x \in gH$, then $x$ is of the form $gh_1$ for some $h_1 \in H$. Then $xH = (gh_1)H$. To check if this equals $gH$, we use our criterion: $g^{-1}x = g^{-1}(gh_1) = h_1 \in H$. Since the condition is met, $xH = gH$.

#### The Partition Property: Identical or Disjoint

A direct consequence of cosets being equivalence classes is that any two left cosets (or any two [right cosets](@entry_id:136335)) are either exactly the same set or they have no elements in common (their intersection is empty).
$$ \text{For any } g_1, g_2 \in G, \text{ either } g_1H = g_2H \text{ or } g_1H \cap g_2H = \emptyset $$
This all-or-nothing property is immensely useful. Suppose we need to find the number of distinct elements in the union of two [cosets](@entry_id:147145), $C_1 = g_1H$ and $C_2 = g_2H$. Using the [principle of inclusion-exclusion](@entry_id:276055), $|C_1 \cup C_2| = |C_1| + |C_2| - |C_1 \cap C_2|$. Because the cosets are either identical or disjoint, their intersection $C_1 \cap C_2$ is either $C_1$ (if they are equal) or the [empty set](@entry_id:261946) $\emptyset$ (if they are not).

Consider the group $S_4$ and the subgroup $H$ of [permutations](@entry_id:147130) that fix the number 4, i.e., $H = \{\sigma \in S_4 \mid \sigma(4) = 4\}$. This subgroup is isomorphic to $S_3$ and has $|H| = 3! = 6$ elements. Let's find the size of the union of the [cosets](@entry_id:147145) $C_1 = (13)H$ and $C_2 = (124)H$. We check if they are disjoint by testing if $g_2^{-1}g_1 = (124)^{-1}(13) = (142)(13)$ is in $H$. An element is in $H$ if it fixes 4. Let's apply this permutation to 4: $((142)(13))(4) = (142)((13)(4)) = (142)(4) = 2$. Since $2 \neq 4$, the element $(142)(13)$ is not in $H$. Therefore, the [cosets](@entry_id:147145) $C_1$ and $C_2$ are disjoint, and their intersection is empty. [@problem_id:1785182]

#### Cardinality and Subgroup Properties

Another key property is that all cosets of a subgroup $H$ have the same size as $H$ itself. This can be demonstrated by constructing a [bijection](@entry_id:138092). For any $g \in G$, consider the map $f: H \to gH$ defined by $f(h) = gh$.
-   **Injectivity:** If $f(h_1) = f(h_2)$, then $gh_1 = gh_2$. By left cancellation, $h_1 = h_2$.
-   **Surjectivity:** Any element $x \in gH$ is, by definition, of the form $gh$ for some $h \in H$. Thus, $x = f(h)$, so the map is surjective.
Since a bijection exists between $H$ and $gH$, they must have the same cardinality: $|gH| = |H|$.

Revisiting our example from $S_4$, since $|H|=6$, we know that $|C_1| = |(13)H| = 6$ and $|C_2| = |(124)H| = 6$. As we found they were disjoint, the size of their union is simply $|C_1 \cup C_2| = |C_1| + |C_2| = 6 + 6 = 12$. [@problem_id:1785182]

Now, consider the subgroup $H$ itself. Is it a coset? Yes. It is the [coset](@entry_id:149651) generated by the identity element, $eH = \{eh \mid h \in H\} = H$. It is also the [coset](@entry_id:149651) generated by any of its own elements. This leads to another fundamental equivalence:
$$g \in H \iff gH = H$$
This is a direct result of the subgroup's [closure property](@entry_id:136899). If $g \in H$, then for any $h \in H$, the product $gh$ is also in $H$, so $gH \subseteq H$. And for any $x \in H$, we can write $x = g(g^{-1}x)$. Since $g \in H$, $g^{-1} \in H$, and thus $g^{-1}x \in H$. This means $x \in gH$, so $H \subseteq gH$. Together, $gH = H$. Conversely, if $gH=H$, then since $e \in H$, we must have $ge = g \in gH=H$. [@problem_id:1785170]

This raises a natural question: can a [coset](@entry_id:149651) $gH$ be a subgroup of $G$? For any set to be a subgroup, it must contain the identity element $e$. If $e \in gH$, then $e = gh$ for some $h \in H$, which implies $g = h^{-1}$. This means $g$ must be an element of $H$. If $g \in H$, we have just shown that the [coset](@entry_id:149651) $gH$ is simply $H$ itself. Therefore, the only coset of $H$ that is also a subgroup of $G$ is $H$ itself. For any $g \notin H$, the [coset](@entry_id:149651) $gH$ is not a subgroup. [@problem_id:1785170]

### Left Cosets versus Right Cosets

So far, we have often treated [left and right cosets](@entry_id:136537) in parallel. However, it is crucial to recognize that for a general group, the left [coset](@entry_id:149651) $gH$ and the right [coset](@entry_id:149651) $Hg$ are not necessarily the same set.

Let's examine this in a [non-abelian group](@entry_id:144791). Consider the dihedral group $D_3 = \{e, r, r^2, s, sr, sr^2\}$ with relations $r^3=e, s^2=e, sr=r^2s$. Let $H$ be the subgroup $\{e, s\}$ and let $g=r$.
-   The **left coset** is $gH = rH = \{r \cdot e, r \cdot s\} = \{r, rs\}$.
-   The **right [coset](@entry_id:149651)** is $Hg = Hr = \{e \cdot r, s \cdot r\} = \{r, sr\}$.

Since the group is non-abelian, we know $rs \neq sr$. (In fact, $sr=r^2s$). Therefore, $rH \neq Hr$. The only element they share is $r$. [@problem_id:1785188] A similar divergence occurs in $S_3$. For the subgroup $H=\{e, (12)\}$ and element $g=(23)$, the left [coset](@entry_id:149651) is $gH = \{(23), (23)(12)\} = \{(23), (132)\}$, while the right coset is $Hg = \{(23), (12)(23)\} = \{(23), (123)\}$. Again, the two cosets are distinct. [@problem_id:1785171]

This distinction vanishes in abelian groups. If a group $G$ is abelian, then for any $g \in G$ and $h \in H$, we have $gh = hg$. Consequently, the sets $gH$ and $Hg$ are identical. Subgroups for which $gH = Hg$ for all $g \in G$, even in [non-abelian groups](@entry_id:145211), are called **normal subgroups** and are of central importance in more advanced group theory.

There is also a neat algebraic relationship connecting [left and right cosets](@entry_id:136537) through the inversion operation. The set of inverses of all elements in a left coset $gH$ is denoted $(gH)^{-1}$.
$$(gH)^{-1} = \{(gh)^{-1} \mid h \in H\}$$
Using the identity $(ab)^{-1} = b^{-1}a^{-1}$, we get:
$$(gH)^{-1} = \{h^{-1}g^{-1} \mid h \in H\}$$
Since $H$ is a subgroup, the set of inverses $\{h^{-1} \mid h \in H\}$ is identical to the set $H$. Therefore:
$$(gH)^{-1} = \{h'g^{-1} \mid h' \in H\} = Hg^{-1}$$
The set of inverses of a left coset of $H$ is a right [coset](@entry_id:149651) of $H$. [@problem_id:1785203]

### The Index of a Subgroup and Lagrange's Theorem

We have established that the set of all left cosets of $H$ forms a partition of $G$. The same is true for the set of all [right cosets](@entry_id:136335). The number of distinct left cosets is called the **index** of $H$ in $G$, denoted by $[G:H]$. Although [left and right cosets](@entry_id:136537) may be different sets, it can be proven that the number of distinct left cosets is always equal to the number of distinct [right cosets](@entry_id:136335).

A classic and illustrative example is the [additive group](@entry_id:151801) of integers, $G = \mathbb{Z}$, with the subgroup $H = n\mathbb{Z} = \{..., -2n, -n, 0, n, 2n, ...\}$ for some positive integer $n$. The [cosets](@entry_id:147145) are of the form $a+H$. Two integers $a$ and $b$ are in the same [coset](@entry_id:149651) if their difference is a multiple of $n$, i.e., $a - b \in n\mathbb{Z}$. This is precisely the definition of [congruence modulo](@entry_id:161640) $n$. By the [division algorithm](@entry_id:156013), any integer $a$ can be written as $a = qn + r$ where $0 \le r \lt n$. This means $a - r = qn \in n\mathbb{Z}$, so $a$ is in the coset $r+n\mathbb{Z}$. The distinct cosets are therefore:
$$0+n\mathbb{Z}, \quad 1+n\mathbb{Z}, \quad \dots, \quad (n-1)+n\mathbb{Z}$$
There are exactly $n$ such cosets, so the index $[\mathbb{Z}:n\mathbb{Z}] = n$. In the context of a control system where diagnostic checks run at times that are multiples of 17, the subgroup is $17\mathbb{Z}$. The set of all time steps is partitioned into 17 distinct [equivalence classes](@entry_id:156032), or cosets, corresponding to the possible remainders upon division by 17. [@problem_id:1785177]

For [finite groups](@entry_id:139710), the concept of the index leads directly to a cornerstone result. Since the cosets partition the group $G$, the sum of their sizes must equal the size of $G$. We have $[G:H]$ distinct [cosets](@entry_id:147145), and each has size $|H|$. This gives the elegant relationship known as **Lagrange's Theorem**:
$$|G| = [G:H] \cdot |H|$$
This theorem has profound consequences, including the fact that the order of any subgroup must divide the order of the group. For computational purposes, we can rearrange the formula to find the index if the group and subgroup orders are known:
$$[G:H] = \frac{|G|}{|H|}$$

For example, let's find the number of distinct left [cosets](@entry_id:147145) of the diagonal subgroup $H = \{(\sigma, \sigma) \mid \sigma \in S_3\}$ in the group $G = S_3 \times S_3$. The order of $S_3$ is $3! = 6$. The order of the [direct product](@entry_id:143046) group is $|G| = |S_3| \times |S_3| = 6 \times 6 = 36$. The subgroup $H$ is in [one-to-one correspondence](@entry_id:143935) with the elements of $S_3$, so $|H| = |S_3| = 6$. The number of distinct [cosets](@entry_id:147145) is the index:
$$[G:H] = \frac{|G|}{|H|} = \frac{36}{6} = 6$$
There are exactly 6 distinct left [cosets](@entry_id:147145) of $H$ in $G$. [@problem_id:1785186]

In summary, [cosets](@entry_id:147145) provide a fundamental tool for deconstructing a group's structure. They arise naturally as equivalence classes, partition the group into equal-sized blocks, and provide the conceptual foundation for Lagrange's Theorem, a pillar of [finite group theory](@entry_id:146601).