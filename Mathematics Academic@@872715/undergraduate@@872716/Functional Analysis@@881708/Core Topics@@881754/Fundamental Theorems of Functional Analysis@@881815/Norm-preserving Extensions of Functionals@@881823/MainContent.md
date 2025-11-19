## Introduction
In [functional analysis](@entry_id:146220), a central challenge is understanding the relationship between a part and the whole. When a linear functional is defined on a mere subspace, can its domain be expanded to the entire space without altering its fundamental characteristics, such as its norm? This question is not just a theoretical curiosity; it underpins the very structure of dual spaces and has far-reaching consequences throughout mathematical analysis. This article addresses this pivotal problem by exploring the theory of norm-preserving extensions.

We will embark on a comprehensive journey structured in three parts. First, in **Principles and Mechanisms**, we will dissect the Hahn-Banach theorem, the cornerstone result that guarantees the existence of such extensions, exploring both its analytical form for [normed spaces](@entry_id:137032) and its more general geometric interpretation involving sublinear functionals. Next, in **Applications and Interdisciplinary Connections**, we will move from theory to practice, investigating how these extensions are constructed and applied in various contexts, from [function spaces](@entry_id:143478) to [operator theory](@entry_id:139990), and we will critically examine the crucial question of when an extension is unique. Finally, in **Hands-On Practices**, you will have the opportunity to solidify your understanding by working through guided exercises that illustrate these concepts in concrete computational settings. By the end, you will have a robust understanding of not only the existence of norm-preserving extensions but also their construction, properties, and significance in modern analysis.

## Principles and Mechanisms

In the study of functional analysis, one of the most fundamental questions concerns the relationship between a linear functional defined on a subspace and its potential to be defined on the entire parent space. If a [continuous linear functional](@entry_id:136289) captures certain information about a part of a space, can we extend its reach to the whole space without losing its essential properties? The answer to this question is not only affirmative but also remarkably powerful, forming the bedrock of many profound results in analysis. This chapter will explore the principles and mechanisms governing the extension of linear functionals, guided by the celebrated Hahn-Banach theorem.

### The Hahn-Banach Theorem: The Core Principle of Extension

The Hahn-Banach theorem, in its various forms, is the central result that guarantees the existence of such extensions. We begin with its most common formulation in the context of [normed vector spaces](@entry_id:274725), which is directly concerned with preserving the "size," or norm, of the functional.

#### The Analytical Form: Norm-Preserving Extensions

Let $X$ be a [normed vector space](@entry_id:144421) over the field $\mathbb{F}$ (either $\mathbb{R}$ or $\mathbb{C}$), and let $Y$ be a [vector subspace](@entry_id:151815) of $X$. A [linear functional](@entry_id:144884) $f: Y \to \mathbb{F}$ is a linear map. Its continuity is equivalent to its [boundedness](@entry_id:746948), which is quantified by the **operator norm**:

$$
\|f\|_{Y^*} = \sup_{y \in Y, y \neq 0} \frac{|f(y)|}{\|y\|_X} = \sup_{y \in Y, \|y\|_X=1} |f(y)|
$$

Here, $Y^*$ denotes the continuous [dual space](@entry_id:146945) of $Y$. The Hahn-Banach theorem for [normed spaces](@entry_id:137032) asserts the following:

**Theorem (Hahn-Banach, Normed Space Version):** Let $f$ be a [continuous linear functional](@entry_id:136289) on a subspace $Y$ of a [normed space](@entry_id:157907) $X$. Then there exists a [continuous linear functional](@entry_id:136289) $\tilde{f}: X \to \mathbb{F}$ that is an **extension** of $f$, meaning $\tilde{f}(y) = f(y)$ for all $y \in Y$, and which is **norm-preserving**, meaning $\|\tilde{f}\|_{X^*} = \|f\|_{Y^*}$.

This theorem is a pure [existence theorem](@entry_id:158097); it guarantees that at least one such extension exists, but it does not, in general, provide a unique formula for it. The power of the theorem lies in knowing that an extension with the exact same norm can always be found.

For example, consider the space $X = C([0, 1])$ of continuous real-valued functions on $[0, 1]$ with the [supremum norm](@entry_id:145717), $\|\cdot\|_\infty$. Let $Y$ be the subspace of linear polynomials $p(t) = a + bt$. If we define a functional $f(p) = p(0) + p(1) = 2a+b$, we can compute its norm. The norm of a linear polynomial is $\|p\|_\infty = \max\{|a|, |a+b|\}$. Using the triangle inequality, $|f(p)| = |2a+b| = |(a+b)+a| \le |a+b| + |a| \le 2\max\{|a|, |a+b|\} = 2\|p\|_\infty$. This shows $\|f\|_{Y^*} \le 2$. The bound is achieved for the constant polynomial $p(t)=1$ (where $a=1, b=0$), for which $|f(p)|/\|p\|_\infty = 2/1 = 2$. Thus, $\|f\|_{Y^*} = 2$. The Hahn-Banach theorem guarantees the existence of one or more extensions $\tilde{f}: C([0, 1]) \to \mathbb{R}$ of $f$, and critically, it tells us that the norm of any such [norm-preserving extension](@entry_id:268703) must be exactly 2 [@problem_id:1892544].

#### Fundamental Consequences of Existence

The guaranteed existence of extensions has profound consequences that shape our entire understanding of [normed spaces](@entry_id:137032). Without the Hahn-Banach theorem, we could not be sure that [infinite-dimensional spaces](@entry_id:141268) have a rich enough supply of [continuous linear functionals](@entry_id:262913) to be interesting.

A direct corollary is that the [dual space](@entry_id:146945) of any non-trivial [normed space](@entry_id:157907) is itself non-trivial [@problem_id:1872135]. To see this, let $V$ be a [normed space](@entry_id:157907) with at least one non-[zero vector](@entry_id:156189), $x_0$. Consider the one-dimensional subspace $U = \text{span}\{x_0\}$. We can define a linear functional $g: U \to \mathbb{F}$ by $g(\alpha x_0) = \alpha \|x_0\|$. This functional is continuous, and its norm is exactly 1, since $|g(\alpha x_0)| = |\alpha|\|x_0\| = \|\alpha x_0\|$. By the Hahn-Banach theorem, there exists a [norm-preserving extension](@entry_id:268703) $F: V \to \mathbb{F}$ of $g$. This functional $F$ is an element of the [dual space](@entry_id:146945) $V^*$, and it is not the zero functional because $F(x_0) = g(x_0) = \|x_0\| \neq 0$. Therefore, $V^*$ contains more than just the zero functional.

This leads to another powerful consequence: the ability to separate points. For any two distinct vectors $x, y$ in a [normed space](@entry_id:157907) $V$, there exists a [continuous linear functional](@entry_id:136289) $f \in V^*$ such that $f(x) \neq f(y)$ [@problem_id:1872135]. This is established by applying the previous result to the non-zero vector $z = x-y$. There exists a functional $f \in V^*$ such that $f(z) \neq 0$. By linearity, $f(x-y) = f(x) - f(y) \neq 0$, which implies $f(x) \neq f(y)$. This means the continuous dual space $V^*$ is "large" enough to distinguish between any two points in the original space, a property crucial for defining topologies like the [weak topology](@entry_id:154352).

#### The Existence of Support Functionals

A particularly useful formulation of this idea is often presented as a corollary: For any non-zero vector $x_0$ in a [normed space](@entry_id:157907) $X$, there exists a functional $f \in X^*$ with $\|f\|_{X^*} = 1$ such that $f(x_0) = \|x_0\|_X$. Such a functional is sometimes called a **support functional** for $x_0$. It acts as a tangent hyperplane to the ball of radius $\|x_0\|$ at the point $x_0$.

The proof is the same one used above to show $V^*$ is non-trivial. The functional $g(\alpha x_0) = \alpha \|x_0\|$ on the subspace $\text{span}\{x_0\}$ has norm 1 and satisfies $g(x_0) = \|x_0\|$. Its norm-preserving Hahn-Banach extension $f$ will have the desired properties.

Let's see this in action. Consider the space $c_0$ of real [sequences converging to zero](@entry_id:267556), with the [supremum norm](@entry_id:145717) $\|\cdot\|_\infty$. Its dual space, $c_0^*$, is isometrically isomorphic to the space $\ell^1$ of absolutely summable sequences. For any $a = (a_n) \in \ell^1$, the corresponding functional $f_a \in c_0^*$ is given by $f_a(x) = \sum_{n=1}^\infty a_n x_n$, and its norm is $\|f_a\|_{c_0^*} = \|a\|_1 = \sum_{n=1}^\infty |a_n|$.

Now, let's take a specific vector in $c_0$, say $x_0 = (\frac{\sin(\pi/n)}{n})_{n=1}^\infty$. We first find its norm: $\|x_0\|_\infty = \sup_n |\frac{\sin(\pi/n)}{n}|$. By simple analysis, one can find that the maximum value is attained at $n=2$, where the component is $\frac{\sin(\pi/2)}{2} = \frac{1}{2}$. Thus, $\|x_0\|_\infty = 1/2$. The Hahn-Banach theorem guarantees there is a functional $f \in c_0^*$ with $\|f\|_{c_0^*} = 1$ such that $f(x_0) = 1/2$. To construct it, we need to find the corresponding sequence $a \in \ell^1$ with $\|a\|_1 = 1$. The natural choice is a sequence that picks out the component of $x_0$ where the maximum is achieved. We choose $a = (0, 1, 0, 0, \ldots)$, i.e., $a_2=1$ and all other $a_n=0$. This sequence is in $\ell^1$ and has $\|a\|_1 = 1$. The corresponding functional is $f(x) = x_2$. This functional satisfies $\|f\|_{c_0^*} = 1$ and $f(x_0) = x_{0,2} = 1/2 = \|x_0\|_\infty$, as required [@problem_id:1872174].

### The Geometric Intuition: Sublinear Functionals and Domination

The version of the Hahn-Banach theorem for [normed spaces](@entry_id:137032) is actually a special case of a more fundamental, geometric version formulated for general [vector spaces](@entry_id:136837) without a predefined norm. This version reveals the underlying mechanism of the extension process.

#### Sublinear Functionals

The key concept is that of a **[sublinear functional](@entry_id:143368)** (also known as a gauge). A functional $p: X \to \mathbb{R}$ on a real vector space $X$ is sublinear if it satisfies:
1.  **Subadditivity**: $p(x+y) \le p(x) + p(y)$ for all $x, y \in X$.
2.  **Positive Homogeneity**: $p(\alpha x) = \alpha p(x)$ for all $x \in X$ and all scalars $\alpha \ge 0$.

Notice that any norm is a [sublinear functional](@entry_id:143368). However, a [sublinear functional](@entry_id:143368) is not necessarily a norm; for instance, it is not required to be symmetric ($p(-x) \neq p(x)$ in general) or to satisfy $p(x)=0 \implies x=0$.

The geometric version of the theorem states:

**Theorem (Hahn-Banach, Geometric Form):** Let $X$ be a real vector space, $p: X \to \mathbb{R}$ a [sublinear functional](@entry_id:143368), and $M$ a subspace of $X$. Let $f: M \to \mathbb{R}$ be a linear functional that is **dominated** by $p$ on $M$, i.e., $f(m) \le p(m)$ for all $m \in M$. Then there exists a linear extension $F: X \to \mathbb{R}$ of $f$ that is dominated by $p$ on all of $X$, i.e., $F(x) \le p(x)$ for all $x \in X$.

The connection to the norm-preserving version is made by choosing the [sublinear functional](@entry_id:143368) astutely. Given a functional $f$ on a subspace $Y$, define $p(x) = \|f\|_{Y^*} \|x\|_X$. This $p$ is clearly a [sublinear functional](@entry_id:143368). The initial functional satisfies $|f(y)| \le \|f\|_{Y^*} \|y\|_X = p(y)$ for all $y \in Y$, which implies $f(y) \le p(y)$. The geometric theorem grants an extension $F$ such that $F(x) \le p(x) = \|f\|_{Y^*} \|x\|_X$ for all $x \in X$. Furthermore, since $F(-x) = -F(x)$, we also have $-F(x) \le p(-x) = \|f\|_{Y^*} \|-x\|_X = \|f\|_{Y^*} \|x\|_X$. Together, these imply $|F(x)| \le \|f\|_{Y^*} \|x\|_X$, which means $\|F\|_{X^*} \le \|f\|_{Y^*}$. Since an extension cannot have a smaller norm than the original functional, we must have equality: $\|F\|_{X^*} = \|f\|_{Y^*}$.

#### Minkowski Functionals: Generating Sublinear Functionals from Geometry

A canonical source of sublinear functionals is the geometry of [convex sets](@entry_id:155617). Let $C$ be a **convex**, **absorbing** set in a real vector space $V$ that contains the origin. (A set $C$ is absorbing if for any $x \in V$, there is a $t > 0$ such that $x/t \in C$.) The **Minkowski functional** (or gauge) of $C$ is defined as:
$$ p_C(x) = \inf \left\{ t > 0 \mid \frac{1}{t}x \in C \right\} $$
One can prove that if $C$ has these properties, $p_C$ is a [sublinear functional](@entry_id:143368).

For instance, let $V = \mathbb{R}^2$ and let $C$ be the diamond-shaped region defined by $|x| + |y| \le 1$. This is the [unit ball](@entry_id:142558) for the $L_1$-norm. This set is convex, absorbing, and contains the origin. The condition $(x/t, y/t) \in C$ means $|x/t| + |y/t| \le 1$, or $t \ge |x|+|y|$. The infimum of such $t$ is therefore $p_C(x,y) = |x|+|y|$, which is precisely the $L_1$-norm. Let's verify its [subadditivity](@entry_id:137224) with an example. For vectors $v_1 = (2, 3)$ and $v_2 = (3, -1)$, we have $p_C(v_1) = |2|+|3| = 5$ and $p_C(v_2) = |3|+|-1| = 4$. Their sum is $v_1+v_2 = (5, 2)$, for which $p_C(v_1+v_2) = |5|+|2| = 7$. As expected from [subadditivity](@entry_id:137224), $p_C(v_1+v_2) = 7 \le 9 = p_C(v_1) + p_C(v_2)$ [@problem_id:1872138].

The requirement that the dominating functional $p$ be sublinear is essential for the theorem's guarantee. If we attempt to use a [dominating function](@entry_id:183140) that is not sublinear, the Hahn-Banach theorem does not apply. For example, consider in $\mathbb{R}^2$ the function $p(x, y) = |x| + \sqrt{|y|}$. This function is not positive homogeneous, a requirement for being sublinear. For instance, let $v=(0,1)$ and $\alpha=4$. Then $p(\alpha v) = p(0,4) = \sqrt{4} = 2$, while $\alpha p(v) = 4 p(0,1) = 4\sqrt{1} = 4$. Since $p(\alpha v) \neq \alpha p(v)$, the function is not sublinear. Suppose we have a functional $f(x, 0) = \frac{1}{2}x$ on the subspace $M = \{(x,0)\}$. We can check that $f(x,0) = \frac{1}{2}x \le |x| = p(x,0)$, so $f$ is dominated by $p$ on $M$. Can we find an extension $\tilde{f}(x, y) = \frac{1}{2}x + cy$ that is dominated by $p$ on all of $\mathbb{R}^2$? This requires $\frac{1}{2}x + cy \le |x| + \sqrt{|y|}$ for all $x, y$. A careful analysis shows that this inequality holds for all $x,y$ if and only if $c=0$. In this specific case, a unique dominated extension exists. However, its existence was not guaranteed by the Hahn-Banach theorem, as the [dominating function](@entry_id:183140) was not sublinear [@problem_id:1872130].

### Constructing Extensions: From Theory to Practice

The proof of the Hahn-Banach theorem is constructive in a stepwise manner. It shows how to extend a functional from a subspace $M$ to a slightly larger space $M \oplus \text{span}\{y_0\}$ for some $y_0 \notin M$. The value of the extended functional at $y_0$, say $c_0$, is constrained by the domination inequality, leading to a valid range of choices for $c_0$. Using a tool from set theory called Zorn's Lemma, this one-step extension process can be chained together to reach the entire space.

In [finite-dimensional spaces](@entry_id:151571), we can often carry out this construction explicitly. Consider $X = \mathbb{R}^3$ with the $L_1$-norm, $\|v\|_1 = |v_1|+|v_2|+|v_3|$. Let $M$ be the plane $x_1+x_2+x_3=0$, and define $f: M \to \mathbb{R}$ by $f(x_1, x_2, x_3) = x_1-x_2$. One can show the norm of this functional is $\|f\|_M=1$. We want to find a [norm-preserving extension](@entry_id:268703) to all of $\mathbb{R}^3$. Any linear functional on $\mathbb{R}^3$ is of the form $F(x) = a \cdot x$ for some vector $a$, and its norm in the dual of $(X, \|\cdot\|_1)$ is $\|F\|_X = \|a\|_\infty = \max\{|a_1|, |a_2|, |a_3|\}$. The condition that $F$ extends $f$ forces $a_1-a_3=1$ and $a_2-a_3=-1$. This means the vector $a$ must be of the form $(1+t, -1+t, t)$ for some $t \in \mathbb{R}$. The norm of the extension is $\|F\|_X = \max\{|1+t|, |-1+t|, |t|\}$. To be norm-preserving, this must equal $\|f\|_M = 1$. The only value of $t$ for which $\max\{|1+t|, |t-1|, |t|\} = 1$ is $t=0$. This gives the unique extension vector $a=(1,-1,0)$, corresponding to the extension $F(x) = x_1-x_2$. In the language of the one-step extension, if we decompose $X = M \oplus \text{span}\{y_0\}$ with $y_0=(1,0,0)$, the value $c_0 = F(y_0)$ would be $c_0 = a \cdot y_0 = a_1 = 1+t$. The unique value is $c_0 = 1$ [@problem_id:1872125].

#### The Complex Case

A special version of the theorem deals with extending functionals on [complex vector spaces](@entry_id:264355). The setup is slightly different: we begin with a real-[linear functional](@entry_id:144884) on a subspace and extend it to a complex-linear functional on the whole space.

Let $X$ be a complex [normed space](@entry_id:157907). Let $f_0: Y \to \mathbb{R}$ be a real-[linear functional](@entry_id:144884) on a subspace $Y$. An extension is a **complex-linear** functional $F: X \to \mathbb{C}$ such that $\text{Re}(F(y)) = f_0(y)$ for all $y \in Y$. The theorem guarantees a [norm-preserving extension](@entry_id:268703) exists, where $\|F\|_{X^*} = \|f_0\|_{Y^*_r}$ (the norm of $f_0$ is taken over $Y$ as a real space).

The key to constructing the complex functional $F$ from its real part $g(x) = \text{Re}(F(x))$ is the identity $F(x) = g(x) - i g(ix)$. For $F$ to be complex-linear, $g$ (itself an extension of $f_0$) cannot be just any real-linear functional. This identity links the real and imaginary parts, and complex linearity imposes constraints.

As an example [@problem_id:1872151], consider $X=\mathbb{C}^2$ with norm $\|(z_1, z_2)\| = |z_1|+|z_2|$. Let $Y = \{(x,0) \mid x \in \mathbb{R}\}$ and define the real-linear functional $f_0: Y \to \mathbb{R}$ by $f_0(x,0)=2x$. Its norm is $\|f_0\| = \sup_{|x|=1} |2x| = 2$. We seek a complex-linear extension $F: \mathbb{C}^2 \to \mathbb{C}$ with $\|F\|=2$ and $\text{Re}(F(x,0)) = 2x$.
- The functional $F(z_1, z_2) = 2z_1$ is complex-linear. For $(x,0) \in Y$, $\text{Re}(F(x,0)) = \text{Re}(2x) = 2x$, so it is an extension. Its norm is $\|F\| = \sup_{\|z\|=1} |2z_1| \le 2$, with equality for $(1,0)$. So it is a valid [norm-preserving extension](@entry_id:268703).
- The functional $F(z_1, z_2) = 2(z_1-z_2)$ is also complex-linear. It extends $f_0$ since for $(x,0) \in Y$, $\text{Re}(F(x,0)) = \text{Re}(2x) = 2x$. Its norm is $\|F\| = \sup_{\|z\|=1} |2(z_1-z_2)| \le \sup_{\|z\|=1} 2(|z_1|+|z_2|) = 2$, with equality for $(1,0)$. This is another valid extension.
- In contrast, $F(z_1, z_2) = 2\text{Re}(z_1)$ is not complex-linear, and $F(z_1, z_2) = 2\overline{z_1}$ is conjugate-linear, not complex-linear.

This illustrates both the construction principle and the possibility of non-uniqueness.

### The Question of Uniqueness

The Hahn-Banach theorem is fundamentally an [existence theorem](@entry_id:158097). Uniqueness of the [norm-preserving extension](@entry_id:268703) is a special property of the ambient space, not a general feature.

#### Non-Uniqueness in General Spaces

For many common spaces, norm-preserving extensions are not unique. The space $C([0,1])$ is a classic example. Let $Y$ be the two-dimensional subspace spanned by $\{1, x^2\}$, and define a functional $\phi(a+bx^2) = (a) - 3(a+b/4) = -2a - \frac{3}{4}b$. The norm of this functional on $Y$ can be calculated to be $\|\phi\|=2$. We can find multiple distinct extensions to $C([0,1])$ that all have this same norm of 2 [@problem_id:1872177].
1.  One extension can be formed as a [linear combination](@entry_id:155091) of point evaluations: $F_1(h) = -\frac{5}{4}h(0) - \frac{3}{4}h(1)$. This functional extends $\phi$ and has norm $\|F_1\| = |-\frac{5}{4}|+|-\frac{3}{4}| = \frac{8}{4} = 2$.
2.  Another extension can be formed by a single point evaluation: $F_2(h) = -2h(\sqrt{3/8})$. This also extends $\phi$ and has norm $\|F_2\|=|-2| \cdot \| \text{eval}_{\sqrt{3/8}} \| = 2$.
Since $F_1$ and $F_2$ depend on the values of the function $h$ at different points, they are clearly distinct functionals. This demonstrates explicitly that the Hahn-Banach extension is not necessarily unique.

#### Uniqueness in Hilbert and Uniformly Convex Spaces

Uniqueness, when it occurs, is a consequence of the geometric properties of the space's norm. The premier examples of spaces with unique extensions are Hilbert spaces.

The reason for uniqueness in a Hilbert space $H$ is the **Riesz Representation Theorem**, which states that for every [continuous linear functional](@entry_id:136289) $\tilde{f}$ on $H$, there exists a unique vector $g \in H$ such that $\tilde{f}(x) = \langle x, g \rangle$ for all $x \in H$, and $\|\tilde{f}\| = \|g\|$.
Let $f$ be a functional on a [closed subspace](@entry_id:267213) $Y \subset H$. Since $Y$ is itself a Hilbert space, there is a unique $v \in Y$ such that $f(y) = \langle y, v \rangle$ for all $y \in Y$, and $\|f\|=\|v\|$. A [norm-preserving extension](@entry_id:268703) $\tilde{f}$ must correspond to a unique vector $g \in H$ with $\tilde{f}(x) = \langle x, g \rangle$ and $\|\tilde{f}\| = \|g\|$. The extension property $\langle y, v \rangle = \langle y, g \rangle$ for all $y \in Y$ means that $\langle y, g-v \rangle = 0$, so $g-v$ is in the orthogonal complement $Y^\perp$. We can write $g=v+z$ where $z \in Y^\perp$. The norm-preserving condition $\|f\| = \|\tilde{f}\|$ becomes $\|v\| = \|g\|$. By the Pythagorean theorem, $\|g\|^2 = \|v+z\|^2 = \|v\|^2 + \|z\|^2$. The only way $\|g\|=\|v\|$ is if $\|z\|=0$, which means $z=0$. Therefore, we must have $g=v$. The representing vector for the extension is uniquely determined to be the same as the representing vector for the original functional. Thus, the extension itself is unique [@problem_id:1872165].

This property of uniqueness extends beyond Hilbert spaces to a class of Banach spaces known as **uniformly convex spaces**. A space is uniformly convex if the midpoints of long chords on its unit sphere are deep inside the unit ball. The spaces $L^p$ for $1  p  \infty$ are the most important examples. In these spaces, the conditions for equality in Hölder's inequality (which is the source of the [dual norm](@entry_id:263611)) are very strict, which ultimately forces the representing function in the dual space to be unique.