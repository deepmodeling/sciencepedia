## Introduction
The invertible elements within the ring of integers of a number field, known as units, form a group whose structure is fundamental to the arithmetic of the field. Understanding this group is a central goal of algebraic number theory. While the celebrated Dirichlet's Unit Theorem provides a beautiful abstract description of this group's structure, it offers no general method for actually constructing the "fundamental units" that generate it. This gap between abstract existence and explicit construction motivates a deeper study of special cases where such a construction is possible.

This article addresses this gap by focusing on the rich and historically crucial setting of [cyclotomic fields](@entry_id:153828). Here, it is possible to explicitly define and construct a special set of units, the [cyclotomic units](@entry_id:184331). As we will see, these explicitly known elements form a subgroup that is "large enough" to reveal profound connections to other deep invariants of the field, most notably its class number.

Across the following chapters, you will embark on a journey from foundational principles to the frontiers of modern research. The first chapter, "Principles and Mechanisms," will introduce Dirichlet's Unit Theorem, the geometric perspective of the [logarithmic embedding](@entry_id:148678), and the construction of [cyclotomic units](@entry_id:184331), culminating in their connection to class numbers. The second chapter, "Applications and Interdisciplinary Connections," will explore how this theory serves as a powerful bridge to analysis through [class number](@entry_id:156164) formulas, and to Galois theory via Iwasawa theory and the Stark conjectures. Finally, the "Hands-On Practices" section will allow you to apply these concepts, guiding you through the computation and analysis of units in specific examples.

## Principles and Mechanisms

This chapter delves into the fundamental principles governing the structure of [units in number fields](@entry_id:182583) and the mechanisms by which they are understood. We begin with the foundational structure theorem of Peter Gustav Lejeune Dirichlet, which provides an abstract description of the [unit group](@entry_id:184012). We then translate this algebraic statement into a geometric picture via the [logarithmic embedding](@entry_id:148678), leading to the concept of the regulator. Subsequently, we focus on the specific and crucial case of [cyclotomic fields](@entry_id:153828), constructing the special subgroup of [cyclotomic units](@entry_id:184331). The significance of these units is revealed through their deep and surprising connection to class numbers, a cornerstone of modern number theory. Finally, we analyze the [unit group](@entry_id:184012) through the lens of representation theory, describing its structure as a Galois module.

### The Structure of the Unit Group: Dirichlet's Unit Theorem

Let $K$ be a number field, and let $\mathcal{O}_K$ be its ring of integers. The set of invertible elements in $\mathcal{O}_K$ forms a multiplicative group, known as the **[unit group](@entry_id:184012)** of $K$, denoted $\mathcal{O}_K^\times$. An element $\alpha \in \mathcal{O}_K$ is a unit if and only if its inverse $\alpha^{-1}$ is also an element of $\mathcal{O}_K$. A key characterization is that an [algebraic integer](@entry_id:155088) $\alpha \in \mathcal{O}_K$ is a unit if and only if its field norm $N_{K/\mathbb{Q}}(\alpha)$ is equal to $\pm 1$.

The structure of this group is one of the classical triumphs of [algebraic number](@entry_id:156710) theory, described by **Dirichlet's Unit Theorem**. This theorem states that $\mathcal{O}_K^\times$ is a [finitely generated abelian group](@entry_id:196575). By the fundamental theorem for such groups, it must be the [direct product](@entry_id:143046) of its [torsion subgroup](@entry_id:139454) and a free [abelian group](@entry_id:139381).

The [torsion subgroup](@entry_id:139454) of $\mathcal{O}_K^\times$ consists of all elements of finite order. In a [number field](@entry_id:148388), the elements of finite [multiplicative order](@entry_id:636522) are precisely the roots of unity contained within the field. We denote this finite, cyclic group by $\mu(K)$.

The rank of the free abelian part is determined by the "archimedean signature" of the field $K$. Let $n = [K:\mathbb{Q}]$ be the degree of the extension. There are $n$ distinct [embeddings](@entry_id:158103) of $K$ into the complex numbers $\mathbb{C}$. Let $r_1$ be the number of these [embeddings](@entry_id:158103) whose image is contained in the real numbers $\mathbb{R}$ (the **real embeddings**), and let $2r_2$ be the number of embeddings whose image is not contained in $\mathbb{R}$ (the **[complex embeddings](@entry_id:189961)**). The [complex embeddings](@entry_id:189961) come in conjugate pairs, so we denote by $r_2$ the number of such pairs. The degree of the field is related to these numbers by the identity $n = r_1 + 2r_2$.

Dirichlet's Unit Theorem provides the precise structure of the [unit group](@entry_id:184012) in terms of these invariants.

**Theorem (Dirichlet's Unit Theorem).** Let $K$ be a [number field](@entry_id:148388) with $r_1$ real embeddings and $r_2$ pairs of [complex embeddings](@entry_id:189961). The [unit group](@entry_id:184012) $\mathcal{O}_K^\times$ is an [abelian group](@entry_id:139381) of the form:
$$
\mathcal{O}_K^\times \cong \mu(K) \times \mathbb{Z}^{r_1 + r_2 - 1}
$$
where $\mu(K)$ is the finite [cyclic group](@entry_id:146728) of [roots of unity](@entry_id:142597) in $K$.

The integer $r = r_1 + r_2 - 1$ is called the **rank** of the [unit group](@entry_id:184012). The theorem asserts that, apart from the roots of unity, every unit can be uniquely expressed as a product of powers of $r$ multiplicatively independent units, called a **system of fundamental units**. For example, for a real [quadratic field](@entry_id:636261) $K = \mathbb{Q}(\sqrt{d})$ with $d>0$, we have $r_1=2, r_2=0$, so the rank is $2+0-1=1$. Its [unit group](@entry_id:184012) is $\mathcal{O}_K^\times \cong \{\pm 1\} \times \mathbb{Z}$, generated by $-1$ and a single [fundamental unit](@entry_id:180485). For an [imaginary quadratic field](@entry_id:203833) $K = \mathbb{Q}(\sqrt{d})$ with $d0$, we have $r_1=0, r_2=1$, so the rank is $0+1-1=0$. In this case, the [unit group](@entry_id:184012) is finite and consists only of the roots of unity in $K$. [@problem_id:3030596]

### The Logarithmic Embedding and the Regulator

The proof of Dirichlet's theorem and a deeper understanding of its meaning come from translating the multiplicative structure of $\mathcal{O}_K^\times$ into an additive structure in a real vector space. This is achieved via the **[logarithmic embedding](@entry_id:148678)**.

Let the real [embeddings](@entry_id:158103) of $K$ be $\sigma_1, \dots, \sigma_{r_1}$, and let us choose one embedding, $\tau_j$, from each of the $r_2$ conjugate pairs of [complex embeddings](@entry_id:189961), giving us $\tau_1, \dots, \tau_{r_2}$. We define the [logarithmic map](@entry_id:637227) $L: \mathcal{O}_K^\times \to \mathbb{R}^{r_1+r_2}$ as follows:
$$
L(u) = \left( \log|\sigma_1(u)|, \dots, \log|\sigma_{r_1}(u)|, 2\log|\tau_1(u)|, \dots, 2\log|\tau_{r_2}(u)| \right)
$$
The map $L$ is a [group homomorphism](@entry_id:140603) from the [multiplicative group](@entry_id:155975) $\mathcal{O}_K^\times$ to the [additive group](@entry_id:151801) $\mathbb{R}^{r_1+r_2}$. [@problem_id:3030626] [@problem_id:3030597]

The kernel of this map consists of units $u$ for which $|\sigma(u)| = 1$ for all embeddings $\sigma: K \hookrightarrow \mathbb{C}$. A celebrated theorem by Leopold Kronecker states that an [algebraic integer](@entry_id:155088) with this property must be a root of unity. Therefore, the kernel of the [logarithmic map](@entry_id:637227) is precisely the [torsion subgroup](@entry_id:139454):
$$
\ker(L) = \mu(K)
$$
This neatly separates the torsion part from the free part of the [unit group](@entry_id:184012). [@problem_id:3030626]

The image of $L$ is constrained by the norm condition on units. For any unit $u \in \mathcal{O}_K^\times$, we have $|N_{K/\mathbb{Q}}(u)|=1$. The norm is the product of all conjugates, so taking the logarithm gives:
$$
\log|N_{K/\mathbb{Q}}(u)| = \sum_{i=1}^{r_1} \log|\sigma_i(u)| + \sum_{j=1}^{r_2} \left( \log|\tau_j(u)| + \log|\overline{\tau_j(u)}| \right) = 0
$$
Since $|\overline{\tau_j(u)}| = |\tau_j(u)|$, this becomes $\sum_{i=1}^{r_1} \log|\sigma_i(u)| + \sum_{j=1}^{r_2} 2\log|\tau_j(u)| = 0$. This shows that the vector $L(u)$ lies in the [hyperplane](@entry_id:636937) $H \subset \mathbb{R}^{r_1+r_2}$ defined by the equation $\sum_{k=1}^{r_1+r_2} x_k = 0$. This [hyperplane](@entry_id:636937) has dimension $r_1+r_2-1$.

Dirichlet's theorem can now be stated in this geometric language: the image $L(\mathcal{O}_K^\times)$ is a **full-rank lattice** in the [hyperplane](@entry_id:636937) $H$. A lattice is a discrete subgroup that spans the vector space over $\mathbb{R}$. The rank of this lattice is the dimension of the space it spans, which is $r_1+r_2-1$. [@problem_id:3030597]

The [covolume](@entry_id:186549) of this lattice, which is the volume of a fundamental parallelotope of $H/L(\mathcal{O}_K^\times)$ with respect to the standard Euclidean measure on $H$, is a fundamental invariant of the [number field](@entry_id:148388) $K$. This volume is called the **regulator** of $K$, denoted $R_K$. If $\varepsilon_1, \dots, \varepsilon_r$ is a system of [fundamental units](@entry_id:148878) (a $\mathbb{Z}$-basis for the free part $\mathcal{O}_K^\times / \mu(K)$), then their images $L(\varepsilon_1), \dots, L(\varepsilon_r)$ form a basis for the lattice. The regulator is the absolute value of the determinant of the matrix formed by these vectors, after deleting one column to account for the projection onto the $(r-1)$-dimensional hyperplane $H$.

The regulator is an intrinsic invariant of the field. A different choice of fundamental units, say $\varepsilon'_1, \dots, \varepsilon'_r$, corresponds to a change of basis for the free [abelian group](@entry_id:139381) $\mathcal{O}_K^\times / \mu(K)$. Any such change of basis is described by an [integer matrix](@entry_id:151642) $U \in \mathrm{GL}_r(\mathbb{Z})$. The defining property of this group is that the determinant of any such matrix is $\det(U) = \pm 1$. Geometrically, a [change of basis](@entry_id:145142) of a lattice by a matrix $U$ multiplies its [covolume](@entry_id:186549) by $|\det(U)|$. Since $|\det(U)|=1$, the [covolume](@entry_id:186549) $R_K$ is independent of the choice of [fundamental units](@entry_id:148878). [@problem_id:3030610]

### Generalization to S-Units

The framework of Dirichlet's theorem can be elegantly extended to a more general class of units. Let $S$ be a finite set of places of $K$ that contains the set $S_\infty$ of all archimedean places. Let $S_f = S \setminus S_\infty$ be the set of finite (non-archimedean) places in $S$. The **ring of S-integers** is defined as:
$$
\mathcal{O}_{K,S} = \{x \in K \mid v_\mathfrak{p}(x) \ge 0 \text{ for all prime ideals } \mathfrak{p} \text{ corresponding to places not in } S_f\}
$$
In other words, S-integers are allowed to have denominators, but only at the primes corresponding to the finite places in $S$. The group of units of this ring, $\mathcal{O}_{K,S}^\times$, is called the **group of S-units**. An element $x \in K^\times$ is an S-unit if its valuation $v_\mathfrak{p}(x)$ is zero for all finite places $\mathfrak{p}$ outside of $S$. The classical units $\mathcal{O}_K^\times$ form a subgroup of $\mathcal{O}_{K,S}^\times$.

**Dirichlet's S-Unit Theorem** describes the structure of this larger group. It states that $\mathcal{O}_{K,S}^\times$ is also a [finitely generated abelian group](@entry_id:196575), whose torsion part is $\mu(K)$. Its rank is given by:
$$
\text{rank}(\mathcal{O}_{K,S}^\times) = |S| - 1
$$
Since $|S| = |S_\infty| + |S_f| = (r_1+r_2) + |S_f|$, the rank is $r_1+r_2-1+|S_f|$. This formula shows that each finite place added to the set $S$ increases the [rank of the unit group](@entry_id:636706) by one. The classical Dirichlet's Unit Theorem is the special case where $S=S_\infty$, so $S_f$ is empty and $|S_f|=0$, yielding the rank $r_1+r_2-1$. [@problem_id:3030606]

### Cyclotomic Fields and Their Units

We now turn our attention to a particularly important class of number fields: [cyclotomic fields](@entry_id:153828). Let $n \ge 3$ be an integer and let $\zeta_n$ be a primitive $n$-th root of unity. The **$n$-th cyclotomic field** is $K = \mathbb{Q}(\zeta_n)$. These fields are central to number theory for many reasons, including their role in the study of Fermat's Last Theorem and [class field theory](@entry_id:155687).

The fundamental properties of $K = \mathbb{Q}(\zeta_n)$ are well-understood. [@problem_id:3030583]
- The [minimal polynomial](@entry_id:153598) of $\zeta_n$ over $\mathbb{Q}$ is the $n$-th [cyclotomic polynomial](@entry_id:154273) $\Phi_n(x)$.
- The degree of the extension is $[K:\mathbb{Q}] = \deg(\Phi_n(x)) = \varphi(n)$, where $\varphi$ is Euler's totient function.
- The extension $K/\mathbb{Q}$ is a Galois extension, and its Galois group is canonically isomorphic to the group of multiplicative units modulo $n$:
$$
\mathrm{Gal}(K/\mathbb{Q}) \cong (\mathbb{Z}/n\mathbb{Z})^\times
$$
The isomorphism is given by mapping an integer $a$ (with $\gcd(a,n)=1$) to the [automorphism](@entry_id:143521) $\sigma_a$ defined by $\sigma_a(\zeta_n) = \zeta_n^a$. Since $(\mathbb{Z}/n\mathbb{Z})^\times$ is an [abelian group](@entry_id:139381), all [cyclotomic fields](@entry_id:153828) are [abelian extensions](@entry_id:152984) of $\mathbb{Q}$.
- The ring of integers is $\mathcal{O}_K = \mathbb{Z}[\zeta_n]$.
- For $n \ge 3$, $K$ is a totally imaginary field, so $r_1=0$ and $r_2 = \varphi(n)/2$. By Dirichlet's theorem, the [rank of the unit group](@entry_id:636706) $\mathcal{O}_K^\times$ is $\frac{\varphi(n)}{2}-1$.

The Galois group $\mathrm{Gal}(K/\mathbb{Q})$ acts on all objects associated with the field, including its ideals and units. This action is functorial; for an ideal $I$, $\sigma_a(I) = \{\sigma_a(x) \mid x \in I\}$, and for a unit $u$, the action is simply the application of the [automorphism](@entry_id:143521) $\sigma_a(u)$. A key property is that Galois conjugation preserves the [norm of an ideal](@entry_id:155476), i.e., $N_{K/\mathbb{Q}}(\sigma_a(I)) = N_{K/\mathbb{Q}}(I)$. [@problem_id:3030623]

### Cyclotomic Units: Construction and Properties

While Dirichlet's theorem guarantees the existence of [fundamental units](@entry_id:148878), it does not provide a way to construct them. For [cyclotomic fields](@entry_id:153828), however, a special subgroup of units can be constructed explicitly. These are the **[cyclotomic units](@entry_id:184331)**.

A natural source of [algebraic integers](@entry_id:151672) in $\mathbb{Q}(\zeta_n)$ are elements of the form $1-\zeta_n^k$. Let's consider the norm of $1-\zeta_n$.
$$
N_{K/\mathbb{Q}}(1-\zeta_n) = \prod_{a \in (\mathbb{Z}/n\mathbb{Z})^\times} \sigma_a(1-\zeta_n) = \prod_{a \in (\mathbb{Z}/n\mathbb{Z})^\times} (1-\zeta_n^a) = \Phi_n(1)
$$
A known result states that $\Phi_n(1)=p$ if $n=p^k$ is a prime power, and $\Phi_n(1)=1$ if $n$ has at least two distinct prime factors. Since an element is a unit if and only if its norm is $\pm 1$, we see that $1-\zeta_n$ is a unit if and only if $n$ is not a prime power. [@problem_id:3030583] [@problem_id:3030623]

To construct elements that are always units, we consider ratios. For any integer $a$ with $\gcd(a,n)=1$, define the element
$$
u_a = \frac{1-\zeta_n^a}{1-\zeta_n}
$$
We can show that $u_a$ is always a unit in $\mathcal{O}_K$.
First, $u_a$ is an [algebraic integer](@entry_id:155088). Using the formula for a geometric sum, we have $u_a = 1 + \zeta_n + \dots + \zeta_n^{a-1}$. Since $\zeta_n$ is in $\mathcal{O}_K = \mathbb{Z}[\zeta_n]$, this sum is also in $\mathcal{O}_K$.
Second, we compute its norm. Since the norm is a homomorphism,
$$
N_{K/\mathbb{Q}}(u_a) = \frac{N_{K/\mathbb{Q}}(1-\zeta_n^a)}{N_{K/\mathbb{Q}}(1-\zeta_n)}
$$
The Galois conjugates of $1-\zeta_n^a$ are the elements $1-\sigma_b(\zeta_n^a) = 1-\zeta_n^{ab}$ for $b \in (\mathbb{Z}/n\mathbb{Z})^\times$. As $b$ runs through $(\mathbb{Z}/n\mathbb{Z})^\times$, so does the product $ab$ (since $a$ is invertible). Thus, the set of conjugates of $1-\zeta_n^a$ is the same as the set of conjugates of $1-\zeta_n$. This implies their norms are equal: $N_{K/\mathbb{Q}}(1-\zeta_n^a) = N_{K/\mathbb{Q}}(1-\zeta_n)$. Therefore, $N_{K/\mathbb{Q}}(u_a) = 1$. As $u_a$ is an [algebraic integer](@entry_id:155088) with norm 1, it is a unit. [@problem_id:3030599]

The **group of [cyclotomic units](@entry_id:184331)**, denoted $C(K)$, is defined as the subgroup of $\mathcal{O}_K^\times$ generated by $-1$, $\zeta_n$, and all the units $u_a$ for $a$ coprime to $n$. [@problem_id:3030598]

### The Significance of Cyclotomic Units

The profound importance of [cyclotomic units](@entry_id:184331) stems from the fact that they constitute a "large" part of the full [unit group](@entry_id:184012). More precisely, it can be shown that the group $C(K)$ has the same rank as $\mathcal{O}_K^\times$, which implies that it is a subgroup of **finite index**.

The relationship becomes most transparent when we consider the **maximal real [subfield](@entry_id:155812)** $K^+ = \mathbb{Q}(\zeta_n + \zeta_n^{-1})$. This is a totally real field of degree $\varphi(n)/2$. Let $E^+ = \mathcal{O}_{K^+}^\times$ be its [unit group](@entry_id:184012) and let $C^+ = C(K) \cap E^+$ be the subgroup of real [cyclotomic units](@entry_id:184331). The ranks of $E^+$ and $C^+$ are both $\frac{\varphi(n)}{2}-1$. The index of $C^+$ in $E^+$ connects the explicitly constructed units to a deep arithmetic invariant of the field: its [class number](@entry_id:156164).

Let $h^+$ be the [class number](@entry_id:156164) of the real subfield $K^+$. A celebrated theorem, derived from the [analytic class number formula](@entry_id:184272), gives the following index formula:
$$
[E^+ : C^+] = h^+
$$
This remarkable equality holds whenever $n$ is a prime power ($p^k$) or twice an odd prime power ($2p^k$). For other values of $n$, the formula is slightly modified by a [power of 2](@entry_id:150972):
$$
[E^+ : C^+] = 2^a h^+
$$
for some integer $a \ge 0$, where $a=0$ precisely in the cases mentioned above. This formula provides a stunning link between analytic objects (special values of L-functions, which enter through the regulator) and [algebraic structures](@entry_id:139459) (units and the [class group](@entry_id:204725)). It suggests that the "missing" part of the [unit group](@entry_id:184012), measured by the index $[E^+:C^+]$, is accounted for by the complexity of the ideal class group, measured by $h^+$. [@problem_id:3030598]

### The Galois Module Structure of Units

The action of the Galois group $G = \mathrm{Gal}(K/\mathbb{Q})$ endows the [unit group](@entry_id:184012) with additional structure, making it a $\mathbb{Z}[G]$-module. To analyze this structure, it is convenient to extend scalars and study the $\mathbb{Q}$-vector space $V = \mathcal{O}_K^\times \otimes_\mathbb{Z} \mathbb{Q}$. Tensoring with $\mathbb{Q}$ eliminates the torsion part $\mu(K)$, so $V$ is a $\mathbb{Q}$-vector space of dimension equal to the [rank of the unit group](@entry_id:636706), $\dim_\mathbb{Q}(V) = \frac{\varphi(n)}{2}-1$.

The structure of $V$ as a $\mathbb{Q}[G]$-module can be made explicit. The element $-1 \in (\mathbb{Z}/n\mathbb{Z})^\times$ corresponds to the [automorphism](@entry_id:143521) $\sigma_{-1}$, which is [complex conjugation](@entry_id:174690). The [logarithmic embedding](@entry_id:148678) shows that the images of all units are "real", in the sense that they are fixed by [complex conjugation](@entry_id:174690). This implies that $\sigma_{-1}$ acts trivially on $V$. Consequently, $V$ is a module over the quotient algebra $\mathbb{Q}[G/\langle-1\rangle]$. A more precise analysis shows that $V$ is isomorphic to the [augmentation ideal](@entry_id:142847) of this quotient algebra:
$$
\mathcal{O}_K^\times \otimes_\mathbb{Z} \mathbb{Q} \cong I_{\mathbb{Q}[G/\langle-1\rangle]}
$$
[@problem_id:3030616]

This algebraic structure becomes even clearer when analyzed using [character theory](@entry_id:144021). Since $G$ is abelian, its irreducible representations over $\mathbb{C}$ are one-dimensional and are given by the Dirichlet characters modulo $n$. The complexified module $V \otimes_\mathbb{Q} \mathbb{C}$ decomposes into a [direct sum](@entry_id:156782) of these one-dimensional representations. The condition that [complex conjugation](@entry_id:174690) acts trivially means that only characters $\chi$ with $\chi(-1)=1$ can appear. These are called **even characters**. The fact that we are looking at the [augmentation ideal](@entry_id:142847) means the trivial character does not appear. Putting this together, we find that the [unit group](@entry_id:184012) module decomposes as:
$$
\mathcal{O}_K^\times \otimes_\mathbb{Z} \mathbb{C} \cong \bigoplus_{\substack{\chi \text{ even} \\ \chi \neq \mathbf{1}}} V_\chi
$$
where $V_\chi$ is the [one-dimensional representation](@entry_id:136509) corresponding to the character $\chi$. This decomposition is fundamental in modern number theory, particularly in the context of the Stark conjectures and Iwasawa theory, where it provides a bridge between the arithmetic of units and the analytic properties of L-functions associated with these characters. [@problem_id:3030616]