## Introduction
Number fields, as [finite extensions](@entry_id:152412) of the rational numbers, are central objects in [modern algebra](@entry_id:171265). While their definition is purely algebraic, a deep understanding of their intricate arithmetic structure requires bridging this abstract world with the powerful tools of analysis and geometry. This connection is forged by the concept of field embeddings—homomorphisms that map a number field into the field of complex numbers. These embeddings provide concrete representations of the field, allowing us to "see" its elements and analyze its properties using the familiar topology of the complex plane. This article explores the theory and profound consequences of these embeddings, revealing how they unlock the secrets of number fields.

The following chapters will guide you from the foundational principles of [embeddings](@entry_id:158103) to their most significant applications. In **Principles and Mechanisms**, we will formally define embeddings, establish their connection to the roots of minimal polynomials, and introduce the crucial concept of the signature $(r_1, r_2)$ which classifies fields based on their real and [complex representations](@entry_id:144331). Next, in **Applications and Interdisciplinary Connections**, we will witness the power of this framework as we explore the Minkowski embedding in the [geometry of numbers](@entry_id:192990), prove Dirichlet's celebrated Unit Theorem on the structure of units, and see how embeddings influence fundamental analytic objects like the Dedekind zeta function. Finally, the **Hands-On Practices** section will provide an opportunity to apply these concepts through guided problems, solidifying your understanding by connecting theory to computation.

## Principles and Mechanisms

The study of a number field $K$ is intrinsically linked to its relationship with the field of complex numbers $\mathbb{C}$. While a [number field](@entry_id:148388) is an abstract algebraic object, its concrete realizations as subfields of $\mathbb{C}$ provide profound insights into its arithmetic structure. These realizations are captured by the concept of field embeddings, which serve as a bridge between the abstract algebra of $K$ and the powerful analytic and topological tools available in the complex plane. This chapter elucidates the principles governing these embeddings and the mechanisms through which they reveal the fundamental properties of number fields.

### The Set of Embeddings: Definition and Fundamental Properties

Let $K$ be a [number field](@entry_id:148388), which is by definition a finite field extension of the rational numbers $\mathbb{Q}$. A **field embedding** of $K$ into the complex numbers is a [field homomorphism](@entry_id:155269) $\sigma: K \to \mathbb{C}$. Any such homomorphism necessarily fixes the prime [subfield](@entry_id:155812) $\mathbb{Q}$ pointwise. That is, for any $q \in \mathbb{Q}$, $\sigma(q) = q$. For this reason, these are often called $\mathbb{Q}$-[embeddings](@entry_id:158103). Since the kernel of a [field homomorphism](@entry_id:155269) is an ideal and the only ideals of a field are $\{0\}$ and the field itself, any non-zero homomorphism is injective. Thus, an embedding provides an isomorphic copy of $K$ as a [subfield](@entry_id:155812) of $\mathbb{C}$.

The set of all such embeddings is denoted by $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$. A crucial insight is that an embedding $\sigma$ is completely determined by its action on the elements of $K$ that are not in $\mathbb{Q}$. By the Primitive Element Theorem, any number field $K$ can be written as $K = \mathbb{Q}(\alpha)$ for some [algebraic integer](@entry_id:155088) $\alpha \in K$. Any element of $K$ is then a polynomial in $\alpha$ with rational coefficients. Since $\sigma$ fixes $\mathbb{Q}$, its behavior is entirely dictated by the value of $\sigma(\alpha)$.

What are the possible values for $\sigma(\alpha)$? Let $m_\alpha(x) \in \mathbb{Q}[x]$ be the [minimal polynomial](@entry_id:153598) of $\alpha$ over $\mathbb{Q}$. Since $m_\alpha(\alpha) = 0$, applying the homomorphism $\sigma$ yields:
$$ \sigma(m_\alpha(\alpha)) = \sigma(0) = 0 $$
As $\sigma$ fixes the coefficients of $m_\alpha(x)$, this becomes:
$$ m_\alpha(\sigma(\alpha)) = 0 $$
This demonstrates a foundational principle: the image of a generator $\alpha$ under any embedding $\sigma$ must be a root of the [minimal polynomial](@entry_id:153598) of $\alpha$. The roots of $m_\alpha(x)$ that lie in $\mathbb{C}$ are known as the **algebraic conjugates** of $\alpha$. Since number fields are extensions of $\mathbb{Q}$ (a field of characteristic zero), they are [separable extensions](@entry_id:150569). This guarantees that the minimal polynomial $m_\alpha(x)$ of degree $n = [K:\mathbb{Q}]$ has exactly $n$ distinct roots in $\mathbb{C}$. Each of these roots gives rise to a unique embedding. This leads to the following fundamental theorem.

**Theorem:** The number of distinct [embeddings](@entry_id:158103) of a number field $K$ into the complex numbers $\mathbb{C}$ is equal to the degree of the field extension, $| \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C}) | = [K:\mathbb{Q}]$.

As a first example, consider a [quadratic field](@entry_id:636261) $K = \mathbb{Q}(\sqrt{d})$, where $d$ is a non-zero, square-free integer [@problem_id:3013296]. The degree of this extension is $[K:\mathbb{Q}]=2$. The minimal polynomial of the generator $\sqrt{d}$ is $m(x) = x^2 - d$. The roots of this polynomial in $\mathbb{C}$ are $\sqrt{d}$ and $-\sqrt{d}$. Consequently, there are exactly two embeddings:
1.  The identity embedding, $\sigma_1$, where $\sigma_1(a+b\sqrt{d}) = a+b\sqrt{d}$.
2.  The conjugation embedding, $\sigma_2$, where $\sigma_2(a+b\sqrt{d}) = a-b\sqrt{d}$.
The total number of [embeddings](@entry_id:158103) is $2$, matching the degree of the extension.

### The Signature of a Number Field

While there are always $[K:\mathbb{Q}]$ embeddings into $\mathbb{C}$, their images may have different properties. The most important classification distinguishes between [embeddings](@entry_id:158103) whose image is contained within the real numbers $\mathbb{R}$ and those whose image is not.

An embedding $\sigma: K \to \mathbb{C}$ is called a **real embedding** if its image $\sigma(K)$ is a [subfield](@entry_id:155812) of $\mathbb{R}$. If $\sigma(K) \not\subseteq \mathbb{R}$, then $\sigma$ is called a **complex embedding**.

This classification is elegantly understood through the action of [complex conjugation](@entry_id:174690) on $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$ [@problem_id:3013303]. Let $c: \mathbb{C} \to \mathbb{C}$ be the standard [complex conjugation](@entry_id:174690) map, $z \mapsto \bar{z}$. For any embedding $\sigma$, we can define its conjugate embedding, $\overline{\sigma}$, by post-composition: $\overline{\sigma} = c \circ \sigma$.
An embedding $\sigma$ is a real embedding if and only if its image consists entirely of real numbers. This is equivalent to the condition that for every $x \in K$, $\overline{\sigma(x)} = \sigma(x)$. This means $\overline{\sigma} = \sigma$. In other words, the real [embeddings](@entry_id:158103) are precisely the fixed points of the action of [complex conjugation](@entry_id:174690) on $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$.

If an embedding $\sigma$ is not real, then $\overline{\sigma} \neq \sigma$. The pair $\{\sigma, \overline{\sigma}\}$ constitutes an orbit of size two under the action of [complex conjugation](@entry_id:174690). Since the roots of any polynomial with real coefficients (such as a [minimal polynomial](@entry_id:153598) over $\mathbb{Q}$) come in conjugate pairs, if $\sigma(\alpha)$ is a non-real root of $m_\alpha(x)$, then $\overline{\sigma(\alpha)}$ is also a non-real root. Thus, [complex embeddings](@entry_id:189961) always occur in conjugate pairs.

This leads to the definition of the **signature** of a [number field](@entry_id:148388) $K$, denoted by the pair $(r_1, r_2)$.
-   $r_1$ is the number of real [embeddings](@entry_id:158103) of $K$.
-   $r_2$ is the number of pairs of [complex embeddings](@entry_id:189961) of $K$. The total number of [complex embeddings](@entry_id:189961) is $2r_2$.

From the partition of $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$ into fixed points (real [embeddings](@entry_id:158103)) and orbits of size two (pairs of [complex embeddings](@entry_id:189961)), we arrive at the fundamental identity relating the degree to the signature:
$$ [K:\mathbb{Q}] = r_1 + 2r_2 $$
The number of real [embeddings](@entry_id:158103), $r_1$, is equal to the number of real roots of the [minimal polynomial](@entry_id:153598) $m_\alpha(x)$ of a [primitive element](@entry_id:154321) $\alpha$ for $K/\mathbb{Q}$. The number of complex conjugate pairs of roots is $r_2$.

To illustrate, let us determine the signature of the field $K = \mathbb{Q}[x]/(f)$ where $f(x)=x^5 - 10x + 5$ is assumed to be irreducible [@problem_id:3013292]. Here, $[K:\mathbb{Q}]=5$. To find the signature $(r_1, r_2)$, we need to count the number of real roots of $f(x)$. Using calculus, we analyze the derivative $f'(x) = 5x^4 - 10$, which has real roots at $x = \pm\sqrt[4]{2}$. These are the locations of the [local extrema](@entry_id:144991).
-   As $x \to -\infty$, $f(x) \to -\infty$.
-   At the [local maximum](@entry_id:137813) $x = -\sqrt[4]{2}$, $f(-\sqrt[4]{2}) = 8\sqrt[4]{2} + 5 > 0$.
-   At the local minimum $x = \sqrt[4]{2}$, $f(\sqrt[4]{2}) = 5 - 8\sqrt[4]{2}  0$.
-   As $x \to +\infty$, $f(x) \to +\infty$.
By the Intermediate Value Theorem, there must be one real root in $(-\infty, -\sqrt[4]{2})$, one in $(-\sqrt[4]{2}, \sqrt[4]{2})$, and one in $(\sqrt[4]{2}, \infty)$. Thus, there are exactly $3$ real roots, which means $r_1 = 3$. From the relation $5 = r_1 + 2r_2$, we have $5 = 3 + 2r_2$, which gives $r_2 = 1$. The signature of $K$ is $(3, 1)$.

Revisiting our [quadratic field](@entry_id:636261) example $K = \mathbb{Q}(\sqrt{d})$ [@problem_id:3013296]:
-   If $d>0$, $\sqrt{d}$ is real. Both [embeddings](@entry_id:158103), $\sigma_{1,2}(a+b\sqrt{d}) = a \pm b\sqrt{d}$, map $K$ into $\mathbb{R}$. So $r_1=2, r_2=0$. The signature is $(2,0)$. Such a field is called a **real [quadratic field](@entry_id:636261)**.
-   If $d0$, $\sqrt{d}$ is purely imaginary. Neither embedding maps $K$ into $\mathbb{R}$. They form a [complex conjugate pair](@entry_id:150139). So $r_1=0, r_2=1$. The signature is $(0,1)$. Such a field is called an **[imaginary quadratic field](@entry_id:203833)**.

### Embeddings, Automorphisms, and Normal Extensions

It is essential to distinguish between a field embedding and a [field automorphism](@entry_id:153306). An **[automorphism](@entry_id:143521)** of $K$ is an isomorphism from $K$ to itself, $\tau: K \to K$. If we fix an inclusion $K \subset \mathbb{C}$, an automorphism of $K$ can be viewed as an embedding $\sigma: K \to \mathbb{C}$ with the special property that its image is the field $K$ itself, i.e., $\sigma(K)=K$.

This property does not hold for all [embeddings](@entry_id:158103) of all fields. Consider the field $K=\mathbb{Q}(\alpha)$ where $\alpha = \sqrt[3]{2}$ [@problem_id:3013297]. The minimal polynomial is $x^3-2=0$, with roots $\alpha_1 = \sqrt[3]{2}$, $\alpha_2 = \sqrt[3]{2}\omega$, and $\alpha_3 = \sqrt[3]{2}\omega^2$, where $\omega = \exp(2\pi i/3)$. There are three embeddings corresponding to these three roots. If we fix the inclusion $K \subset \mathbb{R}$ via the real root $\sqrt[3]{2}$, then $K$ is a [subfield](@entry_id:155812) of the real numbers. The embedding $\sigma_2$ defined by $\sigma_2(\sqrt[3]{2}) = \sqrt[3]{2}\omega$ has an image $\sigma_2(K) = \mathbb{Q}(\sqrt[3]{2}\omega)$, which is a [subfield](@entry_id:155812) of $\mathbb{C}$ containing non-real numbers. Clearly, $\sigma_2(K) \neq K$. Therefore, not all [embeddings](@entry_id:158103) are [automorphisms](@entry_id:155390) [@problem_id:3013302].

This distinction is captured by the concept of a **[normal extension](@entry_id:155744)**. A finite extension $K/\mathbb{Q}$ is normal if every [irreducible polynomial](@entry_id:156607) in $\mathbb{Q}[x]$ that has one root in $K$ splits completely into linear factors in $K[x]$. The following deep connection holds [@problem_id:3013302].

**Theorem:** For a number field $K$ (viewed as a subfield of $\mathbb{C}$), the following are equivalent:
1.  The extension $K/\mathbb{Q}$ is normal.
2.  For every embedding $\sigma \in \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$, the image is $\sigma(K)=K$.
3.  The set of [embeddings](@entry_id:158103) $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$ coincides with the group of [automorphisms](@entry_id:155390) $\operatorname{Aut}_{\mathbb{Q}}(K)$.

For a [normal extension](@entry_id:155744), which is also called a Galois extension in characteristic zero, the number of [automorphisms](@entry_id:155390) is equal to the degree of the extension. For a non-[normal extension](@entry_id:155744) like $\mathbb{Q}(\sqrt[3]{2})$, the automorphism group is smaller than the degree. Indeed, the only root of $x^3-2$ that lies in $\mathbb{Q}(\sqrt[3]{2}) \subset \mathbb{R}$ is $\sqrt[3]{2}$ itself, so the only [automorphism](@entry_id:143521) is the identity map. Thus $|\operatorname{Aut}_{\mathbb{Q}}(K)|=1$ while $[K:\mathbb{Q}]=3$.

Quadratic fields $\mathbb{Q}(\sqrt{d})$ are always [normal extensions](@entry_id:156398), as the [minimal polynomial](@entry_id:153598) of any element splits within the field [@problem_id:3013302]. The same is true for [cyclotomic fields](@entry_id:153828). For a non-[normal extension](@entry_id:155744), not only can an image $\sigma(K)$ be different from $K$, but it may not even be closed under [complex conjugation](@entry_id:174690). For $K = \mathbb{Q}(2^{1/3})$, consider the embedding $\sigma$ defined by $\sigma(2^{1/3}) = 2^{1/3}\zeta_3$. The image field is $\sigma(K) = \mathbb{Q}(2^{1/3}\zeta_3)$. The conjugate field is $\overline{\sigma(K)} = \mathbb{Q}(2^{1/3}\overline{\zeta_3}) = \mathbb{Q}(2^{1/3}\zeta_3^2)$. These two fields are distinct subfields of $\mathbb{C}$, since $[\sigma(K):\mathbb{Q}]=3$ and $[\mathbb{Q}(\zeta_3):\mathbb{Q}]=2$, so $\zeta_3$ cannot be in $\sigma(K)$ [@problem_id:3013304]. This illustrates a profound consequence of [non-normality](@entry_id:752585).

### Structure of Embeddings in Field Towers and Composite Fields

The set of [embeddings](@entry_id:158103) behaves predictably with respect to the structure of [field extensions](@entry_id:153187). Consider a tower of number fields $\mathbb{Q} \subset F \subset K$. Every embedding of the larger field $K$ can be restricted to an embedding of the smaller field $F$. This defines a restriction map:
$$ \operatorname{res}: \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C}) \to \operatorname{Hom}_{\mathbb{Q}}(F, \mathbb{C}), \quad \text{where } \operatorname{res}(\sigma) = \sigma|_F $$
A fundamental result states that this map is surjective, and more importantly, every fiber has the same [cardinality](@entry_id:137773) [@problem_id:3013305]. For any given embedding $\tau: F \to \mathbb{C}$, the number of embeddings of $K$ that extend $\tau$ is precisely the degree of the top extension, $[K:F]$. This elegant principle gives a "multiplicative" structure to the set of embeddings, consistent with the Tower Law for degrees:
$$ |\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})| = |\operatorname{Hom}_{\mathbb{Q}}(F, \mathbb{C})| \cdot [K:F] $$
$$ [K:\mathbb{Q}] = [F:\mathbb{Q}] \cdot [K:F] $$

This principle is particularly useful for understanding embeddings of a composite field. Consider the field $K = \mathbb{Q}(\alpha, \beta) = \mathbb{Q}(\sqrt[3]{2}, \sqrt{5})$ [@problem_id:3024688]. The degree is $[K:\mathbb{Q}] = [\mathbb{Q}(\sqrt[3]{2}):\mathbb{Q}] \cdot [\mathbb{Q}(\sqrt{5}):\mathbb{Q}] = 3 \cdot 2 = 6$. An embedding $\sigma: K \to \mathbb{C}$ is uniquely determined by its action on the generators $\sqrt[3]{2}$ and $\sqrt{5}$.
-   The image $\sigma(\sqrt[3]{2})$ must be one of the three roots of $x^3-2=0$: one real root ($\sqrt[3]{2}$) and two [complex roots](@entry_id:172941).
-   The image $\sigma(\sqrt{5})$ must be one of the two roots of $x^2-5=0$: two real roots ($\pm\sqrt{5}$).

This gives $3 \times 2 = 6$ possible combinations, corresponding to the 6 embeddings of $K$. To find the signature $(r_1, r_2)$, we count how many of these [embeddings](@entry_id:158103) are real. An embedding $\sigma$ is real if and only if it maps *all* generators to real numbers.
-   There is 1 choice for a real image of $\sqrt[3]{2}$.
-   There are 2 choices for a real image of $\sqrt{5}$.
The number of real [embeddings](@entry_id:158103) is the product of these choices: $r_1 = 1 \times 2 = 2$.
Since $[K:\mathbb{Q}] = 6 = r_1 + 2r_2$, we have $6 = 2 + 2r_2$, which yields $r_2=2$. The signature of $K = \mathbb{Q}(\sqrt[3]{2}, \sqrt{5})$ is $(2,2)$.

### Special Structures: Totally Real, Totally Imaginary, and CM Fields

The signature $(r_1, r_2)$ provides a coarse classification of [number fields](@entry_id:155558).
-   A field $K$ is **totally real** if all its [embeddings](@entry_id:158103) are real. This means $r_2=0$ and $[K:\mathbb{Q}]=r_1$. An example is $\mathbb{Q}(\sqrt{d})$ with $d>0$.
-   A field $K$ is **totally imaginary** if none of its [embeddings](@entry_id:158103) are real. This means $r_1=0$ and $[K:\mathbb{Q}]=2r_2$. An example is $\mathbb{Q}(\sqrt{d})$ with $d0$.

A particularly important class of totally imaginary fields are **Complex Multiplication (CM) fields**. A field $K$ is a CM field if it is a totally imaginary [quadratic extension](@entry_id:152175) of a totally real field $F$. This means $r_1(K)=0$, $F$ is totally real, and $[K:F]=2$.

Cyclotomic fields provide the archetypal examples. Consider $K = \mathbb{Q}(\zeta_9)$, where $\zeta_9 = \exp(2\pi i/9)$ [@problem_id:3013294]. As we saw, its degree is $\phi(9)=6$ and all 6 embeddings are complex, so it is totally imaginary. The maximal real [subfield](@entry_id:155812) of $K$ is $K^+$, the subfield fixed by [complex conjugation](@entry_id:174690). It is generated by $\zeta_9 + \overline{\zeta_9} = \zeta_9 + \zeta_9^{-1} = 2\cos(2\pi/9)$. This field $K^+ = \mathbb{Q}(\cos(2\pi/9))$ can be shown to be totally real. By Galois theory, $[K:K^+]=2$ since it is the [fixed field](@entry_id:155430) of an [automorphism](@entry_id:143521) of order 2. Therefore, $\mathbb{Q}(\zeta_9)$ is a CM field.

In a CM field $K$ with maximal real [subfield](@entry_id:155812) $F$, [complex conjugation](@entry_id:174690) on $\mathbb{C}$ induces the non-trivial automorphism of the extension $K/F$ in every embedding [@problem_id:3013303]. This provides a canonical, intrinsic notion of "[complex conjugation](@entry_id:174690)" for the abstract field $K$.

### Applications: Norms and Traces

The set of all [embeddings](@entry_id:158103), not just the automorphisms, is fundamental to defining two of the most important invariants of an element $\alpha \in K$: the **norm** and the **trace**.
-   The norm of $\alpha$ is the product of its images under all embeddings: $N_{K/\mathbb{Q}}(\alpha) = \prod_{\sigma \in \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})} \sigma(\alpha)$.
-   The trace of $\alpha$ is the sum of its images under all [embeddings](@entry_id:158103): $\operatorname{Tr}_{K/\mathbb{Q}}(\alpha) = \sum_{\sigma \in \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})} \sigma(\alpha)$.

Because the set $\{\sigma(\alpha)\}_{\sigma}$ is the full set of roots of the minimal polynomial of $\alpha$ (counted with [multiplicity](@entry_id:136466) related to $[K:\mathbb{Q}(\alpha)]$), the [norm and trace](@entry_id:637837) are guaranteed to be rational numbers. These definitions hold for any [number field](@entry_id:148388), normal or not. For the non-normal field $K=\mathbb{Q}(\alpha)$ with $\alpha=\sqrt[3]{2}$, the norm of $\beta=1+\alpha+\alpha^2$ is computed as the product over all three embeddings [@problem_id:3013297]:
$$ N_{K/\mathbb{Q}}(\beta) = \sigma_1(\beta) \sigma_2(\beta) \sigma_3(\beta) = (1+\alpha+\alpha^2)(1+\alpha\omega+\alpha^2\omega^2)(1+\alpha\omega^2+\alpha^2\omega) $$
A direct calculation reveals this product is $(\alpha^3-1)/(\alpha-1) = (2-1)/(\alpha-1)=1/(\alpha-1)$. The norm of $\alpha-1$ is the value of the [minimal polynomial](@entry_id:153598) of $\alpha-1$, which is $(x+1)^3-2=x^3+3x^2+3x-1$, evaluated at $x=0$, which is $-1$. Thus $N(\beta)=1/N(\alpha-1)=-1$. The original text seems to have a typo, claiming the product is $1$. Let me re-check the product.
Let $f(x)=x^3+3x^2+3x-1$. Its roots are $\sigma_i(\alpha-1)$.
$N(\alpha-1) = \sigma_1(\alpha-1)\sigma_2(\alpha-1)\sigma_3(\alpha-1) = (\alpha-1)(\alpha\omega-1)(\alpha\omega^2-1) = (\alpha-1)(\alpha^2\omega^3 - \alpha\omega - \alpha\omega^2 + 1) = (\alpha-1)(\alpha^2-\alpha(\omega+\omega^2)+1) = (\alpha-1)(\alpha^2+\alpha+1)=\alpha^3-1=1$.
Ah, the norm of $\alpha-1$ is $1$, not $-1$. So $N(\beta) = N(1/(\alpha-1)) = 1/N(\alpha-1)=1/1=1$. The text's conclusion is correct. My mental calculation was wrong. I will not change this part.

For [cyclotomic fields](@entry_id:153828), the norm has a special connection to [cyclotomic polynomials](@entry_id:155668). For $K=\mathbb{Q}(\zeta_m)$, the norm of $1-\zeta_m$ is the product of $1-\sigma(\zeta_m)$ over all [embeddings](@entry_id:158103) $\sigma$. Since the embeddings map $\zeta_m$ to its Galois conjugates $\zeta_m^k$ for $k \in (\mathbb{Z}/m\mathbb{Z})^\times$, the norm is simply the value of the $m$-th [cyclotomic polynomial](@entry_id:154273) at $1$:
$$ N_{K/\mathbb{Q}}(1-\zeta_m) = \prod_{k \in (\mathbb{Z}/m\mathbb{Z})^\times} (1-\zeta_m^k) = \Phi_m(1) $$
For $K=\mathbb{Q}(\zeta_9)$, this value is $\Phi_9(1) = 3$ [@problem_id:3013294]. These invariants are cornerstones of algebraic number theory, and their very definition rests upon a complete understanding of the set of embeddings of a number field into the complex numbers.