## Introduction
In the study of group theory, representations provide a powerful way to understand abstract groups by translating their structure into the concrete language of linear algebra. A key technique for deepening this understanding is the construction of new representations from existing ones. Among the most fundamental of these constructions is the [symmetric square](@entry_id:137676), which arises naturally from the tensor product of a representation with itself. By isolating the symmetric part of this tensor product, we unlock a structure with profound implications and surprisingly diverse applications. This article serves as a comprehensive guide to the [symmetric square](@entry_id:137676) of a representation, bridging the gap between its abstract definition and its practical utility.

Over the next three chapters, we will systematically build an understanding of this essential concept. The first chapter, **Principles and Mechanisms**, will lay the algebraic groundwork, detailing the construction of the [symmetric square](@entry_id:137676) space $S^2(V)$, its basis, and the celebrated formula for its character. We will then explore how these principles translate into real-world impact in the second chapter, **Applications and Interdisciplinary Connections**, which showcases how the [symmetric square](@entry_id:137676) provides critical insights in fields from quantum chemistry and [vibrational spectroscopy](@entry_id:140278) to Lie theory and number theory. Finally, in **Hands-On Practices**, you will have the opportunity to solidify your knowledge by working through concrete problems that highlight the key computational and conceptual aspects of the theory.

## Principles and Mechanisms

From a given representation $(\rho, V)$ of a group $G$, one can construct new representations using standard linear algebraic operations on the vector space $V$. Among the most important of these constructions are the symmetric and alternating squares, which arise from the decomposition of the [tensor product](@entry_id:140694) space $V \otimes V$. This chapter details the construction of the [symmetric square](@entry_id:137676) representation, its character, and its profound connections to other algebraic and geometric structures.

### Construction of the Symmetric Square

Let $V$ be a [finite-dimensional vector space](@entry_id:187130) over a field $F$. The **tensor square** of $V$, denoted $V \otimes V$, is the space of all linear combinations of simple tensors $v \otimes w$, where $v, w \in V$. A fundamental operator on this space is the **swap operator**, a linear map $\tau: V \otimes V \to V \otimes V$ defined by its action on simple tensors:
$$
\tau(v \otimes w) = w \otimes v
$$
This operator is an involution, as applying it twice returns the original tensor: $\tau^2 = \text{id}$. Consequently, its only possible eigenvalues are $+1$ and $-1$.

The subspace of $V \otimes V$ consisting of tensors that are fixed by the swap operator is called the **[symmetric square](@entry_id:137676)** of $V$, denoted $S^2(V)$. It is the [eigenspace](@entry_id:150590) of $\tau$ corresponding to the eigenvalue $+1$.
$$
S^2(V) = \{ x \in V \otimes V \mid \tau(x) = x \}
$$
Conversely, the eigenspace corresponding to the eigenvalue $-1$ is the **alternating square** (or [exterior square](@entry_id:141620)) of $V$, denoted $\Lambda^2(V)$.
$$
\Lambda^2(V) = \{ x \in V \otimes V \mid \tau(x) = -x \}
$$
If the characteristic of the field $F$ is not 2, the tensor square space decomposes into a [direct sum](@entry_id:156782) of these two subspaces:
$$
V \otimes V = S^2(V) \oplus \Lambda^2(V)
$$
This is because any tensor $x \in V \otimes V$ can be uniquely written as the sum of a symmetric part and an alternating part:
$$
x = \frac{1}{2}(x + \tau(x)) + \frac{1}{2}(x - \tau(x))
$$
where the first term lies in $S^2(V)$ and the second in $\Lambda^2(V)$.

To understand the structure of the [symmetric square](@entry_id:137676), we can construct a basis for it. Let $n = \dim(V)$ and let $\{e_1, e_2, \dots, e_n\}$ be a basis for $V$. The set $\{e_i \otimes e_j \mid 1 \le i, j \le n\}$ forms a basis for $V \otimes V$, which thus has dimension $n^2$.
Now consider which [linear combinations](@entry_id:154743) of these basis vectors are symmetric.
For any [basis vector](@entry_id:199546) $e_i$, the tensor $e_i \otimes e_i$ is clearly symmetric: $\tau(e_i \otimes e_i) = e_i \otimes e_i$. There are $n$ such tensors, and they are [linearly independent](@entry_id:148207).
For any pair of distinct basis vectors $e_i$ and $e_j$ with $i \neq j$, the tensor $e_i \otimes e_j$ is not symmetric. However, we can form the symmetric combination $e_i \otimes e_j + e_j \otimes e_i$. These vectors are fixed by $\tau$ and thus belong to $S^2(V)$. The number of such combinations corresponds to the number of ways to choose two distinct indices from $n$, which is $\binom{n}{2}$.

Together, the set of vectors $\{e_i \otimes e_i\}_{i=1}^n$ and $\{e_i \otimes e_j + e_j \otimes e_i\}_{1 \le i  j \le n}$ forms a basis for $S^2(V)$. Therefore, the dimension of the [symmetric square](@entry_id:137676) is the sum of the counts of these two types of basis vectors [@problem_id:1643920]:
$$
\dim S^2(V) = n + \binom{n}{2} = n + \frac{n(n-1)}{2} = \frac{2n + n^2 - n}{2} = \frac{n(n+1)}{2}
$$
For instance, if $V$ is a 21-dimensional vector space, its [symmetric square](@entry_id:137676) $S^2(V)$ has a dimension of $\frac{21(21+1)}{2} = 231$.

### The Induced Representation on the Symmetric Square

When $V$ is the carrier space for a representation $(\rho, V)$ of a group $G$, the tensor square $V \otimes V$ naturally becomes a representation space as well. The action of a group element $g \in G$ on a [simple tensor](@entry_id:201624) is defined as:
$$
\rho_{V \otimes V}(g)(v \otimes w) = \rho(g)v \otimes \rho(g)w
$$
This is known as the **[tensor product representation](@entry_id:143629)**. A crucial property is that this action commutes with the swap operator $\tau$:
$$
\tau(\rho_{V \otimes V}(g)(v \otimes w)) = \tau(\rho(g)v \otimes \rho(g)w) = \rho(g)w \otimes \rho(g)v = \rho_{V \otimes V}(g)(w \otimes v) = \rho_{V \otimes V}(g)(\tau(v \otimes w))
$$
Because the group action commutes with $\tau$, the eigenspaces of $\tau$ are invariant under the action of $G$. This means that $S^2(V)$ and $\Lambda^2(V)$ are subrepresentations of $V \otimes V$. The representation on $S^2(V)$, which we will denote by $(\rho_{S^2(V)}, S^2(V))$, is called the **[symmetric square](@entry_id:137676) representation**.

To make this concrete, let's construct the matrix representation for the [symmetric square](@entry_id:137676) of the defining representation of $SO(2)$ [@problem_id:1643937]. Let $V = \mathbb{R}^2$ with standard basis $\{e_1, e_2\}$. The defining representation of $SO(2)$ is given by rotation matrices:
$$
\rho(g(\theta)) = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}
$$
The space $V$ has dimension $n=2$, so $S^2(V)$ has dimension $\frac{2(3)}{2}=3$. A standard basis for $S^2(V)$ is $\{b_1, b_2, b_3\}$, where $b_1 = e_1 \otimes e_1$, $b_2 = e_1 \otimes e_2 + e_2 \otimes e_1$, and $b_3 = e_2 \otimes e_2$. (Note: some conventions normalize the mixed term). To find the matrix for $\rho_{S^2(V)}(g(\theta))$, we compute its action on each [basis vector](@entry_id:199546). Let $c = \cos\theta$ and $s = \sin\theta$.
The action on the basis of $V$ is:
$$
\rho(g)e_1 = c e_1 + s e_2 \quad \text{and} \quad \rho(g)e_2 = -s e_1 + c e_2
$$
Now, we find the action on the basis of $S^2(V)$:
1.  **Action on $b_1$**:
    $\rho_{S^2(V)}(g)b_1 = (\rho(g)e_1) \otimes (\rho(g)e_1) = (c e_1 + s e_2) \otimes (c e_1 + s e_2)$
    $= c^2(e_1 \otimes e_1) + cs(e_1 \otimes e_2 + e_2 \otimes e_1) + s^2(e_2 \otimes e_2)$
    $= c^2 b_1 + cs b_2 + s^2 b_3$

2.  **Action on $b_2$**:
    $\rho_{S^2(V)}(g)b_2 = (\rho(g)e_1) \otimes (\rho(g)e_2) + (\rho(g)e_2) \otimes (\rho(g)e_1)$
    $= (c e_1 + s e_2) \otimes (-s e_1 + c e_2) + (-s e_1 + c e_2) \otimes (c e_1 + s e_2)$
    $= (-cs(e_1\otimes e_1) + c^2(e_1\otimes e_2) - s^2(e_2\otimes e_1) + sc(e_2\otimes e_2)) + (-sc(e_1\otimes e_1) - s^2(e_1\otimes e_2) + c^2(e_2\otimes e_1) + cs(e_2\otimes e_2))$
    $= -2sc(e_1 \otimes e_1) + (c^2 - s^2)(e_1 \otimes e_2 + e_2 \otimes e_1) + 2sc(e_2 \otimes e_2)$
    $= -2sc b_1 + (c^2 - s^2) b_2 + 2sc b_3$

3.  **Action on $b_3$**:
    $\rho_{S^2(V)}(g)b_3 = (\rho(g)e_2) \otimes (\rho(g)e_2) = (-s e_1 + c e_2) \otimes (-s e_1 + c e_2)$
    $= s^2(e_1 \otimes e_1) - sc(e_1 \otimes e_2 + e_2 \otimes e_1) + c^2(e_2 \otimes e_2)$
    $= s^2 b_1 - sc b_2 + c^2 b_3$

The matrix for $\rho_{S^2(V)}(g(\theta))$ in this basis is formed by using these coordinate vectors as columns:
$$
\rho_{S^2(V)}(g(\theta)) = \begin{pmatrix} c^2  -2sc  s^2 \\ cs  c^2-s^2  -sc \\ s^2  2sc  c^2 \end{pmatrix}
$$

### The Character of the Symmetric Square

While constructing the [matrix representation](@entry_id:143451) is feasible for small examples, it is often more efficient to work with characters. The character $\chi_{S^2(V)}$ can be derived directly from the character $\chi_V$ of the original representation.

Let $T = \rho(g)$ be the operator on $V$ for a given $g \in G$. The operator on $V \otimes V$ is $T \otimes T$. The character of the tensor square representation is given by the identity $\text{Tr}(A \otimes B) = \text{Tr}(A)\text{Tr}(B)$, so:
$$
\chi_{V \otimes V}(g) = \text{Tr}(T \otimes T) = (\text{Tr}(T))^2 = (\chi_V(g))^2
$$
To find the character of the subrepresentation $S^2(V)$, we can take the trace of the operator $T \otimes T$ restricted to the subspace $S^2(V)$. This can be achieved using the projection operator $P_+ = \frac{1}{2}(\text{id} + \tau)$ that projects $V \otimes V$ onto $S^2(V)$.
$$
\chi_{S^2(V)}(g) = \text{Tr}((T \otimes T)|_{S^2(V)}) = \text{Tr}((T \otimes T) \circ P_+) = \frac{1}{2} \text{Tr}(T \otimes T) + \frac{1}{2} \text{Tr}(\tau \circ (T \otimes T))
$$
We already know $\text{Tr}(T \otimes T) = (\chi_V(g))^2$. The second term requires the identity $\text{Tr}(\tau \circ (A \otimes B)) = \text{Tr}(AB)$. Applying this with $A=B=T$, we get:
$$
\text{Tr}(\tau \circ (T \otimes T)) = \text{Tr}(T^2)
$$
Since $T^2 = (\rho(g))^2 = \rho(g^2)$, its trace is simply the character of the representation evaluated at the group element $g^2$, so $\text{Tr}(T^2) = \chi_V(g^2)$.
Combining these results gives the celebrated formula for the character of the [symmetric square](@entry_id:137676) [@problem_id:1643903] [@problem_id:1643956]:
$$
\chi_{S^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 + \chi_V(g^2) \right]
$$
A similar derivation using the projection $P_- = \frac{1}{2}(\text{id} - \tau)$ onto the alternating square $\Lambda^2(V)$ yields its [character formula](@entry_id:142515):
$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 - \chi_V(g^2) \right]
$$
Note that adding these two characters recovers the character of the full tensor square: $\chi_{S^2(V)}(g) + \chi_{\Lambda^2(V)}(g) = (\chi_V(g))^2 = \chi_{V \otimes V}(g)$, as expected from the [direct sum decomposition](@entry_id:263004).

### Properties and Applications of Symmetric Squares

The [symmetric square](@entry_id:137676) construction is not merely a formal exercise; it reveals deep structural properties of representations and has important applications.

#### Eigenvalues of the Induced Operator

The relationship between the eigenvalues of an operator and its induced action on the [symmetric square](@entry_id:137676) is particularly simple and intuitive. Let $A: V \to V$ be a diagonalizable linear operator with eigenvalues $\{\lambda_1, \dots, \lambda_n\}$ corresponding to a basis of eigenvectors $\{v_1, \dots, v_n\}$. The operator induced on the tensor square, $A \otimes A$, has eigenvectors $v_i \otimes v_j$ with corresponding eigenvalues $\lambda_i \lambda_j$.

The [symmetric square](@entry_id:137676) $S^2(V)$ is an invariant subspace under this action. A basis for $S^2(V)$ can be formed by symmetrized combinations of these eigenvectors: $\{v_i \otimes v_i\}$ and $\{v_i \otimes v_j + v_j \otimes v_i\}$ for $i  j$. The action of $A \otimes A$ on these basis vectors is:
$$
(A \otimes A)(v_i \otimes v_j + v_j \otimes v_i) = (A v_i \otimes A v_j) + (A v_j \otimes A v_i) = (\lambda_i v_i \otimes \lambda_j v_j) + (\lambda_j v_j \otimes \lambda_i v_i) = \lambda_i \lambda_j (v_i \otimes v_j + v_j \otimes v_i)
$$
This shows that these symmetric combinations are eigenvectors of the induced operator on $S^2(V)$ with eigenvalues $\lambda_i \lambda_j$. Therefore, the multiset of eigenvalues of the operator on $S^2(V)$ is given by all pairwise products of the original eigenvalues, $\{\lambda_i \lambda_j \mid 1 \le i \le j \le n\}$.

For example, consider an operator $A$ on a 3-dimensional space whose eigenvalues are the cube roots of unity, $\{1, \omega, \omega^2\}$, where $\omega = \exp(2\pi i/3)$ [@problem_id:1643943]. The induced operator on the 6-dimensional space $S^2(V)$ will have eigenvalues given by the products:
- $1 \cdot 1 = 1$
- $\omega \cdot \omega = \omega^2$
- $\omega^2 \cdot \omega^2 = \omega^4 = \omega$
- $1 \cdot \omega = \omega$
- $1 \cdot \omega^2 = \omega^2$
- $\omega \cdot \omega^2 = \omega^3 = 1$
The resulting multiset of eigenvalues is $\{1, 1, \omega, \omega, \omega^2, \omega^2\}$.

#### Isomorphisms and Duality

The [symmetric square](@entry_id:137676) construction behaves well with respect to representation isomorphisms and duals. A fundamental principle in [representation theory](@entry_id:137998) is that for [complex representations](@entry_id:144331) of [finite groups](@entry_id:139710), two representations are isomorphic if and only if they have the same character. From the [character formula](@entry_id:142515) $\chi_{S^2(V)}(g) = \frac{1}{2}[(\chi_V(g))^2 + \chi_V(g^2)]$, it is immediately clear that if $\chi_{V_1} = \chi_{V_2}$, then $\chi_{S^2(V_1)} = \chi_{S^2(V_2)}$. This implies that if two representations are isomorphic, their symmetric squares are also isomorphic [@problem_id:1643954].

Furthermore, there is a natural relationship between the [symmetric square](@entry_id:137676) and the [dual representation](@entry_id:146263). For a finite-dimensional representation $V$, its dual $V^*$ consists of linear functionals on $V$. The [symmetric square](@entry_id:137676) of the dual, $S^2(V^*)$, and the dual of the [symmetric square](@entry_id:137676), $(S^2 V)^*$, are naturally isomorphic. This can be proven by showing their characters are identical. Let's compute their characters [@problem_id:1643926].
The character of a [dual representation](@entry_id:146263) is the complex conjugate of the original character: $\chi_{V^*}(g) = \overline{\chi_V(g)}$.
1.  The character of $(S^2 V)^*$ at $g$ is $\overline{\chi_{S^2 V}(g)} = \overline{\frac{1}{2}[(\chi_V(g))^2 + \chi_V(g^2)]} = \frac{1}{2}[(\overline{\chi_V(g)})^2 + \overline{\chi_V(g^2)}]$.
2.  The character of $S^2(V^*)$ at $g$ is $\frac{1}{2}[(\chi_{V^*}(g))^2 + \chi_{V^*}(g^2)] = \frac{1}{2}[(\overline{\chi_V(g)})^2 + \overline{\chi_V(g^2)}]$.

Since the characters are identical, the representations are isomorphic: $(S^2 V)^* \cong S^2(V^*)$.

#### Invariant Symmetric Bilinear Forms

One of the most significant applications of the [symmetric square](@entry_id:137676) is in counting invariant structures on a vector space. A **[symmetric bilinear form](@entry_id:148281)** on $V$ is a map $B: V \times V \to \mathbb{C}$ that is linear in each argument and symmetric, i.e., $B(v,w) = B(w,v)$. The space of all such forms is canonically isomorphic to the [symmetric square](@entry_id:137676) of the [dual space](@entry_id:146945), $S^2(V^*)$.

If $V$ is a [representation of a group](@entry_id:137513) $G$, a [bilinear form](@entry_id:140194) $B$ is called **$G$-invariant** if $B(\rho(g)v, \rho(g)w) = B(v,w)$ for all $g \in G$ and $v, w \in V$. This condition means that the form $B$, viewed as an element of $S^2(V^*)$, is a fixed point of the induced action of $G$. In other words, $B$ belongs to the subrepresentation of $S^2(V^*)$ on which $G$ acts trivially.

The dimension of the space of $G$-invariant symmetric [bilinear forms](@entry_id:746794) is therefore equal to the multiplicity of the [trivial representation](@entry_id:141357) $1_G$ in the representation $S^2(V^*)$. This [multiplicity](@entry_id:136466) can be computed using the [character inner product](@entry_id:137125):
$$
\dim(\text{Inv. Sym. Forms}) = \langle \chi_{S^2(V^*)}, \chi_{1_G} \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{S^2(V^*)}(g)
$$
For [complex representations](@entry_id:144331) of a finite group, a representation is isomorphic to its double dual, $V \cong V^{**}$. If the character $\chi_V$ is real-valued, then $V$ is isomorphic to its dual $V^*$, and we can simplify the problem to finding the [multiplicity](@entry_id:136466) of the trivial representation in $S^2(V)$ itself [@problem_id:1643919].

For example, for the natural [permutation representation](@entry_id:139139) of $S_3$ on $W = \mathbb{C}^3$, the character $\chi_W$ is real, so we can count the invariant forms by decomposing $S^2(W)$. The character of $S^2(W)$ can be computed to be $(6, 2, 0)$ on the conjugacy classes $(e, (12), (123))$. The [multiplicity](@entry_id:136466) of the trivial representation is then $\frac{1}{6}[1 \cdot 6 + 3 \cdot 2 + 2 \cdot 0] = 2$. This implies that there are exactly two [linearly independent](@entry_id:148207) $S_3$-invariant symmetric [bilinear forms](@entry_id:746794) on $\mathbb{C}^3$.

This connection can be deepened by relating it to the **Frobenius-Schur indicator** of an irreducible representation $V$, defined as $\nu(V) = \frac{1}{|G|} \sum_{g \in G} \chi_V(g^2)$. The multiplicity of the [trivial representation](@entry_id:141357) in $S^2(V)$ for an irreducible $V$ is precisely $\frac{1}{2}(1 + \nu(V))$. The indicator $\nu(V)$ can be $+1$, $-1$, or $0$, which determines whether $V$ admits a non-degenerate invariant symmetric form ($\nu(V)=1$), an invariant skew-symmetric form ($\nu(V)=-1$), or neither ($V$ is not self-dual or $\nu(V)=0$). If $\nu(V)=-1$, the multiplicity of the trivial representation in $S^2(V)$ is $\frac{1}{2}(1-1)=0$, meaning no such invariant symmetric form exists [@problem_id:1643965].

### A Glimpse Beyond: Symmetric Tensors in Characteristic 2

The elegant decomposition $V \otimes V = S^2(V) \oplus \Lambda^2(V)$ relies on the ability to divide by 2, which is impossible in a field $F$ of **characteristic 2**. In this context, the theory becomes more subtle and interesting.

Let $V$ be a representation over a field with characteristic 2. The swap operator $\tau$ still satisfies $\tau^2=\text{id}$. However, the definition of the alternating square becomes problematic since $\tau(x)=-x$ is the same as $\tau(x)=x$. Let's define the submodule of **[symmetric tensors](@entry_id:148092)** $U = \ker(\text{id}-\tau) = \ker(\text{id}+\tau)$ and the submodule $K = \text{im}(\text{id}+\tau)$.
For any $y \in V \otimes V$, the element $y + \tau(y)$ is in $K$. Notice that this element is also symmetric:
$$
\tau(y + \tau(y)) = \tau(y) + \tau^2(y) = \tau(y) + y = y + \tau(y)
$$
This means that $K$ is a subrepresentation of $U$. This is a stark departure from the characteristic-not-2 case, where the symmetric and alternating subspaces are disjoint (apart from the zero vector).

We can define a quotient representation, the space of **symmetric coinvariants**, as $W = (V \otimes V)/K$. A natural question is to relate the structure of $U$ and $W$. Since $K \subseteq U$, the quotient representation $U/K$ is well-defined. It turns out that a "[short exact sequence](@entry_id:137930)" structure emerges. The representation $W$ contains a subrepresentation isomorphic to $U/K$, and the corresponding quotient is isomorphic to $K$ [@problem_id:1643947]. This reveals a more intricate, nested relationship between symmetric invariants and coinvariants when the characteristic of the field interacts with the algebraic structure of the construction. This serves as a powerful reminder that the familiar properties of representations can change dramatically depending on the underlying field.