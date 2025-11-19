## Introduction
Quantum mechanics describes the microscopic world through a sophisticated mathematical framework, and at its heart lie Dirac's [bra-ket notation](@entry_id:154811) and the concept of expectation values. These tools form the essential bridge between abstract quantum states and the concrete, measurable properties of physical systems. However, a superficial familiarity with the "sandwich" formula $\langle\psi|\hat{A}|\psi\rangle$ is insufficient for tackling the complexities of modern physical chemistry. A true graduate-level mastery requires a rigorous understanding of the underlying mathematical machinery—from the properties of Hilbert spaces to the critical distinction between symmetric and [self-adjoint operators](@entry_id:152188)—which governs the validity and application of these calculations. This article provides a comprehensive journey into this formalism. The "Principles and Mechanisms" chapter will systematically construct the bra-ket language and the rules of measurement. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the predictive power of these tools in diverse fields such as [molecular spectroscopy](@entry_id:148164), [quantum statistical mechanics](@entry_id:140244), and quantum computation. Finally, the "Hands-On Practices" section will challenge you to apply this knowledge to solve practical problems, cementing your theoretical understanding.

## Principles and Mechanisms

The abstract framework of quantum mechanics is built upon the mathematical structure of complex Hilbert spaces. Within this framework, Dirac's [bra-ket notation](@entry_id:154811) provides a powerful and elegant language for representing quantum states, [observables](@entry_id:267133), and their interactions. This chapter delves into the fundamental principles and mechanisms governing this notation, from the definition of states and inner products to the rigorous calculation of measurement probabilities and [expectation values](@entry_id:153208). We will systematically build this formalism, starting with its basic syntax and culminating in the advanced mathematical concepts required for its complete justification.

### The Language of Quantum States: Bras, Kets, and Inner Products

At the heart of quantum mechanics lies the representation of a system's physical state. In the Dirac formalism, a quantum state is represented by a [state vector](@entry_id:154607), called a **ket vector** or simply a **ket**, denoted as $|\psi\rangle$. These kets are vectors in a [complex vector space](@entry_id:153448) known as a **Hilbert space**, denoted by $\mathcal{H}$. A Hilbert space is a vector space equipped with an inner product that allows for the definition of length and angle, and it is complete with respect to the norm induced by this inner product.

For every ket $|\psi\rangle$ in the Hilbert space $\mathcal{H}$, there exists a corresponding object in the [dual space](@entry_id:146945) $\mathcal{H}^*$. This [dual space](@entry_id:146945) consists of all [continuous linear functionals](@entry_id:262913) on $\mathcal{H}$. A functional is a map that takes a vector as input and returns a scalar. In Dirac's notation, the functional corresponding to the ket $|\psi\rangle$ is denoted as a **[bra vector](@entry_id:152965)** or simply a **bra**, written as $\langle\psi|$. The action of the bra $\langle\phi|$ on the ket $|\psi\rangle$ yields a complex number, which is precisely the **inner product** of the two vectors, written as $\langle\phi|\psi\rangle$.

This construction provides a seamless notation, but it also enforces a specific set of rules for manipulating these objects. By convention in physics, the inner product must be linear in its second argument (the ket):
$$
\langle\phi|(c_1|\psi_1\rangle + c_2|\psi_2\rangle) = c_1\langle\phi|\psi_1\rangle + c_2\langle\phi|\psi_2\rangle
$$

A defining axiom of any [complex inner product](@entry_id:261242) is **[conjugate symmetry](@entry_id:144131)**:
$$
\langle\phi|\psi\rangle = (\langle\psi|\phi\rangle)^*
$$
where the asterisk denotes [complex conjugation](@entry_id:174690). This property, combined with the linearity in the second argument, dictates how the inner product behaves with respect to the first argument (the bra). Consider the inner product $\langle c\phi|\psi\rangle$. Using [conjugate symmetry](@entry_id:144131), we have $\langle c\phi|\psi\rangle = (\langle\psi|c\phi\rangle)^*$. From linearity in the second slot, we know $\langle\psi|c\phi\rangle = c\langle\psi|\phi\rangle$. Substituting this gives:
$$
\langle c\phi|\psi\rangle = (c\langle\psi|\phi\rangle)^* = c^*(\langle\psi|\phi\rangle)^* = c^*\langle\phi|\psi\rangle
$$
This demonstrates that the inner product is **anti-linear** (or [conjugate linear](@entry_id:268590)) in its first argument [@problem_id:2625866]. An inner product that is linear in one argument and anti-linear in the other is known as a **[sesquilinear form](@entry_id:154766)**.

This anti-linearity directly determines how a bra is constructed from a ket. The correspondence between kets and bras is an anti-linear map. If a ket $|\psi\rangle$ is expanded in an orthonormal basis $\{|e_j\rangle\}$ as $|\psi\rangle = \sum_j c_j |e_j\rangle$, the corresponding bra $\langle\psi|$ must be:
$$
\langle\psi| = \sum_j c_j^* \langle e_j|
$$
The operation of converting a ket into its corresponding bra is known as taking the **Hermitian adjoint**, denoted by the dagger symbol ($\dagger$). Thus, $\langle\psi| = (|\psi\rangle)^\dagger$. This formalism ensures that the norm squared of a vector, $\langle\psi|\psi\rangle$, is always a real, non-negative number:
$$
\langle\psi|\psi\rangle = \left(\sum_j c_j^* \langle e_j|\right) \left(\sum_k c_k |e_k\rangle\right) = \sum_{j,k} c_j^* c_k \langle e_j|e_k\rangle = \sum_{j,k} c_j^* c_k \delta_{jk} = \sum_j |c_j|^2 \ge 0
$$

### Physical States and Observables

While a ket $|\psi\rangle$ is the mathematical object representing a state, not every ket corresponds to a distinct physical state, and not every operator corresponds to a measurable quantity. Specific physical principles must be imposed.

#### Normalization and the Probabilistic Interpretation

A foundational principle of quantum mechanics is that two kets that differ only by a non-zero complex scalar multiple represent the same physical state. That is, $|\psi\rangle$ and $c|\psi\rangle$ (for $c \in \mathbb{C}, c \neq 0$) are physically indistinguishable because all measurable properties, which depend on ratios, are identical [@problem_id:2625879]. The set of all such kets $\{c|\psi\rangle\}$ forms a **ray** in the Hilbert space.

The connection to experiment is made through the **Born rule**, which gives the probability of obtaining a particular measurement outcome. For an observable with discrete outcomes $a_n$ corresponding to eigenstates $|a_n\rangle$, the probability of measuring $a_n$ when the system is in state $|\psi\rangle$ is proportional to $|\langle a_n|\psi\rangle|^2$. To be a valid probability theory, the sum of probabilities over all possible, mutually exclusive outcomes must equal one. If the [eigenstates](@entry_id:149904) $\{|a_n\rangle\}$ form a complete orthonormal basis, the [completeness relation](@entry_id:139077) is $\sum_n |a_n\rangle\langle a_n| = \hat{I}$. The sum of probabilities is then:
$$
\sum_n |\langle a_n|\psi\rangle|^2 = \sum_n \langle\psi|a_n\rangle\langle a_n|\psi\rangle = \langle\psi| \left( \sum_n |a_n\rangle\langle a_n| \right) |\psi\rangle = \langle\psi|\hat{I}|\psi\rangle = \langle\psi|\psi\rangle
$$
To ensure the sum of probabilities is unity, we enforce the **[normalization condition](@entry_id:156486)** $\langle\psi|\psi\rangle = 1$ [@problem_id:2625832]. This is a convention that selects a single representative vector (of unit length) from each ray to represent the physical state. This simplifies the Born rule, allowing us to identify $|\langle a_n|\psi\rangle|^2$ directly as the probability.

For a continuous basis like position, $\{|x\rangle\}$, the same principle applies. The [completeness relation](@entry_id:139077) is $\int |x\rangle\langle x| dx = \hat{I}$, and the total probability is $\int |\langle x|\psi\rangle|^2 dx = \langle\psi|\psi\rangle$. Thus, normalization requires the position-space wavefunction $\psi(x) = \langle x|\psi\rangle$ to satisfy $\int |\psi(x)|^2 dx = 1$ [@problem_id:2625832].

A more general description of a quantum state is given by the **[density operator](@entry_id:138151)**, $\hat{\rho}$. For a pure state $|\psi\rangle$, $\hat{\rho} = |\psi\rangle\langle\psi|$. The [normalization condition](@entry_id:156486) $\langle\psi|\psi\rangle=1$ is then equivalent to the condition that the trace of the [density operator](@entry_id:138151) is unity, $\mathrm{Tr}(\hat{\rho}) = 1$ [@problem_id:2625832, 2625879].

#### Observables as Self-Adjoint Operators

Physical quantities that can be measured, such as energy, momentum, or position, are called **observables**. In quantum mechanics, observables are represented by **self-adjoint operators**. The primary motivation for this postulate is that measurements of physical quantities must yield real numbers. The [expectation value](@entry_id:150961), or average outcome of many measurements of an observable $\hat{A}$ on a system in state $|\psi\rangle$, is given by $\langle\hat{A}\rangle = \langle\psi|\hat{A}|\psi\rangle$. For this to be real for any state $|\psi\rangle$, the operator $\hat{A}$ must be Hermitian (or, more precisely, self-adjoint). A self-adjoint operator satisfies $\hat{A} = \hat{A}^\dagger$, where $\hat{A}^\dagger$ is the Hermitian adjoint of $\hat{A}$, defined by the relation $\langle\phi|\hat{A}|\psi\rangle = \langle\hat{A}^\dagger\phi|\psi\rangle$ for all relevant states.

For graduate-level work, it is crucial to distinguish between a **symmetric** (or Hermitian) operator and a **self-adjoint** one [@problem_id:2625851]. An operator $\hat{A}$ is symmetric if $\langle\phi|\hat{A}\psi\rangle = \langle\hat{A}\phi|\psi\rangle$ for all $|\phi\rangle, |\psi\rangle$ in its domain, $\mathcal{D}(\hat{A})$. This is equivalent to saying $\hat{A} \subseteq \hat{A}^\dagger$, meaning $\hat{A}^\dagger$ agrees with $\hat{A}$ on $\mathcal{D}(\hat{A})$, but the domain of the adjoint, $\mathcal{D}(\hat{A}^\dagger)$, could be larger. An operator is self-adjoint only if it is symmetric *and* their domains are identical: $\mathcal{D}(\hat{A}) = \mathcal{D}(\hat{A}^\dagger)$.

In [finite-dimensional spaces](@entry_id:151571), this distinction vanishes because all operators are defined on the entire space. However, for the infinite-dimensional Hilbert spaces common in physical chemistry (e.g., describing a particle's position), key [observables](@entry_id:267133) like the [position and momentum operators](@entry_id:152590) are **unbounded**, and domain issues become critical. Only [self-adjoint operators](@entry_id:152188) are guaranteed to have a real spectrum and a complete set of eigenvectors (or a generalized equivalent), which is essential for the measurement postulate. Furthermore, **Stone's theorem** on [one-parameter unitary groups](@entry_id:270459) states that an operator $\hat{H}$ is the generator of a continuous unitary time-evolution group $U(t) = \exp(-i\hat{H}t/\hbar)$ if and only if $\hat{H}$ is self-adjoint. A merely symmetric Hamiltonian does not guarantee a unique, physically sensible time evolution for the system [@problem_id:2625851].

### The Mechanics of Measurement and Expectation Values

The connection between the abstract operator $\hat{A}$ and the numerical outcomes of an experiment is formalized by the spectral theorem and the rules for calculating probabilities and expectation values.

#### The Spectral Theorem: The Heart of Measurement

The **[spectral theorem](@entry_id:136620)** is arguably the most important mathematical result for the physical interpretation of quantum mechanics. It provides a way to decompose any self-adjoint operator in terms of its spectrum (its eigenvalues) and corresponding [projection operators](@entry_id:154142).

For any self-adjoint operator $\hat{A}$ on a Hilbert space, there exists a unique **[projection-valued measure](@entry_id:274834) (PVM)**, $\hat{P}$, defined on the Borel sets of the real line, such that the operator can be written as a spectral integral [@problem_id:2625828]:
$$
\hat{A} = \int_{-\infty}^{\infty} a \, d\hat{P}(a)
$$
The PVM assigns a projection operator $\hat{P}(\Delta)$ to each set of possible outcomes $\Delta \subset \mathbb{R}$. These projectors have the properties $\hat{P}(\Delta)^2 = \hat{P}(\Delta)$, $\hat{P}(\Delta)^\dagger = \hat{P}(\Delta)$, and $\hat{P}(\Delta_1)\hat{P}(\Delta_2) = \hat{P}(\Delta_1 \cap \Delta_2)$.

For the familiar case of an operator with a purely [discrete spectrum](@entry_id:150970) $\{a_n\}$, the spectral theorem simplifies to a sum [@problem_id:2625828]:
$$
\hat{A} = \sum_n a_n \hat{P}_n
$$
Here, $\hat{P}_n$ is the operator that projects onto the eigenspace corresponding to the eigenvalue $a_n$. If the eigenvalue is non-degenerate, this projector is simply the outer product of the corresponding normalized eigenvector with itself, $\hat{P}_n = |a_n\rangle\langle a_n|$.

#### Calculating Probabilities and Post-Measurement States

The PVM from the spectral theorem gives us a direct way to calculate measurement probabilities via the Born rule. The probability of a measurement of $\hat{A}$ yielding a result that lies within a set $\Delta$ is:
$$
\mathcal{P}(\Delta) = \langle\psi|\hat{P}(\Delta)|\psi\rangle = \|\hat{P}(\Delta)|\psi\rangle\|^2
$$
If we are interested in a specific (potentially degenerate) eigenvalue $a_n$, the probability of measuring this value is [@problem_id:2625855]:
$$
\mathcal{P}(a_n) = \langle\psi|\hat{P}_n|\psi\rangle
$$

Furthermore, the act of measurement affects the system. According to the **[projection postulate](@entry_id:145685)**, if a measurement of $\hat{A}$ yields the result $a_n$, the state of the system immediately after the measurement "collapses" into the normalized projection of the original state onto the [eigenspace](@entry_id:150590) of $a_n$. The [post-measurement state](@entry_id:148034) $|\psi_{post}\rangle$ is given by [@problem_id:2625855]:
$$
|\psi_{post}\rangle = \frac{\hat{P}_n |\psi\rangle}{\sqrt{\langle\psi|\hat{P}_n|\psi\rangle}} = \frac{\hat{P}_n |\psi\rangle}{\|\hat{P}_n|\psi\rangle\|}
$$
This can be equivalently expressed in the density [operator formalism](@entry_id:180896). If the initial state is $\hat{\rho} = |\psi\rangle\langle\psi|$, the [post-measurement state](@entry_id:148034) is $\hat{\rho}_{post} = \frac{\hat{P}_n \hat{\rho} \hat{P}_n}{\mathrm{Tr}(\hat{\rho}\hat{P}_n)}$ [@problem_id:2625855].

#### Calculating Expectation Values

The [expectation value](@entry_id:150961) $\langle\hat{A}\rangle_\psi = \langle\psi|\hat{A}|\psi\rangle$ can be understood as the average of the eigenvalues weighted by their respective probabilities. Using the [spectral decomposition](@entry_id:148809), we see that it is the first moment of the probability distribution defined by the PVM [@problem_id:2625828]:
$$
\langle\hat{A}\rangle_\psi = \langle\psi| \left( \int a \, d\hat{P}(a) \right) |\psi\rangle = \int a \, d\langle\psi|\hat{P}(a)|\psi\rangle = \int a \, d\mu_\psi(a)
$$

For practical calculations in a finite basis, the [expectation value](@entry_id:150961) is computed by inserting the [completeness relation](@entry_id:139077) $\hat{I} = \sum_j |e_j\rangle\langle e_j|$ twice. Let's consider a concrete example [@problem_id:2625856]. Suppose a vibronic system is described in a 3-level orthonormal basis $\{|e_1\rangle, |e_2\rangle, |e_3\rangle\}$ and we have an observable $\hat{A}$ with [matrix elements](@entry_id:186505) $A_{jk} = \langle e_j|\hat{A}|e_k\rangle$. The operator can be written as $\hat{A} = \sum_{j,k} A_{jk} |e_j\rangle\langle e_k|$. The expectation value for a state $|\psi\rangle = \sum_n c_n |e_n\rangle$ is then:
$$
\langle\hat{A}\rangle_\psi = \left\langle \sum_j c_j \langle e_j| \right| \left( \sum_{k,l} A_{kl} |e_k\rangle\langle e_l| \right) \left| \sum_m c_m |e_m\rangle \right\rangle
$$
$$
= \sum_{j,k,l,m} c_j^* c_m A_{kl} \langle e_j|e_k\rangle \langle e_l|e_m\rangle = \sum_{j,k,l,m} c_j^* c_m A_{kl} \delta_{jk} \delta_{lm} = \sum_{j,m} c_j^* A_{jm} c_m
$$
This is the [standard matrix](@entry_id:151240) formula for an expectation value, $\mathbf{c}^\dagger \mathbf{A} \mathbf{c}$, where $\mathbf{c}$ is the column vector of coefficients and $\mathbf{A}$ is the [matrix representation](@entry_id:143451) of the operator. For instance, if $\hat{A}$ has the matrix representation $\begin{pmatrix} 2  i \\ -i  3 \end{pmatrix}$ in a 2-level basis and the state is $|\psi\rangle = \frac{1}{\sqrt{5}}(|e_1\rangle + 2|e_2\rangle)$, the [expectation value](@entry_id:150961) is:
$$ \langle\hat{A}\rangle = \frac{1}{5} \begin{pmatrix} 1  2 \end{pmatrix} \begin{pmatrix} 2  i \\ -i  3 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \frac{1}{5} \begin{pmatrix} 1  2 \end{pmatrix} \begin{pmatrix} 2+2i \\ -i+6 \end{pmatrix} = \frac{1}{5}(2+2i + 12-2i) = \frac{14}{5} $$
This method provides a direct computational recipe for any finite-dimensional system.

### Superposition and Interference

One of the most profound departures from classical physics is the **[principle of superposition](@entry_id:148082)**. A quantum system can exist in a state that is a [linear combination](@entry_id:155091) of other distinct states. Consider a state $|\chi\rangle = \alpha|\psi\rangle + \beta|\phi\rangle$, where $|\psi\rangle$ and $|\phi\rangle$ might represent a molecule passing through two different paths in an [interferometer](@entry_id:261784) [@problem_id:2625868]. A classical intuition would suggest that the probability of detecting the molecule at some position $x_0$ would be the sum of probabilities for each path: $|\alpha|^2 P(x_0|\psi) + |\beta|^2 P(x_0|\phi)$.

Quantum mechanics predicts something fundamentally different. The probability is found by first adding the probability *amplitudes*, and then taking the squared modulus of the sum:
$$
\mathcal{P}(x_0) = |\langle x_0|\chi\rangle|^2 = |\alpha\langle x_0|\psi\rangle + \beta\langle x_0|\phi\rangle|^2
$$
Let's expand this expression, letting $\psi(x_0) = \langle x_0|\psi\rangle$ and $\phi(x_0) = \langle x_0|\phi\rangle$:
$$
\mathcal{P}(x_0) = (\alpha^*\psi^*(x_0) + \beta^*\phi^*(x_0))(\alpha\psi(x_0) + \beta\phi(x_0))
$$
$$
= |\alpha|^2|\psi(x_0)|^2 + |\beta|^2|\phi(x_0)|^2 + \alpha^*\beta\psi^*(x_0)\phi(x_0) + \beta^*\alpha\phi^*(x_0)\psi(x_0)
$$
The first two terms are the classical-like sum of probabilities. The last two terms represent the quantum **interference term**:
$$
\text{Interference} = 2\mathrm{Re}(\alpha^*\beta\psi^*(x_0)\phi(x_0))
$$
This term depends on the **[relative phase](@entry_id:148120)** between the complex coefficients $\alpha$ and $\beta$. By varying this phase (e.g., by changing the length of one path in the interferometer), the interference can be made constructive (increasing the probability) or destructive (decreasing it). The detection probability can be continuously tuned between a minimum of $(|\alpha||\psi(x_0)| - |\beta||\phi(x_0)|)^2$ and a maximum of $(|\alpha||\psi(x_0)| + |\beta||\phi(x_0)|)^2$ [@problem_id:2625868]. This phenomenon has no classical analogue and is a direct consequence of the superposition principle. It is important to note that the orthogonality of the path states, $\langle\psi|\phi\rangle = 0$, which means $\int\psi^*(x)\phi(x)dx=0$, does *not* imply that their wavefunctions cannot overlap at a specific point $x_0$ [@problem_id:2625868]. Interference occurs precisely in regions where both wavefunctions are non-zero.

### Continuous Spectra and the Rigorous Framework

Many important [observables](@entry_id:267133) in physical chemistry, such as position and momentum, have continuous spectra. This introduces mathematical subtleties that require a more rigorous framework than a simple Hilbert space.

#### The Position Basis

The eigenkets of the [position operator](@entry_id:151496) $\hat{x}$, denoted $|x\rangle$, are not elements of the Hilbert space $L^2(\mathbb{R})$ because they are not square-integrable; their "norm" is infinite. They are **generalized eigenkets**. Nonetheless, they form a complete "basis" in a distributional sense. Their properties are defined by two key relations [@problem_id:2625842]:
1.  **Generalized Orthonormality**: $\langle x|x'\rangle = \delta(x-x')$, where $\delta(x-x')$ is the Dirac delta distribution.
2.  **Completeness Relation**: $\int_{-\infty}^\infty |x\rangle\langle x| dx = \hat{I}$.

These two relations form the bridge between the abstract Dirac notation and the familiar coordinate-space wave mechanics. By inserting the [completeness relation](@entry_id:139077), any inner product or matrix element can be expressed as an integral. For instance, the inner product $\langle\phi|\psi\rangle$ becomes:
$$
\langle\phi|\psi\rangle = \langle\phi|\hat{I}|\psi\rangle = \langle\phi| \left( \int|x\rangle\langle x|dx \right) |\psi\rangle = \int \langle\phi|x\rangle\langle x|\psi\rangle dx = \int \phi^*(x)\psi(x) dx
$$
Similarly, the [expectation value](@entry_id:150961) of an operator $\hat{A}$ becomes:
$$
\langle\psi|\hat{A}|\psi\rangle = \iint \langle\psi|x\rangle\langle x|\hat{A}|x'\rangle\langle x'|\psi\rangle dx dx' = \iint \psi^*(x) A(x,x') \psi(x') dx dx'
$$
where $A(x,x') = \langle x|\hat{A}|x'\rangle$ is the integral kernel of the operator $\hat{A}$ [@problem_id:2625842].

#### The Rigged Hilbert Space (RHS): A Gelfand Triple

To give rigorous meaning to objects like $|x\rangle$ and the Dirac delta function, mathematicians have developed the framework of the **Rigged Hilbert Space (RHS)**, also known as a **Gelfand triple**. This structure consists of three nested spaces [@problem_id:2625843]:
$$
\Phi \subset \mathcal{H} \subset \Phi^\times
$$

Here, $\mathcal{H}$ is the standard Hilbert space (e.g., $L^2(\mathbb{R})$). $\Phi$ is a [dense subspace](@entry_id:261392) of $\mathcal{H}$ containing exceptionally "well-behaved" functions, known as a space of test functions. For problems involving position and momentum on $\mathbb{R}$, the canonical choice for $\Phi$ is the **Schwartz space**, $\mathcal{S}(\mathbb{R})$, which consists of all infinitely differentiable functions that decay, along with all their derivatives, faster than any polynomial power. This space has the crucial property that it is mapped into itself by the [position operator](@entry_id:151496), the [momentum operator](@entry_id:151743), and the Fourier transform [@problem_id:2625843].

The third space, $\Phi^\times$, is the continuous anti-dual of $\Phi$. It is the space of all continuous anti-linear functionals on $\Phi$. In this framework, the generalized kets like $|x\rangle$ and $|p\rangle$ are not in $\mathcal{H}$, but are rigorously defined as elements of $\Phi^\times$. The familiar expression $\langle x|\psi\rangle = \psi(x)$ is now interpreted as the action of the functional $|x\rangle \in \Phi^\times$ on the test function $|\psi\rangle \in \Phi$, which results in the evaluation of the function at the point $x$ [@problem_id:2625843].

This rigorous structure justifies the formal manipulations of Dirac notation. It provides a proper domain ($\Phi$) on which [unbounded operators](@entry_id:144655) are well-behaved and operations like [integration by parts](@entry_id:136350) are valid, which is essential for proving self-adjointness and calculating [expectation values](@entry_id:153208) [@problem_id:2625843]. The RHS thus provides the solid mathematical foundation upon which the practical and intuitive power of [bra-ket notation](@entry_id:154811) rests.