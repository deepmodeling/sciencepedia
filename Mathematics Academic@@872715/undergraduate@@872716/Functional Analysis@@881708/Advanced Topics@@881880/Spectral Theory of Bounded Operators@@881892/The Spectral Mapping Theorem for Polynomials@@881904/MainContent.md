## Introduction
In [functional analysis](@entry_id:146220), the [spectrum of an operator](@entry_id:272027) generalizes the concept of eigenvalues, providing deep insights into the operator's properties. A fundamental question then arises: if we know the [spectrum of an operator](@entry_id:272027) $T$, what can we say about the spectrum of a new operator formed by applying a polynomial to it, $p(T)$? The Spectral Mapping Theorem provides a beautifully complete answer to this question, establishing a direct and powerful connection between $\sigma(T)$ and $\sigma(p(T))$. This article will guide you through this cornerstone result. The first chapter, **Principles and Mechanisms**, will build your intuition from [finite-dimensional spaces](@entry_id:151571), present the formal theorem and its proof for Banach spaces, and explore its immediate consequences. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the theorem's utility in fields ranging from linear algebra and differential equations to modern [graph signal processing](@entry_id:184205). Finally, the **Hands-On Practices** chapter will allow you to apply these concepts to solve concrete problems, solidifying your understanding of this essential theorem.

## Principles and Mechanisms

In our study of [linear operators](@entry_id:149003), the concept of the spectrum serves as a powerful generalization of eigenvalues for matrices. A natural and fundamental question arises: if we understand the [spectrum of an operator](@entry_id:272027) $T$, what can we say about the spectrum of a new operator formed by applying a function, such as a polynomial, to $T$? The answer to this question is provided by a cornerstone result in [operator theory](@entry_id:139990) known as the **Spectral Mapping Theorem**. This chapter will elucidate the version of this theorem for polynomials, exploring its theoretical underpinnings and demonstrating its wide-ranging utility through various applications.

### The Intuitive Foundation: Eigenvalues and Polynomials

Before delving into the abstract framework of Banach spaces, let us build our intuition by considering the familiar territory of finite-dimensional [complex vector spaces](@entry_id:264355). Here, the spectrum of a linear operator $T$ is simply the set of its eigenvalues.

Suppose we have an operator $T: V \to V$, an eigenvector $v \in V$ (where $v \neq 0$), and its corresponding eigenvalue $\lambda \in \mathbb{C}$, such that $T(v) = \lambda v$. Now, let us construct a new operator by applying a polynomial $p(z) = c_n z^n + \dots + c_1 z + c_0$ to $T$. This new operator, denoted $p(T)$, is defined as $p(T) = c_n T^n + \dots + c_1 T + c_0 I$, where $I$ is the [identity operator](@entry_id:204623) and $T^k$ is the composition of $T$ with itself $k$ times.

How does this new operator $p(T)$ act on the eigenvector $v$? Let's first examine the action of $T^k$. A simple induction shows that $v$ is also an eigenvector of $T^k$ with eigenvalue $\lambda^k$.
For $k=2$, we have $T^2(v) = T(T(v)) = T(\lambda v) = \lambda T(v) = \lambda(\lambda v) = \lambda^2 v$.
Assuming $T^k(v) = \lambda^k v$, it follows that $T^{k+1}(v) = T(T^k(v)) = T(\lambda^k v) = \lambda^k T(v) = \lambda^k(\lambda v) = \lambda^{k+1} v$.

With this result, we can now compute the action of $p(T)$ on $v$ directly:
$$
\begin{align}
p(T)v  &= (c_n T^n + \dots + c_1 T + c_0 I)v \\
 &= c_n T^n(v) + \dots + c_1 T(v) + c_0 I(v) \\
 &= c_n \lambda^n v + \dots + c_1 \lambda v + c_0 v \\
 &= (c_n \lambda^n + \dots + c_1 \lambda + c_0)v \\
 &= p(\lambda)v
\end{align}
$$
This elegant result [@problem_id:1902447] reveals a profound connection: if $\lambda$ is an eigenvalue of $T$, then $p(\lambda)$ is an eigenvalue of $p(T)$, with the same eigenvector $v$. This suggests that the set of eigenvalues of $p(T)$ is precisely the set of values obtained by applying the polynomial $p$ to each eigenvalue of $T$. This relationship forms the intuitive core of the Spectral Mapping Theorem.

### The Spectral Mapping Theorem for Polynomials

The intuition developed for eigenvalues generalizes beautifully to the broader concept of the spectrum. For a [bounded linear operator](@entry_id:139516) $T$ on a complex Banach space $X$, its **spectrum**, denoted $\sigma(T)$, is the set of all $\lambda \in \mathbb{C}$ for which the operator $T - \lambda I$ is not invertible. The Spectral Mapping Theorem provides a complete characterization of the spectrum of a [polynomial of an operator](@entry_id:261608).

**Theorem (Spectral Mapping Theorem for Polynomials):** Let $T$ be a [bounded linear operator](@entry_id:139516) on a non-zero complex Banach space $X$, and let $p(z)$ be any polynomial with complex coefficients. Then the spectrum of the operator $p(T)$ is given by:
$$
\sigma(p(T)) = p(\sigma(T)) \equiv \{ p(\lambda) \mid \lambda \in \sigma(T) \}
$$

The proof of this theorem involves showing two set inclusions.

1.  **$p(\sigma(T)) \subseteq \sigma(p(T))$**: Let $\lambda \in \sigma(T)$. We want to show that $p(\lambda) \in \sigma(p(T))$. Consider the polynomial $q(z) = p(z) - p(\lambda)$. Since $z=\lambda$ is a root of $q(z)$, we can factor it as $q(z) = (z-\lambda)r(z)$ for some polynomial $r(z)$. Substituting the operator $T$ gives $p(T) - p(\lambda)I = (T-\lambda I)r(T)$. Since $T$ and $r(T)$ commute, this can also be written as $r(T)(T-\lambda I)$. Because $\lambda \in \sigma(T)$, the operator $T - \lambda I$ is not invertible. This implies that $p(T) - p(\lambda)I$ is also not invertible, which means, by definition, that $p(\lambda) \in \sigma(p(T))$.

2.  **$\sigma(p(T)) \subseteq p(\sigma(T))$**: Let $\mu \in \sigma(p(T))$. We want to show that $\mu = p(\lambda)$ for some $\lambda \in \sigma(T)$. Consider the polynomial $q(z) = p(z) - \mu$. Since we are working over the complex numbers, this polynomial can be factored completely by its roots $z_1, z_2, \dots, z_n$: $q(z) = c(z-z_1)(z-z_2)\dots(z-z_n)$, where $c$ is a non-zero constant. Substituting the operator $T$ gives $p(T) - \mu I = c(T-z_1I)(T-z_2I)\dots(T-z_nI)$. We know that $\mu \in \sigma(p(T))$, so the operator on the left-hand side, $p(T) - \mu I$, is not invertible. This requires that at least one of the factors on the right-hand side, say $T - z_i I$, must also be non-invertible. If $T-z_iI$ is not invertible, then $z_i \in \sigma(T)$. But what is $z_i$? It is a root of $q(z)$, so $q(z_i) = p(z_i) - \mu = 0$. This implies $\mu = p(z_i)$. Since we found a $z_i \in \sigma(T)$ such that $\mu = p(z_i)$, we have shown that $\mu \in p(\sigma(T))$.

Combining both inclusions establishes the theorem.

### Applications and Consequences of the Theorem

The Spectral Mapping Theorem is not merely a theoretical curiosity; it is a powerful computational and conceptual tool. It allows us to determine the spectrum of a complex operator $p(T)$ by performing a potentially much simpler calculation involving the spectrum of $T$ and the polynomial $p$.

#### Calculating Spectra and Spectral Radii

A direct application of the theorem is the calculation of spectra. Let's consider an operator whose spectrum is not just a finite set of points. For instance, the multiplication operator $T$ on the Hilbert space $H = L^2([0,1])$ defined by $(Tf)(x) = xf(x)$ has the spectrum $\sigma(T) = [0,1]$. If we construct a new operator $S = T^2 - 3T + 2I$, the Spectral Mapping Theorem tells us that $\sigma(S) = \sigma(p(T))$ where $p(z) = z^2 - 3z + 2$. Therefore, the spectrum of $S$ is the image of the interval $[0,1]$ under the map $p$:
$$
\sigma(S) = p([0,1]) = \{ z^2 - 3z + 2 \mid z \in [0,1] \}
$$
The function $p(z)$ is a parabola opening upwards with its vertex at $z = 1.5$. On the interval $[0,1]$, the function is strictly decreasing. Its maximum value is $p(0) = 2$ and its minimum value is $p(1) = 1-3+2=0$. Thus, the spectrum is the continuous interval $[0, 2]$ [@problem_id:1902923].

The theorem also provides a direct way to calculate the **spectral radius**, $r(S) = \sup \{|\mu| : \mu \in \sigma(S)\}$. Applying the theorem:
$$
r(p(T)) = \sup \{ |\mu| : \mu \in \sigma(p(T)) \} = \sup \{ |p(\lambda)| : \lambda \in \sigma(T) \}
$$
Since the spectrum $\sigma(T)$ is a compact set and the function $|p(z)|$ is continuous, the supremum is always attained, so we can replace it with a maximum [@problem_id:1902695]:
$$
r(p(T)) = \max_{\lambda \in \sigma(T)} |p(\lambda)|
$$

For example, consider the $2 \times 2$ matrix 
$$ x = \begin{pmatrix} 1  3 \\ 1  -1 \end{pmatrix} $$
Its [characteristic polynomial](@entry_id:150909) is $\det(x - \lambda I) = \lambda^2 - 4$, so its eigenvalues (spectrum) are $\sigma(x) = \{-2, 2\}$. Let's find the spectral radius of $p(x) = x^2 - x + I$. Using the theorem, the spectrum of $p(x)$ is $p(\sigma(x)) = \{p(-2), p(2)\}$. We calculate $p(-2) = (-2)^2 - (-2) + 1 = 7$ and $p(2) = 2^2 - 2 + 1 = 3$. So, $\sigma(p(x)) = \{3, 7\}$. The spectral radius is $r(p(x)) = \max\{|3|, |7|\} = 7$ [@problem_id:1866617].

#### Deducing Spectral Properties from Operator Algebra

One of the most profound consequences of the theorem is its ability to constrain the [spectrum of an operator](@entry_id:272027) that satisfies a given polynomial equation. Suppose an operator $T$ satisfies $q(T) = 0$ for some polynomial $q(z)$. This means the operator $q(T)$ is the zero operator, whose spectrum is just $\{0\}$. By the Spectral Mapping Theorem:
$$
\sigma(q(T)) = q(\sigma(T)) = \{0\}
$$
This implies that for every $\lambda$ in the spectrum of $T$, we must have $q(\lambda) = 0$. In other words, the spectrum of $T$ must be a subset of the roots of the polynomial $q(z)$.

For example, consider the cyclic [shift operator](@entry_id:263113) on $\mathbb{C}^4$, $T(x_1, x_2, x_3, x_4) = (x_4, x_1, x_2, x_3)$. It is easy to see that applying this operator four times returns the original vector, so $T^4 = I$, or $T^4 - I = 0$. The associated polynomial is $q(z) = z^4-1$. Therefore, the spectrum of $T$ must be a subset of the roots of $z^4-1$, which are the fourth roots of unity: $\{1, i, -1, -i\}$. This algebraic constraint dramatically narrows down the possible eigenvalues. We can then use this knowledge to find the spectrum of a related operator, like $S = T-I$. Using the theorem again with $p(z) = z-1$, we find that $\sigma(S) = p(\sigma(T)) = \{1-1, i-1, -1-1, -i-1\} = \{0, -1+i, -2, -1-i\}$ [@problem_id:1902407].

This principle also helps analyze more complex situations. If an operator satisfies $T^3=T$, then $\sigma(T)$ must be a subset of the roots of $z^3-z=0$, which are $\{-1, 0, 1\}$. Now, if we want to find the possible values in the spectrum of $P = 2I - T^2$, we can apply the theorem to the polynomial $p(z) = 2-z^2$. The spectrum $\sigma(P)$ must be a subset of $p(\{-1, 0, 1\}) = \{2-(-1)^2, 2-0^2, 2-1^2\} = \{1, 2\}$. Depending on the specific choice of $T$ (e.g., $T=0$, $T=I$, or an operator with multiple eigenvalues), the spectrum of $P$ could be $\{2\}$, $\{1\}$, or $\{1, 2\}$, but it can never contain any other values [@problem_id:1902446]. It is crucial to remember that $\sigma(T)$ is a *subset* of the roots. Which subset it is depends on the minimal polynomial of the operator [@problem_id:1902453].

#### Invertibility and Polynomials of Operators

The concept of invertibility is intrinsically linked to the spectrum: an operator $S$ is invertible if and only if $0 \notin \sigma(S)$. The Spectral Mapping Theorem translates questions about operator invertibility into questions about the [roots of polynomials](@entry_id:154615).

Consider a scenario where we have two polynomials, $p_1(z)$ and $p_2(z)$, and we know that the operators $p_1(T)$ and $p_2(T)$ are both invertible. This means:
$$
0 \notin \sigma(p_1(T)) = p_1(\sigma(T)) \quad \text{and} \quad 0 \notin \sigma(p_2(T)) = p_2(\sigma(T))
$$
This tells us that for any $\lambda \in \sigma(T)$, it must be that $p_1(\lambda) \neq 0$ and $p_2(\lambda) \neq 0$. In essence, the spectrum of $T$ does not contain any roots of $p_1(z)$ or $p_2(z)$.

Now, what can we say about the operator $q(T)$, where $q(z)$ is the greatest common divisor (GCD) of $p_1(z)$ and $p_2(z)$? The roots of $q(z)$ are precisely the common roots of $p_1(z)$ and $p_2(z)$. Since no element of $\sigma(T)$ can be a root of either polynomial, it certainly cannot be a common root. Therefore, for every $\lambda \in \sigma(T)$, we must have $q(\lambda) \neq 0$. Applying the theorem one last time:
$$
0 \notin q(\sigma(T)) = \sigma(q(T))
$$
This proves that the operator $q(T)$ must be invertible [@problem_id:1902445]. This is a remarkable demonstration of how abstract properties of operators can be deduced by reasoning about the algebraic properties of polynomials.

#### Quasinilpotence and Spectral Collapse

An operator is called **quasinilpotent** if its spectrum consists of only the number zero, i.e., $\sigma(S) = \{0\}$. A key property of quasinilpotent operators is that their [spectral radius](@entry_id:138984) is $r(S)=0$.

The Spectral Mapping Theorem can reveal situations where an operator, which may itself be quite complex, has a very simple spectrum. Suppose we have an operator $T$ and a polynomial $p(z)$ such that $p(z)$ takes on the same constant value $c$ for every $\lambda$ in the spectrum of $T$. That is, $p(\lambda) = c$ for all $\lambda \in \sigma(T)$.
According to the theorem, the spectrum of the operator $S = p(T)$ is:
$$
\sigma(S) = p(\sigma(T)) = \{ p(\lambda) \mid \lambda \in \sigma(T) \} = \{c\}
$$
Even if $S$ is not the simple scalar operator $cI$, its spectrum collapses to a single point. The spectral radius of $S$ is therefore simply $r(S) = |c|$ [@problem_id:1902450]. From this, we can see that the operator $S - cI$ has spectrum $\sigma(S - cI) = \sigma(S) - c = \{c\} - c = \{0\}$. Thus, $S - cI$ is quasinilpotent.

This principle is especially useful when dealing with operators built from a known [quasinilpotent operator](@entry_id:272812). For example, the Volterra integral operator, $(Af)(x) = \int_0^x f(t)dt$, is famously quasinilpotent with $\sigma(A) = \{0\}$. If we construct a more complicated operator as a polynomial in $A$, say $B = q(A) = \beta A^2 + \alpha A + \gamma I$, its spectrum is immediately found:
$$
\sigma(B) = q(\sigma(A)) = q(\{0\}) = \{\beta(0)^2 + \alpha(0) + \gamma\} = \{\gamma\}
$$
We can even take this one step further. If we then form another operator $p(B)$, its spectrum is simply $p(\sigma(B)) = p(\{\gamma\}) = \{p(\gamma)\}$ [@problem_id:1902414]. This ability to track the spectrum through successive polynomial transformations, starting from a simple base case, showcases the immense practical power of the Spectral Mapping Theorem.