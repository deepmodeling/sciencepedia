## Introduction
The mathematical study of symmetry is formalized through the concept of a [group action](@entry_id:143336), which describes how a group of transformations acts upon a set. A fundamental question within this framework is: what remains unchanged? The answer lies in the study of fixed points—elements that are invariant under these transformations. While seemingly simple, the concept of a fixed point is incredibly powerful, offering a key to unlock the deeper structure of groups, the sets they act upon, and the nature of symmetry itself. This article delves into the theory and application of fixed points, addressing the challenge of identifying and interpreting these points of invariance. To provide a comprehensive understanding, our exploration is divided into three parts. We will begin in the **Principles and Mechanisms** chapter by establishing the formal definitions and core properties of fixed points. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the remarkable utility of this concept across algebra, geometry, physics, and more. Finally, you will apply your knowledge directly in the **Hands-On Practices** section, solving concrete problems that reinforce these theoretical ideas.

## Principles and Mechanisms

In the study of [group actions](@entry_id:268812), which formalize the concept of symmetry, one of the most fundamental questions we can ask is: what remains unchanged? The elements of a set that are not moved by a [group action](@entry_id:143336), or by specific elements within the group, are known as **fixed points**. These points of invariance are not merely passive bystanders; they often hold the key to understanding the structure of the group, the set being acted upon, and the action itself. This chapter explores the principles governing fixed points, from their basic definition to the mechanisms that reveal their deeper structural significance.

### The Definition of a Fixed Point

Let us begin with the foundational concepts. A [group action](@entry_id:143336) of a group $G$ on a set $X$ is a map from $G \times X$ to $X$, denoted $(g, x) \mapsto g \cdot x$, that satisfies certain axioms. The core idea is that each element of the group $g$ corresponds to a permutation of the set $X$.

#### Fixed Points of a Single Group Element

For a specific element $g \in G$, a point $x_0 \in X$ is called a **fixed point** of $g$ if the action of $g$ on $x_0$ leaves it unmoved. Formally, this condition is:

$$ g \cdot x_0 = x_0 $$

The set of all points in $X$ that are fixed by a particular element $g$ is denoted by $X^g$.

$$ X^g = \{x \in X \mid g \cdot x = x\} $$

This set $X^g$ can be empty, contain a single element, or comprise many elements, depending on the group, the set, and the specific element $g$.

Consider, for instance, the group $G = \{-1, 1\}$ acting on the vector space $X = M_2(\mathbb{R})$ of $2 \times 2$ real matrices by [scalar multiplication](@entry_id:155971) [@problem_id:1619071]. To find the fixed points of the element $g = -1$, we seek all matrices $A \in M_2(\mathbb{R})$ such that $(-1)A = A$. This equation simplifies to $-A = A$, or $2A = 0$. In the vector space of real matrices, this implies that $A$ must be the [zero matrix](@entry_id:155836). Thus, for this action, the set of fixed points for the element $-1$ is $X^{-1} = \left\{ \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix} \right\}$. The identity element $1 \in G$, by contrast, fixes every matrix in $M_2(\mathbb{R})$, so $X^1 = M_2(\mathbb{R})$.

The existence of fixed points is not guaranteed for every non-identity element. Consider a group $G$ of transformations acting on the set of real numbers $X = \mathbb{R}$ [@problem_id:1619047]. The elements of $G$ are pairs $(s, t)$ with $s \in \{-1, 1\}$ and $t \in \mathbb{R}$, and the action is defined as $(s, t) \cdot x = sx + t$. Let's analyze the fixed points of a non-[identity element](@entry_id:139321) $g = (s, t)$. The fixed point equation is $sx + t = x$, which can be rewritten as $(s-1)x = -t$.
- If $s=1$, the element $g=(1,t)$ with $t \neq 0$ represents a pure translation. The equation becomes $0 \cdot x = -t$, which has no solution. Thus, a non-identity translation has no fixed points.
- If $s=-1$, the element $g=(-1,t)$ represents a reflection followed by a translation. The equation becomes $-2x = -t$, which has the unique solution $x = t/2$. Every such element has exactly one fixed point.

This example demonstrates that the nature of the fixed-point set is intrinsically tied to the algebraic properties of the group element performing the action.

Fixed-point sets can also possess a rich geometric structure. Let the symmetric group $S_3$ act on the Euclidean space $\mathbb{R}^3$ by permuting the coordinates of a vector $\mathbf{v} = (v_1, v_2, v_3)$ according to the rule $\sigma \cdot \mathbf{v} = (v_{\sigma^{-1}(1)}, v_{\sigma^{-1}(2)}, v_{\sigma^{-1}(3)})$ [@problem_id:1619054]. Let's find the fixed points of the cyclic permutation $\rho = (1, 2, 3)$. Its inverse is $\rho^{-1} = (1, 3, 2)$. The action is $\rho \cdot (v_1, v_2, v_3) = (v_{\rho^{-1}(1)}, v_{\rho^{-1}(2)}, v_{\rho^{-1}(3)}) = (v_3, v_1, v_2)$. A vector is a fixed point if $(v_1, v_2, v_3) = (v_3, v_1, v_2)$, which implies the system of equations $v_1 = v_3$, $v_2 = v_1$, and $v_3 = v_2$. The solution is $v_1 = v_2 = v_3$. The set of fixed points is therefore $\{(t, t, t) \mid t \in \mathbb{R}\}$, which is the main diagonal line in $\mathbb{R}^3$. Here, the algebraic condition of being a fixed point defines a geometric subspace.

### Fixed Points of a Group

While it is informative to study points fixed by a single element, the concept becomes even more powerful when we consider points fixed by an entire group or a subgroup.

#### The Set of Global Invariants

A point $x_0 \in X$ is a **fixed point of the group** $G$ if it is fixed by *every* element of $G$. The set of all such points, denoted $X^G$, represents the global invariants of the action.

$$ X^G = \{x \in X \mid g \cdot x = x \text{ for all } g \in G\} $$

This set can be expressed as the intersection of the fixed-point sets of all individual elements:

$$ X^G = \bigcap_{g \in G} X^g $$

A critical and highly practical principle arises from this definition: to determine if a point is fixed by a subgroup $H$, it is sufficient to check only if it is fixed by the generators of $H$. If $H = \langle g_1, g_2, \dots, g_k \rangle$, and $g_i \cdot x = x$ for all generators $g_i$, then any element $h \in H$ can be written as a product of these generators and their inverses. Since $g_i \cdot x = x$ implies $x = g_i^{-1} \cdot (g_i \cdot x) = g_i^{-1} \cdot x$, any combination of these operations will also fix $x$. For example, $(g_1 g_2) \cdot x = g_1 \cdot (g_2 \cdot x) = g_1 \cdot x = x$. This property dramatically simplifies the search for fixed points [@problem_id:1619086].

Let's apply this principle to an action by a subgroup of affine transformations on $\mathbb{R}$ [@problem_id:1619076]. Consider the group $G$ generated by $g_1(x) = 3x - 3$ and $g_2(x) = 5x - 6$. To find the points in $\mathbb{R}$ fixed by all elements of $G$, we need only find the points fixed by both generators simultaneously.
For $g_1$: $3x - 3 = x \implies 2x = 3 \implies x = 3/2$.
For $g_2$: $5x - 6 = x \implies 4x = 6 \implies x = 3/2$.
Since both generators fix the unique point $x_0 = 3/2$, this must be the unique fixed point for the entire group $G$.

In a different context, consider the [group of units](@entry_id:140130) modulo 8, $G = \{1, 3, 5, 7\}$, acting on the set $S = \{0, 1, \dots, 7\}$ by multiplication modulo 8 [@problem_id:1619049]. A fixed point $s \in S$ must satisfy $gs \equiv s \pmod{8}$ for all $g \in G$. This is equivalent to the [system of congruences](@entry_id:148057) $(g-1)s \equiv 0 \pmod{8}$ for $g \in \{1, 3, 5, 7\}$.
- For $g=3$: $2s \equiv 0 \pmod{8}$, which implies $s$ must be a multiple of 4. So $s \in \{0, 4\}$.
- For $g=5$: $4s \equiv 0 \pmod{8}$, which implies $s$ must be a multiple of 2. So $s \in \{0, 2, 4, 6\}$.
- For $g=7$: $6s \equiv 0 \pmod{8}$, which implies $3s \equiv 0 \pmod{4}$, so $s$ must be a multiple of 4. So $s \in \{0, 4\}$.
The intersection of all solution sets is $\{0, 4\}$. Thus, the set of points fixed by the entire group is $X^G = \{0, 4\}$.

### Structural Properties and Induced Actions

The concept of fixed points is deeply intertwined with other fundamental concepts of group theory, such as orbits, and it extends naturally to actions on more complex structures derived from the original set $X$.

#### Fixed Points and Orbits

Recall that the **orbit** of an element $x \in X$ is the set of all points that can be reached from $x$ by the action of group elements: $\text{Orb}_G(x) = \{g \cdot x \mid g \in G\}$. There is a direct and crucial relationship between orbits and fixed points:

An element $x \in X$ is a fixed point of the entire group $G$ if and only if its orbit has a size of 1.

The statement $|\text{Orb}_G(x)| = 1$ means that the set $\{g \cdot x \mid g \in G\}$ contains only one element. Since the [identity element](@entry_id:139321) $e$ is in $G$ and $e \cdot x = x$, this single element must be $x$ itself. Therefore, $g \cdot x = x$ for all $g \in G$, which is precisely the definition of $x$ being a fixed point of the group.

This equivalence provides an alternative lens for identifying fixed points. For example, let the [group of units](@entry_id:140130) modulo 20, $G = (\mathbb{Z}/20\mathbb{Z})^\times$, act on the set $X = \mathbb{Z}/20\mathbb{Z}$ by multiplication [@problem_id:1619085]. To find the elements with an orbit size of 1, we seek all $x \in X$ such that $gx \equiv x \pmod{20}$ for all $g \in G$. This is equivalent to finding the simultaneous solutions to $(g-1)x \equiv 0 \pmod{20}$ for all $g$ [relatively prime](@entry_id:143119) to 20. A careful analysis shows that this condition holds if and only if $x$ is a multiple of $\text{lcm}_{g \in G} \frac{20}{\gcd(20, g-1)}$. By calculating this [least common multiple](@entry_id:140942) over all $g \in G$, one finds it to be 10. Thus, the elements whose orbits have size 1 are the multiples of 10 in $X$, namely $\{0, 10\}$. The sum is $10$.

#### Induced Actions and Their Fixed Points

A [group action on a set](@entry_id:145041) $X$ can naturally induce an action on related, more complex sets, such as the [power set](@entry_id:137423) of $X$ (the set of all subsets of $X$) or a set of functions with domain $X$. The notion of a fixed point applies equally in these induced settings, often with subtle and important implications.

Consider an action on the set of all 2-element subsets of a set of vertices $V = \{v_0, \dots, v_5\}$ of a regular hexagon [@problem_id:1619089]. Let the group $\mathbb{Z}_6$ act on $V$ by rotation, where $k \in \mathbb{Z}_6$ sends $v_i$ to $v_{(i+k) \pmod{6}}$. This induces an action on pairs, where $k \cdot \{v_i, v_j\} = \{v_{(i+k) \pmod{6}}, v_{(j+k) \pmod{6}}\}$. Let's find the pairs fixed by the element $3 \in \mathbb{Z}_6$ (a 180-degree rotation). A pair $S = \{v_i, v_j\}$ is a fixed point if $3 \cdot S = S$, meaning $\{v_{i+3}, v_{j+3}\} = \{v_i, v_j\}$. This equality of sets holds if either the elements are individually fixed (e.g., $v_{i+3}=v_i$) or if they are swapped (e.g., $v_{i+3}=v_j$ and $v_{j+3}=v_i$). The first case is impossible, as $i+3 \equiv i \pmod{6}$ has no solution. The second case requires $j \equiv i+3 \pmod{6}$. This means the fixed pairs are precisely the main diagonals of the hexagon: $\{v_0, v_3\}$, $\{v_1, v_4\}$, and $\{v_2, v_5\}$. This illustrates a critical point: a set can be fixed under an action even if its individual elements are not.

Another important induced action is on a space of functions. Let $G$ act on a set $V$, and let $S$ be the set of all functions from $V$ to another set $C$. The action of $g \in G$ on a function $f \in S$ is defined to produce a new function $g \star f$ where $(g \star f)(v) = f(g^{-1} \cdot v)$ for all $v \in V$. A function $f$ is a fixed point of $g$ if $g \star f = f$. This condition translates to $f(g^{-1} \cdot v) = f(v)$ for all $v \in V$. Replacing $v$ with $g \cdot v$, we get the equivalent condition $f(v) = f(g \cdot v)$ for all $v \in V$. Iterating this implies that the function $f$ must take the same value on all elements within a single orbit of $V$ under the action of the subgroup generated by $g$.

For example, let $G = \mathbb{Z}_3$ act on $V = \{v_1, v_2, v_3\}$ by cyclic permutation, and consider functions from $V$ to $C = \{c_1, c_2\}$ [@problem_id:1619066]. The generator $g=[1] \in \mathbb{Z}_3$ permutes the elements of $V$ in a single cycle $v_1 \mapsto v_2 \mapsto v_3 \mapsto v_1$. The orbit of any element is the entire set $V$. For a function $f: V \to C$ to be fixed by $g$, it must be constant on this orbit. That is, $f(v_1) = f(v_2) = f(v_3)$. Since the codomain $C$ has two elements, there are exactly two such constant functions: one that maps all of $V$ to $c_1$, and one that maps all of $V$ to $c_2$.

### Symmetries of the Fixed-Point Set

Finally, we touch upon a more advanced topic that reveals the elegant recursive nature of symmetry in algebra. The set of fixed points $X^g$ is not merely a subset of $X$; it often inherits a symmetric structure of its own.

A remarkable principle is that the fixed-point set $X^g$ is itself acted upon by the **[centralizer](@entry_id:146604)** of $g$ in $G$. The [centralizer](@entry_id:146604), $C_G(g) = \{h \in G \mid hg = gh\}$, is the subgroup of elements in $G$ that commute with $g$. To see why $C_G(g)$ acts on $X^g$, take any $h \in C_G(g)$ and any $x \in X^g$. We must show that the point $h \cdot x$ is also fixed by $g$. We compute the action of $g$ on $h \cdot x$:
$$ g \cdot (h \cdot x) = (gh) \cdot x $$
Because $h$ is in the [centralizer](@entry_id:146604), $gh=hg$. So,
$$ (gh) \cdot x = (hg) \cdot x = h \cdot (g \cdot x) $$
And because $x$ is a fixed point of $g$, $g \cdot x = x$. Therefore,
$$ h \cdot (g \cdot x) = h \cdot x $$
We have shown that $g \cdot (h \cdot x) = h \cdot x$, which confirms that $h \cdot x$ is indeed in $X^g$. Thus, the action of any element of $C_G(g)$ maps the set $X^g$ to itself. This establishes a well-defined [group action](@entry_id:143336) of $C_G(g)$ on $X^g$.

This principle can be used to analyze the structure of $X^g$ by studying its [orbits and stabilizers](@entry_id:137467) under the action of the [centralizer](@entry_id:146604) [@problem_id:1619084]. Such investigations demonstrate that fixed points are not endpoints of analysis but gateways to a deeper understanding of the intricate web of symmetries governed by the laws of group theory.