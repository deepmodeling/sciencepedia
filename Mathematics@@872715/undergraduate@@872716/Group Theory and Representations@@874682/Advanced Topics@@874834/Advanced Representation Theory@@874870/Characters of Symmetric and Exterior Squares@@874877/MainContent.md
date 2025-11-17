## Introduction
In the study of [group representation theory](@entry_id:141930), a powerful technique is the construction of new representations from existing ones. Among the most fundamental constructions are the **[symmetric square](@entry_id:137676)** and the **[exterior square](@entry_id:141620)**, which arise from the natural [decomposition of a representation](@entry_id:147581)'s [tensor product](@entry_id:140694) with itself. This tensor square, $V \otimes V$, is often reducible, and understanding its internal structure is a key challenge. This article provides the tools to dissect this structure by focusing on the characters of its symmetric and exterior components.

Across the following chapters, you will gain a comprehensive understanding of this topic. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, deriving the celebrated character formulas for both the symmetric and exterior squares from first principles. Following this, the **Applications and Interdisciplinary Connections** chapter will showcase the power of these formulas, demonstrating how they are used to decompose representations, determine the geometric nature of irreducible representations via the Frobenius-Schur indicator, and even connect to fields like combinatorics. Finally, the **Hands-On Practices** section will allow you to apply these concepts to concrete problems, solidifying your knowledge. We begin by exploring the principles that govern these important constructions.

## Principles and Mechanisms

Building upon the foundational concepts of [group representations](@entry_id:145425), we now explore more advanced constructions that allow us to build new representations from existing ones. Among the most important of these are the **[symmetric square](@entry_id:137676)** and the **[exterior square](@entry_id:141620)** (also known as the alternating square). These arise naturally from the decomposition of the tensor product of a representation with itself, and their characters hold a wealth of information about the original representation's structure.

### Decomposing the Tensor Square

Let $V$ be a vector space affording a representation $\rho: G \to GL(V)$ of a group $G$. We can form the [tensor product](@entry_id:140694) space $V \otimes V$. This space also carries a representation of $G$, often denoted $V^{\otimes 2}$ or $\rho^{\otimes 2}$, where the action of a group element $g \in G$ on a pure tensor $v_1 \otimes v_2$ is defined by the diagonal action:
$$
\rho^{\otimes 2}(g)(v_1 \otimes v_2) = (\rho(g)v_1) \otimes (\rho(g)v_2)
$$
The character of this tensor square representation, $\chi_{V^{\otimes 2}}$, is simply the square of the original character $\chi_V$. That is, for any $g \in G$:
$$
\chi_{V^{\otimes 2}}(g) = \chi_V(g)^2
$$
This follows directly from the property that the [trace of a tensor](@entry_id:190669) product of linear operators is the product of their individual traces.

The space $V \otimes V$ possesses an additional layer of structure. Consider the **flip operator** $S: V \otimes V \to V \otimes V$, a [linear map](@entry_id:201112) defined by its action on pure tensors:
$$
S(v_1 \otimes v_2) = v_2 \otimes v_1
$$
This operator is an [involution](@entry_id:203735), as applying it twice returns the original tensor: $S^2 = I$, where $I$ is the identity operator. Consequently, its only possible eigenvalues are $+1$ and $-1$. The [eigenspace](@entry_id:150590) corresponding to the eigenvalue $+1$ consists of **[symmetric tensors](@entry_id:148092)** (tensors $t$ such that $S(t) = t$), while the [eigenspace](@entry_id:150590) for the eigenvalue $-1$ consists of **alternating** or **anti-[symmetric tensors](@entry_id:148092)** (tensors $t$ such that $S(t) = -t$).

Crucially, the group action commutes with the flip operator. For any $g \in G$ and any $v_1, v_2 \in V$:
$$
\rho^{\otimes 2}(g)(S(v_1 \otimes v_2)) = \rho^{\otimes 2}(g)(v_2 \otimes v_1) = (\rho(g)v_2) \otimes (\rho(g)v_1)
$$
$$
S(\rho^{\otimes 2}(g)(v_1 \otimes v_2)) = S((\rho(g)v_1) \otimes (\rho(g)v_2)) = (\rho(g)v_2) \otimes (\rho(g)v_1)
$$
Since $\rho^{\otimes 2}(g) \circ S = S \circ \rho^{\otimes 2}(g)$, Schur's Lemma implies that the [eigenspaces](@entry_id:147356) of $S$ are stable under the group action. They are, therefore, sub-representations of $V \otimes V$. This gives us a [canonical decomposition](@entry_id:634116) of the tensor square representation.

We define:
-   The **[symmetric square](@entry_id:137676)** of $V$, denoted $\mathrm{Sym}^2(V)$, as the sub-representation corresponding to the $+1$ eigenspace of $S$.
-   The **[exterior square](@entry_id:141620)** of $V$, denoted $\Lambda^2(V)$, as the sub-representation corresponding to the $-1$ [eigenspace](@entry_id:150590) of $S$.

This leads to the fundamental [direct sum decomposition](@entry_id:263004) of the representation:
$$
V \otimes V \cong \mathrm{Sym}^2(V) \oplus \Lambda^2(V)
$$
This [isomorphism](@entry_id:137127) of representations implies that their characters must also sum accordingly:
$$
\chi_{V^{\otimes 2}}(g) = \chi_{\mathrm{Sym}^2(V)}(g) + \chi_{\Lambda^2(V)}(g)
$$
for all $g \in G$. [@problem_id:1605595]

### The Character Formulas

To understand the structure of $\mathrm{Sym}^2(V)$ and $\Lambda^2(V)$, we need to determine their characters. We can derive these characters elegantly using [projection operators](@entry_id:154142). The projectors onto the symmetric and exterior subspaces are given by:
$$
P_{\mathrm{Sym}} = \frac{1}{2}(I + S) \quad \text{and} \quad P_{\Lambda} = \frac{1}{2}(I - S)
$$
The character of the sub-representation on $\mathrm{Sym}^2(V)$ is the trace of the projected group action, $\text{Tr}(P_{\mathrm{Sym}} \circ \rho^{\otimes 2}(g))$. Let's write $A = \rho(g)$ for brevity. The operator on the tensor square is $A \otimes A$.
$$
\chi_{\mathrm{Sym}^2(V)}(g) = \text{Tr}\left(\frac{1}{2}(I + S) \circ (A \otimes A)\right) = \frac{1}{2} \left[ \text{Tr}(A \otimes A) + \text{Tr}(S \circ (A \otimes A)) \right]
$$
We have already established that $\text{Tr}(A \otimes A) = (\text{Tr}(A))^2 = (\chi_V(g))^2$. A key identity in linear algebra states that for any [linear operators](@entry_id:149003) $X, Y$ on $V$, $\text{Tr}(S \circ (X \otimes Y)) = \text{Tr}(XY)$. Applying this with $X=Y=A$, we find:
$$
\text{Tr}(S \circ (A \otimes A)) = \text{Tr}(A^2) = \text{Tr}(\rho(g)^2) = \text{Tr}(\rho(g^2)) = \chi_V(g^2)
$$
The step $\text{Tr}(\rho(g)^2) = \text{Tr}(\rho(g^2))$ holds because $\rho$ is a [group homomorphism](@entry_id:140603). Substituting these results into our expression for the character gives the celebrated formula for the character of the [symmetric square](@entry_id:137676) [@problem_id:1605558]:

$$
\chi_{\mathrm{Sym}^2(V)}(g) = \frac{1}{2} \left( (\chi_V(g))^2 + \chi_V(g^2) \right)
$$

A parallel calculation using the projector $P_{\Lambda}$ yields the character of the [exterior square](@entry_id:141620):

$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} \left( (\chi_V(g))^2 - \chi_V(g^2) \right)
$$

These two formulas are cornerstones for analyzing these representations. Note that their sum is indeed $(\chi_V(g))^2$, confirming their consistency with the decomposition of $V \otimes V$.

### Fundamental Properties and Consequences

These character formulas immediately reveal several fundamental properties.

#### Dimensions of the Representations

The dimension of a representation is its character evaluated at the [identity element](@entry_id:139321) $e \in G$. Let $n = \dim(V) = \chi_V(e)$. Since $e^2 = e$, we have $\chi_V(e^2) = \chi_V(e) = n$. Applying this to our formulas:

$$
\dim(\mathrm{Sym}^2(V)) = \chi_{\mathrm{Sym}^2(V)}(e) = \frac{1}{2} \left( (\chi_V(e))^2 + \chi_V(e^2) \right) = \frac{1}{2}(n^2 + n) = \frac{n(n+1)}{2}
$$
This result [@problem_id:1605556] aligns perfectly with the combinatorial understanding of the dimension of the [symmetric square](@entry_id:137676): for a basis $\{e_1, \dots, e_n\}$ of $V$, a basis for $\mathrm{Sym}^2(V)$ is $\{e_i \otimes e_j + e_j \otimes e_i\}_{1 \le i \le j \le n}$, and there are $\binom{n}{2} + n = \frac{n(n+1)}{2}$ such basis vectors.

Similarly, for the [exterior square](@entry_id:141620):
$$
\dim(\Lambda^2(V)) = \chi_{\Lambda^2(V)}(e) = \frac{1}{2} \left( (\chi_V(e))^2 - \chi_V(e^2) \right) = \frac{1}{2}(n^2 - n) = \frac{n(n-1)}{2}
$$
This also corresponds to the combinatorial dimension, given by the number of basis vectors $\{e_i \otimes e_j - e_j \otimes e_i\}_{1 \le i  j \le n}$, which is $\binom{n}{2}$.

#### One-Dimensional Representations

Let's consider the simplest non-trivial case: a [one-dimensional representation](@entry_id:136509) $V$ with character $\psi$. Since $\dim V = 1$, the [exterior square](@entry_id:141620) $\Lambda^2(V)$ must be zero-dimensional, as $\frac{1(1-1)}{2}=0$. The [symmetric square](@entry_id:137676) $\mathrm{Sym}^2(V)$ has dimension $\frac{1(1+1)}{2}=1$. What is its character? Since $\psi$ is a homomorphism from $G$ to $\mathbb{C}^\times$, we have $\psi(g^2) = (\psi(g))^2$. Applying the formula:
$$
\chi_{\mathrm{Sym}^2(V)}(g) = \frac{1}{2} \left( (\psi(g))^2 + \psi(g^2) \right) = \frac{1}{2} \left( (\psi(g))^2 + (\psi(g))^2 \right) = (\psi(g))^2
$$
Thus, for a [one-dimensional representation](@entry_id:136509) $\psi$, the character of its [symmetric square](@entry_id:137676) is simply $\psi^2$ [@problem_id:1605535]. This is intuitive, as for a one-dimensional space $V = \text{span}(v)$, the tensor square $V \otimes V$ is spanned by $v \otimes v$, which is inherently symmetric. The action of $g$ on this [basis vector](@entry_id:199546) is $\psi(g)v \otimes \psi(g)v = (\psi(g))^2 (v \otimes v)$.

#### Isomorphism Condition

When are the symmetric and [exterior square](@entry_id:141620) representations isomorphic? Two representations are isomorphic if and only if their characters are identical. Setting $\chi_{\mathrm{Sym}^2(V)}(g) = \chi_{\Lambda^2(V)}(g)$ for all $g \in G$:
$$
\frac{1}{2} \left( (\chi_V(g))^2 + \chi_V(g^2) \right) = \frac{1}{2} \left( (\chi_V(g))^2 - \chi_V(g^2) \right)
$$
This simplifies to $2\chi_V(g^2) = 0$, which implies that the necessary and sufficient condition is:
$$
\chi_V(g^2) = 0 \quad \text{for all } g \in G
$$
This condition has a powerful consequence. It must hold for the identity element $g=e$. This means $\chi_V(e^2) = \chi_V(e) = 0$. Since $\chi_V(e)$ is the dimension of the representation, this forces $\dim(V) = 0$. Therefore, the only representation for which $\mathrm{Sym}^2(V)$ and $\Lambda^2(V)$ are isomorphic is the zero-dimensional representation, for which both squares are also the zero representation [@problem_id:1605548].

### Applications and Further Insights

The true power of these character formulas lies in their application to analyzing and decomposing representations.

#### Decomposing Representations: An Example with $S_3$

The primary utility of finding the character of a new representation is to decompose it into a [direct sum](@entry_id:156782) of irreducible representations. Let's illustrate this with a concrete example. Consider the [symmetric group](@entry_id:142255) $S_3$, which has three [conjugacy classes](@entry_id:143916) represented by $e$ (identity), $(12)$ ([transposition](@entry_id:155345)), and $(123)$ (3-cycle). It possesses a 2-dimensional [irreducible representation](@entry_id:142733) $V$ (the standard representation), whose character $\chi_V$ is given by the values $(2, 0, -1)$ on these respective classes.

Let's find the structure of $\mathrm{Sym}^2(V)$, which might correspond to the state space of two identical bosonic particles in a system with $S_3$ symmetry [@problem_id:1605586]. We first compute its character, $\chi_{\mathrm{Sym}^2(V)}$, using our formula. We need the values of $\chi_V(g^2)$:
-   For $g = e$, $g^2 = e$, so $\chi_V(g^2) = \chi_V(e) = 2$.
-   For $g = (12)$, $g^2 = e$, so $\chi_V(g^2) = \chi_V(e) = 2$.
-   For $g = (123)$, $g^2 = (132)$, which is in the same conjugacy class as $(123)$, so $\chi_V(g^2) = \chi_V((123)) = -1$.

Now we apply the formula $\chi_{\mathrm{Sym}^2(V)}(g) = \frac{1}{2}((\chi_V(g))^2 + \chi_V(g^2))$:
-   $g = e: \quad \chi_{\mathrm{Sym}^2(V)}(e) = \frac{1}{2}(2^2 + 2) = 3$.
-   $g = (12): \quad \chi_{\mathrm{Sym}^2(V)}((12)) = \frac{1}{2}(0^2 + 2) = 1$. [@problem_id:1605553]
-   $g = (123): \quad \chi_{\mathrm{Sym}^2(V)}((123)) = \frac{1}{2}((-1)^2 + (-1)) = 0$.

So, the character of $\mathrm{Sym}^2(V)$ is $(3, 1, 0)$. To decompose it, we use the [character inner product](@entry_id:137125). Let $\chi_1$ be the trivial character $(1, 1, 1)$ and $\chi_2$ be the [sign character](@entry_id:137578) $(1, -1, 1)$, and $\chi_3 = \chi_V$ be the character of $V$. The multiplicity $a_i$ of an irreducible representation $V_i$ in $\mathrm{Sym}^2(V)$ is given by $a_i = \langle \chi_{\mathrm{Sym}^2(V)}, \chi_i \rangle$.
$$
a_1 = \frac{1}{6} [1 \cdot (3)(1) + 3 \cdot (1)(1) + 2 \cdot (0)(1)] = \frac{1}{6}(3+3) = 1
$$
$$
a_2 = \frac{1}{6} [1 \cdot (3)(1) + 3 \cdot (1)(-1) + 2 \cdot (0)(1)] = \frac{1}{6}(3-3) = 0
$$
$$
a_3 = \frac{1}{6} [1 \cdot (3)(2) + 3 \cdot (1)(0) + 2 \cdot (0)(-1)] = \frac{1}{6}(6) = 1
$$
Thus, we find the decomposition $\mathrm{Sym}^2(V) \cong V_1 \oplus V_3$, where $V_1$ is the trivial representation and $V_3$ is the original standard representation $V$. This reveals the precise irreducible structure of the [symmetric square](@entry_id:137676). A similar calculation for $\Lambda^2(V)$ yields the character $(1, -1, 1)$, which is exactly the [sign character](@entry_id:137578) $\chi_2$. So, $\Lambda^2(V)$ is the one-dimensional sign representation [@problem_id:1617883].

#### The Exterior Square and the Determinant

For two-dimensional representations, the character of the [exterior square](@entry_id:141620) has a particularly elegant interpretation. Let $V$ be a 2-dimensional representation and let the eigenvalues of $\rho(g)$ be $\lambda_1$ and $\lambda_2$. Then:
$$
\chi_V(g) = \text{Tr}(\rho(g)) = \lambda_1 + \lambda_2
$$
$$
\chi_V(g^2) = \text{Tr}(\rho(g^2)) = \text{Tr}(\rho(g)^2) = \lambda_1^2 + \lambda_2^2
$$
Let's compute the character of $\Lambda^2(V)$ using these eigenvalues:
$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} \left( (\lambda_1 + \lambda_2)^2 - (\lambda_1^2 + \lambda_2^2) \right) = \frac{1}{2} \left( (\lambda_1^2 + 2\lambda_1\lambda_2 + \lambda_2^2) - (\lambda_1^2 + \lambda_2^2) \right) = \lambda_1\lambda_2
$$
The product of the eigenvalues is, by definition, the determinant of the operator. Therefore, for any 2-dimensional representation $V$:
$$
\chi_{\Lambda^2(V)}(g) = \det(\rho(g))
$$
This provides a profound link between the [character theory](@entry_id:144021) of the [exterior square](@entry_id:141620) and a fundamental invariant of the [matrix representation](@entry_id:143451) itself. The character of the [exterior square](@entry_id:141620) *is* the determinant character [@problem_id:1605577].

#### Constructions with Direct Sums

The symmetric and [exterior square](@entry_id:141620) constructions also have well-defined behaviors with respect to direct sums of representations. For representations $U$ and $W$, one can show the following isomorphisms:
$$
\mathrm{Sym}^2(U \oplus W) \cong \mathrm{Sym}^2(U) \oplus (U \otimes W) \oplus \mathrm{Sym}^2(W)
$$
$$
\Lambda^2(U \oplus W) \cong \Lambda^2(U) \oplus (U \otimes W) \oplus \Lambda^2(W)
$$
These identities are invaluable for analyzing representations that are known to be reducible. For instance, if one considers a representation $V = \chi_a \oplus \chi_a \oplus \chi_b \oplus \chi_b$ for an [abelian group](@entry_id:139381), where $\chi_a$ and $\chi_b$ are distinct 1D characters, one can compute the character of $\Lambda^2(V)$ by applying this rule [@problem_id:1605543]. Setting $U = \chi_a \oplus \chi_a$ and $W = \chi_b \oplus \chi_b$, we would find $\Lambda^2(V) \cong \Lambda^2(U) \oplus (U \otimes W) \oplus \Lambda^2(W)$. The characters of each piece can be computed, leading to the character of the whole. For example, the character of $U \otimes W$ would be $(2\chi_a)(2\chi_b) = 4\chi_a\chi_b$, since characters multiply under tensor products and add under direct sums.

In conclusion, the symmetric and exterior squares are not merely abstract algebraic constructions. They provide powerful tools for representation theory, equipped with elegant character formulas that unlock deeper structural properties, facilitate the decomposition of [complex representations](@entry_id:144331), and reveal connections to fundamental concepts like the determinant. The appearance of the $\chi_V(g^2)$ term hints at even deeper structures, such as the Frobenius-Schur indicator, which connect the [character theory](@entry_id:144021) of a group to the field over which its representations can be realized.