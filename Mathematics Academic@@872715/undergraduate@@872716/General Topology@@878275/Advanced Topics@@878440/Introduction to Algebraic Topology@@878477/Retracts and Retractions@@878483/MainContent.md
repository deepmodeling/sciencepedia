## Introduction
In the study of topology, understanding the relationship between a space and its subspaces is of paramount importance. One of the most elegant and powerful of these relationships is that of a retract, which formalizes the intuitive idea of continuously "shrinking" a space onto one of its parts. This concept is not merely a definitional curiosity; it is a fundamental tool that reveals deep structural truths, helps classify spaces, and serves as a linchpin connecting topology to geometry, analysis, and algebra. This article demystifies the concept of retracts and retractions, addressing the need for a rigorous yet intuitive framework for analyzing how subspaces are embedded within larger spaces.

Over the following chapters, you will gain a thorough understanding of this essential topological concept. The journey begins in **Principles and Mechanisms**, where we will establish the formal definition of a retraction, explore foundational examples, and examine how topological properties are inherited by retracts. Next, **Applications and Interdisciplinary Connections** will broaden our perspective, showcasing how the existence (or non-existence) of a retraction is used to prove major theorems in algebraic topology and how the concept manifests in fields like geometric analysis and the theory of [topological groups](@entry_id:155664). Finally, **Hands-On Practices** will provide an opportunity to solidify your understanding by tackling concrete problems and constructing your own arguments. Let's begin by exploring the core principles that govern this fascinating topological relationship.

## Principles and Mechanisms

In our study of [topological spaces](@entry_id:155056), we often focus on the relationship between a space and its subspaces. One of the most fundamental and fruitful of these relationships is that of a **retract**. Informally, a subspace is a retract of a larger space if the larger space can be continuously "shrunk" or "collapsed" onto the subspace in such a way that the subspace itself remains fixed throughout the process. This concept not only provides a powerful tool for [classifying spaces](@entry_id:148422) but also serves as a gateway to more advanced topics in algebraic topology.

### The Formal Definition of a Retraction

Let $X$ be a topological space and let $A$ be a subspace of $X$. We say that $A$ is a **retract** of $X$ if there exists a [continuous map](@entry_id:153772) $r: X \to A$ such that the restriction of $r$ to $A$ is the identity map on $A$. In other words, for every point $a \in A$, the map $r$ must satisfy $r(a) = a$. Such a map $r$ is called a **retraction** of $X$ onto $A$.

This definition contains three critical components:
1.  The map $r$ must be continuous.
2.  The map $r$ must send every point of $X$ to a point within the subspace $A$. This implies that a retraction is always a surjective map onto its codomain.
3.  The map $r$ must be the identity on the subspace $A$; it must fix every point of $A$.

A direct and important consequence of this definition concerns the fixed points of the retraction map. If we consider the retraction $r: X \to A$ as a map from $X$ into itself (since $A \subseteq X$), a fixed point is any $x \in X$ such that $r(x) = x$. By the definition of a retraction, every point $a \in A$ is a fixed point. Furthermore, if $x \in X$ is a fixed point, then $r(x) = x$. Since the [codomain](@entry_id:139336) of $r$ is $A$, we must have $r(x) \in A$, which implies $x \in A$. Therefore, the set of all fixed points of a retraction $r: X \to A$ is precisely the subspace $A$ itself [@problem_id:1572025].

### Constructing Retractions: Foundational Examples

To build an intuition for retractions, it is helpful to examine several canonical examples.

A very common method for constructing retractions is through projection. For instance, consider the Euclidean plane $X = \mathbb{R}^2$ and its subspace $A = \{(x, 0) \mid x \in \mathbb{R}\}$, which is the $x$-axis. The map $r: \mathbb{R}^2 \to A$ defined by $r(x, y) = (x, 0)$ is a retraction. This map is continuous, as it is a standard projection. For any point $(x_0, 0)$ already on the $x$-axis, $r(x_0, 0) = (x_0, 0)$, so the map fixes every point in $A$. Thus, the $x$-axis is a retract of the plane [@problem_id:1572037]. This idea extends naturally. For example, any diameter of the closed [unit disk](@entry_id:172324) $D^2$ is a retract of the disk, with the retraction map given by [orthogonal projection](@entry_id:144168) onto the line containing the diameter [@problem_id:1572010].

Another powerful example is radial projection. Let $X$ be the punctured plane, $\mathbb{R}^2 \setminus \{(0,0)\}$, and let $A$ be the unit circle $S^1$. The map $r: X \to A$ given by
$$ r(\mathbf{v}) = \frac{\mathbf{v}}{\|\mathbf{v}\|} $$
is a retraction [@problem_id:1572002]. For any non-[zero vector](@entry_id:156189) $\mathbf{v} = (x,y)$, $\|\mathbf{v}\| = \sqrt{x^2+y^2}$ is a positive, continuous function, so $r$ is continuous on $X$. The image point $r(\mathbf{v})$ has norm $\|r(\mathbf{v})\| = \|\mathbf{v}\|/\|\mathbf{v}\| = 1$, so it lies on $S^1$. If a point $\mathbf{v}_0$ is already on the circle $S^1$, its norm is $\|\mathbf{v}_0\| = 1$, so $r(\mathbf{v}_0) = \mathbf{v}_0/1 = \mathbf{v}_0$. Thus, $S^1$ is a retract of the [punctured plane](@entry_id:150262).

Retractions can also be constructed piecewise. Consider $X = \mathbb{R}$ and the closed interval $A = [0, 1]$. The map $r: \mathbb{R} \to [0, 1]$ defined by
$$ r(x) = \begin{cases} 0 & \text{if } x \lt 0 \\ x & \text{if } 0 \le x \le 1 \\ 1 & \text{if } x \gt 1 \end{cases} $$
is a continuous map that fixes every point in $[0, 1]$, and is therefore a retraction [@problem_id:1571990]. This "clamping" function demonstrates how a space can be retracted onto a bounded subspace.

Finally, it is not necessary for the ambient space to be connected. Let $X$ be the [disconnected space](@entry_id:155520) $[0, 1] \cup [2, 3]$ and $A$ be the two-point set $\{0, 3\}$. The map
$$ r(x) = \begin{cases} 0 & \text{if } x \in [0, 1] \\ 3 & \text{if } x \in [2, 3] \end{cases} $$
is continuous on $X$ by the pasting lemma, since its restrictions to the [closed sets](@entry_id:137168) $[0,1]$ and $[2,3]$ are continuous. It clearly fixes the points $0$ and $3$. Therefore, $A$ is a retract of $X$ [@problem_id:1572037].

### An Algebraic Characterization: Idempotent Maps

In some cases, a retraction is a map from a space $X$ back into itself, where the retract is simply the image of the map. This leads to a useful algebraic characterization. A [continuous map](@entry_id:153772) $f: X \to X$ is called **idempotent** if applying it twice is the same as applying it once; that is, $f \circ f = f$.

A continuous map $f: X \to X$ is a retraction onto its image, $A = \mathrm{Im}(f)$, if and only if it is idempotent [@problem_id:1572001].
To see this, first assume $f$ is a retraction onto $A = \mathrm{Im}(f)$. For any $x \in X$, the point $f(x)$ lies in $A$. Since $f$ must fix all points in $A$, we have $f(f(x)) = f(x)$. As this holds for all $x \in X$, we conclude $f \circ f = f$.
Conversely, assume $f$ is idempotent. Let $A = \mathrm{Im}(f)$. We need to show that $f$ fixes every point in $A$. Let $a \in A$. By definition of the image, there exists some $x \in X$ such that $a = f(x)$. Applying $f$ to $a$, we get $f(a) = f(f(x))$. Since $f$ is idempotent, $f(f(x)) = f(x)$, which is just $a$. Thus, $f(a) = a$, and $f$ is a retraction onto its image.

This provides a simple test. For example, the map $f: \mathbb{R} \to \mathbb{R}$ given by $f(x) = |x|$ is a retraction onto its image $[0, \infty)$ because $f(f(x)) = ||x|| = |x| = f(x)$. Similarly, the projection map $f: \mathbb{R}^2 \to \mathbb{R}^2$ given by $f(x,y) = (x,x)$ is a retraction onto the diagonal line because $f(f(x,y)) = f(x,x) = (x,x) = f(x,y)$. In contrast, $f(x) = x^3$ is not a retraction onto its image, as $f(f(x)) = (x^3)^3 = x^9 \neq x^3$ in general [@problem_id:1572001].

### Inherited Topological Properties

Since a retraction $r: X \to A$ is a continuous [surjection](@entry_id:634659), any [topological property](@entry_id:141605) that is preserved under continuous surjective maps will be inherited by a retract $A$ from the [ambient space](@entry_id:184743) $X$.

Two of the most important such properties are **compactness** and **connectedness**.
*   If $X$ is a compact space and $A$ is a retract of $X$, then $A$ must be compact. This is a direct consequence of the theorem that the [continuous image of a compact space](@entry_id:265606) is compact. Since $r: X \to A$ is a continuous [surjection](@entry_id:634659), $A = r(X)$ is compact [@problem_id:1571999].
*   If $X$ is a [connected space](@entry_id:153144) and $A$ is a retract of $X$, then $A$ must be connected. Similarly, this follows because the continuous image of a connected space is connected [@problem_id:1571999], [@problem_id:1572037].

It is important to note that the reverse implications are not true. A subspace being compact or connected does not imply the [ambient space](@entry_id:184743) has the same property. For example, $A=[0,1]$ is a connected and compact retract of the non-compact and [connected space](@entry_id:153144) $X = \mathbb{R}$, which in turn is a subspace of the [disconnected space](@entry_id:155520) $Y = \mathbb{R} \setminus \{1.5\}$.

Furthermore, some properties are inherited by all subspaces, and therefore by all retracts. For instance, any subspace of a Hausdorff space is Hausdorff. Consequently, if $X$ is a Hausdorff space, any retract $A$ of $X$ must also be Hausdorff [@problem_id:1571999].

### Obstructions to Retraction

The inheritance of topological properties provides one of the most powerful techniques in topology: proving the non-existence of certain maps. If we can show that a subspace $A$ lacks a property that it *must* inherit from a space $X$ were it a retract, then we can conclude that no retraction from $X$ to $A$ exists.

The most common tool for this is the [connectedness](@entry_id:142066) argument. Consider the real line $X = \mathbb{R}$ and its subspace of integers $A = \mathbb{Z}$. The space $\mathbb{R}$ is connected. The subspace $\mathbb{Z}$, with the subspace topology inherited from $\mathbb{R}$, is a [discrete space](@entry_id:155685) and is therefore totally disconnected. If a retraction $r: \mathbb{R} \to \mathbb{Z}$ existed, its image $r(\mathbb{R})$ would have to be a connected subset of $\mathbb{Z}$. The only connected subsets of a [discrete space](@entry_id:155685) are single points. This would mean $r$ must be a constant map. However, a retraction must be surjective onto its codomain, and since $\mathbb{Z}$ contains more than one point, this is a contradiction. Therefore, no retraction from $\mathbb{R}$ to $\mathbb{Z}$ can exist [@problem_id:1572029]. A similar argument shows there is no retraction from the connected interval $[0,1]$ onto its disconnected two-point boundary $\{0,1\}$ [@problem_id:1572037].

A more subtle and famous result is that **the boundary circle $S^1$ is not a retract of the [closed disk](@entry_id:148403) $D^2$**. While the proof of this theorem requires the machinery of algebraic topology (specifically, fundamental groups), it is a cornerstone result with profound implications, including a proof of the Brouwer Fixed-Point Theorem [@problem_id:1571990], [@problem_id:1572010].

Another powerful obstruction arises when dealing with compact Hausdorff spaces.
**Theorem:** A retract of a compact Hausdorff space must be a [closed subspace](@entry_id:267213).
*Proof:* Let $X$ be a compact Hausdorff space and let $A$ be a retract of $X$. Since $X$ is Hausdorff, its subspace $A$ is also Hausdorff. As $A$ is the continuous image of the compact space $X$ under the retraction $r$, $A$ is compact. Finally, a well-known theorem states that any [compact subspace](@entry_id:153124) of a Hausdorff space is closed. Therefore, $A$ must be a [closed subset](@entry_id:155133) of $X$ [@problem_id:1571980], [@problem_id:1572010].

This theorem provides an immediate proof that the open disk $B^2 = \{(x,y) \mid x^2+y^2 \lt 1\}$ cannot be a retract of the [closed disk](@entry_id:148403) $D^2 = \{(x,y) \mid x^2+y^2 \le 1\}$. The space $D^2$ is compact and Hausdorff. The subspace $B^2$ is not a [closed subset](@entry_id:155133) of $D^2$ (its closure is $D^2$). Therefore, by the theorem, it cannot be a retract of $D^2$ [@problem_id:1572010].

### The Extension Property: A Key Application

One of the primary reasons retracts are so important in topology is their relationship to the extension of functions. The **[extension problem](@entry_id:150521)** asks: given a subspace $A \subseteq X$ and a continuous map $f: A \to Y$, can we find a continuous map $F: X \to Y$ that extends $f$, meaning that the restriction of $F$ to $A$ is $f$?

The existence of a retraction provides a definitive answer.
**Theorem:** If $A$ is a retract of $X$, then any continuous map $f: A \to Y$ from $A$ to an arbitrary space $Y$ can be extended to a continuous map $F: X \to Y$.

The proof is constructive. Let $r: X \to A$ be the retraction. We define the extension $F: X \to Y$ as the composition:
$$ F = f \circ r $$
This map is continuous because it is the composition of two [continuous maps](@entry_id:153855), $r: X \to A$ and $f: A \to Y$. To verify that it is an extension of $f$, we take any point $a \in A$ and evaluate $F(a)$:
$$ F(a) = (f \circ r)(a) = f(r(a)) $$
Since $r$ is a retraction, it fixes points in $A$, so $r(a) = a$. Thus, $F(a) = f(a)$ for all $a \in A$. This confirms that $F$ is a [continuous extension](@entry_id:161021) of $f$ [@problem_id:1571982].

Finally, it is worth noting the properties of retraction maps themselves. While a retraction $r: X \to A$ is always continuous and surjective, it need not be an [open map](@entry_id:155659) or a [closed map](@entry_id:150357) in general. However, as established earlier, a retraction from a [compact space](@entry_id:149800) to a Hausdorff space is always a [closed map](@entry_id:150357) [@problem_id:1571980]. Because of this strong structural relationship between a space and its retracts, they remain a central object of study in modern topology.