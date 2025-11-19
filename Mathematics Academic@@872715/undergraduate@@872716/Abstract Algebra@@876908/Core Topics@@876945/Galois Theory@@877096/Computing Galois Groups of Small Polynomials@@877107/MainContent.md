## Introduction
Galois theory provides a profound link between the theory of fields and the theory of groups, offering deep insights into the structure of polynomial equations. The Galois group of a polynomial, an object of abstract algebra, acts as a measure of the equation's inherent symmetries. However, moving from this abstract definition to concrete computation for a given polynomial presents a significant challenge. This article addresses the knowledge gap between theory and practice by providing a clear, step-by-step guide to computing the Galois groups of polynomials of small degree.

Across three chapters, you will gain a robust toolkit for this task. The first chapter, "Principles and Mechanisms," establishes the foundational methods, explaining how to interpret the Galois group as a group of permutations and how to use tools like the [discriminant](@entry_id:152620) and modular arithmetic to constrain its structure. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the power of these computations by exploring their impact on classical problems in geometry, their deep connections to number theory, and their role in proving the [unsolvability of the quintic](@entry_id:148624). Finally, the "Hands-On Practices" section will allow you to apply these techniques to specific problems, solidifying your understanding and building computational fluency.

## Principles and Mechanisms

Having introduced the foundational concepts of Galois theory, we now turn to the practical matter of its application. The central objective of this chapter is to develop a systematic methodology for computing the Galois group of a given polynomial, particularly those of small degree with rational coefficients. This endeavor is not merely a computational exercise; it is a profound exploration into the hidden symmetries of numbers and equations. We will see how the structure of a polynomial's Galois group is intricately linked to properties such as its irreducibility, the nature of its roots, and even its behavior under [modular arithmetic](@entry_id:143700).

### The Galois Group as a Group of Permutations

The cornerstone of computing a Galois group lies in its interpretation as a group of [permutations](@entry_id:147130). Let $f(x)$ be a polynomial of degree $n$ with coefficients in a field $F$, and let $K$ be its [splitting field](@entry_id:156669). The **Galois group** $\text{Gal}(K/F)$ consists of all automorphisms of $K$ that fix every element of $F$.

A crucial property of any such automorphism $\sigma \in \text{Gal}(K/F)$ is that it must preserve the algebraic structure of the field. If $\alpha$ is a root of $f(x)$, so $f(\alpha) = 0$, then applying $\sigma$ to this equation yields:
$$
\sigma(f(\alpha)) = f(\sigma(\alpha)) = 0
$$
The second equality holds because the coefficients of $f(x)$ are in $F$ and are therefore fixed by $\sigma$. This demonstrates that $\sigma(\alpha)$ must also be a root of $f(x)$. Consequently, every automorphism in the Galois group permutes the roots of the polynomial. This observation gives us a concrete representation of the abstract Galois group: it can be viewed as a subgroup of the [symmetric group](@entry_id:142255) $S_n$, the group of all permutations of the $n$ roots.

This embedding, $\text{Gal}(K/F) \hookrightarrow S_n$, is one of the most powerful tools at our disposal. The order of the Galois group, $|\text{Gal}(K/F)|$, is equal to the degree of the [splitting field](@entry_id:156669) extension, $[K:F]$.

A further critical constraint arises when the polynomial $f(x)$ is **irreducible** over $F$. In this case, the Galois group acts **transitively** on the set of roots. This means that for any two roots $\alpha_i$ and $\alpha_j$, there exists an automorphism $\sigma \in \text{Gal}(K/F)$ such that $\sigma(\alpha_i) = \alpha_j$. This significantly narrows down the possible subgroups of $S_n$ that can serve as the Galois group. For instance, the Galois group of an irreducible cubic must be a transitive subgroup of $S_3$.

### The Impact of Reducibility

The first step in analyzing any polynomial is to test for its reducibility over the base field, typically $\mathbb{Q}$. The structure of the Galois group is fundamentally different for reducible and [irreducible polynomials](@entry_id:152257).

If a polynomial $f(x) \in \mathbb{Q}[x]$ factors completely into linear terms over $\mathbb{Q}$, for example $f(x) = (x-1)(x-2)(x+3)$, then all its roots ($1, 2, -3$) are already in the base field [@problem_id:1783802]. The [splitting field](@entry_id:156669) is $\mathbb{Q}$ itself. The only automorphism of $\mathbb{Q}$ that fixes $\mathbb{Q}$ is the identity map. Therefore, the Galois group is the [trivial group](@entry_id:151996), $\{e\}$.

More generally, if $f(x)$ is reducible over $\mathbb{Q}$, say $f(x) = g(x)h(x)$, its [splitting field](@entry_id:156669) is the **compositum** of the [splitting fields](@entry_id:151552) of its factors. Let $L_g$ and $L_h$ be the [splitting fields](@entry_id:151552) for $g(x)$ and $h(x)$, respectively. The [splitting field](@entry_id:156669) of $f(x)$ is $L_f = L_g L_h$. A powerful theorem states that if $L_g$ and $L_h$ are both Galois extensions of $\mathbb{Q}$ with $L_g \cap L_h = \mathbb{Q}$, then the Galois group of the compositum is the [direct product](@entry_id:143046) of the individual Galois groups:
$$
\text{Gal}(L_f / \mathbb{Q}) \cong \text{Gal}(L_g / \mathbb{Q}) \times \text{Gal}(L_h / \mathbb{Q})
$$

Consider, for instance, the polynomial $h(x) = (x^3 - 2)(x^2 - 5)$ over $\mathbb{Q}$ [@problem_id:1783771]. The [splitting field](@entry_id:156669) of $g(x) = x^2 - 5$ is $M = \mathbb{Q}(\sqrt{5})$, a degree-2 extension with Galois group $\text{Gal}(M/\mathbb{Q}) \cong C_2$. The polynomial $f(x) = x^3 - 2$ is irreducible and its [splitting field](@entry_id:156669) is $L = \mathbb{Q}(\sqrt[3]{2}, \omega)$, where $\omega$ is a primitive cube root of unity. The Galois group is $\text{Gal}(L/\mathbb{Q}) \cong S_3$. To check if $L \cap M = \mathbb{Q}$, we can examine the quadratic subfields. The unique quadratic subfield of $L$ corresponds to the index-2 subgroup $A_3$ and is given by $\mathbb{Q}(\sqrt{\Delta_f})$, where $\Delta_f = -108$ is the [discriminant](@entry_id:152620) of $x^3-2$. This [subfield](@entry_id:155812) is $\mathbb{Q}(\sqrt{-3})$. Since $\mathbb{Q}(\sqrt{-3}) \neq \mathbb{Q}(\sqrt{5})$, the intersection of the [splitting fields](@entry_id:151552) is indeed just $\mathbb{Q}$. We can therefore conclude that the Galois group of $h(x)$ is $\text{Gal}(h/\mathbb{Q}) \cong S_3 \times C_2$.

### The Cubic Case: The Discriminant as a Decisive Tool

For an irreducible cubic polynomial $f(x) \in \mathbb{Q}[x]$, we know its Galois group must be a transitive subgroup of $S_3$. The only possibilities are the alternating group $A_3$ (which is cyclic of order 3) and the full [symmetric group](@entry_id:142255) $S_3$ (of order 6).

The choice between these two groups is determined by a single number: the **[discriminant](@entry_id:152620)** of the polynomial. For a general cubic $x^3+ax^2+bx+c$, the [discriminant](@entry_id:152620) is given by the formula $\Delta = a^2b^2 - 4b^3 - 4a^3c - 27c^2 + 18abc$. For the depressed cubic $x^3+px+q$, this simplifies to $\Delta = -4p^3 - 27q^2$.

Let the roots of the cubic be $\alpha_1, \alpha_2, \alpha_3$. The discriminant is $\Delta = [(\alpha_1-\alpha_2)(\alpha_2-\alpha_3)(\alpha_3-\alpha_1)]^2$. The key insight is to consider the square root of the discriminant, $\delta = \sqrt{\Delta}$. An [automorphism](@entry_id:143521) $\sigma \in S_3$ fixes $\delta$ if and only if it is an [even permutation](@entry_id:152892) (i.e., $\sigma \in A_3$). Therefore, the entire Galois group is contained within $A_3$ if and only if $\delta$ is fixed by all [automorphisms](@entry_id:155390), which means $\delta$ must belong to the base field $\mathbb{Q}$. This leads to a simple and powerful rule:

**For an irreducible cubic polynomial over $\mathbb{Q}$, its Galois group is $A_3$ if the [discriminant](@entry_id:152620) is a perfect square in $\mathbb{Q}$, and $S_3$ otherwise.**

Let's examine two illustrative examples.
1.  Consider $P(x) = x^3 - 3x + 1$ [@problem_id:1783768]. This polynomial is irreducible over $\mathbb{Q}$. Its discriminant is $\Delta = -4(-3)^3 - 27(1)^2 = 108 - 27 = 81$. Since $81 = 9^2$ is a square in $\mathbb{Q}$, the Galois group is $A_3 \cong \mathbb{Z}/3\mathbb{Z}$.
2.  Consider $P(x) = x^3 - 6x^2 + 7x + 3$ [@problem_id:1783792]. This polynomial is also irreducible over $\mathbb{Q}$. Its [discriminant](@entry_id:152620) is $\Delta = 473$. As $473$ is not a perfect square in $\mathbb{Q}$, the Galois group must be $S_3$.

This principle extends to the abstract case. For the "generic" cubic $y^3 + py + q$ over the field of [rational functions](@entry_id:154279) $F = \mathbb{Q}(p,q)$, the [discriminant](@entry_id:152620) is $\Delta = -4p^3 - 27q^2$. One can show that this $\Delta$ is not a square in $F$. This implies that the generic cubic has Galois group $S_3$, reinforcing the idea that $S_3$ is the default or most general symmetry group for a degree-3 equation [@problem_id:1783736].

### The Quartic Case: A Richer Landscape

For an irreducible quartic (degree-4) polynomial, the Galois group must be a transitive subgroup of $S_4$. There are five such groups: the cyclic group $C_4$, the Klein four-group $V_4 \cong C_2 \times C_2$, the [dihedral group](@entry_id:143875) $D_4$ of order 8, the [alternating group](@entry_id:140499) $A_4$, and the full [symmetric group](@entry_id:142255) $S_4$. While general methods involving a resolvent cubic exist, certain structural forms of the polynomial allow for a more direct determination.

A common and important type is the **biquadratic polynomial**, whose roots can be expressed using only nested square roots. For instance, consider $p(x) = x^4 - 10x^2 + 1$ [@problem_id:1783782]. By treating it as a quadratic in $x^2$, we find its roots to be $\pm \sqrt{5 \pm 2\sqrt{6}}$. These simplify to $\pm(\sqrt{3}+\sqrt{2})$ and $\pm(\sqrt{3}-\sqrt{2})$. The [splitting field](@entry_id:156669) is evidently $K = \mathbb{Q}(\sqrt{2}, \sqrt{3})$. This is a biquadratic extension of degree 4 over $\mathbb{Q}$. An [automorphism](@entry_id:143521) is determined by where it sends the generators $\sqrt{2}$ and $\sqrt{3}$. The possibilities are $\sqrt{2} \mapsto \pm\sqrt{2}$ and $\sqrt{3} \mapsto \pm\sqrt{3}$, leading to four distinct automorphisms. This group is isomorphic to the Klein four-group, $V_4$.

Another important class of quartics involves transformations of simpler polynomials. The Galois group is invariant under linear substitution of the variable. For example, the polynomial $P(x) = x^4 - 4x^3 + 6x^2 - 4x - 1$ can be recognized as $(x-1)^4 - 2$ [@problem_id:1783757]. Its roots are $x = 1 \pm \sqrt[4]{2}$ and $x = 1 \pm i\sqrt[4]{2}$. The [splitting field](@entry_id:156669) for $P(x)$ is the same as the [splitting field](@entry_id:156669) for $y^4-2$, namely $K = \mathbb{Q}(\sqrt[4]{2}, i)$. The degree of this extension is $[K:\mathbb{Q}] = [\mathbb{Q}(\sqrt[4]{2}, i) : \mathbb{Q}(\sqrt[4]{2})] \cdot [\mathbb{Q}(\sqrt[4]{2}) : \mathbb{Q}] = 2 \cdot 4 = 8$. The Galois group is thus of order 8. By defining automorphisms $\sigma: (\sqrt[4]{2} \mapsto i\sqrt[4]{2}, i \mapsto i)$ and $\tau: (\sqrt[4]{2} \mapsto \sqrt[4]{2}, i \mapsto -i)$, one can verify the relations $\sigma^4 = \text{id}$, $\tau^2 = \text{id}$, and $\tau\sigma\tau^{-1} = \sigma^{-1}$. These are the defining relations for the dihedral group $D_4$, the symmetry group of a square.

### The Power of Modular Arithmetic: Dedekind's Theorem

A remarkably powerful technique for probing the structure of a Galois group involves reducing the polynomial modulo a prime $p$. The connection is provided by a theorem of Dedekind.

**Dedekind's Theorem (Informal Statement):** Let $f(x) \in \mathbb{Z}[x]$ be a [monic polynomial](@entry_id:152311). For any prime $p$ that does not divide the discriminant of $f(x)$, consider the factorization of $f(x)$ into [irreducible polynomials](@entry_id:152257) in $\mathbb{F}_p[x]$:
$$
f(x) \equiv f_1(x) f_2(x) \cdots f_k(x) \pmod{p}
$$
The list of the degrees of these factors, $(\deg f_1, \deg f_2, \dots, \deg f_k)$, corresponds to the cycle structure of some permutation in the Galois group $\text{Gal}(f/\mathbb{Q})$.

By factoring a polynomial modulo several different primes, we can "collect" different cycle structures that must be present in the Galois group. This often provides enough information to identify the group uniquely.

Let's apply this to $f(x) = x^3 - x - 1$ [@problem_id:1783763]. This cubic is irreducible over $\mathbb{Q}$. Its discriminant is $\Delta = -23$, which is not a square, so we already suspect the group is $S_3$. Let's confirm this using Dedekind's theorem.
*   **Modulo 2:** $f(x) \equiv x^3 + x + 1 \pmod{2}$. This polynomial has no roots in $\mathbb{F}_2$, so it is irreducible. The factorization gives one irreducible factor of degree 3. This implies that the Galois group contains a 3-cycle.
*   **Modulo 5:** $f(x) \equiv x^3 - x - 1 \pmod{5}$. We find that $f(2) = 8-2-1=5 \equiv 0$, so $(x-2)$ is a factor. Polynomial division yields $x^3 - x - 1 \equiv (x-2)(x^2+2x+3) \pmod{5}$. The quadratic factor is irreducible over $\mathbb{F}_5$. The degrees of the factors are (1, 2). This implies the Galois group contains a permutation with cycle structure (1)(23), which is a 2-cycle ([transposition](@entry_id:155345)).

Since the Galois group is a subgroup of $S_3$ that contains both a 3-cycle and a 2-cycle, it must be $S_3$ itself.

This technique can even provide information about much larger groups. For the polynomial $f(x) = x^5 - x - 1$, its reduction modulo 2 is $x^5+x+1$, which factors in $\mathbb{F}_2[x]$ as $(x^2+x+1)(x^3+x^2+1)$ [@problem_id:1783737]. The degrees of these irreducible factors are (2, 3). By Dedekind's theorem, we can deduce that the Galois group of $f(x)$ over $\mathbb{Q}$ contains a permutation with cycle structure $(ab)(cde)$.

### Group Actions and Intermediate Fields

The Fundamental Theorem of Galois Theory establishes a beautiful correspondence between subgroups of the Galois group and [intermediate fields](@entry_id:153550) of the extension. We can use our understanding of [group actions](@entry_id:268812) to illuminate this connection.

Consider an [irreducible polynomial](@entry_id:156607) $f(x)$ with roots $\{\alpha_1, \dots, \alpha_n\}$ and Galois group $G = \text{Gal}(K/\mathbb{Q})$. The group $G$ acts transitively on the roots. The **stabilizer** of a root $\alpha_i$, denoted $\text{Stab}_G(\alpha_i)$, is the subgroup of automorphisms that fix $\alpha_i$. By the Fundamental Theorem, this subgroup corresponds precisely to the intermediate field $\mathbb{Q}(\alpha_i)$.
$$
\text{Stab}_G(\alpha_i) = \text{Gal}(K/\mathbb{Q}(\alpha_i))
$$
The Orbit-Stabilizer Theorem from group theory states that $|G| = |\text{Orb}_G(\alpha_i)| \cdot |\text{Stab}_G(\alpha_i)|$. Since the action is transitive, the orbit of any root is the entire set of $n$ roots. Thus, the size of the [stabilizer subgroup](@entry_id:137216) is simply $|G|/n$.

Let's return to a cubic with Galois group $S_3$, such as $f(x) = x^3 - 2x + 2$ [@problem_id:1783798]. The group $G \cong S_3$ has order 6, and it acts on 3 roots. The stabilizer of a root $\alpha_1$ is a subgroup of order $|G|/n = 6/3 = 2$. There is only one type of subgroup of order 2 in $S_3$, generated by a transposition. If we label the roots $\alpha_1, \alpha_2, \alpha_3$, the subgroup that fixes $\alpha_1$ must be the one that permutes $\alpha_2$ and $\alpha_3$. In [cycle notation](@entry_id:146599), this is the subgroup $\{e, (23)\}$. This provides a clear, tangible link between the abstract algebraic structure of [field extensions](@entry_id:153187) and the concrete combinatorial nature of [permutation groups](@entry_id:142907).