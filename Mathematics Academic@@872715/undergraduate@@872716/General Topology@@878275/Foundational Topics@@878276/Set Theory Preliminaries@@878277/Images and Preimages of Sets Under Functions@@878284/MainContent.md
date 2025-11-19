## Introduction
When studying functions, we often begin by considering how they map individual elements from a domain to a codomain. However, to unlock deeper insights in fields like topology and analysis, we must shift our perspective from single points to entire sets of points. This raises a fundamental question: how do functions transform subsets, and what properties of the function are revealed by this transformation? The concepts of the **image** and **[preimage](@entry_id:150899)** of a set provide the [formal language](@entry_id:153638) to answer this question, forming a cornerstone of modern mathematics.

This article provides a comprehensive exploration of these crucial tools. The first chapter, **Principles and Mechanisms**, establishes the rigorous definitions of [image and preimage](@entry_id:148315) and systematically investigates their interactions with [set operations](@entry_id:143311), revealing how they characterize function properties such as [injectivity and surjectivity](@entry_id:262885). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of these concepts beyond pure theory, showing their role in the geometric analysis of functions, the definition of [continuity in topology](@entry_id:155799), and as a modeling framework in various scientific fields. Finally, **Hands-On Practices** will offer a series of guided problems to solidify your understanding and build practical problem-solving skills. By progressing through these sections, you will gain a robust command of how to use images and preimages to analyze functions and the spaces they connect.

## Principles and Mechanisms

In our exploration of functions as mappings between sets, we move from considering the action of a function on individual elements to its effect on entire subsets of the domain and [codomain](@entry_id:139336). This perspective is foundational to many areas of higher mathematics, particularly in topology and analysis, where the properties of spaces are often studied by observing how they are transformed by functions. The core tools for this analysis are the concepts of **image** and **[preimage](@entry_id:150899)** of a set. This chapter will define these concepts rigorously and systematically explore their fundamental properties, especially in relation to [set operations](@entry_id:143311) such as union, intersection, and complement.

### Fundamental Definitions: Image and Preimage

A function $f: X \to Y$ establishes a clear correspondence from each element of the domain $X$ to a single element in the codomain $Y$. We can extend this correspondence to operate on collections of points, or subsets.

The **image** of a subset $A \subseteq X$ under a function $f$, denoted $f(A)$, is the set of all values in the [codomain](@entry_id:139336) $Y$ that are the image of at least one element from $A$. Formally, the definition is:

$$f(A) = \{y \in Y \mid \text{there exists some } x \in A \text{ such that } f(x) = y\}$$

Alternatively, and more compactly, we can write $f(A) = \{f(x) \mid x \in A\}$. The image of the entire domain, $f(X)$, is commonly called the **range** of the function.

Conversely, we can ask which elements of the domain $X$ are mapped into a specific subset of the [codomain](@entry_id:139336) $Y$. This leads to the concept of the preimage. The **preimage** (or **[inverse image](@entry_id:154161)**) of a subset $B \subseteq Y$ under a function $f$, denoted $f^{-1}(B)$, is the set of all elements in the domain $X$ that map to an element within $B$. Formally:

$$f^{-1}(B) = \{x \in X \mid f(x) \in B\}$$

It is crucial to recognize that the notation $f^{-1}(B)$ does not imply that the function $f$ has an [inverse function](@entry_id:152416), $f^{-1}$. The preimage is defined for any function, regardless of whether it is invertible. The symbol $f^{-1}$ in this context is an operator on subsets of the codomain, not a function on elements of the codomain.

To make these definitions concrete, let us consider a function defined on a discrete domain. Suppose we have a set $S = \{-2, -1, 0, 1, 2\}$ and a function $f: S \times S \to \mathbb{Z}$ defined by the rule $f(x, y) = |x - 2y|$. Let's find the image of the subset $A = \{(x, y) \in S \times S \mid x + y = 0\}$ and the [preimage](@entry_id:150899) of the subset $B = \{1, 3\} \subseteq \mathbb{Z}$.

First, we identify the elements of $A$: the pairs $(x,y)$ in $S \times S$ where $y = -x$. These are $A = \{(-2, 2), (-1, 1), (0, 0), (1, -1), (2, -2)\}$. To find the image $f(A)$, we apply the function to each element of $A$:
- $f(-2, 2) = |-2 - 2(2)| = |-6| = 6$
- $f(-1, 1) = |-1 - 2(1)| = |-3| = 3$
- $f(0, 0) = |0 - 2(0)| = 0$
- $f(1, -1) = |1 - 2(-1)| = |3| = 3$
- $f(2, -2) = |2 - 2(-2)| = |6| = 6$

Collecting these output values, we obtain the image set: $f(A) = \{0, 3, 6\}$.

Next, we find the [preimage](@entry_id:150899) $f^{-1}(B) = f^{-1}(\{1, 3\})$. We need to find all pairs $(x,y) \in S \times S$ such that $f(x,y) = |x - 2y|$ is either $1$ or $3$. This is equivalent to finding all $(x,y)$ where $x - 2y \in \{-3, -1, 1, 3\}$. We can systematically test each possible value of $y \in S$ to find the corresponding valid values of $x \in S$ [@problem_id:1375385]. For instance, if $y = -1$, we need $x - 2(-1) = x+2$ to be in $\{-3, -1, 1, 3\}$. This means $x$ would have to be in $\{-5, -3, -1, 1\}$. The values that are also in $S$ are $-1$ and $1$. So, the pairs $(-1, -1)$ and $(1, -1)$ are in the [preimage](@entry_id:150899). Continuing this process for all $y \in S$ yields the complete set:
$$f^{-1}(\{1, 3\}) = \{(-1, -2), (-1, -1), (1, -1), (-1, 0), (1, 0), (-1, 1), (1, 1), (1, 2)\}$$

The same principles apply to functions on continuous domains. Consider the function $f: [0, 4] \to \mathbb{R}$ given by $f(x) = \cos(\pi x)$. To determine the [preimage](@entry_id:150899) of the interval $A = [\frac{1}{2}, 1]$, we must find all $x \in [0, 4]$ such that $f(x) \in [\frac{1}{2}, 1]$. This translates to the inequality $\frac{1}{2} \le \cos(\pi x) \le 1$. Since the maximum value of cosine is $1$, we only need to solve $\cos(\pi x) \ge \frac{1}{2}$.

Let $t = \pi x$. As $x$ varies in $[0, 4]$, $t$ varies in $[0, 4\pi]$. The inequality becomes $\cos(t) \ge \frac{1}{2}$. We know that $\cos(t) = \frac{1}{2}$ for $t = \frac{\pi}{3} + 2\pi k$ and $t = -\frac{\pi}{3} + 2\pi k$ for any integer $k$. In the interval $[0, 4\pi]$, the solution to $\cos(t) \ge \frac{1}{2}$ is the union of the intervals $[0, \frac{\pi}{3}]$, $[\frac{5\pi}{3}, \frac{7\pi}{3}]$, and $[\frac{11\pi}{3}, 4\pi]$. Converting back to $x$ by dividing by $\pi$, we find the preimage:
$$f^{-1}\left(\left[\frac{1}{2}, 1\right]\right) = \left[0, \frac{1}{3}\right] \cup \left[\frac{5}{3}, \frac{7}{3}\right] \cup \left[\frac{11}{3}, 4\right]$$
This example [@problem_id:1558100] illustrates that the [preimage](@entry_id:150899) of a simple connected interval can be a [disconnected set](@entry_id:158535), reflecting the periodic nature of the function.

### Interaction with Set Operations: A Tale of Two Operators

A deep understanding of [image and preimage](@entry_id:148315) comes from studying their interaction with [set operations](@entry_id:143311). We will find that the preimage operator exhibits a remarkable consistency and "good behavior," while the image operator's behavior is more nuanced and often reveals key properties of the function itself.

#### The Preimage Operator: A Model of Consistency

The [preimage](@entry_id:150899) operator commutes gracefully with union, intersection, and complementation. For any function $f: X \to Y$ and any subsets $C, D \subseteq Y$:

1.  **Union**: $f^{-1}(C \cup D) = f^{-1}(C) \cup f^{-1}(D)$
2.  **Intersection**: $f^{-1}(C \cap D) = f^{-1}(C) \cap f^{-1}(D)$
3.  **Complement**: $f^{-1}(D^c) = (f^{-1}(D))^c$

The proofs for these identities are elegant exercises in definition-chasing. For instance, let's prove the complement property, which is particularly vital in topology. An element $x \in X$ belongs to $f^{-1}(D^c)$ if and only if $f(x) \in D^c$. This is true if and only if $f(x) \notin D$. By definition of preimage, this is equivalent to $x \notin f^{-1}(D)$, which in turn is equivalent to $x \in (f^{-1}(D))^c$. Since this chain of equivalences holds for any arbitrary $x \in X$, the sets must be equal: $f^{-1}(D^c) = (f^{-1}(D))^c$ [@problem_id:2301735].

Let's verify the intersection property with an example. Let $f: \mathbb{R} \to \mathbb{R}$ be $f(x) = |x|$, and consider the [codomain](@entry_id:139336) subsets $C = [-3, 1]$ and $D = [-1, 2]$.
First, we compute the left-hand side: $L = f^{-1}(C \cap D)$. The intersection is $C \cap D = [-1, 1]$. The [preimage](@entry_id:150899) is therefore $L = f^{-1}([-1, 1]) = \{x \in \mathbb{R} \mid |x| \in [-1, 1]\}$. Since $|x|$ is always non-negative, this simplifies to $0 \le |x| \le 1$, which corresponds to the interval $L = [-1, 1]$.
Now, for the right-hand side: $R = f^{-1}(C) \cap f^{-1}(D)$. We find the individual preimages first:
$f^{-1}(C) = f^{-1}([-3, 1]) = \{x \in \mathbb{R} \mid |x| \in [-3, 1]\} = \{x \in \mathbb{R} \mid |x| \le 1\} = [-1, 1]$.
$f^{-1}(D) = f^{-1}([-1, 2]) = \{x \in \mathbb{R} \mid |x| \in [-1, 2]\} = \{x \in \mathbb{R} \mid |x| \le 2\} = [-2, 2]$.
The intersection of these preimages is $R = [-1, 1] \cap [-2, 2] = [-1, 1]$.
As expected, $L=R$, confirming the general identity for this specific case [@problem_id:1558084].

This predictable behavior makes the preimage operator a powerful tool. For instance, in topology, the [continuity of a function](@entry_id:147842) is defined by the property that the preimage of every open set is open. The fact that preimage commutes with unions and intersections is what allows this definition to be both powerful and tractable.

#### The Image Operator: A More Nuanced Behavior

In contrast to the preimage, the image operator's relationship with [set operations](@entry_id:143311) is more complex. While it distributes over unions, its interaction with intersection and complement is not as straightforward and depends critically on the function's properties.

1.  **Union**: For any subsets $A, B \subseteq X$, it is always true that $f(A \cup B) = f(A) \cup f(B)$.
    The proof is a direct application of the definitions. An element $y$ is in $f(A \cup B)$ if and only if it is the image of some $x \in A \cup B$. This is true if and only if $x \in A$ or $x \in B$, which is equivalent to $y \in f(A)$ or $y \in f(B)$. This, in turn, is equivalent to $y \in f(A) \cup f(B)$.

2.  **Intersection**: For intersection, the equality breaks down. Only an inclusion is guaranteed to hold for any function:
    $$f(A \cap B) \subseteq f(A) \cap f(B)$$
    This holds because if $y \in f(A \cap B)$, then $y = f(x)$ for some $x$ that is in both $A$ and $B$. Therefore, $y$ is an image of an element of $A$ (so $y \in f(A)$) and $y$ is an image of an element of $B$ (so $y \in f(B)$). Thus, $y \in f(A) \cap f(B)$.

    The reverse inclusion, $f(A) \cap f(B) \subseteq f(A \cap B)$, is not generally true. An element $y$ can be in $f(A) \cap f(B)$ without being in $f(A \cap B)$. This happens if $y$ is the image of an element $x_1 \in A$ and also the image of a *different* element $x_2 \in B$, where neither $x_1$ nor $x_2$ is in the intersection $A \cap B$. This situation is precisely what occurs when a function is not **injective** (one-to-one).

    Consider the function $f(x) = x^2$ on $\mathbb{R}$, with $A = [-2, 1]$ and $B = [-1, 2]$ [@problem_id:1558085].
    -   $A \cap B = [-1, 1]$, so $f(A \cap B) = f([-1, 1]) = [0, 1]$.
    -   $f(A) = f([-2, 1]) = [0, 4]$.
    -   $f(B) = f([-1, 2]) = [0, 4]$.
    -   $f(A) \cap f(B) = [0, 4] \cap [0, 4] = [0, 4]$.
    Here, we see that $f(A \cap B) = [0, 1]$ is a [proper subset](@entry_id:152276) of $f(A) \cap f(B) = [0, 4]$. For example, the value $4$ is in $f(A) \cap f(B)$ because $4 = f(-2)$ with $-2 \in A$ and $4=f(2)$ with $2 \in B$. However, there is no single element $x$ in the intersection $A \cap B = [-1, 1]$ such that $f(x) = 4$.

    A simpler discrete example makes the point even more sharply. Let $f(x) = |x|$ on $\mathbb{Z}$, with $A = \{-3, -1, 5\}$ and $B = \{1, 3, 4\}$ [@problem_id:1558047].
    -   $A \cap B = \emptyset$, so $f(A \cap B) = f(\emptyset) = \emptyset$.
    -   $f(A) = \{f(-3), f(-1), f(5)\} = \{3, 1, 5\}$.
    -   $f(B) = \{f(1), f(3), f(4)\} = \{1, 3, 4\}$.
    -   $f(A) \cap f(B) = \{1, 3, 5\} \cap \{1, 3, 4\} = \{1, 3\}$.
    Here, $f(A \cap B) = \emptyset \neq \{1, 3\} = f(A) \cap f(B)$. The discrepancy arises because $f(-1) = 1 = f(1)$ and $f(-3) = 3 = f(3)$, but the preimages $(-1, 1)$ and $(-3, 3)$ are split between the [disjoint sets](@entry_id:154341) $A$ and $B$.

    This observation leads to a profound characterization of [injectivity](@entry_id:147722). A function $f$ is injective if and only if it preserves intersections for all subsets of its domain. More formally, for a function $f: X \to Y$, the following are equivalent [@problem_id:2301757]:
    a. $f$ is injective.
    b. For any collection of subsets $\{A_i\}_{i \in I}$ of $X$, $f\left(\bigcap_{i \in I} A_i\right) = \bigcap_{i \in I} f(A_i)$.

3.  **Complement**: The relationship between the image of a complement, $f(A^c)$, and the complement of an image, $(f(A))^c$, is the most intricate. In general, there is no guaranteed inclusion in either direction. For example, if $f: \{1, 2\} \to \{a\}$ is a constant function and $A = \{1\}$, then $A^c = \{2\}$. We have $f(A^c) = \{a\}$ but $(f(A))^c = (\{a\})^c = \emptyset$. In this case, $(f(A))^c \subset f(A^c)$.

    However, a specific inclusion holds universally if and only if the function has a certain property. A function $f: X \to Y$ is **surjective** (onto) if and only if for every subset $A \subseteq X$, the following inclusion holds:
    $$f(A)^c \subseteq f(A^c)$$
    To see why this is true, first assume $f$ is surjective. Let $y \in f(A)^c$. This means $y \in Y$ and $y \notin f(A)$. Since $f$ is surjective, there must be some $x \in X$ such that $f(x) = y$. This $x$ cannot be in $A$, because if it were, $y$ would be in $f(A)$. Therefore, $x$ must be in $A^c$. But if $x \in A^c$, then its image, $y$, must be in $f(A^c)$. Thus, $f(A)^c \subseteq f(A^c)$.
    Conversely, to prove necessity, assume the inclusion holds for all $A \subseteq X$. Let us choose the specific set $A = \emptyset$. Then $f(A) = f(\emptyset) = \emptyset$, and its complement is $(f(A))^c = Y$. The set $A^c$ is $X \setminus \emptyset = X$. The inclusion becomes $Y \subseteq f(X)$. Since $f(X)$ is by definition a subset of $Y$, this implies $Y = f(X)$, which is the definition of [surjectivity](@entry_id:148931) [@problem_id:1558035].

    The [logistic function](@entry_id:634233) $f(x) = \frac{10}{1 + \exp(-x)}$ from a sensor problem provides a good practical context [@problem_id:1558054]. Its range is $(0, 10)$, so it is not surjective onto $\mathbb{R}$. As shown in the problem, for the "normal" range of inputs $A = [-\ln(9), \ln(9)]$, the image is $f(A) = [1, 9]$. The image of the complement is $f(A^c) = (0, 1) \cup (9, 10)$. The complement of the image is $(f(A))^c = (-\infty, 1) \cup (9, \infty)$. We can see that $f(A)^c$ is not a subset of $f(A^c)$, as required for a non-[surjective function](@entry_id:147405). For example, $11 \in (f(A))^c$ but $11 \notin f(A^c)$ because $11$ is outside the function's range.

### Compositional Properties: Image and Preimage

Finally, we examine the properties that arise from composing the [image and preimage](@entry_id:148315) operations. What happens when we take the image of a set and then its [preimage](@entry_id:150899), or vice versa?

#### From Domain to Codomain and Back: The set $f^{-1}(f(A))$

For any function $f: X \to Y$ and any subset $A \subseteq X$, the following inclusion always holds:
$$A \subseteq f^{-1}(f(A))$$
This is straightforward to prove [@problem_id:2301735]: for any $x \in A$, its image $f(x)$ is, by definition, in $f(A)$. But if $f(x) \in f(A)$, then by the definition of preimage, $x$ must belong to $f^{-1}(f(A))$.

When does this inclusion become a strict one? The set $f^{-1}(f(A))$ contains *all* points in the domain that map into the set $f(A)$. If $f$ is not injective, there may be points $x' \notin A$ that map to the same values as points in $A$. These points $x'$ will be "pulled into" the set $f^{-1}(f(A))$, making it larger than $A$.

Consider a function $f: \{1, 2, 3, 4, 5\} \to \{\alpha, \beta, \gamma, \delta\}$ defined by $f(1)=\alpha, f(2)=\beta, f(3)=\alpha, f(4)=\gamma, f(5)=\gamma$. Let $A = \{1, 2\}$.
First, we find the image of $A$: $f(A) = \{f(1), f(2)\} = \{\alpha, \beta\}$.
Next, we find the preimage of this resulting set: $f^{-1}(f(A)) = f^{-1}(\{\alpha, \beta\})$. We must find all elements in the domain that map to either $\alpha$ or $\beta$. Looking at the function's definition, these are $f(1)=\alpha$, $f(2)=\beta$, and $f(3)=\alpha$.
Thus, $f^{-1}(f(A)) = \{1, 2, 3\}$.
In this case, $A = \{1, 2\}$ is a [proper subset](@entry_id:152276) of $f^{-1}(f(A)) = \{1, 2, 3\}$ [@problem_id:1797410]. The element $3$ is included because its image, $\alpha$, is also the image of an element in $A$ (namely, $1$).

This leads to another characterization of [injectivity](@entry_id:147722): a function $f$ is injective if and only if $f^{-1}(f(A)) = A$ for every subset $A$ of its domain.

#### From Codomain to Domain and Back: The set $f(f^{-1}(B))$

When we apply the operators in the reverse order, a different inclusion holds. For any function $f: X \to Y$ and any subset $B \subseteq Y$:
$$f(f^{-1}(B)) \subseteq B$$
The proof is again direct: if $y \in f(f^{-1}(B))$, then $y = f(x)$ for some $x \in f^{-1}(B)$. By definition of preimage, $x \in f^{-1}(B)$ means that $f(x) \in B$. Since $y=f(x)$, it follows that $y \in B$.

This time, equality fails if the set $B$ contains elements that are not in the **range** of $f$. The [preimage](@entry_id:150899) $f^{-1}(B)$ only captures domain elements that map into $B$. If a point $y \in B$ has no preimage at all (i.e., $y$ is not in the range $f(X)$), then it cannot possibly be in the set $f(f^{-1}(B))$, which by definition only contains images of points. This gives us the precise identity:
$$f(f^{-1}(B)) = B \cap f(X)$$
That is, the round trip from [codomain](@entry_id:139336) to domain and back filters the original set $B$ through the range of the function [@problem_id:2301735].

For example, let $f: \mathbb{R} \to \mathbb{R}$ be $f(x) = x^2$, so its range is $f(\mathbb{R}) = [0, \infty)$. Let $B = [-1, 4]$.
-   The [preimage](@entry_id:150899) is $f^{-1}(B) = f^{-1}([-1, 4]) = \{x \mid x^2 \in [-1, 4]\} = \{x \mid 0 \le x^2 \le 4\} = [-2, 2]$.
-   The image of this preimage is $f(f^{-1}(B)) = f([-2, 2]) = [0, 4]$.
Here, $f(f^{-1}(B)) = [0, 4]$ is a [proper subset](@entry_id:152276) of $B = [-1, 4]$. The negative part of $B$ was lost because it lies outside the range of $f(x)=x^2$. Notice that $[0, 4] = [-1, 4] \cap [0, \infty) = B \cap f(X)$.

From this identity, it follows immediately that $f(f^{-1}(B)) = B$ for all subsets $B \subseteq Y$ if and only if the function $f$ is surjective ($f(X)=Y$). This provides our final characterization, a neat dual to the one for injectivity.

In summary, the seemingly simple operations of forming images and preimages of sets are deeply intertwined with the fundamental properties of functions. The "well-behaved" nature of preimages makes them a cornerstone of topology, while the more complex behavior of images provides powerful criteria for classifying functions as injective or surjective.