## Introduction
In mathematics, functions are first introduced as rules that map a single input to a single output. While this point-wise perspective is foundational, a deeper understanding requires us to ask a broader question: how do functions transform entire *sets* of points? This shift in perspective is essential for navigating advanced fields like [mathematical analysis](@entry_id:139664), topology, and measure theory, where the behavior of collections of points is often more significant than the fate of any individual element. This article bridges the gap between the elementary and advanced views of functions by providing a thorough exploration of images and preimages of sets. It is designed to equip you with the definitions, tools, and intuition needed to analyze how functions act as mappings between collections of sets.

We will begin our journey in the **Principles and Mechanisms** chapter, where we formally define the [image and preimage](@entry_id:148315), explore methods for their calculation, and uncover the crucial algebraic rules they obey. Next, the **Applications and Interdisciplinary Connections** chapter will reveal the far-reaching impact of these concepts, demonstrating their use in fields from functional analysis and topology to [fractal geometry](@entry_id:144144) and [ecological modeling](@entry_id:193614). Finally, the **Hands-On Practices** section will allow you to solidify your understanding by tackling carefully selected problems that highlight key principles and techniques. Let's begin by establishing the fundamental principles that govern how functions transform sets from their domain to their codomain.

## Principles and Mechanisms

In the study of functions, we typically begin by considering how a function $f$ maps an individual element $x$ from its domain to a unique element $y$ in its codomain. However, in [mathematical analysis](@entry_id:139664), topology, and other advanced fields, our interest often extends beyond individual points to the behavior of entire sets of points under a function's action. This chapter delves into the principles governing how functions transform sets, introducing the fundamental concepts of the **image** and **[preimage](@entry_id:150899)** of a set. We will explore the mechanics of calculating these, the algebraic rules they obey, and the profound connections between a function's intrinsic properties (like continuity and [injectivity](@entry_id:147722)) and its behavior as a mapping between collections of sets.

### The Image of a Set: The Forward Mapping

The most intuitive way to extend a function's action from points to sets is to collect all the outputs that result from applying the function to every point in a given subset of the domain. This collection is called the image of the set.

**Definition (Image):** Let $f: X \to Y$ be a function and let $A$ be a subset of the domain $X$. The **image** of the set $A$ under $f$, denoted by $f(A)$, is the set of all elements in the [codomain](@entry_id:139336) $Y$ that are the image of at least one element in $A$. Formally,
$$
f(A) = \{f(x) \mid x \in A\}.
$$
It is crucial to note that $f(A)$ is a subset of the codomain $Y$. The set of all possible outputs of the function, $f(X)$, is called the **range** or **image of the function**.

Calculating the image of a set requires a systematic analysis of the function's behavior across the entire set in question. The method for this analysis depends on the nature of the domain and the function itself.

For functions defined on discrete sets, such as the integers $\mathbb{Z}$, we can often determine the image by understanding the function's underlying structure. Consider a function whose output depends on the [congruence](@entry_id:194418) class of the input. For instance, let's analyze the function $f: \mathbb{Z} \to \mathbb{Z}$ defined by $f(n) = n - 3 \lfloor \frac{n-1}{3} \rfloor$. By examining the behavior of $n$ modulo $3$, we can simplify this expression. If $n = 3q+r$ for some integer $q$ and remainder $r \in \{0, 1, 2\}$, we find that $f(n)=1$ if $n \equiv 1 \pmod{3}$, $f(n)=2$ if $n \equiv 2 \pmod{3}$, and $f(n)=3$ if $n \equiv 0 \pmod{3}$. The function effectively maps any integer to one of three values based on its residue modulo 3. With this understanding, we can find the image of complex sets. The set of prime numbers $P = \{2, 3, 5, 7, \dots\}$ contains numbers from all three [congruence classes](@entry_id:635978) modulo 3 (e.g., $7 \equiv 1$, $2 \equiv 2$, $3 \equiv 0$), so its image is $f(P) = \{1, 2, 3\}$. The set of perfect squares $S = \{0, 1, 4, 9, \dots\}$ contains only numbers congruent to $0$ or $1$ modulo 3. Therefore, its image under $f$ can only contain the values corresponding to these residues, namely $f(S) = \{1, 3\}$ [@problem_id:2301745].

For functions defined on continuous sets, such as intervals of real numbers, calculus provides essential tools. If a function $f$ is continuous on a closed, bounded interval $[a, b]$, the Extreme Value Theorem guarantees that $f$ attains a maximum and minimum value. The Intermediate Value Theorem ensures that the image $f([a,b])$ is the closed interval connecting these minimum and maximum values. For more complex intervals or functions, we must analyze the function's monotonicity and limiting behavior.

A common technique is to simplify the function's expression. Consider the function $g(x) = (x - \lfloor x \rfloor)^2 - (x - \lfloor x \rfloor) + c$ for some constant $c$. The term $t = x - \lfloor x \rfloor$ represents the [fractional part](@entry_id:275031) of $x$, which is always in the interval $[0, 1)$. By substituting $t$, we see that the image of all of $\mathbb{R}$ under $g$ is identical to the image of the interval $[0, 1)$ under the much simpler quadratic function $h(t) = t^2 - t + c$. By completing the square, $h(t) = (t - \frac{1}{2})^2 - \frac{1}{4} + c$. On $[0, 1)$, this parabola has its minimum at $t = \frac{1}{2}$, with value $c - \frac{1}{4}$. The maximum value is approached as $t \to 1$ and is also attained at $t=0$, giving $h(0)=c$. Thus, the image of $\mathbb{R}$ under $g$ is the interval $[c - \frac{1}{4}, c)$ union $\{c\}$, which is $[c-\frac{1}{4}, c]$. If we are given that the minimum is $\frac{11}{4}$, we can solve $c - \frac{1}{4} = \frac{11}{4}$ to find $c=3$, which means the [supremum](@entry_id:140512) of the image is 3 [@problem_id:2301733].

The [topological properties](@entry_id:154666) of the domain set are not always preserved in the image. For instance, the image of a closed set under a continuous function is not necessarily closed. Consider the function $f(x) = \exp(-x^2)$ and the closed, unbounded set $A = [1, \infty)$. The function is continuous and strictly decreasing on this interval. The maximum value is at the endpoint, $f(1) = e^{-1}$. As $x \to \infty$, $f(x) \to 0$. Since $f(x)$ is always positive, the image $f(A)$ is the interval $(0, e^{-1}]$. This set is not closed in $\mathbb{R}$ because it does not contain its limit point 0, and it is not open because it contains its endpoint $e^{-1}$ [@problem_id:2301753]. The points in the closure of an image that are not in the image itself are known as **unattained [limit points](@entry_id:140908)**. These often arise from the limiting behavior of the function over open or unbounded intervals [@problem_id:2301737].

### The Preimage of a Set: The Reverse Mapping

Complementary to the concept of an image is the [preimage](@entry_id:150899), which involves looking backward from the codomain to identify all points in the domain that map into a specific target set.

**Definition (Preimage):** Let $f: X \to Y$ be a function and let $B$ be a subset of the codomain $Y$. The **[preimage](@entry_id:150899)** (or **[inverse image](@entry_id:154161)**) of the set $B$ under $f$, denoted by $f^{-1}(B)$, is the set of all elements in the domain $X$ that map to an element in $B$. Formally,
$$
f^{-1}(B) = \{x \in X \mid f(x) \in B\}.
$$
It is critical to understand that the notation $f^{-1}$ here refers to the [preimage](@entry_id:150899) of a *set* and does not imply that an inverse *function* exists. The preimage is well-defined for any function, regardless of whether it is bijective.

Calculating a preimage typically involves solving an equation or an inequality. We seek all $x$ in the domain that satisfy the condition $f(x) \in B$.

If the target set $B$ is a singleton, $B = \{c\}$, its preimage $f^{-1}(\{c\})$ is the set of all $x$ such that $f(x) = c$. This is often called a **level set** of the function $f$. For example, consider the function $f: \mathbb{C} \to \mathbb{R}$ given by $f(z) = \text{Re}(z^2 + \bar{z})$. To find the [preimage](@entry_id:150899) of $\{0\}$, we set up the equation $f(z)=0$. By writing $z = x+iy$, we find $f(z) = x^2 - y^2 + x$. The level set is thus defined by the equation $x^2 - y^2 + x = 0$. By [completing the square](@entry_id:265480) in $x$, we can rewrite this as $(x + \frac{1}{2})^2 - y^2 = \frac{1}{4}$. This is the [standard equation of a hyperbola](@entry_id:175413). Thus, the preimage of $\{0\}$ is not a collection of discrete points but a continuous curve in the complex plane [@problem_id:2301738].

If the target set $B$ is an interval, the preimage is found by solving an inequality. Let's find the [preimage](@entry_id:150899) of the interval $S = [0, 1]$ under the function $f: \mathbb{R}^2 \to \mathbb{R}$ defined by $f(x, y) = x^2 - y$. The condition for a point $(x, y)$ to be in the [preimage](@entry_id:150899) $f^{-1}(S)$ is that its image $f(x,y)$ must be in $S$. This gives the double inequality:
$$
0 \le f(x, y) \le 1
$$
Substituting the function's definition, we get:
$$
0 \le x^2 - y \le 1
$$
This can be broken down into two separate inequalities: $x^2 - y \ge 0$, which implies $y \le x^2$, and $x^2 - y \le 1$, which implies $y \ge x^2 - 1$. The preimage is the set of all points $(x,y)$ in the plane that satisfy both conditions simultaneously: $x^2 - 1 \le y \le x^2$. Geometrically, this describes the closed region bounded between the two parabolas $y=x^2-1$ and $y=x^2$ [@problem_id:2301719].

### Interactions with Set Operations

The true power and subtlety of images and preimages become apparent when we study how they interact with [set operations](@entry_id:143311) like union, intersection, and complement. We find that preimages have very "well-behaved" properties, whereas images require more care.

Let $f: X \to Y$ be a function, with $A, A_i \subseteq X$ and $B, B_i \subseteq Y$.

**Properties of Preimages:**
The [preimage](@entry_id:150899) operator commutes elegantly with all standard [set operations](@entry_id:143311). For any collection of subsets $\{B_i\}_{i \in I}$ of $Y$:
*   **Union:** $f^{-1}(\bigcup_{i \in I} B_i) = \bigcup_{i \in I} f^{-1}(B_i)$
*   **Intersection:** $f^{-1}(\bigcap_{i \in I} B_i) = \bigcap_{i \in I} f^{-1}(B_i)$
*   **Complement:** $f^{-1}(B^c) = (f^{-1}(B))^c$

The proof for the complement property is particularly illustrative of the direct logical flow. An element $x \in X$ is in $f^{-1}(B^c)$ if and only if $f(x) \in B^c$. This is equivalent to saying that $f(x)$ is *not* in $B$, which in turn is equivalent to $x$ *not* being in $f^{-1}(B)$. Finally, this is true if and only if $x$ is in the complement of $f^{-1}(B)$, i.e., $x \in (f^{-1}(B))^c$. Since this holds for all $x$, the sets are equal [@problem_id:2301735]. This reliable behavior makes preimages a cornerstone of topology, where the [continuity of a function](@entry_id:147842) is defined by the property that the [preimage](@entry_id:150899) of any open set is open.

**Properties of Images:**
The image operator does not share the same universal compatibility with [set operations](@entry_id:143311).
*   **Union:** The image operator distributes over unions: $f(\bigcup_{i \in I} A_i) = \bigcup_{i \in I} f(A_i)$. An element $y$ is in the image of the union if and only if it's the image of some $x$ in the union, which means $x$ must be in at least one $A_i$, and thus $y$ is in the image of at least one $f(A_i)$.
*   **Intersection:** For intersections, we only have a guaranteed inclusion: $f(A_1 \cap A_2) \subseteq f(A_1) \cap f(A_2)$. The reason equality may fail is that a point $y$ could be in $f(A_1) \cap f(A_2)$ without arising from an element in $A_1 \cap A_2$. This happens if $y = f(x_1)$ and $y = f(x_2)$ for some $x_1 \in A_1$ and a *different* point $x_2 \in A_2$. If $x_1$ and $x_2$ are distinct, then there is no single point in the intersection $A_1 \cap A_2$ that maps to $y$.
    For a concrete example, let $f(x) = (x-1)^2$, with $A = [0, 3]$ and $B = [-2, 2]$. The intersection is $A \cap B = [0, 2]$, whose image is $f([0,2]) = [0, 1]$. However, the individual images are $f(A) = [0, 4]$ and $f(B) = [0, 9]$. Their intersection is $f(A) \cap f(B) = [0, 4]$. Clearly, $f(A \cap B) = [0,1]$ is a [proper subset](@entry_id:152276) of $f(A) \cap f(B) = [0,4]$. The [set difference](@entry_id:140904) $(1, 4]$ exists because values like $y=4$ are in the intersection of the images (since $f(3)=4$ and $f(-1)=4$), but the preimages $3$ and $-1$ are not both in $A \cap B$ [@problem_id:2301729].

**Compositions of Image and Preimage:**
Finally, we consider the composition of [image and preimage](@entry_id:148315) operations. Two fundamental relations are always true:
1.  $A \subseteq f^{-1}(f(A))$ for any $A \subseteq X$.
    If $x \in A$, then by definition $f(x) \in f(A)$. And by the definition of preimage, any element that maps into $f(A)$ must belong to $f^{-1}(f(A))$. Therefore, $x \in f^{-1}(f(A))$. This inclusion is an equality if and only if $f$ is injective.
2.  $f(f^{-1}(B)) \subseteq B$ for any $B \subseteq Y$.
    If $y \in f(f^{-1}(B))$, then $y = f(x)$ for some $x \in f^{-1}(B)$. By definition of [preimage](@entry_id:150899), this means $f(x)$ must be an element of $B$. Therefore, $y \in B$. This inclusion becomes an equality, $f(f^{-1}(B)) = B$, if and only if $B$ is a subset of the function's range, $B \subseteq f(X)$ [@problem_id:2301735].

### Deeper Connections: Characterizing Functions

The ways in which a function interacts with [set operations](@entry_id:143311) can serve to define the function's core properties. This provides a more abstract and powerful lens through which to understand concepts like injectivity and continuity.

A striking example is the relationship between [injectivity](@entry_id:147722) and the preservation of intersections. As we saw, the inclusion $f(\bigcap A_i) \subseteq \bigcap f(A_i)$ holds for any function. The reverse inclusion, $\bigcap f(A_i) \subseteq f(\bigcap A_i)$, is not generally true. It turns out that this reverse inclusion holding for all collections of subsets $\{A_i\}$ is a condition *equivalent* to the function being injective. Therefore, a function $f$ is injective if and only if $f(\bigcap A_i) = \bigcap f(A_i)$ for any collection of subsets $\{A_i\}$ of its domain. The failure of intersection preservation is a direct consequence of multiple domain points collapsing to a single image point [@problem_id:2301757].

An even deeper connection exists between topology and set mappings. We know that a function $f: \mathbb{R} \to \mathbb{R}$ is continuous if and only if the [preimage](@entry_id:150899) of every [closed set](@entry_id:136446) is closed. A different property is that of being a **[closed map](@entry_id:150357)**, where the *image* of every [closed set](@entry_id:136446) is closed. What if a function has both of these properties, and their converses? That is, what can we say about a function $f: \mathbb{R} \to \mathbb{R}$ for which the statement "$A$ is a [closed set](@entry_id:136446)" is *equivalent* to "$f(A)$ is a [closed set](@entry_id:136446)" for any subset $A \subseteq \mathbb{R}$?

Such a function must be a **[homeomorphism](@entry_id:146933)**—a [continuous bijection](@entry_id:198258) whose inverse is also continuous. The argument is revealing:
1.  The condition implies $f$ is continuous (since $f^{-1}(B)$ must be closed for any closed set $B$).
2.  The condition also states directly that $f$ is a [closed map](@entry_id:150357).
3.  A continuous, [closed map](@entry_id:150357) between nice spaces like $\mathbb{R}$ must be either constant or surjective. Combined with the forward implication ($A$ closed $\implies f(A)$ closed), we can show it cannot be constant, and in fact must be a [bijection](@entry_id:138092). A non-[injective function](@entry_id:141653) would lead to contradictions when considering sets like $A=\mathbb{R} \setminus \{x_2\}$ where $f(x_1)=f(x_2)$.
4.  A [continuous bijection](@entry_id:198258) from $\mathbb{R}$ to $\mathbb{R}$ is a strictly [monotone function](@entry_id:637414) whose range is all of $\mathbb{R}$. Such a function is a [homeomorphism](@entry_id:146933).
Conversely, any homeomorphism from $\mathbb{R}$ to $\mathbb{R}$ satisfies the condition. This characterization represents a pinnacle of understanding, linking the point-wise properties of a function to its global behavior on the entire topology of its domain and codomain [@problem_id:2301740].