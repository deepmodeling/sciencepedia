## Introduction
Bilinear and sesquilinear forms are fundamental concepts in linear algebra that generalize the familiar dot product, equipping [vector spaces](@entry_id:136837) with a rich geometric structure. They provide a powerful language to describe notions like length, angle, and orthogonality in contexts far beyond standard Euclidean space, including [function spaces](@entry_id:143478) and the spacetime of modern physics. However, moving from the intuitive properties of the dot product to these more abstract constructs requires a careful development of new definitions and tools. This article addresses this by systematically building the theory of these forms, clarifying the crucial distinctions between operations on real and [complex vector spaces](@entry_id:264355).

This journey is structured to provide a comprehensive understanding. The first chapter, "Principles and Mechanisms," will establish the rigorous definitions of bilinear and sesquilinear forms, explore their powerful representation as matrices, and classify them according to their fundamental properties like [symmetry and degeneracy](@entry_id:177833). Next, "Applications and Interdisciplinary Connections" will bridge theory and practice, showcasing how these forms are indispensable in fields ranging from quantum mechanics and special relativity to [functional analysis](@entry_id:146220) and differential geometry. Finally, "Hands-On Practices" will offer a set of curated problems to reinforce these concepts and develop your computational skills. We begin our exploration with a deep dive into the foundational principles that govern these essential mathematical objects.

## Principles and Mechanisms

Having introduced the broad concept of bilinear and sesquilinear forms, we now embark on a more rigorous exploration of their foundational principles and the mechanisms by which they operate. This chapter will dissect their definitions, explore their representation as matrices, uncover their fundamental structural properties, and investigate how these properties classify them and determine their applications.

### The Formal Definition of Forms

At its core, a bilinear or [sesquilinear form](@entry_id:154766) is a function that takes two vectors as input and produces a scalar. The "linearity" in their names refers to how they behave with respect to [vector addition and scalar multiplication](@entry_id:151375), but the rules differ in crucial ways, particularly when moving from real to [complex vector spaces](@entry_id:264355).

#### Bilinear Forms

Let $V$ be a vector space over a field of scalars $K$ (such as the real numbers $\mathbb{R}$ or complex numbers $\mathbb{C}$). A **[bilinear form](@entry_id:140194)** on $V$ is a function $B: V \times V \to K$ that is linear in each of its two arguments. This means that for any vectors $u, v, w \in V$ and any scalar $c \in K$, the following four conditions hold:

1.  **Additivity in the first argument:** $B(u+v, w) = B(u, w) + B(v, w)$
2.  **Homogeneity in the first argument:** $B(cu, w) = c B(u, w)$
3.  **Additivity in the second argument:** $B(u, v+w) = B(u, v) + B(u, w)$
4.  **Homogeneity in the second argument:** $B(u, cw) = c B(u, w)$

The first two conditions can be combined into a single linearity condition for the first argument: $B(c_1 u_1 + c_2 u_2, w) = c_1 B(u_1, w) + c_2 B(u_2, w)$. Similarly, the last two define linearity in the second argument.

To make this definition concrete, let's consider the real vector space $P_2(\mathbb{R})$ of polynomials with real coefficients and degree at most two. The operations of calculus provide a rich source of examples. Consider the map $B_1(p,q) = \int_0^1 p'(t)q(t) dt$, where $p'(t)$ is the derivative of $p(t)$ [@problem_id:1350858]. To verify if this is a bilinear form, we check its linearity in each argument.

For the first argument, the [linearity of differentiation](@entry_id:161574), $(c_1 p_1 + c_2 p_2)' = c_1 p_1' + c_2 p_2'$, and the [linearity of the integral](@entry_id:189393) allow us to write:
$$
B_1(c_1 p_1 + c_2 p_2, q) = \int_0^1 (c_1 p_1'(t) + c_2 p_2'(t)) q(t) dt = c_1 \int_0^1 p_1'(t)q(t) dt + c_2 \int_0^1 p_2'(t)q(t) dt = c_1 B_1(p_1, q) + c_2 B_1(p_2, q)
$$
For the second argument, the integral's linearity is sufficient:
$$
B_1(p, c_1 q_1 + c_2 q_2) = \int_0^1 p'(t) (c_1 q_1(t) + c_2 q_2(t)) dt = c_1 \int_0^1 p'(t)q_1(t) dt + c_2 \int_0^1 p'(t)q_2(t) dt = c_1 B_1(p, q_1) + c_2 B_1(p, q_2)
$$
Since $B_1$ is linear in both arguments, it is a bilinear form. Similarly, a map like $B_4(p,q) = p''(0)q(1) - 2p(1)q'(0)$ is also a bilinear form, as it is constructed from linear operations like differentiation and evaluation at a point [@problem_id:1350858].

Conversely, a map can fail to be bilinear if it violates linearity in either slot. A common cause of failure is the presence of constant terms or nonlinear operations. For instance, the map $B_2(p,q) = \int_0^1 p(t)q(t) dt + 1$ is not bilinear because $B_2(2p, q) = 2 \int p(t)q(t) dt + 1$, which is not equal to $2 B_2(p, q) = 2 \int p(t)q(t) dt + 2$. The additive constant breaks homogeneity. Likewise, $B_3(p,q) = p(0)q(1) - (q(0))^2$ is not bilinear because the term $(q(0))^2$ is not linear in $q$ [@problem_id:1350858].

A crucial, often overlooked aspect of the definition is the interplay between the vector space, the [scalar field](@entry_id:154310) $K$, and the [codomain](@entry_id:139336) of the form. Consider the vector space $V = \mathbb{C}^2$ over the complex numbers. What if we define a map $f: \mathbb{C}^2 \times \mathbb{C}^2 \to \mathbb{R}$? For example, let $f(z, w) = \text{Re}(z_1 \bar{w}_2)$ [@problem_id:1350820]. If we view $\mathbb{C}^2$ as a vector space over the *real* numbers (a 4-dimensional real space), $f$ is indeed $\mathbb{R}$-bilinear, because for any real scalar $r$, $\text{Re}(rz_1 \bar{w}_2) = r \text{Re}(z_1 \bar{w}_2)$. However, if we treat $\mathbb{C}^2$ as a vector space over the *complex* numbers, $f$ fails to be $\mathbb{C}$-bilinear. Taking the scalar $i \in \mathbb{C}$, we find $f(iz, w) = \text{Re}(iz_1\bar{w}_2)$, which is not generally equal to $if(z,w) = i\text{Re}(z_1\bar{w}_2)$. The latter is not even guaranteed to be a real number, while the [codomain](@entry_id:139336) of $f$ is $\mathbb{R}$. This highlights the necessity of a modified definition for [complex vector spaces](@entry_id:264355), one that is better adapted to their structure.

#### Sesquilinear Forms

When working with [complex vector spaces](@entry_id:264355), especially in contexts involving geometric notions like length and angle, a more natural and useful construct is the [sesquilinear form](@entry_id:154766). The standard Euclidean notion of length-squared for a vector $z=(z_1, \dots, z_n) \in \mathbb{C}^n$ is $|z_1|^2 + \dots + |z_n|^2$, which can be written as $z_1\bar{z}_1 + \dots + z_n\bar{z}_n$. This expression involves [complex conjugation](@entry_id:174690), which is not a linear operation. This motivates the following definition.

Let $V$ be a vector space over the complex numbers $\mathbb{C}$. A **[sesquilinear form](@entry_id:154766)** on $V$ is a function $f: V \times V \to \mathbb{C}$ that is linear in its first argument and **conjugate-linear** in its second. (The name comes from Latin *sesqui-*, meaning "one and a half".) The conditions are:

1.  $f(u+v, w) = f(u, w) + f(v, w)$
2.  $f(cu, w) = c f(u, w)$
3.  $f(u, v+w) = f(u, v) + f(u, w)$
4.  $f(u, cw) = \bar{c} f(u, w)$ (Conjugate-linearity)

Here, $\bar{c}$ is the complex conjugate of the scalar $c$. This modification elegantly handles the properties of complex inner products. For instance, the function $f(z, w) = z_1\bar{w}_1 + i z_2\bar{w}_1 - i z_1\bar{w}_2 + z_2\bar{w}_2$ on $\mathbb{C}^2$ can be verified as a [sesquilinear form](@entry_id:154766) [@problem_id:1350822]. Its linearity in the first argument is straightforward. For the second, we must verify conjugate-linearity. For a scalar $\alpha \in \mathbb{C}$:
$$
f(z, \alpha w) = z_1\overline{(\alpha w_1)} + i z_2\overline{(\alpha w_1)} - i z_1\overline{(\alpha w_2)} + z_2\overline{(\alpha w_2)}
$$
$$
= z_1\bar{\alpha}\bar{w}_1 + i z_2\bar{\alpha}\bar{w}_1 - i z_1\bar{\alpha}\bar{w}_2 + z_2\bar{\alpha}\bar{w}_2 = \bar{\alpha} (z_1\bar{w}_1 + i z_2\bar{w}_1 - i z_1\bar{w}_2 + z_2\bar{w}_2) = \bar{\alpha} f(z, w)
$$
This satisfies the definition. Note that this form is not bilinear over $\mathbb{C}$ because it fails homogeneity in the second argument.

### Matrix Representation of Forms

For [finite-dimensional vector spaces](@entry_id:265491), bilinear and sesquilinear forms can be concretely represented by matrices. This correspondence is not only computationally powerful but also provides a bridge between the abstract properties of forms and the well-understood properties of matrices.

#### The Matrix of a Form in a Given Basis

Let $V$ be an $n$-dimensional vector space with an ordered basis $\mathcal{B} = \{v_1, v_2, \dots, v_n\}$.

For a **[bilinear form](@entry_id:140194)** $B: V \times V \to K$, its **matrix representation** with respect to $\mathcal{B}$ is the $n \times n$ matrix $A$ whose entries are given by:
$$
A_{ij} = B(v_i, v_j)
$$
If vectors $x$ and $y$ have coordinate vectors $[x]_{\mathcal{B}}$ and $[y]_{\mathcal{B}}$ with respect to this basis, the form can be evaluated using matrix multiplication:
$$
B(x, y) = [x]_{\mathcal{B}}^T A [y]_{\mathcal{B}}
$$
where $[x]_{\mathcal{B}}^T$ is the transpose of the column vector $[x]_{\mathcal{B}}$.

For a **[sesquilinear form](@entry_id:154766)** $f: V \times V \to \mathbb{C}$, the definition is analogous. Its matrix representation $A$ with respect to basis $\mathcal{B}$ has entries $A_{ij} = f(v_i, v_j)$. The evaluation formula, however, incorporates conjugation:
$$
f(x, y) = [x]_{\mathcal{B}}^T A \overline{[y]_{\mathcal{B}}}
$$
where $\overline{[y]_{\mathcal{B}}}$ denotes the vector whose entries are the complex conjugates of the entries of $[y]_{\mathcal{B}}$. This formula directly reflects the conjugate-linearity in the second argument.

To see this in action, consider the [sesquilinear form](@entry_id:154766) $f(\mathbf{u}, \mathbf{v}) = u_1 \overline{v_1} + i u_1 \overline{v_2} - i u_2 \overline{v_1} + 2 u_2 \overline{v_2}$ on $\mathbb{C}^2$ and the basis $\mathcal{B} = \{\mathbf{b}_1, \mathbf{b}_2\}$ where $\mathbf{b}_1 = (1, i)$ and $\mathbf{b}_2 = (1, -i)$ [@problem_id:1350864]. To find the matrix $A_{\mathcal{B}}$, we compute its four entries:
$$
(A_{\mathcal{B}})_{11} = f(\mathbf{b}_1, \mathbf{b}_1) = f((1,i), (1,i)) = 1\cdot\bar{1} + i(1)\bar{i} - i(i)\bar{1} + 2(i)\bar{i} = 1 + i(-i) - i^2 + 2i(-i) = 1+1+1+2 = 5
$$
$$
(A_{\mathcal{B}})_{12} = f(\mathbf{b}_1, \mathbf{b}_2) = f((1,i), (1,-i)) = 1\cdot\bar{1} + i(1)\overline{(-i)} - i(i)\bar{1} + 2(i)\overline{(-i)} = 1 + i(i) - i^2 + 2i(i) = 1-1+1-2 = -1
$$
By similar calculations, we find $(A_{\mathcal{B}})_{21} = 3$ and $(A_{\mathcal{B}})_{22} = 1$. Thus, the matrix representation is:
$$
A_{\mathcal{B}} = \begin{pmatrix} 5  -1 \\ 3  1 \end{pmatrix}
$$

#### Change of Basis

The matrix representation of a form is basis-dependent. A natural question is: how does the matrix change when we change the basis? Let $A$ be the matrix of a form with respect to an "old" basis $\mathcal{E}$, and let $A'$ be the matrix with respect to a "new" basis $\mathcal{B}$. Let $P$ be the [change-of-basis matrix](@entry_id:184480) whose columns are the coordinate vectors of the new basis vectors $\{\mathbf{b}_i\}$ expressed in the old basis $\mathcal{E}$. That is, $[\mathbf{b}_i]_{\mathcal{E}}$ is the $i$-th column of $P$. Then any vector $v$ has coordinates satisfying $[v]_{\mathcal{E}} = P [v]_{\mathcal{B}}$.

For a **bilinear form** $B$, we have $B(x, y) = [x]_{\mathcal{E}}^T A [y]_{\mathcal{E}}$. Substituting the [change of coordinates](@entry_id:273139), we get:
$$
B(x, y) = (P[x]_{\mathcal{B}})^T A (P[y]_{\mathcal{B}}) = [x]_{\mathcal{B}}^T (P^T A P) [y]_{\mathcal{B}}
$$
This shows that the new matrix is $A' = P^T A P$. This transformation is called a **[congruence transformation](@entry_id:154837)**. As an example, if a [bilinear form](@entry_id:140194) on $\mathbb{R}^2$ has matrix $A = \begin{pmatrix} 1  -2 \\ 3  1 \end{pmatrix}$ in the standard basis, and we change to the basis $\mathcal{B} = \{(1, -1), (2, 1)\}$, the [change-of-basis matrix](@entry_id:184480) is $P = \begin{pmatrix} 1  2 \\ -1  1 \end{pmatrix}$. The new matrix is then [@problem_id:1350841]:
$$
A' = P^T A P = \begin{pmatrix} 1  -1 \\ 2  1 \end{pmatrix} \begin{pmatrix} 1  -2 \\ 3  1 \end{pmatrix} \begin{pmatrix} 1  2 \\ -1  1 \end{pmatrix} = \begin{pmatrix} 1  -7 \\ 8  7 \end{pmatrix}
$$

For a **[sesquilinear form](@entry_id:154766)** $f$, the transformation law is slightly different due to the conjugation.
$$
f(x, y) = [x]_{\mathcal{E}}^T A \overline{[y]_{\mathcal{E}}} = (P[x]_{\mathcal{B}})^T A \overline{(P[y]_{\mathcal{B}})} = [x]_{\mathcal{B}}^T P^T A \bar{P} \overline{[y]_{\mathcal{B}}}
$$
The new matrix representation is $A' = P^T A \bar{P}$.

Conversely, if we are given the matrix of a form in a non-standard basis, we can use these tools to evaluate it for vectors given in standard coordinates. Suppose a bilinear form $f$ on $\mathbb{R}^2$ has matrix $B = \begin{pmatrix} 2  1 \\ -3  4 \end{pmatrix}$ with respect to the basis $\mathcal{B} = \{v_1, v_2\}$ where $v_1 = (1, 1)$ and $v_2 = (1, -1)$ [@problem_id:1350840]. To compute $f(x, y)$ for $x = (3, 1)$ and $y = (0, 2)$, we first need to find their coordinates in the $\mathcal{B}$ basis. This requires the inverse of the [change-of-basis matrix](@entry_id:184480) $S = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$. We find $[x]_{\mathcal{B}} = S^{-1}x = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$ and $[y]_{\mathcal{B}} = S^{-1}y = \begin{pmatrix} 1 \\ -1 \end{pmatrix}$. Now we can apply the formula:
$$
f(x, y) = [x]_{\mathcal{B}}^T B [y]_{\mathcal{B}} = \begin{pmatrix} 2  1 \end{pmatrix} \begin{pmatrix} 2  1 \\ -3  4 \end{pmatrix} \begin{pmatrix} 1 \\ -1 \end{pmatrix} = -5
$$

### Fundamental Properties and Decompositions

Forms can be classified based on their symmetry properties, which are reflected in their [matrix representations](@entry_id:146025) and have profound implications for their geometric interpretation.

#### Symmetry Properties

A [bilinear form](@entry_id:140194) $B$ is:
*   **Symmetric** if $B(u, v) = B(v, u)$ for all $u, v \in V$. This is equivalent to its matrix representation $A$ being a symmetric matrix ($A = A^T$) in any basis.
*   **Skew-symmetric** (or alternating) if $B(u, v) = -B(v, u)$ for all $u, v \in V$. This implies that $B(v,v)=0$ (if the [field characteristic](@entry_id:154386) is not 2). This is equivalent to its matrix $A$ being skew-symmetric ($A = -A^T$).

For a [sesquilinear form](@entry_id:154766) $f$, the analogous properties involve conjugation:
*   **Hermitian** if $f(u, v) = \overline{f(v, u)}$ for all $u, v \in V$. Its [matrix representation](@entry_id:143451) $A$ is then a Hermitian matrix ($A = A^H$, where $A^H = \bar{A}^T$ is the [conjugate transpose](@entry_id:147909)) in any basis. The form from [@problem_id:1350822], whose matrix in the standard basis is $\begin{pmatrix}1  -i \\ i  1\end{pmatrix}$, is Hermitian.
*   **Skew-Hermitian** if $f(u, v) = -\overline{f(v, u)}$ for all $u, v \in V$. This is equivalent to its matrix being skew-Hermitian ($A = -A^H$).

#### Decomposition into Symmetric and Skew-Symmetric Parts

Any bilinear form $B$ on a vector space over a field of characteristic not equal to 2 (e.g., $\mathbb{R}$ or $\mathbb{C}$) can be uniquely decomposed into the sum of a symmetric form $B_s$ and a skew-symmetric form $B_a$. These components are given by the formulas:
$$
B_s(u, v) = \frac{1}{2} (B(u, v) + B(v, u))
$$
$$
B_a(u, v) = \frac{1}{2} (B(u, v) - B(v, u))
$$
It is a simple exercise to check that $B_s$ is symmetric, $B_a$ is skew-symmetric, and $B_s + B_a = B$. For example, let's find the value of the skew-symmetric part of the form $B(p, q) = p(0)q(1)$ on $P_1(\mathbb{R})$ for the polynomials $p_1(t) = 3t+5$ and $p_2(t) = 2-4t$ [@problem_id:1350832]. We first compute $B(p_1, p_2) = p_1(0)p_2(1) = 5(-2) = -10$ and $B(p_2, p_1) = p_2(0)p_1(1) = 2(8) = 16$. Then,
$$
B_a(p_1, p_2) = \frac{1}{2}(B(p_1, p_2) - B(p_2, p_1)) = \frac{1}{2}(-10 - 16) = -13
$$
Similarly, any [sesquilinear form](@entry_id:154766) can be decomposed into a Hermitian and a skew-Hermitian part.

#### The Associated Quadratic Form

A form that takes two vector inputs can be restricted to a function of a single vector by "feeding it the same vector twice." This gives rise to the associated [quadratic form](@entry_id:153497).

For a bilinear form $B$, the **associated [quadratic form](@entry_id:153497)** is $q: V \to K$ defined by $q(x) = B(x, x)$. Note that both the symmetric and skew-symmetric parts of $B$ contribute to $q(x)$. Specifically, $q(x) = B_s(x,x) + B_a(x,x)$. Since $B_a(x,x) = -B_a(x,x)$, we have $B_a(x,x)=0$, so $q(x) = B_s(x,x)$. This means the [quadratic form](@entry_id:153497) only "sees" the symmetric part of the [bilinear form](@entry_id:140194).

This observation has a powerful converse: a [quadratic form](@entry_id:153497) $q$ determines a *unique symmetric* bilinear form from which it can arise. This symmetric form can be recovered using the **[polarization identity](@entry_id:271819)**. For a real vector space, it is:
$$
B(u, v) = \frac{1}{2} (q(u+v) - q(u) - q(v))
$$
For example, given the quadratic form $q(\mathbf{x}) = x_1^2 + 6x_1x_2 - 2x_2^2$ on $\mathbb{R}^2$ [@problem_id:1350839], we can find its unique symmetric parent form $B$. Let $\mathbf{u}=(u_1, u_2)$ and $\mathbf{v}=(v_1, v_2)$. Then $q(\mathbf{u}+\mathbf{v}) = (u_1+v_1)^2 + 6(u_1+v_1)(u_2+v_2) - 2(u_2+v_2)^2$. After expanding and subtracting $q(\mathbf{u})$ and $q(\mathbf{v})$, the [polarization identity](@entry_id:271819) yields:
$$
B(\mathbf{u}, \mathbf{v}) = \frac{1}{2}(2u_1v_1 + 6u_1v_2 + 6u_2v_1 - 4u_2v_2) = u_1v_1 + 3u_1v_2 + 3u_2v_1 - 2u_2v_2
$$

For a [sesquilinear form](@entry_id:154766) $f$, the quadratic form is also $q(v) = f(v,v)$. Here, a different and equally fundamental property emerges: **the quadratic form $q(v)$ is real-valued for all $v \in V$ if and only if the [sesquilinear form](@entry_id:154766) $f$ is Hermitian** [@problem_id:1350874].
The proof is direct:
- If $f$ is Hermitian, then $f(v,v) = \overline{f(v,v)}$, which by definition means $f(v,v)$ is a real number.
- Conversely, if $f(v,v)$ is always real, one can use a more advanced [polarization identity](@entry_id:271819) for sesquilinear forms to show that $f(u,v) = \overline{f(v,u)}$.

This provides a powerful criterion for checking the Hermitian property. For example, the form $f_D(u, v) = i u_1 \bar{v}_2 - i u_2 \bar{v}_1$ is Hermitian because its quadratic form $q_D(v) = i v_1 \bar{v}_2 - i v_2 \bar{v}_1 = i(v_1 \bar{v}_2 - \overline{v_1 \bar{v}_2}) = i(2i \text{Im}(v_1\bar{v}_2)) = -2\text{Im}(v_1\bar{v}_2)$ is always real. In contrast, $f_F(u, v) = u_1 \bar{v}_1 + u_1 \bar{v}_2 - u_2 \bar{v}_1 + u_2 \bar{v}_2$ is not Hermitian, because its [quadratic form](@entry_id:153497) $q_F(v) = |v_1|^2+|v_2|^2 + 2i\text{Im}(v_1\bar{v}_2)$ is not always real [@problem_id:1350874].

### Degeneracy and the Radical

An important classifying property of a form is whether it is "degenerate". This concept is central to understanding the geometric structures they define.

A [symmetric bilinear form](@entry_id:148281) $B$ is said to be **degenerate** if there exists a non-[zero vector](@entry_id:156189) $v \in V$ such that $B(v, w) = 0$ for all vectors $w \in V$. Such a vector $v$ is called "orthogonal" to the entire space, including itself. The set of all such vectors forms a subspace of $V$ called the **radical** or **kernel** of the form, denoted $\text{rad}(B)$.
$$
\text{rad}(B) = \{v \in V \mid B(v, w) = 0 \text{ for all } w \in V\}
$$
A form is **non-degenerate** if its radical is the trivial subspace $\{0\}$. In terms of [matrix representations](@entry_id:146025), a form is non-degenerate if and only if its matrix $A$ in any basis is invertible (i.e., $\det(A) \neq 0$). The radical is precisely the [null space](@entry_id:151476) of the matrix $A$, i.e., $\text{rad}(B) = \ker(A)$.

Degenerate forms can be conceptually challenging, but linear algebra provides an elegant way to handle them. We can "factor out" the degenerate part by moving to the quotient space $W = V/\text{rad}(B)$. The elements of this space are [cosets](@entry_id:147145) of the form $x + \text{rad}(B)$. On this [quotient space](@entry_id:148218), we can define a new bilinear form $\tilde{B}$ induced by $B$:
$$
\tilde{B}(x + \text{rad}(B), y + \text{rad}(B)) = B(x, y)
$$
This definition is well-defined because if we choose different representatives $x' = x+r_1$ and $y' = y+r_2$ (with $r_1, r_2 \in \text{rad}(B)$), the value of $B(x', y')$ remains unchanged, as all terms involving $r_1$ or $r_2$ vanish by the definition of the radical. The crucial result is that **the induced form $\tilde{B}$ on the [quotient space](@entry_id:148218) $V/\text{rad}(B)$ is always non-degenerate.**

Let's illustrate this with an example [@problem_id:1350850]. Consider the [bilinear form](@entry_id:140194) on $\mathbb{R}^4$ defined by the matrix
$$A = \begin{pmatrix} 1  0  1  0 \\ 0  1  0  1 \\ 1  0  1  0 \\ 0  1  0  1 \end{pmatrix}$$
The radical is the null space of $A$, which is the set of vectors $(x_1, x_2, x_3, x_4)$ such that $x_1+x_3=0$ and $x_2+x_4=0$. This is a 2-dimensional subspace. The quotient space $V/\text{rad}(B)$ is therefore also 2-dimensional. Let's take the basis for this quotient space represented by the vectors $\mathbf{v}_1 = (1, 1, 1, 1)^T$ and $\mathbf{v}_2 = (1, -1, 1, -1)^T$. The matrix $M$ of the induced form $\tilde{B}$ with respect to this basis has entries $M_{ij} = B(\mathbf{v}_i, \mathbf{v}_j)$.
$$
M_{11} = B(\mathbf{v}_1, \mathbf{v}_1) = \mathbf{v}_1^T A \mathbf{v}_1 = 8
$$
$$
M_{12} = B(\mathbf{v}_1, \mathbf{v}_2) = \mathbf{v}_1^T A \mathbf{v}_2 = 0
$$
$$
M_{22} = B(\mathbf{v}_2, \mathbf{v}_2) = \mathbf{v}_2^T A \mathbf{v}_2 = 8
$$
The matrix of the induced form is $M = \begin{pmatrix} 8  0 \\ 0  8 \end{pmatrix}$. The determinant is $\det(M) = 64$, which is non-zero. This confirms that the induced form $\tilde{B}$ is non-degenerate, effectively capturing the "essential" non-degenerate part of the original form $B$.