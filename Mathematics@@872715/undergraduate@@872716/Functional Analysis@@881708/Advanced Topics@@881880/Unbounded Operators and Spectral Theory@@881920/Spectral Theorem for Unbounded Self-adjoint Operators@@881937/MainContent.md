## Introduction
The Spectral Theorem is one of the crown jewels of functional analysis, providing a complete structural blueprint for a crucial class of operators. While its form for [bounded operators](@entry_id:264879) on Hilbert spaces is a direct generalization of diagonalizing a Hermitian matrix, its extension to **[unbounded operators](@entry_id:144655)** unlocks a far richer and more complex world. These operators are not mathematical abstractions; they are the essential tools for describing [physical observables](@entry_id:154692) like energy and momentum in quantum mechanics and for analyzing partial differential equations. The central challenge, and the focus of this article, is that the properties of an [unbounded operator](@entry_id:146570) are delicately tied to its domain, leading to a critical distinction between symmetric and self-adjoint operators that has profound physical consequences.

This article navigates the theory and application of the Spectral Theorem for [unbounded self-adjoint operators](@entry_id:189288), designed to build a robust understanding from the ground up. Across three chapters, you will gain a clear perspective on this foundational topic. We will begin by exploring the core principles and mechanisms, dissecting the difference between symmetric and [self-adjoint operators](@entry_id:152188) and examining the two powerful formulations of the [spectral theorem](@entry_id:136620). From there, we will bridge theory and practice by investigating its extensive applications in quantum mechanics and [mathematical physics](@entry_id:265403), seeing how it explains phenomena like [energy quantization](@entry_id:145335) and particle dynamics. Finally, you will have the opportunity to solidify your knowledge through a series of hands-on practices that connect the abstract concepts to concrete calculations.

Our journey begins in the first chapter, "Principles and Mechanisms," where we lay the essential groundwork. We will start by defining the adjoint of an [unbounded operator](@entry_id:146570) and see precisely how the choice of domain distinguishes a merely [symmetric operator](@entry_id:275833) from a truly self-adjoint one—the necessary condition for an operator to represent a physical observable.

## Principles and Mechanisms

In the study of [bounded operators](@entry_id:264879) on a Hilbert space, the concepts of symmetric and [self-adjoint operators](@entry_id:152188) coincide. However, for [unbounded operators](@entry_id:144655), which are essential for describing physical [observables in quantum mechanics](@entry_id:152184) and for the analysis of differential equations, a critical distinction emerges. This distinction lies at the heart of the spectral theory for [unbounded operators](@entry_id:144655) and is determined entirely by the operator's domain.

### From Symmetric to Self-Adjoint: The Crucial Role of the Domain

An unbounded linear operator $T$ is not defined on the entire Hilbert space $\mathcal{H}$, but on a [dense subspace](@entry_id:261392) $D(T) \subset \mathcal{H}$ known as its **domain**. The properties of $T$ are inextricably linked to the choice of $D(T)$. To explore these properties, we must first introduce the concept of the adjoint operator.

The **adjoint** of an operator $T$, denoted $T^*$, is defined both by its action and its domain, $D(T^*)$. A vector $g \in \mathcal{H}$ belongs to $D(T^*)$ if there exists a vector $h \in \mathcal{H}$ such that the relation $\langle Tf, g \rangle = \langle f, h \rangle$ holds for all $f \in D(T)$. If such an $h$ exists, it is unique (since $D(T)$ is dense), and we define the action of the adjoint as $T^*g = h$.

With this definition, we can distinguish two important classes of operators:

1.  An operator $T$ is **symmetric** if $\langle Tf, g \rangle = \langle f, Tg \rangle$ for all $f, g \in D(T)$. This is equivalent to the condition that $T$ is a restriction of its adjoint, written as $T \subseteq T^*$. This means $D(T) \subseteq D(T^*)$ and $Tf = T^*f$ for all $f \in D(T)$.

2.  An operator $T$ is **self-adjoint** if $T = T^*$. This is a much stronger condition, as it requires not only that the actions of $T$ and $T^*$ agree, but also that their domains are identical: $D(T) = D(T^*)$.

All [self-adjoint operators](@entry_id:152188) are symmetric, but the converse is not true. The difference between a [symmetric operator](@entry_id:275833) and a self-adjoint one is a matter of domain. A [symmetric operator](@entry_id:275833) might have "too small" a domain, such that $D(T)$ is a [proper subset](@entry_id:152276) of $D(T^*)$.

To make this concrete, let's consider the momentum operator, whose formal expression is $i\frac{d}{dx}$, on the Hilbert space $H = L^2([0,1])$. The properties of this operator depend entirely on the boundary conditions imposed on its domain. Let's assume the domain consists of continuously differentiable functions, $f \in C^1([0,1])$. For any two such functions $f, g$, [integration by parts](@entry_id:136350) yields a fundamental boundary term:
$$ \langle i f', g \rangle - \langle f, i g' \rangle = i \int_0^1 f'(x) \overline{g(x)} \,dx + i \int_0^1 f(x) \overline{g'(x)} \,dx = i [f(x)\overline{g(x)}]_0^1 $$
An operator $Tf = if'$ is symmetric if and only if this boundary term vanishes for all $f, g$ in its domain $D(T)$.

Consider the domain $D(T_A) = \{f \in C^1([0,1]) \mid f(0) = 0 \text{ and } f(1) = 0\}$. For any $f, g \in D(T_A)$, the boundary term $i(f(1)\overline{g(1)} - f(0)\overline{g(0)})$ is clearly zero, so the operator $T_A$ is symmetric. To determine if it is self-adjoint, we must find the domain of its adjoint, $D(T_A^*)$. A function $g$ is in $D(T_A^*)$ if $\langle T_A f, g \rangle = \langle f, h \rangle$ for some $h$. The calculation above shows that for any sufficiently smooth $g$, $\langle T_A f, g \rangle = \langle f, i g' \rangle + i(f(1)\overline{g(1)} - f(0)\overline{g(0)})$. Since $f(0)=f(1)=0$ for all $f \in D(T_A)$, the boundary term vanishes regardless of the values of $g(0)$ and $g(1)$. This means any function $g \in C^1([0,1])$ (with no boundary conditions) is in the domain of the adjoint, with $T_A^*g = ig'$. Thus, $D(T_A) \subsetneq D(T_A^*)$, and the operator $T_A$ is symmetric but **not** self-adjoint [@problem_id:1881968].

This example reveals a general principle. If we start with a [symmetric operator](@entry_id:275833) on a very restrictive domain, such as the space of infinitely differentiable functions with [compact support](@entry_id:276214) $C_c^\infty((0,1))$, its adjoint will be defined on a much larger domain. For $T = i\frac{d}{dx}$ on $D(T) = C_c^\infty((0,1))$, any function $f \in D(T)$ vanishes at the boundaries. The adjoint's domain $D(T^*)$ turns out to be the Sobolev space $H^1(0,1)$, which consists of functions in $L^2((0,1))$ whose [weak derivative](@entry_id:138481) is also in $L^2((0,1))$, with no boundary restrictions imposed [@problem_id:1881961].

A [symmetric operator](@entry_id:275833) that is not self-adjoint is a candidate for having **[self-adjoint extensions](@entry_id:264525)**. These are [self-adjoint operators](@entry_id:152188) $S$ such that $T \subset S$. Finding a [self-adjoint extension](@entry_id:151493) involves carefully enlarging the domain $D(T)$ to a new domain $D(S)$ such that $D(S) = D(S^*)$. This is typically achieved by imposing specific boundary conditions. For the operator expression $-\frac{d^2}{dx^2}$ on $L^2([0,1])$, there is a whole family of possible [self-adjoint extensions](@entry_id:264525), each corresponding to a different set of boundary conditions (e.g., Dirichlet, Neumann, periodic, Robin). Each of these extensions represents a distinct, well-posed physical system [@problem_id:1881943]. Self-adjointness is the mathematically precise condition for an operator to represent a physical observable.

### The Spectrum of a Self-Adjoint Operator

The **[resolvent set](@entry_id:261708)** of an operator $A$, denoted $\rho(A)$, is the set of complex numbers $\lambda$ for which the operator $(A - \lambda I)$ has a bounded inverse defined on the entire Hilbert space. The **spectrum** of $A$, denoted $\sigma(A)$, is the complement of the [resolvent set](@entry_id:261708) in the complex plane, $\sigma(A) = \mathbb{C} \setminus \rho(A)$.

A cornerstone of [spectral theory](@entry_id:275351) is that the spectrum of a self-adjoint operator is purely real.

**Theorem:** If $A$ is a self-adjoint operator on a Hilbert space $\mathcal{H}$, then its spectrum $\sigma(A)$ is a subset of the real line $\mathbb{R}$.

This can be demonstrated by showing that any non-real complex number $\lambda = \alpha + i\beta$ (with $\beta \neq 0$) must belong to the [resolvent set](@entry_id:261708). For any $f \in D(A)$, we can compute the squared norm of $(A-\lambda I)f$:
$$ \|(A-\lambda I)f\|^2 = \langle (A - \alpha I - i\beta I)f, (A - \alpha I - i\beta I)f \rangle $$
Since $A$ is self-adjoint, $(A-\alpha I)$ is also self-adjoint, and $\langle (A-\alpha I)f, f \rangle$ is real. Expanding the inner product gives:
$$ \|(A-\lambda I)f\|^2 = \|(A-\alpha I)f\|^2 + |\beta|^2 \|f\|^2 $$
This inequality implies that $\|(A-\lambda I)f\| \ge |\beta|\|f\|$. This shows that $(A-\lambda I)$ is an [injective map](@entry_id:262763) with a closed range. A deeper result shows its range is all of $\mathcal{H}$, and its inverse $(A-\lambda I)^{-1}$ is a [bounded operator](@entry_id:140184) with norm satisfying $\|(A-\lambda I)^{-1}\| \le \frac{1}{|\beta|}$. In fact, for a self-adjoint operator $A$, the precise norm of the resolvent for non-real $\lambda$ is given by the distance from $\lambda$ to the spectrum $\sigma(A)$. If $\sigma(A) = \mathbb{R}$, this becomes:
$$ \|(A - (\alpha+i\beta)I)^{-1}\| = \sup_{t \in \mathbb{R}} \frac{1}{|t - (\alpha+i\beta)|} = \frac{1}{|\beta|} = \frac{1}{|\text{Im}(\lambda)|} \quad [@problem_id:1881960] $$
This result elegantly quantifies how the [resolvent operator](@entry_id:271964)'s [boundedness](@entry_id:746948) deteriorates as $\lambda$ approaches the real axis.

The spectrum of a [self-adjoint operator](@entry_id:149601) is partitioned into two main types:
*   The **[point spectrum](@entry_id:274057)**, $\sigma_p(A)$, consists of all **eigenvalues** of $A$. An eigenvalue is a number $\lambda$ for which there exists a non-[zero vector](@entry_id:156189) $f$ (an eigenvector) such that $Af = \lambda f$. The reality of the spectrum implies that all eigenvalues of a self-adjoint operator must be real. This property is foundational in quantum mechanics, ensuring that the measured values of [physical observables](@entry_id:154692) are real numbers [@problem_id:1881919].
*   The **continuous spectrum**, $\sigma_c(A)$, consists of $\lambda \in \sigma(A)$ that are not eigenvalues and for which the range of $(A-\lambda I)$ is dense in $\mathcal{H}$.

For [self-adjoint operators](@entry_id:152188), the third part of the spectrum, the [residual spectrum](@entry_id:269789), is always empty.

A canonical example illustrating a purely continuous spectrum is the **position operator** $Q$ on $L^2(\mathbb{R})$, defined by $(Qf)(x) = xf(x)$. Let's find its eigenvalues. The equation $Qf = \lambda f$ becomes $xf(x) = \lambda f(x)$, or $(x-\lambda)f(x)=0$. For this to hold for all $x$, $f(x)$ must be zero for every $x \neq \lambda$. A function that is non-zero at only a single point has an $L^2$ norm of zero, meaning it is the zero vector in the Hilbert space. Since eigenvectors must be non-zero, the position operator $Q$ has no eigenvalues, i.e., $\sigma_p(Q) = \emptyset$.
However, for any real $\lambda$, the operator $(Q-\lambda I)^{-1}$, which corresponds to multiplication by the function $\frac{1}{x-\lambda}$, is unbounded. Therefore, no real number is in the [resolvent set](@entry_id:261708). Combining these facts, the spectrum of the position operator is the entire real line, and it is purely continuous: $\sigma(Q) = \sigma_c(Q) = \mathbb{R}$ [@problem_id:1881921].

### The Spectral Theorem: A Generalization of Diagonalization

The [spectral theorem](@entry_id:136620) is one of the most significant results in [functional analysis](@entry_id:146220). It provides a way to "diagonalize" any [self-adjoint operator](@entry_id:149601), extending the familiar concept of diagonalizing a Hermitian matrix to the infinite-dimensional setting. The theorem has several equivalent formulations, two of which are particularly useful.

#### The Multiplication Operator Form

This version of the theorem states that every [self-adjoint operator](@entry_id:149601) is unitarily equivalent to a simple multiplication operator.

**Theorem (Multiplication Operator Form):** For any [self-adjoint operator](@entry_id:149601) $A$ on a separable Hilbert space $\mathcal{H}$, there exists a [measure space](@entry_id:187562) $(M, \mu)$, a real-valued [measurable function](@entry_id:141135) $g$ on $M$, and a [unitary operator](@entry_id:155165) $U: \mathcal{H} \to L^2(M, \mu)$ such that:
$$ A = U^{-1} M_g U \quad \text{or} \quad U A U^{-1} = M_g $$
where $M_g$ is the multiplication operator on $L^2(M, \mu)$ defined by $(M_g \psi)(p) = g(p)\psi(p)$.

The unitary map $U$ acts as a change of representation, transforming the problem into a space where the operator $A$ becomes a simple multiplication. The range of the function $g$ is the spectrum of $A$.

A quintessential example is the **[momentum operator](@entry_id:151743)** $P = -i\hbar \frac{d}{dx}$ on $L^2(\mathbb{R})$. The unitary operator that diagonalizes $P$ is the **Fourier transform**, $\mathcal{F}$. The action of $P$ in the [position representation](@entry_id:154751) is transformed into a simple multiplication in the momentum (or Fourier) representation:
$$ (\mathcal{F}P\mathcal{F}^{-1})\hat{\psi}(k) = \hbar k \cdot \hat{\psi}(k) $$
Here, the operator $P$ in position space is equivalent to the operator of multiplication by the function $g(k) = \hbar k$ in momentum space. This transformation simplifies many problems in quantum mechanics, turning differential equations in [position space](@entry_id:148397) into algebraic equations in momentum space [@problem_id:1881923]. The spectrum of $P$ is the range of $g(k)$, which is all of $\mathbb{R}$.

#### The Projection-Valued Measure (PVM) Form

This formulation expresses a [self-adjoint operator](@entry_id:149601) as an integral over its spectrum with respect to a special kind of measure whose values are [projection operators](@entry_id:154142). A **[projection-valued measure](@entry_id:274834)** (PVM) $E$ on $\mathbb{R}$ assigns to each Borel set $\Omega \subseteq \mathbb{R}$ an [orthogonal projection](@entry_id:144168) operator $E(\Omega)$ on $\mathcal{H}$.

**Theorem (PVM Form):** To every self-adjoint operator $A$ on $\mathcal{H}$, there corresponds a unique PVM $E$ on the Borel sets of $\mathbb{R}$ such that:
$$ A = \int_{\sigma(A)} \lambda \, dE(\lambda) $$
The physical interpretation of this form is powerful. The [projection operator](@entry_id:143175) $P_\Omega = E(\Omega)$ projects a state vector $\psi$ onto the subspace of states for which a measurement of the observable $A$ is guaranteed to yield a value in the set $\Omega$. The probability of this outcome is given by $\|P_\Omega \psi\|^2$.

The [position operator](@entry_id:151496) $Q$ provides the most intuitive example. Its associated PVM is simply multiplication by the indicator function $\mathbf{1}_\Omega(x)$ of the set $\Omega$:
$$ (E(\Omega)\psi)(x) = \mathbf{1}_\Omega(x) \psi(x) $$
If a particle is in a state $\psi(x)$, the state after filtering for positions in the interval $[-a, a]$ is $\psi_a(x) = (E([-a,a])\psi)(x) = \mathbf{1}_{[-a,a]}(x)\psi(x)$. The squared norm of this projected state, $\|\psi_a\|^2 = \int_{-a}^a |\psi(x)|^2 dx$, gives the probability that a measurement of the particle's position will find it within this interval [@problem_id:1881944].

### The Functional Calculus: Defining Functions of Operators

The true power of the [spectral theorem](@entry_id:136620) is realized through the **[functional calculus](@entry_id:138358)**, which allows us to define functions of a [self-adjoint operator](@entry_id:149601). If $A = U^{-1} M_g U$ is the [spectral representation](@entry_id:153219) of $A$, and $\phi: \mathbb{R} \to \mathbb{C}$ is a Borel function, we can define the operator $\phi(A)$ as:
$$ \phi(A) := U^{-1} M_{\phi \circ g} U = U^{-1} M_{\phi(g)} U $$
Equivalently, using the PVM, $\phi(A) = \int_{\sigma(A)} \phi(\lambda) \, dE(\lambda)$. This definition not only gives the action of the new operator $\phi(A)$ but also precisely specifies its domain:
$$ D(\phi(A)) = \left\{ f \in \mathcal{H} \mid \int_{\sigma(A)} |\phi(\lambda)|^2 d\|E(\lambda)f\|^2  \infty \right\} $$

This machinery allows us to define operators like $\exp(itA)$ (the [time evolution operator](@entry_id:139668) in quantum mechanics) or $\sqrt{A}$ for a [positive operator](@entry_id:263696) $A$. Let's consider the positive self-adjoint operator $A = -\frac{d^2}{dx^2}$ on $L^2(\mathbb{R})$, which represents kinetic energy. Its [spectral representation](@entry_id:153219) via the Fourier transform is $A = \mathcal{F}^{-1} M_{k^2} \mathcal{F}$. To find its unique positive square root, $B = \sqrt{A}$, we apply the function $\phi(t) = \sqrt{t}$ to its [spectral representation](@entry_id:153219):
$$ B = \sqrt{A} = \mathcal{F}^{-1} M_{\sqrt{k^2}} \mathcal{F} = \mathcal{F}^{-1} M_{|k|} \mathcal{F} $$
The action of $B$ is given by $(Bf)(x) = \mathcal{F}^{-1}(|k|\hat{f}(k))(x)$. The [functional calculus](@entry_id:138358) also determines its domain: $D(B)$ consists of functions $f$ for which the Fourier transform $\hat{f}$ satisfies $\int |k|^2|\hat{f}(k)|^2 dk  \infty$. By Plancherel's theorem, this is precisely the condition that the first derivative of $f$ is square-integrable, corresponding to the Sobolev space $H^1(\mathbb{R})$ [@problem_id:1881935].

This framework applies equally well to operators with [discrete spectra](@entry_id:153575). For an operator on $\ell^2(\mathbb{Z})$ defined by $(Tx)_k = (|k|+1)x_k$, the [spectral representation](@entry_id:153219) is already given. It is a multiplication operator with the multiplication function $f(k) = |k|+1$. The [functional calculus](@entry_id:138358) can then be used to analyze expressions involving this operator and its spectrum [@problem_id:1881964]. In all cases, the [spectral theorem](@entry_id:136620) provides a unified and powerful blueprint for understanding the structure and function of [self-adjoint operators](@entry_id:152188).