## Introduction
In the study of linear algebra and [tensor analysis](@entry_id:184019), we often think of [linear maps](@entry_id:185132) as operations that "push" vectors from one space to another. This forward-acting perspective, known as the pushforward, describes how vectors themselves transform. However, to gain a complete understanding, we must also consider a complementary, "backward-acting" operation that describes how [linear functionals](@entry_id:276136)—the very objects that measure vectors—are affected by such a transformation. This operation is the **pullback**, a fundamental concept that illuminates the dual nature of vector spaces and serves as a cornerstone of [differential geometry](@entry_id:145818), [continuum mechanics](@entry_id:155125), and theoretical physics.

This article addresses the crucial knowledge gap between understanding vector transformations and understanding the corresponding transformations of their dual counterparts. By mastering the [pullback](@entry_id:160816), you will gain a deeper, more unified perspective on linear algebra and its applications. We will build this understanding across three distinct chapters. The first, "Principles and Mechanisms," will formally define the pullback, explore its essential algebraic properties, and reveal its elegant connection to the [matrix transpose](@entry_id:155858). Following this, "Applications and Interdisciplinary Connections" will showcase the pullback's power in practical contexts, from simple geometric transformations to advanced applications in physics and [computational engineering](@entry_id:178146). Finally, the "Hands-On Practices" section will offer targeted exercises to solidify your computational skills and conceptual grasp of the topic.

## Principles and Mechanisms

In our study of [linear transformations](@entry_id:149133), we have primarily focused on maps that transform vectors from one vector space into another. This is a "forward" action, often called a [pushforward](@entry_id:158718) in geometric contexts. However, there is a complementary and equally powerful perspective: understanding how a linear map affects [linear functionals](@entry_id:276136)—the objects that measure vectors. This "backward-acting" construction, known as the **[pullback](@entry_id:160816)**, provides deep insights into the dual nature of vector spaces and their transformations. It forms a foundational concept in [tensor analysis](@entry_id:184019), [differential geometry](@entry_id:145818), and theoretical mechanics.

### The Definition of the Pullback

Let $V$ and $W$ be two [vector spaces](@entry_id:136837) over the same field (typically $\mathbb{R}$ for our purposes), and let $T: V \to W$ be a [linear transformation](@entry_id:143080). Recall that the [dual space](@entry_id:146945) of $W$, denoted $W^*$, is the vector space of all linear functionals on $W$—that is, all [linear maps](@entry_id:185132) from $W$ to $\mathbb{R}$.

Suppose we have a linear functional $g \in W^*$. The functional $g$ is designed to act on vectors in $W$. How can we use $T$ and $g$ to create a new functional that acts on vectors in $V$? A natural approach is to first use $T$ to map a vector $v \in V$ into the space $W$, obtaining the vector $T(v) \in W$. Since $T(v)$ is now an element of $W$, we can apply the functional $g$ to it, yielding a scalar value $g(T(v))$.

This two-step process, represented by the composition $g \circ T$, takes a vector $v \in V$ and returns a scalar in $\mathbb{R}$. Let's verify that this composite map is linear. For any vectors $v_1, v_2 \in V$ and any scalar $c$:
$$ (g \circ T)(v_1 + c v_2) = g(T(v_1 + c v_2)) $$
By the linearity of $T$:
$$ g(T(v_1 + c v_2)) = g(T(v_1) + c T(v_2)) $$
And by the linearity of $g$:
$$ g(T(v_1) + c T(v_2)) = g(T(v_1)) + c g(T(v_2)) = (g \circ T)(v_1) + c (g \circ T)(v_2) $$
The composite map $g \circ T$ is indeed a linear functional on $V$, and therefore it is an element of the dual space $V^*$. This new functional is called the **[pullback](@entry_id:160816)** of $g$ by $T$.

Formally, for a [linear map](@entry_id:201112) $T: V \to W$ and a linear functional $g \in W^*$, the pullback of $g$, denoted $T^*g$, is the [linear functional](@entry_id:144884) in $V^*$ defined by:
$$ (T^*g)(v) = g(T(v)) \quad \text{for all } v \in V $$
The notation $T^*g$ emphasizes that we are using the map $T$ to "pull" the functional $g$ from $W^*$ back to $V^*$.

To make this concrete, let's consider a specific example [@problem_id:1508866]. Let $V = P_2(\mathbb{R})$ be the [vector space of polynomials](@entry_id:196204) of degree at most 2, and let $W = \mathbb{R}^3$. Consider the linear map $T: V \to W$ defined by evaluating a polynomial and its first derivative at specific points:
$$ T(p(x)) = \begin{pmatrix} p(0) \\ p'(0) \\ p(1) \end{pmatrix} $$
Now, let $g \in W^*$ be a [linear functional](@entry_id:144884) on $\mathbb{R}^3$ given by $g(\mathbf{w}) = 2w_1 - w_2 + 3w_3$ for a vector $\mathbf{w} = (w_1, w_2, w_3)^T$. The [pullback](@entry_id:160816) $T^*g$ is a functional on the [polynomial space](@entry_id:269905) $V$. Let's see how it acts on a specific polynomial, $q(x) = 4 - 2x + 5x^2$.

Following the definition, $(T^*g)(q) = g(T(q))$. First, we apply the map $T$:
$$ q(0) = 4, \quad q'(x) = -2 + 10x \implies q'(0) = -2, \quad q(1) = 4 - 2 + 5 = 7 $$
So, $T(q(x)) = (4, -2, 7)^T$. This vector is in $W = \mathbb{R}^3$. Now we apply the functional $g$:
$$ g(T(q)) = g(4, -2, 7) = 2(4) - (-2) + 3(7) = 8 + 2 + 21 = 31 $$
Thus, the [pullback](@entry_id:160816) functional $T^*g$, when applied to the polynomial $q(x)$, yields the value $31$. In this way, a functional defined on $\mathbb{R}^3$ has been pulled back to act meaningfully on a space of polynomials [@problem_id:1508866] [@problem_id:1533747].

### The Pullback Map and Its Properties

The [pullback](@entry_id:160816) construction is not just about transforming individual functionals; it defines a map between the dual spaces themselves. For a given [linear map](@entry_id:201112) $T: V \to W$, the **pullback map** (also known as the **dual map** or **[transpose map](@entry_id:152972)**) is the operator $T^*: W^* \to V^*$ that takes each functional $g \in W^*$ to the corresponding [pullback](@entry_id:160816) functional $T^*g \in V^*$.

A crucial property of this map is that it is itself a [linear transformation](@entry_id:143080). To prove this, we must show that for any two functionals $g_1, g_2 \in W^*$ and any scalar $c$, we have $T^*(g_1 + c g_2) = T^*(g_1) + c T^*(g_2)$. We can verify this by checking that the functionals on both sides of the equation give the same result when applied to an arbitrary vector $v \in V$:
$$ (T^*(g_1 + c g_2))(v) = (g_1 + c g_2)(T(v)) \quad \text{(by definition of pullback)} $$
$$ = g_1(T(v)) + c g_2(T(v)) \quad \text{(by definition of addition and scalar multiplication in } W^*) $$
$$ = (T^*g_1)(v) + c (T^*g_2)(v) \quad \text{(by definition of pullback)} $$
$$ = (T^*g_1 + c T^*g_2)(v) \quad \text{(by definition of addition and scalar multiplication in } V^*) $$
Since this holds for all $v \in V$, we conclude that $T^*(g_1 + c g_2) = T^*g_1 + c T^*g_2$, confirming that $T^*: W^* \to V^*$ is a linear map.

Furthermore, the [pullback](@entry_id:160816) operation is linear with respect to the original map. If $S: V \to W$ and $T: V \to W$ are two [linear maps](@entry_id:185132), their sum $S+T$ is also a linear map. For any functional $\alpha \in W^*$, the [pullback](@entry_id:160816) by the sum map relates to the individual [pullbacks](@entry_id:160469) in a simple way [@problem_id:1533715]:
$$ (S+T)^*\alpha = S^*\alpha + T^*\alpha $$
This follows directly from the linearity of $\alpha$:
$$ ((S+T)^*\alpha)(v) = \alpha((S+T)(v)) = \alpha(S(v) + T(v)) = \alpha(S(v)) + \alpha(T(v)) = (S^*\alpha)(v) + (T^*\alpha)(v) $$

### Matrix Representation of the Pullback Map

The connection between $T$ and $T^*$ becomes exceptionally clear when we consider their [matrix representations](@entry_id:146025). Let $V$ and $W$ be [finite-dimensional vector spaces](@entry_id:265491) with ordered bases $\mathcal{B}_V = \{e_1, \dots, e_m\}$ and $\mathcal{B}_W = \{f_1, \dots, f_n\}$, respectively. Let the corresponding [dual bases](@entry_id:151162) be $\mathcal{B}_V^* = \{\epsilon^1, \dots, \epsilon^m\}$ for $V^*$ and $\mathcal{B}_W^* = \{\phi^1, \dots, \phi^n\}$ for $W^*$. Recall that a [dual basis](@entry_id:145076) is defined by the property $\epsilon^i(e_j) = \delta^i_j$, where $\delta^i_j$ is the Kronecker delta.

Let the [linear map](@entry_id:201112) $T: V \to W$ be represented by the $n \times m$ matrix $A$, where the $j$-th column of $A$ is the [coordinate vector](@entry_id:153319) of $T(e_j)$ in the basis $\mathcal{B}_W$. That is, if $T(e_j) = \sum_{k=1}^n A_{kj} f_k$, then $[T]_{\mathcal{B}_W, \mathcal{B}_V} = A$.

What is the matrix representation of the [pullback](@entry_id:160816) map $T^*: W^* \to V^*$ with respect to the [dual bases](@entry_id:151162) $\mathcal{B}_W^*$ and $\mathcal{B}_V^*$? Let this $m \times n$ matrix be $B$. The $k$-th column of $B$ will be the [coordinate vector](@entry_id:153319) of $T^*(\phi^k)$ in the basis $\mathcal{B}_V^*$. If we write $T^*(\phi^k) = \sum_{j=1}^m B_{jk} \epsilon^j$, the component $B_{jk}$ is found by applying this functional to the basis vector $e_j$:
$$ (T^*(\phi^k))(e_j) = \left(\sum_{i=1}^m B_{ik} \epsilon^i\right)(e_j) = B_{jk} $$
But by the definition of the pullback, we can also compute this value as:
$$ (T^*(\phi^k))(e_j) = \phi^k(T(e_j)) $$
Substituting the expression for $T(e_j)$:
$$ \phi^k(T(e_j)) = \phi^k\left(\sum_{i=1}^n A_{ij} f_i\right) = \sum_{i=1}^n A_{ij} \phi^k(f_i) = \sum_{i=1}^n A_{ij} \delta^k_i = A_{kj} $$
By comparing the two results, we find that $B_{jk} = A_{kj}$. This means that the matrix $B$ representing the [pullback](@entry_id:160816) map $T^*$ is the **transpose** of the matrix $A$ representing the original map $T$:
$$ [T^*]_{\mathcal{B}_V^*, \mathcal{B}_W^*} = ([T]_{\mathcal{B}_W, \mathcal{B}_V})^T $$
This fundamental result provides the alternate name "[transpose map](@entry_id:152972)" for $T^*$ and offers a powerful computational tool [@problem_id:1533719]. For example, if $T:\mathbb{R}^3 \to \mathbb{R}^2$ has the matrix representation $A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 3 & -1 \end{pmatrix}$, then the [pullback](@entry_id:160816) map $T^*: (\mathbb{R}^2)^* \to (\mathbb{R}^3)^*$ is represented by the matrix $A^T = \begin{pmatrix} 1 & 0 \\ 2 & 3 \\ 0 & -1 \end{pmatrix}$.

### Core Algebraic Properties and Functoriality

The [pullback](@entry_id:160816) possesses several key algebraic properties that are central to its role in modern mathematics.

#### Contravariance and Composition

Consider three [vector spaces](@entry_id:136837) $U, V, W$ and two linear maps $T: U \to V$ and $S: V \to W$. We can compose them to form a map $S \circ T: U \to W$. What is the pullback of a functional $\omega \in W^*$ by this composite map?
For any vector $u \in U$, we have:
$$ ((S \circ T)^*\omega)(u) = \omega((S \circ T)(u)) = \omega(S(T(u))) $$
Let's analyze the right side. The expression $\omega(S(v))$ for a vector $v \in V$ is precisely the definition of the [pullback](@entry_id:160816) $(S^*\omega)(v)$. Applying this, with $v = T(u)$, we get:
$$ \omega(S(T(u))) = (S^*\omega)(T(u)) $$
Now, this new expression is of the form $\eta(T(u))$, where $\eta = S^*\omega$ is a functional in $V^*$. This is the definition of the [pullback](@entry_id:160816) $(T^*\eta)(u)$. Substituting back, we find:
$$ (S^*\omega)(T(u)) = (T^*(S^*\omega))(u) = (T^* \circ S^*)(\omega)(u) $$
Since this holds for any $u \in U$ and any $\omega \in W^*$, we have established the crucial composition rule:
$$ (S \circ T)^* = T^* \circ S^* $$
This reversal of order is a defining characteristic of what is known as a **contravariant [functor](@entry_id:260898)**. While the original ("covariant") maps compose in the order $S \circ T$, the dual maps compose in the opposite order $T^* \circ S^*$. This property is not just an algebraic curiosity; it is a fundamental structural feature that appears throughout [geometry and physics](@entry_id:265497) [@problem_id:1533753].

#### The Double Pullback

We can apply the [pullback](@entry_id:160816) construction again. Given $T: V \to W$, we have $T^*: W^* \to V^*$. Since $T^*$ is a [linear map](@entry_id:201112), it also has a [pullback](@entry_id:160816) map, $(T^*)^*: (V^*)^* \to (W^*)^*$. This map is often called the **double [pullback](@entry_id:160816)**. It maps elements of the double dual of $V$ (denoted $V^{**}$) to the double dual of $W$ (denoted $W^{**}$).

For [finite-dimensional vector spaces](@entry_id:265491), there exists a canonical, or natural, [isomorphism](@entry_id:137127) $J_V: V \to V^{**}$ that identifies a vector space with its double dual. This [isomorphism](@entry_id:137127) maps a vector $v \in V$ to the evaluation functional $\text{ev}_v \in V^{**}$, whose action on any functional $\phi \in V^*$ is simply $\text{ev}_v(\phi) = \phi(v)$.

Let's trace the action of the double [pullback](@entry_id:160816). For any $v \in V$, the corresponding element in $V^{**}$ is $J_V(v) = \text{ev}_v$. The double [pullback](@entry_id:160816) maps this to $(T^*)^*(\text{ev}_v) \in W^{**}$. What element of $W^{**}$ is this? We can identify it by seeing how it acts on an arbitrary functional $\psi \in W^*$:
$$ ((T^*)^*(\text{ev}_v))(\psi) = \text{ev}_v(T^*\psi) \quad \text{(by definition of double pullback)} $$
$$ = (T^*\psi)(v) \quad \text{(by definition of evaluation map)} $$
$$ = \psi(T(v)) \quad \text{(by definition of pullback)} $$
The final expression, $\psi(T(v))$, is exactly how the evaluation functional $\text{ev}_{T(v)} \in W^{**}$ acts on $\psi$. Therefore, we have shown that for any $\psi \in W^*$:
$$ ((T^*)^*(\text{ev}_v))(\psi) = \text{ev}_{T(v)}(\psi) $$
This implies that $(T^*)^*(\text{ev}_v) = \text{ev}_{T(v)}$. Under the canonical identification where we treat $V$ and $V^{**}$ (and $W$ and $W^{**}$) as the same space, this result simplifies dramatically. The action of $(T^*)^*$ on $v$ is simply $T(v)$ [@problem_id:1533709]. This means the double pullback is equivalent to the original map $T$. This elegant result, often summarized by the commutative diagram identity $(T^*)^* \circ J_V = J_W \circ T$, demonstrates the profound self-consistency of the duality framework.

### Structural Relationships: Kernel and Image

The [pullback](@entry_id:160816) provides a powerful lens through which to view the [fundamental subspaces](@entry_id:190076) associated with a [linear map](@entry_id:201112): its kernel and its image.

A key relationship arises when a pullback vanishes. Suppose for a non-zero functional $\alpha \in W^*$, we find that its pullback $T^*\alpha$ is the zero functional in $V^*$. This means $(T^*\alpha)(v) = 0$ for all $v \in V$. By definition, this is equivalent to $\alpha(T(v)) = 0$ for all $v \in V$. The set of all vectors $\{T(v) | v \in V\}$ is precisely the image of $T$, denoted $\text{Im}(T)$. The condition states that the functional $\alpha$ evaluates to zero for every vector in the image of $T$. This means that the image of $T$ must be a subspace of the kernel of $\alpha$ [@problem_id:1533741]:
$$ T^*\alpha = 0 \iff \text{Im}(T) \subseteq \ker(\alpha) $$

This insight leads directly to a fundamental theorem relating [surjectivity](@entry_id:148931) and [injectivity](@entry_id:147722).
- A map $T: V \to W$ is **surjective** (its image is all of $W$) if and only if its pullback map $T^*: W^* \to V^*$ is **injective** (has a trivial kernel).
*Proof Sketch*: If $T^*$ is not injective, there exists a non-zero functional $\alpha \in W^*$ such that $T^*\alpha = 0$. As shown above, this implies $\text{Im}(T) \subseteq \ker(\alpha)$. Since $\alpha$ is non-zero, its kernel is a proper subspace of $W$. Therefore, $\text{Im}(T)$ is contained in a proper subspace of $W$, meaning $T$ is not surjective. The converse follows by reversing the logic. This duality is highlighted in [@problem_id:1533711].

The dual statement is also true:
- A map $T: V \to W$ is **injective** (its kernel is $\{0\}$) if and only if its [pullback](@entry_id:160816) map $T^*: W^* \to V^*$ is **surjective** (its image is all of $V^*$).

To formalize this, we introduce the concept of the **annihilator**. For a subspace $S \subseteq V$, its annihilator $S^0$ is the subspace of $V^*$ consisting of all functionals that vanish on every vector in $S$:
$$ S^0 = \{ \phi \in V^* \mid \phi(s) = 0 \text{ for all } s \in S \} $$
With this language, we can state two of the most important theorems of this subject:
1.  $\ker(T^*) = (\text{Im}(T))^0$: The kernel of the [pullback](@entry_id:160816) map consists of all functionals that annihilate the image of the original map.
2.  $\text{Im}(T^*) = (\ker(T))^0$: The image of the [pullback](@entry_id:160816) map consists of all functionals that annihilate the kernel of the original map.

The second theorem provides a profound characterization of the functionals that can be produced by a pullback. A functional $\phi \in V^*$ is in the image of $T^*$ if and only if it is zero on the kernel of $T$. In terms of [matrix representations](@entry_id:146025), this means the image of $T^*$ (the [column space](@entry_id:150809) of $A^T$) is the same as the row space of $A$. This provides a direct method for finding a basis for $\text{Im}(T^*)$: simply find a basis for the row space of the matrix of $T$, for instance by using Gaussian elimination to find its [row-echelon form](@entry_id:199986) [@problem_id:1533726].

### Extension to Differential Forms

The concept of the [pullback](@entry_id:160816) extends naturally from the purely algebraic setting of linear algebra to the geometric world of manifolds and [differential forms](@entry_id:146747). In [differential geometry](@entry_id:145818), we associate a [tangent space](@entry_id:141028) $T_p M$ (a vector space) with each point $p$ on a manifold $M$. The dual of this tangent space is the [cotangent space](@entry_id:270516) $T_p^* M$, and its elements are called [covectors](@entry_id:157727) or **1-forms** at $p$.

A [smooth map](@entry_id:160364) $\Phi: M \to N$ between two manifolds induces a linear map between their tangent spaces at corresponding points, called the differential or pushforward, $d\Phi_p: T_p M \to T_{\Phi(p)} N$. The [pullback of a 1-form](@entry_id:160530) $\alpha$ on $N$ to the manifold $M$, denoted $\Phi^*\alpha$, is defined point-wise by using the dual of the differential map. At each point $p \in M$, the value of the pulled-back 1-form is an element of $T_p^*M$ given by:
$$ (\Phi^*\alpha)_p = (d\Phi_p)^* \alpha_{\Phi(p)} $$
In [local coordinates](@entry_id:181200), this operation translates into a direct application of the [chain rule](@entry_id:147422). If $M$ has coordinates $(x^1, \dots, x^m)$ and $N$ has coordinates $(u^1, \dots, u^n)$, the map $\Phi$ is given by functions $u^i(x^1, \dots, x^m)$. A 1-form $\alpha$ on $N$ can be written as $\alpha = \sum_i f_i(u) du^i$. The pullback $\Phi^*\alpha$ is found by substituting the functions for $u$ and transforming the basis 1-forms $du^i$:
$$ du^i = d(u^i(x)) = \sum_j \frac{\partial u^i}{\partial x^j} dx^j $$
Let's consider a map from a plane with coordinates $(x,y)$ to another plane with coordinates $(u,v)$, given by $\Phi(x,y) = (x \cos y, x \sin y)$. This maps Cartesian coordinates to [polar coordinates](@entry_id:159425) (with radius $x$ and angle $y$). Let a 1-form $\alpha = u^2 du + v^2 dv$ be defined on the target space. To compute the pullback $\Phi^*\alpha$, we first express $u$ and $v$ and their differentials in terms of $x$ and $y$ [@problem_id:1533733]:
$$ u = x \cos y \quad \implies \quad du = \cos y \,dx - x \sin y \,dy $$
$$ v = x \sin y \quad \implies \quad dv = \sin y \,dx + x \cos y \,dy $$
Substituting these into the expression for $\alpha$:
$$ \Phi^*\alpha = (x \cos y)^2 (\cos y \,dx - x \sin y \,dy) + (x \sin y)^2 (\sin y \,dx + x \cos y \,dy) $$
Collecting the terms for $dx$ and $dy$:
$$ \Phi^*\alpha = (x^2(\cos^3 y + \sin^3 y)) \,dx + (x^3(\sin^2 y \cos y - \cos^2 y \sin y)) \,dy $$
This result is a [1-form](@entry_id:275851) on the original $(x,y)$ space, demonstrating how the [pullback](@entry_id:160816) seamlessly translates geometric objects (like 1-forms) from a target space back to a source space. This procedure is fundamental to [integration on manifolds](@entry_id:156150), the formulation of physical laws in a coordinate-independent manner, and many other advanced applications.