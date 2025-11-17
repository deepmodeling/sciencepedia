## Introduction
In algebraic topology, understanding how spaces can be continuously deformed into one another is a central goal. To study these deformations, or homotopies, rigorously, we need formal tools that can capture this intuitive idea. The cylinder and [mapping cylinder](@entry_id:155932) constructions provide precisely such a mechanism, allowing us to build a bridge between spaces and the maps between them. These constructions address a fundamental need: to transform any [continuous map](@entry_id:153772) into a more structured form—an inclusion—without losing essential topological information. This conversion simplifies proofs and calculations, making the [mapping cylinder](@entry_id:155932) an indispensable part of the modern topologist's toolkit.

The following chapters will guide you through this essential concept. In "Principles and Mechanisms," we will formally define the standard and mapping cylinders and explore their fundamental properties, such as [deformation retraction](@entry_id:148036) and homotopy equivalence. "Applications and Interdisciplinary Connections" will demonstrate their utility within homotopy theory and reveal their conceptual parallels in other scientific fields. Finally, "Hands-On Practices" will provide opportunities to solidify your understanding through targeted exercises.

## Principles and Mechanisms

In the study of topology, we are often concerned with properties that are invariant under continuous deformation. The cylinder construction is a fundamental tool that allows us to formalize these deformations and to relate different spaces and maps in a powerful, unified framework. This chapter delves into the principles governing the standard cylinder and its more general variant, the [mapping cylinder](@entry_id:155932), exploring their construction, core properties, and applications.

### The Standard Cylinder and Deformation Retraction

Let us begin with the most basic form of a cylinder. Given any non-empty topological space $X$, the **standard cylinder** over $X$ is simply the [product space](@entry_id:151533) $C = X \times I$, where $I = [0,1]$ is the closed unit interval. This construction gives us a space that intuitively looks like the space $X$ extended or "swept out" along the interval $I$. The original space $X$ can be identified with the "base" of the cylinder, the subspace $X \times \{0\}$, and also with its "top", the subspace $X \times \{1\}$.

A central concept in algebraic topology is that of **homotopy equivalence**, which captures the idea of two spaces being continuously deformable into one another. A more specific and visually intuitive type of homotopy equivalence is a **[deformation retraction](@entry_id:148036)**. A subspace $A \subseteq Y$ is a **[deformation retract](@entry_id:154224)** of $Y$ if there exists a continuous map $H: Y \times I \to Y$, called a [deformation retraction](@entry_id:148036), satisfying:
1.  $H(y, 0) = y$ for all $y \in Y$ (it starts as the identity map).
2.  $H(y, 1) \in A$ for all $y \in Y$ (it ends by mapping all of $Y$ into $A$).
3.  $H(a, t) = a$ for all $a \in A$ and $t \in I$ (the subspace $A$ remains fixed throughout the deformation).

The standard cylinder provides a canonical example of this phenomenon. The entire cylinder $X \times I$ can be continuously "squashed" down onto its base $X \times \{0\}$. This process can be described by a specific [deformation retraction](@entry_id:148036) [@problem_id:1642511]. Consider the map $H: (X \times I) \times I \to X \times I$ defined by:
$$
H((x, s), t) = (x, (1 - t)s)
$$
Here, $(x,s)$ is a point in the cylinder $X \times I$, and $t$ is the "time" parameter of the deformation. Observe that the $X$-coordinate remains unchanged throughout the process. The second coordinate, $s$, is linearly scaled by a factor $(1-t)$. At time $t=0$, the factor is 1, so $H((x,s), 0) = (x,s)$, and the map is the identity. At time $t=1$, the factor is 0, so $H((x,s), 1) = (x,0)$, and every point has been mapped to the base $X \times \{0\}$. Furthermore, if a point $(x,0)$ is already on the base, its second coordinate is $s=0$, so $H((x,0), t) = (x,0)$ for all $t$. Thus, the base remains fixed. This map $H$ is a [deformation retraction](@entry_id:148036) of $X \times I$ onto $X \times \{0\}$.

The existence of this [deformation retraction](@entry_id:148036) implies that the cylinder $X \times I$ is homotopy equivalent to its base $X$. From the perspective of homotopy theory, they are indistinguishable; they possess the same homotopy groups, homology groups, and other homotopy-invariant properties.

### The Mapping Cylinder: Converting Maps into Inclusions

While the standard cylinder is a product of a space and an interval, the **[mapping cylinder](@entry_id:155932)** is a more general and profoundly useful construction that involves a [continuous map](@entry_id:153772) $f: X \to Y$. Its primary purpose is to create a new space in which the map $f$ is represented by a subspace inclusion, in a way that preserves homotopy information.

**Definition:** Given a [continuous map](@entry_id:153772) $f: X \to Y$, the **[mapping cylinder](@entry_id:155932)** of $f$, denoted $M_f$, is the quotient space obtained from the disjoint union of the cylinder on $X$ and the space $Y$. Specifically,
$$
M_f = \big( (X \times [0,1]) \sqcup Y \big) / \sim
$$
where $\sim$ is the equivalence relation generated by identifying the "top" of the cylinder over each point $x \in X$ with its image in $Y$. That is, for every $x \in X$, we identify $(x, 1) \sim f(x)$.

Visually, one can imagine taking the cylinder $X \times I$ and "gluing" its top end, $X \times \{1\}$, to the space $Y$ according to the instructions provided by the map $f$. The resulting space $M_f$ contains a natural copy of $Y$ as a subspace, as well as a copy of $X$ (as $X \times \{0\}$) at the "bottom" end. It is important to note that some authors define the attachment at $t=0$, i.e., $(x,0) \sim f(x)$. These two conventions produce homeomorphic spaces, as one can be transformed into the other via the [homeomorphism](@entry_id:146933) on the cylinder part given by $(x,t) \mapsto (x, 1-t)$.

### The Fundamental Property: Homotopy Equivalence

The single most important feature of the [mapping cylinder](@entry_id:155932) is that it is homotopy equivalent to the [codomain](@entry_id:139336) (or target space) of the map.

**Theorem:** For any [continuous map](@entry_id:153772) $f: X \to Y$, the space $Y$ is a [strong deformation retract](@entry_id:155000) of the [mapping cylinder](@entry_id:155932) $M_f$. Consequently, $M_f$ and $Y$ are homotopy equivalent.

To prove this, we explicitly construct the [deformation retraction](@entry_id:148036). Let us denote points in $M_f$ by their [equivalence classes](@entry_id:156032), $[z]$. A point $z$ is either of the form $(x,t) \in X \times I$ or $y \in Y$. The [deformation retraction](@entry_id:148036) $H: M_f \times I \to M_f$ is defined as follows:
$$
H([x,t], u) = [x, (1-u)t + u]
$$
$$
H([y], u) = [y]
$$
This homotopy intuitively describes a "flow" within $M_f$. For any point $[x,t]$ in the cylinder part, as the time parameter $u$ goes from $0$ to $1$, its "height" $(1-u)t + u$ goes from $t$ to $1$. At $u=1$, the point becomes $[x,1]$, which is identified with $[f(x)]$. Points already in $Y$ remain fixed for all $u$. This process continuously retracts the entire [mapping cylinder](@entry_id:155932) onto its subspace $Y$.

This powerful result means we can study the homotopy type of $Y$ by studying the space $M_f$, in which the map $f$ has been replaced by the inclusion of $Y$. This has immediate and profound consequences for computing [topological invariants](@entry_id:138526) [@problem_id:1642526] [@problem_id:1642557] [@problem_id:1642518].

*   **Path-Connectedness:** A space is path-connected if and only if its set of path components $\pi_0$ has one element. Since $M_f$ is homotopy equivalent to $Y$, they have isomorphic sets of path components, $\pi_0(M_f) \cong \pi_0(Y)$. Therefore, $M_f$ is path-connected if and only if $Y$ is path-connected. The [path-connectedness](@entry_id:142695) of $X$ is irrelevant [@problem_id:1642526].

*   **Fundamental Group and Homology:** Homotopy equivalence implies isomorphism of all homotopy groups and homology groups. Thus, $\pi_n(M_f, p) \cong \pi_n(Y, f(p))$ and $H_n(M_f) \cong H_n(Y)$ for all $n \ge 0$. This allows for direct computation. For example, consider the map $f: S^1 \to S^1$ given by $f(z) = z^n$ for some integer $n > 0$. The [mapping cylinder](@entry_id:155932) $M_f$ is homotopy equivalent to the [codomain](@entry_id:139336) $S^1$. Therefore, its fundamental group is $\pi_1(M_f) \cong \pi_1(S^1) \cong \mathbb{Z}$, regardless of the degree $n$ of the map [@problem_id:1642557]. Similarly, if we take the inclusion $f$ of the figure-eight $X = S^1 \vee S^1$ into the torus $Y = S^1 \times S^1$, the homology of the [mapping cylinder](@entry_id:155932) is simply the homology of the torus: $H_1(M_f, \mathbb{Z}) \cong H_1(S^1 \times S^1, \mathbb{Z}) \cong \mathbb{Z}^2$, so its rank is 2 [@problem_id:1642518].

### Special Cases and Related Constructions

The versatility of the [mapping cylinder](@entry_id:155932) construction becomes apparent when we consider specific choices for the map $f$.

*   **The Identity Map:** If we take $f$ to be the identity map $\text{id}_X: X \to X$, the [mapping cylinder](@entry_id:155932) $M_{\text{id}_X}$ attaches the top of the cylinder, $X \times \{1\}$, to $X$ by identifying each point $(x,1)$ with $x$. The result is a space homeomorphic to the standard cylinder $X \times [0,1]$ [@problem_id:1642533]. This confirms our intuition that gluing the lid back onto a can in the obvious way just gives us back the can.

*   **The Constant Map and the Cone:** Let $Y = \{*\}$ be a one-point space, and let $f: X \to \{*\}$ be the unique constant map. The [mapping cylinder](@entry_id:155932) $M_f$ is formed by taking $(X \times I) \sqcup \{*\}$ and identifying $(x,1) \sim *$ for all $x \in X$. This is precisely the definition of the **cone** on $X$, denoted $CX$, where the entire "top" face $X \times \{1\}$ is collapsed to a single point (the apex of the cone). If one were to use the convention of attaching at $t=0$, the resulting space $M_f$ would be $(X \times [0,1]) / (X \times \{0\})$, which is also homeomorphic to the cone $CX$. This shows that the cone is a special case of a [mapping cylinder](@entry_id:155932) [@problem_id:1642566].

The [mapping cylinder](@entry_id:155932) also serves as a stepping stone to another important construction: the **[mapping cone](@entry_id:261103)**. The [mapping cone](@entry_id:261103) of $f: X \to Y$, denoted $C_f$, is obtained by taking the [mapping cylinder](@entry_id:155932) $M_f$ and collapsing the "bottom" subspace $X \times \{0\}$ to a single point.
$$
C_f = M_f / (X \times \{0\})
$$
This relationship is reflected in their homology groups. For any good pair of spaces $(A,B)$, there is a [natural isomorphism](@entry_id:276379) between the [relative homology](@entry_id:159348) of the pair and the [reduced homology](@entry_id:274187) of the quotient space, $H_n(A,B) \cong \tilde{H}_n(A/B)$. Applying this to the pair $(M_f, X \times \{0\})$, we immediately obtain a fundamental relationship for all $n \ge 0$ [@problem_id:1642515]:
$$
H_n(M_f, X \times \{0\}) \cong \tilde{H}_n(C_f)
$$
This [isomorphism](@entry_id:137127) is a key ingredient in constructing the long exact sequence in homology associated with a map $f$.

### General Topological Properties

We can also ask how the [mapping cylinder](@entry_id:155932) construction interacts with standard topological properties like compactness and the Hausdorff condition.

*   **Compactness:** If the spaces $X$ and $Y$ are both compact, then the [mapping cylinder](@entry_id:155932) $M_f$ is always compact. The proof is a direct application of fundamental topological theorems. First, the product of [compact spaces](@entry_id:155073) $X$ and $[0,1]$ is compact by the Tychonoff theorem. Second, the disjoint union of a finite number of [compact spaces](@entry_id:155073)—in this case, $X \times [0,1]$ and $Y$—is compact. Finally, the [mapping cylinder](@entry_id:155932) $M_f$ is the image of this [compact space](@entry_id:149800) under the continuous [quotient map](@entry_id:140877). Since the [continuous image of a compact space](@entry_id:265606) is always compact, $M_f$ must be compact [@problem_id:1642556].

*   **Hausdorff Property:** The situation with the Hausdorff property is more subtle. If $X$ and $Y$ are both Hausdorff, is $M_f$ necessarily Hausdorff? In general, quotients of Hausdorff spaces need not be Hausdorff. However, in many common situations, the property is preserved. A sufficient condition for the quotient of a space $Z$ to be Hausdorff is that $Z$ is compact and Hausdorff. If $X$ and $Y$ are compact Hausdorff spaces, then the space $(X \times [0,1]) \sqcup Y$ is also compact and Hausdorff. Its quotient, the [mapping cylinder](@entry_id:155932) $M_f$, is therefore compact and also Hausdorff. Without compactness, one must verify more technical conditions, and counterexamples can be constructed.

### Homotopy and Functoriality

The true power of the [mapping cylinder](@entry_id:155932) lies in its excellent behavior with respect to homotopy.

We have seen that $M_f$ is homotopy equivalent to $Y$. A deeper result connects homotopic *maps* to homotopy equivalent *mapping cylinders*.

**Theorem:** If two maps $f, g: X \to Y$ are homotopic, then their mapping cylinders $M_f$ and $M_g$ are homotopy equivalent.

This means that the homotopy type of the [mapping cylinder](@entry_id:155932) depends only on the homotopy class of the map $f$. A homotopy $H: X \times I \to Y$ between $f$ and $g$ can be used to construct an explicit homotopy equivalence $\Phi: M_f \to M_g$ [@problem_id:1642558]. The map $\Phi$ is defined piece-wise. On the $Y$ part of $M_f$, it is the identity. On the cylinder part $[x,t]_f$, the map first compresses the cylinder interval $[0,1]$ into $[0, 1/2]$, then uses the homotopy $H$ to "slide" the attachment along the path from $f(x)$ to $g(x)$, and finally re-expands the interval. For instance, a point $[x, t]_f$ with $t \in [1/2, 1]$ would map to $[H(x, 2-2t)]_g$ in $M_g$. The parameter $2-2t$ traces the homotopy's time from $1$ (for $t=1/2$) down to $0$ (for $t=1$), effectively reversing the homotopy path to connect $f(x)$ to $g(x)$.

This property can be formalized using the language of [category theory](@entry_id:137315), which provides a higher-level perspective on mathematical structures [@problem_id:1642523]. Let $\text{Top}$ be the category of topological spaces and $\text{Top}^2$ be the **arrow category**, whose objects are [continuous maps](@entry_id:153855) $f: X \to Y$ and whose morphisms are commuting squares. The [mapping cylinder](@entry_id:155932) construction can be viewed as a **[functor](@entry_id:260898)** $M: \text{Top}^2 \to \text{Top}$. This functor has important structural properties:
*   It **preserves coproducts**. The [mapping cylinder](@entry_id:155932) of a disjoint union of maps is the disjoint union of their individual mapping cylinders: $M(\coprod f_i) \cong \coprod M_{f_i}$. The construction behaves predictably when placing objects side-by-side.
*   It **does not preserve products**. In general, $M(f \times g)$ is not homeomorphic to $M(f) \times M(g)$. For example, if $f$ is the identity on a single point, $M(f)$ is homeomorphic to $[0,1]$. Then $M(f) \times M(f)$ is the square $[0,1] \times [0,1]$, while $f \times f$ is still the identity on a point, so $M(f \times f)$ is again just $[0,1]$.

In summary, the cylinder and [mapping cylinder](@entry_id:155932) are not merely examples but essential machinery in algebraic topology. They provide a concrete way to realize homotopies, to transform arbitrary maps into inclusions while preserving homotopy type, and to build related structures like cones, forming a cornerstone of the modern topological toolkit.