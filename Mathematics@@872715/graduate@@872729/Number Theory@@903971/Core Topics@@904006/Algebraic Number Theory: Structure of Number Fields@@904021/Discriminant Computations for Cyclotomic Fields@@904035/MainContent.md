## Introduction
In the study of algebraic number theory, the [discriminant](@entry_id:152620) stands as a fundamental invariant, encoding essential arithmetic information about a number field. For the class of [cyclotomic fields](@entry_id:153828), $\mathbb{Q}(\zeta_n)$, the [discriminant](@entry_id:152620) is not only computable but also serves as a gateway to understanding some of the deepest structures in the field. This article addresses the challenge of moving beyond a single definition of the [discriminant](@entry_id:152620) to a multifaceted understanding that integrates algebraic computation, the theory of ramification, and the elegance of [character theory](@entry_id:144021).

Throughout this exploration, you will gain a comprehensive toolkit for calculating and interpreting the discriminant of any cyclotomic field. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork. It establishes the discriminant's definition via the [trace pairing](@entry_id:187369) and minimal polynomials, provides explicit formulas for prime and prime-power moduli, and reveals its profound connection to ramification through local analysis and the [different ideal](@entry_id:204193). Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, explores the [discriminant](@entry_id:152620)'s role in determining the ring of integers, its utility in [class field theory](@entry_id:155687) via the [conductor-discriminant formula](@entry_id:193874), and its appearance in seminal results like the Analytic Class Number Formula and the Minkowski bound. Finally, the **Hands-On Practices** section offers a curated set of problems to reinforce these concepts, guiding you through concrete calculations that solidify the theoretical principles discussed.

## Principles and Mechanisms

In this chapter, we delve into the principles and mechanisms that govern the discriminant of a cyclotomic field. Building upon the foundational concepts introduced previously, we will establish several equivalent definitions of the [discriminant](@entry_id:152620), explore powerful computational techniques, and connect its structure to the profound theories of ramification and [class field theory](@entry_id:155687). Our goal is to move from concrete calculations to a deep structural understanding of this fundamental invariant.

### The Discriminant via the Trace Pairing

A cornerstone of [algebraic number](@entry_id:156710) theory is the **[field discriminant](@entry_id:198568)**, an integer that encapsulates crucial information about the arithmetic of a [number field](@entry_id:148388). For a number field $K$ of degree $d$ over $\mathbb{Q}$, with its ring of integers denoted by $\mathcal{O}_K$, the discriminant can be defined through the [trace pairing](@entry_id:187369).

Let $(b_1, b_2, \dots, b_d)$ be any **[integral basis](@entry_id:190217)**, which is a $\mathbb{Z}$-basis for the free $\mathbb{Z}$-module $\mathcal{O}_K$. The [trace map](@entry_id:194370), $\mathrm{Tr}_{K/\mathbb{Q}}: K \to \mathbb{Q}$, gives rise to a [symmetric bilinear form](@entry_id:148281) on $K$, known as the **trace form**, defined by $\langle x, y \rangle = \mathrm{Tr}_{K/\mathbb{Q}}(xy)$. The [discriminant](@entry_id:152620) of the [number field](@entry_id:148388) $K$, denoted $\mathrm{Disc}(K/\mathbb{Q})$, is defined as the determinant of the Gram matrix of the trace form with respect to an [integral basis](@entry_id:190217):

$$
\mathrm{Disc}(K/\mathbb{Q}) = \det \left( \left( \mathrm{Tr}_{K/\mathbb{Q}}(b_i b_j) \right)_{1 \le i,j \le d} \right)
$$

A critical feature of the [field discriminant](@entry_id:198568) is that its value is independent of the choice of [integral basis](@entry_id:190217) [@problem_id:3012105]. To see why, consider another [integral basis](@entry_id:190217) $(b'_1, \dots, b'_d)$. Since both sets are $\mathbb{Z}$-bases for the same module $\mathcal{O}_K$, they are related by a [change-of-basis matrix](@entry_id:184480) $B \in \mathrm{GL}_d(\mathbb{Z})$, the group of invertible $d \times d$ matrices with integer entries. The condition that both $B$ and its inverse $B^{-1}$ have integer entries forces the determinant of $B$ to be a unit in $\mathbb{Z}$, i.e., $\det(B) = \pm 1$. If $G$ and $G'$ are the Gram matrices for the bases $(b_i)$ and $(b'_j)$ respectively, the transformation rule for [bilinear forms](@entry_id:746794) dictates that $G' = B G B^\top$. Taking [determinants](@entry_id:276593), we find:

$$
\det(G') = \det(B) \det(G) \det(B^\top) = (\det(B))^2 \det(G)
$$

Since $(\det(B))^2 = (\pm 1)^2 = 1$, we have $\det(G') = \det(G)$. This confirms that the [field discriminant](@entry_id:198568) is a well-defined invariant of the field $K$.

For the cyclotomic field $K = \mathbb{Q}(\zeta_n)$, where $\zeta_n$ is a primitive $n$-th root of unity, a foundational theorem states that its [ring of integers](@entry_id:155711) is precisely $\mathcal{O}_K = \mathbb{Z}[\zeta_n]$. This implies that the set of powers $\{1, \zeta_n, \zeta_n^2, \dots, \zeta_n^{\phi(n)-1}\}$, where $\phi$ is Euler's totient function, forms an [integral basis](@entry_id:190217). This fact is of immense practical importance, as it provides a canonical and convenient basis for computation.

### Relation to the Minimal Polynomial

An alternative and powerful perspective links the [discriminant](@entry_id:152620) to the conjugates of a [primitive element](@entry_id:154321). Let $K = \mathbb{Q}(\alpha)$ be a [number field](@entry_id:148388) of degree $d$ generated by an [algebraic integer](@entry_id:155088) $\alpha$, and let $\sigma_1, \dots, \sigma_d$ be the distinct [embeddings](@entry_id:158103) of $K$ into $\mathbb{C}$. The [discriminant](@entry_id:152620) of the power basis $\{1, \alpha, \dots, \alpha^{d-1}\}$ can be expressed as the square of a determinant involving these embeddings [@problem_id:3012085]:

$$
\mathrm{Disc}(1, \alpha, \dots, \alpha^{d-1}) = \det\left((\sigma_j(\alpha^{i-1}))\right)^2_{1 \le i,j \le d}
$$

The matrix $(\sigma_j(\alpha^{i-1}))$ is a **Vandermonde matrix** whose determinant is $\prod_{1 \le j  k \le d} (\sigma_k(\alpha) - \sigma_j(\alpha))$. Consequently, the [discriminant](@entry_id:152620) of the basis is given by the famous product-of-differences formula:

$$
\mathrm{Disc}(1, \alpha, \dots, \alpha^{d-1}) = \prod_{1 \le j  k \le d} (\sigma_j(\alpha) - \sigma_k(\alpha))^2
$$

This quantity is also known as the discriminant of the element $\alpha$, $\mathrm{Disc}(\alpha)$, and is equal to the [discriminant](@entry_id:152620) of its [minimal polynomial](@entry_id:153598), $\Phi(x)$. A crucial identity connects this to the derivative of the [minimal polynomial](@entry_id:153598):

$$
\mathrm{Disc}(\alpha) = (-1)^{d(d-1)/2} N_{K/\mathbb{Q}}(\Phi'(\alpha))
$$

where $N_{K/\mathbb{Q}}$ is the field norm. For a cyclotomic field $K = \mathbb{Q}(\zeta_n)$, since $\mathcal{O}_K = \mathbb{Z}[\zeta_n]$, the power basis of $\zeta_n$ is an [integral basis](@entry_id:190217). Therefore, the [field discriminant](@entry_id:198568) $\mathrm{Disc}(K/\mathbb{Q})$ is identical to $\mathrm{Disc}(\zeta_n)$, and we can compute it using the minimal polynomial of $\zeta_n$, which is the $n$-th [cyclotomic polynomial](@entry_id:154273) $\Phi_n(x)$. The sign of the discriminant is determined by the number of pairs of [complex embeddings](@entry_id:189961), $r_2$. For $\mathbb{Q}(\zeta_n)$ with $n  2$, all embeddings are complex, so $r_1=0$ and $2r_2 = \phi(n)$, giving a sign of $(-1)^{\phi(n)/2}$.

### Explicit Computations

These formulas provide a direct path for computing discriminants. Let's illustrate this with the canonical examples.

#### The Case of a Prime Modulus, $n=p$

Consider $K = \mathbb{Q}(\zeta_p)$ for a prime $p$. The minimal polynomial is $\Phi_p(x) = \frac{x^p-1}{x-1} = 1 + x + \dots + x^{p-1}$. To compute its discriminant, we follow the procedure outlined in [@problem_id:3012100].

First, we find an expression for $\Phi_p'(\zeta_p)$. Differentiating the identity $(x-1)\Phi_p(x) = x^p - 1$ yields $\Phi_p(x) + (x-1)\Phi_p'(x) = px^{p-1}$. Evaluating at $x = \zeta_p$, and using $\Phi_p(\zeta_p) = 0$, we get:

$$
(\zeta_p - 1)\Phi_p'(\zeta_p) = p\zeta_p^{p-1} \implies \Phi_p'(\zeta_p) = \frac{p\zeta_p^{p-1}}{\zeta_p - 1}
$$

Next, we compute the norm of this element. The embeddings of $K$ are given by $\sigma_a: \zeta_p \mapsto \zeta_p^a$ for $a \in \{1, \dots, p-1\}$.

$$
N_{K/\mathbb{Q}}(\Phi_p'(\zeta_p)) = \prod_{a=1}^{p-1} \sigma_a(\Phi_p'(\zeta_p)) = \prod_{a=1}^{p-1} \Phi_p'(\zeta_p^a) = \prod_{a=1}^{p-1} \frac{p(\zeta_p^a)^{p-1}}{\zeta_p^a - 1}
$$

The product of the numerators is $p^{p-1} \prod_{a=1}^{p-1} \zeta_p^{-a} = p^{p-1} \zeta_p^{-p(p-1)/2} = p^{p-1}(-1)^{p-1}$. The product of the denominators is $\prod_{a=1}^{p-1} (\zeta_p^a - 1) = (-1)^{p-1}\prod_{a=1}^{p-1} (1 - \zeta_p^a)$. By evaluating $\Phi_p(x)$ at $x=1$, we find $\prod_{a=1}^{p-1} (1 - \zeta_p^a) = \Phi_p(1) = p$. Thus, the norm is:

$$
N_{K/\mathbb{Q}}(\Phi_p'(\zeta_p)) = \frac{p^{p-1}(-1)^{p-1}}{p(-1)^{p-1}} = p^{p-2}
$$

The degree is $d = p-1$. The sign factor is $(-1)^{(p-1)(p-2)/2}$. The discriminant is therefore $\mathrm{Disc}(\mathbb{Q}(\zeta_p)) = (-1)^{(p-1)(p-2)/2} p^{p-2}$. For an odd prime $p$, this sign is $(-1)^{(p-1)/2}$. The absolute value is $|\mathrm{Disc}(\mathbb{Q}(\zeta_p))| = p^{p-2}$.

#### The Case of a Prime Power Modulus, $n=p^k$

The same principles extend to $K = \mathbb{Q}(\zeta_{p^k})$, although the calculations are more involved. The [minimal polynomial](@entry_id:153598) is $\Phi_{p^k}(x) = \frac{x^{p^k}-1}{x^{p^{k-1}}-1} = \sum_{j=0}^{p-1} (x^{p^{k-1}})^j$. Differentiating this expression and evaluating at $\zeta_{p^k}$ yields the value of the derivative ([@problem_id:3012086]):

$$
\Phi_{p^k}'(\zeta_{p^k}) = \frac{p^k}{\zeta_{p^k}((\zeta_{p^k})^{p^{k-1}} - 1)}
$$

Calculating the norm of this expression and applying the discriminant formula leads to the $p$-adic valuation of the discriminant for $K = \mathbb{Q}(\zeta_{p^k})$:

$$
v_p(\mathrm{Disc}(K/\mathbb{Q})) = \phi(p^k)\left(k - \frac{1}{p-1}\right) = p^{k-1}((p-1)k-1)
$$

This formula is a key ingredient in understanding the general case and reveals a structure tied to the nature of ramification.

### Ramification and the Local Perspective

The discriminant is intimately connected to the phenomenon of **ramification**, the splitting behavior of [prime ideals](@entry_id:154026) in [field extensions](@entry_id:153187). A prime $p$ is said to ramify in a [number field](@entry_id:148388) $K$ if and only if $p$ divides $\mathrm{Disc}(K/\mathbb{Q})$ [@problem_id:3012074]. For the cyclotomic field $\mathbb{Q}(\zeta_n)$, the set of [ramified primes](@entry_id:183288) is precisely the set of prime divisors of $n$.

For an extension of [local fields](@entry_id:195717) $L/F$ with residue characteristic $p$, the ramification is classified as **tame** if the [ramification index](@entry_id:186386) $e$ is not divisible by $p$, and **wild** if $p$ divides $e$. In the global extension $K = \mathbb{Q}(\zeta_{p^k})/\mathbb{Q}$, the prime $p$ is [totally ramified](@entry_id:189971) with [ramification index](@entry_id:186386) $e = [K:\mathbb{Q}] = \phi(p^k) = p^{k-1}(p-1)$.

- If $k=1$ and $p$ is an odd prime, then $e=p-1$, which is not divisible by $p$. The ramification is **tame**.
- If $k \ge 2$ or if $p=2$ (and $k \ge 2$), then $p$ divides $p^{k-1}$, so $p|e$. The ramification is **wild** [@problem_id:3012073].

This distinction has a direct impact on the discriminant. The exponent of a prime $p$ in the discriminant is determined by the **[different ideal](@entry_id:204193)** $\mathfrak{D}_{K/\mathbb{Q}}$ via the relation that the [discriminant ideal](@entry_id:200833) $\mathfrak{d}_{K/\mathbb{Q}}$ is the norm of the different: $\mathfrak{d}_{K/\mathbb{Q}} = N_{K/\mathbb{Q}}(\mathfrak{D}_{K/\mathbb{Q}})$. The valuation of the different can be computed using the structure of the ramification groups of the corresponding local extension.

For the tame case $K=\mathbb{Q}(\zeta_p)$ (with $p$ odd), we consider the local extension $L=\mathbb{Q}_p(\zeta_p)/\mathbb{Q}_p$. The Galois group $G = \mathrm{Gal}(L/\mathbb{Q}_p)$ has ramification groups $G_i$. One finds that [the inertia group](@entry_id:200010) is $G_0 = G$ and the first (wild) ramification group is trivial, $G_1 = \{1\}$ [@problem_id:3012078]. Hilbert's different formula gives the valuation of the local different:

$$
v_L(\mathfrak{D}_{L/\mathbb{Q}_p}) = \sum_{i=0}^{\infty} (|G_i| - 1) = (|G_0|-1) + (|G_1|-1) + \dots = (p-1-1) + 0 + \dots = p-2
$$

Since the global discriminant exponent at $p$ is equal to this local different valuation, we find $v_p(\mathrm{Disc}(\mathbb{Q}(\zeta_p))) = p-2$, recovering our previous result from a deeper, structural perspective.

In the wild case, the higher ramification groups $G_i$ for $i \ge 1$ are non-trivial, leading to a larger different exponent and thus a larger power of $p$ in the discriminant, as reflected in the formula $v_p(\mathrm{Disc}) = p^{k-1}((p-1)k-1)$. The "depth" of this [wild ramification](@entry_id:149250) can be measured by the **Swan conductor**. For the local extension $\mathbb{Q}_p(\mu_{p^k})$, the Swan conductor of a [faithful character](@entry_id:147339) of the [wild ramification](@entry_id:149250) group is $k-1$, corresponding to the highest jump in the upper numbering [ramification filtration](@entry_id:190087) [@problem_id:3012077].

### The Conductor-Discriminant Formula: A Character-Theoretic Synthesis

The most elegant and comprehensive approach to the [discriminant](@entry_id:152620) of $\mathbb{Q}(\zeta_n)$ comes from [class field theory](@entry_id:155687), using the language of characters. The Galois group $G = \mathrm{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ is canonically isomorphic to the group of units $(\mathbb{Z}/n\mathbb{Z})^\times$. Since $G$ is abelian, its irreducible complex characters are one-dimensional and correspond precisely to **Dirichlet characters modulo $n$** [@problem_id:3012074]. Each such character $\chi$ has a **conductor**, $f(\chi)$, which is the smallest divisor $d$ of $n$ such that $\chi$ can be viewed as a character modulo $d$. A character is **primitive** if its conductor is $n$.

The celebrated **[conductor-discriminant formula](@entry_id:193874)** states that the absolute value of the [discriminant](@entry_id:152620) is the product of the conductors of all characters of the Galois group:

$$
|\mathrm{Disc}(\mathbb{Q}(\zeta_n)/\mathbb{Q})| = \prod_{\chi \in \widehat{G}} f(\chi)
$$

This remarkable formula links the arithmetic invariant ([discriminant](@entry_id:152620)) to analytic objects (character conductors). Taking the $p$-adic valuation of both sides gives an expression for the exponent of a prime $p$ in the discriminant:

$$
v_p(\mathrm{Disc}(K/\mathbb{Q})) = \sum_{\chi \in \widehat{G}} v_p(f(\chi))
$$

By decomposing the character group $\widehat{G} \cong \widehat{(\mathbb{Z}/n\mathbb{Z})^\times}$ according to the [prime factorization](@entry_id:152058) of $n$, one can perform this sum. Let $n = \prod p^{e_p}$ be the prime factorization of $n$. The analysis, which involves counting characters by their conductor, yields the following precise formula for the exponent of a prime $p$ dividing $n$ [@problem_id:3012080]:

$$
v_p(\mathrm{Disc}(\mathbb{Q}(\zeta_n)/\mathbb{Q})) = \phi(n)\left(e_p - \frac{1}{p-1}\right)
$$

Combining the contributions from all primes dividing $n$ and attaching the sign factor $(-1)^{\phi(n)/2}$, we arrive at the general formula for the [discriminant](@entry_id:152620) of any cyclotomic field:

$$
\mathrm{Disc}(\mathbb{Q}(\zeta_n)/\mathbb{Q}) = (-1)^{\phi(n)/2} \frac{n^{\phi(n)}}{\prod_{p|n} p^{\phi(n)/(p-1)}} = (-1)^{\phi(n)/2} \prod_{p|n} p^{\phi(n)e_p - \frac{\phi(n)}{p-1}}
$$

The term $-\frac{\phi(n)}{p-1}$ in the exponent has a beautiful structural interpretation [@problem_id:3012091]. The term $\phi(n)e_p$ can be seen as a "naive" maximal contribution. The subtraction arises as a correction term. This correction is precisely equal to the number of characters of $G$ whose $p$-primary component is trivial on the "tame quotient" of the local [inertia group](@entry_id:143171) at $p$. In other words, it counts characters whose local behavior at $p$ is purely wild. This insight reveals a deep symmetry in the structure of ramification, perfectly captured by the language of characters and their conductors.