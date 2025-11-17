## Introduction
In the study of abstract algebra, understanding the internal structure of a group is a central objective. While subgroups offer a view into smaller, self-contained algebraic systems within a larger group, a deeper analysis requires tools to understand how a subgroup relates to and organizes the entire group. This leads to a fundamental question: can we use a subgroup to systematically break down its parent group into simpler, more uniform components?

This article explores the properties of [cosets](@entry_id:147145), the mathematical objects that provide a definitive answer to this question. Cosets allow us to partition a group into a collection of disjoint subsets, each mirroring the size and structure of the originating subgroup. By studying these partitions, we unlock profound insights into the nature of groups. This article will guide you through the core principles and applications of [cosets](@entry_id:147145) across three chapters. The "Principles and Mechanisms" chapter will formally define [cosets](@entry_id:147145) as [equivalence classes](@entry_id:156032), establish their key properties, and use them to prove Lagrange's Theorem, a foundational result in [finite group theory](@entry_id:146601). The "Applications and Interdisciplinary Connections" chapter will demonstrate the power of cosets in classifying group elements, constructing new [algebraic structures](@entry_id:139459) like [quotient groups](@entry_id:145113), and solving problems in fields from linear algebra to information theory. Finally, the "Hands-On Practices" section will provide opportunities to apply these concepts and solidify your understanding.

## Principles and Mechanisms

Having established the foundational concept of a subgroup in the preceding chapter, we now explore one of its most profound consequences: the decomposition of a group into smaller, uniformly sized pieces. This decomposition, known as a partition into cosets, provides a powerful lens through which to analyze the internal structure of a group. It culminates in one of the most fundamental results in [finite group theory](@entry_id:146601), Lagrange's Theorem, and lays the groundwork for understanding [quotient groups](@entry_id:145113) and homomorphisms.

### Cosets as Equivalence Classes

The central idea is to use a subgroup $H$ of a group $G$ to define a relationship between the elements of $G$. We can ask: when are two elements $a$ and $b$ in $G$ "related" with respect to $H$? A fruitful approach is to consider whether one can be reached from the other by an operation involving an element of $H$. This idea can be formalized through the concept of an equivalence relation.

An **[equivalence relation](@entry_id:144135)**, denoted by $\sim$, is a [binary relation](@entry_id:260596) on a set that is reflexive ($a \sim a$), symmetric (if $a \sim b$, then $b \sim a$), and transitive (if $a \sim b$ and $b \sim c$, then $a \sim c$). Such a relation partitions the set into disjoint subsets called [equivalence classes](@entry_id:156032). Let's examine how a subgroup $H$ can induce such a relation on its parent group $G$.

Consider the relation defined as: $a \sim b$ if and only if $a^{-1}b \in H$. Let us verify if this constitutes a valid equivalence relation [@problem_id:1815717].
1.  **Reflexivity**: For any $a \in G$, we must check if $a \sim a$. This requires $a^{-1}a \in H$. Since $a^{-1}a = e$, the identity element, and $H$ is a subgroup, it must contain the identity. Thus, $e \in H$, and the relation is reflexive.
2.  **Symmetry**: Suppose $a \sim b$, which means $a^{-1}b \in H$. Since $H$ is a subgroup, it is closed under taking inverses. Therefore, $(a^{-1}b)^{-1}$ must also be in $H$. The inverse is $(b^{-1})(a^{-1})^{-1} = b^{-1}a$. The condition $b^{-1}a \in H$ means that $b \sim a$. Thus, the relation is symmetric.
3.  **Transitivity**: Suppose $a \sim b$ and $b \sim c$. This means $a^{-1}b \in H$ and $b^{-1}c \in H$. Since $H$ is a subgroup, it is closed under the group operation. Therefore, the product $(a^{-1}b)(b^{-1}c)$ must be in $H$. This product simplifies to $a^{-1}(bb^{-1})c = a^{-1}ec = a^{-1}c$. The condition $a^{-1}c \in H$ means that $a \sim c$. Thus, the relation is transitive.

Since the relation is reflexive, symmetric, and transitive, it is indeed an equivalence relation. The equivalence class of an element $g \in G$ is the set of all elements $x \in G$ such that $g \sim x$. Let's characterize this set:
$$[g] = \{x \in G \mid g \sim x\} = \{x \in G \mid g^{-1}x \in H\}$$
If $g^{-1}x = h$ for some $h \in H$, then by multiplying on the left by $g$, we get $x = gh$. This means that the equivalence class of $g$ is precisely the set $\{gh \mid h \in H\}$. This set is known as the **left [coset](@entry_id:149651)** of $H$ with respect to $g$, denoted **$gH$**.

Similarly, the relation $a \sim b$ if and only if $ab^{-1} \in H$ also defines an equivalence relation, whose equivalence classes are the **[right cosets](@entry_id:136335)** $Hg = \{hg \mid h \in H\}$ [@problem_id:1815717]. For the remainder of this chapter, we will primarily focus on left cosets, but analogous properties hold for [right cosets](@entry_id:136335).

### Fundamental Properties of Cosets

The fact that [cosets](@entry_id:147145) are [equivalence classes](@entry_id:156032) endows them with several crucial properties that form the bedrock of their utility.

#### Condition for Coset Equality

A direct consequence of their origin as [equivalence classes](@entry_id:156032) is a simple criterion for determining when two cosets are identical. The [cosets](@entry_id:147145) $g_1H$ and $g_2H$ are the equivalence classes of $g_1$ and $g_2$, respectively. From the theory of [equivalence relations](@entry_id:138275), we know that two [equivalence classes](@entry_id:156032) are identical if and only if their representative elements are related. Therefore:
$$g_1H = g_2H \iff g_1 \sim g_2 \iff g_1^{-1}g_2 \in H$$
This single condition is remarkably powerful. For instance, consider the [symmetric group](@entry_id:142255) $G=S_4$ and the subgroup $H$ of [permutations](@entry_id:147130) that fix the element $4$, i.e., $H = \{ \pi \in S_4 \mid \pi(4) = 4 \}$. Let's determine which permutations $\tau_i$ generate the same left coset as $\sigma = (14)$. According to our criterion, $\tau_i H = \sigma H$ if and only if $\sigma^{-1}\tau_i \in H$. By the definition of $H$, this is equivalent to the permutation $\sigma^{-1}\tau_i$ fixing the element $4$, which means $(\sigma^{-1}\tau_i)(4) = 4$. Applying $\sigma$ to both sides, and noting that $\sigma = \sigma^{-1}$ since it is a transposition, we get $\tau_i(4) = \sigma(4)$. Since $\sigma = (14)$, it maps $4$ to $1$. Thus, the condition simplifies to $\tau_i(4) = 1$. This provides a simple check: for any element $\tau \in S_4$, its coset $\tau H$ is identical to $\sigma H$ if and only if $\tau$ maps $4$ to $1$ [@problem_id:1636517].

#### The Partition of a Group

Equivalence classes are defined by two signature properties: every element of the set belongs to exactly one class, and the union of all classes reconstitutes the entire set. Applied to [cosets](@entry_id:147145), this means:

1.  For a subgroup $H \subseteq G$, any two left cosets $aH$ and $bH$ are either **identical or disjoint**. That is, $(aH) \cap (bH) = \emptyset$ or $aH = bH$. They can never partially overlap. This follows directly from the transitivity of the equivalence relation. If they share even one element, say $x$, then $x \in aH$ implies $xH=aH$ and $x \in bH$ implies $xH=bH$. Thus, $aH=bH$. [@problem_id:1815735].

2.  The union of all distinct left cosets of $H$ is the entire group $G$. This is because every element $g \in G$ belongs to at least one [coset](@entry_id:149651)—namely, its own. Since the identity $e$ is in $H$, we have $g = ge \in gH$. Therefore, $G = \bigcup_{g \in G} gH$ [@problem_id:1815709].

Together, these properties state that the set of all left cosets of $H$ in $G$, denoted $\{gH \mid g \in G\}$, forms a **partition** of the group $G$.

#### Cardinality of Cosets

A striking feature of this partition is its uniformity. Every [coset](@entry_id:149651) of a subgroup $H$ has exactly the same number of elements as $H$ itself. This can be proven by constructing an explicit [one-to-one correspondence](@entry_id:143935), or **bijection**, between $H$ and any of its [cosets](@entry_id:147145) $gH$.

Consider the map $\phi: H \to gH$ defined by $\phi(h) = gh$. This map is surjective by definition of $gH$. It is also injective because if $\phi(h_1) = \phi(h_2)$, then $gh_1 = gh_2$, and by left cancellation, $h_1 = h_2$. Thus, $\phi$ is a bijection.

Alternatively, and more useful for certain proofs, we can define a map from the coset back to the subgroup. Consider the function $\phi: gH \to H$ given by $\phi(x) = g^{-1}x$. For any element $x \in gH$, we can write $x = gh$ for some unique $h \in H$. Applying $\phi$, we get $\phi(x) = g^{-1}(gh) = h$, which is indeed in $H$. This map is a bijection [@problem_id:1636513]:
*   **Injectivity**: If $\phi(x_1) = \phi(x_2)$, then $g^{-1}x_1 = g^{-1}x_2$. Left-multiplying by $g$ gives $x_1 = x_2$.
*   **Surjectivity**: For any $h \in H$, we need to find an element $x \in gH$ such that $\phi(x) = h$. The element $x = gh$ is in $gH$, and $\phi(gh) = g^{-1}(gh) = h$.

Thus, there is a one-to-one correspondence between the elements of $H$ and the elements of any of its left cosets. This means $|gH| = |H|$ for all $g \in G$.

For example, consider the infinite group $G = (\mathbb{Z}, +)$ and its subgroup of even integers $H = 2\mathbb{Z}$. The [coset](@entry_id:149651) $1+H$ is the set of all odd integers. The function $f: H \to 1+H$ defined by $f(x) = x+1$ is a bijection. An even number $x=2k$ is mapped to $2k+1$, which is an odd number. This function is clearly injective and surjective, demonstrating the [one-to-one correspondence](@entry_id:143935) between the set of even integers and the set of odd integers [@problem_id:1636541].

### Lagrange's Theorem

The culmination of these properties for finite groups is **Lagrange's Theorem**, a cornerstone of group theory. Let $G$ be a finite group and $H$ be a subgroup of $G$. We have established that:
1.  $G$ is partitioned into a collection of disjoint left cosets of $H$.
2.  Each of these [cosets](@entry_id:147145) has the same size, $|H|$.

Let the number of distinct left cosets be denoted by $[G:H]$, called the **index** of $H$ in $G$. Since these $[G:H]$ [disjoint sets](@entry_id:154341), each of size $|H|$, make up the entirety of $G$, a simple counting argument gives:
$$|G| = [G:H] \cdot |H|$$

This elegant formula is Lagrange's Theorem. It places a strong constraint on the possible structure of a finite group. A direct corollary is that the order of any subgroup $H$ must divide the order of the group $G$. Likewise, the order of any element $g \in G$ (which is the order of the [cyclic subgroup](@entry_id:138079) $\langle g \rangle$) must also divide the order of $G$.

The index $[G:H]$ is simply the number of distinct left [cosets](@entry_id:147145). For a [finite group](@entry_id:151756), it can be computed directly as $[G:H] = \frac{|G|}{|H|}$. For example, in the group $G = \mathbb{Z}_{12} \times \mathbb{Z}_{18}$, the order is $|G| = 12 \times 18 = 216$. For the [cyclic subgroup](@entry_id:138079) $H$ generated by $(3,4)$, we first find the order of this element. The order of $3$ in $\mathbb{Z}_{12}$ is $4$, and the order of $4$ in $\mathbb{Z}_{18}$ is $9$. The order of $(3,4)$ is $\operatorname{lcm}(4,9) = 36$. Therefore, $|H|=36$. The number of distinct left cosets of $H$ in $G$ is $[G:H] = \frac{216}{36} = 6$ [@problem_id:1815694].

The index possesses its own multiplicative properties. If $K \leq H \leq G$ is a chain of subgroups, then $[G:K] = [G:H][H:K]$. This property is invaluable in [structural analysis](@entry_id:153861), as seen in problems involving intersections of subgroups. For instance, if given a group $G$ of order 792 and two subgroups $H$ and $K$ of orders 72 and 99 respectively, with the [side information](@entry_id:271857) that their indices, $[G:H]=11$ and $[G:K]=8$, are [relatively prime](@entry_id:143119), we can determine the order of their intersection. The index $[G:HK]$ must divide both $[G:H]$ and $[G:K]$. Since they are [relatively prime](@entry_id:143119), $[G:HK]=1$, which implies $HK=G$. Using the [product formula](@entry_id:137076) $|HK| = \frac{|H||K|}{|H \cap K|}$, we find $|H \cap K| = \frac{|H||K|}{|G|} = \frac{72 \cdot 99}{792} = 9$ [@problem_id:1636534].

### Normal Subgroups, Homomorphisms, and Quotient Groups

We have focused on left cosets, but everything said so far has a parallel version for [right cosets](@entry_id:136335) $Hg$. A natural question arises: is the left [coset](@entry_id:149651) $gH$ always the same as the right [coset](@entry_id:149651) $Hg$?

The answer is no. Consider the [symmetric group](@entry_id:142255) $S_3$ and its subgroup $H = \{e, (12)\}$. Let's compute the cosets for $g=(13)$.
*   Left [coset](@entry_id:149651): $gH = \{(13)e, (13)(12)\} = \{(13), (123)\}$
*   Right [coset](@entry_id:149651): $Hg = \{e(13), (12)(13)\} = \{(13), (132)\}$
Clearly, $gH \neq Hg$ [@problem_id:1815724]. This observation motivates a crucial definition. A subgroup $H$ of $G$ is called a **[normal subgroup](@entry_id:144438)** if $gH = Hg$ for all $g \in G$. This is equivalent to the condition $gHg^{-1} = H$ for all $g \in G$.

Normal subgroups are intimately connected to group homomorphisms. A **homomorphism** is a map $\phi: G \to K$ between two groups that preserves the group structure, i.e., $\phi(ab) = \phi(a)\phi(b)$. The **kernel** of a homomorphism, $\operatorname{ker}(\phi)$, is the set of elements in $G$ that map to the [identity element](@entry_id:139321) in $K$. The kernel is always a normal subgroup of $G$.

Cosets appear naturally in this context. The set of all elements in $G$ that map to a specific element $k \in K$ is called the **preimage** of $k$, denoted $\phi^{-1}(k)$. If this set is non-empty, let $g$ be any element such that $\phi(g)=k$. Then the entire preimage of $k$ is precisely the left [coset](@entry_id:149651) $g(\operatorname{ker}(\phi))$. To see this, let $x \in \phi^{-1}(k)$. Then $\phi(x)=k=\phi(g)$, which implies $\phi(g)^{-1}\phi(x) = e_K$. Since $\phi$ is a homomorphism, this becomes $\phi(g^{-1}x) = e_K$. This means $g^{-1}x \in \operatorname{ker}(\phi)$, so $x \in g(\operatorname{ker}(\phi))$. This shows that the fibers of a homomorphism are precisely the cosets of its kernel [@problem_id:1636496].

The property of normality is exactly what is needed for the set of [cosets](@entry_id:147145) itself to form a group. We can define a "product" of two left [cosets](@entry_id:147145), $(aH)(bH)$, as the set of all products $\{xy \mid x \in aH, y \in bH\}$. This set product is not, in general, a single [coset](@entry_id:149651). However, if (and only if) $H$ is a [normal subgroup](@entry_id:144438) of $G$, the product of any two left [cosets](@entry_id:147145) is another left coset:
$$(aH)(bH) = a(Hb)H = a(bH)H = (ab)HH = (ab)H$$
This [closure property](@entry_id:136899) allows us to define a [binary operation](@entry_id:143782) on the set of all left cosets of a [normal subgroup](@entry_id:144438) $H$, denoted $G/H$. With the operation $(aH)(bH) = (ab)H$, the set $G/H$ forms a group called the **quotient group** (or [factor group](@entry_id:152975)) of $G$ by $H$ [@problem_id:1815682]. This construction is one of the most powerful tools in abstract algebra, allowing us to build new groups from old ones and to understand the structure of a group in terms of a smaller group and its normal subgroup.