## Introduction
In the vast landscape of number theory, the study of [modular forms](@entry_id:160014) stands as a central pillar connecting analysis, algebra, and geometry. The natural domain for these powerful functions is not the entire [modular group](@entry_id:146452) SL₂(ℤ), but rather a specific class of its subgroups known as **[congruence subgroups](@entry_id:195720)**. While the full [modular group](@entry_id:146452) offers a starting point, its rigid structure can be restrictive. By considering subgroups defined by arithmetic conditions—specifically, [congruences](@entry_id:273198) on matrix entries—a far richer and more nuanced theory unfolds, one that is capable of capturing deep arithmetic information. This article addresses the fundamental principles and profound applications of these essential mathematical objects.

Over the following chapters, you will embark on a journey into the world of [congruence subgroups](@entry_id:195720).
-   First, **Principles and Mechanisms** will lay the groundwork, formally defining the primary families Γ(N), Γ₁(N), and Γ₀(N). We will explore their algebraic structure, normality properties, and interrelations using the powerful tool of the reduction homomorphism, and touch upon the modern adelic framework that unifies them.
-   Next, **Applications and Interdisciplinary Connections** will reveal their significance beyond pure group theory. We will see how they give rise to geometric objects called [modular curves](@entry_id:199342), function as [moduli spaces](@entry_id:159780) for [elliptic curves](@entry_id:152409), and provide the setting for the arithmetic theory of modular forms, culminating in the celebrated Modularity Theorem.
-   Finally, **Hands-On Practices** will offer an opportunity to solidify these concepts through guided problems, connecting abstract theory to concrete computation and deepening your understanding of their structure and geometric implications.

## Principles and Mechanisms

The study of modular forms is inextricably linked to the discrete subgroups of the [modular group](@entry_id:146452), $\mathrm{SL}_2(\mathbb{Z})$. While the full [modular group](@entry_id:146452) is of paramount importance, its structure is in some respects too rigid. A richer and more intricate theory emerges when one considers specific families of its subgroups, known as **[congruence subgroups](@entry_id:195720)**. These subgroups are defined by imposing [congruence](@entry_id:194418) conditions on the entries of the matrices. This chapter elucidates the definitions, structural properties, and interrelations of the most fundamental of these subgroups.

### Defining the Congruence Subgroups

Let $N$ be a positive integer, which we will refer to as the **level**. The three primary families of [congruence subgroups](@entry_id:195720) of $\mathrm{SL}_2(\mathbb{Z})$ are defined as follows:

1.  The **principal congruence subgroup of level $N$**, denoted $\Gamma(N)$, is the set of matrices in $\mathrm{SL}_2(\mathbb{Z})$ that are congruent to the identity matrix $I$ modulo $N$. Formally:
    $$
    \Gamma(N) = \left\{ \begin{pmatrix} a & b \\ c & d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}) : a \equiv d \equiv 1 \pmod{N}, \ b \equiv c \equiv 0 \pmod{N} \right\}.
    $$

2.  The **Hecke [congruence](@entry_id:194418) subgroup $\Gamma_0(N)$** is defined by a condition on a single entry. It consists of matrices whose lower-left entry is a multiple of $N$:
    $$
    \Gamma_0(N) = \left\{ \begin{pmatrix} a & b \\ c & d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}) : c \equiv 0 \pmod{N} \right\}.
    $$

3.  The **Hecke congruence subgroup $\Gamma_1(N)$** sits between $\Gamma(N)$ and $\Gamma_0(N)$. It requires the matrix to be upper-triangular and unipotent modulo $N$:
    $$
    \Gamma_1(N) = \left\{ \begin{pmatrix} a & b \\ c & d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}) : a \equiv d \equiv 1 \pmod{N}, \ c \equiv 0 \pmod{N} \right\}.
    $$
    An equivalent and often useful characterization is that $A \in \Gamma_1(N)$ if and only if $A \equiv \begin{pmatrix} 1 & * \\ 0 & 1 \end{pmatrix} \pmod N$, where the asterisk denotes an arbitrary residue class modulo $N$ [@problem_id:3010521].

### The Reduction Modulo N and Group Structure

A powerful tool for understanding these subgroups is the **reduction homomorphism** $\rho_N$, which maps a matrix in $\mathrm{SL}_2(\mathbb{Z})$ to its reduction modulo $N$ in the group $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$:
$$
\rho_N : \mathrm{SL}_2(\mathbb{Z}) \longrightarrow \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z}), \quad \begin{pmatrix} a & b \\ c & d \end{pmatrix} \mapsto \begin{pmatrix} a \pmod N & b \pmod N \\ c \pmod N & d \pmod N \end{pmatrix}.
$$
This map is well-defined because the determinant condition $ad-bc=1$ in $\mathbb{Z}$ implies that the determinant of the reduced matrix is $1 \pmod N$.

#### The Principal Congruence Subgroup as a Kernel

The definition of $\Gamma(N)$ can be rephrased elegantly using the reduction homomorphism. A matrix $A \in \mathrm{SL}_2(\mathbb{Z})$ is in $\Gamma(N)$ if and only if it is congruent to the identity matrix modulo $N$. This is equivalent to saying that its image under $\rho_N$ is the identity matrix in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$. Therefore, $\Gamma(N)$ is precisely the kernel of the reduction homomorphism $\rho_N$ [@problem_id:3010521] [@problem_id:3010548]:
$$
\Gamma(N) = \ker(\rho_N).
$$
This observation immediately implies that $\Gamma(N)$ is a normal subgroup of $\mathrm{SL}_2(\mathbb{Z})$ for any $N \geq 1$.

#### The Role of Strong Approximation

A fundamental result, known as the **Strong Approximation Theorem for $\mathrm{SL}_2$**, states that the reduction homomorphism $\rho_N$ is surjective for every integer $N \geq 1$ [@problem_id:3010548]. This theorem has profound consequences. It means that any matrix in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ can be "lifted" to a matrix in $\mathrm{SL}_2(\mathbb{Z})$.

By the First Isomorphism Theorem for groups, this [surjectivity](@entry_id:148931) provides a [canonical isomorphism](@entry_id:202335):
$$
\mathrm{SL}_2(\mathbb{Z}) / \Gamma(N) \cong \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z}).
$$
Furthermore, the [surjectivity](@entry_id:148931) of $\rho_N$ establishes a deep connection between subgroups of $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ and a class of subgroups of $\mathrm{SL}_2(\mathbb{Z})$. Specifically, the **Correspondence Theorem** implies a [bijection](@entry_id:138092) between the subgroups of $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ and the subgroups of $\mathrm{SL}_2(\mathbb{Z})$ that contain $\Gamma(N)$. For any subgroup $H \le \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$, its [preimage](@entry_id:150899) $\Gamma_H = \rho_N^{-1}(H)$ is a subgroup of $\mathrm{SL}_2(\mathbb{Z})$ containing $\Gamma(N)$, and importantly, $\rho_N(\Gamma_H) = H$. Any subgroup of $\mathrm{SL}_2(\mathbb{Z})$ that contains some $\Gamma(M)$ is, by definition, a **congruence subgroup**. Thus, every subgroup of the [finite group](@entry_id:151756) $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ can be realized as the image of a [congruence](@entry_id:194418) subgroup of level dividing $N$ [@problem_id:3010522].

#### Images of $\Gamma_0(N)$ and $\Gamma_1(N)$

The subgroups $\Gamma_0(N)$ and $\Gamma_1(N)$ also have natural interpretations in terms of the reduction map.

An element of $\Gamma_0(N)$ has its lower-left entry $c \equiv 0 \pmod N$. Its image under $\rho_N$ is therefore an [upper-triangular matrix](@entry_id:150931). The [surjectivity](@entry_id:148931) of $\rho_N$ ensures that every [upper-triangular matrix](@entry_id:150931) in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ can be realized as the image of some element of $\Gamma_0(N)$. Thus, the image of $\Gamma_0(N)$ is precisely the subgroup of upper-[triangular matrices](@entry_id:149740) in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$, often called a **Borel subgroup** [@problem_id:3010541] [@problem_id:3010532].
$$
\rho_N(\Gamma_0(N)) = \left\{ \begin{pmatrix} \alpha & \beta \\ 0 & \delta \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z}) \right\}.
$$

Similarly, an element of $\Gamma_1(N)$ satisfies $a \equiv d \equiv 1 \pmod N$ and $c \equiv 0 \pmod N$. Its image under $\rho_N$ is a **unipotent** [upper-triangular matrix](@entry_id:150931). Again, it can be shown that this map is surjective onto its image.
$$
\rho_N(\Gamma_1(N)) = \left\{ \begin{pmatrix} 1 & \beta \\ 0 & 1 \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z}) \right\}.
$$

### The Hierarchy of Congruence Subgroups

#### Inclusion Relations and Normality

The definitions immediately imply a chain of inclusions for any $N \geq 1$ [@problem_id:3010521] [@problem_id:3023962]:
$$
\Gamma(N) \subset \Gamma_1(N) \subset \Gamma_0(N) \subset \mathrm{SL}_2(\mathbb{Z}).
$$
An element in $\Gamma(N)$ satisfies all conditions for $\Gamma_1(N)$, and an element in $\Gamma_1(N)$ satisfies the condition for $\Gamma_0(N)$. These inclusions are strict for $N > 2$.

The structural relationships extend to normality.
-   As the [kernel of a homomorphism](@entry_id:145895), $\Gamma(N)$ is normal in $\mathrm{SL}_2(\mathbb{Z})$.
-   The image of $\Gamma_1(N)$ in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ is the group of unipotent matrices, which is a [normal subgroup](@entry_id:144438) of the Borel (upper-triangular) subgroup. This implies that $\Gamma_1(N)$ is a [normal subgroup](@entry_id:144438) of $\Gamma_0(N)$ [@problem_id:3010521].
-   However, $\Gamma_0(N)$ is generally **not** a [normal subgroup](@entry_id:144438) of $\mathrm{SL}_2(\mathbb{Z})$ for $N>1$. For example, conjugating an [upper-triangular matrix](@entry_id:150931) in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ by the Weyl element $w = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$ typically results in a [lower-triangular matrix](@entry_id:634254), showing that the Borel subgroup is not normal. Since the image $\rho_N(\Gamma_0(N))$ is not normal, its full preimage $\Gamma_0(N)$ cannot be normal [@problem_id:3010521].

#### Index Computations

The indices of these subgroups, which measure their relative sizes, are of fundamental importance. They can be computed by analyzing their images in the [finite group](@entry_id:151756) $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$.

-   **Index of $\Gamma(N)$**: From the [isomorphism](@entry_id:137127) $\mathrm{SL}_2(\mathbb{Z})/\Gamma(N) \cong \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$, the index is simply the order of this [finite group](@entry_id:151756):
    $$
    [\mathrm{SL}_2(\mathbb{Z}) : \Gamma(N)] = |\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})| = N^3 \prod_{p|N} \left(1 - \frac{1}{p^2}\right),
    $$
    where the product is over the distinct prime divisors of $N$ [@problem_id:3023962]. For a prime $p$, this simplifies to $|\mathrm{SL}_2(\mathbb{F}_p)| = (p^2-1)(p^2-p)/(p-1) = p^3-p$ [@problem_id:3010521].

-   **Indices of $\Gamma_1(N)$ and $\Gamma_0(N)$**: The indices of intermediate subgroups can be found using the Tower Law. First, we compute the orders of their images [@problem_id:3010532].
    -   The size of $\rho_N(\Gamma_1(N))$ (unipotent matrices) is $N$, as the entry $\beta$ can be any of the $N$ residues.
    -   The size of $\rho_N(\Gamma_0(N))$ (Borel subgroup) is $N\varphi(N)$, where $\varphi$ is Euler's totient function. This is because there are $\varphi(N)$ choices for the invertible entry $\alpha$, which then determines $\delta=\alpha^{-1}$, and $N$ choices for $\beta$.
    
    Using the [isomorphism theorems](@entry_id:145702), we find the indices of the quotients:
    $$
    [\Gamma_1(N) : \Gamma(N)] = |\rho_N(\Gamma_1(N))| = N.
    $$
    $$
    [\Gamma_0(N) : \Gamma_1(N)] = \frac{|\rho_N(\Gamma_0(N))|}{|\rho_N(\Gamma_1(N))|} = \frac{N\varphi(N)}{N} = \varphi(N).
    $$
    For a prime $p$, these become $[\Gamma_1(p) : \Gamma(p)] = p$ and $[\Gamma_0(p) : \Gamma_1(p)] = p-1$ [@problem_id:3010521].

    Finally, the index of $\Gamma_0(N)$ in $\mathrm{SL}_2(\mathbb{Z})$ can be computed by considering the action on the projective line over $\mathbb{Z}/N\mathbb{Z}$. The set of left [cosets](@entry_id:147145) $\mathrm{SL}_2(\mathbb{Z})/\Gamma_0(N)$ is in bijection with the set of points on $\mathbb{P}^1(\mathbb{Z}/N\mathbb{Z})$. The size of this set is given by:
    $$
    [\mathrm{SL}_2(\mathbb{Z}) : \Gamma_0(N)] = |\mathbb{P}^1(\mathbb{Z}/N\mathbb{Z})| = N \prod_{p|N} \left(1 + \frac{1}{p}\right).
    $$
    This formula elegantly captures the geometric nature of $\Gamma_0(N)$ [@problem_id:3023962].

### Geometric Manifestations

The abstract group theory of [congruence subgroups](@entry_id:195720) is realized through their geometric action on the complex upper half-plane $\mathbb{H} = \{z \in \mathbb{C} : \mathrm{Im}(z) > 0 \}$.

#### Action on the Upper Half-Plane: Cusps

The group $\mathrm{SL}_2(\mathbb{Z})$ acts on $\mathbb{H} \cup \mathbb{Q} \cup \{\infty\}$ via fractional [linear transformations](@entry_id:149133). The points in $\mathbb{Q} \cup \{\infty\}$ are known as **cusps**. The stabilizer of the cusp at infinity, $\infty$, is the subgroup of translations, generated by the matrix $T = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$. For any congruence subgroup $\Gamma$, the stabilizer of $\infty$ within $\Gamma$ is generated by some power $T^h$, where $h$ is the smallest positive integer for which $T^h \in \Gamma$. This integer $h$ is called the **width of the cusp** at $\infty$.

-   For $\Gamma_0(N)$ and $\Gamma_1(N)$, the matrix $T$ itself satisfies the defining conditions ($c=0$ and $a=d=1$). Thus, for these groups, the stabilizer of $\infty$ is generated by $T$, and the cusp width is $h=1$ [@problem_id:3023962].
-   For $\Gamma(N)$, the condition $b \equiv 0 \pmod N$ is also required. Since $T$ has $b=1$, $T$ is not in $\Gamma(N)$ for $N>1$. However, $T^N = \begin{pmatrix} 1 & N \\ 0 & 1 \end{pmatrix}$ is in $\Gamma(N)$. The cusp width at $\infty$ for $\Gamma(N)$ is therefore $h=N$ [@problem_id:3023962].

#### Torsion Elements and Elliptic Points

Points in $\mathbb{H}$ with non-trivial finite stabilizers are called **[elliptic points](@entry_id:273590)**. Their existence corresponds to the presence of elements of finite order ([torsion elements](@entry_id:148301)) in the acting group. An important question for applications is whether a congruence subgroup is **torsion-free**.

The only non-trivial element in the center of $\mathrm{SL}_2(\mathbb{Z})$ is $-I = \begin{pmatrix} -1 & 0 \\ 0 & -1 \end{pmatrix}$. We can determine when this central element belongs to a [congruence](@entry_id:194418) subgroup.
-   For $-I$ to be in $\Gamma_1(N)$ or $\Gamma(N)$, its diagonal entries must satisfy $-1 \equiv 1 \pmod N$. This is equivalent to $N$ dividing $2$. Thus, $-I$ belongs to $\Gamma_1(N)$ and $\Gamma(N)$ if and only if $N=1$ or $N=2$ [@problem_id:3010529].
-   The projection from $\mathrm{SL}_2(\mathbb{Z})$ to $\mathrm{PSL}_2(\mathbb{Z}) = \mathrm{SL}_2(\mathbb{Z}) / \{\pm I\}$ is injective when restricted to a subgroup $\Gamma$ if and only if $-I \notin \Gamma$. Therefore, the projections from $\Gamma_1(N)$ and $\Gamma(N)$ are injective for all $N>2$.

More generally, one can show:
-   $\Gamma(N)$ is torsion-free for all $N \geq 3$.
-   $\Gamma_1(N)$ is torsion-free for all $N \geq 4$.
-   $\Gamma_0(N)$ may contain elliptic elements of orders 2 and 3 for many values of $N$ [@problem_id:3023962].

The absence of torsion is a highly desirable property, as it implies the [quotient space](@entry_id:148218) $\Gamma \backslash \mathbb{H}$ is a smooth Riemann surface, simplifying many analytic and geometric arguments.

#### A Lattice-Theoretic View of $\Gamma_0(N)$

The definition of $\Gamma_0(N)$ has a profound geometric interpretation related to its action on the lattice $\Lambda = \mathbb{Z}^2$. An element $M \in \mathrm{SL}_2(\mathbb{Z})$ acts on column vectors in $\Lambda$. The condition $c \equiv 0 \pmod N$ for $M = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$ is precisely the condition that $M$ stabilizes the "horizontal" [cyclic subgroup](@entry_id:138079) $\langle (1,0) \rangle$ within the [quotient module](@entry_id:155903) $(\mathbb{Z}/N\mathbb{Z})^2$.

That is, $\Gamma_0(N)$ is the [preimage](@entry_id:150899) under $\rho_N$ of the stabilizer of the line spanned by $(1,0)$ in $(\mathbb{Z}/N\mathbb{Z})^2$. This is equivalent to saying that $\rho_N(\Gamma_0(N))$ is the group of upper-[triangular matrices](@entry_id:149740) in $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ [@problem_id:3010541]. This perspective is central to the modular interpretation of the corresponding modular curve $X_0(N)$ as a [moduli space](@entry_id:161715) for [elliptic curves](@entry_id:152409) with a specified [cyclic subgroup](@entry_id:138079) of order $N$.

### The Topological and Adelic Framework

The theory of [congruence subgroups](@entry_id:195720) finds its most powerful expression in a topological and adelic language, which synthesizes the information from all levels $N$ simultaneously.

#### The Congruence Topology and Profinite Completion

We can define a topology on $\mathrm{SL}_2(\mathbb{Z})$, the **congruence topology**, by taking the family of principal [congruence subgroups](@entry_id:195720) $\{\Gamma(N)\}_{N \ge 1}$ as a basis of open neighborhoods of the identity. This makes $\mathrm{SL}_2(\mathbb{Z})$ into a [topological group](@entry_id:154498) [@problem_id:3010548].

The completion of $\mathrm{SL}_2(\mathbb{Z})$ with respect to this topology is the inverse limit of the finite [quotient groups](@entry_id:145113):
$$
\widehat{\mathrm{SL}_2(\mathbb{Z})} = \varprojlim_{N} \mathrm{SL}_2(\mathbb{Z}) / \Gamma(N) \cong \varprojlim_{N} \mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z}).
$$
This completion is canonically isomorphic to the group $\mathrm{SL}_2(\widehat{\mathbb{Z}})$, where $\widehat{\mathbb{Z}} = \varprojlim_N \mathbb{Z}/N\mathbb{Z}$ is the **profinite completion** of the integers. By the Chinese Remainder Theorem, $\widehat{\mathbb{Z}}$ decomposes into a product of the rings of $p$-adic integers: $\widehat{\mathbb{Z}} \cong \prod_p \mathbb{Z}_p$. This induces an [isomorphism](@entry_id:137127) of [topological groups](@entry_id:155664) [@problem_id:3010548]:
$$
\mathrm{SL}_2(\widehat{\mathbb{Z}}) \cong \mathrm{SL}_2\left(\prod_p \mathbb{Z}_p\right) \cong \prod_p \mathrm{SL}_2(\mathbb{Z}_p).
$$
The group $\prod_p \mathrm{SL}_2(\mathbb{Z}_p)$ is a key component of the adelic group $\mathrm{SL}_2(\mathbb{A}_{\mathbb{Q}})$.

#### From Local Conditions to Global Subgroups

This adelic framework allows us to construct [congruence subgroups](@entry_id:195720) by intersecting $\mathrm{SL}_2(\mathbb{Z})$ with open subgroups of its completion, $\mathrm{SL}_2(\widehat{\mathbb{Z}})$. An open subgroup $K \subset \mathrm{SL}_2(\widehat{\mathbb{Z}})$ is of the form $K = \prod_p K_p$, where each $K_p$ is an open subgroup of $\mathrm{SL}_2(\mathbb{Z}_p)$ and $K_p = \mathrm{SL}_2(\mathbb{Z}_p)$ for all but finitely many primes $p$.

The standard [congruence subgroups](@entry_id:195720) arise from specific choices of local conditions [@problem_id:3010514]:
-   If we set $K_p = \{g \in \mathrm{SL}_2(\mathbb{Z}_p) : g \equiv I \pmod{p^{n_p}}\}$ and let $N = \prod_p p^{n_p}$, then $\mathrm{SL}_2(\mathbb{Z}) \cap K = \Gamma(N)$.
-   If we take $K_p$ to be matrices that are upper-triangular modulo $p^{n_p}$, then $\mathrm{SL}_2(\mathbb{Z}) \cap K = \Gamma_0(N)$.
-   If we take $K_p$ to be matrices that are unipotent upper-triangular modulo $p^{n_p}$, then $\mathrm{SL}_2(\mathbb{Z}) \cap K = \Gamma_1(N)$.

The Strong Approximation Theorem, in this language, states that the image of $\mathrm{SL}_2(\mathbb{Z})$ is dense in $\mathrm{SL}_2(\widehat{\mathbb{Z}})$. This is the powerful principle that guarantees that any [finite set](@entry_id:152247) of simultaneous local [congruence](@entry_id:194418) conditions can be realized by a global matrix in $\mathrm{SL}_2(\mathbb{Z})$ [@problem_id:3010514].

#### The Congruence Subgroup Problem

One might wonder if all finite-index subgroups of $\mathrm{SL}_2(\mathbb{Z})$ are [congruence subgroups](@entry_id:195720). This is known as the **Congruence Subgroup Problem**. For $\mathrm{SL}_2(\mathbb{Z})$, the answer is no. There exist finite-index subgroups that do not contain any $\Gamma(N)$. These are called **non-[congruence subgroups](@entry_id:195720)**.

This has a topological interpretation [@problem_id:3010536]. We can define another topology on $\mathrm{SL}_2(\mathbb{Z})$, the **profinite topology**, where the [neighborhood basis](@entry_id:148053) at the identity consists of *all* finite-index [normal subgroups](@entry_id:147397).
-   In the profinite topology, every finite-index subgroup is open.
-   In the [congruence](@entry_id:194418) topology, a subgroup is open if and only if it contains some $\Gamma(N)$, i.e., if it is a [congruence](@entry_id:194418) subgroup.

Since there exist non-[congruence subgroups](@entry_id:195720) of finite index, not every finite-index subgroup is open in the [congruence](@entry_id:194418) topology. This implies that the [congruence](@entry_id:194418) topology is strictly coarser than the profinite topology for $\mathrm{SL}_2(\mathbb{Z})$. The failure of these two natural topologies to coincide is a deep and fundamental feature of the [modular group](@entry_id:146452).