## Introduction
After defining the fundamental group as a powerful algebraic invariant for a [topological space](@entry_id:149165), a natural question arises: how does this invariant behave when we consider maps between spaces? The answer lies in one of the most fundamental constructions in algebraic topology, the **[induced homomorphism](@entry_id:149311)**. This concept provides a bridge, translating the continuous world of topological maps into the discrete, structured world of group theory. By understanding this connection, we gain the ability to tackle complex topological problems—such as whether two spaces are different, or whether certain types of maps can exist—by performing algebraic calculations.

This article explores the theory and application of [induced homomorphisms](@entry_id:266478). It addresses the crucial gap between defining an invariant and using it to deduce meaningful topological consequences. Across three chapters, you will gain a comprehensive understanding of this essential tool.

First, in **Principles and Mechanisms**, we will formally define the [induced homomorphism](@entry_id:149311) and establish its two most important properties: [functoriality](@entry_id:150069) and homotopy invariance. These principles form the bedrock upon which the entire theory is built. Following this, **Applications and Interdisciplinary Connections** will showcase the power of this machinery, demonstrating how it is used to prove classic results, classify maps, and reveal deep connections to [covering space theory](@entry_id:273250) and knot theory. Finally, **Hands-On Practices** provides a series of guided problems to help you apply these abstract concepts and solidify your understanding by translating geometric situations into algebraic statements.

## Principles and Mechanisms

Having established the fundamental group, $\pi_1(X, x_0)$, as an algebraic invariant of a pointed topological space $(X, x_0)$, we now explore how this algebraic structure interacts with the primary objects of study in topology: [continuous maps](@entry_id:153855). A continuous map between two spaces provides a bridge, and as we will see, this bridge extends to the algebraic realm of their fundamental groups. This connection, known as the **[induced homomorphism](@entry_id:149311)**, is not merely a technical construction; it is a functorial assignment that translates topological problems into the language of group theory, allowing us to use algebraic tools to deduce profound topological consequences.

### The Definition of the Induced Homomorphism

Let $(X, x_0)$ and $(Y, y_0)$ be two [pointed topological spaces](@entry_id:275011), and let $f: X \to Y$ be a continuous map that preserves the basepoints, meaning $f(x_0) = y_0$. Consider a loop $\alpha: [0, 1] \to X$ based at $x_0$. Since $f$ is continuous, the composition $f \circ \alpha: [0, 1] \to Y$ is also a [continuous path](@entry_id:156599). This new path begins at $(f \circ \alpha)(0) = f(\alpha(0)) = f(x_0) = y_0$ and ends at $(f \circ \alpha)(1) = f(\alpha(1)) = f(x_0) = y_0$. Thus, $f$ transforms a loop based at $x_0$ in $X$ into a loop based at $y_0$ in $Y$.

This action on loops extends naturally to an action on homotopy classes. If two loops $\alpha_0$ and $\alpha_1$ are homotopic in $X$ relative to their endpoints, via a homotopy $H: [0, 1] \times [0, 1] \to X$, then the composition $f \circ H$ provides a homotopy in $Y$ between the loops $f \circ \alpha_0$ and $f \circ \alpha_1$. This ensures that the map on homotopy classes is well-defined. We can therefore define a map, denoted $f_*$, from the fundamental group of $X$ to that of $Y$:
$$f_*: \pi_1(X, x_0) \to \pi_1(Y, y_0)$$
by the rule
$$f_*([\alpha]) = [f \circ \alpha]$$
for any homotopy class of loops $[\alpha] \in \pi_1(X, x_0)$.

This map $f_*$ is not just a function between sets; it is a **[group homomorphism](@entry_id:140603)**. To see this, consider two loop classes $[\alpha]$ and $[\beta]$ in $\pi_1(X, x_0)$. Their product is represented by the concatenated loop $\alpha * \beta$. The image of this product under $f_*$ is
$$f_*([\alpha * \beta]) = [f \circ (\alpha * \beta)]$$
By the definition of path concatenation, the composite loop $f \circ (\alpha * \beta)$ is equivalent to concatenating the individual composite loops, $(f \circ \alpha) * (f \circ \beta)$. Therefore,
$$[f \circ (\alpha * \beta)] = [(f \circ \alpha) * (f \circ \beta)] = [f \circ \alpha] * [f \circ \beta] = f_*([\alpha]) * f_*([\beta])$$
This confirms that $f_*$ preserves the group structure.

A simple yet illustrative case is the constant map. Let $f: X \to Y$ be the constant map defined by $f(x) = y_0$ for all $x \in X$. For any loop $\alpha$ in $X$ based at $x_0$, the composite loop $f \circ \alpha$ is the constant loop at $y_0$. The homotopy class of the constant loop is the identity element of the group $\pi_1(Y, y_0)$. Consequently, $f_*$ maps every element of $\pi_1(X, x_0)$ to the [identity element](@entry_id:139321) in $\pi_1(Y, y_0)$. Such a homomorphism is known as the **trivial homomorphism** [@problem_id:1558610].

### Functoriality and Homotopy Invariance

The assignment of the [induced homomorphism](@entry_id:149311) $f_*$ to a continuous map $f$ is not arbitrary; it adheres to a rigid and powerful set of rules that are foundational to algebraic topology. These rules are encapsulated in the concepts of [functoriality](@entry_id:150069) and homotopy invariance.

#### Functorial Properties

The term "functor" comes from [category theory](@entry_id:137315) and, in this context, signifies that the process of assigning a fundamental group to a space and an [induced homomorphism](@entry_id:149311) to a map respects the basic structures of identity and composition.

1.  **Identity:** The identity map on a space, $\text{id}_X: (X, x_0) \to (X, x_0)$, induces the identity homomorphism on its fundamental group. That is, $(\text{id}_X)_* = \text{id}_{\pi_1(X, x_0)}$. This is clear from the definition, as $(\text{id}_X)_*([\alpha]) = [\text{id}_X \circ \alpha] = [\alpha]$.

2.  **Composition:** Consider a sequence of pointed [continuous maps](@entry_id:153855) $f: (X, x_0) \to (Y, y_0)$ and $g: (Y, y_0) \to (Z, z_0)$. We can form the composition $g \circ f: (X, x_0) \to (Z, z_0)$, which induces its own homomorphism $(g \circ f)_*$. The [functoriality](@entry_id:150069) property states that this [induced map](@entry_id:271712) is precisely the composition of the individual [induced homomorphisms](@entry_id:266478):
    $$(g \circ f)_* = g_* \circ f_*$$
    To prove this, we simply apply the definitions to an arbitrary loop class $[\alpha] \in \pi_1(X, x_0)$:
    $$(g \circ f)_*([\alpha]) = [(g \circ f) \circ \alpha] = [g \circ (f \circ \alpha)] = g_*([f \circ \alpha]) = g_*(f_*([\alpha])) = (g_* \circ f_*)([\alpha])$$
    This property is of paramount importance, as it ensures that the algebraic picture faithfully mirrors the topological one [@problem_id:1558620].

#### Homotopy Invariance

Perhaps the most significant property of the [induced homomorphism](@entry_id:149311) is its invariance under homotopy. This property ensures that the fundamental group is a genuine topological invariant, sensitive only to the "shape" of a space, not the specific choice of maps used to probe it.

The central theorem is as follows: If two pointed [continuous maps](@entry_id:153855) $f, g: (X, x_0) \to (Y, y_0)$ are homotopic relative to the basepoint $x_0$, then their [induced homomorphisms](@entry_id:266478) are identical, i.e., $f_* = g_*$. A basepoint-preserving homotopy between $f$ and $g$ is a continuous map $H: X \times [0, 1] \to Y$ such that $H(x, 0) = f(x)$, $H(x, 1) = g(x)$, and $H(x_0, t) = y_0$ for all $t \in [0, 1]$. This homotopy $H$ can be used to construct a [path homotopy](@entry_id:149610) between any loop $f \circ \alpha$ and $g \circ \alpha$, demonstrating that $[f \circ \alpha] = [g \circ \alpha]$ in $\pi_1(Y, y_0)$.

A direct and important consequence arises when a map $f$ is basepoint-preservingly homotopic to the identity map $\text{id}_X$. In this case, the homotopy invariance theorem implies that $f_* = (\text{id}_X)_*$. As we saw from the functorial properties, $(\text{id}_X)_*$ is the identity homomorphism on $\pi_1(X, x_0)$. Therefore, if $f \simeq \text{id}_X$ relative to the basepoint, then $f_*$ is the identity homomorphism [@problem_id:1558596].

The concept of the **degree** of a map from the circle to itself provides a concrete example of this principle. The fundamental group $\pi_1(S^1, 1)$ is isomorphic to the integers $\mathbb{Z}$. For any map $h: (S^1, 1) \to (S^1, 1)$, the [induced homomorphism](@entry_id:149311) $h_*: \mathbb{Z} \to \mathbb{Z}$ must be of the form $n \mapsto kn$ for some integer $k$. This integer $k$ is defined as the degree of $h$. The homotopy invariance theorem tells us that any two maps that are homotopic relative to the basepoint must have the same degree, as they induce the same homomorphism [@problem_id:1558642].

### Applications of Induced Homomorphisms

The principles of [functoriality](@entry_id:150069) and homotopy invariance are the engine that drives many classical results in algebraic topology. They allow us to translate [topological properties](@entry_id:154666) of spaces and maps into algebraic statements about groups and homomorphisms.

#### Homeomorphisms and Topological Invariance

The most fundamental application is to show that the fundamental group is a topological invariant. If two spaces $X$ and $Y$ are homeomorphic, there exists a [homeomorphism](@entry_id:146933) $f: (X, x_0) \to (Y, y_0)$ with a continuous inverse $g: (Y, y_0) \to (X, x_0)$. By definition, $g \circ f = \text{id}_X$ and $f \circ g = \text{id}_Y$. Applying the [functoriality](@entry_id:150069) property, we get:
$$g_* \circ f_* = (g \circ f)_* = (\text{id}_X)_* = \text{id}_{\pi_1(X, x_0)}$$
$$f_* \circ g_* = (f \circ g)_* = (\text{id}_Y)_* = \text{id}_{\pi_1(Y, y_0)}$$
These equations show that $f_*$ and $g_*$ are group isomorphisms, each being the inverse of the other. Therefore, if $X$ and $Y$ are homeomorphic, their fundamental groups $\pi_1(X, x_0)$ and $\pi_1(Y, y_0)$ must be isomorphic [@problem_id:1558612]. This gives us a powerful tool: to prove that two spaces are *not* homeomorphic, we can simply show that their fundamental groups are not isomorphic.

#### Retractions and Surjectivity

A **retraction** is a continuous map $r: X \to A$ from a space to a subspace $A \subseteq X$ such that $r(a) = a$ for all $a \in A$. Let $i: A \hookrightarrow X$ be the inclusion map. The defining property of a retraction can be stated as $r \circ i = \text{id}_A$. If we choose a basepoint $a_0 \in A$, we can consider the [induced homomorphisms](@entry_id:266478) on fundamental groups. Applying the [functoriality](@entry_id:150069) property to the retraction equation gives:
$$(r \circ i)_* = r_* \circ i_* = (\text{id}_A)_* = \text{id}_{\pi_1(A, a_0)}$$
In group theory, if a homomorphism $g: G \to H$ has a [right inverse](@entry_id:161498) (a homomorphism $h: H \to G$ such that $g \circ h = \text{id}_H$), then $g$ must be surjective. In our case, $r_*$ has the [right inverse](@entry_id:161498) $i_*$, so we can conclude that the homomorphism $r_*: \pi_1(X, a_0) \to \pi_1(A, a_0)$ is always surjective [@problem_id:1558608]. This result is a key ingredient in proving famous theorems, such as the impossibility of retracting a disk onto its boundary circle, which in turn leads to a proof of the Brouwer [fixed-point theorem](@entry_id:143811).

#### Covering Maps and Injectivity

Another class of maps with a special relationship to fundamental groups are **[covering maps](@entry_id:169347)**. A map $p: \tilde{X} \to X$ is a covering map if every point in $X$ has an open neighborhood that is "evenly covered" by a disjoint union of open sets in $\tilde{X}$. One of the most important theorems in the theory of [covering spaces](@entry_id:152318) states that if the [covering space](@entry_id:139261) $\tilde{X}$ is path-connected, the [induced homomorphism](@entry_id:149311) $p_*: \pi_1(\tilde{X}, \tilde{x}_0) \to \pi_1(X, x_0)$ is always **injective** [@problem_id:1558630].

The intuition behind this result lies in the unique lifting properties of [covering spaces](@entry_id:152318). If a loop $\gamma$ in the covering space $\tilde{X}$ has the property that its projection $p \circ \gamma$ is [null-homotopic](@entry_id:153762) in the base space $X$, the homotopy [lifting property](@entry_id:156717) guarantees that the null-homotopy in $X$ can be lifted to a null-homotopy of $\gamma$ in $\tilde{X}$. This means that if an element $[\gamma]$ is in the kernel of $p_*$, it must have been the identity element to begin with. The injectivity of $p_*$ establishes a deep connection between the subgroups of $\pi_1(X, x_0)$ and the various [covering spaces](@entry_id:152318) of $X$.

### The Interplay of Geometry and Algebra

The [induced homomorphism](@entry_id:149311) provides a dictionary for translating between the geometric properties of maps and the algebraic properties of groups. Understanding this dictionary is key to applying algebraic topology effectively.

#### The Trivial Homomorphism and The Extension Problem

As we have seen, the constant map induces the trivial homomorphism. A more profound question is the converse: if an [induced homomorphism](@entry_id:149311) $f_*$ is trivial, what does this imply about the map $f$?

Consider a map $f: (S^1, s_0) \to (Y, y_0)$. The fundamental group $\pi_1(S^1, s_0)$ is isomorphic to $\mathbb{Z}$ and is generated by the homotopy class of a loop $\gamma$ that traverses the circle once. The [induced homomorphism](@entry_id:149311) $f_*$ is completely determined by where it sends this generator: $f_*([\gamma]) = [f \circ \gamma]$. If $f_*$ is the trivial homomorphism, this means it maps the generator $[\gamma]$ to the [identity element](@entry_id:139321) in $\pi_1(Y, y_0)$. This is equivalent to saying that the loop in $Y$ defined by the map $f$ is [null-homotopic](@entry_id:153762) [@problem_id:1558603].

This algebraic condition has a direct geometric interpretation related to the **[extension problem](@entry_id:150521)**. Can the map $f: S^1 \to Y$ be continuously extended to a map $F: D^2 \to Y$ defined on the entire [closed disk](@entry_id:148403)? A fundamental theorem states that such an extension exists if and only if the map $f$ is [null-homotopic](@entry_id:153762) (homotopic to a constant map). Combining these facts, we arrive at a powerful conclusion:
A [continuous map](@entry_id:153772) $f: S^1 \to Y$ can be extended to the disk $D^2$ if and only if the [induced homomorphism](@entry_id:149311) $f_*: \pi_1(S^1, s_0) \to \pi_1(Y, f(s_0))$ is the trivial homomorphism [@problem_id:1558640]. This theorem brilliantly converts a geometric [extension problem](@entry_id:150521) into an algebraic calculation.

#### A Cautionary Note: Map Properties vs. Homomorphism Properties

It is natural to wonder if [topological properties](@entry_id:154666) of a map $f$ translate directly to algebraic properties of $f_*$. For instance, if $f$ is injective, must $f_*$ also be injective? The answer is a firm no, and this subtlety is a source of the theory's power.

Consider the inclusion map $f: S^1 \to D^2$ that embeds the circle as the boundary of the [closed disk](@entry_id:148403). This map is clearly injective. However, the [induced homomorphism](@entry_id:149311) is $f_*: \pi_1(S^1) \to \pi_1(D^2)$. We know that $\pi_1(S^1) \cong \mathbb{Z}$ and, because the disk is contractible, $\pi_1(D^2)$ is the trivial group $\{e\}$. The homomorphism $f_*: \mathbb{Z} \to \{e\}$ must send every integer to the [identity element](@entry_id:139321). This map is far from injective; its kernel is the entire group $\mathbb{Z}$ [@problem_id:1558629].

This example demonstrates that the [induced homomorphism](@entry_id:149311) captures information not about the point-set properties of the map, but about how the map transforms the "loop structure" of the domain space within the [codomain](@entry_id:139336) space. The fact that an [injective map](@entry_id:262763) can induce a non-[injective homomorphism](@entry_id:143562) is precisely the phenomenon that allows us to prove results like the non-existence of a retraction from $D^2$ to $S^1$. The [induced homomorphism](@entry_id:149311) is a sophisticated tool that distills specific, often non-obvious, topological information into an algebraic form.