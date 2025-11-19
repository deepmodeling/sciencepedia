## Introduction
Public-key [cryptography](@entry_id:139166) represents a monumental leap forward in the field of secure communications, fundamentally changing how we protect information in a digital world. Unlike traditional symmetric systems that rely on a pre-[shared secret key](@entry_id:261464), public-key methods solve the critical problem of key distribution, allowing [secure communication](@entry_id:275761) between parties with no prior contact. This article demystifies the number-theoretic magic behind this paradigm. In the upcoming chapters, you will explore the core principles that make public-key systems possible. The journey begins with **Principles and Mechanisms**, where we will delve into the mathematical concepts of one-way functions, [modular arithmetic](@entry_id:143700), and Euler's theorem, and see how they are used to construct the foundational RSA and Diffie-Hellman protocols. Next, **Applications and Interdisciplinary Connections** will bridge theory and practice, examining how these protocols are used for encryption and [digital signatures](@entry_id:269311), optimized for performance, and hardened against real-world attacks. Finally, **Hands-On Practices** will offer a chance to apply these concepts, guiding you through the essential calculations that bring these powerful cryptographic tools to life.

## Principles and Mechanisms

The cryptographic systems discussed in the previous chapter operate under a symmetric paradigm, where the same key is used for both [encryption and decryption](@entry_id:637674) (or for message authentication [code generation](@entry_id:747434) and verification). The security of such systems relies entirely on the secrecy of this shared key. Public-key [cryptography](@entry_id:139166) introduces a revolutionary paradigm shift: the use of an asymmetric key pair, consisting of a public key, which can be distributed widely, and a private key, which must be kept secret by its owner. This asymmetry allows for secure communication and the creation of [digital signatures](@entry_id:269311) without the prerequisite of a pre-[shared secret key](@entry_id:261464). The functionality of these systems hinges on the existence of special mathematical functions, whose principles and mechanisms are the focus of this chapter.

### The Computational Foundation: One-Way and Trapdoor Functions

At the heart of [public-key cryptography](@entry_id:150737) lies the concept of a **[one-way function](@entry_id:267542)**. Informally, this is a function $f$ that is easy to compute for any given input, but computationally infeasible to invert on average. That is, given an output $y = f(x)$, it is extremely difficult to find any input $x'$ such that $f(x') = y$. More formally, we say a function is one-way if it can be computed by a deterministic polynomial-time algorithm, but any [probabilistic polynomial-time](@entry_id:271220) (PPT) adversary has only a negligible probability of finding a pre-image for a randomly chosen output [@problem_id:3086476].

A prime candidate for a [one-way function](@entry_id:267542) comes from number theory. Consider a large prime number $p$ and a generator $g$ of the multiplicative group of non-zero elements modulo $p$. The discrete exponentiation function, $f(x) = g^x \pmod{p}$, is easy to compute using algorithms like [binary exponentiation](@entry_id:276203). However, the inverse problem—given $y$, finding an $x$ such that $g^x \equiv y \pmod{p}$—is the **Discrete Logarithm Problem (DLP)**. For well-chosen groups, the DLP is believed to be computationally intractable, making discrete exponentiation a candidate [one-way function](@entry_id:267542) [@problem_id:3086452] [@problem_id:3086476].

While one-way functions are interesting, they are not sufficient for public-key encryption on their own. If a function is hard for everyone to invert, the intended recipient of an encrypted message would be just as unable to decrypt it as an adversary. This necessitates a more specialized tool: a **trapdoor permutation**. This is a special kind of [one-way function](@entry_id:267542) that possesses a secret piece of information, the "trapdoor." Without the trapdoor, the function is hard to invert. With the trapdoor, inversion becomes easy. Formally, a trapdoor permutation is a bijection $f$ on a domain $D$, where $f$ is easy to compute, hard to invert for a PPT adversary, but easy to invert given the trapdoor information [@problem_id:3086476]. The canonical example of a trapdoor permutation is the RSA function, which we will construct in detail.

### Modular Arithmetic: The Mathematical Setting

To understand the construction of systems like RSA and Diffie-Hellman, we must first establish their mathematical environment: the world of [modular arithmetic](@entry_id:143700).

#### The Ring of Integers Modulo n and the Group of Units

For any integer $n \ge 2$, we can partition the integers $\mathbb{Z}$ into equivalence classes based on their remainder when divided by $n$. We say $a \equiv b \pmod{n}$ if $n$ divides $a-b$. The set of these [equivalence classes](@entry_id:156032) is denoted $\mathbb{Z}/n\mathbb{Z}$, which forms a **[commutative ring](@entry_id:148075)** with addition and multiplication defined as $[a] + [b] = [a+b]$ and $[a] \cdot [b] = [ab]$.

Within this ring, some elements are special. An element $[a] \in \mathbb{Z}/n\mathbb{Z}$ is called a **unit** or is said to be **invertible** if there exists an element $[b]$ such that $[a] \cdot [b] = [1]$. The element $[b]$ is the [multiplicative inverse](@entry_id:137949) of $[a]$. A fundamental result states that an element $[a]$ is invertible if and only if the greatest common divisor of $a$ and $n$ is 1, i.e., $\gcd(a,n)=1$ [@problem_id:3086453].

This equivalence can be understood through Bézout's identity. If $\gcd(a,n)=1$, then there exist integers $x$ and $y$ such that $ax+ny=1$. Taking this equation modulo $n$, the term $ny$ becomes 0, leaving us with $ax \equiv 1 \pmod{n}$. This means $[x]$ is the [multiplicative inverse](@entry_id:137949) of $[a]$. Conversely, if $[a]$ is invertible with inverse $[b]$, then $ab \equiv 1 \pmod{n}$, which implies $ab - 1 = nk$ for some integer $k$. Rearranging gives $ab - nk = 1$, a [linear combination](@entry_id:155091) of $a$ and $n$ that equals 1, which by the properties of the GCD, forces $\gcd(a,n)=1$ [@problem_id:3086453].

The set of all invertible elements in $\mathbb{Z}/n\mathbb{Z}$ is denoted $(\mathbb{Z}/n\mathbb{Z})^\times$. This set forms a group under multiplication, known as the **[group of units modulo n](@entry_id:155600)**. For example, for $n=12$, the integers $a$ between 1 and 11 that are coprime to 12 (i.e., not divisible by 2 or 3) are 1, 5, 7, and 11. Thus, the group of units is $(\mathbb{Z}/12\mathbb{Z})^\times = \{[1], [5], [7], [11]\}$ [@problem_id:3086453]. Elements that are not units and are not zero, such as $[2], [3], [4]$ in $\mathbb{Z}/12\mathbb{Z}$, are **zero divisors**, because they can be multiplied by another non-zero element to yield zero (e.g., $[3] \cdot [4] = [12] = [0]$). A ring $\mathbb{Z}/n\mathbb{Z}$ has no non-zero zero divisors if and only if $n$ is a prime number.

#### Euler's Totient Function and Theorem

The order (or size) of the [group of units](@entry_id:140130) $(\mathbb{Z}/n\mathbb{Z})^\times$ is of paramount importance in [public-key cryptography](@entry_id:150737). This quantity is given by **Euler's totient function**, $\varphi(n)$, which counts the number of positive integers less than or equal to $n$ that are [relatively prime](@entry_id:143119) to $n$.

The computation of $\varphi(n)$ relies on two key properties.
1.  For a prime power $p^k$, $\varphi(p^k) = p^k - p^{k-1}$. This can be derived by counting: there are $p^k$ integers from 1 to $p^k$. The integers not coprime to $p^k$ are precisely the multiples of $p$, which are $p, 2p, \dots, (p^{k-1})p$. There are $p^{k-1}$ such multiples. Subtracting these from the total gives the result [@problem_id:3086494].
2.  If $\gcd(a,b)=1$, then $\varphi(ab) = \varphi(a)\varphi(b)$. This multiplicative property is a consequence of the Chinese Remainder Theorem, which establishes a [ring isomorphism](@entry_id:147982) $\mathbb{Z}/(ab)\mathbb{Z} \cong \mathbb{Z}/a\mathbb{Z} \times \mathbb{Z}/b\mathbb{Z}$, that in turn induces a [group isomorphism](@entry_id:147371) on their groups of units: $(\mathbb{Z}/(ab)\mathbb{Z})^\times \cong (\mathbb{Z}/a\mathbb{Z})^\times \times (\mathbb{Z}/b\mathbb{Z})^\times$. The order of the group on the left must equal the product of the orders of the groups on the right, giving the multiplicative property [@problem_id:3086494].

Combining these, if the [prime factorization](@entry_id:152058) of $n$ is $n = p_1^{k_1} p_2^{k_2} \cdots p_r^{k_r}$, then $\varphi(n) = n \prod_{i=1}^r (1 - \frac{1}{p_i})$. For instance, to compute $\varphi(360)$, we factor $360 = 2^3 \cdot 3^2 \cdot 5^1$. Using the properties, $\varphi(360) = \varphi(2^3)\varphi(3^2)\varphi(5^1) = (2^3-2^2)(3^2-3^1)(5^1-5^0) = (4)(6)(4) = 96$ [@problem_id:3086494].

A cornerstone result from group theory (Lagrange's Theorem) applied to $(\mathbb{Z}/n\mathbb{Z})^\times$ yields **Euler's totient theorem**: for any integer $a$ such that $\gcd(a,n)=1$, we have $a^{\varphi(n)} \equiv 1 \pmod{n}$. This theorem is the engine that drives RSA.

#### A Refinement: The Carmichael Function

Euler's theorem guarantees that $\varphi(n)$ is an exponent that "annihilates" every element of the group of units. However, it may not be the *smallest* such exponent. The **Carmichael function**, $\lambda(n)$, is defined as the smallest positive integer $m$ such that $a^m \equiv 1 \pmod n$ for all $a$ coprime to $n$. This value, $\lambda(n)$, is the **exponent** of the group $(\mathbb{Z}/n\mathbb{Z})^\times$.

The values of $\varphi(n)$ and $\lambda(n)$ are equal if and only if the group $(\mathbb{Z}/n\mathbb{Z})^\times$ is cyclic. When the group is not cyclic, $\lambda(n)$ is a proper divisor of $\varphi(n)$. A key example occurs for powers of 2. Consider $n=1024=2^{10}$. The [group of units](@entry_id:140130) $(\mathbb{Z}/1024\mathbb{Z})^\times$ consists of the 512 odd integers less than 1024, so $\varphi(1024) = 512$. However, this group is not cyclic; it is isomorphic to $C_2 \times C_{256}$. The exponent is the [least common multiple](@entry_id:140942) of the orders of the elements in this [direct product](@entry_id:143046), so $\lambda(1024) = \text{lcm}(2, 256) = 256$ [@problem_id:3086477]. This means that for any odd integer $a$, it is true that $a^{256} \equiv 1 \pmod{1024}$, a much stronger statement than that guaranteed by Euler's theorem. This distinction is relevant for optimizing RSA implementations.

### Mechanism 1: The RSA Cryptosystem

Armed with these number-theoretic tools, we can now construct the Rivest-Shamir-Adleman (RSA) cryptosystem, the first and most famous public-key algorithm.

#### Key Generation, Encryption, and Decryption

The RSA algorithm works as follows:

1.  **Key Generation**:
    *   Choose two distinct large prime numbers, $p$ and $q$.
    *   Compute the public modulus $n = pq$.
    *   Compute the order of the group of units, $\varphi(n) = (p-1)(q-1)$.
    *   Choose a public exponent $e$ such that $1  e  \varphi(n)$ and $\gcd(e, \varphi(n)) = 1$. A common choice is $e = 65537$, which is prime and has a binary representation with only two 1s, making exponentiation efficient.
    *   Compute the private exponent $d$, which is the unique multiplicative inverse of $e$ modulo $\varphi(n)$. That is, find $d$ such that $ed \equiv 1 \pmod{\varphi(n)}$. This is done efficiently using the Extended Euclidean Algorithm [@problem_id:3086456].

2.  **Key Distribution**: The public key is the pair $(n, e)$. The private key is the exponent $d$. The primes $p$ and $q$ must be kept secret and can be discarded after $d$ is computed.

3.  **Encryption**: To encrypt a message $m$ (represented as an integer where $0 \le m  n$), the sender computes the ciphertext $c$ as:
    $c \equiv m^e \pmod{n}$.

4.  **Decryption**: To decrypt the ciphertext $c$, the recipient uses their private key $d$ to compute:
    $m \equiv c^d \pmod{n}$.

The decryption process works because of Euler's theorem. We have $c^d \equiv (m^e)^d = m^{ed} \pmod{n}$. Since $ed \equiv 1 \pmod{\varphi(n)}$, we can write $ed = 1 + k\varphi(n)$ for some integer $k$. Therefore, for any message $m$ coprime to $n$:
$m^{ed} = m^{1+k\varphi(n)} = m \cdot (m^{\varphi(n)})^k \equiv m \cdot 1^k \equiv m \pmod{n}$.
(A slightly more involved argument using the Chinese Remainder Theorem shows this also holds for the few messages $m$ where $\gcd(m,n) \ne 1$).

#### The RSA Trapdoor Explained

The security of RSA relies on the difficulty of computing the private exponent $d$ given only the public key $(n, e)$. The process of computing $d$ requires finding the inverse of $e$ modulo $\varphi(n)$. This, in turn, requires knowing the value of $\varphi(n)$. Herein lies the trapdoor [@problem_id:3086460].

For the legitimate owner of the keys, who knows the prime factors $p$ and $q$, computing $\varphi(n)=(p-1)(q-1)$ is trivial. For an adversary, who only knows $n$, computing $\varphi(n)$ is a computationally hard problem. In fact, it is computationally equivalent to factoring $n$. If an adversary could find $\varphi(n)$, they could also find the sum of the prime factors $p+q = n - \varphi(n) + 1$. Knowing the sum $p+q$ and the product $pq=n$, the adversary could easily find $p$ and $q$ by solving the quadratic equation $x^2 - (p+q)x + pq = 0$.

Thus, the factorization of $n$ is the trapdoor. It allows for the efficient computation of $\varphi(n)$ and subsequently the private key $d$, while for anyone without this knowledge, computing $d$ is believed to be as difficult as factoring the large integer $n$ [@problem_id:3086460].

#### Security Considerations for RSA

The security of RSA is thus tied to the difficulty of the **Integer Factorization Problem**. The relationship between breaking RSA and factoring is subtle.
*   **RSA Inversion is reducible to Factoring**: As we have seen, if an adversary can factor $n$, they can easily compute $\varphi(n)$ and $d$, and thus invert the RSA function (decrypt any message). This is a [polynomial-time reduction](@entry_id:275241) [@problem_id:3086466].
*   **Factoring's reducibility to RSA Inversion**: It is a major open question whether the converse is true for any choice of public exponent $e$. That is, given an oracle that can decrypt any ciphertext (solve the RSA Inversion Problem), can we efficiently factor $n$? No general method is known. This means that breaking RSA could potentially be easier than factoring $n$.

However, for certain specific choices of $e$, this equivalence has been proven. The most famous case is the **Rabin Cryptosystem**, which is essentially RSA with $e=2$. For this system, it can be shown that an algorithm capable of finding square roots modulo $n$ can be used to factor $n$ with high probability. This makes the security of the Rabin system provably equivalent to the hardness of factoring [@problem_id:3086466].

A final practical note concerns the generation of the primes $p$ and $q$. To find such large primes, one typically generates a large random number and tests it for primality. A common method is **Fermat's [primality test](@entry_id:266856)**, based on Fermat's Little Theorem ($a^{n-1} \equiv 1 \pmod n$ if $n$ is prime and $a$ is not a multiple of $n$). However, this test is not foolproof. There exist [composite numbers](@entry_id:263553) $n$, known as **Carmichael numbers**, which satisfy $a^{n-1} \equiv 1 \pmod n$ for *every* base $a$ that is coprime to $n$. Such numbers will pass the Fermat test for almost all bases, making them "false primes." The smallest such number is $561 = 3 \cdot 11 \cdot 17$. The existence of Carmichael numbers necessitates the use of more sophisticated primality tests, such as Miller-Rabin, in practice [@problem_id:3086492].

### Mechanism 2: The Diffie-Hellman Key Exchange

The second major family of public-key algorithms is based on the difficulty of the Discrete Logarithm Problem. The pioneering protocol in this family is the Diffie-Hellman key exchange.

#### The Protocol and its Security

The Diffie-Hellman protocol allows two parties, Alice and Bob, to establish a [shared secret key](@entry_id:261464) over an insecure channel, without any prior shared secrets.

1.  **Public Parameters**: Alice and Bob first agree on a public finite cyclic group $G$ of large [prime order](@entry_id:141580) $q$, and a generator $g \in G$. A common choice is the [multiplicative group](@entry_id:155975) of integers modulo a large prime $p$, where $q$ is a large prime factor of $p-1$.

2.  **Key Exchange**:
    *   Alice chooses a secret random integer $a \in \{1, \dots, q-1\}$. She computes her public value $A = g^a$ and sends it to Bob.
    *   Bob chooses a secret random integer $b \in \{1, \dots, q-1\}$. He computes his public value $B = g^b$ and sends it to Alice.
    *   Alice computes the shared secret $K = B^a = (g^b)^a = g^{ab}$.
    *   Bob computes the same shared secret $K = A^b = (g^a)^b = g^{ab}$.

Alice and Bob now share the secret key $K = g^{ab}$, while an eavesdropper, Eve, has only seen the public values $g, A=g^a,$ and $B=g^b$. To derive the key, Eve must compute $g^{ab}$ from these values. This is known as the **Computational Diffie-Hellman (CDH) problem**. The security of the protocol relies on the **CDH assumption**, which posits that this problem is computationally intractable [@problem_id:3086488].

The CDH problem is closely related to the DLP. If Eve could solve the DLP, she could compute Alice's secret $a$ from her public value $A=g^a$, and then compute the key herself as $K = B^a$. Therefore, an efficient algorithm for DLP implies an efficient algorithm for CDH. This establishes a hierarchy of problem difficulty: the DLP is at least as hard as the CDH problem.

For some applications, a stronger security guarantee is needed. The **Decisional Diffie-Hellman (DDH) assumption** asserts that it is computationally infeasible to distinguish a real Diffie-Hellman tuple $(g^a, g^b, g^{ab})$ from a tuple with a random exponent in the third position, $(g^a, g^b, g^c)$, where $c$ is chosen randomly. The DDH problem is considered easier than the CDH problem, because if one can solve CDH, one can simply compute the true $g^{ab}$ and compare it to the third element of the tuple to solve DDH. This leads to the standard hierarchy of hardness assumptions in group-based cryptography [@problem_id:3086488]:
**DDH is no harder than CDH, which is no harder than DLP.**
In many groups used in [cryptography](@entry_id:139166), these relationships are believed to be strict inequalities. The choice of which assumption to rely upon depends on the security goals of the specific cryptographic protocol being designed.