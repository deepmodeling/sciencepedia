## Introduction
In the [representation theory of finite groups](@entry_id:143275), constructing the complete character table of a group $G$ is a central goal, yet it can be a complex and challenging task. A powerful strategy to simplify this problem is to leverage the group's internal structure, particularly its [normal subgroups](@entry_id:147397) and corresponding [quotient groups](@entry_id:145113). This article addresses this by focusing on a fundamental technique known as **lifting** or **inflation**, which allows for the construction of characters of $G$ from the simpler characters of a [quotient group](@entry_id:142790) $G/N$. By understanding this method, we can systematically populate parts of a group's character table and gain deeper insight into its representation structure.

This article will guide you through this elegant process in three parts. First, the **Principles and Mechanisms** chapter will lay the theoretical groundwork, defining the lifting mechanism, exploring the crucial properties of [lifted characters](@entry_id:137777), and examining their algebraic structure within the character ring. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the practical power of lifting, showing how it is used to find linear characters, construct [character tables](@entry_id:146676) for important groups like $S_n$ and $D_n$, and how it relates to other key concepts like [permutation representations](@entry_id:142960) and [character induction](@entry_id:140107). Finally, the **Hands-On Practices** section will provide targeted exercises to reinforce these concepts and develop your computational skills.

## Principles and Mechanisms

In the study of [group representations](@entry_id:145425), a central task is to construct and classify the [irreducible characters](@entry_id:145398) of a given group $G$. While this can be a formidable challenge for large and complex groups, powerful techniques exist that leverage the group's structure. One such technique involves building characters of $G$ from the characters of a simpler, smaller group: one of its quotients. This process, formally known as **inflation** or, more colloquially, **lifting**, allows us to understand a portion of the character table of $G$ by analyzing the full [character table](@entry_id:145187) of a quotient group $G/N$. This chapter explores the principles and mechanisms governing this elegant and useful method.

### The Lifting Mechanism: From Quotient to Group

The fundamental idea behind lifting is to use the natural structural relationship between a group $G$ and its quotient group $G/N$. Let $G$ be a group and $N$ be a normal subgroup of $G$. The **canonical projection** (or canonical [surjective homomorphism](@entry_id:150152)) is the map $\pi: G \to G/N$ defined by $\pi(g) = gN$, which sends each element of $G$ to the [coset](@entry_id:149651) it belongs to.

Now, suppose we have a representation of the quotient group, $\rho: G/N \to \text{GL}(V)$ for some vector space $V$. We can define a new map, $\tilde{\rho}: G \to \text{GL}(V)$, by simply composing $\rho$ with the projection $\pi$.

**Definition:** The **lifted representation** $\tilde{\rho}$ of $\rho$ to $G$ is defined as the composition $\tilde{\rho} = \rho \circ \pi$. For any $g \in G$, its action is given by:
$$ \tilde{\rho}(g) = \rho(\pi(g)) = \rho(gN) $$
Since both $\pi$ and $\rho$ are homomorphisms, their composition $\tilde{\rho}$ is also a homomorphism, and thus defines a valid representation of $G$.

The character of this new representation, $\tilde{\chi}_{\rho}$, is called the **[lifted character](@entry_id:139173)**. Its value for any element $g \in G$ is the trace of the corresponding linear transformation:
$$ \tilde{\chi}_{\rho}(g) = \text{tr}(\tilde{\rho}(g)) = \text{tr}(\rho(gN)) = \chi_{\rho}(gN) $$
More generally, for any character $\chi$ of $G/N$ (which may or may not be irreducible), we define its **lift** (or **inflation**) to $G$, denoted $\tilde{\chi}$, by the rule:
$$ \tilde{\chi}(g) = \chi(gN) \quad \text{for all } g \in G $$
This construction effectively "pulls back" a character from the [quotient group](@entry_id:142790) $G/N$ to create a character on the parent group $G$ [@problem_id:1628425].

To see this process in action, consider the [dihedral group](@entry_id:143875) of order 8, $G = D_8$, representing the symmetries of a square. Let its generators be $r$ (rotation by $\frac{\pi}{2}$) and $s$ (a reflection). The center of this group is $N = Z(G) = \{e, r^2\}$, which is a normal subgroup. The [quotient group](@entry_id:142790) $H = G/N$ has order $\frac{|G|}{|N|} = \frac{8}{2} = 4$ and is isomorphic to the Klein four-group. Let's denote the cosets that generate $H$ by $R = [r] = rN$ and $S = [s] = sN$. Suppose we are given a one-dimensional character $\chi$ of $H$ defined by its values on these generators: $\chi(R) = 1$ and $\chi(S) = -1$.

To find the values of the [lifted character](@entry_id:139173) $\tilde{\chi}$ on $G$, we apply the definition $\tilde{\chi}(g) = \chi(gN)$. Since characters are constant on [conjugacy classes](@entry_id:143916), we only need to evaluate $\tilde{\chi}$ on one representative from each class of $D_8$.
The five [conjugacy classes](@entry_id:143916) of $D_8$ are $C_1 = \{e\}$, $C_2 = \{r^2\}$, $C_3 = \{r, r^{-1}\}$, $C_4 = \{s, sr^2\}$, and $C_5 = \{sr, sr^3\}$.

*   For $C_1$: $\tilde{\chi}(e) = \chi(eN) = \chi(E) = 1$, where $E$ is the identity in $H$.
*   For $C_2$: The element $r^2$ is in $N$, so $r^2N = N = E$. Thus, $\tilde{\chi}(r^2) = \chi(E) = 1$.
*   For $C_3$: $\tilde{\chi}(r) = \chi(rN) = \chi(R) = 1$.
*   For $C_4$: $\tilde{\chi}(s) = \chi(sN) = \chi(S) = -1$.
*   For $C_5$: $\tilde{\chi}(sr) = \chi(srN) = \chi((sN)(rN)) = \chi(SR) = \chi(S)\chi(R) = (-1)(1) = -1$.

The values of the [lifted character](@entry_id:139173) $\tilde{\chi}$ on the five conjugacy classes are therefore $(1, 1, 1, -1, -1)$ [@problem_id:1628450]. This calculation demonstrates how a simple character of a small [quotient group](@entry_id:142790) can generate a more complex-looking character of the larger group.

### Fundamental Properties of Lifted Characters

Lifted characters possess several crucial and easily identifiable properties that follow directly from their definition. These properties are key to both using and recognizing them.

#### Behavior on the Normal Subgroup

The most distinctive feature of a [lifted character](@entry_id:139173) is its behavior on the elements of the normal subgroup $N$ from which it was lifted. For any element $n \in N$, the coset it belongs to is $nN = N$. In the quotient group $G/N$, the [coset](@entry_id:149651) $N$ is the identity element, $e_{G/N}$.

Therefore, for any [lifted character](@entry_id:139173) $\tilde{\chi}$ and any $n \in N$:
$$ \tilde{\chi}(n) = \chi(nN) = \chi(N) = \chi(e_{G/N}) $$
The value of a character at the identity element is its degree. Thus, $\chi(e_{G/N}) = \deg(\chi)$. Furthermore, the degree of the [lifted character](@entry_id:139173) $\tilde{\chi}$ is:
$$ \deg(\tilde{\chi}) = \tilde{\chi}(e_G) = \chi(e_G N) = \chi(N) = \chi(e_{G/N}) $$
Combining these facts, we arrive at a cornerstone property: **for any element $n$ in the normal subgroup $N$, the value of the [lifted character](@entry_id:139173) $\tilde{\chi}(n)$ is equal to the degree of $\tilde{\chi}$** [@problem_id:1628478].
$$ \tilde{\chi}(n) = \tilde{\chi}(e_G) = \deg(\tilde{\chi}) \quad \text{for all } n \in N $$

#### Degree Preservation

As we saw above, the degree of a [lifted character](@entry_id:139173) $\tilde{\chi}$ is equal to the degree of the original character $\chi$ on the [quotient group](@entry_id:142790).
$$ \deg(\tilde{\chi}) = \deg(\chi) $$
This property is straightforward but essential. For instance, consider the [regular representation](@entry_id:137028) of a quotient group $H = G/N$. The degree of its character, $\chi_{\text{reg}}$, is equal to the order of the group, $|H|$. If we lift this character to $G$, the resulting character $\tilde{\chi}_{\text{reg}}$ will have degree $|H|$. For example, for $G=S_4$ and its normal subgroup $N$ (the Klein four-group), the quotient $H = G/N$ is isomorphic to $S_3$, so $|H|=6$. The character of $G$ obtained by lifting the regular character of $H$ will have degree 6 [@problem_id:1628426].

#### The Kernel and Faithfulness

The property that $\tilde{\chi}(n) = \deg(\tilde{\chi})$ for all $n \in N$ has a profound consequence for the underlying representation. Recall that the [kernel of a character](@entry_id:146159) $\chi$ is defined as $\ker(\chi) = \{g \in G \mid \chi(g) = \deg(\chi)\}$. From our previous result, it is immediately clear that:
$$ N \subseteq \ker(\tilde{\chi}) $$
The kernel of the corresponding representation $\tilde{\rho}$ is $\ker(\tilde{\rho}) = \{g \in G \mid \tilde{\rho}(g) = I\}$, where $I$ is the identity matrix. Since $\chi(g) = \deg(\chi)$ if and only if $\rho(g)=I$ for [irreducible representations](@entry_id:138184), this inclusion holds for the representation's kernel as well: $N \subseteq \ker(\tilde{\rho})$.

A representation is called **faithful** if its kernel is the [trivial subgroup](@entry_id:141709) $\{e\}$. Since the kernel of any lifted representation $\tilde{\rho}$ contains the entire subgroup $N$, it follows that if $N$ is non-trivial ($N \neq \{e\}$), then $\tilde{\rho}$ can **never** be faithful [@problem_id:1628467].

We can state the structure of the kernel even more precisely. Since $\tilde{\chi} = \chi \circ \pi$, the kernel of $\tilde{\chi}$ is the [preimage](@entry_id:150899) of the kernel of $\chi$ under the projection map $\pi$:
$$ \ker(\tilde{\chi}) = \pi^{-1}(\ker(\chi)) $$
The **Correspondence Theorem** for groups tells us that there is a one-to-one correspondence between subgroups of $G/N$ and subgroups of $G$ that contain $N$. The kernel of $\chi$, being a [normal subgroup](@entry_id:144438) of $G/N$, must correspond to a unique normal subgroup $K$ of $G$ such that $N \subseteq K$ and $\ker(\chi) = K/N$. The [preimage](@entry_id:150899) $\pi^{-1}(K/N)$ is precisely this subgroup $K$. Therefore, the kernel of the [lifted character](@entry_id:139173) $\tilde{\chi}$ is exactly the subgroup $K$ in $G$ that corresponds to the kernel of $\chi$ in $G/N$ [@problem_id:1628449].

### Identifying Lifted Characters

We have established a clear path for constructing a character $\tilde{\chi}$ on $G$ from a character $\chi$ on $G/N$. This raises a natural question: given the full character table of a group $G$, how can we determine which of its characters are lifts from a particular quotient $G/N$?

The key lies in the property we identified earlier. A character $\psi$ of $G$ is a lift from $G/N$ if and only if it is constant on the cosets of $N$. This is equivalent to the condition that $N$ is contained in the kernel of $\psi$, i.e., $\psi(n) = \psi(e_G)$ for all $n \in N$.

This provides a direct and practical test. To check if an [irreducible character](@entry_id:145297) $\psi$ of $G$ is a lift from $G/N$:
1. Identify the conjugacy classes of $G$ that are contained entirely within $N$.
2. For each such conjugacy class $C_k \subseteq N$, check if $\psi(C_k) = \psi(C_1)$, where $C_1 = \{e_G\}$. If this holds for all classes within $N$, the character $\psi$ is a lift from $G/N$.

Let's apply this to an example. Consider the [dihedral group](@entry_id:143875) $D_6$ of order 12, with the [normal subgroup](@entry_id:144438) $N = \langle r^3 \rangle = \{1, r^3\}$. In $D_6$, the [identity element](@entry_id:139321) $1$ forms the conjugacy class $C_1$, and $r^3$ forms its own class, $C_2$. To identify characters lifted from $G/N$, we must find those characters $\psi$ for which $\psi(r^3) = \psi(1)$. Looking at the [character table](@entry_id:145187), this means we select the rows where the entry in the column for $C_2$ is the same as the entry in the column for $C_1$.

For instance, given a partial character table for $D_6$ [@problem_id:1628472]:
$$
\begin{array}{|c|c|c|c|}
\hline
\text{Character} & C_1=\{1\} & C_2=\{r^3\} & \dots \\
\hline
\psi_A & 1 & 1 & \dots \\
\psi_B & 1 & 1 & \dots \\
\psi_C & 2 & 2 & \dots \\
\psi_D & 2 & -2 & \dots \\
\hline
\end{array}
$$
We can immediately see that $\psi_A$, $\psi_B$, and $\psi_C$ satisfy the condition $\psi(C_1) = \psi(C_2)$, as their values are $(1,1)$, $(1,1)$, and $(2,2)$ respectively. In contrast, $\psi_D$ fails the test since $2 \neq -2$. Thus, $\psi_A, \psi_B, \psi_C$ are characters lifted from $G/N$, while $\psi_D$ is not. These [lifted characters](@entry_id:137777) essentially form the [character table](@entry_id:145187) of the [quotient group](@entry_id:142790) $G/N \cong D_3$.

### Algebraic and Analytic Structure

The process of lifting not only provides a method for constructing characters but also reveals a deep structural relationship between the [character theory](@entry_id:144021) of a group and its quotients. This relationship is elegantly expressed through the [inner product of characters](@entry_id:137615) and the algebraic structure of the character ring.

#### Isometry of the Inner Product

The standard inner product for characters (or any class functions) of a [finite group](@entry_id:151756) $K$ is given by:
$$ \langle \psi_a, \psi_b \rangle_K = \frac{1}{|K|} \sum_{k \in K} \psi_a(k) \overline{\psi_b(k)} $$
A remarkable property of lifting is that it preserves this inner product. Let $\chi_1$ and $\chi_2$ be two class functions on $H=G/N$, and let $\tilde{\chi}_1$ and $\tilde{\chi}_2$ be their respective lifts to $G$. The inner product of the lifted functions on $G$ is:
$$ \langle \tilde{\chi}_1, \tilde{\chi}_2 \rangle_G = \frac{1}{|G|} \sum_{g \in G} \tilde{\chi}_1(g) \overline{\tilde{\chi}_2(g)} = \frac{1}{|G|} \sum_{g \in G} \chi_1(gN) \overline{\chi_2(gN)} $$
Since every [coset](@entry_id:149651) $c \in H$ is of the form $gN$ and contains exactly $|N|$ elements of $G$, we can regroup the sum over the [cosets](@entry_id:147145):
$$ \langle \tilde{\chi}_1, \tilde{\chi}_2 \rangle_G = \frac{1}{|G|} \sum_{c \in H} |N| \cdot \chi_1(c) \overline{\chi_2(c)} = \frac{|N|}{|G|} \sum_{c \in H} \chi_1(c) \overline{\chi_2(c)} $$
Using Lagrange's theorem, $|G|/|N| = |H|$, we arrive at the final result:
$$ \langle \tilde{\chi}_1, \tilde{\chi}_2 \rangle_G = \frac{1}{|H|} \sum_{c \in H} \chi_1(c) \overline{\chi_2(c)} = \langle \chi_1, \chi_2 \rangle_H $$
This shows that lifting is an **[isometry](@entry_id:150881)**; it preserves lengths and angles in the space of class functions [@problem_id:1628477]. An immediate and powerful corollary is that if $\chi$ is an [irreducible character](@entry_id:145297) of $G/N$, its norm is $\langle \chi, \chi \rangle_{G/N} = 1$. Consequently, the norm of its lift is $\langle \tilde{\chi}, \tilde{\chi} \rangle_G = 1$, which proves that **the lift of an [irreducible character](@entry_id:145297) is an [irreducible character](@entry_id:145297)**.

#### The Subring of Lifted Characters

The set of characters of $G$ lifted from $G/N$ has a rich algebraic structure. If $\tilde{\chi}_1$ and $\tilde{\chi}_2$ are lifts of $\chi_1$ and $\chi_2$ from $G/N$, their sum $\tilde{\chi}_1 + \tilde{\chi}_2$ is a lift of $\chi_1 + \chi_2$. More interestingly, consider their pointwise product $(\tilde{\chi}_1 \tilde{\chi}_2)(g) = \tilde{\chi}_1(g)\tilde{\chi}_2(g)$.
$$ (\tilde{\chi}_1 \tilde{\chi}_2)(g) = \chi_1(gN) \chi_2(gN) = (\chi_1 \chi_2)(gN) $$
This shows that the product $\tilde{\chi}_1 \tilde{\chi}_2$ is precisely the lift of the product character $\chi_1 \chi_2$ from $G/N$ [@problem_id:1628421]. This means the set of characters of $G$ lifted from $G/N$ is closed under both addition and multiplication.

The set of all integer [linear combinations](@entry_id:154743) of irreducible characters of $G$, known as **virtual characters**, forms a ring called the **character ring**, $R(G)$. Let $L(G,N)$ be the subset of $R(G)$ consisting of virtual characters that are linear combinations of only those [irreducible characters](@entry_id:145398) lifted from $G/N$. Our previous observation implies that $L(G,N)$ is a **subring** of $R(G)$.

This raises a natural algebraic question: is $L(G,N)$ also an **ideal** of $R(G)$? An ideal $I$ of a ring $R$ must satisfy the property that for any $i \in I$ and any $r \in R$, the product $ri$ is also in $I$. In our context, this would mean that the product of a [lifted character](@entry_id:139173) (from $L(G,N)$) with *any* character of $G$ (from $R(G)$) must also be a [lifted character](@entry_id:139173).

This is generally not true. However, let's consider when it might be. The trivial character $1_G$ (with value 1 for all $g \in G$) has kernel $G$, so it always contains $N$. Therefore, $1_G \in L(G,N)$. If $L(G,N)$ were an ideal, then for any character $\psi \in R(G)$, the product $\psi \cdot 1_G = \psi$ would have to be in $L(G,N)$. This would force $L(G,N) = R(G)$, meaning *all* irreducible characters of $G$ are lifted from $G/N$. This requires that $N \subseteq \ker(\chi)$ for every [irreducible character](@entry_id:145297) $\chi$ of $G$. The intersection of the kernels of all [irreducible characters](@entry_id:145398) of a group is known to be the [trivial subgroup](@entry_id:141709), $\{e\}$. Therefore, we must have $N \subseteq \{e\}$, which implies $N=\{e\}$.

Conversely, if $N=\{e\}$, then $G/N \cong G$, and every character of $G$ is trivially a lift from $G/N$. In this case, $L(G,N) = R(G)$, which is indeed an ideal of itself. Thus, the subring of [lifted characters](@entry_id:137777) $L(G,N)$ is an ideal of the character ring $R(G)$ if and only if $N$ is the [trivial subgroup](@entry_id:141709) [@problem_id:1628434]. This result neatly places the set of [lifted characters](@entry_id:137777) within the broader algebraic framework of [character theory](@entry_id:144021), highlighting its status as a special, but not typically ideal, subring.