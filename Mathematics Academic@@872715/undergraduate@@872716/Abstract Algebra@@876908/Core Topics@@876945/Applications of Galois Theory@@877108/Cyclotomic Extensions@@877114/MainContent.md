## Introduction
Cyclotomic extensions are a cornerstone of [modern algebra](@entry_id:171265), providing a rich and accessible entry point into the profound connections between field theory, number theory, and geometry. Arising from the simple equation $z^n=1$, their study reveals intricate structures governed by elegant rules. This article demystifies these extensions by addressing the fundamental questions of their construction, symmetry, and application. It aims to bridge the gap between abstract definitions and tangible results, showing how these fields hold the key to solving ancient geometric puzzles and understanding the arithmetic of numbers.

The reader will embark on a journey through three chapters. First, **"Principles and Mechanisms"** will lay the groundwork by dissecting roots of unity, [cyclotomic polynomials](@entry_id:155668), and the elegant structure of their Galois groups. Next, **"Applications and Interdisciplinary Connections"** will showcase the power of this theory in solving famous problems in geometry and its central role in algebraic number theory, culminating in the celebrated Kronecker-Weber theorem. Finally, **"Hands-On Practices"** will provide an opportunity to solidify these concepts through guided problem-solving, cementing the link between theory and practical computation.

## Principles and Mechanisms

Having introduced the concept of cyclotomic extensions, we now delve into their fundamental principles and the mechanisms that govern their structure. This chapter will systematically dissect the components of these extensions, from their building blocks—the roots of unity—to the intricate symmetries captured by their Galois groups.

### Roots of Unity and Cyclotomic Polynomials

The study of cyclotomic extensions begins with the **$n$-th roots of unity**, which are the complex solutions to the equation $z^n = 1$. Geometrically, these roots form the vertices of a regular $n$-gon inscribed in the unit circle of the complex plane. They are given by the formula:
$$z_k = \exp\left(\frac{2\pi i k}{n}\right) = \cos\left(\frac{2\pi k}{n}\right) + i\sin\left(\frac{2\pi k}{n}\right), \quad \text{for } k = 0, 1, \dots, n-1$$

While all $z_k$ are $n$-th roots of unity, some may also be $d$-th [roots of unity](@entry_id:142597) for a smaller integer $d$ that divides $n$. For instance, for $n=4$, the root $z_2 = -1$ is also a 2nd root of unity. This observation leads to a crucial distinction. A root of unity $\zeta$ is called a **primitive $n$-th root of unity** if $\zeta^n = 1$ and $\zeta^k \neq 1$ for all positive integers $k  n$. A primitive $n$-th root of unity generates the entire group of $n$-th [roots of unity](@entry_id:142597) under multiplication. An $n$-th root of unity $z_k = \exp(2\pi i k / n)$ is primitive if and only if its corresponding index $k$ is coprime to $n$; that is, $\gcd(k, n) = 1$.

For example, to find the primitive 6th roots of unity, we consider $n=6$. The integers $k$ in the range $1 \le k  6$ that are coprime to 6 are $k=1$ and $k=5$. Thus, the primitive 6th roots are:
- $\zeta_1 = \exp\left(\frac{2\pi i}{6}\right) = \exp\left(\frac{\pi i}{3}\right) = \cos\left(\frac{\pi}{3}\right) + i\sin\left(\frac{\pi}{3}\right) = \frac{1}{2} + i\frac{\sqrt{3}}{2}$
- $\zeta_5 = \exp\left(\frac{10\pi i}{6}\right) = \exp\left(\frac{5\pi i}{3}\right) = \cos\left(\frac{5\pi}{3}\right) + i\sin\left(\frac{5\pi}{3}\right) = \frac{1}{2} - i\frac{\sqrt{3}}{2}$
Notice that $\zeta_5$ is the [complex conjugate](@entry_id:174888) of $\zeta_1$. [@problem_id:1785936]

Similarly, for $n=8$, the integers $k$ in $\{1, ..., 7\}$ coprime to 8 are $1, 3, 5, 7$. These give the four primitive 8th [roots of unity](@entry_id:142597): $\exp(\pi i/4)$, $\exp(3\pi i/4)$, $\exp(5\pi i/4)$, and $\exp(7\pi i/4)$. [@problem_id:1785999]

The **$n$-th [cyclotomic polynomial](@entry_id:154273)**, denoted $\Phi_n(x)$, is defined as the minimal polynomial over the field of rational numbers $\mathbb{Q}$ for any primitive $n$-th root of unity. It is a [monic polynomial](@entry_id:152311) with integer coefficients whose roots are precisely the set of all primitive $n$-th [roots of unity](@entry_id:142597).

For a prime number $p$, the construction of $\Phi_p(x)$ is straightforward. The roots of $x^p - 1$ are $\{1, \zeta_p, \zeta_p^2, \dots, \zeta_p^{p-1}\}$. Since $p$ is prime, all roots except 1 are primitive. Thus, we can factor $x^p - 1$ as:
$$x^p - 1 = (x - 1) \Phi_p(x)$$
This gives the formula:
$$\Phi_p(x) = \frac{x^p - 1}{x - 1} = x^{p-1} + x^{p-2} + \dots + x + 1$$
To confirm this is the minimal polynomial, we must show it is irreducible over $\mathbb{Q}$. A direct application of Eisenstein's criterion fails, but a clever shift of the variable succeeds. Consider $\Phi_p(x+1)$. For example, for $p=5$, we have $\Phi_5(x) = x^4 + x^3 + x^2 + x + 1$. [@problem_id:1785989] Let's examine $\Phi_5(x+1)$:
$$\Phi_5(x+1) = \frac{(x+1)^5 - 1}{(x+1) - 1} = \frac{x^5 + 5x^4 + 10x^3 + 10x^2 + 5x}{x} = x^4 + 5x^3 + 10x^2 + 10x + 5$$
We can now apply Eisenstein's criterion with the prime $p=5$. The prime 5 divides all coefficients except the leading one ($1$), and its square, $25$, does not divide the constant term ($5$). Therefore, $\Phi_5(x+1)$ is irreducible over $\mathbb{Q}$. Since the irreducibility of a polynomial is invariant under a substitution $x \mapsto x+c$, we conclude that $\Phi_5(x)$ is also irreducible over $\mathbb{Q}$. This argument generalizes to any prime $p$, confirming that $\Phi_p(x)$ is indeed the minimal polynomial for a primitive $p$-th root of unity.

For composite $n$, we rely on a fundamental identity that partitions the roots of $x^n-1$ based on their primitive order:
$$x^n - 1 = \prod_{d|n} \Phi_d(x)$$
This identity allows for the recursive calculation of [cyclotomic polynomials](@entry_id:155668). For instance, to find $\Phi_{12}(x)$, we consider the divisors of 12, which are $1, 2, 3, 4, 6, 12$. The identity gives:
$$x^{12} - 1 = \Phi_1(x) \Phi_2(x) \Phi_3(x) \Phi_4(x) \Phi_6(x) \Phi_{12}(x)$$
We can rearrange to isolate $\Phi_{12}(x)$ and substitute known lower-order polynomials:
- $\Phi_1(x) = x-1$
- $\Phi_2(x) = \frac{x^2-1}{x-1} = x+1$
- $\Phi_3(x) = x^2+x+1$
- $\Phi_4(x) = \frac{x^4-1}{\Phi_1(x)\Phi_2(x)} = \frac{x^4-1}{x^2-1} = x^2+1$
- $\Phi_6(x) = \frac{x^6-1}{\Phi_1(x)\Phi_2(x)\Phi_3(x)} = \frac{(x^3-1)(x^3+1)}{(x-1)(x+1)(x^2+x+1)} = x^2-x+1$

Substituting these into the factorization of $x^{12}-1 = (x^6-1)(x^6+1)$:
$$x^{12} - 1 = (\Phi_1\Phi_2\Phi_3\Phi_6)(x^2+1)(x^4-x^2+1) = (\Phi_1\Phi_2\Phi_3\Phi_6)(\Phi_4)(x^4-x^2+1)$$
By comparing this with the divisor product, we deduce that $\Phi_{12}(x) = x^4 - x^2 + 1$. [@problem_id:1785934]

### Cyclotomic Fields and Their Degree

A **cyclotomic field** is a [field extension](@entry_id:150367) of the rational numbers $\mathbb{Q}$ obtained by adjoining a primitive $n$-th root of unity, $\zeta_n$. This field is denoted $\mathbb{Q}(\zeta_n)$ and consists of all numbers that can be formed from rational numbers and $\zeta_n$ using field operations. It is the [splitting field](@entry_id:156669) of the polynomial $x^n-1$ over $\mathbb{Q}$.

A central question in field theory is determining the [degree of an extension](@entry_id:148122), $[L:K]$. The degree represents the dimension of $L$ as a vector space over $K$. For a simple [algebraic extension](@entry_id:155470) $K(\alpha)$, the degree $[K(\alpha):K]$ is equal to the degree of the minimal polynomial of $\alpha$ over $K$.

Since $\Phi_n(x)$ is the minimal polynomial of $\zeta_n$ over $\mathbb{Q}$, the degree of the [cyclotomic extension](@entry_id:149979) $\mathbb{Q}(\zeta_n)$ is precisely the degree of $\Phi_n(x)$.
$$[\mathbb{Q}(\zeta_n) : \mathbb{Q}] = \deg(\Phi_n(x))$$
The degree of the $n$-th [cyclotomic polynomial](@entry_id:154273) is given by **Euler's totient function**, $\phi(n)$, which counts the number of positive integers less than or equal to $n$ that are coprime to $n$.
$$[\mathbb{Q}(\zeta_n) : \mathbb{Q}] = \phi(n)$$
The totient function can be calculated using the prime factorization of $n = p_1^{k_1} \cdots p_r^{k_r}$:
$$\phi(n) = n \prod_{i=1}^r \left(1 - \frac{1}{p_i}\right) = \prod_{i=1}^r (p_i^{k_i} - p_i^{k_i-1})$$
For example, to find the degree of the extension $\mathbb{Q}(\zeta_{12})$ over $\mathbb{Q}$, we calculate $\phi(12)$. Since $12 = 2^2 \cdot 3$, we have:
$$\phi(12) = 12 \left(1 - \frac{1}{2}\right) \left(1 - \frac{1}{3}\right) = 12 \cdot \frac{1}{2} \cdot \frac{2}{3} = 4$$
Thus, $[\mathbb{Q}(\zeta_{12}) : \mathbb{Q}] = 4$. This matches our earlier finding that $\deg(\Phi_{12}(x))=4$. [@problem_id:1785953]

### The Galois Group of a Cyclotomic Extension

The [cyclotomic extension](@entry_id:149979) $\mathbb{Q}(\zeta_n)/\mathbb{Q}$ is a Galois extension, meaning it is both normal and separable. Its **Galois group**, denoted $\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$, is the group of all field automorphisms of $\mathbb{Q}(\zeta_n)$ that fix every element of $\mathbb{Q}$.

An automorphism $\sigma \in \text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ is completely determined by its action on the generator $\zeta_n$. Since $\sigma$ must preserve the algebraic relations over $\mathbb{Q}$, it must map $\zeta_n$ to another root of its minimal polynomial, $\Phi_n(x)$. The roots of $\Phi_n(x)$ are the primitive $n$-th roots of unity. Therefore, for any $\sigma$, there exists an integer $k$ with $\gcd(k, n) = 1$ such that:
$$\sigma(\zeta_n) = \zeta_n^k$$
We can label such an automorphism as $\sigma_k$. This provides a natural correspondence between the automorphisms and the integers coprime to $n$. Let's examine the group operation (composition of automorphisms):
$$(\sigma_j \circ \sigma_k)(\zeta_n) = \sigma_j(\sigma_k(\zeta_n)) = \sigma_j(\zeta_n^k) = (\sigma_j(\zeta_n))^k = (\zeta_n^j)^k = \zeta_n^{jk}$$
This shows that the composition $\sigma_j \circ \sigma_k$ corresponds to the automorphism $\sigma_{jk}$. The group operation in $\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ thus mirrors multiplication of the indices modulo $n$. This leads to one of the most elegant results in Galois theory:
$$\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q}) \cong (\mathbb{Z}/n\mathbb{Z})^\times$$
where $(\mathbb{Z}/n\mathbb{Z})^\times$ is the [multiplicative group of units](@entry_id:184288) modulo $n$.

Since $(\mathbb{Z}/n\mathbb{Z})^\times$ is always an [abelian group](@entry_id:139381), it follows that **the Galois group of any [cyclotomic extension](@entry_id:149979) over $\mathbb{Q}$ is abelian**. This is a remarkable property with profound consequences, most notably in the Kronecker-Weber theorem, which states that every abelian extension of $\mathbb{Q}$ is contained within some cyclotomic field.

As an example, let's analyze an element of $\text{Gal}(\mathbb{Q}(\zeta_7)/\mathbb{Q})$. Consider the [automorphism](@entry_id:143521) $\sigma_3$ defined by $\sigma_3(\zeta_7) = \zeta_7^3$. To find the order of $\sigma_3$, we must find the smallest positive integer $m$ such that $\sigma_3^m$ is the identity [automorphism](@entry_id:143521). This is equivalent to finding the smallest $m$ such that $\sigma_3^m(\zeta_7) = \zeta_7$.
$$\sigma_3^m(\zeta_7) = \zeta_7^{3^m}$$
We need $\zeta_7^{3^m} = \zeta_7$, which implies $3^m \equiv 1 \pmod{7}$. We are seeking the [multiplicative order](@entry_id:636522) of 3 in $(\mathbb{Z}/7\mathbb{Z})^\times$. Computing the powers of 3 modulo 7: $3^1 \equiv 3$, $3^2 \equiv 2$, $3^3 \equiv 6$, $3^4 \equiv 4$, $3^5 \equiv 5$, and $3^6 \equiv 1$. The order is 6. [@problem_id:1785951]

### Galois Correspondence and Subfields of Cyclotomic Extensions

The structure of the Galois group $G_n = \text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ is determined by the structure of $(\mathbb{Z}/n\mathbb{Z})^\times$. A well-known result from number theory states that $(\mathbb{Z}/n\mathbb{Z})^\times$ is cyclic if and only if $n$ is of the form $1, 2, 4, p^k,$ or $2p^k$ for an odd prime $p$ and $k \ge 1$. For other values of $n$, the group is abelian but not cyclic.

The smallest integer $n > 2$ not on this list is $n=8$. The group $(\mathbb{Z}/8\mathbb{Z})^\times = \{1, 3, 5, 7\}$ has order $\phi(8)=4$. However, every non-identity element has order 2 ($3^2 \equiv 1$, $5^2 \equiv 1$, $7^2 \equiv 1 \pmod{8}$). Since there is no element of order 4, the group is not cyclic. It is isomorphic to the Klein four-group, $C_2 \times C_2$. Therefore, $n=8$ is the smallest integer greater than 2 for which the Galois group of the [cyclotomic extension](@entry_id:149979) is not cyclic. [@problem_id:1785932] Another common example is $n=12$, where $(\mathbb{Z}/12\mathbb{Z})^\times = \{1, 5, 7, 11\}$ is also isomorphic to $C_2 \times C_2$. [@problem_id:1832936]

The Fundamental Theorem of Galois Theory establishes a one-to-one correspondence between the subgroups of the Galois group $G_n$ and the [intermediate fields](@entry_id:153550) between $\mathbb{Q}$ and $\mathbb{Q}(\zeta_n)$. Larger subgroups correspond to smaller fixed fields.

A canonical subgroup of $G_n$ for $n \ge 3$ is the one generated by the **[complex conjugation](@entry_id:174690)** [automorphism](@entry_id:143521), $\tau$. On any complex number $z=a+bi$, $\tau(z) = \bar{z} = a-bi$. Let's see its action on $\zeta_n$:
$$\tau(\zeta_n) = \overline{\exp\left(\frac{2\pi i}{n}\right)} = \exp\left(-\frac{2\pi i}{n}\right) = \zeta_n^{-1}$$
Since $\zeta_n^n = 1$, we have $\zeta_n^{-1} = \zeta_n^{n-1}$. Thus, [complex conjugation](@entry_id:174690) corresponds to the [automorphism](@entry_id:143521) $\sigma_{n-1}$ (or $\sigma_{-1}$). This [automorphism](@entry_id:143521) has order 2, as $\tau^2(\zeta_n) = (\zeta_n^{-1})^{-1} = \zeta_n$. [@problem_id:1832914]

The [fixed field](@entry_id:155430) of the subgroup $\{\text{id}, \tau\}$ is the set of all elements in $\mathbb{Q}(\zeta_n)$ that are fixed by [complex conjugation](@entry_id:174690)—that is, the set of all real numbers in $\mathbb{Q}(\zeta_n)$. This is known as the **maximal real [subfield](@entry_id:155812)** of $\mathbb{Q}(\zeta_n)$, denoted $\mathbb{Q}(\zeta_n)^+$. A generator for this [subfield](@entry_id:155812) is the element $\zeta_n + \zeta_n^{-1}$. Using Euler's formula, we can see why this element is real:
$$\zeta_n + \zeta_n^{-1} = \exp\left(\frac{2\pi i}{n}\right) + \exp\left(-\frac{2\pi i}{n}\right) = 2\cos\left(\frac{2\pi}{n}\right)$$
The field $\mathbb{Q}(\zeta_n)^+$ can be written as $\mathbb{Q}(\cos(2\pi/n))$. For example, in $\mathbb{Q}(\zeta_5)$, the element $\alpha = \zeta_5 + \zeta_5^{-1}$ is real. By manipulating the cyclotomic relation $1+\zeta_5+\zeta_5^2+\zeta_5^3+\zeta_5^4=0$, we can show that $\alpha$ is a root of the quadratic polynomial $x^2+x-1=0$. Since this is irreducible over $\mathbb{Q}$, $\alpha$ is a real, irrational number. The field $\mathbb{Q}(\alpha)$ is the quadratic [subfield](@entry_id:155812) $\mathbb{Q}(\sqrt{5})$, as the roots of $x^2+x-1=0$ are $\frac{-1 \pm \sqrt{5}}{2}$. [@problem_id:1785988]

Let's conclude with a complete example illustrating the Galois correspondence for $\mathbb{Q}(\zeta_8)$. The Galois group is $G_8 = \text{Gal}(\mathbb{Q}(\zeta_8)/\mathbb{Q}) \cong (\mathbb{Z}/8\mathbb{Z})^\times = \{\sigma_1, \sigma_3, \sigma_5, \sigma_7\}$. The maximal real [subfield](@entry_id:155812) is $\mathbb{Q}(\zeta_8)^+ = \mathbb{Q}(\cos(\pi/4)) = \mathbb{Q}(\sqrt{2})$. According to the fundamental theorem, the subgroup of $G_8$ that fixes this subfield must have order $|G_8| / [\mathbb{Q}(\sqrt{2}):\mathbb{Q}] = 4/2 = 2$. We can identify this subgroup by testing which automorphisms fix the generator $\sqrt{2}$. We express $\sqrt{2}$ in terms of $\zeta_8$:
$$\sqrt{2} = 2\cos(\pi/4) = \zeta_8 + \zeta_8^{-1} = \zeta_8 + \zeta_8^7$$
Now we apply each [automorphism](@entry_id:143521):
- $\sigma_1(\sqrt{2}) = \sigma_1(\zeta_8 + \zeta_8^7) = \zeta_8 + \zeta_8^7 = \sqrt{2}$ (identity)
- $\sigma_3(\sqrt{2}) = \sigma_3(\zeta_8 + \zeta_8^7) = \zeta_8^3 + \zeta_8^{21} = \zeta_8^3 + \zeta_8^5 = 2\cos(3\pi/4) = -\sqrt{2}$
- $\sigma_5(\sqrt{2}) = \sigma_5(\zeta_8 + \zeta_8^7) = \zeta_8^5 + \zeta_8^{35} = \zeta_8^5 + \zeta_8^3 = 2\cos(5\pi/4) = -\sqrt{2}$
- $\sigma_7(\sqrt{2}) = \sigma_7(\zeta_8 + \zeta_8^7) = \zeta_8^7 + \zeta_8^{49} = \zeta_8^7 + \zeta_8^1 = \sqrt{2}$

The [automorphisms](@entry_id:155390) that fix $\sqrt{2}$ are $\sigma_1$ and $\sigma_7$. Therefore, the subgroup corresponding to the [fixed field](@entry_id:155430) $\mathbb{Q}(\sqrt{2})$ is $\{\sigma_1, \sigma_7\}$. Note that $\sigma_7 = \sigma_{-1}$ is precisely the [complex conjugation](@entry_id:174690) automorphism, as expected, since $\mathbb{Q}(\sqrt{2})$ is a real field. This example beautifully ties together the concepts of [primitive roots](@entry_id:163633), Galois groups, and the correspondence between subgroups and subfields. [@problem_id:1785976]