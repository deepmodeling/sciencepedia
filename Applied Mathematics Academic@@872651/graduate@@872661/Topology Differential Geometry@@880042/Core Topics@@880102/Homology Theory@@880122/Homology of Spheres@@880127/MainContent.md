## Introduction
The [n-sphere](@entry_id:268045), $S^n$, stands as one of the most fundamental objects in geometry and topology. Its apparent simplicity belies a deep and rich structure, the understanding of which is crucial for the study of more complex spaces. A central goal in algebraic topology is to classify spaces using algebraic invariants, and the homology of the [n-sphere](@entry_id:268045) provides a foundational benchmark for this entire endeavor. This article addresses the core task of computing these homology groups and explores the far-reaching consequences of the result. It bridges the gap between abstract computation and concrete geometric insight, demonstrating why the homology of spheres is a cornerstone of the field.

The reader will embark on a journey through three distinct stages. The first chapter, **Principles and Mechanisms**, will establish the main result by presenting two classic computational approaches—suspension and the Mayer-Vietoris sequence—and explore its immediate consequences, such as the [degree of a map](@entry_id:158493) and the proof of Brouwer's Fixed-Point Theorem. The second chapter, **Applications and Interdisciplinary Connections**, will broaden our view, showcasing how the homology of spheres is used to analyze complex structures like [fiber bundles](@entry_id:154670), [product spaces](@entry_id:151693), and even informs topics in [differential geometry](@entry_id:145818) and group theory. Finally, the **Hands-On Practices** section will offer a series of guided problems designed to reinforce these theoretical concepts and build practical computational skills.

## Principles and Mechanisms

The $n$-dimensional sphere, $S^n$, is one of the most fundamental objects of study in topology. Its algebraic invariants, particularly its homology groups, serve as a benchmark and a foundational tool for a vast range of theories and applications. In this chapter, we will rigorously determine the homology of spheres and explore the profound consequences of this result, from the classification of spaces to the construction of more complex topological structures.

### The Foundational Result: Homology of the n-Sphere

The primary result that underpins this chapter is the computation of the [singular homology](@entry_id:158380) groups of the $n$-sphere, $S^n$, with integer coefficients ($\mathbb{Z}$). For $n \ge 1$, the unreduced homology groups are given by:
$$
H_k(S^n; \mathbb{Z}) \cong
\begin{cases}
\mathbb{Z}  \text{ if } k=0 \text{ or } k=n \\
0  \text{ otherwise}
\end{cases}
$$

The group $H_0(S^n; \mathbb{Z}) \cong \mathbb{Z}$ reflects the fact that $S^n$ is path-connected for $n \ge 1$. The most significant feature is the appearance of a single non-[trivial homology](@entry_id:265875) group in the dimension of the sphere itself, $H_n(S^n; \mathbb{Z}) \cong \mathbb{Z}$. This group is often called the **[fundamental class](@entry_id:158335)** or **orientation class** of the sphere.

For the special case of the $0$-sphere, $S^0$, which consists of two discrete points, the homology is:
$$
H_k(S^0; \mathbb{Z}) \cong
\begin{cases}
\mathbb{Z} \oplus \mathbb{Z}  \text{ if } k=0 \\
0  \text{ otherwise}
\end{cases}
$$

It is often more convenient to work with **[reduced homology](@entry_id:274187)**, $\tilde{H}_k(X)$, which is defined by the relation $H_k(X) \cong \tilde{H}_k(X) \oplus H_k(\text{point})$ for $k>0$, and $H_0(X) \cong \tilde{H}_0(X) \oplus \mathbb{Z}$ for a [path-connected space](@entry_id:156428) $X$. In essence, [reduced homology](@entry_id:274187) trivializes the homology of a point and eliminates the $H_0$ group for [path-connected spaces](@entry_id:152443). For all $n \ge 0$, the [reduced homology](@entry_id:274187) of the $n$-sphere is elegantly summarized as:
$$
\tilde{H}_k(S^n; \mathbb{Z}) \cong
\begin{cases}
\mathbb{Z}  \text{ if } k=n \\
0  \text{ otherwise}
\end{cases}
$$
This unified statement highlights the defining characteristic of a sphere: from the perspective of homology, it is a space that "exists" only in dimension $n$.

### Two Fundamental Computational Approaches

The computation of the homology of spheres can be approached in several ways, each illuminating a different aspect of [homological algebra](@entry_id:155139). We present two of the most classical and instructive methods.

#### The Inductive Approach: Suspension

The concept of **suspension** provides a powerful inductive tool for relating spheres of different dimensions. The suspension of a [topological space](@entry_id:149165) $X$, denoted $SX$, is formed by taking the cylinder $X \times [0,1]$ and collapsing the top lid $X \times \{1\}$ to a single point (the "north pole") and the bottom lid $X \times \{0\}$ to another point (the "south pole"). A crucial geometric fact is that the suspension of an $n$-sphere is homeomorphic to an $(n+1)$-sphere: $SS^n \cong S^{n+1}$.

This geometric construction has a direct algebraic counterpart in the **Suspension Isomorphism Theorem**, which states that for any non-empty space $X$, there is a [natural isomorphism](@entry_id:276379):
$$
\tilde{H}_{k+1}(SX) \cong \tilde{H}_k(X) \quad \text{for all } k \ge 0
$$

This theorem allows us to compute the homology of all spheres inductively, starting from the simplest case, $S^0$.
The [reduced homology](@entry_id:274187) of $S^0$ is known: $\tilde{H}_0(S^0) \cong \mathbb{Z}$, and $\tilde{H}_k(S^0) = 0$ for $k > 0$.

Now, we can proceed by induction. Let's compute the homology of $S^1$:
$$
\tilde{H}_k(S^1) \cong \tilde{H}_k(SS^0) \cong \tilde{H}_{k-1}(S^0)
$$
This isomorphism gives $\tilde{H}_1(S^1) \cong \tilde{H}_0(S^0) \cong \mathbb{Z}$, and $\tilde{H}_k(S^1) = 0$ for all $k \neq 1$.

Assuming we have established that $\tilde{H}_k(S^{n-1})$ is $\mathbb{Z}$ for $k=n-1$ and $0$ otherwise, we can compute the homology of $S^n$ using the relationship $S^n \cong SS^{n-1}$:
$$
\tilde{H}_k(S^n) \cong \tilde{H}_k(SS^{n-1}) \cong \tilde{H}_{k-1}(S^{n-1})
$$
By the [inductive hypothesis](@entry_id:139767), $\tilde{H}_{k-1}(S^{n-1})$ is non-trivial only when $k-1 = n-1$, which implies $k=n$. In this case, $\tilde{H}_n(S^n) \cong \tilde{H}_{n-1}(S^{n-1}) \cong \mathbb{Z}$. For all other values of $k$, the group is trivial. This completes the inductive proof, establishing the fundamental result for all spheres.

#### The Deconstructive Approach: Mayer-Vietoris Sequence

An alternative and equally powerful method for computing homology is the **Mayer-Vietoris sequence**, which embodies a "[divide and conquer](@entry_id:139554)" strategy. The central idea is to decompose a space $X$ into two open subsets, $U$ and $V$, such that $X = U \cup V$, and then relate the homology of $X$ to the homology of $U$, $V$, and their intersection $U \cap V$.

For the $n$-sphere $S^n$ (with $n \ge 1$), we can choose a decomposition that is particularly effective. Let $N$ and $S$ be the north and south poles of $S^n$, respectively. Define the open sets $U = S^n \setminus \{N\}$ and $V = S^n \setminus \{S\}$.
- The set $U$ is the sphere with one point removed. Via stereographic projection from the north pole, $U$ is homeomorphic to $\mathbb{R}^n$. Similarly, $V$ is homeomorphic to $\mathbb{R}^n$. Both $U$ and $V$ are therefore **contractible**. A contractible space has the homology of a point, which means its [reduced homology](@entry_id:274187) groups are all trivial: $\tilde{H}_k(U) \cong \tilde{H}_k(V) = 0$ for all $k \ge 0$.
- The intersection $U \cap V$ is the sphere with both poles removed. This space is homotopy equivalent to the equatorial $(n-1)$-sphere, $S^{n-1}$. Consequently, $\tilde{H}_k(U \cap V) \cong \tilde{H}_k(S^{n-1})$.

The reduced Mayer-Vietoris [long exact sequence](@entry_id:153438) for this decomposition is:
$$
\cdots \to \tilde{H}_k(U \cap V) \to \tilde{H}_k(U) \oplus \tilde{H}_k(V) \to \tilde{H}_k(S^n) \xrightarrow{\partial} \tilde{H}_{k-1}(U \cap V) \to \cdots
$$
Substituting the known homology groups for $U$ and $V$:
$$
\cdots \to \tilde{H}_k(S^{n-1}) \to 0 \oplus 0 \to \tilde{H}_k(S^n) \xrightarrow{\partial} \tilde{H}_{k-1}(S^{n-1}) \to 0 \oplus 0 \to \cdots
$$
From the [exactness](@entry_id:268999) of this sequence, the map from $\tilde{H}_k(S^{n-1})$ to $0$ must have its image as the kernel of the next map, so the map from $0$ to $\tilde{H}_k(S^n)$ is injective. Similarly, the map from $\tilde{H}_k(S^n)$ to $\tilde{H}_{k-1}(S^{n-1})$ must have its kernel as the image of the previous map (which is $0$), so it is injective. Finally, the map from $\tilde{H}_{k-1}(S^{n-1})$ to $0$ must be surjective. This chain of reasoning implies that the boundary map $\partial: \tilde{H}_k(S^n) \to \tilde{H}_{k-1}(S^{n-1})$ is an [isomorphism](@entry_id:137127) for all $k$.

This gives us the same recursive relationship as the [suspension isomorphism](@entry_id:156388): $\tilde{H}_k(S^n) \cong \tilde{H}_{k-1}(S^{n-1})$. Starting with the base case of $S^0$, this again yields the definitive result for the homology of all spheres.

### Immediate Consequences and Invariants

The simple and elegant structure of the homology of spheres has several profound and immediate consequences.

#### Distinguishing Spheres

A fundamental principle of algebraic topology is that homology is a **homotopy invariant**. This means that if two [topological spaces](@entry_id:155056) $X$ and $Y$ are homotopy equivalent, then their homology groups must be isomorphic, i.e., $H_k(X) \cong H_k(Y)$ for all $k$.

We can use this principle to prove that spheres of different dimensions are topologically distinct in a very strong sense. Consider two spheres, $S^k$ and $S^n$, where $k$ and $n$ are distinct positive integers. Let's examine their homology in dimension $k$. According to our result:
$$
H_k(S^k) \cong \mathbb{Z}
$$
However, since $k \neq n$, the $k$-th homology group of $S^n$ is:
$$
H_k(S^n) \cong 0
$$
Since $\mathbb{Z}$ is not isomorphic to the trivial group $0$, the homology groups of $S^k$ and $S^n$ are different. Therefore, $S^k$ and $S^n$ cannot be homotopy equivalent for $k \neq n$. This confirms our geometric intuition that a circle is fundamentally different from a 2-sphere, and so on.

#### Euler Characteristic of Spheres

The **Euler characteristic**, $\chi(X)$, is a numerical [topological invariant](@entry_id:142028) that can be computed from the Betti numbers of a space. The $k$-th Betti number, $b_k(X)$, is the rank of the $k$-th homology group $H_k(X; \mathbb{Z})$. The Euler characteristic is the alternating sum of these Betti numbers:
$$
\chi(X) = \sum_{k=0}^{\infty} (-1)^k b_k(X)
$$
For the $n$-sphere ($n \ge 1$), the only non-zero Betti numbers are $b_0(S^n)=1$ and $b_n(S^n)=1$. Therefore, its Euler characteristic is:
$$
\chi(S^n) = (-1)^0 b_0(S^n) + (-1)^n b_n(S^n) = 1 + (-1)^n
$$
This gives the familiar sequence $2, 0, 2, 0, \dots$ for $n=1, 2, 3, 4, \dots$.

The **reduced Euler characteristic**, $\tilde{\chi}(X)$, is defined using the ranks of the [reduced homology](@entry_id:274187) groups. For any space, $\chi(X) = \tilde{\chi}(X) + 1$. For the $n$-sphere ($n \ge 0$), there is only one non-trivial reduced Betti number, $\tilde{b}_n(S^n)=1$. This gives a much simpler expression:
$$
\tilde{\chi}(S^n) = \sum_{k=0}^{\infty} (-1)^k \tilde{b}_k(S^n) = (-1)^n \tilde{b}_n(S^n) = (-1)^n
$$

### The Degree of a Map: A Key Application

The fact that $H_n(S^n) \cong \mathbb{Z}$ for $n \ge 1$ is not just a classification tool; it enables the definition of one of the most important concepts in algebraic topology: the **degree** of a map.

#### Definition and Properties

Let $f: S^n \to S^n$ be a continuous map. By the [functoriality of homology](@entry_id:269512), this map induces a [group homomorphism](@entry_id:140603) on the $n$-th homology group:
$$
f_*: H_n(S^n; \mathbb{Z}) \to H_n(S^n; \mathbb{Z})
$$
Since $H_n(S^n; \mathbb{Z}) \cong \mathbb{Z}$, this is a homomorphism from $\mathbb{Z}$ to itself. Any such homomorphism must be of the form $x \mapsto d \cdot x$ for some unique integer $d$. This integer $d$ is defined as the **degree of the map** $f$, denoted $\deg(f)$.

Geometrically, the degree represents the number of times the domain sphere "wraps around" the target sphere, taking orientation into account. The degree has several crucial properties:
1.  **Identity Map**: The identity map has degree 1, $\deg(\text{id}_{S^n}) = 1$.
2.  **Composition**: For maps $f, g: S^n \to S^n$, the degree of their composition is the product of their degrees: $\deg(g \circ f) = \deg(g) \cdot \deg(f)$.
3.  **Homotopy Invariance**: If two maps $f$ and $g$ are homotopic, then they have the same degree, $\deg(f) = \deg(g)$.
4.  **Constant Maps**: Any constant map has degree 0.

#### Fundamental Examples

The power of the degree concept is best illustrated through examples.

A **reflection** of $S^n$ across a hyperplane in $\mathbb{R}^{n+1}$ is a map that reverses orientation. It can be shown that any such reflection has degree -1.

A particularly important map is the **[antipodal map](@entry_id:151775)**, $a: S^n \to S^n$, defined by $a(x) = -x$. We can view this map as a composition of $n+1$ reflections. For example, in $\mathbb{R}^{n+1}$, the map $(x_0, x_1, \dots, x_n) \mapsto (-x_0, -x_1, \dots, -x_n)$ can be written as the composition of the reflections $R_i(x_0, \dots, x_n) = (x_0, \dots, -x_i, \dots, x_n)$ for $i=0, \dots, n$. Using the composition property of degree, we can compute the degree of the [antipodal map](@entry_id:151775):
$$
\deg(a) = \deg(R_0 \circ R_1 \circ \cdots \circ R_n) = \prod_{i=0}^{n} \deg(R_i) = \prod_{i=0}^{n} (-1) = (-1)^{n+1}
$$
This result is highly significant. For even-dimensional spheres (like $S^2$), the [antipodal map](@entry_id:151775) has degree -1, while for odd-dimensional spheres (like $S^1$ or $S^3$), it has degree 1. This implies, for instance, that the [antipodal map](@entry_id:151775) on $S^2$ is not homotopic to the identity, whereas on $S^1$ it is (it's simply a rotation by $\pi$ [radians](@entry_id:171693)).

More complex linear maps can be analyzed by decomposing them into simpler operations. Consider the map $F: S^3 \to S^3$ given by $F(x_1, x_2, x_3, x_4) = (x_3, -x_4, -x_1, x_2)$. We can decompose $F$ into a permutation of coordinates followed by negations: $F = N \circ P$, where $P(x_1, x_2, x_3, x_4) = (x_3, x_4, x_1, x_2)$ and $N(y_1, y_2, y_3, y_4) = (y_1, -y_2, -y_3, y_4)$.
- The permutation $P$ swaps the pair $(x_1, x_2)$ with $(x_3, x_4)$. This can be achieved by two coordinate-pair swaps, each of which corresponds to an orientation-preserving transformation (a composition of two reflections, e.g., swapping $x_1$ and $x_3$ then $x_2$ and $x_4$). A more rigorous analysis shows this permutation is a rotation and is homotopic to the identity, thus $\deg(P)=1$.
- The negation map $N$ reflects across two hyperplanes ($y_2=0$ and $y_3=0$). Each reflection has degree -1. So, $\deg(N) = (-1) \cdot (-1) = 1$.
- Finally, the degree of the full map is $\deg(F) = \deg(N) \cdot \deg(P) = 1 \cdot 1 = 1$.

### Profound Consequences in Topology

The simple fact that $H_n(S^n) \neq 0$ is the linchpin for some of the most celebrated theorems in topology.

#### The Non-Retraction Theorem and Brouwer's Fixed-Point Theorem

A **retraction** is a [continuous map](@entry_id:153772) $r: X \to A$ from a space $X$ to a subspace $A \subseteq X$ such that the restriction of $r$ to $A$ is the identity map on $A$. A classic question is whether the $(n+1)$-dimensional [closed ball](@entry_id:157850) $D^{n+1}$ can be continuously retracted onto its boundary sphere $S^n$. Intuitively, this seems impossible—one cannot "squash" the entire ball onto its skin without tearing it—and homology provides a rigorous proof of this intuition.

Suppose, for the sake of contradiction, that such a retraction $r: D^{n+1} \to S^n$ exists. Let $i: S^n \to D^{n+1}$ be the standard inclusion map. The definition of a retraction means that the composition $r \circ i$ is the identity map on $S^n$.

Now, we apply the $n$-th homology functor to this sequence of maps:
$$
H_n(S^n) \xrightarrow{i_*} H_n(D^{n+1}) \xrightarrow{r_*} H_n(S^n)
$$
The functorial properties of homology dictate that $(r \circ i)_* = r_* \circ i_*$. Since $r \circ i = \text{id}_{S^n}$, the [induced map](@entry_id:271712) $(r \circ i)_*$ is the identity homomorphism on $H_n(S^n)$.

However, we know the homology of the spaces involved. The ball $D^{n+1}$ is contractible, so all its [reduced homology](@entry_id:274187) groups are trivial. In particular, for $n \ge 1$, $H_n(D^{n+1}) = 0$. This means the sequence of homomorphisms is:
$$
\mathbb{Z} \xrightarrow{i_*} 0 \xrightarrow{r_*} \mathbb{Z}
$$
Any homomorphism from a non-[trivial group](@entry_id:151996) to the [trivial group](@entry_id:151996) must be the zero map. And any homomorphism from the trivial group is also the zero map. Therefore, the composition $r_* \circ i_*$ must be the zero homomorphism.

This leads to a fundamental contradiction:
$$
\text{id}_{\mathbb{Z}} = (\text{id}_{S^n})_* = (r \circ i)_* = r_* \circ i_* = 0
$$
The identity map on the integers cannot be the zero map. Thus, our initial assumption must be false: no such retraction $r$ can exist.

This powerful result is a key ingredient in proving **Brouwer's Fixed-Point Theorem**, which states that any continuous function from a [closed ball](@entry_id:157850) to itself must have at least one fixed point.

### Spheres as Building Blocks

Beyond their intrinsic interest, spheres are the fundamental building blocks for a vast class of spaces known as CW complexes. Understanding how homology behaves when spheres are attached to each other or used to construct more complex spaces is crucial.

#### Relative Homology and Excision

Let us consider the pair $(S^n, S^{n-1})$, where $S^{n-1}$ is embedded as the equator of $S^n$. The **[long exact sequence of a pair](@entry_id:158857)** connects the homology of the space, the subspace, and their [relative homology](@entry_id:159348):
$$
\cdots \to H_k(S^{n-1}) \to H_k(S^n) \to H_k(S^n, S^{n-1}) \to H_{k-1}(S^{n-1}) \to \cdots
$$
We can use this sequence to compute the [relative homology groups](@entry_id:159711) $H_k(S^n, S^{n-1})$. For $k > n$ and $k \le 1$ (for $n\ge 2$), most groups in the sequence are zero, implying $H_k(S^n, S^{n-1})=0$. The interesting parts of the sequence are around dimension $n$:
$$
\cdots \to H_n(S^{n-1}) \to H_n(S^n) \to H_n(S^n, S^{n-1}) \to H_{n-1}(S^{n-1}) \to H_{n-1}(S^n) \to \cdots
$$
Plugging in the known homology groups for $n \ge 2$:
$$
\cdots \to 0 \to \mathbb{Z} \to H_n(S^n, S^{n-1}) \to \mathbb{Z} \to 0 \to \cdots
$$
This segment reveals a [short exact sequence](@entry_id:137930): $0 \to \mathbb{Z} \to H_n(S^n, S^{n-1}) \to \mathbb{Z} \to 0$. For integer coefficients, this sequence splits, yielding the [isomorphism](@entry_id:137127) $H_n(S^n, S^{n-1}) \cong \mathbb{Z} \oplus \mathbb{Z}$. A similar analysis for the case with $(S^3, S^2)$ yields $H_3(S^3, S^2) \cong \mathbb{Z} \oplus \mathbb{Z}$.

This algebraic result has a beautiful geometric interpretation. The [relative homology](@entry_id:159348) group $H_k(X,A)$ is isomorphic to the [reduced homology](@entry_id:274187) $\tilde{H}_k(X/A)$ of the [quotient space](@entry_id:148218) where $A$ is collapsed to a point. In our case, collapsing the equator $S^{n-1}$ of $S^n$ splits the sphere into its northern and southern hemispheres, which now share a common point. The resulting space $S^n/S^{n-1}$ is homeomorphic to a wedge of two $n$-spheres, $S^n \vee S^n$. The $n$-th homology of $S^n \vee S^n$ is indeed $\mathbb{Z} \oplus \mathbb{Z}$.

#### Attaching Cells and Creating Torsion

A primary method for constructing new spaces is by attaching cells. Consider a space $X$ formed by attaching an $(n+1)$-cell, $e^{n+1}$, to an $n$-sphere, $S^n$, via an [attaching map](@entry_id:153852) $f: \partial e^{n+1} \to S^n$. Since $\partial e^{n+1} \cong S^n$, the [attaching map](@entry_id:153852) is a map $f: S^n \to S^n$, which has a well-defined degree, say $k$. The resulting space is denoted $X = S^n \cup_f e^{n+1}$.

The homology of $X$ can be computed using its [cellular chain complex](@entry_id:160435). For $n \ge 2$, this complex is very simple in the relevant dimensions:
$$
\cdots \to 0 \to C_{n+1}(X) \xrightarrow{d_{n+1}} C_n(X) \to \cdots
$$
Here, $C_{n+1}(X) \cong \mathbb{Z}$, generated by the single $(n+1)$-cell, and $C_n(X) \cong \mathbb{Z}$, generated by the $n$-cell of the base sphere $S^n$. A fundamental theorem of [cellular homology](@entry_id:157864) states that the boundary map $d_{n+1}$ is multiplication by the degree of the [attaching map](@entry_id:153852) $f$. So, $d_{n+1}$ is multiplication by $k$.

The homology groups of $X$ are the homology of this [chain complex](@entry_id:150246).
- $H_{n+1}(X; \mathbb{Z}) = \ker(d_{n+1})$. Since $d_{n+1}$ is multiplication by a non-zero integer $k$ (assuming $k \neq 0$), its kernel is trivial. So, $H_{n+1}(X; \mathbb{Z}) = 0$.
- $H_n(X; \mathbb{Z}) = \ker(d_n) / \text{im}(d_{n+1})$. The image of $d_{n+1}$ is the subgroup $k\mathbb{Z} \subset \mathbb{Z}$. Assuming $d_n$ is the zero map (which it is in this case), we get $H_n(X; \mathbb{Z}) \cong \mathbb{Z} / k\mathbb{Z} = \mathbb{Z}_k$.

This remarkable result shows a direct connection between the geometric notion of degree and the algebraic creation of **torsion**. Attaching a cell with a degree $k$ map creates a finite cyclic group of order $k$ in the homology of the resulting space. The space $S^n \cup_f e^{n+1}$ with $\deg(f)=k$ is often called a **Moore space** $M(\mathbb{Z}_k, n)$.

This analysis can be extended by considering homology with different coefficient groups, which requires the **Universal Coefficient Theorem**. For instance, to compute $H_{n+1}(X; \mathbb{Z}_m)$, the theorem provides the [short exact sequence](@entry_id:137930):
$$
0 \to H_{n+1}(X; \mathbb{Z}) \otimes \mathbb{Z}_m \to H_{n+1}(X; \mathbb{Z}_m) \to \text{Tor}(H_n(X; \mathbb{Z}), \mathbb{Z}_m) \to 0
$$
Substituting our previously computed homology groups:
$$
0 \to 0 \otimes \mathbb{Z}_m \to H_{n+1}(X; \mathbb{Z}_m) \to \text{Tor}(\mathbb{Z}_k, \mathbb{Z}_m) \to 0
$$
This implies that $H_{n+1}(X; \mathbb{Z}_m) \cong \text{Tor}(\mathbb{Z}_k, \mathbb{Z}_m)$. The torsion product of two [cyclic groups](@entry_id:138668) is known to be $\text{Tor}(\mathbb{Z}_k, \mathbb{Z}_m) \cong \mathbb{Z}_{\gcd(k,m)}$. Therefore, the order of this homology group is $\gcd(k,m)$. This result beautifully illustrates the intricate interplay between the topology of the [attaching map](@entry_id:153852) (its degree $k$) and the algebraic structure of the coefficient group (its order $m$).