## Introduction
The study of [group representations](@entry_id:145425) often involves breaking down complex structures into simpler, more manageable components. But what if we could reverse this process? How can we construct [complex representations](@entry_id:144331) of a group from the simpler representations of its subgroups? This fundamental question is answered by the concept of the [induced module](@entry_id:137976), a powerful and ubiquitous tool in [representation theory](@entry_id:137998). It provides a systematic bridge between the [representation theory](@entry_id:137998) of a group and its various substructures, revealing deep connections that are essential for both theoretical understanding and practical application. This article serves as a comprehensive introduction to this vital topic. In the following chapters, you will first learn the core **Principles and Mechanisms**, including the formal construction of the [induced module](@entry_id:137976), the formula for its character, and the celebrated Frobenius Reciprocity theorem. Next, we will explore its diverse **Applications and Interdisciplinary Connections**, demonstrating its role in constructing representations and its impact on fields from number theory to solid-state physics. Finally, you will solidify your understanding through **Hands-On Practices**, applying these concepts to solve concrete problems.

## Principles and Mechanisms

Having established the foundational concepts of [group representations](@entry_id:145425), we now turn to a powerful and ubiquitous construction method: induction. Induction provides a systematic way to build representations of a group $G$ from the representations of its subgroups $H$. This process is not merely a technical device; it is a fundamental tool that reveals deep structural connections between the representation theories of a group and its various substructures. In this chapter, we will define the [induced representation](@entry_id:140832), explore its essential properties through [character theory](@entry_id:144021), and establish the key theorems that govern its behavior.

### The Construction of the Induced Module

Let $G$ be a finite group and $H$ a subgroup of $G$. Suppose we are given a representation of $H$ on a [complex vector space](@entry_id:153448) $W$. Our goal is to "lift" this to a representation of the entire group $G$. The resulting $G$-module is called the **[induced module](@entry_id:137976)** or **[induced representation](@entry_id:140832)**, denoted $\text{Ind}_H^G W$.

Formally, the [induced module](@entry_id:137976) is defined using the language of modules and tensor products. Recall that a [representation of a group](@entry_id:137513) is equivalent to a module over its [group algebra](@entry_id:145139). Thus, $W$ is a left $\mathbb{C}[H]$-module. The [group algebra](@entry_id:145139) $\mathbb{C}[G]$ can be viewed as a left $\mathbb{C}[G]$-module (by left multiplication) and also as a right $\mathbb{C}[H]$-module (by right multiplication). This structure, known as a $(\mathbb{C}[G], \mathbb{C}[H])$-bimodule, is precisely what is needed to form a tensor product. The **[induced module](@entry_id:137976)** is defined as:

$$ \text{Ind}_H^G W := \mathbb{C}[G] \otimes_{\mathbb{C}[H]} W $$

The tensor product is taken over the ring $\mathbb{C}[H]$, which resolves the right $\mathbb{C}[H]$-action on $\mathbb{C}[G]$ and the left $\mathbb{C}[H]$-action on $W$. The resulting space, $\text{Ind}_H^G W$, inherits a left $\mathbb{C}[G]$-module structure from the left multiplication on $\mathbb{C}[G]$, thus defining a representation of $G$.

While this definition is algebraically precise, a more concrete construction is often helpful. Let $[G:H] = n$ be the index of $H$ in $G$, and let $\{t_1, t_2, \dots, t_n\}$ be a set of representatives for the left [cosets](@entry_id:147145) of $H$ in $G$, so that $G = \bigsqcup_{i=1}^n t_i H$. The vector space underlying $\text{Ind}_H^G W$ can be constructed as a [direct sum](@entry_id:156782) of $n$ copies of $W$:

$$ V_{\text{ind}} = t_1 \otimes W \oplus t_2 \otimes W \oplus \dots \oplus t_n \otimes W = \bigoplus_{i=1}^n t_i \otimes W $$

Here, each $t_i \otimes W$ is a vector space isomorphic to $W$, and an element of this space is a formal sum $\sum_{i=1}^n t_i \otimes w_i$ where $w_i \in W$. The action of an element $g \in G$ on a vector $t_i \otimes w$ is defined as follows: for each $i$, the element $g t_i$ must belong to some coset, say $t_j H$. Thus, $g t_i = t_j h$ for some unique $j$ and some $h \in H$. The action is then given by:

$$ g \cdot (t_i \otimes w) = t_j \otimes (h \cdot w) $$

Extending this action by linearity gives a representation of $G$. This construction reveals a most fundamental property of [induced representations](@entry_id:136842). The dimension of the induced space is the sum of the dimensions of its constituent parts. Since there are $[G:H]$ copies of $W$, we have the crucial dimension formula:

$$ \dim(\text{Ind}_H^G W) = [G:H] \dim(W) $$

For instance, if $H$ is a subgroup of index 3 in a group $G$, and $W$ is a 2-dimensional representation of $H$, the representation of $G$ induced from $W$ will have dimension $\dim(\text{Ind}_H^G W) = 3 \times 2 = 6$ [@problem_id:1650423]. This formula provides a quick and essential check on any calculation involving [induced representations](@entry_id:136842).

### The Character of an Induced Representation

To analyze the structure of an [induced representation](@entry_id:140832) and decompose it into [irreducible components](@entry_id:153033), we must compute its character. Let $\psi$ be the character of the representation $W$ of $H$. We can extend $\psi$ to a function $\dot{\psi}$ on all of $G$ by defining it to be zero for any element not in $H$:
$$ \dot{\psi}(g) = \begin{cases} \psi(g)  \text{if } g \in H \\ 0  \text{if } g \notin H \end{cases} $$

Let $\chi_{\text{ind}}$ denote the character of the [induced representation](@entry_id:140832) $\text{Ind}_H^G W$. A direct calculation from the definition yields a formula for its value at an element $g \in G$ in terms of the character $\psi$ of the original representation. One of the most useful forms of this formula is an average over the entire group $G$:

$$ \chi_{\text{ind}}(g) = \frac{1}{|H|} \sum_{x \in G} \dot{\psi}(x^{-1}gx) $$

This formula sums the values of $\psi$ over all conjugates of $g$ that happen to fall back into the subgroup $H$. An immediate and important consequence is that if an element $g \in G$ has no conjugates that lie in $H$ (other than the identity if $g=e$), then its character value in the [induced representation](@entry_id:140832) is zero [@problem_id:1650355].

Let's illustrate this with an example. Consider the symmetric group $G = S_3$ and the subgroup $H = \{e, (13)\}$ generated by a [transposition](@entry_id:155345). Let $\psi$ be the one-dimensional [sign character](@entry_id:137578) of $H$, where $\psi(e)=1$ and $\psi((13))=-1$. We wish to find the character $\chi$ of $\text{Ind}_H^G \psi$. The group $S_3$ has three conjugacy classes, with representatives $e$, $(12)$, and $(123)$.

*   **For the identity element $g=e$**: The formula simplifies to $\chi(e) = \frac{|G|}{|H|} \psi(e) = [G:H] \dim(W) = \frac{6}{2} \cdot 1 = 3$. This confirms the dimension formula.

*   **For a 3-cycle $g=(123)$**: The conjugates of a 3-cycle are all 3-cycles. None of these lie in $H=\{e, (13)\}$. Therefore, the sum in the [character formula](@entry_id:142515) is empty, and $\chi((123)) = 0$.

*   **For a 2-cycle $g=(12)$**: We need to sum over all $x \in S_3$ for which $x^{-1}(12)x \in H$. Since elements of $H$ have order 1 or 2, the conjugate $x^{-1}(12)x$ cannot be the identity (unless $g=e$). Thus, we must have $x^{-1}(12)x = (13)$. The set of elements $x$ that conjugate a given element to another in the same [conjugacy class](@entry_id:138270) is a coset of the [centralizer](@entry_id:146604). More directly, we can use an alternative form of the [character formula](@entry_id:142515):
    $$ \chi_{\text{ind}}(g) = \frac{|C_G(g)|}{|H|} \sum_{h \in \text{Cl}_G(g) \cap H} \psi(h) $$
    where $C_G(g)$ is the centralizer of $g$ in $G$ and $\text{Cl}_G(g)$ is its [conjugacy class](@entry_id:138270). For $g=(12)$, its conjugacy class is $\{(12), (13), (23)\}$, so the intersection with $H$ is just $\{(13)\}$. The centralizer of $(12)$ in $S_3$ is $\{e, (12)\}$, so its size is 2. The formula gives:
    $$ \chi((12)) = \frac{|C_{S_3}((12))|}{|H|} \psi((13)) = \frac{2}{2} \cdot (-1) = -1 $$

Combining these results, the character of the [induced representation](@entry_id:140832) is given by the values $(3, -1, 0)$ on the conjugacy classes of $e$, 2-cycles, and 3-cycles, respectively [@problem_id:1650418] [@problem_id:1650355]. Similar calculations can be performed for other groups, such as the dihedral group $D_4$ [@problem_id:1650376].

### Frobenius Reciprocity

One of the cornerstones of representation theory is a beautiful duality relationship between the operation of inducing a representation from a subgroup and the operation of restricting a representation to that subgroup. This relationship is encapsulated in the **Frobenius Reciprocity Theorem**.

Let $W$ be a representation of a subgroup $H \subset G$, and let $V$ be a representation of $G$. The theorem states that there is a [natural isomorphism](@entry_id:276379) between the spaces of intertwining maps (homomorphisms):

$$ \text{Hom}_G(\text{Ind}_H^G W, V) \cong \text{Hom}_H(W, \text{Res}_H^G V) $$

Here, $\text{Hom}_G$ denotes the space of $G$-module homomorphisms, and $\text{Res}_H^G V$ is the representation $V$ restricted to the subgroup $H$. In the language of characters, this powerful statement becomes an elegant and remarkably useful formula for inner products. If $\psi$ is the character of $W$ and $\chi$ is the character of $V$, then:

$$ \langle \chi_{\text{Ind}_H^G \psi}, \chi \rangle_G = \langle \psi, \chi_{\text{Res}_H^G V} \rangle_H $$

Recall that the [inner product of characters](@entry_id:137615) gives the [multiplicity](@entry_id:136466) of one irreducible representation within another. Frobenius reciprocity tells us that the [multiplicity](@entry_id:136466) of an irreducible $G$-representation $V$ in the [induced representation](@entry_id:140832) $\text{Ind}_H^G W$ is equal to the [multiplicity](@entry_id:136466) of the irreducible $H$-representation $W$ in the restriction of $V$ to $H$. This allows us to answer a question about a large representation of $G$ by performing a much simpler calculation entirely within the subgroup $H$.

Consider, for example, the group $G=S_4$ and its [cyclic subgroup](@entry_id:138079) $H = \langle (1234) \rangle$ of order 4. Let $W$ be a [one-dimensional representation](@entry_id:136509) of $H$ where the generator $(1234)$ acts as multiplication by $i = \sqrt{-1}$. Let $\psi$ be its character, so $\psi((1234)^k) = i^k$. Let $V$ be the irreducible 3-dimensional representation of $S_4$ with character $\chi_4$ (as given in standard [character tables](@entry_id:146676)). To find the multiplicity of $V$ in the decomposition of $\text{Ind}_H^G W$, we use Frobenius reciprocity [@problem_id:1650400]:

$$ \langle \chi_{\text{Ind}_H^G \psi}, \chi_4 \rangle_G = \langle \psi, \text{Res}_H^G \chi_4 \rangle_H = \frac{1}{|H|} \sum_{h \in H} \psi(h) \overline{\chi_4(h)} $$

We need the values of $\chi_4$ on the elements of $H$: $e, (1234), (13)(24), (1432)$. From the character table of $S_4$, these values are $\chi_4(e)=3$, $\chi_4((1234))=-1$, $\chi_4((13)(24))=-1$, and $\chi_4((1432))=-1$. The sum becomes:
$$ \frac{1}{4} \left( \psi(e)\overline{\chi_4(e)} + \psi(\sigma)\overline{\chi_4(\sigma)} + \psi(\sigma^2)\overline{\chi_4(\sigma^2)} + \psi(\sigma^3)\overline{\chi_4(\sigma^3)} \right) $$
$$ = \frac{1}{4} \left( 1 \cdot 3 + i \cdot (-1) + (-1) \cdot (-1) + (-i) \cdot (-1) \right) = \frac{1}{4} (3 - i + 1 + i) = \frac{4}{4} = 1 $$
Thus, the 3-dimensional representation $V$ appears with multiplicity 1 in the [induced representation](@entry_id:140832). This calculation would have been far more cumbersome without Frobenius reciprocity.

### Fundamental Algebraic Properties

Induction behaves predictably with respect to other standard constructions in representation theory, such as direct sums, tensor products, and repeated application.

*   **Additivity**: Induction distributes over direct sums. If $W_1$ and $W_2$ are representations of $H$, then there is a [natural isomorphism](@entry_id:276379) of $G$-modules:
    $$ \text{Ind}_H^G(W_1 \oplus W_2) \cong (\text{Ind}_H^G W_1) \oplus (\text{Ind}_H^G W_2) $$
    This follows from the fact that the tensor product distributes over direct sums. It implies that to decompose a representation induced from a [direct sum](@entry_id:156782), one can induce each component separately and then sum the results [@problem_id:1650388].

*   **Transitivity of Induction**: If we have a chain of subgroups $K \subset H \subset G$ and a representation $V$ of the smallest subgroup $K$, we can induce in two steps: first from $K$ to $H$, and then from $H$ to $G$. Alternatively, we can induce directly from $K$ to $G$. The [transitivity](@entry_id:141148) property states that these two procedures yield the same result:
    $$ \text{Ind}_H^G (\text{Ind}_K^H V) \cong \text{Ind}_K^G V $$
    This is a consequence of the associativity of the [tensor product of modules](@entry_id:155679). It provides a powerful consistency check and simplifies many theoretical arguments [@problem_id:1650415].

*   **Tensor Identity (Frobenius Identity)**: This identity describes how induction interacts with tensor products. Let $V$ be a representation of $H$ and $W$ be a representation of $G$. The [tensor product](@entry_id:140694) $(\text{Ind}_H^G V) \otimes W$ is a new representation of $G$. The identity states:
    $$ (\text{Ind}_H^G V) \otimes W \cong \text{Ind}_H^G (V \otimes \text{Res}_H^G W) $$
    This means that tensoring an [induced representation](@entry_id:140832) with $W$ is equivalent to first restricting $W$ to $H$, tensoring it with $V$, and then inducing the result back up to $G$. At the level of characters, this gives the simple product rule $\chi_{(\text{Ind} V) \otimes W} = \chi_{\text{Ind} V} \cdot \chi_W$, which is often used in computations [@problem_id:1650417].

### Special Cases and Advanced Structures

The general theory of [induced representations](@entry_id:136842) simplifies and reveals further structure in certain important special cases.

A particularly elegant result occurs when we induce the [regular representation](@entry_id:137028) of the subgroup $H$. The [left regular representation](@entry_id:146345) of $H$ is the [group algebra](@entry_id:145139) $\mathbb{C}[H]$ viewed as a module over itself. Inducing this representation to $G$ yields the [left regular representation](@entry_id:146345) of $G$:
$$ \text{Ind}_H^G (\mathbb{C}[H]) \cong \mathbb{C}[G] $$
This follows from the property $\mathbb{C}[G] \otimes_{\mathbb{C}[H]} \mathbb{C}[H] \cong \mathbb{C}[G]$ for group algebras. As a consequence, we can find the decomposition of this specific [induced module](@entry_id:137976) by using the well-known [decomposition of the regular representation](@entry_id:146409) of $G$: it contains each irreducible representation $V_i$ of $G$ with [multiplicity](@entry_id:136466) equal to its dimension, $\dim(V_i)$ [@problem_id:1650404].

Another important special case is induction from a **normal subgroup** $H \trianglelefteq G$. The structure of $\text{Ind}_H^G W$ is then governed by what is known as **Clifford Theory**. When $H$ is normal, the group $G$ acts on the set of irreducible representations of $H$ by conjugation. For an irreducible representation $W$ of $H$ and an element $g \in G$, the [conjugate representation](@entry_id:139136) $g \cdot W$ is defined on the same vector space, where an element $h \in H$ acts as the element $g^{-1}hg$ does in the original representation $W$.

The key to understanding $\text{Ind}_H^G W$ is the **inertia subgroup** of $W$ in $G$, defined as $I_G(W) = \{ g \in G \mid g \cdot W \cong W \}$. This is the subgroup of $G$ that fixes the [isomorphism](@entry_id:137127) class of $W$. Clifford's theorem states that the [induced representation](@entry_id:140832) $\text{Ind}_H^G W$ is irreducible if and only if $W$ is irreducible and its inertia subgroup is just $H$ itself. If [the inertia group](@entry_id:200010) is larger than $H$, the [induced representation](@entry_id:140832) decomposes.

For example, consider $G=S_4$ and its normal subgroup $H=V_4$, the Klein four-group. Let $W$ be a non-trivial [one-dimensional representation](@entry_id:136509) of $H$. One can show that its [inertia group](@entry_id:143171) is larger than $H$, and as a result, $\text{Ind}_H^G W$ is reducible. A calculation using Frobenius reciprocity reveals that it decomposes into the direct sum of the two non-isomorphic 3-dimensional [irreducible representations](@entry_id:138184) of $S_4$ [@problem_id:1650399]. This provides a glimpse into the rich, intricate structure that induction reveals about the relationship between a group and its [normal subgroups](@entry_id:147397).