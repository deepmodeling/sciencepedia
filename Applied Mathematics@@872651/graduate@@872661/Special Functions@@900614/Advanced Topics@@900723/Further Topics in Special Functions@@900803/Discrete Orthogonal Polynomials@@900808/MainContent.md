## Introduction
Discrete [orthogonal polynomials](@entry_id:146918) represent a powerful and elegant class of [special functions](@entry_id:143234) that serve as a cornerstone in both pure and applied mathematics. Just as [trigonometric functions](@entry_id:178918) provide a natural basis for analyzing periodic phenomena, these polynomials offer the ideal framework for understanding systems defined on discrete sets of points, such as integers. Their significance stems from a rich theoretical structure that connects algebra, calculus of finite differences, and [hypergeometric series](@entry_id:192973). However, navigating this theory can be challenging, as the true utility of these polynomials lies not just in their definitions but in a web of powerful, interconnected properties that are not immediately obvious.

This article bridges the gap between abstract definitions and practical application by systematically exploring the world of discrete [orthogonal polynomials](@entry_id:146918). It is structured to guide you from foundational concepts to advanced applications, providing a coherent and comprehensive understanding of the subject.

The first chapter, "Principles and Mechanisms," lays the theoretical groundwork. We will construct these polynomials from first principles, explore the fundamental concept of orthogonality on a discrete support, and uncover the three defining properties that characterize the classical families: the [three-term recurrence relation](@entry_id:176845), the second-order difference equation, and the Rodrigues-type formula. The subsequent chapter, "Applications and Interdisciplinary Connections," demonstrates the remarkable utility of this mathematical machinery. We will see how discrete orthogonal polynomials provide exact solutions and deep insights into problems in probability theory, quantum mechanics, coding theory, and computational science. Finally, the "Hands-On Practices" section offers a curated set of problems designed to solidify your grasp of these concepts and techniques. By starting with the core principles, we will build a solid foundation for understanding the remarkable power and versatility of these mathematical objects.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms that define and characterize discrete [orthogonal polynomials](@entry_id:146918). Building upon the introductory concepts, we will systematically construct these mathematical objects from first principles, explore their essential properties, and uncover the rich structure that connects different families of polynomials.

### The Foundation of Orthogonality on a Discrete Support

The concept of orthogonality is a generalization of the geometric notion of perpendicular vectors. In the context of function spaces, it is defined by means of an **inner product**. For discrete orthogonal polynomials, the variable $x$ does not vary continuously but is restricted to a [discrete set](@entry_id:146023) of points, often non-negative integers $S = \{0, 1, 2, \dots, N\}$ or $S = \{0, 1, 2, \dots\}$.

The inner product of two real-valued functions, $f(x)$ and $g(x)$, on such a discrete support is defined as a weighted sum:

$$
\langle f, g \rangle = \sum_{x \in S} f(x) g(x) w(x)
$$

Here, $w(x)$ is a non-negative **weight function** defined on the support $S$, for which the total sum $\sum_{x \in S} w(x)$ is finite and positive. A sequence of polynomials $\{p_n(x)\}_{n=0}^{N}$ (where the degree of $p_n(x)$ is exactly $n$) is said to be **orthogonal** with respect to the weight function $w(x)$ if their inner product is zero for different degrees:

$$
\langle p_n, p_m \rangle = \sum_{x \in S} p_n(x) p_m(x) w(x) = d_n^2 \delta_{nm}
$$

where $\delta_{nm}$ is the Kronecker delta, which is 1 if $n=m$ and 0 otherwise. The constant $d_n^2 = \langle p_n, p_n \rangle$ is the squared **norm** of the polynomial $p_n(x)$. If $d_n^2=1$ for all $n$, the polynomials are called **orthonormal**.

### A Constructive Approach: The Gram-Schmidt Procedure

While the definition of orthogonality provides a condition to verify, it does not immediately provide the polynomials themselves. The most fundamental method for constructing a set of [orthogonal polynomials](@entry_id:146918) is the **Gram-Schmidt [orthogonalization](@entry_id:149208) process**. This procedure takes a set of linearly independent functions—in our case, the simple monomial basis $\{1, x, x^2, \dots, x^n, \dots\}$—and generates an orthogonal set that spans the same space.

Let us denote the sequence of monic [orthogonal polynomials](@entry_id:146918) by $\{\hat{p}_n(x)\}$, where a **monic** polynomial is one whose leading coefficient (the coefficient of the highest power of $x$) is 1. The Gram-Schmidt process proceeds as follows:

1.  Start with the simplest polynomial: $\hat{p}_0(x) = 1$.
2.  Construct $\hat{p}_1(x)$ by taking the next basis function, $x$, and subtracting its projection onto $\hat{p}_0(x)$:
    $$ \hat{p}_1(x) = x - \frac{\langle x, \hat{p}_0 \rangle}{\langle \hat{p}_0, \hat{p}_0 \rangle} \hat{p}_0(x) $$
3.  Continue this process. To find $\hat{p}_n(x)$, we take $x^n$ and subtract its projections onto all previously constructed orthogonal polynomials $\hat{p}_0, \hat{p}_1, \dots, \hat{p}_{n-1}$:
    $$ \hat{p}_n(x) = x^n - \sum_{k=0}^{n-1} \frac{\langle x^n, \hat{p}_k \rangle}{\langle \hat{p}_k, \hat{p}_k \rangle} \hat{p}_k(x) $$
The resulting polynomial $\hat{p}_n(x)$ is orthogonal to all $\hat{p}_k(x)$ for $k  n$ by construction, and it is monic because we start with $x^n$ and only subtract polynomials of lower degree.

To make this concrete, let's construct the second-degree monic Meixner polynomial, $\hat{M}_2(x; \beta, c)$ [@problem_id:655452]. The Meixner polynomials are orthogonal with respect to the weight function $w(x; \beta, c) = \frac{(\beta)_x c^x}{x!}$ for $x = 0, 1, 2, \dots$, where $\beta > 0$, $0  c  1$, and $(\beta)_x = \beta(\beta+1)\cdots(\beta+x-1)$ is the Pochhammer symbol.

The inner product is $\langle f, g \rangle = \sum_{x=0}^{\infty} f(x)g(x)w(x)$. The quantities $\mu_k = \langle x^k, 1 \rangle / \langle 1, 1 \rangle$ are the moments of the associated [discrete probability distribution](@entry_id:268307).

-   **Step 0:** The zeroth [monic polynomial](@entry_id:152311) is $\hat{M}_0(x) = 1$.

-   **Step 1:** The first [monic polynomial](@entry_id:152311) is:
    $$ \hat{M}_1(x) = x - \frac{\langle x, 1 \rangle}{\langle 1, 1 \rangle} = x - \mu_1 $$
    For the Meixner distribution, the first moment (mean) is $\mu_1 = \frac{\beta c}{1-c}$. Thus, $\hat{M}_1(x) = x - \frac{\beta c}{1-c}$.

-   **Step 2:** The second [monic polynomial](@entry_id:152311) is constructed from $x^2$:
    $$ \hat{M}_2(x) = x^2 - \frac{\langle x^2, \hat{M}_1 \rangle}{\langle \hat{M}_1, \hat{M}_1 \rangle} \hat{M}_1(x) - \frac{\langle x^2, \hat{M}_0 \rangle}{\langle \hat{M}_0, \hat{M}_0 \rangle} \hat{M}_0(x) $$
    This requires computing several inner products, which correspond to moments of the distribution. After carrying out these sums (a non-trivial exercise involving properties of the Gamma function and [hypergeometric series](@entry_id:192973)), we find the projection coefficients. For instance, the coefficient of $\hat{M}_1(x)$ is $\frac{\langle x^2, \hat{M}_1 \rangle}{\langle \hat{M}_1, \hat{M}_1 \rangle} = \frac{2\beta c + 1 + c}{1-c}$. The final result is:
    $$ \hat{M}_2(x; \beta, c) = x^2 - \frac{2\beta c+1+c}{1-c}x + \frac{\beta(\beta+1)c^2}{(1-c)^2} $$
This example illustrates that while the Gram-Schmidt process is fundamentally sound, its direct application can involve laborious calculations. This motivates the search for more direct and elegant characterizations of these polynomials.

### The Defining Properties of Classical Polynomials

The so-called "classical" families of discrete orthogonal polynomials (such as those of Hahn, Krawtchouk, Meixner, and Charlier) are special because they satisfy several powerful, equivalent properties. Understanding these properties provides deeper insight and more efficient tools than direct construction.

#### The Three-Term Recurrence Relation

A cornerstone of the theory of orthogonal polynomials is a result known as **Favard's Theorem**, which states that any sequence of monic [orthogonal polynomials](@entry_id:146918) $\{\hat{p}_n(x)\}$ must satisfy a [three-term recurrence relation](@entry_id:176845):

$$
\hat{p}_{n+1}(x) = (x - a_n) \hat{p}_n(x) - b_n \hat{p}_{n-1}(x), \quad \text{for } n \ge 0
$$

with initial conditions $\hat{p}_{-1}(x) = 0$ and $\hat{p}_0(x) = 1$. The recurrence coefficients $a_n$ and $b_n$ are constants (with respect to $x$) that depend on the specific polynomial family and its parameters. This relation is immensely powerful; it allows for the rapid generation of the entire polynomial sequence once the coefficients are known.

For example, the monic Meixner polynomials have coefficients [@problem_id:655461]:
$$ a_n = \frac{n(1+c) + \beta c}{1-c}, \qquad b_n = \frac{nc(n+\beta-1)}{(1-c)^2} $$
The [recurrence relation](@entry_id:141039) is not just a computational shortcut; it encodes the fundamental parameters of the system. Suppose experimental observation provides the values of certain recurrence coefficients. For instance, if we found that $a_0 = A$ and $b_2 = B$ for some positive constants $A$ and $B$, we could then work backward to identify the system parameters $\beta$ and $c$. Using the formulas above:
$$ a_0 = \frac{\beta c}{1-c} = A \quad \implies \quad \beta = \frac{A(1-c)}{c} $$
$$ b_2 = \frac{2c(2+\beta-1)}{(1-c)^2} = \frac{2c(\beta+1)}{(1-c)^2} = B $$
Substituting the expression for $\beta$ into the second equation yields a quadratic equation in $c$. Solving this equation gives the value of $c$ in terms of the "measured" coefficients $A$ and $B$, demonstrating the deep connection between the recurrence coefficients and the underlying structure of the polynomial family.

#### The Difference Equation as an Eigenvalue Problem

In analogy with classical continuous [orthogonal polynomials](@entry_id:146918) (e.g., Legendre, Hermite, Laguerre), which are [eigenfunctions](@entry_id:154705) of second-order linear [differential operators](@entry_id:275037), classical discrete orthogonal polynomials are [eigenfunctions](@entry_id:154705) of second-order linear **difference operators**.

A general linear second-order difference operator $\mathcal{L}$ acts on a function $f(x)$ by evaluating it at neighboring points, typically $x-1$, $x$, and $x+1$. A common form is:
$$ (\mathcal{L}f)(x) = B(x)[f(x+1) - f(x)] - D(x)[f(x) - f(x-1)] $$
where $B(x)$ and $D(x)$ are polynomials in $x$. The classical discrete polynomials $p_n(x)$ are the solutions to the eigenvalue equation:
$$ (\mathcal{L}p_n)(x) = \lambda_n p_n(x) $$
Here, $\lambda_n$ is the **eigenvalue**, a constant that depends on the degree $n$ but not on the variable $x$. A crucial property of this operator is that it does not change the degree of the polynomial it acts upon.

As a direct verification, consider the Charlier polynomial $C_2(x; a) = 1 - \frac{2x}{a} + \frac{x(x-1)}{a^2}$ and the operator $\mathcal{D}[f(x)] = -x f(x-1) + (x+a) f(x) - a f(x+1)$ [@problem_id:655590]. By substituting $f(x) = C_2(x; a)$, $f(x-1) = C_2(x-1; a)$, and $f(x+1) = C_2(x+1; a)$ into the expression for $\mathcal{D}$ and performing careful algebraic simplification, one finds that all terms involving $x$ cancel in a remarkable way, leaving:
$$ \mathcal{D}[C_2(x; a)] = 2 \left( 1 - \frac{2x}{a} + \frac{x(x-1)}{a^2} \right) = 2 C_2(x; a) $$
This calculation explicitly demonstrates that $C_2(x;a)$ is an [eigenfunction](@entry_id:149030) of $\mathcal{D}$ with the eigenvalue $\lambda_2 = 2$.

While direct verification is instructive, there is a more efficient method to determine the eigenvalue. Since $\mathcal{L}[p_n(x)]$ is a polynomial of the same degree as $p_n(x)$, we can find $\lambda_n$ by simply comparing the coefficients of the leading term, $x^n$, on both sides of the [eigenvalue equation](@entry_id:272921). Let $p_n(x) = c_n x^n + \dots$ (where $c_n \neq 0$). Then $\mathcal{L}[p_n(x)] = \lambda_n c_n x^n + \dots$. The eigenvalue is the ratio of these leading coefficients.

Let's apply this to the Hahn polynomials $Q_n(x; \alpha, \beta, N)$ [@problem_id:655426]. The Hahn operator is $L[f(x)] = B(x)\Delta f(x) - D(x)\nabla f(x)$, where $\Delta$ and $\nabla$ are the forward and [backward difference](@entry_id:637618) operators, and $B(x), D(x)$ are quadratic in $x$. If we take a generic quadratic $Q_2(x) = c_2 x^2 + c_1 x + c_0$, its [forward difference](@entry_id:173829) $\Delta Q_2(x)$ and [backward difference](@entry_id:637618) $\nabla Q_2(x)$ are both linear polynomials with leading term $2c_2 x$. When we compute $L[Q_2(x)]$, the highest power of $x$ comes from multiplying the $x^2$ term in $B(x)$ and $D(x)$ by the $x$ term in the differences. A careful calculation shows that the coefficient of $x^2$ in $L[Q_2(x)]$ is $2c_2(3+\alpha+\beta)$. Therefore, the eigenvalue is:
$$ \lambda_2 = \frac{\text{leading coeff of } L[Q_2(x)]}{\text{leading coeff of } Q_2(x)} = \frac{2c_2(3+\alpha+\beta)}{c_2} = 2(3+\alpha+\beta) $$
This method elegantly extracts the eigenvalue without needing the full expression for the polynomial or verifying the identity for all terms.

#### The Rodrigues-Type Formula

A third powerful characterization is the **Rodrigues-type formula**, which provides an explicit construction for the polynomials. It is analogous to the formula for classical continuous polynomials, such as $P_n(x) = \frac{(-1)^n}{2^n n!} \frac{d^n}{dx^n}(1-x^2)^n$ for the Legendre polynomials. The discrete version replaces the derivative with a difference operator.

The general form is typically $p_n(x) = \frac{C_n}{w(x)} \mathcal{O}^n [f(x)]$, where $C_n$ is a normalization constant, $w(x)$ is the weight function, $\mathcal{O}$ is a difference operator, and $f(x)$ is a function closely related to the weight.

For the monic Charlier polynomials $\hat{C}_n(x;a)$, the formula is [@problem_id:655457]:
$$ \hat{C}_n(x;a) = (-a)^n \frac{x!}{a^x} \Delta^n \left( \frac{a^{x-n}}{(x-n)!} \right) $$
where $\Delta f(x) = f(x+1) - f(x)$ is the [forward difference](@entry_id:173829) operator. Let's verify this for $n=2$. We need to compute the second-order difference $\Delta^2 f(x) = f(x+2) - 2f(x+1) + f(x)$ for the function $g(x) = \frac{a^{x-2}}{(x-2)!}$.
$$ \Delta^2 g(x) = \frac{a^x}{x!} - 2\frac{a^{x-1}}{(x-1)!} + \frac{a^{x-2}}{(x-2)!} $$
Plugging this into the Rodrigues formula for $n=2$:
$$ \hat{C}_2(x;a) = (-a)^2 \frac{x!}{a^x} \left( \frac{a^x}{x!} - 2\frac{a^{x-1}}{(x-1)!} + \frac{a^{x-2}}{(x-2)!} \right) $$
Distributing the pre-factors term by term, we get:
$$ \hat{C}_2(x;a) = a^2 \left( 1 - 2\frac{x}{a} + \frac{x(x-1)}{a^2} \right) = a^2 - 2ax + x^2 - x = x^2 - (2a+1)x + a^2 $$
This provides yet another path to the explicit polynomial form, complementing the Gram-Schmidt procedure and the recurrence relation.

### Deeper Structures and Interconnections

The properties discussed above are fundamental to individual polynomial families. However, the world of discrete [orthogonal polynomials](@entry_id:146918) is also characterized by profound structural relationships that connect them.

#### Self-Adjointness of the Difference Operator

A critical property of the classical difference operator $\mathcal{L}$ is that it is **self-adjoint** (or Hermitian) with respect to the associated inner product. This means that for any two functions $f(x)$ and $g(x)$ in the appropriate space:
$$ \langle \mathcal{L}f, g \rangle = \langle f, \mathcal{L}g \rangle $$
This property is the ultimate reason why the [eigenfunctions](@entry_id:154705) of $\mathcal{L}$ (the [orthogonal polynomials](@entry_id:146918)) corresponding to distinct eigenvalues are orthogonal. It elevates the difference equation from a mere curiosity to a central part of the orthogonality structure.

The power of self-adjointness is best seen in action. Consider the task of evaluating the sum $S = \sum_{x=0}^{N} Q_2(x) (\mathcal{L}[x Q_1(x)]) \rho(x)$, where $Q_n$ are Hahn polynomials and $\mathcal{L}$ is the Hahn operator [@problem_id:655579]. This sum is precisely the inner product $\langle Q_2, \mathcal{L}(x Q_1) \rangle$. A direct attack would be nightmarish. However, a strategic application of the core principles yields an elegant solution:

1.  Use **self-adjointness** to transfer the operator:
    $$ S = \langle Q_2, \mathcal{L}(x Q_1) \rangle = \langle \mathcal{L}Q_2, x Q_1 \rangle $$
2.  Use the **eigenvalue property** $\mathcal{L}Q_2 = \lambda_2 Q_2$:
    $$ S = \langle \lambda_2 Q_2, x Q_1 \rangle = \lambda_2 \langle Q_2, x Q_1 \rangle $$
3.  Use the **[three-term recurrence relation](@entry_id:176845)** to expand $x Q_1(x)$:
    $$ x Q_1(x) = a_1 Q_2(x) + b_1 Q_1(x) + c_1 Q_0(x) $$
4.  Substitute this into the inner product and use **orthogonality**:
    $$ S = \lambda_2 \langle Q_2, a_1 Q_2 + b_1 Q_1 + c_1 Q_0 \rangle = \lambda_2 ( a_1 \langle Q_2, Q_2 \rangle + b_1 \langle Q_2, Q_1 \rangle + c_1 \langle Q_2, Q_0 \rangle ) $$
    Since $\langle Q_2, Q_1 \rangle = 0$ and $\langle Q_2, Q_0 \rangle = 0$, the expression collapses to:
    $$ S = \lambda_2 a_1 \langle Q_2, Q_2 \rangle = \lambda_2 a_1 d_2^2 $$
The final result is obtained by simply plugging in the known formulas for the eigenvalue $\lambda_2$, the recurrence coefficient $a_1$, and the squared norm $d_2^2$. This demonstrates a beautiful synergy between the core properties.

#### Duality

Duality is a remarkable symmetry present in certain families of orthogonal polynomials, where the roles of the polynomial degree $n$ and the variable $x$ can be interchanged. This property often leads to surprising identities and computational shortcuts.

A prime example is the symmetric Krawtchouk polynomials $k_n(x, N)$ (corresponding to $p=1/2$), which satisfy the [self-duality](@entry_id:140268) relation [@problem_id:655453]:
$$ k_n(x, N) = k_x(n, N) \quad \text{for } n, x \in \{0, 1, \dots, N\} $$
Consider the sum $S = \sum_{n=0}^{N} \binom{N}{n} [k_n(x_0, N)]^2$ for a fixed integer $x_0$. At first glance, this seems difficult. However, applying the duality property transforms the sum:
$$ S = \sum_{n=0}^{N} \binom{N}{n} [k_{x_0}(n, N)]^2 $$
We now recognize this sum as the orthogonality relation for the Krawtchouk polynomial of degree $x_0$, $k_{x_0}(n, N)$, summed over the variable $n$. The orthogonality relation for Krawtchouk polynomials is $\sum_{x=0}^N \binom{N}{x} k_n(x,N)k_m(x,N) = 2^N \binom{N}{n} \delta_{nm}$. With roles reversed, our sum becomes $\sum_{n=0}^N \binom{N}{n} k_{x_0}(n,N)k_{x_0}(n,N) = 2^N \binom{N}{x_0}$. Duality turned a complex problem into a textbook application of orthogonality.

Duality can also be a structural principle that maps the properties of one polynomial family to another. The Hahn polynomials $Q_n(x; \alpha, \beta, N)$ and Dual Hahn polynomials $R_n(\lambda(x); \alpha, \beta, N)$ are related by $Q_x(n; \alpha, \beta, N) = R_n(\lambda(x); \alpha, \beta, N)$ [@problem_id:655444]. The [three-term recurrence](@entry_id:755957) for Hahn polynomials is a relation in the degree $n$. Duality implies this can be reinterpreted as a relation for Dual Hahn polynomials in the variable index $x$. This allows one to derive the recurrence coefficients for the dual family directly from the original family by a simple swap of variables $n \leftrightarrow x$.

#### Limiting Transitions and the Askey Scheme

The various families of discrete [orthogonal polynomials](@entry_id:146918) are not isolated specimens; they are part of a grand, hierarchical structure often visualized as the **Askey scheme**. This scheme organizes [hypergeometric orthogonal polynomials](@entry_id:182622), showing that many families can be obtained as special cases or limiting cases of more general ones.

A powerful way to see this is by examining the limit of the recurrence coefficients. For example, the Charlier polynomials can be derived from the Meixner polynomials [@problem_id:655458]. The Meixner recurrence coefficients depend on parameters $\beta$ and $c$:
$$ B_n^{Meixner} = \frac{n(1+c)+\beta c}{1-c}, \quad C_n^{Meixner} = \frac{nc(n+\beta-1)}{(1-c)^2} $$
To obtain a finite, non-trivial limit as $\beta \to \infty$, the parameter $c$ must approach zero. The key is to balance the terms. For $B_n$, the term $\beta c$ must remain finite, suggesting we should let $c$ depend on $\beta$ such that their product is constant. This motivates the substitution $c = a/\beta$ for some new parameter $a > 0$. Taking the limit $\beta \to \infty$:
$$ \lim_{\beta\to\infty} B_n^{Meixner} = \lim_{\beta\to\infty} \frac{n(1+a/\beta) + a}{1-a/\beta} = n+a $$
$$ \lim_{\beta\to\infty} C_n^{Meixner} = \lim_{\beta\to\infty} \frac{n(a/\beta)(n+\beta-1)}{(1-a/\beta)^2} = \lim_{\beta\to\infty} \frac{na(1 + (n-1)/\beta)}{(1-a/\beta)^2} = na $$
These limiting coefficients, $B_n' = n+a$ and $C_n' = an$, are precisely the recurrence coefficients for the monic Charlier polynomials $\hat{C}_n(x;a)$. This demonstrates a concrete link between the two families and illustrates a fundamental principle of the Askey scheme.

### Representation in the Newton Basis

Just as any polynomial can be written in the standard power basis $\{1, x, x^2, \dots\}$, it can also be expressed in other useful bases. For discrete polynomials, a particularly natural choice is the **Newton basis**, which consists of the **[falling factorials](@entry_id:274146)**:
$$ (x)_k = x(x-1)(x-2)\cdots(x-k+1) $$
for integer $k \ge 1$, with $(x)_0=1$. The expansion of a polynomial $P_n(x)$ in this basis is called its **Newton series**:
$$ P_n(x) = \sum_{k=0}^{n} c_k (x)_k $$
The coefficients $c_k$ have a beautiful connection to the [forward difference](@entry_id:173829) operator, $\Delta$. They are given by:
$$ c_k = \frac{\Delta^k P_n(0)}{k!} = \frac{1}{k!} \sum_{j=0}^{k} (-1)^{k-j} \binom{k}{j} P_n(j) $$
This means that to find the coefficient of $(x)_k$, one needs to evaluate the polynomial at the first $k+1$ integers, compute the $k$-th order [forward difference](@entry_id:173829) at $x=0$, and divide by $k!$.

For instance, to find the coefficient $c_2$ of $(x)_2$ in the Newton series for the Krawtchouk polynomial $K_3(x; p, N)$ [@problem_id:655575], we would compute $c_2 = \frac{\Delta^2 K_3(0)}{2!} = \frac{K_3(2) - 2K_3(1) + K_3(0)}{2}$. This involves calculating the value of the polynomial $K_3(x)$ at $x=0, 1, 2$ from its explicit sum definition, performing the subtractions, and simplifying the resulting expression in terms of the parameters $p$ and $N$. This provides a bridge between the calculus of finite differences and the theory of discrete [orthogonal polynomials](@entry_id:146918).