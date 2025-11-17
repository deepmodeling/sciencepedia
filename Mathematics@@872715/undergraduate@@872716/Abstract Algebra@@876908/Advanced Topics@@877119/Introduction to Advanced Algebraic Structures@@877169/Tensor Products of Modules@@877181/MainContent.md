## Introduction
In the landscape of [modern algebra](@entry_id:171265), the [tensor product of modules](@entry_id:155679) stands as a fundamental and powerful construction. It provides a universal language to transform complex, multilinear problems into the more manageable and well-understood domain of linear algebra. While seemingly abstract, this tool is the cornerstone for building new algebraic objects, relating different mathematical structures, and uncovering deep connections between fields.

At its heart, the [tensor product](@entry_id:140694) addresses the challenge of systematically handling functions that are linear in several variables simultaneously—bilinear or multilinear maps. By creating a new module where these maps become simple [linear transformations](@entry_id:149133), the [tensor product](@entry_id:140694) offers a powerful conceptual and computational simplification.

This article will guide you through the essential aspects of tensor products. We will begin in the first chapter, **Principles and Mechanisms**, by defining the [tensor product](@entry_id:140694) through its crucial universal property, exploring the structure of its elements, and establishing the fundamental rules and isomorphisms that govern its behavior. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the [tensor product](@entry_id:140694)'s utility as a practical tool across linear algebra, [commutative algebra](@entry_id:149047), and [representation theory](@entry_id:137998). Finally, the **Hands-On Practices** section provides an opportunity to solidify these abstract concepts through guided problem-solving, bridging theory with practical application.

## Principles and Mechanisms

The tensor product is a construction of central importance in [modern algebra](@entry_id:171265), providing a universal mechanism for transforming multilinear [algebraic structures](@entry_id:139459) into linear ones. Having introduced its categorical role, we now turn to the concrete principles and mechanisms that govern its behavior. This chapter will develop the [tensor product](@entry_id:140694) from its defining [universal property](@entry_id:145831), explore the structure of its elements, and establish the fundamental algebraic rules and isomorphisms that make it a powerful computational and conceptual tool.

### The Universal Property: Linearizing Bilinear Maps

The conceptual foundation of the [tensor product](@entry_id:140694) of two $R$-modules, $M$ and $N$, is its role as the most general object that linearizes [bilinear maps](@entry_id:186502) originating from $M \times N$. Let $R$ be a [commutative ring](@entry_id:148075). An **$R$-[bilinear map](@entry_id:150924)** is a function $B: M \times N \to P$, where $P$ is another $R$-module, that is $R$-linear in each variable separately. That is, for all $m, m_1, m_2 \in M$, $n, n_1, n_2 \in N$, and $r \in R$:
- $B(m_1 + m_2, n) = B(m_1, n) + B(m_2, n)$
- $B(m, n_1 + n_2) = B(m, n_1) + B(m, n_2)$
- $B(rm, n) = B(m, rn) = rB(m, n)$

The tensor product $M \otimes_R N$ is an $R$-module equipped with a canonical [bilinear map](@entry_id:150924) $\otimes: M \times N \to M \otimes_R N$, written $(m, n) \mapsto m \otimes n$, which satisfies the following **universal property**: For any $R$-module $P$ and any $R$-[bilinear map](@entry_id:150924) $B: M \times N \to P$, there exists a *unique* $R$-[linear map](@entry_id:201112) $\phi: M \otimes_R N \to P$ such that $B = \phi \circ \otimes$. In other words, $\phi(m \otimes n) = B(m, n)$ for all $m \in M, n \in N$.

This property states that any [bilinear map](@entry_id:150924) from $M \times N$ can be "factored through" the [tensor product](@entry_id:140694). Instead of studying the [bilinear map](@entry_id:150924) $B$, we can study the corresponding [linear map](@entry_id:201112) $\phi$, which is often much simpler.

A classic example arises in linear algebra. Let $V = \mathbb{R}^3$ be a vector space over the field $\mathbb{R}$. The standard Euclidean dot product, $\cdot: \mathbb{R}^3 \times \mathbb{R}^3 \to \mathbb{R}$, is an $\mathbb{R}$-[bilinear map](@entry_id:150924). By the universal property, there must exist a unique [linear map](@entry_id:201112) $\phi: \mathbb{R}^3 \otimes_{\mathbb{R}} \mathbb{R}^3 \to \mathbb{R}$ such that $\phi(\mathbf{x} \otimes \mathbf{y}) = \mathbf{x} \cdot \mathbf{y}$ for all vectors $\mathbf{x}, \mathbf{y} \in \mathbb{R}^3$. The linearity of $\phi$ allows us to evaluate its action on more complex elements. For example, consider an element $T = (3\mathbf{e}_1 - \mathbf{e}_2) \otimes (2\mathbf{e}_1 + \mathbf{e}_2) + (\mathbf{e}_2 + 2\mathbf{e}_3) \otimes (\mathbf{e}_3 - \mathbf{e}_2)$ in $\mathbb{R}^3 \otimes_{\mathbb{R}} \mathbb{R}^3$, where $\{\mathbf{e}_i\}$ is the standard orthonormal basis. Since $\phi$ is linear, its action distributes over the sum:
$$ \phi(T) = \phi((3\mathbf{e}_1 - \mathbf{e}_2) \otimes (2\mathbf{e}_1 + \mathbf{e}_2)) + \phi((\mathbf{e}_2 + 2\mathbf{e}_3) \otimes (\mathbf{e}_3 - \mathbf{e}_2)) $$
By the defining property of $\phi$, this becomes a sum of dot products:
$$ \phi(T) = (3\mathbf{e}_1 - \mathbf{e}_2) \cdot (2\mathbf{e}_1 + \mathbf{e}_2) + (\mathbf{e}_2 + 2\mathbf{e}_3) \cdot (\mathbf{e}_3 - \mathbf{e}_2) $$
Using the [bilinearity](@entry_id:146819) of the dot product and the fact that $\mathbf{e}_i \cdot \mathbf{e}_j = \delta_{ij}$, the first term is $6(\mathbf{e}_1 \cdot \mathbf{e}_1) - (\mathbf{e}_2 \cdot \mathbf{e}_2) = 6 - 1 = 5$. The second term is $2(\mathbf{e}_3 \cdot \mathbf{e}_3) - (\mathbf{e}_2 \cdot \mathbf{e}_2) = 2 - 1 = 1$. Thus, $\phi(T) = 5 + 1 = 6$. [@problem_id:1825325] This example demonstrates how the universal property provides a concrete bridge between bilinear operations and the linear algebra of tensor spaces.

### The Structure of Tensor Product Modules

An element of $M \otimes_R N$ is called a **tensor**. The elements of the form $m \otimes n$ are called **simple tensors** or **pure tensors**. It is a common misconception that every element of the [tensor product](@entry_id:140694) is a [simple tensor](@entry_id:201624). In fact, a general element of $M \otimes_R N$ is a finite sum of simple tensors, like $\sum_{i=1}^k m_i \otimes n_i$.

All manipulations of tensors are derived from the [bilinearity](@entry_id:146819) of the $\otimes$ map. Specifically, for all $m, m_1, m_2 \in M$, $n, n_1, n_2 \in N$, and $r \in R$:
1.  $(m_1 + m_2) \otimes n = m_1 \otimes n + m_2 \otimes n$
2.  $m \otimes (n_1 + n_2) = m \otimes n_1 + m \otimes n_2$
3.  $(rm) \otimes n = m \otimes (rn)$

This last relation is called the **balancing property** and is fundamental. It shows how scalars can be moved across the tensor symbol.

To see that not all tensors are simple, let's consider the vector space $V = \mathbb{R}^2$ as an $\mathbb{R}$-module, with standard basis $\{e_1, e_2\}$. The [tensor product](@entry_id:140694) $V \otimes_{\mathbb{R}} V$ has a basis given by $\{e_i \otimes e_j\}_{i,j=1,2}$, which is $\{e_1 \otimes e_1, e_1 \otimes e_2, e_2 \otimes e_1, e_2 \otimes e_2\}$. Now consider the tensor $T = e_1 \otimes e_2 + e_2 \otimes e_1$. Let us assume, for the sake of contradiction, that $T$ is a [simple tensor](@entry_id:201624). This would mean $T = v \otimes w$ for some vectors $v = ae_1 + be_2$ and $w = ce_1 + de_2$ in $V$. Expanding this expression using the [bilinearity](@entry_id:146819) rules gives:
$$ v \otimes w = (ae_1 + be_2) \otimes (ce_1 + de_2) = ac(e_1 \otimes e_1) + ad(e_1 \otimes e_2) + bc(e_2 \otimes e_1) + bd(e_2 \otimes e_2) $$
For this to be equal to $T = 0(e_1 \otimes e_1) + 1(e_1 \otimes e_2) + 1(e_2 \otimes e_1) + 0(e_2 \otimes e_2)$, we must equate the coefficients of the basis vectors. This yields a system of equations for the scalars $a,b,c,d \in \mathbb{R}$:
$$ ac = 0, \quad ad = 1, \quad bc = 1, \quad bd = 0 $$
From $ad=1$ and $bc=1$, we know that none of $a, b, c, d$ can be zero. But if $a \neq 0$ and $c \neq 0$, then $ac \neq 0$, which contradicts the first equation. This contradiction proves that our initial assumption was false. Therefore, $T = e_1 \otimes e_2 + e_2 \otimes e_1$ cannot be written as a [simple tensor](@entry_id:201624). [@problem_id:1825387] Such elements are sometimes referred to as "entangled," a term borrowed from quantum mechanics where the tensor product is used to model composite systems.

### Fundamental Isomorphisms

Several canonical isomorphisms are essential for working with tensor products. Let $R$ be a [commutative ring](@entry_id:148075) and $L, M, N$ be $R$-modules.

**Commutativity:** There is a [natural isomorphism](@entry_id:276379) $M \otimes_R N \cong N \otimes_R M$.
To establish this, consider the map $f: M \times N \to N \otimes_R M$ given by $f(m,n) = n \otimes m$. One can verify that this map is $R$-bilinear. For example, additivity in the first argument holds because $f(m_1+m_2, n) = n \otimes (m_1+m_2) = n \otimes m_1 + n \otimes m_2 = f(m_1, n) + f(m_2, n)$. The other properties are verified similarly. [@problem_id:1825338] By the universal property of $M \otimes_R N$, this [bilinear map](@entry_id:150924) $f$ induces a unique linear map $\phi: M \otimes_R N \to N \otimes_R M$ such that $\phi(m \otimes n) = n \otimes m$. A symmetric argument produces a linear map $\psi: N \otimes_R M \to M \otimes_R N$ where $\psi(n \otimes m) = m \otimes n$. Since $\psi \circ \phi$ and $\phi \circ \psi$ are the identity maps on their respective domains, $\phi$ and $\psi$ are isomorphisms.

**Associativity:** There is a [natural isomorphism](@entry_id:276379) $(L \otimes_R M) \otimes_R N \cong L \otimes_R (M \otimes_R N)$.
This [isomorphism](@entry_id:137127), sending $(l \otimes m) \otimes n$ to $l \otimes (m \otimes n)$, allows us to write expressions like $L \otimes_R M \otimes_R N$ without ambiguity. A concrete, if dramatic, illustration can be seen with $\mathbb{Z}$-modules. Let $M=\mathbb{Q}, N=\mathbb{Z}/2\mathbb{Z}, P=\mathbb{Z}/3\mathbb{Z}$. We find that $M \otimes_{\mathbb{Z}} N = \mathbb{Q} \otimes_{\mathbb{Z}} (\mathbb{Z}/2\mathbb{Z}) \cong \mathbb{Q}/2\mathbb{Q} = \{0\}$, because $\mathbb{Q}$ is a divisible group. Thus, $(M \otimes_{\mathbb{Z}} N) \otimes_{\mathbb{Z}} P \cong \{0\} \otimes_{\mathbb{Z}} P = \{0\}$. On the other hand, $N \otimes_{\mathbb{Z}} P = (\mathbb{Z}/2\mathbb{Z}) \otimes_{\mathbb{Z}} (\mathbb{Z}/3\mathbb{Z}) \cong \mathbb{Z}/\text{gcd}(2,3)\mathbb{Z} = \mathbb{Z}/\mathbb{Z} = \{0\}$. Therefore, $M \otimes_{\mathbb{Z}} (N \otimes_{\mathbb{Z}} P) \cong M \otimes_{\mathbb{Z}} \{0\} = \{0\}$. Both sides are isomorphic to the trivial module, consistent with associativity. [@problem_id:1825365]

**Identity Element:** For any $R$-module $M$, there is a [natural isomorphism](@entry_id:276379) $R \otimes_R M \cong M$, given by the map $r \otimes m \mapsto rm$. This shows that tensoring with the base ring $R$ does not change the module.

**Tensor Products with Quotients:** For any ideal $I$ of $R$ and any $R$-module $M$, there is a [natural isomorphism](@entry_id:276379) $(R/I) \otimes_R M \cong M/IM$.
Here, $IM$ is the submodule of $M$ generated by elements of the form $im$ for $i \in I, m \in M$. This is a particularly powerful tool for computation. To see why it's true, consider the [bilinear map](@entry_id:150924) $B: (R/I) \times M \to M/IM$ defined by $B(r+I, m) = rm + IM$. This map is well-defined and bilinear, so it induces a linear map $\phi: (R/I) \otimes_R M \to M/IM$. One can then construct its inverse, showing it is an isomorphism.

Let's apply this in a more advanced context. Let $R = \mathbb{Z}[i]$ be the ring of Gaussian integers and consider the ideal $I = \langle 1+i \rangle$. Let $M$ be the $R$-module $M = R/\langle 3-i \rangle$. We want to compute $N = (R/I) \otimes_R M$. Using our isomorphism:
$$ N \cong M/IM = \frac{R/\langle 3-i \rangle}{\langle 1+i \rangle (R/\langle 3-i \rangle)} $$
The submodule in the denominator is $(\langle 1+i \rangle + \langle 3-i \rangle) / \langle 3-i \rangle$. By the [third isomorphism theorem](@entry_id:142893) for modules, this quotient is isomorphic to $R/(\langle 1+i \rangle + \langle 3-i \rangle)$. The problem reduces to understanding the sum of the two ideals. In the ring $\mathbb{Z}[i]$, we can check if one generator divides the other:
$$ \frac{3-i}{1+i} = \frac{(3-i)(1-i)}{(1+i)(1-i)} = \frac{3-3i-i+i^2}{1^2-i^2} = \frac{2-4i}{2} = 1-2i $$
Since $1-2i$ is a Gaussian integer, we have $3-i = (1-2i)(1+i)$, which implies that $\langle 3-i \rangle \subseteq \langle 1+i \rangle$. Therefore, the sum of the ideals is just the larger ideal, $\langle 1+i \rangle + \langle 3-i \rangle = \langle 1+i \rangle$. Our [tensor product](@entry_id:140694) is thus isomorphic to $R/\langle 1+i \rangle = \mathbb{Z}[i]/\langle 1+i \rangle$. The size of this [quotient ring](@entry_id:155460) is the norm of the generator, $N(1+i) = 1^2 + 1^2 = 2$. A ring of size 2 must be isomorphic to $\mathbb{Z}/2\mathbb{Z}$. So, $(R/I) \otimes_R M \cong \mathbb{Z}/2\mathbb{Z}$. [@problem_id:1825378]

### Tensor Products and Exactness: Flat Modules

One of the most important properties of the [tensor product](@entry_id:140694) is its behavior with respect to [exact sequences](@entry_id:151503). A sequence of $R$-module homomorphisms $\dots \to A \xrightarrow{f} B \xrightarrow{g} C \to \dots$ is **exact** at $B$ if $\text{Im}(f) = \text{Ker}(g)$. A **[short exact sequence](@entry_id:137930)** is a sequence of the form $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$ which is exact at $A$, $B$, and $C$. This means $f$ is injective, $g$ is surjective, and $\text{Im}(f) = \text{Ker}(g)$.

Given an $R$-module $M$, we can apply the [functor](@entry_id:260898) $-\otimes_R M$ to a [short exact sequence](@entry_id:137930), which yields a new sequence:
$$ A \otimes_R M \xrightarrow{f \otimes 1_M} B \otimes_R M \xrightarrow{g \otimes 1_M} C \otimes_R M \to 0 $$
A fundamental theorem states that this resulting sequence is always exact at $B \otimes_R M$ and $C \otimes_R M$. This property is called the **right-exactness** of the [tensor product](@entry_id:140694). However, the map $f \otimes 1_M$ is not guaranteed to be injective, even if $f$ is. The functor $-\otimes_R M$ is not, in general, a left-exact functor.

For example, consider the [short exact sequence](@entry_id:137930) of $\mathbb{Z}$-modules $0 \to \mathbb{Z} \xrightarrow{\times 12} \mathbb{Z} \to \mathbb{Z}/12\mathbb{Z} \to 0$. Let's tensor this with the module $M=\mathbb{Z}/30\mathbb{Z}$. The resulting sequence is:
$$ \mathbb{Z} \otimes_{\mathbb{Z}} (\mathbb{Z}/30\mathbb{Z}) \xrightarrow{f'} \mathbb{Z} \otimes_{\mathbb{Z}} (\mathbb{Z}/30\mathbb{Z}) \xrightarrow{g'} (\mathbb{Z}/12\mathbb{Z}) \otimes_{\mathbb{Z}} (\mathbb{Z}/30\mathbb{Z}) \to 0 $$
Using the isomorphisms $\mathbb{Z} \otimes_{\mathbb{Z}} N \cong N$ and $(\mathbb{Z}/m\mathbb{Z}) \otimes_{\mathbb{Z}} (\mathbb{Z}/n\mathbb{Z}) \cong \mathbb{Z}/\gcd(m,n)\mathbb{Z}$, the sequence becomes:
$$ \mathbb{Z}/30\mathbb{Z} \xrightarrow{\times 12} \mathbb{Z}/30\mathbb{Z} \xrightarrow{g'} \mathbb{Z}/6\mathbb{Z} \to 0 $$
The map $g'$ is the canonical projection. The exactness at $\mathbb{Z}/6\mathbb{Z}$ is guaranteed, meaning $g'$ is surjective. Right-[exactness](@entry_id:268999) also guarantees that $\text{Im}(f') = \text{Ker}(g')$. The image of the multiplication-by-12 map on $\mathbb{Z}/30\mathbb{Z}$ is the subgroup generated by 12, which is $12(\mathbb{Z}/30\mathbb{Z})$. This subgroup has order $30/\gcd(12,30) = 30/6=5$. Thus, $\text{Ker}(g')$ is a cyclic group of order 5. [@problem_id:1825317] Notice that the original map $f$ was injective, but the new map $f'$ (multiplication by 12 on $\mathbb{Z}/30\mathbb{Z}$) is not, as its kernel is the subgroup generated by $30/6=5$, which is of order 6.

This leads to a crucial definition. An $R$-module $F$ is called **flat** if the functor $-\otimes_R F$ is exact, meaning it preserves injective maps. That is, for any injection $f: M \to N$, the [induced map](@entry_id:271712) $f \otimes 1_F: M \otimes_R F \to N \otimes_R F$ is also injective.

The most important class of [flat modules](@entry_id:153965) are **[free modules](@entry_id:152514)**. A free $R$-module is one that has a basis, i.e., it is isomorphic to a direct sum of copies of $R$. Since the tensor product distributes over direct sums, i.e., $(\bigoplus_i M_i) \otimes_R N \cong \bigoplus_i (M_i \otimes_R N)$, to show a [free module](@entry_id:150200) $R^{\oplus I}$ is flat, it suffices to show $R$ itself is flat. This is true because tensoring an injection $f: M \to N$ with $R$ gives the map $f \otimes 1_R: M \otimes_R R \to N \otimes_R R$, which is isomorphic to the original injection $f: M \to N$ under the identification $M \otimes_R R \cong M$. [@problem_id:1825315]

While all [projective modules](@entry_id:149251) are flat (and [free modules](@entry_id:152514) are projective), the converse is not true. A module can be flat without being projective. The canonical example is the $\mathbb{Z}$-module $\mathbb{Q}$. To show $\mathbb{Q}$ is flat, one must verify that for any injection of $\mathbb{Z}$-modules $f: A \hookrightarrow B$, the map $1_\mathbb{Q} \otimes f: \mathbb{Q} \otimes_{\mathbb{Z}} A \to \mathbb{Q} \otimes_{\mathbb{Z}} B$ is injective. This is a general property of localization.
However, $\mathbb{Q}$ is not a projective $\mathbb{Z}$-module. A module is projective if and only if it is a [direct summand](@entry_id:150541) of a [free module](@entry_id:150200). Since $\mathbb{Z}$ is a Principal Ideal Domain, any submodule (and thus any [direct summand](@entry_id:150541)) of a free $\mathbb{Z}$-module is itself free. If $\mathbb{Q}$ were projective, it would have to be a free $\mathbb{Z}$-module. But free $\mathbb{Z}$-modules are not divisible (multiplication by any $n \neq 0, \pm 1$ is not surjective), whereas $\mathbb{Q}$ is the archetypal divisible group. Thus, $\mathbb{Q}$ is a flat but not projective $\mathbb{Z}$-module. [@problem_id:1825385]

### Applications and Further Structures

#### Torsion, Divisibility, and the Zero Module

When working with $\mathbb{Z}$-modules (abelian groups), the interplay between torsion and divisibility provides a powerful computational shortcut.
- A $\mathbb{Z}$-module $A$ is a **[torsion module](@entry_id:151266)** if every element has finite order.
- A $\mathbb{Z}$-module $B$ is a **divisible module** if for every $b \in B$ and non-zero integer $n$, the equation $nx=b$ has a solution in $B$.

A key result states that if $A$ is a [torsion module](@entry_id:151266) and $B$ is a divisible module, then $A \otimes_{\mathbb{Z}} B = \{0\}$.
To prove this, take any [simple tensor](@entry_id:201624) $a \otimes b \in A \otimes_{\mathbb{Z}} B$. Since $A$ is torsion, there exists a non-zero integer $n$ such that $na=0$. Since $B$ is divisible, there exists $c \in B$ such that $nc=b$. We can then write:
$$ a \otimes b = a \otimes (nc) = (na) \otimes c = 0 \otimes c = 0 $$
Since every [simple tensor](@entry_id:201624) is zero, every element of the [tensor product](@entry_id:140694) (being a sum of simple tensors) is zero.

For example, the module $\mathbb{Q}/\mathbb{Z}$ is a [torsion module](@entry_id:151266), as any element $p/q + \mathbb{Z}$ is annihilated by $q$. The module $\mathbb{Q}$ is divisible. Therefore, $(\mathbb{Q}/\mathbb{Z}) \otimes_{\mathbb{Z}} \mathbb{Q} = \{0\}$. [@problem_id:1825347] This principle elegantly resolves many computations that would otherwise be cumbersome.

#### Extension of Scalars

One of the most significant applications of the tensor product is **[extension of scalars](@entry_id:150588)**. Suppose we have a [ring homomorphism](@entry_id:153804) $f: R \to A$, making $A$ an $R$-algebra. For any $R$-module $M$, we can construct a new module, $M \otimes_R A$. This new object naturally carries the structure of an $A$-module. The [scalar multiplication](@entry_id:155971) by an element $a' \in A$ is defined on simple tensors by:
$$ a' \cdot (m \otimes a) = m \otimes (a'a) $$
and extended linearly to all of $M \otimes_R A$. This construction effectively "extends" the scalars acting on $M$ from the ring $R$ to the larger algebra $A$.

For instance, consider the ring of integers $R=\mathbb{Z}$ and the Gaussian integers $A=\mathbb{Z}[i]$. Let $M = \mathbb{Z}/6\mathbb{Z}$ be a $\mathbb{Z}$-module. The [tensor product](@entry_id:140694) $V = (\mathbb{Z}/6\mathbb{Z}) \otimes_{\mathbb{Z}} \mathbb{Z}[i]$ becomes a $\mathbb{Z}[i]$-module. Let's compute a product in this module, for example, $(2-i) \cdot u$ where $u = (2 \otimes (1+2i)) + (3 \otimes (3-i))$.
Using the definition of the $A$-module action and its linearity:
$$ (2-i) \cdot u = (2-i) \cdot (2 \otimes (1+2i)) + (2-i) \cdot (3 \otimes (3-i)) $$
$$ = 2 \otimes ((2-i)(1+2i)) + 3 \otimes ((2-i)(3-i)) $$
The products in $\mathbb{Z}[i]$ are $(2-i)(1+2i) = 4+3i$ and $(2-i)(3-i) = 5-5i$. So we have:
$$ v = 2 \otimes (4+3i) + 3 \otimes (5-5i) $$
Now we use the balancing property of the tensor product over $\mathbb{Z}$. Since the first component is in $\mathbb{Z}/6\mathbb{Z}$, we can think of the integer 2 as $2 \cdot 1$, where $1$ is the generator of $\mathbb{Z}/6\mathbb{Z}$.
$$ 2 \otimes (4+3i) = (2 \cdot 1) \otimes (4+3i) = 1 \otimes (2(4+3i)) = 1 \otimes (8+6i) $$
Similarly, $3 \otimes (5-5i) = 1 \otimes (3(5-5i)) = 1 \otimes (15-15i)$. Adding these gives:
$$ v = 1 \otimes (8+6i) + 1 \otimes (15-15i) = 1 \otimes ((8+6i) + (15-15i)) = 1 \otimes (23-9i) $$
Finally, we must remember that calculations in the first component are modulo 6. This is equivalent to saying that $1 \otimes z$ depends only on the coset of $z$ in $\mathbb{Z}[i]/6\mathbb{Z}[i]$. We reduce the coefficients of $23-9i$ modulo 6: $23 \equiv 5 \pmod 6$ and $-9 \equiv 3 \pmod 6$.
Thus, $v = 1 \otimes (5+3i)$. [@problem_id:1825360] This example shows how a module over a [simple ring](@entry_id:149244) like $\mathbb{Z}$ can be transformed into a module over a more complex algebraic structure, carrying its arithmetic with it.