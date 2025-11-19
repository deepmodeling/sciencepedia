## Introduction
The Quantum Fourier Transform (QFT) is one of the most powerful tools in quantum computing, providing a quantum analogue to the classical Fourier transform with an [exponential speedup](@entry_id:142118). Its significance lies in its unparalleled ability to efficiently solve problems that are considered intractable for even the most powerful classical supercomputers. This capability directly addresses a critical challenge in modern information security: the reliance of [public-key cryptography](@entry_id:150737) on the presumed difficulty of problems like [integer factorization](@entry_id:138448) and the [discrete logarithm](@entry_id:266196). By providing a pathway to solve these problems, QFT-based algorithms represent a paradigm shift in computation and a fundamental threat to our current cryptographic infrastructure.

This article provides a comprehensive exploration of the QFT's application to these foundational problems. Over the next three chapters, you will gain a deep understanding of this quantum method. The journey begins in **"Principles and Mechanisms"**, which dissects how the QFT works as a periodicity detector and details its step-by-step application in Shor's algorithm and the [discrete logarithm problem](@entry_id:144538). Next, **"Applications and Interdisciplinary Connections"** broadens the perspective, demonstrating how these core algorithms impact cryptography, extend to other number-theoretic problems, and can be generalized under the powerful algebraic framework of the Hidden Subgroup Problem. Finally, the **"Hands-On Practices"** chapter offers a series of targeted exercises, allowing you to engage directly with the concepts of phase estimation, classical post-processing, and the effects of noise on algorithm performance.

## Principles and Mechanisms

The Quantum Fourier Transform (QFT) stands as a cornerstone of [quantum algorithm](@entry_id:140638) design, serving as the quantum analogue of the classical discrete Fourier transform. Its power lies in its ability to efficiently reveal [periodic structures](@entry_id:753351) within quantum states. This chapter will elucidate the fundamental principles by which the QFT achieves this, and then explore its application in two of the most significant [quantum algorithms](@entry_id:147346): Shor's algorithm for [integer factorization](@entry_id:138448) and algorithms for solving the [discrete logarithm problem](@entry_id:144538). We will see that both problems can be elegantly reformulated as finding a hidden [periodicity](@entry_id:152486), a task for which the QFT is uniquely suited.

### The Quantum Fourier Transform as a Periodicity Detector

The QFT is a unitary transformation on an $n$-qubit register, which operates on a Hilbert space of dimension $N=2^n$. Its action on a computational basis state $|j\rangle$, for $j \in \{0, 1, \dots, N-1\}$, is defined as:

$$
\text{QFT}|j\rangle = \frac{1}{\sqrt{N}} \sum_{k=0}^{N-1} \exp\left(\frac{2\pi i j k}{N}\right) |k\rangle
$$

The true power of the QFT is realized when it is applied not to a single basis state, but to a superposition of states that exhibits some [periodicity](@entry_id:152486). Consider a state $|\psi\rangle$ that is a uniform superposition of basis states whose labels are multiples of some integer $r$, which we call the period. Such a state can be written as:

$$
|\psi\rangle = \frac{1}{\sqrt{M}} \sum_{j=0}^{M-1} |jr\rangle
$$

where $r$ is the period and $M$ is the number of periodic terms in the superposition that fit within the register size $N$. For simplicity, let's first assume $r$ divides $N$, so $M = N/r$. Applying the QFT to this state, by linearity, gives:

$$
\text{QFT}|\psi\rangle = \frac{1}{\sqrt{M}} \sum_{j=0}^{M-1} \text{QFT}|jr\rangle = \frac{1}{\sqrt{MN}} \sum_{j=0}^{M-1} \sum_{k=0}^{N-1} \exp\left(\frac{2\pi i (jr)k}{N}\right) |k\rangle
$$

By swapping the order of summation, we can examine the amplitude of each basis state $|k\rangle$:

$$
\beta_k = \frac{1}{\sqrt{MN}} \sum_{j=0}^{M-1} \exp\left(\frac{2\pi i jrk}{N}\right) = \frac{1}{\sqrt{MN}} \sum_{j=0}^{M-1} \left( \exp\left(\frac{2\pi i rk}{N}\right) \right)^j
$$

This is a geometric series. The sum evaluates to $M$ if the base of the exponentiation, $\exp(2\pi i rk/N)$, is equal to 1. This condition holds if and only if the exponent $rk/N$ is an integer. Let's denote this integer as $c$. Then $k = c \cdot \frac{N}{r}$. If $rk/N$ is not an integer, the phases $\exp(2\pi i jrk/N)$ for different values of $j$ will be distributed around the unit circle, leading to destructive interference. For a periodic state where $r$ divides $N$, the interference is perfectly destructive, and the sum is zero.

Thus, the resulting state after the QFT is:

$$
\text{QFT}|\psi\rangle = \frac{\sqrt{M}}{\sqrt{N}} \sum_{c=0}^{r-1} |c \cdot N/r\rangle
$$

This remarkable result shows that the Fourier transform of a periodic state is a superposition of states whose labels are integer multiples of $N/r$. A measurement of this final state will yield one of these multiples. If we obtain a measurement outcome $k = c \cdot N/r$, we can deduce information about the period $r$.

A concrete example illustrates this interference mechanism perfectly [@problem_id:48295]. Consider a 4-qubit register ($N=16$) and a state with period $r=4$: $|\psi\rangle = \frac{1}{2}(|0\rangle + |4\rangle + |8\rangle + |12\rangle)$. Applying the QFT yields a state $|\phi\rangle = \sum_k \beta_k |k\rangle$. The principle of interference dictates that the only non-zero amplitudes $\beta_k$ will be for $k$ that are multiples of $N/r = 16/4 = 4$. These are $k \in \{0, 4, 8, 12\}$. For any other value of $k$, such as $k=2$, the amplitude $\beta_2$ will be a sum of terms that cancel each other out, resulting in $\beta_2=0$.

In a more realistic scenario, the number of periodic terms $M$ may not be exactly $N/r$, for instance when we only have access to a function for a limited range. The state might be of the form $|\psi\rangle = \frac{1}{\sqrt{M}} \sum_{j=0}^{M-1} |jr\rangle$, where $M = \lfloor (N-1)/r \rfloor + 1$ [@problem_id:48171]. In this case, the destructive interference for $k$ values that are not multiples of $N/r$ is not perfect. However, the probability distribution of measurement outcomes remains sharply peaked around these multiples. The probability of measuring an outcome $y$ can be derived from the geometric sum and is given by:

$$
P(y) = \frac{1}{MN} \frac{\sin^2(\pi Mry/N)}{\sin^2(\pi ry/N)}
$$

This function has large peaks when the denominator approaches zero, which occurs when $ry/N$ is close to an integer, i.e., $y \approx c \cdot N/r$. This confirms that even in this more general case, measuring the output of the QFT provides a strong candidate for a multiple of $N/r$.

### Application I: Shor's Integer Factorization Algorithm

The celebrated algorithm developed by Peter Shor for factoring integers provides the most prominent application of quantum [period-finding](@entry_id:141657). The algorithm ingeniously reduces the problem of factoring an integer $N$ to the problem of finding the period of a modular exponential function.

#### The Order-Finding Problem

The classical part of Shor's algorithm begins by choosing a random integer $a$ such that $1 \lt a \lt N$ and $\text{gcd}(a, N) = 1$. If $\text{gcd}(a, N) \neq 1$, we have found a factor of $N$, and the algorithm terminates. Otherwise, we seek the **order** of $a$ modulo $N$, which is the smallest positive integer $r$ such that $a^r \equiv 1 \pmod{N}$. This order $r$ is precisely the period of the function $f(x) = a^x \pmod{N}$.

The quantum part of the algorithm is a direct implementation of the [period-finding](@entry_id:141657) procedure described above. An $n$-qubit register is prepared (where $2^n$ is typically chosen to be between $N^2$ and $2N^2$) to find the period $r$ of this function $f(x)$. The algorithm yields a measurement outcome $k$ from the final QFT step. With high probability, the ratio $k/2^n$ is a very good approximation of an unknown fraction $j/r$ for some integer $j$.

It is important to note that the group $(\mathbb{Z}/N\mathbb{Z})^\times$ of which we are finding the order is not necessarily cyclic. For example, when factoring $N=35$, the group $(\mathbb{Z}/35\mathbb{Z})^\times$ is not cyclic. Nonetheless, every element has a well-defined order, which the quantum subroutine can find. For instance, the order of the element $g=11$ modulo $35$ is $r=3$, a value that can be found by calculating powers of $11$ or by using the Chinese Remainder Theorem [@problem_id:48173].

#### From Measurement to Period

The core challenge after the quantum measurement is classical: how to recover the period $r$ from the measurement $k$ and the known register size $2^n$? We have the approximation:

$$
\left| \frac{k}{2^n} - \frac{j}{r} \right| \le \frac{1}{2^{n+1}}
$$

This inequality guarantees that $k/2^n$ is a uniquely good [rational approximation](@entry_id:136715) of $j/r$. The **[continued fraction algorithm](@entry_id:635794)** is the classical tool perfectly suited for this task. By computing the [continued fraction expansion](@entry_id:636208) of $k/2^n$, we generate a sequence of rational approximations (convergents) $p_i/q_i$ that are successively better. The denominator $q_i$ of one of these convergents is a strong candidate for the period $r$.

For instance, if an experiment with an $n=10$ qubit register ($2^n=1024$) yields a measurement $k=341$, we would compute the continued fraction of $341/1024$. The convergents are $0/1, 1/3, 341/1024$. The denominator $q_1=3$ is a non-trivial candidate for the period $r$ [@problem_id:48194]. We can then test if $a^3 \equiv 1 \pmod N$.

In practice, multiple runs of the quantum algorithm might be necessary. Suppose two independent runs yield outcomes $k_1$ and $k_2$. Each gives a hypothesis for the period, say $r_1$ and $r_2$, via the continued fraction method. If $r_1 \neq r_2$, we can determine the more likely period by checking which candidate provides a better explanation for *both* measurement outcomes, for example, by minimizing the sum of squared errors between the measured $k_i$ and the predicted values $j_i \cdot 2^n/r$ for each hypothetical period $r$ [@problem_id:48166].

#### Analysis of Success and Failure

Once a candidate period $r$ is found, the final classical step is to find a factor of $N$. If $r$ is even, we can compute $x = a^{r/2}$. Since $a^r \equiv 1 \pmod N$, we have $(a^{r/2}-1)(a^{r/2}+1) \equiv 0 \pmod N$. This means $N$ must divide the product $(x-1)(x+1)$. If, additionally, $a^{r/2} \not\equiv -1 \pmod N$, then $N$ does not divide $(x+1)$ alone. In this case, $\text{gcd}(x-1, N)$ and $\text{gcd}(x+1, N)$ are guaranteed to be non-trivial factors of $N$.

The algorithm can fail at this final stage for two reasons:
1.  The measured period $r$ is odd.
2.  The period $r$ is even, but $a^{r/2} \equiv -1 \pmod N$.

For example, when attempting to factor $N=65$, if we choose the base $a=2$, the quantum subroutine would (ideally) return the order $r=12$. This is even, so we proceed to check the second condition. We find $2^{12/2} = 2^6 = 64 \equiv -1 \pmod{65}$. Thus, for the base $a=2$, the classical post-processing step fails [@problem_id:48315]. In such cases, we must simply choose a new random base $a$ and repeat the algorithm.

A more subtle source of difficulty arises from the measurement process itself. The measurement outcome $k$ approximates $j/r$. The [continued fraction algorithm](@entry_id:635794) will find $r$ only if $\text{gcd}(j,r)=1$. If $j$ and $r$ share a common factor, the algorithm will likely return a [divisor](@entry_id:188452) of $r$, which may or may not be useful. The probability of obtaining a "successful" measurement (i.e., one corresponding to a $j$ coprime to $r$) can be quantified. In an idealized scenario where each of the $r$ possible values of $j \in \{0, \ldots, r-1\}$ is equally likely, the success probability is the ratio of the number of integers coprime to $r$ to the total number, which is $\phi(r)/r$, where $\phi$ is Euler's totient function [@problem_id:48293].

The probability of the classical step failing for a randomly chosen base $a$ is a question of profound group-theoretic nature. For an integer $N$ with $k$ distinct prime factors, the probability that a random base $a$ with an even order $r$ fails because $a^{r/2} \equiv -1 \pmod N$ can be precisely calculated. This probability depends on the structure of the 2-Sylow subgroup of the [multiplicative group](@entry_id:155975) $(\mathbb{Z}/N\mathbb{Z})^\times$ [@problem_id:48186], [@problem_id:48217]. This advanced analysis reveals that for numbers with many prime factors, this specific mode of failure becomes less likely, increasing the overall efficacy of the algorithm.

### Application II: The Discrete Logarithm Problem

The [discrete logarithm problem](@entry_id:144538) (DLP) is another cornerstone of modern cryptography, and like [integer factorization](@entry_id:138448), it is believed to be intractable for classical computers. The problem is to find an integer $x$ such that $g^x \equiv h \pmod p$, given a prime $p$, a generator $g$ of the multiplicative group $(\mathbb{Z}/p\mathbb{Z})^\times$, and an element $h$ in that group.

#### Framing DLP as a Periodicity Problem

The quantum algorithm for the DLP elegantly transforms the problem into one of finding a hidden period, but this time in a two-dimensional space. The algorithm considers the function of two variables, $f(a,b) = g^a h^b \pmod p$, defined over $\mathbb{Z}_r \times \mathbb{Z}_r$, where $r$ is the order of $g$. Since $h \equiv g^x$, we can write this as $f(a,b) = g^{a+xb} \pmod p$.

This function $f(a,b)$ is periodic. The set of vectors $(a,b)$ for which $f(a,b)$ is constant forms a set of shifted [parallel lines](@entry_id:169007) in the $\mathbb{Z}_r \times \mathbb{Z}_r$ grid. Specifically, the function value depends only on the value of $a+xb \pmod r$. The "period" is a vector in this 2D space. The set of vectors $(a,b)$ that map to the same value as $(0,0)$ satisfies $a+xb \equiv 0 \pmod r$. This relation defines a one-dimensional subgroup (or a lattice) $L$ within the group $\mathbb{Z}_r \times \mathbb{Z}_r$. The [quantum algorithm](@entry_id:140638)'s task is to identify this hidden subgroup.

The algorithm begins by preparing two quantum registers in a uniform superposition over all possible pairs $(a,b)$:

$$
|\psi_{init}\rangle = \frac{1}{r} \sum_{a=0}^{r-1} \sum_{b=0}^{r-1} |a\rangle |b\rangle
$$

An oracle then computes $f(a,b)$ into a third register. A measurement on this third register collapses the state of the first two registers into a uniform superposition over all pairs $(a,b)$ that yielded the measured function value. This state corresponds to a [coset](@entry_id:149651) of the hidden subgroup $L$. For instance, before any QFT, the probability of measuring any specific basis state $|k\rangle|j\rangle$ in the first two registers is simply $1/r^2$, reflecting the initial uniform superposition [@problem_id:48200].

#### The 2D QFT and Extracting the Logarithm

To find the hidden structure, a 2D QFT over $\mathbb{Z}_r \times \mathbb{Z}_r$ is applied to the first two registers. Just as the 1D QFT maps a periodic state to a sparse set of peaks, the 2D QFT maps a state supported on a hidden subgroup [coset](@entry_id:149651) to a state supported on its dual subgroup.

The measurement outcomes $(k_1, k_2)$ after the 2D QFT are not random. They are constrained by a condition that is dual to the hidden subgroup's structure. The amplitude for a state $|k_1, k_2\rangle$ will be non-zero only if the character $\chi_{(k_1,k_2)}(a,b) = \exp(\frac{2\pi i}{r}(k_1 a + k_2 b))$ is trivial on the hidden subgroup $L$. That is, for all $(a,b)$ such that $a+xb \equiv 0 \pmod r$, we must have $k_1 a + k_2 b \equiv 0 \pmod r$. Substituting $a \equiv -xb \pmod r$ into this condition gives $k_1(-xb) + k_2 b \equiv 0 \pmod r$, which simplifies to $b(-xk_1+k_2) \equiv 0 \pmod r$. Since this must hold for all $b$, we find the crucial relation:

$$
-xk_1 + k_2 \equiv 0 \pmod r \quad \text{or} \quad k_2 \equiv xk_1 \pmod r
$$

This single measurement outcome $(k_1, k_2)$ provides one linear equation for the unknown [discrete logarithm](@entry_id:266196) $x$. If $\text{gcd}(k_1, r)=1$, we can find $x$ directly by computing $x \equiv k_2 k_1^{-1} \pmod r$. If not, additional runs of the algorithm will yield other pairs $(k_1', k_2')$, providing more equations that can be combined to solve for $x$. The number of possible measurement outcomes $(k_1, k_2)$ that satisfy this [congruence](@entry_id:194418) for a given $x$ is exactly $r$, since for each of the $r$ choices for $k_1$, the value of $k_2$ is uniquely determined [@problem_id:48297].

This general method can be adapted to variations of the oracle function. For example, for a [generalized function](@entry_id:182848) $f(a,b) = g^{\alpha a} h^{\beta b}$, the same principles apply, leading to a different [linear congruence](@entry_id:273259) that reveals the ratio between coefficients related to $x$ [@problem_id:48312]. This demonstrates the robustness of the QFT-based approach. The underlying geometry can be viewed as finding a hidden shifted lattice, where the Fourier coefficients encode the shift in their phase [@problem_id:48211].

### Generalizations and the Hidden Subgroup Problem Framework

The algorithms for [period-finding](@entry_id:141657) and discrete logarithms are specific instances of a more general problem: the **Abelian Hidden Subgroup Problem (HSP)**. The HSP provides a unified framework for understanding a wide class of quantum algorithms.

#### The Abelian Hidden Subgroup Problem

In an Abelian group $G$, given a function $f: G \to S$ that is constant on the cosets of an unknown subgroup $H \le G$ and distinct on different [cosets](@entry_id:147145), the goal is to find a set of generators for $H$. The standard quantum algorithm involves preparing a superposition over $G$, applying the oracle for $f$, measuring the output register to create a superposition over a random [coset](@entry_id:149651) of $H$, and finally applying the QFT over $G$. A measurement of the final state yields an element of the [dual group](@entry_id:141479) $G^*$ that is trivial on $H$, providing information that restricts the possibilities for $H$.

A prime example is **Simon's Algorithm**, which solves the HSP over the group $G = (\mathbb{Z}_2^n, \oplus)$. Here, the function has a hidden period $s$, such that $f(x) = f(y)$ if and only if $y = x \oplus s$. This corresponds to a hidden subgroup $H = \{0, s\}$. The QFT over this group is the Walsh-Hadamard transform. A measurement after the transform yields a vector $y$ such that the bitwise inner product $y \cdot s \equiv 0 \pmod 2$. By collecting several such [linearly independent](@entry_id:148207) vectors $y_i$, one can solve the resulting system of linear equations to find the hidden string $s$ [@problem_id:48163].

#### The Hidden Coset and Hidden Shift Problems

A closely related problem is the **Hidden Coset Problem**, where the subgroup $H$ is known, but the state is a superposition over an unknown [coset](@entry_id:149651) $s+H$. The task is to find the shift $s$. The QFT provides a beautiful solution. The locations of the non-zero peaks in the Fourier spectrum are determined by the subgroup $H$ (they form the dual subgroup $H^\perp$), while the unknown shift $s$ is encoded in the *relative phases* between these peaks. For a state over the [coset](@entry_id:149651) $s+\langle r \rangle$ in $\mathbb{Z}_N$, the amplitude of the $c$-th Fourier peak (at position $y_c = c \cdot N/r$) has a phase of $2\pi i s y_c / N$. The relative phase between two peaks is therefore directly proportional to $s$ and the distance between the peaks, allowing for the determination of $s$ [@problem_id:48159]. The probability of measuring any given Fourier peak depends on the structure of the function defining the cosets, as exemplified by specific instances of the Hidden Shift problem [@problem_id:48224].

This framework is surprisingly robust. It can be extended to cases where the [periodicity](@entry_id:152486) is not exact but "twisted", such as when $f(x+r) = e^{i\theta}f(x)$. In this scenario, the QFT still produces sharp peaks, but their locations in the spectrum are shifted by an amount proportional to the twist angle $\theta$ [@problem_id:48158]. Similarly, faulty oracles that introduce systematic phase errors can be analyzed, as they correspond to shifts in the Fourier domain [@problem_id:48151].

#### A Glimpse into Non-Abelian HSP

The success of the HSP framework for Abelian groups has inspired significant research into its non-Abelian counterpart. For a non-Abelian group $G$, the QFT is defined in terms of the group's [irreducible representations](@entry_id:138184) (irreps). The algorithm proceeds similarly, but the final measurement yields an irrep $\rho$ of $G$. The probability distribution over the irreps contains information about the hidden subgroup $H$.

For example, in the dihedral group $D_{16}$, if the hidden subgroup is $H = \langle r^4 \rangle$, the probability of measuring the trivial irrep after the QFT is simply the ratio of the subgroup size to the group size, $|H|/|G|$ [@problem_id:48139]. For more complex irreps, such as the 2-dimensional irrep of the [symmetric group](@entry_id:142255) $S_3$, the probabilities depend on the characters and [matrix elements](@entry_id:186505) of the representation, requiring tools from representation theory for their calculation [@problem_id:48287]. While a general, efficient [quantum algorithm](@entry_id:140638) for the non-Abelian HSP remains elusive, this area continues to be a fertile ground for research, holding the key to solving problems like the Graph Isomorphism and certain lattice problems.