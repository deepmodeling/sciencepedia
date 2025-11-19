## Introduction
In the study of topology, homotopy groups provide a powerful algebraic lens to classify and understand the "shape" of spaces. However, these tools often fall short when we need to understand not just a space in isolation, but how a subspace is embedded within it. This raises a fundamental question: how can we algebraically describe the relationship between a space and its subspace? To address this, we generalize the concept of homotopy to relative homotopy, which leads to the construction of [relative homotopy groups](@entry_id:261406). These groups capture the topological features—the "holes" and connectivity—of a larger space that are not already present in the chosen subspace.

This article provides a comprehensive introduction to [relative homotopy groups](@entry_id:261406) and their central role in algebraic topology. Over three chapters, you will gain a deep understanding of this essential concept.
*   **Principles and Mechanisms**: We begin by formally defining relative homotopy and the [relative homotopy groups](@entry_id:261406) Πₙ(X, A). We will explore their algebraic structure and introduce the single most important tool associated with them: the [long exact sequence of a pair](@entry_id:158857).
*   **Applications and Interdisciplinary Connections**: Next, we demonstrate the power of this machinery by applying it to concrete problems, from computing the homotopy groups of CW complexes to formalizing the ideas of [obstruction theory](@entry_id:161880) and exploring deep connections with [fibrations](@entry_id:156331).
*   **Hands-On Practices**: Finally, you will have the opportunity to solidify your knowledge by working through guided problems that bridge the abstract theory with tangible geometric calculations.

By the end, you will see how [relative homotopy groups](@entry_id:261406) transform complex geometric questions about spaces and subspaces into tractable algebraic problems, making them an indispensable part of the modern topologist's toolkit.

## Principles and Mechanisms

Having introduced the fundamental concepts of homotopy theory, we now extend these ideas to pairs of [topological spaces](@entry_id:155056). This generalization, known as relative homotopy, provides a powerful lens for understanding how a subspace is situated within a larger ambient space. The algebraic invariants we construct, the **[relative homotopy groups](@entry_id:261406)**, do not merely measure the intrinsic shape of the spaces involved, but rather the connectivity and "holes" of the larger space that are not already present in the subspace. These groups are interconnected through one of the most fundamental tools in algebraic topology: the [long exact sequence of a pair](@entry_id:158857).

### The Concept of a Relative Homotopy

The core idea of homotopy is [continuous deformation](@entry_id:151691). For relative homotopy, we consider deformations that are constrained with respect to a given subspace. We formalize this using the language of pairs. A **topological pair** $(X, A)$ consists of a [topological space](@entry_id:149165) $X$ and a subspace $A \subseteq X$. A **map of pairs** $f: (X, A) \to (Y, B)$ is a continuous map $f: X \to Y$ such that the image of the subspace $A$ is contained within the subspace $B$, i.e., $f(A) \subseteq B$.

A **homotopy of pairs** between two maps of pairs, $f_0, f_1: (X, A) \to (Y, B)$, is a continuous map $H: X \times [0,1] \to Y$ that is a homotopy from $f_0$ to $f_1$ and, crucially, which itself constitutes a map of pairs $(X \times [0,1], A \times [0,1]) \to (Y, B)$ at every stage. This means that for all $t \in [0,1]$, the map $H_t(x) = H(x, t)$ satisfies $H_t(A) \subseteq B$. In essence, the deformation of $X$ must always respect the subspace condition.

This constraint is far from trivial; it can introduce profound obstructions to homotopies that might otherwise seem possible. Consider a hypothetical scenario modeling the closing of a string bag [@problem_id:1671104]. We can represent the bag as the [unit disk](@entry_id:172324) $D^2$ and its drawstring rim as the unit circle $S^1$. The process of closing the bag is a continuous deformation $H: D^2 \times [0,1] \to D^2$. At time $t=0$, the bag is open, so $H(z, 0)$ is the identity map. At time $t=1$, the bag is cinched to a point on its rim, say $x_0 \in S^1$, so $H(z, 1)$ is the constant map to $x_0$. The physical constraint is that the drawstring never leaves the rim, meaning for any point $w \in S^1$, its position $H(w,t)$ must remain in $S^1$ for all time $t$.

This process describes a homotopy of pairs from the identity map $\text{id}: (D^2, S^1) \to (D^2, S^1)$ to the constant map $c_{x_0}: (D^2, S^1) \to (D^2, S^1)$. While it is true that $D^2$ is contractible and thus any map *into* $D^2$ can be deformed to a point, the constraint on the boundary changes everything. The homotopy of pairs $H$ requires that its restriction to the boundary, $H|_{S^1 \times [0,1]}: S^1 \times [0,1] \to S^1$, must be a homotopy entirely within $S^1$. This would be a homotopy between the identity map on $S^1$ (at $t=0$) and a constant map on $S^1$ (at $t=1$). The identity map on $S^1$ has a [winding number](@entry_id:138707) (or degree) of 1, while a constant map has degree 0. Since degree is a homotopy invariant for maps $S^1 \to S^1$, no such homotopy can exist. Therefore, the seemingly simple process of closing the bag is impossible under this mathematical model, revealing a non-trivial element of relative homotopy.

### Formal Definition of Relative Homotopy Groups

To capture such obstructions algebraically, we define the **$n$-th relative homotopy group** of a pair $(X, A)$ with a basepoint $x_0 \in A$, denoted $\pi_n(X, A, x_0)$. Its elements are homotopy classes of maps from an $n$-dimensional model space (like a cube or a disk) into $X$, with boundary conditions that involve both $A$ and $x_0$.

There are two common, equivalent constructions.

**The Cube Model**: For $n \ge 1$, we consider maps from the $n$-cube, $f: I^n \to X$, where $I^n = [0,1]^n$. The boundary $\partial I^n$ is partitioned. We distinguish the "bottom face" $I_0^{n-1} = I^{n-1} \times \{0\}$ from the rest of the boundary, $J^{n-1} = \text{cl}(\partial I^n \setminus I_0^{n-1})$. An element of $\pi_n(X, A, x_0)$ is a homotopy class of maps $f$ satisfying:
1. $f(I_0^{n-1}) \subseteq A$ (the bottom face maps into the subspace).
2. $f(J^{n-1}) = \{x_0\}$ (the rest of the boundary collapses to the basepoint).
Homotopies must preserve these conditions at every stage.

**The Disk Model**: We consider maps from the $n$-disk, $g: D^n \to X$, with a basepoint $s_0$ on its boundary sphere $S^{n-1} = \partial D^n$. An element of $\pi_n(X, A, x_0)$ is a homotopy class of maps $g$ satisfying:
1. $g(S^{n-1}) \subseteq A$ (the entire boundary maps into the subspace).
2. $g(s_0) = x_0$ (the basepoint on the boundary is respected).

These two definitions yield [isomorphic groups](@entry_id:148221), provided the subspace $A$ is **path-connected**. The isomorphism is established not by a simple homeomorphism of the domains, but by a clever geometric manipulation [@problem_id:1671160]. Starting with a map $g$ in the disk model, one can perform a homotopy (relative to the basepoint $s_0$) that "shrinks" one hemisphere of the boundary $S^{n-1}$ to the point $s_0$. This new map sends one hemisphere to $x_0$ and the other into $A$. This configuration, a disk with its boundary split into two parts, is homeomorphic to the cube with its boundary split into $J^{n-1}$ and $I_0^{n-1}$, establishing a correspondence between the models.

A crucial sanity check for this definition is the case where the subspace is trivial, i.e., $A = \{x_0\}$. In this scenario, the condition $f(I_0^{n-1}) \subseteq \{x_0\}$ combined with $f(J^{n-1}) = \{x_0\}$ forces the entire boundary $\partial I^n$ to be mapped to the single point $x_0$. A map from $I^n$ that collapses its boundary to a point is equivalent to a based map from the [quotient space](@entry_id:148218) $I^n / \partial I^n$, which is homeomorphic to the $n$-sphere $S^n$. This is precisely the definition of the absolute homotopy group $\pi_n(X, x_0)$. Thus, we have a [natural isomorphism](@entry_id:276379) $\pi_n(X, \{x_0\}, x_0) \cong \pi_n(X, x_0)$, showing that our relative theory is a proper generalization of the absolute one [@problem_id:1671132].

### The Structure of $\pi_n(X, A, x_0)$

The algebraic structure of $\pi_n(X, A, x_0)$ depends critically on the dimension $n$.

For $n \ge 2$, $\pi_n(X, A, x_0)$ is a group. The group operation is most easily defined using the cube model. Given two representatives $[f]$ and $[g]$, their sum $[f] + [g]$ is defined by concatenating the maps along a coordinate that is *transverse* to the special coordinate defining the bottom face. For instance, if $I_0^{n-1}$ is defined by $t_n=0$, we concatenate along the $t_1$ direction [@problem_id:1671169]:
$$
(f+g)(t_1, \dots, t_n) = \begin{cases} f(2t_1, t_2, \dots, t_n)  \text{ if } 0 \le t_1 \le 1/2 \\ g(2t_1 - 1, t_2, \dots, t_n)  \text{ if } 1/2 \le t_1 \le 1 \end{cases}
$$
This new map is well-defined and continuous because at the seam where $t_1=1/2$, the first piece is evaluated at points with first coordinate $1$ and the second at points with first coordinate $0$. Both of these boundary faces are part of $J^{n-1}$, so both $f$ and $g$ map them to $x_0$, ensuring the pieces match up. For $n \ge 3$, this group is abelian.

For $n=1$, the object $\pi_1(X, A, x_0)$ is generally not a group, but a **pointed set**. An element is a homotopy class of paths $\gamma: [0,1] \to X$ such that $\gamma(0) = x_0$ and the endpoint $\gamma(1)$ lies somewhere in $A$. The homotopy $H(s,t)$ must fix the starting point, $H(0,t)=x_0$, but the endpoint is only required to move within $A$, i.e., $H(1,t) \in A$. A crucial invariant of such a homotopy class is the path-component of $A$ in which the path's endpoint lies. If $A$ is not path-connected, paths ending in different components cannot be homotopic [@problem_id:1671172]. For example, if $A$ is the union of two disjoint circles $C_1$ and $C_2$, and $x_0 \in C_1$, then the constant path at $x_0$ cannot be deformed into a path that ends on $C_2$, because the endpoint would have to trace a continuous path from $C_1$ to $C_2$ within $A$, which is impossible.

### The Long Exact Sequence of a Pair

The true power of [relative homotopy groups](@entry_id:261406) is unleashed through their connection to the absolute homotopy groups of $X$ and $A$. This connection is formalized in the **long exact sequence of the pair** $(X, A)$:

$$
\cdots \to \pi_n(A, x_0) \xrightarrow{i_*} \pi_n(X, x_0) \xrightarrow{j_*} \pi_n(X, A, x_0) \xrightarrow{\partial} \pi_{n-1}(A, x_0) \to \cdots \to \pi_1(X, A, x_0)
$$

Here, $i_*$ is induced by the inclusion map $i: A \hookrightarrow X$ and $j_*$ is induced by the inclusion $j: (X, \{x_0\}) \hookrightarrow (X, A)$. The most significant map is the **boundary map** $\partial: \pi_n(X, A, x_0) \to \pi_{n-1}(A, x_0)$.

Geometrically, the boundary map is constructed by "restricting to the boundary." Given a representative $f: I^n \to X$ of a class in $\pi_n(X, A, x_0)$, its restriction to the bottom face $I_0^{n-1}$ gives a map from $I_0^{n-1}$ to $A$. This map, after identifying $I_0^{n-1}$ with $I^{n-1}$, satisfies the boundary conditions for an element of $\pi_{n-1}(A, x_0)$ because the boundary of $I_0^{n-1}$ is contained in $J^{n-1}$, which $f$ maps to $x_0$. Therefore, $\partial[f]$ is simply the class of $f|_{I_0^{n-1}}$ [@problem_id:1671137].

The **exactness** of this sequence at each group provides a profound geometric interpretation. Exactness at $\pi_{n-1}(A, x_0)$ means that $\text{Im}(\partial) = \ker(i_*)$. This is a cornerstone result. It states that a homotopy class $[\alpha] \in \pi_{n-1}(A, x_0)$ is the boundary of some relative class in $\pi_n(X, A, x_0)$ if and only if $[\alpha]$ becomes trivial when considered as a class in $\pi_{n-1}(X, x_0)$. In other words, a sphere (or loop) in $A$ can be "filled in" by a disk in the larger space $X$ if and only if it represents the boundary of a relative $n$-cell.

This principle is beautifully illustrated when $X$ is constructed from $A$ by attaching cells.
- Consider the torus $T^2$ as a 2-cell attached to its 1-skeleton $A = S^1 \vee S^1$ [@problem_id:1671175]. The [attaching map](@entry_id:153852) corresponds to the commutator loop $[a][b][a]^{-1}[b]^{-1}$ in $\pi_1(A, x_0)$. In the space $X=T^2$, this loop is [null-homotopic](@entry_id:153762) because it bounds the 2-cell. The exact sequence predicts this: the class of $[a][b][a]^{-1}[b]^{-1}$ is in $\ker(i_*)$ and therefore must be in $\text{Im}(\partial)$. It is the boundary of the relative 2-cell that *is* the 2-cell of the torus.
- If we construct a space $X$ by attaching a 2-disk to $A = S^1 \vee S^1$ along a map representing the generator $a \in \pi_1(A, x_0)$, then in $X$, any loop homotopic to $a$, or any of its conjugates like $bab^{-1}$, becomes [null-homotopic](@entry_id:153762). The kernel of $i_*: \pi_1(A, x_0) \to \pi_1(X, x_0)$ is the **[normal closure](@entry_id:139625)** of $a$, denoted $\langle \! \langle a \rangle \! \rangle$. By exactness, this must be the image of the boundary map, $\text{Im}(\partial) = \langle \! \langle a \rangle \! \rangle$ [@problem_id:1671159]. This highlights how the non-abelian structure of $\pi_1(A, x_0)$ is respected by the sequence.

Furthermore, the long exact sequence is **natural**. A map of pairs $f: (X, A, x_0) \to (Y, B, y_0)$ induces a "ladder" diagram connecting the long [exact sequences](@entry_id:151503) of the two pairs. Every square in this ladder commutes. The commutation of the square involving the boundary map, $\partial_Y \circ f_* = (f|_A)_* \circ \partial_X$, is a powerful computational tool [@problem_id:1671176]. It allows us to relate the boundary of an element in one space to the boundary of its image in another, purely by considering the map's effect on the subspaces.

### The Action of $\pi_1(X,x_0)$

The $n=1$ portion of the long exact sequence involves pointed sets.
$$
\pi_1(A,x_0) \xrightarrow{i_*} \pi_1(X,x_0) \xrightarrow{j_*} \pi_1(X,A,x_0) \xrightarrow{\partial} \pi_0(A)
$$
The fundamental group $\pi_1(X, x_0)$ acts on the set $\pi_1(X, A, x_0)$. Given a loop $[\gamma] \in \pi_1(X, x_0)$ and a relative path $[f] \in \pi_1(X, A, x_0)$, the action is defined by pre-concatenation: $[\gamma] \cdot [f] = [\bar{\gamma} * f]$, where $\bar{\gamma}$ is the reverse path of $\gamma$. This action partitions $\pi_1(X, A, x_0)$ into orbits.

A key result states that two elements of $\pi_1(X, A, x_0)$ are in the same orbit if and only if their endpoints lie in the same path-component of $A$. That is, the set of orbits is in [bijection](@entry_id:138092) with $\pi_0(A)$. If $A$ is path-connected, the action is transitive, meaning there is only one orbit [@problem_id:1671148]. In this case, the exact sequence implies that $j_*$ is surjective, and $\pi_1(X, A, x_0)$ is in bijection with the set of [right cosets](@entry_id:136335) $\text{Im}(i_*) \backslash \pi_1(X, x_0)$. The action is then simply the standard action of a group on its [coset space](@entry_id:180459). This provides a complete algebraic description of the set $\pi_1(X, A, x_0)$ and its relationship to the other groups in the sequence.

In summary, [relative homotopy groups](@entry_id:261406) and the associated long exact sequence provide a rigorous and deeply insightful framework for analyzing the relationship between a space and its subspaces. By transforming geometric problems of inclusion and extension into algebraic problems of [exact sequences](@entry_id:151503) and group theory, they form an indispensable part of the modern topological toolkit.