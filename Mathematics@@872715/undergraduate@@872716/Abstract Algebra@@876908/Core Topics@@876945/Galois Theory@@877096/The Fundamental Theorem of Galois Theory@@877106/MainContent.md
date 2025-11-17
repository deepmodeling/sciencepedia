## Introduction
At the heart of abstract algebra lies a quest to understand the structure of mathematical objects. While [field theory](@entry_id:155241) provides the language for studying [roots of polynomials](@entry_id:154615), its intricate hierarchy of extensions can be difficult to navigate. The profound insight of Évariste Galois was to reveal that this complexity could be understood through the more discrete and combinatorial world of group theory. The Fundamental Theorem of Galois Theory is the culmination of this idea, creating a beautiful and powerful 'dictionary' that translates problems about fields into problems about finite groups. This article serves as a comprehensive guide to this cornerstone theorem. In the following chapters, you will first learn the core **Principles and Mechanisms** of the Galois correspondence, exploring the bijection between [intermediate fields](@entry_id:153550) and subgroups and the special role of [normal extensions](@entry_id:156398). Next, we will delve into its far-reaching **Applications and Interdisciplinary Connections**, demonstrating how the theorem solves the ancient problem of [solvability by radicals](@entry_id:154539) and provides structural insights into finite fields and other algebraic systems. Finally, you will have the opportunity to solidify your understanding through a series of **Hands-On Practices** designed to apply the theory to concrete examples.

## Principles and Mechanisms

The Fundamental Theorem of Galois Theory provides the profound and beautiful connection between field theory and group theory. Having established the preliminary concepts of Galois groups and [field extensions](@entry_id:153187), we now delve into the principles and mechanisms of the theorem itself. This theorem provides a precise, dictionary-like correspondence that translates complex questions about field structures into more manageable problems within [finite group theory](@entry_id:146601). We will explore the structure of this correspondence, its key properties, and the special role played by [normal extensions](@entry_id:156398).

### The Galois Correspondence: A Bridge Between Fields and Groups

The centerpiece of Galois theory is a remarkable [bijection](@entry_id:138092). For any finite **Galois extension** $L/K$ with Galois group $G = \text{Gal}(L/K)$, the theorem establishes a [one-to-one correspondence](@entry_id:143935) between two sets:

1.  The set of all **[intermediate fields](@entry_id:153550)** $E$, such that $K \subseteq E \subseteq L$.
2.  The set of all **subgroups** $H$ of the Galois group $G$.

This correspondence is realized through two mutually inverse maps. First, any intermediate field $E$ is mapped to the subgroup of automorphisms that fix every element of $E$. This subgroup is denoted $\text{Gal}(L/E)$.

Conversely, any subgroup $H \subseteq G$ is mapped to its **[fixed field](@entry_id:155430)**, denoted $L^H$. This is the set of all elements in $L$ that are left unchanged by every automorphism in $H$:
$$L^H = \{x \in L \mid \sigma(x) = x \text{ for all } \sigma \in H\}$$
It can be verified that $L^H$ is indeed an intermediate field between $K$ and $L$.

This correspondence is not merely a pairing; it carries rich structural information. Two of its most fundamental properties are:

-   **Inclusion-Reversing**: The correspondence reverses inclusions. If $E_1$ and $E_2$ are two [intermediate fields](@entry_id:153550) with corresponding subgroups $H_1 = \text{Gal}(L/E_1)$ and $H_2 = \text{Gal}(L/E_2)$, then $E_1 \subseteq E_2$ if and only if $H_2 \subseteq H_1$. A larger field is fixed by a smaller group of [automorphisms](@entry_id:155390), and a larger group of [automorphisms](@entry_id:155390) can only fix a smaller field.

-   **Degrees and Orders**: The correspondence relates the degrees of [field extensions](@entry_id:153187) to the orders of the corresponding groups. For any intermediate field $E$ corresponding to a subgroup $H$, we have:
    $$[L:E] = |H|$$
    $$[E:K] = \frac{[L:K]}{|H|} = \frac{|G|}{|H|} = [G:H]$$
    where $[G:H]$ is the index of the subgroup $H$ in $G$.

This relationship is an exceptionally powerful computational tool. For instance, consider the extension $L/K$ where $K = \mathbb{Q}$ and $L$ is the [splitting field](@entry_id:156669) of the polynomial $p(x) = x^3 - 5$. The roots of this polynomial are $\sqrt[3]{5}$, $\sqrt[3]{5}\omega$, and $\sqrt[3]{5}\omega^2$, where $\omega = \exp(i\frac{2\pi}{3})$ is a primitive cube root of unity. The [splitting field](@entry_id:156669) is thus $L = \mathbb{Q}(\sqrt[3]{5}, \omega)$, and the degree of the extension $[L:\mathbb{Q}]$ is 6. If we examine the intermediate field $E = \mathbb{Q}(\sqrt[3]{5})$, we can determine the degree $[L:E]$ using this principle. The degree of the lower extension is $[E:\mathbb{Q}] = 3$, as the [minimal polynomial](@entry_id:153598) of $\sqrt[3]{5}$ over $\mathbb{Q}$ is $x^3-5$. The Galois group $G = \text{Gal}(L/\mathbb{Q})$ has order $|G| = [L:\mathbb{Q}] = 6$. The subgroup $H = \text{Gal}(L/E)$ corresponding to $E$ must have an order such that $[E:\mathbb{Q}] = [G:H]$, which gives $3 = 6 / |H|$, implying $|H|=2$. Consequently, the degree of the top part of the extension must be $[L:E] = |H| = 2$. This matches the direct calculation, as $L = E(\omega)$ and the [minimal polynomial](@entry_id:153598) of $\omega$ over the real field $E$ is $x^2+x+1$, which is of degree 2 [@problem_id:1832446].

Conversely, knowing the [degree of an extension](@entry_id:148122) can help identify the corresponding subgroup. In the [cyclotomic extension](@entry_id:149979) $L = \mathbb{Q}(\zeta_7)$ over $\mathbb{Q}$, where $\zeta_7$ is a primitive 7th root of unity, the Galois group $G = \text{Gal}(L/\mathbb{Q})$ is cyclic of order $\varphi(7)=6$. If we are told there exists a unique cubic subfield $F$ (i.e., $[F:\mathbb{Q}]=3$), the theorem guarantees it corresponds to a subgroup $H$ of index $[G:H] = [F:\mathbb{Q}] = 3$. This means the order of the subgroup must be $|H| = |G|/3 = 6/3=2$. Since $G$ is cyclic, it has a unique subgroup of order 2. This subgroup must be $H = \{\sigma_1, \sigma_6\}$, where $\sigma_k(\zeta_7) = \zeta_7^k$, as $k=6$ is the unique element of [multiplicative order](@entry_id:636522) 2 modulo 7 [@problem_id:1832420].

### Visualizing the Correspondence: Lattices of Fields and Subgroups

The inclusion-reversing nature of the Galois correspondence allows for a powerful visualization. The collection of all [intermediate fields](@entry_id:153550) of an extension $L/K$ forms a lattice under inclusion. Similarly, the subgroups of the Galois group $G$ form a lattice. The Fundamental Theorem implies that the lattice diagram of [intermediate fields](@entry_id:153550) is the inverted mirror image of the lattice diagram of subgroups.

A classic illustration is the biquadratic extension $K = \mathbb{Q}(\sqrt{3}, \sqrt{5})$ over $\mathbb{Q}$. This is the [splitting field](@entry_id:156669) of $(x^2-3)(x^2-5)$, a Galois extension of degree 4. Its Galois group $G = \text{Gal}(K/\mathbb{Q})$ is isomorphic to the Klein four-group, $V_4 \cong \mathbb{Z}_2 \times \mathbb{Z}_2$. The group $G$ has four elements. Let us define two [automorphisms](@entry_id:155390), $\sigma$ and $\tau$, by their actions on the generators:
-   $\sigma(\sqrt{3}) = -\sqrt{3}$ and $\sigma(\sqrt{5}) = \sqrt{5}$
-   $\tau(\sqrt{3}) = \sqrt{3}$ and $\tau(\sqrt{5}) = -\sqrt{5}$

The group is then $G = \{e, \sigma, \tau, \sigma\tau\}$, where $e$ is the identity. This group has exactly five subgroups: the trivial group $\{e\}$, the entire group $G$, and three distinct subgroups of order 2:
-   $H_1 = \langle \sigma \rangle = \{e, \sigma\}$
-   $H_2 = \langle \tau \rangle = \{e, \tau\}$
-   $H_3 = \langle \sigma\tau \rangle = \{e, \sigma\tau\}$

The Fundamental Theorem asserts there must be exactly three [intermediate fields](@entry_id:153550) between $\mathbb{Q}$ and $K$. We find these by determining the [fixed field](@entry_id:155430) for each subgroup:
-   The [fixed field](@entry_id:155430) of $H_1$, $K^{H_1}$, must contain elements fixed by $\sigma$. Clearly, $\sqrt{5}$ is fixed, so $K^{H_1} = \mathbb{Q}(\sqrt{5})$.
-   The [fixed field](@entry_id:155430) of $H_2$, $K^{H_2}$, must contain elements fixed by $\tau$. Clearly, $\sqrt{3}$ is fixed, so $K^{H_2} = \mathbb{Q}(\sqrt{3})$.
-   The [fixed field](@entry_id:155430) of $H_3$, $K^{H_3}$, contains elements fixed by $\sigma\tau$. The element $\sqrt{15} = \sqrt{3}\sqrt{5}$ has the property that $(\sigma\tau)(\sqrt{3}\sqrt{5}) = \sigma(\sqrt{3})\tau(\sqrt{5}) = (-\sqrt{3})(-\sqrt{5}) = \sqrt{15}$. Thus, $K^{H_3} = \mathbb{Q}(\sqrt{15})$.

This perfectly illustrates the correspondence: the three proper non-trivial subgroups map to three proper non-trivial [intermediate fields](@entry_id:153550). The sum of the square-free integers defining these fields is $3+5+15=23$ [@problem_id:1832391].

### The Special Role of Normal Extensions

A particularly important aspect of the Fundamental Theorem concerns [normal extensions](@entry_id:156398). An intermediate extension $E/K$ is **normal** if and only if its corresponding subgroup $H = \text{Gal}(L/E)$ is a **normal subgroup** of $G = \text{Gal}(L/K)$.

Recall that an extension $E/K$ is normal if every [irreducible polynomial](@entry_id:156607) in $K[x]$ that has at least one root in $E$ must split into linear factors in $E[x]$. This property is often difficult to check directly. Galois theory provides an elegant group-theoretic equivalent.

For example, the extension $\mathbb{Q}(\sqrt[3]{5})/\mathbb{Q}$ is not normal. The [minimal polynomial](@entry_id:153598) of $\sqrt[3]{5}$ is $p(x) = x^3-5$. This polynomial is irreducible over $\mathbb{Q}$, has one root in $\mathbb{Q}(\sqrt[3]{5})$, but its other two roots, $\sqrt[3]{5}\omega$ and $\sqrt[3]{5}\omega^2$, are non-real complex numbers and thus are not in the real field $\mathbb{Q}(\sqrt[3]{5})$. Because the polynomial does not split, the extension is not normal [@problem_id:1832425].

This connection allows us to count non-normal intermediate extensions by counting non-normal subgroups. Consider the [splitting field](@entry_id:156669) of $x^4-5$ over $\mathbb{Q}$, which is $K = \mathbb{Q}(\sqrt[4]{5}, i)$. This is a Galois extension of degree 8, and its Galois group $G = \text{Gal}(K/\mathbb{Q})$ is isomorphic to the dihedral group of order 8, $D_4$. To find the number of [intermediate fields](@entry_id:153550) $E$ where $E/\mathbb{Q}$ is not a Galois (and thus not normal) extension, we simply need to find the number of non-normal subgroups of $D_4$. The group $D_4$ has five subgroups of order 2. One, the center $\langle r^2 \rangle$, is normal. The other four, generated by the "reflections," are not. Thus, there are exactly four [intermediate fields](@entry_id:153550) of $K$ that are not [normal extensions](@entry_id:156398) over $\mathbb{Q}$ [@problem_id:1779465].

When an intermediate extension $E/K$ is indeed normal (and thus Galois), the theorem provides a further insight. The Galois group of this sub-extension, $\text{Gal}(E/K)$, is isomorphic to the quotient group of the larger Galois groups:
$$ \text{Gal}(E/K) \cong G/H = \text{Gal}(L/K) / \text{Gal}(L/E) $$
The [isomorphism](@entry_id:137127) is given by the natural restriction map, which takes an automorphism $\sigma \in G$ and restricts its domain to the field $E$. Since $E/K$ is normal, any automorphism of $L$ that fixes $K$ must map $E$ to itself, making this restriction well-defined. For example, in the tower $\mathbb{Q} \subset E = \mathbb{Q}(i, \sqrt{3}) \subset L = \mathbb{Q}(\sqrt[4]{3}, i)$, an [automorphism](@entry_id:143521) $\sigma \in \text{Gal}(L/\mathbb{Q})$ defined by $\sigma(\sqrt[4]{3}) = i\sqrt[4]{3}$ and $\sigma(i)=-i$ can be restricted to an automorphism $\tau \in \text{Gal}(E/\mathbb{Q})$. The action of $\tau$ on the generators of $E$ is determined by $\sigma$: $\tau(i) = \sigma(i) = -i$ and $\tau(\sqrt{3}) = \sigma((\sqrt[4]{3})^2) = (\sigma(\sqrt[4]{3}))^2 = (i\sqrt[4]{3})^2 = -\sqrt{3}$ [@problem_id:1647846].

### Operations on Fields and Groups

The Galois correspondence also translates common constructions on fields into constructions on groups.

-   **Intersection and Generated Subgroups**: The subgroup corresponding to the intersection of two [intermediate fields](@entry_id:153550), $E_1 \cap E_2$, is the smallest subgroup containing both of their corresponding subgroups, $H_1$ and $H_2$. This is the **subgroup generated by the union** of $H_1$ and $H_2$, denoted $\langle H_1, H_2 \rangle$. This does not correspond to $H_1 \cap H_2$ or $H_1 \cup H_2$ (which is generally not a group) [@problem_id:1832445].

-   **Compositum and Intersection of Subgroups**: Dually, the subgroup corresponding to the **compositum** of two fields, $E_1 E_2$ (the smallest field containing both $E_1$ and $E_2$), is the intersection of their corresponding subgroups, $H_1 \cap H_2$. An automorphism fixes the compositum if and only if it fixes both $E_1$ and $E_2$ individually.

-   **Normal Closure**: The **[normal closure](@entry_id:139625)** of an extension $E/K$ is the smallest extension of $E$ that is normal over $K$. Within a larger Galois extension $L/K$, the [normal closure](@entry_id:139625) of an intermediate field $E=L^H$ corresponds to the largest [normal subgroup](@entry_id:144438) of $G$ that is contained within $H$. For example, consider the extension $L = \mathbb{Q}(\sqrt[6]{7}, \zeta_6)$ over $\mathbb{Q}$, with Galois group $G \cong D_6$ (order 12). The intermediate field $E = \mathbb{Q}((\sqrt[6]{7})^2) = \mathbb{Q}(\sqrt[3]{7})$ is not normal. Its [normal closure](@entry_id:139625) is $N = \mathbb{Q}(\sqrt[3]{7}, \zeta_3)$. This is a degree 6 extension over $\mathbb{Q}$. By the degree formula, the subgroup $H_N = \text{Gal}(L/N)$ must have order $|G|/[N:\mathbb{Q}] = 12/6 = 2$. Since $N/\mathbb{Q}$ is normal, $H_N$ must be a normal subgroup of $G \cong D_6$. The unique [normal subgroup](@entry_id:144438) of order 2 in $D_6$ is its center, which corresponds to the subgroup $\langle r^3 \rangle$ in a standard presentation [@problem_id:1832377].

The practical mechanism of finding a [fixed field](@entry_id:155430) involves identifying elements or combinations of generators that are invariant under the action of a given subgroup. For the cyclotomic field $K = \mathbb{Q}(\zeta_{12})$, the Galois group $\text{Gal}(K/\mathbb{Q})$ is isomorphic to $(\mathbb{Z}/12\mathbb{Z})^\times = \{1, 5, 7, 11\}$. To find the [fixed field](@entry_id:155430) of the subgroup $H = \langle \sigma_5 \rangle$, where $\sigma_5(\zeta_{12}) = \zeta_{12}^5$, we test the action of $\sigma_5$ on simple elements of $K$. One such element is $i = \zeta_{12}^3$. We find $\sigma_5(i) = \sigma_5(\zeta_{12}^3) = (\zeta_{12}^5)^3 = \zeta_{12}^{15} = \zeta_{12}^3 = i$. Thus, $i$ is in the [fixed field](@entry_id:155430), which implies $\mathbb{Q}(i)$ is contained in the [fixed field](@entry_id:155430). By degree considerations, the [fixed field](@entry_id:155430) is exactly $\mathbb{Q}(i) = \mathbb{Q}(\sqrt{-1})$ [@problem_id:1832373].

### Why "Galois"? The Consequences of Non-Galois Extensions

The elegance and power of the Fundamental Theorem depend critically on the hypothesis that the extension $L/K$ is a **Galois extension** (i.e., it is finite, normal, and separable). If any of these conditions fail, the beautiful [one-to-one correspondence](@entry_id:143935) breaks down.

Let's consider an extension that is not Galois and observe the failure of the correspondence. Let $K=\mathbb{Q}$ and $E = \mathbb{Q}(\alpha)$ where $\alpha = \sqrt[4]{2}$. The minimal polynomial for $\alpha$ is $x^4-2=0$. Its roots are $\pm \alpha$ and $\pm i\alpha$. Since $E$ is a subfield of the real numbers, it contains $\alpha$ and $-\alpha$ but not the [complex roots](@entry_id:172941). Therefore, the extension $E/K$ is not normal, and thus not Galois.

The group of [automorphisms](@entry_id:155390) $\text{Aut}(E/K)$ consists of maps that fix $\mathbb{Q}$ and send $\alpha$ to another root of $x^4-2$ that lies within $E$. The only possibilities are $\alpha \mapsto \alpha$ (the identity, $\text{id}$) and $\alpha \mapsto -\alpha$ (let's call this $\sigma$). Thus, $\text{Aut}(E/K) = \{\text{id}, \sigma\}$, a group of order 2.

Now, let's examine the "Galois correspondence" for this non-Galois extension.
-   The base field is $F_1 = \mathbb{Q}$. The subgroup that fixes it is, by definition, the entire [automorphism group](@entry_id:139672), $\text{Aut}(E/\mathbb{Q}) = \{\text{id}, \sigma\}$.
-   Consider the intermediate field $F_2 = \mathbb{Q}(\sqrt{2}) = \mathbb{Q}(\alpha^2)$. An automorphism $\phi \in \text{Aut}(E/\mathbb{Q})$ fixes $F_2$ if it fixes $\alpha^2$. Let's check our two automorphisms:
    -   $\text{id}(\alpha^2) = (\text{id}(\alpha))^2 = \alpha^2$.
    -   $\sigma(\alpha^2) = (\sigma(\alpha))^2 = (-\alpha)^2 = \alpha^2$.
    Both automorphisms in $\text{Aut}(E/\mathbb{Q})$ fix the field $\mathbb{Q}(\sqrt{2})$. Thus, the group corresponding to $F_2$ is also $\text{Aut}(E/F_2) = \{\text{id}, \sigma\}$.

Here we have two distinct [intermediate fields](@entry_id:153550), $\mathbb{Q}$ and $\mathbb{Q}(\sqrt{2})$, that both correspond to the same subgroup of automorphisms. This demonstrates a failure of [injectivity](@entry_id:147722) for the map from fields to groups. The [one-to-one correspondence](@entry_id:143935) is broken [@problem_id:1832385]. This example underscores why the normality condition is not just a technical detail but is essential to the entire structure of the theory.