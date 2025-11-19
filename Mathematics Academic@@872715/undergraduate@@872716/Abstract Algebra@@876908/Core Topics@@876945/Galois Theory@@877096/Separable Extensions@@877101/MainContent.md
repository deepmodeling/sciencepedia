## Introduction
In the study of [field extensions](@entry_id:153187), the [roots of polynomials](@entry_id:154615) are of central importance. While the degree of a polynomial indicates the maximum number of its roots, it does not tell us whether these roots are distinct or repeated. This distinction is not merely a technical detail; it forms a critical foundation for understanding the symmetries of fields and is a cornerstone of Galois theory. This article addresses the fundamental concept of separability, which provides the theoretical framework for analyzing [repeated roots](@entry_id:151486).

We will embark on a comprehensive exploration of this topic, structured across three chapters. In the first chapter, 'Principles and Mechanisms,' we will define separability using the algebraic tool of the [formal derivative](@entry_id:150637), investigate the conditions that lead to inseparable polynomials, and classify fields as perfect or imperfect. The second chapter, 'Applications and Interdisciplinary Connections,' will demonstrate the far-reaching consequences of separability in areas like [algebraic number](@entry_id:156710) theory and its elegant connection to linear algebra. Finally, the 'Hands-On Practices' chapter will provide a series of guided problems to solidify your understanding of these abstract concepts. This journey will illuminate how separability shapes the structure of [field extensions](@entry_id:153187) and their applications throughout modern algebra.

## Principles and Mechanisms

In our study of [field extensions](@entry_id:153187), a central theme is the analysis of [roots of polynomials](@entry_id:154615). While the degree of a polynomial tells us the maximum possible number of roots, it does not guarantee that these roots are all distinct. The distinction between polynomials with distinct roots and those with [repeated roots](@entry_id:151486) is foundational to Galois theory and the broader theory of fields. This leads to the crucial concept of separability.

### Separability of Polynomials: The Formal Derivative

An intuitive understanding of a repeated root of a polynomial, for instance $f(x)=(x-a)^2 g(x)$, suggests that the graph of the function $y=f(x)$ is tangent to the x-axis at $x=a$. In calculus, this corresponds to the condition that both $f(a)=0$ and its derivative $f'(a)=0$. While calculus is defined over the real or complex numbers, this derivative criterion can be formalized in a purely algebraic manner, applicable to any polynomial ring.

For a polynomial $f(x) = \sum_{k=0}^{n} c_k x^k$ in a polynomial ring $F[x]$, we define its **[formal derivative](@entry_id:150637)**, denoted $f'(x)$ or $\frac{d}{dx}f(x)$, as the polynomial:
$$f'(x) = \sum_{k=1}^{n} k c_k x^{k-1}$$
Here, the term $k c_k$ represents the sum of the coefficient $c_k$ with itself $k$ times. This definition requires no concept of limits and obeys the familiar sum and product rules of calculus.

The utility of the [formal derivative](@entry_id:150637) lies in the following fundamental theorem: A non-constant polynomial $f(x) \in F[x]$ has a repeated root in its [splitting field](@entry_id:156669) if and only if $f(x)$ and its derivative $f'(x)$ share a common factor of degree at least 1 in $F[x]$, i.e., $\gcd(f(x), f'(x)) \neq 1$.

If $\alpha$ is a repeated root of $f(x)$, we can write $f(x) = (x-\alpha)^m g(x)$ for some integer $m \ge 2$. Applying the product rule for derivatives gives $f'(x) = m(x-\alpha)^{m-1}g(x) + (x-\alpha)^m g'(x)$. It is clear that $(x-\alpha)$ is a factor of both terms, so $f'(\alpha) = 0$. This means $\alpha$ is a root of both $f(x)$ and $f'(x)$, implying that the minimal polynomial of $\alpha$ divides both $f(x)$ and $f'(x)$, and thus their [greatest common divisor](@entry_id:142947) is not a constant. Conversely, if $\gcd(f, f')$ has a root $\alpha$, then $\alpha$ is a root of both $f$ and $f'$. Since $\alpha$ is a root of $f'$, it must be a multiple root of $f$.

A polynomial that has no [repeated roots](@entry_id:151486) in its [splitting field](@entry_id:156669) is called a **[separable polynomial](@entry_id:149432)**. If it does have [repeated roots](@entry_id:151486), it is **inseparable**.

Consider the polynomial $f(x) = x^4 - 2x^2 + 1$ over the field of rational numbers $\mathbb{Q}$. Its [formal derivative](@entry_id:150637) is $f'(x) = 4x^3 - 4x$. To find common roots, we can find the roots of $f'(x)$: $4x(x^2-1) = 4x(x-1)(x+1)=0$, so the roots are $x=0, 1, -1$. We check these in the original polynomial: $f(0)=1 \neq 0$, but $f(1)=1-2+1=0$ and $f(-1)=1-2+1=0$. Since $x=1$ and $x=-1$ are common roots of $f(x)$ and $f'(x)$, they are [repeated roots](@entry_id:151486) of $f(x)$. Indeed, $f(x) = (x^2-1)^2 = (x-1)^2(x+1)^2$. Thus, $f(x)$ is an [inseparable polynomial](@entry_id:150131) [@problem_id:1820626].

### Perfect Fields and the Case of Characteristic Zero

The utility of the derivative criterion depends heavily on the characteristic of the base field $F$. Let us first consider fields of characteristic 0, such as $\mathbb{Q}$, $\mathbb{R}$, or $\mathbb{C}$.

Let $f(x)$ be an [irreducible polynomial](@entry_id:156607) of degree $n \ge 1$ over a field $F$ of characteristic 0. Its derivative, $f'(x)$, is a polynomial of degree $n-1$. Since the characteristic is 0, the leading coefficient $n a_n$ of $f'(x)$ is non-zero. Crucially, this means $f'(x)$ is not the zero polynomial.
Now, suppose $f(x)$ were inseparable. Then $\gcd(f(x), f'(x)) \neq 1$. Since $f(x)$ is irreducible, its only monic [divisor](@entry_id:188452) of positive degree is itself. This would imply that $f(x)$ must divide $f'(x)$. However, this is impossible, as a polynomial of degree $n$ cannot divide a non-zero polynomial of degree $n-1$. This contradiction forces us to conclude that $\gcd(f(x), f'(x)) = 1$.

This proves a profound result: **Every [irreducible polynomial](@entry_id:156607) over a field of characteristic zero is separable.**

This property is so fundamental that it motivates a new definition. A field $F$ is called a **[perfect field](@entry_id:156337)** if every [irreducible polynomial](@entry_id:156607) in $F[x]$ is separable. From our argument, it follows immediately that all fields of characteristic 0 are [perfect fields](@entry_id:152655) [@problem_id:1820631] [@problem_id:1820620].

### Inseparability: A Phenomenon of Prime Characteristic

The argument for separability in characteristic zero hinges on the fact that $f'(x)$ is never the zero polynomial for a non-constant $f(x)$. This can fail in a field $F$ of [prime characteristic](@entry_id:155979) $p$. In such a field, for any coefficient $c_k$, the term $kc_k$ in the derivative is zero if $p$ divides $k$.

Consider a polynomial $f(x) = \sum a_k x^k$. Its derivative is $f'(x) = \sum k a_k x^{k-1}$. For $f'(x)$ to be the zero polynomial, we must have $k a_k = 0$ for all $k \ge 1$. In a field of characteristic $p$, this means that for every non-zero coefficient $a_k$, its index $k$ must be a multiple of $p$. This implies that every power of $x$ with a non-zero coefficient is a multiple of $p$. Therefore, a non-constant polynomial $f(x)$ has a [zero derivative](@entry_id:145492) if and only if it is a polynomial in $x^p$. That is, $f(x)$ can be written in the form:
$$f(x) = b_m (x^p)^m + \dots + b_1 x^p + b_0 = g(x^p)$$
for some polynomial $g(y) \in F[y]$.

When an [irreducible polynomial](@entry_id:156607) $f(x)$ has a [zero derivative](@entry_id:145492), our previous argument breaks down. In this case, $\gcd(f(x), f'(x)) = \gcd(f(x), 0) = f(x)$, which is not a constant. Thus, such a polynomial is inseparable.

The canonical example of this phenomenon occurs over the field of [rational functions](@entry_id:154279) $\mathbb{F}_p(t)$, which consists of fractions of polynomials in an indeterminate $t$. Consider the polynomial $P(x) = x^p - t \in \mathbb{F}_p(t)[x]$. By Eisenstein's criterion, using the prime element $t$ in the ring $\mathbb{F}_p[t]$, this polynomial is irreducible over $\mathbb{F}_p(t)$ [@problem_id:1820631]. Its derivative is $P'(x) = p x^{p-1} - 0 = 0$, since the field has characteristic $p$.
Because $P(x)$ is both irreducible and has a [zero derivative](@entry_id:145492), it is an [inseparable polynomial](@entry_id:150131). In its [splitting field](@entry_id:156669), if $\alpha$ is a root such that $\alpha^p = t$, we can factor $P(x)$ using the "[freshman's dream](@entry_id:155678)" [binomial expansion](@entry_id:269603) $(a-b)^p = a^p - b^p$, which holds in characteristic $p$:
$$P(x) = x^p - t = x^p - \alpha^p = (x - \alpha)^p$$
This shows that the [irreducible polynomial](@entry_id:156607) $P(x)$ has only one distinct root, $\alpha$, with multiplicity $p$ [@problem_id:1820609]. The existence of such an irreducible [inseparable polynomial](@entry_id:150131) means that $\mathbb{F}_p(t)$ is not a [perfect field](@entry_id:156337). A similar conclusion holds for the polynomial $x^2 - u$ over the field $\mathbb{F}_2(u)$ [@problem_id:1820595].

### Classifying Perfect Fields: The Frobenius Automorphism

We have seen that fields of characteristic 0 are perfect, while fields like $\mathbb{F}_p(t)$ are not. This raises the question: which fields of characteristic $p$ are perfect? The answer is elegantly provided by the **Frobenius map**.

For a field $K$ of characteristic $p$, the Frobenius map $\phi: K \to K$ is defined by $\phi(a) = a^p$. This map is a [field homomorphism](@entry_id:155269) because $(a+b)^p = a^p+b^p$ and $(ab)^p = a^p b^p$. Since any [field homomorphism](@entry_id:155269) is injective, the Frobenius map is always an injective endomorphism.

A field $K$ of characteristic $p$ is perfect if and only if this Frobenius map is surjective, making it an [automorphism](@entry_id:143521). To see the connection, suppose the Frobenius map is surjective. This means every element in $K$ is a $p$-th power. Now, if we have an [irreducible polynomial](@entry_id:156607) $f(x)$ that is also inseparable, it must be of the form $f(x) = g(x^p) = \sum b_i (x^p)^i$. Since every $b_i \in K$ is a $p$-th power, we can write $b_i = c_i^p$ for some $c_i \in K$. Then:
$$f(x) = \sum c_i^p (x^p)^i = \sum (c_i x^i)^p = (\sum c_i x^i)^p$$
But this means $f(x)$ is the $p$-th power of another polynomial, which contradicts its irreducibility. Therefore, if the Frobenius map is surjective, no [irreducible polynomial](@entry_id:156607) can be inseparable, and the field must be perfect.

This criterion provides a straightforward way to classify fields.
- **Finite fields:** Any [finite field](@entry_id:150913) $\mathbb{F}_{p^n}$ is perfect. The Frobenius map $\phi: \mathbb{F}_{p^n} \to \mathbb{F}_{p^n}$ is an [injective function](@entry_id:141653) from a [finite set](@entry_id:152247) to itself. Such a map is necessarily surjective. Therefore, every element in a finite field has a unique $p$-th root within the field [@problem_id:1820620]. For example, in $\mathbb{F}_{27}$, the map $x \mapsto x^3$ is an automorphism. For any $\beta \in \mathbb{F}_{27}$, the polynomial $x^3 - \beta$ has a root $a \in \mathbb{F}_{27}$ and factors as $(x-a)^3$. It is inseparable but, crucially, reducible [@problem_id:1820613].
- **Imperfect fields:** The field of [rational functions](@entry_id:154279) $\mathbb{F}_p(t)$ is not perfect. The element $t$ cannot be the $p$-th power of any element in $\mathbb{F}_p(t)$, because if $t = (f(t)/g(t))^p = f(t^p)/g(t^p)$, a comparison of polynomial degrees leads to a contradiction. Thus the Frobenius map is not surjective [@problem_id:1820620] [@problem_id:1820631]. The same reasoning applies to the field of formal Laurent series $\mathbb{F}_p((t))$ [@problem_id:1820620].

### Separable and Inseparable Extensions

The concept of separability extends from polynomials to elements and [field extensions](@entry_id:153187).

- An [algebraic element](@entry_id:149440) $\alpha$ over a field $F$ is **separable** over $F$ if its [minimal polynomial](@entry_id:153598), $m_{\alpha,F}(x)$, is a [separable polynomial](@entry_id:149432).
- An algebraic field extension $K/F$ is a **separable extension** if every element $\alpha \in K$ is separable over $F$. For a finite extension, this is equivalent to the existence of a single separable element $\alpha$ such that $K=F(\alpha)$ (the Primitive Element Theorem).

In characteristic $p$, we also define the opposite notion.
- An element $\alpha$ algebraic over $F$ is **purely inseparable** over $F$ if its minimal polynomial over $F$ has only one distinct root. For such an element, there exists an integer $k \ge 0$ such that $\alpha^{p^k} \in F$.
- An extension $K/F$ is **purely inseparable** if every element of $K$ is purely inseparable over $F$.

### The Structure of Finite Extensions: Separable and Inseparable Degrees

Remarkably, any finite [field extension](@entry_id:150367) can be decomposed into a separable part and a purely inseparable part. This structure provides a deep insight into the nature of fields.

For any finite extension $K/F$, the set of all elements in $K$ that are separable over $F$ forms an intermediate field, denoted $K_s$. This field is called the **maximal separable subextension** of $K/F$. The structure theorem states:
1. The extension $K_s/F$ is separable.
2. The extension $K/K_s$ is purely inseparable.
3. The degree of the extension is multiplicative: $[K:F] = [K_s:F] \cdot [K:K_s]$.

This decomposition gives rise to two important quantities:
- The **separable degree** of the extension, $[K:F]_s$, is defined as the degree of the maximal separable subextension: $[K:F]_s = [K_s:F]$.
- The **inseparable degree**, $[K:F]_i$, is defined as the degree of the remaining purely inseparable part: $[K:F]_i = [K:K_s]$.

The separable degree has an alternative, powerful characterization: it is the number of distinct field homomorphisms $\sigma: K \to \bar{F}$ that fix the base field $F$ (i.e., $\sigma(a)=a$ for all $a \in F$), where $\bar{F}$ is a fixed [algebraic closure](@entry_id:151964) of $F$.

Let's illustrate this with a sophisticated example. Consider the polynomial $f(x) = x^4 + t x^2 + t$ over the imperfect field $F = \mathbb{F}_2(t)$ [@problem_id:1820578]. Let $K$ be the [splitting field](@entry_id:156669) of $f(x)$ over $F$.
We can view $f(x)$ as a quadratic in $x^2$. Let $y=x^2$, giving the polynomial $g(y) = y^2 + ty + t$. The derivative is $g'(y) = t \neq 0$, so $g(y)$ is a [separable polynomial](@entry_id:149432). It is also irreducible over $F$. Let $\beta$ be a root of $g(y)$.
The field $E = F(\beta)$ is the maximal separable subextension of $K/F$, so $K_s=E$. The degree $[E:F] = \deg(g) = 2$. Thus, the separable degree is $[K:F]_s = 2$.
The original polynomial $f(x)$ factors over $E$ as $(x^2 - \beta_1)(x^2 - \beta_2)$, where $\beta_1, \beta_2$ are the roots of $g(y)$. In characteristic 2, this becomes $(x-\sqrt{\beta_1})^2 (x-\sqrt{\beta_2})^2$. The [splitting field](@entry_id:156669) $K$ is obtained by adjoining the roots of these two purely inseparable polynomials to $E$. The extension $K/E$ is purely inseparable.
The total number of distinct roots of $f(x)$ is 2, which matches the separable degree $[K:F]_s=2$. This is also the number of distinct embeddings of $K$ into an [algebraic closure](@entry_id:151964) of $F$ [@problem_id:1820568].

We can see the same structure in another example. Let $F=\mathbb{F}_p(u)$ and let $\alpha$ be a root of $P(y) = y^{2p} - u^p y^p - u$. The extension is $K=F(\alpha)$ [@problem_id:1820625]. Let $z = \alpha^p$. Then $z$ is a root of the [separable polynomial](@entry_id:149432) $R(T) = T^2 - u^p T - u$. The maximal separable subextension is $K_s = F(z)$, and $[K_s:F]=2$. The element $\alpha$ is a root of $x^p - z$ over $K_s$. This is a purely [inseparable polynomial](@entry_id:150131) of degree $p$. Thus, the inseparable degree is $[K:K_s]=p$. The total degree of the extension is $[K:F] = [K_s:F][K:K_s] = 2p$.

In summary, the concept of separability, which begins with the simple algebraic tool of the [formal derivative](@entry_id:150637), blossoms into a structural theory that neatly partitions every finite field extension into a separable component and a purely inseparable component. This decomposition is essential for understanding the symmetries of fields and is a prerequisite for the deeper results of Galois theory.