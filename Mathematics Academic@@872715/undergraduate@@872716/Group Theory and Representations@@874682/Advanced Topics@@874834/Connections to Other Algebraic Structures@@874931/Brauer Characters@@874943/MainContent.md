## Introduction
In the study of finite groups, representation theory over the complex numbers offers a beautifully complete picture, largely thanks to Maschke's Theorem ensuring the decomposability of representations. However, when we shift to a field of [prime characteristic](@entry_id:155979) $p$ that divides the order of the group—the domain of [modular representation theory](@entry_id:147491)—this elegant structure collapses. This article introduces Brauer characters, a profound theoretical tool developed by Richard Brauer to restore much of the power of [character theory](@entry_id:144021) in this more complex setting. We will explore how these characters are constructed, how they relate to the underlying module structure, and how they bridge the gap between modular and ordinary representations. This journey will begin with the foundational "Principles and Mechanisms," where we define Brauer characters and their essential properties. We will then explore their "Applications and Interdisciplinary Connections," showing how they are used to analyze group structure and solve problems. Finally, the "Hands-On Practices" section will provide opportunities to apply these concepts to concrete examples.

## Principles and Mechanisms

The theory of Brauer characters provides a powerful analogue to ordinary [character theory](@entry_id:144021) for studying representations over fields of [prime characteristic](@entry_id:155979). While the failure of Maschke's Theorem in the modular setting—when the characteristic $p$ of the underlying field divides the order of the group $|G|$—complicates the module structure, Brauer characters restore a significant portion of the elegant framework we enjoy in characteristic zero. This chapter elucidates the foundational principles and mechanisms of this theory, from the definition of its domain to its deep connections with module structure and ordinary characters.

### The Domain of Brauer Characters: p-Regular Elements

The first departure from ordinary [character theory](@entry_id:144021) lies in the domain of definition. Whereas ordinary characters are defined on the entire group $G$, Brauer characters are defined only on a specific subset of its elements. This distinction is the cornerstone of the entire theory.

An element $g$ of a finite group $G$ is defined as **$p$-regular** if its order, $\operatorname{ord}(g)$, is not divisible by the prime $p$. Conversely, an element whose order is a multiple of $p$ is termed **$p$-singular**. The set of all $p$-regular elements of $G$ is often denoted by $G_{p'}$.

This classification is not arbitrary; it is precisely the condition $p \nmid \operatorname{ord}(g)$ that guarantees the existence of the tools needed to construct the character value, as we shall see. For now, let us consider how to identify these elements in practice.

For instance, in the [symmetric group](@entry_id:142255) $S_n$, the [order of a permutation](@entry_id:146478) is the [least common multiple](@entry_id:140942) of the lengths of the cycles in its [disjoint cycle decomposition](@entry_id:137482). Consider an element $\sigma \in S_6$ with a [cycle type](@entry_id:136710) of $(4,2)$. Its order is $\operatorname{lcm}(4,2) = 4$. If we are interested in modular representations for the prime $p=3$, we check if $3$ divides the order. Since $3 \nmid 4$, the element $\sigma$ is a $3$-regular element [@problem_id:1601430]. The classification depends only on the order of the element, which is determined by its conjugacy class (and in $S_n$, by its [cycle type](@entry_id:136710)), not on the specific symbols being permuted.

The set of $p$-regular elements forms a union of conjugacy classes, which we call the **$p$-regular [conjugacy classes](@entry_id:143916)**. The Brauer characters are constant on these classes. To illustrate, let us examine the [symmetric group](@entry_id:142255) $G=S_3$ with $p=3$. The order of $S_3$ is $3! = 6$, so this is a modular case. The elements of $S_3$ are the identity $e$ (order 1), the three [transpositions](@entry_id:142115) like $(12)$ (order 2), and the two 3-cycles like $(123)$ (order 3).
- The order of $e$ is $1$. Since $3 \nmid 1$, $e$ is $3$-regular.
- The order of any transposition is $2$. Since $3 \nmid 2$, all transpositions are $3$-regular.
- The order of any $3$-cycle is $3$. Since $3 \mid 3$, the $3$-cycles are $3$-singular.
Therefore, the set of $3$-regular elements in $S_3$ is $\{e, (12), (13), (23)\}$. Any Brauer character for $S_3$ with $p=3$ will be a function defined on this set [@problem_id:1601434].

### The Construction of Brauer Characters

A striking feature of Brauer characters is that although they arise from representations over a field $k$ of characteristic $p$, their values are complex numbers. This is achieved through a beautiful "lifting" process that connects roots of unity in different number systems.

Let $S$ be a finite-dimensional module for the [group algebra](@entry_id:145139) $kG$, where $k$ is a sufficiently large field of characteristic $p$. For any $g \in G$, the action of $g$ on $S$ is a [linear transformation](@entry_id:143080), represented by a matrix $\rho(g)$. If $g$ is a $p$-regular element of order $m$, its eigenvalues $\{\lambda_1, \dots, \lambda_d\}$ are $m$-th roots of unity in the field $k$. Since $p \nmid m$, the polynomial $x^m - 1$ has distinct roots in an [algebraically closed field](@entry_id:151401) of characteristic $p$, allowing us to distinguish them.

The core of the construction is a canonical bijection between the group of $m$-th [roots of unity](@entry_id:142597) in $k$ and the group of $m$-th [roots of unity](@entry_id:142597) in the complex numbers $\mathbb{C}$. We can fix a primitive $m$-th root of unity $\alpha$ in $k$ and a primitive $m$-th root of unity $\zeta = \exp(2\pi i / m)$ in $\mathbb{C}$. The **lift** is a [group isomorphism](@entry_id:147371) that maps $\alpha^j \mapsto \zeta^j$ for any integer $j$.

The **Brauer character** $\phi_S$ of the module $S$ is the function $\phi_S: G_{p'} \to \mathbb{C}$ defined by
$$ \phi_S(g) = \sum_{j=1}^{\dim(S)} \widehat{\lambda_j} $$
where $\lambda_1, \dots, \lambda_{\dim(S)}$ are the eigenvalues of $\rho(g)$ and $\widehat{\lambda_j}$ denotes the lift of $\lambda_j$ to $\mathbb{C}$. The value $\phi_S(g)$ is thus the trace of a "lifted" matrix, analogous to the ordinary character definition.

As an example of this lifting mechanism, suppose we are working in characteristic 2 and consider an element of order 5. The eigenvalues of its [matrix representation](@entry_id:143451) might be $\lambda_1 = \alpha$ and $\lambda_2 = \alpha^4$, where $\alpha$ is a primitive 5th root of unity in our characteristic-2 field. To compute the Brauer character value, we lift these to the complex plane. The lift of $\alpha$ is $\zeta = \exp(2\pi i / 5)$, and the lift of $\alpha^4$ is $\zeta^4$. The contribution to the Brauer character from these two eigenvalues would be the sum of their lifts, $\zeta + \zeta^4$. Using the [cyclotomic polynomial](@entry_id:154273) identity $1 + \zeta + \zeta^2 + \zeta^3 + \zeta^4 = 0$, and noting that $\zeta^4 = \zeta^{-1}$, we can find this value explicitly. Let $s = \zeta + \zeta^4$. Then $\zeta^2 + \zeta^3 = s^2 - 2$. Substituting into the identity gives $1 + s + (s^2 - 2) = 0$, or $s^2 + s - 1 = 0$. The roots are $s = \frac{-1 \pm \sqrt{5}}{2}$. Since $\zeta + \zeta^4 = 2\cos(2\pi/5) > 0$, we must choose the positive root, yielding $\frac{-1 + \sqrt{5}}{2}$ [@problem_id:1601408]. This calculation demonstrates how [algebraic integers](@entry_id:151672) in $\mathbb{C}$ arise naturally as Brauer character values.

### The Space of Brauer Characters

Just as with ordinary characters, we can define irreducible Brauer characters as the characters of the simple (or irreducible) $kG$-modules. These irreducible Brauer characters play a central role, forming a basis for a certain space of functions.

The irreducible Brauer characters are class functions on the set of $p$-regular conjugacy classes. A cornerstone of the theory, established by Richard Brauer, is the following theorem:

**Theorem:** The number of non-isomorphic simple $kG$-modules, and thus the number of irreducible Brauer characters, is equal to the number of $p$-regular [conjugacy classes](@entry_id:143916) of $G$.

For example, for the [alternating group](@entry_id:140499) $A_4$ and prime $p=2$, the element orders for the four [conjugacy classes](@entry_id:143916) are 1, 2, 3, and 3. The $2$-regular classes are those with orders not divisible by 2, namely the class of order 1 and the two classes of order 3. There are three such classes. The theorem thus predicts that there must be exactly three irreducible Brauer characters for $A_4$ at $p=2$ [@problem_id:1601417].

The set of irreducible Brauer characters $\{\phi_1, \dots, \phi_l\}$ forms an [orthonormal basis](@entry_id:147779) for the space of complex-valued class functions on $G_{p'}$, with respect to a suitable inner product. This means any Brauer character $\psi$ (i.e., the character of any $kG$-module, not necessarily simple) can be uniquely expressed as a linear combination of the irreducible ones with non-negative integer coefficients: $\psi = \sum_{j=1}^l a_j \phi_j$.

For example, consider the product of two Brauer characters. This corresponds to the character of the [tensor product](@entry_id:140694) of the underlying modules, and is itself a Brauer character. For $S_3$ at $p=2$, there are two irreducible Brauer characters, $\phi_1$ (trivial) and $\phi_2$, with values $(\phi_1(e), \phi_1((123))) = (1, 1)$ and $(\phi_2(e), \phi_2((123))) = (2, -1)$. If we form the product character $\psi = \phi_2 \cdot \phi_2 = \phi_2^2$, its values are $\psi(e) = 2^2=4$ and $\psi((123)) = (-1)^2=1$. Since $\psi$ is not one of the [irreducible characters](@entry_id:145398), it must be decomposable. We can find its decomposition $\psi = a \phi_1 + b \phi_2$ by solving the system of linear equations:
$a(1) + b(2) = 4$
$a(1) + b(-1) = 1$
Solving this system yields $a=2$ and $b=1$. Thus, $\phi_2^2 = 2\phi_1 + \phi_2$. This illustrates that the product of irreducible Brauer characters is not necessarily irreducible, but it decomposes predictably [@problem_id:1601424].

### The Bridge to Ordinary Characters: The Decomposition Matrix

One of the most profound aspects of [modular representation theory](@entry_id:147491) is its relationship with ordinary (characteristic 0) [representation theory](@entry_id:137998). Brauer characters provide the essential link between these two worlds.

Let $\chi$ be an ordinary [irreducible character](@entry_id:145297) of $G$. We can restrict this function to the set of $p$-regular elements, $G_{p'}$, to obtain a function $\chi|_{G_{p'}}$. This restricted function is still a [class function](@entry_id:146970) on the $p$-regular classes. As such, it must be a unique [linear combination](@entry_id:155091) of the irreducible Brauer characters. A fundamental theorem states that the coefficients in this expansion are non-negative integers.

**Theorem:** For any ordinary [irreducible character](@entry_id:145297) $\chi$, its restriction to $G_{p'}$ can be written as:
$$ \chi|_{G_{p'}} = \sum_{j=1}^{l} d_{\chi\phi_j} \phi_j $$
where $\phi_j$ are the irreducible Brauer characters and $d_{\chi\phi_j} \in \mathbb{Z}_{\ge 0}$.

These integers $d_{\chi\phi_j}$ are known as the **decomposition numbers**. They essentially describe how an ordinary [irreducible representation](@entry_id:142733) "decomposes" when viewed through the lens of modular theory. If we are given the expansion $\chi|_{G_{p'}} = 2\phi_1 + \phi_2$, the uniqueness of this decomposition immediately tells us that the decomposition numbers are $d_{\chi\phi_1} = 2$ and $d_{\chi\phi_2} = 1$ [@problem_id:1601406].

These numbers can be organized into a matrix. If we index the rows by the ordinary irreducible characters $\{\chi_i\}$ and the columns by the irreducible Brauer characters $\{\phi_j\}$, the resulting matrix $D = (d_{\chi_i\phi_j})$ is the **decomposition matrix**. This matrix is a central object of study, encoding the precise relationship between the ordinary and modular representation theories of the group.

For example, consider the group $S_4$ and $p=3$. The $2$-dimensional ordinary [irreducible character](@entry_id:145297) $\chi_2$ has values $(2,0,0,2)$ on the $3$-regular classes represented by $e, (12), (1234), (12)(34)$. The two 1-dimensional irreducible Brauer characters are the trivial character $\phi_1=(1,1,1,1)$ and another character $\phi_{\text{sign}'}=(1,-1,-1,1)$. The restriction $\chi_2|_{G_{3'}}$ can be seen to be the sum $\phi_1 + \phi_{\text{sign}'}$, since $(1+1, 1-1, 1-1, 1+1)=(2,0,0,2)$. This implies that the decomposition numbers for $\chi_2$ with respect to these two Brauer characters are both 1 [@problem_id:1601395].

### Connections to Module Structure

The theory of Brauer characters is deeply intertwined with the structure of $kG$-modules. When the characteristic $p$ divides $|G|$, the [group algebra](@entry_id:145139) $kG$ is not semisimple, leading to the existence of modules that are indecomposable but not simple.

A key class of such modules are the **principal [indecomposable modules](@entry_id:145125) (PIMs)**. These are the indecomposable direct summands of the regular module $kG$. Each PIM has a unique simple top (quotient) and a unique simple socle (submodule). This property establishes a crucial [bijection](@entry_id:138092):

**Theorem:** There is a one-to-one correspondence between the [isomorphism classes](@entry_id:147854) of simple $kG$-modules and the [isomorphism classes](@entry_id:147854) of PIMs.

This immediately implies that the number of non-isomorphic PIMs is equal to the number of [simple modules](@entry_id:137323), which in turn equals the number of irreducible Brauer characters [@problem_id:1601443]. This gives us three equivalent counts for this fundamental invariant of the [group algebra](@entry_id:145139) $kG$:
$$ (\text{Number of irred. Brauer characters}) = (\text{Number of } p\text{-reg. classes}) = (\text{Number of PIMs}) $$

The failure of semisimplicity also means that some classical results from ordinary [character theory](@entry_id:144021) no longer hold. For instance, the sum of the squares of the dimensions of the [irreducible characters](@entry_id:145398) no longer equals the order of the group. For $S_3$ at $p=2$, we found there are two [simple modules](@entry_id:137323): the trivial module of dimension 1 and another simple module of dimension 2. The sum of their dimensions is $1+2=3$ [@problem_id:1601399]. The sum of the squares of their dimensions is $1^2 + 2^2 = 5$, which is not equal to $|S_3|=6$.

To complete the picture, we introduce the **Cartan matrix**, $C$. The entry $c_{ij}$ of the Cartan matrix is defined as the number of times the simple module $S_i$ appears as a composition factor in the PIM $P_j$. This matrix encodes the internal structure of the principal [indecomposable modules](@entry_id:145125).

Remarkably, the Cartan matrix is not independent of the decomposition matrix. They are related by one of the most celebrated formulas in the theory:
$$ C = D^T D $$
where $D^T$ is the transpose of the decomposition matrix $D$. This equation provides a powerful computational bridge. If one can determine the ordinary characters and how they restrict (to find $D$), one can compute the Cartan matrix $C$, which reveals deep information about the structure of [indecomposable modules](@entry_id:145125) in characteristic $p$.

For example, if a hypothetical decomposition matrix for some group and prime is given as
$$ D = \begin{pmatrix} 1  0  0 \\ 0  1  1 \\ 1  1  0 \\ 0  0  2 \end{pmatrix} $$
then the corresponding Cartan matrix can be computed directly as $C = D^T D$:
$$ C = \begin{pmatrix} 1  0  1  0 \\ 0  1  1  0 \\ 0  1  0  2 \end{pmatrix} \begin{pmatrix} 1  0  0 \\ 0  1  1 \\ 1  1  0 \\ 0  0  2 \end{pmatrix} = \begin{pmatrix} 2  1  0 \\ 1  2  1 \\ 0  1  5 \end{pmatrix} $$
The entries of $C$ provide multiplicities of [simple modules](@entry_id:137323) within PIMs, linking the abstract character-level information in $D$ to the concrete module structure [@problem_id:1601407]. This elegant formula encapsulates the profound unity between the ordinary and modular representation theories of finite groups.