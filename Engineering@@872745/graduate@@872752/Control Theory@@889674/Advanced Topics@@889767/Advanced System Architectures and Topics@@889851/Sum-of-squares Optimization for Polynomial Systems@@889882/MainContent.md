## Introduction
Many fundamental challenges in engineering and the sciences—from proving the stability of a [nonlinear system](@entry_id:162704) to finding the [global minimum](@entry_id:165977) of a cost function—ultimately depend on answering a single, difficult question: is a given polynomial function nonnegative? While simple to state, this problem is notoriously intractable and classified as NP-hard for general polynomials, posing a significant barrier to systematic analysis and design. This intractability has motivated the development of powerful alternative approaches that trade absolute completeness for computational feasibility.

This article delves into one of the most successful and versatile of these approaches: **Sum-of-Squares (SOS) optimization**. Instead of directly tackling the nonnegativity problem, SOS methods enforce a stronger, [sufficient condition](@entry_id:276242)—that the polynomial can be expressed as a sum of squares of other polynomials. This algebraic property, which guarantees nonnegativity, can be verified efficiently using [convex optimization](@entry_id:137441), specifically [semidefinite programming](@entry_id:166778) (SDP). This article provides a graduate-level introduction to the theory, application, and practice of this transformative technique.

The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, explaining the core SOS certificate, its limitations, and the crucial connection to SDPs via the Gram [matrix representation](@entry_id:143451). It explores how this connection allows us to formulate tractable relaxations for complex optimization problems and introduces foundational results like the Positivstellensätze for constrained settings. The second chapter, **Applications and Interdisciplinary Connections**, showcases the profound impact of SOS programming, demonstrating its use in synthesizing Lyapunov functions and barrier certificates in control theory, performing [spectral factorization](@entry_id:173707) in signal processing, and estimating ground state energies in quantum physics. Finally, **Hands-On Practices** provides a set of guided exercises designed to build practical intuition and bridge the gap between theory and implementation.

## Principles and Mechanisms

The analysis and control of systems described by polynomial dynamics often hinge on our ability to answer a seemingly simple question: is a given multivariate polynomial nonnegative over a specified domain? Whether we are searching for a Lyapunov function to certify stability, a barrier certificate for safety verification, or the [global minimum](@entry_id:165977) of a cost function, the problem of polynomial nonnegativity is a recurring and fundamental challenge. However, this problem is notoriously difficult; for a general polynomial of degree four or higher, deciding global nonnegativity is an NP-hard problem [@problem_id:2751060]. This computational barrier arises because the nonnegativity of a high-degree polynomial can encode the solution to hard combinatorial problems.

Faced with this intractability, the field has developed a powerful alternative strategy: instead of tackling the nonnegativity problem directly, we enforce a stronger, [sufficient condition](@entry_id:276242) that is computationally tractable. This condition is that the polynomial can be written as a **sum of squares (SOS)**. This chapter elucidates the principles and mechanisms of this approach, detailing its theoretical foundations, its formulation as a convex optimization problem, and its application to [system analysis](@entry_id:263805) and design.

### The Sum-of-Squares Certificate and Its Limitations

A real polynomial $p(x)$ in variables $x \in \mathbb{R}^n$ is called a **sum of squares (SOS)** if there exist other real polynomials $q_1(x), \dots, q_m(x)$ such that $p(x) = \sum_{i=1}^m q_i(x)^2$. The central utility of this property lies in a simple observation: if a polynomial is a [sum of squares](@entry_id:161049), it must be globally nonnegative. For any real vector $x$, each term $q_i(x)^2$ is nonnegative, and thus their sum $p(x)$ must be nonnegative [@problem_id:2751064].

This provides a powerful one-way implication:
$$
p(x) \in \text{SOS} \implies p(x) \ge 0 \quad \forall x \in \mathbb{R}^n
$$

An SOS decomposition serves as an algebraic *certificate* of nonnegativity that is easily verifiable. This leads to a natural question: is the converse true? Is every globally nonnegative polynomial a [sum of squares](@entry_id:161049)? If so, the sets of nonnegative and SOS polynomials would be identical, and we would have an algebraic equivalent for the geometric condition of nonnegativity.

In a landmark investigation in 1888, David Hilbert showed that the answer is, in general, **no**. The cone of SOS polynomials is a strict subset of the cone of nonnegative polynomials. The exceptions, where nonnegativity and the SOS property coincide, are few and important:
1.  Univariate polynomials ($n=1$, any degree).
2.  Quadratic polynomials ($2d=2$, any number of variables $n$).
3.  Bivariate quartic polynomials ($n=2$, $2d=4$).

Outside of these specific cases, there exist polynomials that are nonnegative but cannot be written as a [sum of squares](@entry_id:161049) of polynomials [@problem_id:2751064] [@problem_id:2751109]. The most famous [counterexample](@entry_id:148660) is the **Motzkin polynomial**:
$$
m(x,y) = x^4y^2 + x^2y^4 + 1 - 3x^2y^2
$$
This polynomial is globally nonnegative, a fact that can be established by applying the Arithmetic Mean-Geometric Mean (AM-GM) inequality to the nonnegative terms $x^4y^2$, $x^2y^4$, and $1$, which shows $x^4y^2 + x^2y^4 + 1 \ge 3 \sqrt[3]{x^6y^6} = 3x^2y^2$. However, it can be proven that $m(x,y)$ is not a [sum of squares](@entry_id:161049) of polynomials [@problem_id:2751064]. The existence of such polynomials establishes that replacing the nonnegativity constraint with an SOS constraint is a conservative approximation, or a *relaxation*.

A deeper result by Emil Artin in 1927, solving Hilbert's 17th problem, showed that any nonnegative polynomial can be written as a [sum of squares](@entry_id:161049) of *rational functions* [@problem_id:2751055]. For the Motzkin polynomial, for instance, we have the identity $(x^2+y^2+1)m(x,y) = \text{sum of squares}$. Clearing the denominator gives $D(x,y)^2 m(x,y) = \text{SOS}$ for some polynomial $D$. While theoretically complete, searching for an unknown denominator polynomial makes the problem nonconvex and computationally intractable for optimization purposes.

Therefore, the power of the polynomial SOS approach stems not from its completeness, but from its tractability, which we explore next.

### The Gram Matrix Representation: Bridging SOS and SDP

The critical mechanism that renders the SOS condition useful is its exact equivalence to a problem in [convex optimization](@entry_id:137441), specifically, a **semidefinite program (SDP)**. This connection is established through the **Gram matrix** representation of a polynomial.

Consider a polynomial $p(x)$ of degree $2d$. If $p(x)$ is a sum of squares, $p(x) = \sum_i q_i(x)^2$, then the degree of each $q_i(x)$ can be no more than $d$. This means each $q_i(x)$ is a [linear combination](@entry_id:155091) of monomials up to degree $d$. Let $z(x)$ be a column vector containing a basis of all such monomials. For any $q_i(x)$, we can write it as $q_i(x) = v_i^T z(x)$ for some coefficient vector $v_i$. The sum of squares then becomes:
$$
p(x) = \sum_i (v_i^T z(x))^2 = \sum_i z(x)^T v_i v_i^T z(x) = z(x)^T \left( \sum_i v_i v_i^T \right) z(x)
$$
Defining the matrix $Q = \sum_i v_i v_i^T$, we arrive at the Gram matrix representation:
$$
p(x) = z(x)^T Q z(x)
$$
Each matrix $v_i v_i^T$ is symmetric and positive semidefinite, and since the cone of [positive semidefinite matrices](@entry_id:202354) is convex, their sum $Q$ must also be a symmetric and [positive semidefinite matrix](@entry_id:155134). This is denoted $Q \succeq 0$. This shows that if $p(x)$ is SOS, it admits a representation with a positive semidefinite Gram matrix. The converse is also true: if such a $Q \succeq 0$ exists, it can be factorized as $Q = \sum_i v_i v_i^T$, immediately yielding an SOS representation. Thus, the following are equivalent:
1.  $p(x)$ is a [sum of squares](@entry_id:161049).
2.  There exists a symmetric matrix $Q \succeq 0$ such that $p(x) = z(x)^T Q z(x)$.

The identity $p(x) = z(x)^T Q z(x)$ imposes a set of [linear equality constraints](@entry_id:637994) on the entries of $Q$. This is because the coefficients of $p(x)$ must match the coefficients of the polynomial resulting from expanding the [quadratic form](@entry_id:153497) $z(x)^T Q z(x)$.

**Example: A Bivariate Quartic Polynomial** [@problem_id:2751087]
Let $p(x_1, x_2)$ be a polynomial of total degree at most four. The degree of the constituent squares can be at most two. A basis for monomials of degree up to two is given by the vector:
$$
z(x) = \begin{pmatrix} 1 & x_1 & x_2 & x_1^2 & x_1 x_2 & x_2^2 \end{pmatrix}^T
$$
The Gram matrix $Q$ will be a $6 \times 6$ [symmetric matrix](@entry_id:143130). If we expand $z(x)^T Q z(x)$ and equate its coefficients with those of $p(x_1, x_2) = \sum_{i+j \le 4} c_{ij} x_1^i x_2^j$, we obtain a [system of linear equations](@entry_id:140416). For example, the coefficient of $x_1^4$ in $p(x)$ is $c_{40}$. In the expansion of $z(x)^T Q z(x)$, the only term that produces $x_1^4$ is $q_{44} z_4(x)^2 = q_{44} (x_1^2)^2$. Thus, we have the constraint $c_{40} = q_{44}$. The coefficient of $x_1^2 x_2$ is $c_{21}$. Terms producing $x_1^2 x_2$ are $q_{25} z_2(x)z_5(x)$ and $q_{52} z_5(x)z_2(x)$ (which are the same due to symmetry), and $q_{34} z_3(x)z_4(x)$ and $q_{43} z_4(x)z_3(x)$. This yields the constraint $c_{21} = 2q_{25} + 2q_{34}$. Continuing this for all 15 monomials of degree up to four yields 15 [linear equations](@entry_id:151487) relating the 21 unique entries of the [symmetric matrix](@entry_id:143130) $Q$ to the 15 coefficients of $p(x)$.

The task of checking if $p(x)$ is SOS is now reduced to a **[semidefinite programming](@entry_id:166778) (SDP) feasibility problem**:
$$
\text{Find } Q \in \mathbb{S}^k \quad \text{such that} \quad \mathcal{A}(Q) = c \quad \text{and} \quad Q \succeq 0
$$
where $\mathbb{S}^k$ is the space of $k \times k$ [symmetric matrices](@entry_id:156259), $\mathcal{A}(Q)=c$ represents the linear coefficient-matching constraints, and $Q \succeq 0$ is the [positive semidefiniteness](@entry_id:147720) constraint. SDPs are a class of convex optimization problems that can be solved efficiently (in [polynomial time](@entry_id:137670) to a given accuracy) using [interior-point methods](@entry_id:147138). This tractability is the principal reason for the widespread adoption of SOS techniques [@problem_id:2751060].

### SOS Relaxations for Polynomial Optimization

The ability to check the SOS property via SDP allows us to formulate tractable relaxations for hard [polynomial optimization](@entry_id:162619) problems.

#### Unconstrained Global Optimization

Consider the problem of finding the [global minimum](@entry_id:165977) of a polynomial $p(x)$:
$$
p^* = \min_{x \in \mathbb{R}^n} p(x)
$$
This is equivalent to finding the largest scalar $\gamma$ such that $p(x) - \gamma \ge 0$ for all $x \in \mathbb{R}^n$. As previously discussed, this nonnegativity constraint is intractable. We relax it to an SOS condition:
$$
\gamma_{\text{sos}} = \sup_{\gamma \in \mathbb{R}} \quad \text{s.t.} \quad p(x) - \gamma \in \text{SOS}
$$
This is the **primal SOS program**. Because the SOS condition is sufficient but not necessary for nonnegativity, $\gamma_{\text{sos}}$ is a lower bound on the true minimum $p^*$, i.e., $\gamma_{\text{sos}} \le p^*$. This formulation can be directly translated into an SDP.

**Example: Analytical Solution of an SOS Program** [@problem_id:2751032]
Let's find the SOS lower bound on the minimum of $p(x) = x^4 + ax^2 + 1$. We seek the maximum $t$ such that $p(x) - t = x^4 + ax^2 + (1-t)$ is SOS. Using the monomial basis $z(x) = (1, x, x^2)^T$, we require the existence of a matrix $Q \succeq 0$ such that:
$$
x^4 + ax^2 + (1-t) = \begin{pmatrix} 1 & x & x^2 \end{pmatrix} Q \begin{pmatrix} 1 \\ x \\ x^2 \end{pmatrix}
$$
Matching coefficients reveals that $Q$ must have the form:
$$
Q = \begin{pmatrix} 1-t & 0 & q_{13} \\ 0 & q_{22} & 0 \\ q_{13} & 0 & 1 \end{pmatrix}
$$
subject to the linear constraint $2q_{13} + q_{22} = a$. For $Q$ to be positive semidefinite, we require all principal minors to be nonnegative. This simplifies to two key conditions: $q_{22} \ge 0$ and $(1-t) - q_{13}^2 \ge 0$. We wish to maximize $t$, which is equivalent to maximizing $t \le 1 - q_{13}^2$. Using the linear constraint to express $q_{13} = (a - q_{22})/2$, we want to maximize $t$ subject to $t \le 1 - \frac{(a-q_{22})^2}{4}$ and $q_{22} \ge 0$. This is achieved by finding the value of $q_{22} \ge 0$ that minimizes $(a-q_{22})^2$.
- If $a \ge 0$, the minimum is at $q_{22}=a$, giving $t \le 1$. The optimal bound is $t^*=1$.
- If $a  0$, the minimum over $q_{22} \ge 0$ is at $q_{22}=0$, giving $t \le 1 - a^2/4$. The optimal bound is $t^*=1-a^2/4$.
In this case, the SOS relaxation is exact and finds the true global minimum of the polynomial.

The SOS program has a beautiful dual formulation in terms of **moments**. The [dual problem](@entry_id:177454) is to minimize the expected value of $p(x)$ over all pseudo-measures that satisfy certain moment matrix constraints. For the unconstrained problem, this corresponds to finding a sequence of "moments" $y_k$ (representing $\int x^k d\mu$) that minimize $\sum p_i y_i$ subject to the constraint that the **moment matrix** $M_d(y)$ is positive semidefinite [@problem_id:2751032]. For our example, the [dual problem](@entry_id:177454) is to minimize $y_4 + ay_2 + y_0$ subject to $y_0=1$ and the moment matrix $M_2(y) = \begin{pmatrix} y_0  y_1  y_2 \\ y_1  y_2  y_3 \\ y_2  y_3  y_4 \end{pmatrix} \succeq 0$. Strong duality for SDPs ensures that the optimal value of the primal SOS program equals the optimal value of the dual moment program.

### Constrained Problems and the Positivstellensätze

Most problems in control involve constraints, requiring us to certify polynomial nonnegativity not on all of $\mathbb{R}^n$, but on a **semialgebraic set** $K = \{x \in \mathbb{R}^n \mid g_i(x) \ge 0, i=1,\dots,m\}$.

A simple certificate for $p(x) \ge 0$ on $K$ can be constructed using multipliers. For example, if we can find an SOS polynomial $s_1(x)$ such that $p(x) - s_1(x)g_1(x)$ is itself SOS, say $s_0(x)$, then $p(x) = s_0(x) + s_1(x)g_1(x)$. On the set where $g_1(x) \ge 0$, both terms on the right are nonnegative, certifying that $p(x) \ge 0$. This is a generalization of the Lagrangian method.

A foundational result in this area is the **S-lemma**, which applies when $p(x)$ and $g(x)$ are both quadratic polynomials. Under a mild [strict feasibility](@entry_id:636200) (Slater) condition, it states that $p(x) \ge 0$ for all $x$ where $g(x) \ge 0$ if and only if there exists a scalar multiplier $\lambda \ge 0$ such that $p(x) - \lambda g(x)$ is globally nonnegative. Since a nonnegative quadratic is always SOS, this condition is equivalent to $p(x) - \lambda g(x) \in \text{SOS}$. The S-lemma provides a rare case of a *lossless* or *exact* SOS relaxation for a constrained problem [@problem_id:2751044] [@problem_id:2751106]. However, the S-lemma does not generally hold for more than one quadratic constraint or for higher-degree polynomials.

For the general polynomial case, we need more powerful certificates, given by theorems known as **Positivstellensätze** ("theorems of the positive"). These theorems provide algebraic certificates for positivity on semialgebraic sets. A central result is **Putinar's Positivstellensatz**. It uses the concept of a **quadratic module** generated by the constraints $\{g_i\}$:
$$
M(g) = \left\{ \sigma_0(x) + \sum_{i=1}^m \sigma_i(x) g_i(x) \mid \sigma_0, \dots, \sigma_m \in \text{SOS} \right\}
$$
Any polynomial in $M(g)$ is clearly nonnegative on $K$. Putinar's theorem provides a partial converse. It requires the quadratic module $M(g)$ to be **Archimedean**, an algebraic condition implying that the set $K$ is compact (for instance, if $R - \|x\|^2 \in M(g)$ for some $R>0$). The theorem states:

*If the quadratic module $M(g)$ is Archimedean, then any polynomial $p(x)$ that is strictly positive on $K$ (i.e., $p(x) > 0$ for all $x \in K$) belongs to the quadratic module $M(g)$.* [@problem_id:2751065]

This theorem is of immense practical importance. It guarantees that if a polynomial is strictly positive on a compact set, a degree-bounded SOS certificate of the form $p(x) = \sigma_0 + \sum_i \sigma_i g_i$ must exist and can be found by solving a hierarchy of successively larger SDPs. This means the SOS relaxation is **asymptotically complete** for certifying strict positivity on such sets [@problem_id:2751055].

The dual perspective to these SOS certificates for constrained problems leads to the **Lasserre hierarchy** of moment relaxations. To solve the [constrained optimization](@entry_id:145264) problem $\min_{x \in K} p(x)$, we can formulate a sequence of SDPs over truncated moment sequences $y$. In addition to the moment matrix $M_d(y) \succeq 0$, the constraints $g_i(x) \ge 0$ impose further conditions on the moments, captured by the [positive semidefiniteness](@entry_id:147720) of **localizing matrices** $M_{k}(g_i y) \succeq 0$ for each constraint $g_i$ [@problem_id:2751108]. Under the Archimedean condition, the sequence of solutions to these SDP relaxations is guaranteed to converge to the true minimum $p^*$.

**Example: The Lasserre Hierarchy** [@problem_id:2751108]
To minimize $p(x)=x^2-2x$ over $K=[0,1]$, defined by $g_1(x)=x \ge 0$ and $g_2(x)=1-x \ge 0$, we can set up the first-order ($d=1$) Lasserre relaxation. We seek to minimize $y_2 - 2y_1$ subject to moment constraints on $(y_0, y_1, y_2)$:
- Normalization: $y_0 = 1$.
- Moment matrix: $M_1(y) = \begin{pmatrix} y_0  y_1 \\ y_1  y_2 \end{pmatrix} = \begin{pmatrix} 1  y_1 \\ y_1  y_2 \end{pmatrix} \succeq 0$. This implies $y_2 \ge y_1^2$.
- Localizing matrix for $g_1(x)=x$: $M_0(xy) = (y_1) \succeq 0$, so $y_1 \ge 0$.
- Localizing matrix for $g_2(x)=1-x$: $M_0((1-x)y) = (y_0 - y_1) = (1 - y_1) \succeq 0$, so $y_1 \le 1$.
The problem reduces to minimizing $y_1^2 - 2y_1$ over $y_1 \in [0,1]$, which occurs at $y_1=1$, giving an optimal value of $-1$. This is indeed the true minimum of $x^2-2x$ on $[0,1]$.

### A Landscape of Exactness and Conservatism

The Sum-of-Squares methodology provides a unified, computationally tractable framework for a wide range of polynomial problems. The central theme is the trade-off between computational complexity and exactness. We can summarize the landscape as follows:

- **The Core Problem:** Deciding polynomial nonnegativity is NP-hard.
- **The SOS Relaxation:** Replacing nonnegativity with the SOS property yields a tractable SDP. This is generally a conservative relaxation.
- **Sources of Exactness:** The SOS relaxation is guaranteed to be exact (lossless) in certain structured cases:
    - For polynomials in the special classes where nonnegative is equivalent to SOS (univariate, quadratic).
    - For problems with a single quadratic constraint (the S-lemma).
    - For a class of convex [optimization problems](@entry_id:142739) where the objective and constraint functions are **SOS-convex**, a condition ensuring that the Lagrangian has an exact SOS relaxation for its global minimum [@problem_id:2751106].
- **Asymptotic Exactness:** For constrained problems over compact sets satisfying the Archimedean condition, the SOS hierarchy (primal) and Lasserre hierarchy (dual) are asymptotically exact, converging to the true solution as the relaxation order (and thus SDP size) increases.

This landscape allows practitioners to choose the right tool for the job, with a clear understanding of whether the obtained result is an exact solution or a certified bound. For many problems in control, even a conservative bound provided by a low-order SOS relaxation is sufficient to prove the desired system property, making this one of the most powerful and versatile techniques in modern [systems theory](@entry_id:265873).