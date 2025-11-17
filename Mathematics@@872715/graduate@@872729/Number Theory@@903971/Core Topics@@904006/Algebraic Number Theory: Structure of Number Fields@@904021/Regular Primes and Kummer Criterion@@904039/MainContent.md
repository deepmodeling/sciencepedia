## Introduction
The theory of [regular primes](@entry_id:196257), pioneered by Ernst Kummer, stands as a landmark achievement in number theory, forging a surprising and profound link between the worlds of analysis and algebra. At its heart lies a criterion that connects the divisibility properties of a sequence of rational numbers—the Bernoulli numbers—to the intricate structure of ideal [class groups](@entry_id:182524) in [cyclotomic fields](@entry_id:153828). This connection was instrumental in making the first substantial progress on Fermat's Last Theorem, but its significance extends far beyond this classical problem, forming a cornerstone of modern [algebraic number](@entry_id:156710) theory. This article aims to bridge the gap between the computational simplicity of Kummer's criterion and the deep algebraic truths it encodes.

We will embark on a journey to unravel this elegant theory. The first chapter, "Principles and Mechanisms," lays the groundwork by introducing Bernoulli numbers and demonstrating how the Herbrand-Ribet theorem connects them to the Galois module structure of the class group. Following this, the "Applications and Interdisciplinary Connections" chapter explores the historical impact on Fermat's Last Theorem and traces the evolution of these ideas into the powerful frameworks of *p*-adic L-functions and Iwasawa theory. Finally, the "Hands-On Practices" section provides an opportunity to solidify your understanding by applying these concepts to concrete computational and theoretical problems, translating abstract principles into practical skills.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms that underpin the theory of [regular primes](@entry_id:196257). Having established the historical context in the introduction, we now build the formal framework, starting with the analytical objects—Bernoulli numbers—and constructing a bridge to the [algebraic structures](@entry_id:139459) they so surprisingly govern—the [class groups](@entry_id:182524) of [cyclotomic fields](@entry_id:153828). Our goal is to dissect Kummer's criterion, revealing the deep connections between analysis, algebra, and geometry that it represents.

### The Bridge from Analysis to Algebra: Bernoulli Numbers

The theory of [regular primes](@entry_id:196257) is inextricably linked to a sequence of rational numbers known as the **Bernoulli numbers**. These numbers, denoted $B_n$, appear in various contexts in mathematics, from the [series expansion](@entry_id:142878) of [trigonometric functions](@entry_id:178918) to the Euler-Maclaurin formula. For our purposes, we define them by their [exponential generating function](@entry_id:270200).

**Definition.** The Bernoulli numbers $B_n$ are defined by the formal [power series expansion](@entry_id:273325):
$$ \frac{t}{\exp(t)-1} = \sum_{n=0}^{\infty} B_n \frac{t^n}{n!} $$

This definition, with $B_1 = -\frac{1}{2}$, is one of two common conventions. The other choice arises from the [generating function](@entry_id:152704) $\frac{t e^t}{e^t-1}$, which differs only in the sign of the $t^1$ term, yielding $B_1 = +\frac{1}{2}$. Since we are primarily concerned with Bernoulli numbers of even index, this distinction is of minor importance, but we will adhere to the former convention.

To work with these numbers, a recurrence relation is more practical than direct [series expansion](@entry_id:142878). By multiplying the defining equation by $\exp(t)-1$, we obtain $t = (\sum_{j=1}^{\infty} \frac{t^j}{j!}) (\sum_{k=0}^{\infty} B_k \frac{t^k}{k!})$. Comparing the coefficients of $t^n$ on both sides yields $B_0=1$ for $n=1$, and for $n>1$, a powerful recurrence emerges [@problem_id:3022705]:
$$ \sum_{k=0}^{n-1} \binom{n}{k} B_k = 0 $$

Using this formula, we can compute the initial Bernoulli numbers. For $n=2$, we have $\binom{2}{0}B_0 + \binom{2}{1}B_1 = 0$, which gives $1(1) + 2B_1 = 0$, so $B_1 = -\frac{1}{2}$. The subsequent values are:
- $B_0 = 1$
- $B_2 = \frac{1}{6}$
- $B_4 = -\frac{1}{30}$
- $B_6 = \frac{1}{42}$
- $B_8 = -\frac{1}{30}$
- $B_{10} = \frac{5}{66}$
- $B_{12} = -\frac{691}{2730}$

A key property, readily seen by analyzing the [generating function](@entry_id:152704), is that $B_k=0$ for all odd integers $k > 1$. Therefore, our attention will be exclusively on the even-indexed Bernoulli numbers.

The denominators of these numbers are described by the celebrated **Clausen-von Staudt theorem**. It states that for an even index $k \ge 2$, the denominator of $B_k$ (in lowest terms) is the product of all prime numbers $q$ such that $(q-1)$ divides $k$. A direct consequence is that for a prime $p$, $p$ appears in the denominator of $B_k$ if and only if $p-1$ divides $k$. This means for any even index $k$ in the range $2 \le k \le p-3$, the condition $p-1 \nmid k$ holds, and thus $B_k$ is a **$p$-integral** rational number. This observation is fundamental, as it legitimizes considering the value of $B_k$ modulo $p$ by simply reducing its numerator modulo $p$ [@problem_id:3022736].

Bernoulli numbers also appear as special values of the **Riemann zeta function** at negative integers. For any integer $k \ge 2$, we have the identity:
$$ \zeta(1-k) = -\frac{B_k}{k} $$
This formula provides the first hint of a deep connection between Bernoulli numbers and arithmetic, linking them to a central object in [analytic number theory](@entry_id:158402) [@problem_id:3022736].

### Kummer's Criterion and the Notion of Regularity

With the Bernoulli numbers defined, we can state the criterion that lies at the heart of this chapter. It provides a purely computational test for a property that, as we will see, has profound algebraic significance.

**Definition (Kummer's Criterion).** An odd prime $p$ is said to be **regular** if it does not divide the numerator of any of the Bernoulli numbers $B_2, B_4, \ldots, B_{p-3}$. If $p$ divides the numerator of at least one of these numbers, it is called **irregular**. The number of even indices $k \in [2, p-3]$ for which $p$ divides the numerator of $B_k$ is called the **index of irregularity** of $p$, denoted $i(p)$ or $r(p)$. Thus, a prime $p$ is regular if and only if its index of irregularity is zero [@problem_id:3022688] [@problem_id:3022736].

For example, to determine if the prime $p=13$ is regular, we examine the numerators of $B_2, B_4, B_6, B_8, B_{10}$. As computed previously, these numerators are $1, -1, 1, -1, 5$, respectively. Since none of these is divisible by $13$, the prime $13$ is regular, and its index of irregularity is $i(13)=0$ [@problem_id:3022705]. The first few [irregular primes](@entry_id:189527) are $37, 59, 67, 101, 103, 131, 149,$ and $157$. The smallest, $p=37$, is irregular because $37$ divides the numerator of $B_{32}$.

The historical significance of this concept stems from Kummer's work on Fermat's Last Theorem. In the mid-19th century, Kummer proved that Fermat's Last Theorem is true for any exponent $p$ that is a [regular prime](@entry_id:202179) [@problem_id:3022736]. This was a monumental step, but it immediately raised a fundamental question: Why should the [divisibility](@entry_id:190902) of these seemingly arbitrary rational numbers determine the solvability of a Diophantine equation? The answer lies in the algebraic structure of [cyclotomic fields](@entry_id:153828).

### The Algebraic Heart of the Matter: Cyclotomic Fields and Class Groups

The true meaning of regularity is revealed not through analysis, but through algebra. The proper context for understanding Kummer's criterion is the arithmetic of **[cyclotomic fields](@entry_id:153828)**.

Let $p$ be an odd prime and $\zeta_p = \exp(2\pi i / p)$ be a primitive $p$-th root of unity. The $p$-th cyclotomic field is $K = \mathbb{Q}(\zeta_p)$. This is a Galois extension of $\mathbb{Q}$ of degree $p-1$, with Galois group $\mathrm{Gal}(K/\mathbb{Q})$ canonically isomorphic to $(\mathbb{Z}/p\mathbb{Z})^\times$. The [algebraic integers](@entry_id:151672) in $K$ do not necessarily form a [unique factorization domain](@entry_id:155710). The obstruction to [unique factorization](@entry_id:152313) is measured by the **ideal class group**, $\mathrm{Cl}(K)$, a finite abelian group whose order is the **class number**, $h_p = |\mathrm{Cl}(K)|$.

The algebraic definition of regularity is as follows:

**Definition (Algebraic Regularity).** An odd prime $p$ is **regular** if and only if $p$ does not divide the [class number](@entry_id:156164) $h_p$ of the cyclotomic field $\mathbb{Q}(\zeta_p)$ [@problem_id:3022729] [@problem_id:3022736].

Kummer's great discovery was that these two definitions—one via Bernoulli numbers, one via the class number—are equivalent. To understand this equivalence, we must dissect the structure of the class group.

The Galois group $\mathrm{Gal}(K/\mathbb{Q})$ contains a special element of order two: [complex conjugation](@entry_id:174690), denoted by $c$. Under the isomorphism $\mathrm{Gal}(K/\mathbb{Q}) \cong (\mathbb{Z}/p\mathbb{Z})^\times$, where an [automorphism](@entry_id:143521) $\sigma_a$ is defined by $\sigma_a(\zeta_p) = \zeta_p^a$, [complex conjugation](@entry_id:174690) corresponds to the element $a=-1$ [@problem_id:3022701]. The [fixed field](@entry_id:155430) of this automorphism is the **maximal real subfield** of $K$, denoted $K^+ = \mathbb{Q}(\zeta_p + \zeta_p^{-1})$. This is a field of degree $(p-1)/2$ over $\mathbb{Q}$ [@problem_id:3022701].

Let $A$ be the **$p$-primary part** of the [class group](@entry_id:204725) $\mathrm{Cl}(K)$, i.e., its Sylow $p$-subgroup. The action of [complex conjugation](@entry_id:174690) $c$ on $A$ allows for a [canonical decomposition](@entry_id:634116). Since $c^2=1$ and $p$ is odd, the integer $2$ is invertible on the abelian $p$-group $A$. This allows us to decompose $A$ into [eigenspaces](@entry_id:147356) for the action of $c$ [@problem_id:3022727]:
$$ A = A^+ \oplus A^- $$
Here, $A^+ = \{a \in A \mid c(a) = a\}$ is the `+1`-eigenspace, and $A^- = \{a \in A \mid c(a) = a^{-1}\}$ is the `-1`-[eigenspace](@entry_id:150590) (using multiplicative notation for the [class group](@entry_id:204725)). These are often called the **plus** and **minus parts** of the $p$-class group. This decomposition of the $p$-class group corresponds to a factorization of the $p$-part of the class number. We write $h_p = h_p^+ h_p^-$, where $h_p^+$ is the [class number](@entry_id:156164) of the real subfield $K^+$, and $h_p^-$ is the **relative class number**. It can be shown that $|A^+|$ is the order of the $p$-Sylow subgroup of $\mathrm{Cl}(K^+)$, while $|A^-|$ is the $p$-part of $h_p^-$.

A deep theorem, due in one direction to Herbrand, states that if $p \mid h_p$, then necessarily $p \mid h_p^-$. This means that the property of being irregular ($p \mid h_p$) is entirely a phenomenon of the minus part of the class group ($p \mid h_p^-$ or equivalently, $A^- \neq \{0\}$). The plus part, $A^+$, is governed by a famous open problem, **Vandiver's Conjecture**, which asserts that $A^+$ is always trivial (i.e., $p \nmid h_p^+$). This conjecture has been verified for all primes up to very large bounds but remains unproven. It is connected to the structure of the **[cyclotomic units](@entry_id:184331)** of $K^+$ [@problem_id:3022722]. However, the equivalence of Kummer's criteria does not depend on Vandiver's Conjecture [@problem_id:3022688]. The link between Bernoulli numbers and irregularity is forged entirely within the minus part, $A^-$.

### The Herbrand-Ribet Theorem: The Unifying Principle

The final piece of the puzzle connecting Bernoulli numbers to the [class group](@entry_id:204725) is the remarkable **Herbrand-Ribet Theorem**. This theorem provides a precise, character-by-character correspondence between the divisibility of Bernoulli numbers and the structure of the minus part of the [class group](@entry_id:204725), $A^-$.

The Galois group $\Delta = \mathrm{Gal}(K/\mathbb{Q})$ acts on the $p$-[class group](@entry_id:204725) $A$. This makes $A$ a module over the [group ring](@entry_id:146647) $\mathbb{Z}_p[\Delta]$. The group $A$ can be decomposed into a direct sum of eigenspaces (isotypical components) corresponding to the characters of $\Delta$. Let $\omega: \Delta \to \mathbb{Z}_p^\times$ be the **Teichmüller character**, which gives the "identity" map $\sigma_a \mapsto a \pmod p$. Any character of $\Delta$ is a power of $\omega$. The decomposition is:
$$ A = \bigoplus_{i=0}^{p-2} A_i \quad \text{where } A_i = \{ a \in A \mid \sigma(a) = \omega^i(\sigma)a \text{ for all } \sigma \in \Delta \} $$
The minus part $A^-$ corresponds to the sum over odd indices $i$, and the plus part $A^+$ corresponds to the sum over even indices $i$.

The Herbrand-Ribet Theorem states:

**Theorem (Herbrand-Ribet).** Let $p$ be an odd prime and let $k$ be an even integer such that $2 \le k \le p-3$. Then $p$ divides the numerator of the Bernoulli number $B_k$ if and only if the $\omega^{1-k}$-[eigenspace](@entry_id:150590) of the $p$-class group $A$ is non-trivial.
$$ p \mid \mathrm{num}(B_k) \iff A_{1-k} \neq \{0\} $$

This theorem is the fundamental mechanism behind Kummer's criterion [@problem_id:3022688] [@problem_id:3022732]. Since $k$ is even, the index $1-k$ is odd, so the character $\omega^{1-k}$ is an odd character. This confirms that the divisibility of $B_k$ is detecting non-triviality in a component of the minus part, $A^-$. The full equivalence now becomes clear:

$p$ is irregular $\iff p \mid h_p \iff A \neq \{0\} \iff A^- \neq \{0\}$
$\iff$ at least one odd-indexed [eigenspace](@entry_id:150590) $A_j$ is non-trivial
$\iff$ at least one $A_{1-k}$ is non-trivial for some even $k \in [2, p-3]$
$\iff p \mid \mathrm{num}(B_k)$ for some even $k \in [2, p-3]$.

This elegant chain of equivalences fully explains why a computational check on Bernoulli numbers reveals deep arithmetic information about the class group of a cyclotomic field. The irregular index $i(p)$ is not merely a count; it is precisely the number of non-trivial odd eigenspaces (for indices other than 1) in the $p$-class group [@problem_id:3022729].

### Modern Perspectives: L-functions and Iwasawa Theory

The connection between Bernoulli numbers and [class groups](@entry_id:182524) can be viewed from an even more powerful, modern perspective using $p$-adic analysis and L-functions. This approach shows that the collection of Bernoulli numbers in Kummer's criterion are not just a disparate list of values, but are intrinsically linked as special values of a single analytic function.

First, one can define **generalized Bernoulli numbers** $B_{n,\chi}$ for any Dirichlet character $\chi$. These are related to the values of Dirichlet L-functions at non-positive integers by $L(1-n, \chi) = -B_{n,\chi}/n$. For an odd character $\chi = \omega^{1-k}$ (with $k$ even, $2 \le k \le p-3$), the generalized Bernoulli number $B_{1,\chi}$ is related to the classical Bernoulli number $B_k$ via the **Kummer congruence**:
$$ B_{1,\omega^{1-k}} \equiv \frac{B_k}{k} \pmod p $$
Since $k$ is not divisible by $p$ in this range, the condition $p \mid \mathrm{num}(B_k)$ is equivalent to $B_{1,\omega^{1-k}} \equiv 0 \pmod p$. Thus, Kummer's criterion can be restated: $p$ is irregular if and only if $B_{1,\chi} \equiv 0 \pmod p$ for some odd character $\chi$ corresponding to an even $k \in [2, p-3]$ [@problem_id:3022730].

The ultimate unification comes from the **Kubota-Leopoldt $p$-adic L-function**, denoted $L_p(s, \chi)$. For a fixed prime $p$ and character $\chi$, this is a continuous function from the $p$-adic integers $\mathbb{Z}_p$ to $\mathbb{Q}_p$ that "interpolates" the special values of the classical Dirichlet L-function. The key interpolation formula connecting to the classical Bernoulli numbers is [@problem_id:3022696]:
$$ L_p(1-k, \omega^k) = -(1-p^{k-1})\frac{B_k}{k} $$
For the range $2 \le k \le p-3$, the term $-(1-p^{k-1})$ is a $p$-adic unit and $k$ is not divisible by $p$. Thus, the $p$-adic valuation of $B_k$ is the same as that of $L_p(1-k, \omega^k)$. Therefore, the condition $p \mid \mathrm{num}(B_k)$ is precisely equivalent to the condition that this special value of the $p$-adic L-function is divisible by $p$:
$$ p \mid \mathrm{num}(B_k) \iff L_p(1-k, \omega^k) \equiv 0 \pmod p $$
A prime $p$ is irregular if and only if one of these special values of a $p$-adic L-function is divisible by $p$ [@problem_id:3022696]. This reframing of irregularity as the existence of "exceptional zeros" modulo $p$ of $p$-adic L-functions is the starting point for **Iwasawa theory**, a vast and powerful theory that studies the growth of [class groups](@entry_id:182524) in towers of [number fields](@entry_id:155558).