## Introduction
Quantum entanglement stands as one of the most defining and non-classical features of quantum mechanics, describing profound correlations between systems that defy everyday intuition. While understanding entanglement conceptually is a first step, a rigorous, quantitative framework is essential to harness its power and explore its implications. The central problem is how to move from a qualitative idea of "[connectedness](@entry_id:142066)" to a concrete, measurable quantity. Entanglement entropy rises to this challenge, providing a powerful information-theoretic tool to measure the degree of entanglement in a quantum system. This article provides a comprehensive exploration of entanglement entropy for undergraduate students. The journey begins in the "Principles and Mechanisms" chapter, where we will derive entanglement entropy from the ground up, starting with the [partial trace](@entry_id:146482) and the concept of mixedness, and introduce the powerful Schmidt decomposition as a calculational shortcut. Next, the "Applications and Interdisciplinary Connections" chapter will showcase the remarkable utility of entanglement entropy, demonstrating how it serves as a unifying language across fields as diverse as quantum computing, condensed matter physics, and fundamental theories of spacetime. Finally, the "Hands-On Practices" section offers a chance to apply these concepts through targeted problems, solidifying your understanding and building practical skills.

## Principles and Mechanisms

In the study of [composite quantum systems](@entry_id:193313), one of the most profound and counter-intuitive concepts is entanglement. While the previous chapter introduced its conceptual foundations, this chapter delves into the quantitative framework used to measure it. The central tool for this task, particularly in [bipartite pure states](@entry_id:138323), is the **entanglement entropy**. It serves as a rigorous measure of the quantum correlations shared between subsystems, providing a bridge between the abstract structure of Hilbert space and tangible, measurable information-theoretic quantities.

### The Origin of Entanglement Entropy: Partial Trace and Mixedness

Consider a composite quantum system $S$ partitioned into two subsystems, $A$ and $B$. The total Hilbert space is the [tensor product](@entry_id:140694) $\mathcal{H}_S = \mathcal{H}_A \otimes \mathcal{H}_B$. Let us assume the total system is prepared in a known [pure state](@entry_id:138657) $|\psi\rangle_{AB} \in \mathcal{H}_S$. A natural and fundamental question arises: what is the state of subsystem $A$ alone?

If an observer has access only to subsystem $A$, they cannot, in general, describe their subsystem with a state vector. The complete information is encoded in the global state $|\psi\rangle_{AB}$, and correlations with subsystem $B$ fundamentally affect what can be known about $A$. The correct mathematical description of subsystem $A$ is given by its **[reduced density matrix](@entry_id:146315)**, $\rho_A$. This operator is obtained by "averaging" or "tracing out" the degrees of freedom of subsystem $B$. This operation is known as the **[partial trace](@entry_id:146482)**, defined as:

$$
\rho_A = \mathrm{Tr}_B(|\psi\rangle_{AB}\langle\psi|_{AB})
$$

The operator $\rho_A$ encapsulates all possible information that can be extracted from subsystem $A$ through local measurements. A remarkable feature of quantum mechanics is that even if the total state $|\psi\rangle_{AB}$ is pure, the reduced state $\rho_A$ can be **mixed**. A [mixed state](@entry_id:147011) represents a [statistical ensemble](@entry_id:145292) of quantum states and is characterized by having more than one non-zero eigenvalue. The degree of mixedness of a quantum state $\rho$ is quantified by the **von Neumann entropy**, defined as:

$$
S(\rho) = -\mathrm{Tr}(\rho \ln \rho)
$$

If the eigenvalues of $\rho$ are given by $\{\lambda_i\}$, the von Neumann entropy can be calculated as $S(\rho) = -\sum_i \lambda_i \ln \lambda_i$, with the convention that $0 \ln 0 = 0$. The von Neumann entropy is zero if and only if the state is pure (one eigenvalue is 1, all others are 0) and is maximal for a maximally mixed state (all eigenvalues are equal).

When we apply this concept to a [reduced density matrix](@entry_id:146315) derived from a pure bipartite state, the resulting entropy is termed the **entanglement entropy** of the subsystem:

$$
S_A \equiv S(\rho_A)
$$

The entanglement entropy $S_A$ is therefore a measure of the mixedness of subsystem $A$. Since the total system $AB$ is in a [pure state](@entry_id:138657), this mixedness does not arise from classical uncertainty about the preparation of the state. Instead, it arises exclusively from the quantum correlations—the entanglement—between subsystem $A$ and subsystem $B$. A non-zero entanglement entropy signifies that information about the system is stored non-locally in the correlations between its parts.

### The Spectrum of Entanglement: From Separable to Maximally Entangled States

The value of the entanglement entropy provides a continuous scale to quantify entanglement, ranging from zero for unentangled states to a maximum value for maximally [entangled states](@entry_id:152310).

A bipartite state $|\psi\rangle_{AB}$ is called **separable** or a **product state** if it can be written as the [tensor product](@entry_id:140694) of individual states in each subsystem: $|\psi\rangle_{AB} = |\phi\rangle_A \otimes |\chi\rangle_B$. In this case, the subsystems are independent and not entangled. Let's calculate the [reduced density matrix](@entry_id:146315) for subsystem $A$:

$$
\rho_A = \mathrm{Tr}_B \left( (|\phi\rangle_A \langle\phi|_A) \otimes (|\chi\rangle_B \langle\chi|_B) \right) = |\phi\rangle_A \langle\phi|_A \cdot \mathrm{Tr}(|\chi\rangle_B \langle\chi|_B)
$$

Since $|\chi\rangle_B$ is a normalized state vector, $\mathrm{Tr}(|\chi\rangle_B \langle\chi|_B) = \langle\chi|\chi\rangle_B = 1$. Thus, $\rho_A = |\phi\rangle_A \langle\phi|_A$. This is the [density matrix](@entry_id:139892) of a [pure state](@entry_id:138657). A [pure state](@entry_id:138657) operator is a projector, and its eigenvalues are $\{1, 0, \dots, 0\}$. The entanglement entropy is therefore:

$$
S_A = -(1 \cdot \ln(1) + 0 \cdot \ln(0) + \dots) = 0
$$

This is a cornerstone result: a pure bipartite state has zero entanglement entropy if and only if it is a [separable state](@entry_id:142989). This provides a definitive criterion for the absence of entanglement. For example, a state like $|\psi\rangle = |+\rangle_A |-\rangle_B$ is a product state, and its entanglement entropy is exactly zero, confirming the lack of entanglement [@problem_id:2091848]. For a general two-qubit state written as $|\psi\rangle = \sum_{i,j \in \{0,1\}} c_{ij}|i\rangle_A |j\rangle_B$, the condition for separability, and thus for zero entanglement entropy, can be expressed as a simple algebraic relation between its coefficients: $c_{00} c_{11} - c_{01} c_{10} = 0$ [@problem_id:2091801].

At the other end of the spectrum are **maximally [entangled states](@entry_id:152310)**. A canonical example for two qubits ($d=2$) is the Bell state $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$. Let's compute $\rho_A$:

$$
\rho_{AB} = |\Phi^+\rangle\langle\Phi^+| = \frac{1}{2}(|00\rangle\langle 00| + |00\rangle\langle 11| + |11\rangle\langle 00| + |11\rangle\langle 11|)
$$

$$
\rho_A = \mathrm{Tr}_B(\rho_{AB}) = \frac{1}{2}(|0\rangle\langle 0| \cdot \langle 0|0\rangle_B + |1\rangle\langle 1| \cdot \langle 1|1\rangle_B) = \frac{1}{2}(|0\rangle\langle 0| + |1\rangle\langle 1|) = \frac{1}{2}I_A
$$

The reduced state of subsystem $A$ is the **maximally mixed state**. Its eigenvalues are $\{\frac{1}{2}, \frac{1}{2}\}$. The entropy is:

$$
S_A = -\left(\frac{1}{2}\ln\frac{1}{2} + \frac{1}{2}\ln\frac{1}{2}\right) = -\ln\frac{1}{2} = \ln 2
$$

This is the maximum possible entropy for a two-level system (a qubit). In general, for a bipartite system in $\mathcal{H}_A \otimes \mathcal{H}_B$ where $\dim(\mathcal{H}_A) = d$, the maximum entanglement entropy is $\ln d$. States that achieve this maximum are called maximally entangled states.

### The Schmidt Decomposition and Its Consequences

Calculating the [reduced density matrix](@entry_id:146315) and its eigenvalues can be a tedious process. Fortunately, a powerful mathematical tool known as the **Schmidt decomposition theorem** provides profound insight and simplifies calculations immensely. The theorem states that for any [pure state](@entry_id:138657) $|\psi\rangle_{AB}$ of a bipartite system, there exist [orthonormal bases](@entry_id:753010) $\{|u_i\rangle_A\}$ for subsystem $A$ and $\{|v_i\rangle_B\}$ for subsystem $B$ such that $|\psi\rangle_{AB}$ can be written as:

$$
|\psi\rangle_{AB} = \sum_{i=1}^k \sqrt{p_i} |u_i\rangle_A \otimes |v_i\rangle_B
$$

Here, the coefficients $\sqrt{p_i}$ are real, non-negative numbers called **Schmidt coefficients**, satisfying the [normalization condition](@entry_id:156486) $\sum_i p_i = 1$. The number of non-zero terms, $k$, is called the **Schmidt rank** of the state.

The true power of this decomposition becomes apparent when we calculate the [reduced density matrices](@entry_id:190237). The state written in this form makes the [partial trace](@entry_id:146482) trivial:

$$
\rho_A = \mathrm{Tr}_B\left( \sum_{i,j} \sqrt{p_i p_j} |u_i\rangle_A\langle u_j|_A \otimes |v_i\rangle_B\langle v_j|_B \right) = \sum_{i,j} \sqrt{p_i p_j} |u_i\rangle_A\langle u_j|_A \cdot \delta_{ij} = \sum_i p_i |u_i\rangle_A\langle u_i|_A
$$

$$
\rho_B = \mathrm{Tr}_A\left( \sum_{i,j} \sqrt{p_i p_j} |u_i\rangle_A\langle u_j|_A \otimes |v_i\rangle_B\langle v_j|_B \right) = \sum_{i,j} \sqrt{p_i p_j} \delta_{ij} \cdot |v_i\rangle_B\langle v_j|_B = \sum_i p_i |v_i\rangle_B\langle v_i|_B
$$

These expressions reveal two fundamental properties:
1.  The Schmidt basis $\{|u_i\rangle_A\}$ diagonalizes $\rho_A$, and the Schmidt basis $\{|v_i\rangle_B\}$ diagonalizes $\rho_B$.
2.  The non-zero eigenvalues of $\rho_A$ and $\rho_B$ are identical and are given by the squares of the Schmidt coefficients, $\{p_i\}$.

From the second point, a crucial consequence immediately follows: the entanglement entropy of subsystem $A$ is equal to that of subsystem $B$.

$$
S_A = -\sum_i p_i \ln p_i = S_B
$$

This equality underscores that entanglement is a shared property of the relationship between $A$ and $B$, not a property of one subsystem alone. If one party, Alice, measures the entanglement entropy of her subsystem to be a certain value, she instantly knows that her partner, Bob, would find the exact same entropy for his subsystem, without any communication [@problem_id:2091814]. The entanglement entropy is thus an unambiguous measure of the entanglement across the $A|B$ partition for any pure state.

### A Practical Guide to Calculating Entanglement Entropy

With the theoretical framework in place, let's establish a clear procedure for calculating entanglement entropy.

1.  **Identify the Bipartite Pure State:** Begin with the state vector $|\psi\rangle_{AB}$.
2.  **Find the Schmidt Decomposition (if easy):** If the state is simple, you might be able to write it in Schmidt form by inspection. A state of the form $|\psi\rangle = \sum_i c_i |i\rangle_A |i\rangle_B$ is already in Schmidt form. The eigenvalues of $\rho_A$ are simply $|c_i|^2$.
3.  **Construct the Reduced Density Matrix:** If the Schmidt form is not obvious, compute $\rho_A = \mathrm{Tr}_B(|\psi\rangle\langle\psi|)$. A useful formula for its matrix elements in a basis $\{|k\rangle_A\}$ is $(\rho_A)_{kl} = \sum_j \langle k|_A \langle j|_B |\psi\rangle \langle\psi| l\rangle_A |j\rangle_B$.
4.  **Find the Eigenvalues:** Calculate the eigenvalues, $\{\lambda_i\}$, of the matrix $\rho_A$.
5.  **Compute the Entropy:** Use the von Neumann entropy formula: $S_A = -\sum_i \lambda_i \ln \lambda_i$.

Let's illustrate this with examples.

**Example 1: State in Schmidt Form**
Consider a [two-qubit system](@entry_id:203437) prepared in the state $|\psi\rangle = \frac{\sqrt{3}}{2}|00\rangle + \frac{1}{2}|11\rangle$. This is a pure state that is already in its Schmidt form. The Schmidt coefficients are $\sqrt{p_1} = \sqrt{3}/2$ and $\sqrt{p_2} = 1/2$. The eigenvalues of $\rho_A$ are thus $p_1 = 3/4$ and $p_2 = 1/4$. The entanglement entropy is calculated directly [@problem_id:2091808], [@problem_id:2091838], [@problem_id:2091793]:

$$
S_A = -\left(\frac{3}{4}\ln\frac{3}{4} + \frac{1}{4}\ln\frac{1}{4}\right) = -\frac{3}{4}(\ln 3 - \ln 4) - \frac{1}{4}(-\ln 4) = \ln 4 - \frac{3}{4}\ln 3 = 2\ln 2 - \frac{3}{4}\ln 3 \approx 0.8113 \text{ nats}
$$
(Note: "nats" are the units of entropy when using the natural logarithm). Similarly, for a state like $|\psi\rangle = \sqrt{0.7} |01\rangle + \sqrt{0.3} |10\rangle$, while the basis states for B are permuted, it is still in Schmidt form with eigenvalues $0.7$ and $0.3$ [@problem_id:2091840], [@problem_id:2091839].

**Example 2: General State Requiring Diagonalization**
Consider a state that is not in a simple Schmidt form, such as $|\psi\rangle = \frac{1}{\sqrt{3}}(|00\rangle + |01\rangle + |11\rangle)$ [@problem_id:2091815], [@problem_id:2091831]. To find $S_A$, we must construct $\rho_A$. We can group terms by subsystem A's [basis states](@entry_id:152463):

$$
|\psi\rangle = |0\rangle_A \otimes \frac{1}{\sqrt{3}}(|0\rangle_B + |1\rangle_B) + |1\rangle_A \otimes \frac{1}{\sqrt{3}}|1\rangle_B
$$

The matrix elements of $\rho_A$ in the $\{|0\rangle_A, |1\rangle_A\}$ basis are:
$(\rho_A)_{00} = \langle\psi|0\rangle_A\langle 0|_A|\psi\rangle = \frac{1}{3}(\langle 0|_B + \langle 1|_B)(|0\rangle_B + |1\rangle_B) = \frac{2}{3}$
$(\rho_A)_{11} = \langle\psi|1\rangle_A\langle 1|_A|\psi\rangle = \frac{1}{3}\langle 1|_B|1\rangle_B = \frac{1}{3}$
$(\rho_A)_{01} = \langle\psi|0\rangle_A\langle 1|_A|\psi\rangle = \frac{1}{3}(\langle 0|_B + \langle 1|_B)|1\rangle_B = \frac{1}{3}$
$(\rho_A)_{10} = (\rho_A)_{01}^* = \frac{1}{3}$

So, the [reduced density matrix](@entry_id:146315) is $\rho_A = \frac{1}{3}\begin{pmatrix} 2  1 \\ 1  1 \end{pmatrix}$. This matrix is not diagonal. Its eigenvalues are found by solving the [characteristic equation](@entry_id:149057), which yields $\lambda_{\pm} = \frac{3 \pm \sqrt{5}}{6}$. The entanglement entropy is then:

$$
S_A = -\left[ \frac{3 + \sqrt{5}}{6}\ln\left(\frac{3 + \sqrt{5}}{6}\right) + \frac{3 - \sqrt{5}}{6}\ln\left(\frac{3 - \sqrt{5}}{6}\right) \right]
$$

**Example 3: Partitions in Multipartite Systems**
The concept of entanglement entropy extends to any partition of a pure system into two parts. For a tripartite [pure state](@entry_id:138657) $|\psi\rangle_{ABC}$, we can study the entanglement between qubit $A$ and the composite system $BC$. The procedure remains the same: we treat $BC$ as a single subsystem and trace it out. For the state $|\psi\rangle_{ABC} = \sqrt{0.1} |000\rangle + \sqrt{0.2} |011\rangle + \sqrt{0.3} |101\rangle + \sqrt{0.4} |110\rangle$ [@problem_id:2091832], we find $\rho_A$ by tracing over $B$ and $C$. Grouping terms gives:

$$
|\psi\rangle = |0\rangle_A \otimes (\sqrt{0.1}|00\rangle_{BC} + \sqrt{0.2}|11\rangle_{BC}) + |1\rangle_A \otimes (\sqrt{0.3}|01\rangle_{BC} + \sqrt{0.4}|10\rangle_{BC})
$$

The resulting [reduced density matrix](@entry_id:146315) for A is $\rho_A = \begin{pmatrix} 0.3  0 \\ 0  0.7 \end{pmatrix}$, with entropy $S_A = -(0.3 \ln 0.3 + 0.7 \ln 0.7) \approx 0.6109$ nats.

### Beyond Bipartite Pure States: An Outlook on Multipartite Entanglement

The elegance of entanglement entropy as a unique measure of entanglement is specific to [bipartite pure states](@entry_id:138323). When the total system is in a mixed state, or when we consider partitions of a multipartite system into more than two parts, the situation becomes far more intricate.

Consider the celebrated Greenberger-Horne-Zeilinger (GHZ) state of three qubits:

$$
|\psi\rangle_{ABC} = \frac{1}{\sqrt{2}}(|000\rangle + |111\rangle)
$$

This is a [pure state](@entry_id:138657) of the total system, so $S_{ABC} = 0$. Let's examine the entropies of its subsystems. The reduced state of any single qubit is maximally mixed. For instance:

$$
\rho_A = \mathrm{Tr}_{BC}(|\psi\rangle\langle\psi|) = \frac{1}{2}(|0\rangle\langle 0| + |1\rangle\langle 1|)
$$

This gives $S_A = \ln 2$. By symmetry, $S_B = S_C = \ln 2$. Now consider the reduced state of the $AB$ subsystem by tracing out $C$ [@problem_id:2091826]:

$$
\rho_{AB} = \mathrm{Tr}_{C}(|\psi\rangle\langle\psi|) = \frac{1}{2}(|00\rangle\langle 00| + |11\rangle\langle 11|)
$$

This is a [mixed state](@entry_id:147011), not a pure entangled Bell state. Its entropy is $S_{AB} = \ln 2$. This reveals a key feature of [multipartite entanglement](@entry_id:142544): the entanglement is distributed globally. Tracing out even one qubit can leave the remaining subsystems in a [mixed state](@entry_id:147011). The entanglement is "brittle."

These entropies must obey certain [consistency conditions](@entry_id:637057), such as the **[strong subadditivity](@entry_id:147619) inequality**, which for a tripartite system states $S_{AB} + S_{BC} \ge S_B + S_{ABC}$. Since our total state is pure, $S_{ABC}=0$, and the inequality becomes $S_{AB} + S_{BC} \ge S_B$. For the GHZ state, we found $S_{AB} = \ln 2$, $S_{BC} = \ln 2$, and $S_B = \ln 2$. The inequality holds: $\ln 2 + \ln 2 \ge \ln 2$. Such inequalities reveal the deep mathematical structure governing the distribution of information and entanglement in [many-body quantum systems](@entry_id:161678). While a full exploration is beyond this chapter's scope, the entanglement entropy remains a fundamental starting point for these more advanced investigations.