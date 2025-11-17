## Introduction
The Hahn-Banach theorem is a pillar of [functional analysis](@entry_id:146220), an indispensable tool that guarantees the existence of [continuous linear functionals](@entry_id:262913) with specific, controllable properties. While many theorems in mathematics provide constructive methods, Hahn-Banach is a pure [existence theorem](@entry_id:158097), assuring us that the abstract world of dual spaces is sufficiently rich to analyze and understand the geometric and topological structure of the spaces they are built from. It addresses a fundamental problem: given a [linear functional](@entry_id:144884) defined on a small part of a space (a subspace), can we extend it to the entire space without losing control over its behavior? The theorem's affirmative answer opens the door to a vast range of theoretical results and practical applications.

This article will guide you through the multifaceted world of the Hahn-Banach theorem. The first chapter, **Principles and Mechanisms**, delves into the core of the theorem, presenting its fundamental analytic and geometric forms, exploring the uniqueness of extensions, and introducing its most direct consequences. In the second chapter, **Applications and Interdisciplinary Connections**, we will see the theorem in action, exploring how it provides dual solutions to [optimization problems](@entry_id:142739), underpins other major theorems in analysis, and connects to advanced topics like [spectral theory](@entry_id:275351) and the geometry of Banach spaces. Finally, the **Hands-On Practices** section provides an opportunity to engage with the concepts directly, solving problems that move from fundamental calculations to the nuanced question of extension uniqueness.

## Principles and Mechanisms

The Hahn-Banach theorem is a cornerstone of [functional analysis](@entry_id:146220), providing the theoretical foundation for the existence of [continuous linear functionals](@entry_id:262913) with specific properties. While its proof relies on non-constructive tools like Zorn's Lemma, its consequences are deeply practical, enabling us to analyze the structure of [normed spaces](@entry_id:137032), understand their duals, and establish geometric properties of sets within them. This chapter delves into the core principles of the theorem, exploring its different forms, its geometric interpretations, and its most significant corollaries.

### The Analytic Form: Extension Dominated by a Sublinear Functional

The most fundamental version of the Hahn-Banach theorem addresses the problem of extending a [linear functional](@entry_id:144884) from a subspace to a larger vector space while maintaining control over its "size." This control is not necessarily a norm but a more general object known as a [sublinear functional](@entry_id:143368).

A function $p: X \to \mathbb{R}$ on a real vector space $X$ is called a **[sublinear functional](@entry_id:143368)** if it satisfies two conditions:
1.  **Positive Homogeneity:** $p(\alpha x) = \alpha p(x)$ for all $\alpha \ge 0$ and $x \in X$.
2.  **Subadditivity:** $p(x+y) \le p(x) + p(y)$ for all $x, y \in X$.

Notice that any norm is a [sublinear functional](@entry_id:143368), but the converse is not true. A [sublinear functional](@entry_id:143368) need not be symmetric ($p(-x) \neq p(x)$) or satisfy $p(x)=0 \iff x=0$. For example, on $X = \mathbb{R}^2$, the function $p(x_1, x_2) = |x_1| + 2|x_2|$ is a [sublinear functional](@entry_id:143368) [@problem_id:1892585]. It is clearly positive homogeneous and subadditive (as a weighted $L_1$ norm), but many other functions, like $p(x) = \max\{0, x_1\}$, also qualify.

With this definition, we can state the primary [extension theorem](@entry_id:139304).

**Theorem (Hahn-Banach, Analytic Form):** Let $X$ be a real vector space, $p: X \to \mathbb{R}$ a [sublinear functional](@entry_id:143368), and $Y$ a subspace of $X$. If $f: Y \to \mathbb{R}$ is a [linear functional](@entry_id:144884) such that $f(y) \le p(y)$ for all $y \in Y$, then there exists a linear extension $\tilde{f}: X \to \mathbb{R}$ of $f$ (i.e., $\tilde{f}(y) = f(y)$ for all $y \in Y$) such that $\tilde{f}(x) \le p(x)$ for all $x \in X$.

The power of this theorem lies in its generality. The condition on $p$ is relatively weak, yet the existence of a "controlled" extension is guaranteed. The sublinearity of $p$ is, however, essential. If we attempt to use a [dominating function](@entry_id:183140) that is not sublinear, the [extension theorem](@entry_id:139304) may fail. For instance, if we try to extend a functional on a subspace of $\mathbb{R}^2$ dominated by the non-sublinear function $p(x_1, x_2) = x_1^2 + |x_2|$, we find that an extension is not guaranteed in general. In some specific cases, an extension might exist, but its properties are often rigidly determined in a way that is not characteristic of the Hahn-Banach theorem's flexibility [@problem_id:1892536].

The extension provided by the theorem is generally not unique. The set of all valid extensions itself forms a [convex set](@entry_id:268368). This allows us to search for an extension that is optimal with respect to some additional criterion. For example, if we consider a functional $f$ on the subspace $Y = \{(t, 3t) \mid t \in \mathbb{R}\}$ of $\mathbb{R}^2$ with $f(1, 3) = 5$, which is dominated by $p(x_1, x_2) = |x_1| + 2|x_2|$, the Hahn-Banach theorem guarantees many extensions $\tilde{f}(x_1, x_2) = ax_1 + bx_2$. The conditions $a+3b=5$, $|a| \le 1$, and $|b| \le 2$ define the family of valid extensions. Within this family, we can seek the unique extension that maximizes a certain value, such as $\tilde{f}(0,1) = b$. This optimization yields a unique solution $\tilde{f}(x_1, x_2) = -x_1 + 2x_2$ [@problem_id:1892585].

### Extensions in Normed Spaces and the Complex Case

The most common application of the Hahn-Banach theorem is in the context of [normed spaces](@entry_id:137032). Here, the goal is to extend a [bounded linear functional](@entry_id:143068) from a subspace without increasing its norm. This is a direct consequence of the analytic form.

**Theorem (Hahn-Banach, Norm-Preserving Extension):** Let $Y$ be a subspace of a [normed space](@entry_id:157907) $X$. For any [bounded linear functional](@entry_id:143068) $f \in Y^*$, there exists an extension $\tilde{f} \in X^*$ such that $\tilde{f}(y) = f(y)$ for all $y \in Y$ and $\|\tilde{f}\|_{X^*} = \|f\|_{Y^*}$.

This is achieved by applying the analytic form with the [sublinear functional](@entry_id:143368) $p(x) = \|f\|_{Y^*} \|x\|_X$. Since $f$ is bounded on $Y$, we have $|f(y)| \le \|f\|_{Y^*} \|y\|_X = p(y)$ for all $y \in Y$. The theorem then guarantees an extension $\tilde{f}$ satisfying $|\tilde{f}(x)| \le p(x) = \|f\|_{Y^*} \|x\|_X$ for all $x \in X$. This inequality directly implies that $\|\tilde{f}\|_{X^*} \le \|f\|_{Y^*}$. Since the norm of an extension cannot be smaller than the norm of the original functional, we must have equality, $\|\tilde{f}\|_{X^*} = \|f\|_{Y^*}$.

This result is immensely powerful. For instance, consider the functional $f(p) = p(0) + p(1)$ defined on the subspace $Y$ of linear polynomials within the space $X = C([0, 1])$. By analyzing the ratio $|f(p)| / \|p\|_\infty$, we can find that $\|f\|_{Y^*} = 2$. The Hahn-Banach theorem then asserts, without needing to construct it, that there exists an extension $\tilde{f}: C([0, 1]) \to \mathbb{R}$ with $\|\tilde{f}\|_{X^*} = 2$ [@problem_id:1892544].

The extension to **[complex vector spaces](@entry_id:264355)** requires a careful approach. A direct application of the theorem is not possible, as the proof relies on ordering principles that do not apply straightforwardly with complex scalars. The standard technique is to treat the complex space $X$ as a real vector space $X_\mathbb{R}$. Given a complex linear functional $f: Y \to \mathbb{C}$, its real part, $u(y) = \text{Re}(f(y))$, is a real linear functional on $Y$ (viewed as a real space). We can find a real linear extension $\tilde{u}: X_\mathbb{R} \to \mathbb{R}$ for $u$. The desired complex linear extension $\tilde{f}$ is then reconstructed from $\tilde{u}$.

For any complex [linear functional](@entry_id:144884) $f$, its imaginary part is determined by its real part $u$ due to linearity: $f(ix) = i f(x)$ implies $u(ix) + i v(ix) = i(u(x) + i v(x)) = -v(x) + i u(x)$, where $v = \text{Im}(f)$. Equating real parts gives $v(x) = -u(ix)$. This leads to the unique reconstruction formula:
$$ f(x) = u(x) - i u(ix) $$
This construction guarantees that if one starts with a real-[linear functional](@entry_id:144884) $u$ on a complex space, $f(x) = u(x) - i u(ix)$ defines the unique complex-linear functional whose real part is $u$ [@problem_id:1892579]. The Hahn-Banach theorems for complex spaces are then proven by applying this machinery.

### On the Uniqueness of Extensions

A natural question arises: is the [norm-preserving extension](@entry_id:268703) guaranteed by the Hahn-Banach theorem unique? In general, the answer is no. The uniqueness of the extension depends critically on the geometry of the space.

Consider the space $X = \mathbb{R}^2$ with the $L^1$-norm, $\|(x,y)\|_1 = |x| + |y|$. Let $Y$ be the subspace spanned by $(1,0)$, and define $f_0: Y \to \mathbb{R}$ by $f_0((c,0)) = c$. The norm of $f_0$ is 1. An extension to $X$ must have the form $f(x,y) = x+by$. For this extension to be norm-preserving, its [dual norm](@entry_id:263611) must be 1. The [dual norm](@entry_id:263611) of $f$ on $(\mathbb{R}^2, \|\cdot\|_1)$ is $\max\{1, |b|\}$. Thus, any $b$ with $|b| \le 1$ yields a valid, distinct, [norm-preserving extension](@entry_id:268703). For example, $f_1(x,y) = x$ (for $b=0$) and $f_2(x,y) = x+y$ (for $b=1$) are two different norm-preserving extensions of $f_0$ [@problem_id:1892569].

In stark contrast, **in a Hilbert space, the [norm-preserving extension](@entry_id:268703) is always unique**. This is a consequence of the Riesz Representation Theorem, which provides a concrete mechanism for the extension. For a functional $f$ on a subspace $Y$ of a Hilbert space $H$, there is a unique vector $y_0 \in Y$ such that $f(y) = \langle y, y_0 \rangle$ for all $y \in Y$. The unique [norm-preserving extension](@entry_id:268703) $\tilde{f}$ to all of $H$ is simply given by $\tilde{f}(x) = \langle x, y_0 \rangle$ [@problem_id:1892539]. The rigid geometric structure imposed by the inner product forces this uniqueness.

This dichotomy between general [normed spaces](@entry_id:137032) and Hilbert spaces points to a deeper geometric principle. The property of uniqueness is connected to the "roundness" of the unit ball. A [normed space](@entry_id:157907) is **strictly convex** if its unit sphere contains no line segments. The definitive result is that a norm-preserving Hahn-Banach extension is unique for every functional on every subspace if and only if the dual space $X^*$ is strictly convex [@problem_id:1892584]. This beautiful theorem provides a complete geometric characterization for the uniqueness property.

### Geometric Interpretations and Consequences

The Hahn-Banach theorem can be reframed in geometric language, where it becomes a powerful tool for separating [convex sets](@entry_id:155617). This perspective leads to some of its most important consequences.

#### Supporting Hyperplanes and the Dual Norm

A key corollary of the Hahn-Banach theorem asserts the existence of functionals that "support" a given vector.

**Corollary:** For any non-[zero vector](@entry_id:156189) $x_0$ in a [normed space](@entry_id:157907) $X$, there exists a [bounded linear functional](@entry_id:143068) $f \in X^*$ such that $\|f\|_{X^*} = 1$ and $f(x_0) = \|x_0\|$.

This functional is said to be **norm-attaining** at $x_0$. This corollary immediately proves that the [dual space](@entry_id:146945) $X^*$ of any non-trivial [normed space](@entry_id:157907) is itself non-trivial. Finding such a functional can be a concrete task. For the function $x_0(t) = 3t^2 + 2t$ in $C([0,1])$, its norm is $\|x_0\|_\infty = 5$, attained at $t=1$. The supporting functional is the [evaluation map](@entry_id:149774) $f(g) = g(1)$, which has norm 1 and satisfies $f(x_0) = x_0(1) = 5$ [@problem_id:1892538].

Geometrically, this corollary guarantees the existence of **supporting [hyperplanes](@entry_id:268044)**. A [hyperplane](@entry_id:636937) is a set of the form $H = \{x \in X \mid f(x) = \alpha\}$ for some $f \in X^*$ and $\alpha \in \mathbb{R}$. If $B$ is the closed [unit ball](@entry_id:142558) in $X$ and $x_0$ is a point on its boundary ($\|x_0\|=1$), a [supporting hyperplane](@entry_id:274981) at $x_0$ is a [hyperplane](@entry_id:636937) $H$ containing $x_0$ such that the entire ball $B$ lies on one side of it. The functional $f$ from the corollary, with $\|f\|=1$ and $f(x_0)=1$, defines precisely such a [hyperplane](@entry_id:636937) $H = \{x \in X \mid f(x) = 1\}$. Since $|f(x)| \le \|f\| \|x\| = \|x\|$, any point $x \in B$ satisfies $f(x) \le 1$. Thus, $B$ is contained in the closed half-space $\{x \mid f(x) \le 1\}$. Multiple supporting [hyperplanes](@entry_id:268044) can exist at the same point. For the function $x_0(t) = 4t^3 - 3t$ in $C([0,1])$, which has norm 1, the points where the norm is attained are $t=1$ (where $x_0(1)=1$) and $t=1/2$ (where $x_0(1/2)=-1$). Consequently, both $f_1(g) = g(1)$ and $f_2(g) = -g(1/2)$ are norm-1 functionals that equal 1 at $x_0$, and both define supporting hyperplanes at $x_0$ [@problem_id:1892586].

#### Separation of Convex Sets

The most general geometric formulation of the theorem deals with separating disjoint [convex sets](@entry_id:155617) with a [hyperplane](@entry_id:636937).

**Theorem (Hahn-Banach Separation Theorem):** Let $A$ and $B$ be two non-empty, disjoint, convex subsets of a [normed space](@entry_id:157907) $X$.
1.  If $A$ is open, there exists $f \in X^*$ and $\alpha \in \mathbb{R}$ such that $f(a)  \alpha \le f(b)$ for all $a \in A, b \in B$.
2.  If $A$ is compact and $B$ is closed, there exists $f \in X^*$ and $\alpha, \beta \in \mathbb{R}$ such that $f(a) \le \alpha  \beta \le f(b)$ for all $a \in A, b \in B$. This is known as **strict separation**.

The second case is particularly strong. The condition of strict separation implies $\sup_{a \in A} f(a)  \inf_{b \in B} f(b)$. For example, in $\mathbb{R}^2$, the compact, convex [unit disk](@entry_id:172324) $K = \{ (x,y) \mid x^2+y^2 \le 1 \}$ and the closed, convex half-plane $C = \{ (x,y) \mid x \ge 2 \}$ are disjoint. The [separation theorem](@entry_id:147599) guarantees the existence of a functional that strictly separates them. Indeed, the functional $f(x,y)=x$ achieves this, as $\sup_{k \in K} f(k) = 1$ and $\inf_{c \in C} f(c) = 2$, so $1  2$ [@problem_id:1892551].

### Profound Consequences for Normed Spaces

The principles of extension and separation give rise to several foundational results that shape our understanding of the relationship between a [normed space](@entry_id:157907) and its dual.

1.  **The Dual Space Separates Points:** A direct consequence of the existence of supporting functionals is that the continuous [dual space](@entry_id:146945) $X^*$ is "rich" enough to distinguish any two points in $X$. If $x_1 \neq x_2$, then $x_1 - x_2 \neq 0$, and there must exist an $f \in X^*$ such that $f(x_1 - x_2) \neq 0$, which implies $f(x_1) \neq f(x_2)$. The contrapositive statement is a powerful tool: if $f(x_0)=0$ for *every* functional $f \in X^*$, then the vector $x_0$ must be the zero vector [@problem_id:1892559].

2.  **A Dual Formulation of the Norm:** The corollary on supporting functionals leads to an alternative, and often very useful, definition of the [norm of a vector](@entry_id:154882):
    $$ \|x\| = \sup_{\|f\|_{X^*} = 1} |f(x)| $$
    The inequality $\|x\| \ge |f(x)|$ for any norm-1 functional $f$ is straightforward. The existence of a specific $f_0$ with $\|f_0\|=1$ and $f_0(x)=\|x\|$ shows that the [supremum](@entry_id:140512) is in fact attained and equals $\|x\|$.

3.  **The Canonical Embedding:** Every [normed space](@entry_id:157907) $X$ can be mapped into its [bidual space](@entry_id:266768) $X^{**}$ (the dual of the [dual space](@entry_id:146945)) via the **canonical map** $J: X \to X^{**}$. For each $x \in X$, $J(x)$ is a functional on $X^*$, defined by its action on any $f \in X^*$:
    $$ (J(x))(f) = f(x) $$
    A remarkable consequence of the Hahn-Banach theorem is that this map is an **isometry**. That is, it preserves norms: $\|J(x)\|_{X^{**}} = \|x\|_X$. The proof is a direct application of the dual formulation of the norm:
    $$ \|J(x)\|_{X^{**}} = \sup_{\|f\|_{X^*} \le 1} |(J(x))(f)| = \sup_{\|f\|_{X^*} \le 1} |f(x)| = \|x\|_X $$
    This [isometric embedding](@entry_id:152303) allows us to view $X$ as a subspace of $X^{**}$. This is a crucial first step in defining reflexive spaces—those for which this map is not just an [isometry](@entry_id:150881) but also surjective ($J(X) = X^{**}$). Calculating the bidual norm of an element $J(x)$ simply amounts to calculating the norm of the original element $x$ [@problem_id:1892583].

In summary, the Hahn-Banach theorem, in its various guises, acts as an existence principle that populates the dual space with a rich supply of functionals. These functionals, in turn, serve as probes that reveal the analytic and geometric structure of the original space.