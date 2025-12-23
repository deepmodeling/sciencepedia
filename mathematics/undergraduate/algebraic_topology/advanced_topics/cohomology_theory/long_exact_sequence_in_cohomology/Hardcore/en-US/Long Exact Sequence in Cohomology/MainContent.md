## Introduction
The [long exact sequence](@entry_id:153438) in cohomology stands as one of the most powerful and ubiquitous tools in algebraic topology. It provides a foundational bridge between the geometric properties of topological spaces and the computable world of abstract algebra. Many fundamental questions in topology, such as distinguishing between different spaces or understanding their intricate structures, are computationally intractable without a systematic method to calculate their algebraic invariants. The [long exact sequence](@entry_id:153438) addresses this challenge by providing a rigid, predictable relationship between the cohomology groups of a space, a subspace, and the pair they form.

This article provides a comprehensive exploration of this essential tool. We will begin in the **Principles and Mechanisms** chapter by dissecting the algebraic construction of the sequence, with a special focus on the origin and function of the crucial [connecting homomorphism](@entry_id:160713). Next, the **Applications and Interdisciplinary Connections** chapter will shift from theory to practice, showcasing how the sequence is used to compute the cohomology of fundamental spaces like spheres, [projective spaces](@entry_id:157963), and knot complements, and revealing its connections to manifold theory and differential geometry. Finally, the **Hands-On Practices** section offers a series of guided problems to reinforce these concepts and develop practical computational skills. By navigating these chapters, the reader will gain a deep, functional understanding of the long exact sequence and its central role in modern mathematics.

## Principles and Mechanisms

The long exact sequence in cohomology for a pair of spaces $(X, A)$ is one of the most powerful and fundamental tools in algebraic topology. It provides a computable, algebraic linkage between the cohomology of a space $X$, a subspace $A$, and their [relative cohomology](@entry_id:272456). This sequence allows us to deduce information about one of these objects if we know information about the other two, turning topological problems into algebraic ones. In this chapter, we will dissect the principles that govern this sequence and the mechanisms that underpin its construction and application.

### The Long Exact Sequence of a Pair

For any pair of topological spaces $(X, A)$, where $A$ is a subspace of $X$, and any [abelian group](@entry_id:139381) $G$ of coefficients, there exists a **long exact sequence of cohomology groups**:

$$
\cdots \to H^{n-1}(A; G) \xrightarrow{\delta^{n-1}} H^n(X, A; G) \xrightarrow{j^*} H^n(X; G) \xrightarrow{i^*} H^n(A; G) \xrightarrow{\delta^n} H^{n+1}(X, A; G) \to \cdots
$$

This sequence extends infinitely in both directions. The maps in this sequence are group homomorphisms with specific origins:

*   The homomorphism $i^*: H^n(X; G) \to H^n(A; G)$ is the **restriction map**, induced by the inclusion map $i: A \hookrightarrow X$. Intuitively, it takes a cohomology class on the larger space $X$ and restricts its representative [cochains](@entry_id:159583) to the subspace $A$.

*   The homomorphism $j^*: H^n(X, A; G) \to H^n(X; G)$ is induced by the inclusion of pairs $j: (X, \emptyset) \hookrightarrow (X, A)$. It maps a [relative cohomology](@entry_id:272456) class to the absolute [cohomology class](@entry_id:263961) on $X$ obtained by "forgetting" the relative condition.

*   The homomorphism $\delta^n: H^n(A; G) \to H^{n+1}(X, A; G)$ is the **[connecting homomorphism](@entry_id:160713)** (or **[coboundary operator](@entry_id:162168)**). This map is the most remarkable feature of the sequence, as it increases degree by one and connects the cohomology of the subspace $A$ to the [relative cohomology](@entry_id:272456) of the pair.

The term **exact sequence** is a precise algebraic statement: at every group in the sequence, the image of the incoming homomorphism is exactly equal to the kernel of the outgoing homomorphism. For example, at the group $H^n(A; G)$, this means $\text{Im}(i^*) = \text{Ker}(\delta^n)$. This property is the source of the sequence's immense computational power.

### The Connecting Homomorphism: Construction and Mechanism

The existence and properties of the [connecting homomorphism](@entry_id:160713) $\delta^*$ are derived from a careful analysis at the level of [cochain](@entry_id:275805) complexes, often called a **diagram chase**. Understanding this construction is crucial to grasping how the sequence links the different cohomology groups.

The long exact sequence arises from a **[short exact sequence](@entry_id:137930) of [cochain](@entry_id:275805) complexes**:
$$
0 \to C^\bullet(X, A; G) \xrightarrow{j^\#} C^\bullet(X; G) \xrightarrow{i^\#} C^\bullet(A; G) \to 0
$$
Here, $C^n(X, A; G)$ is the group of relative $n$-[cochains](@entry_id:159583), which are [cochains](@entry_id:159583) on $X$ that vanish on any [singular simplex](@entry_id:265569) contained entirely in $A$. The map $i^\#$ is the restriction of [cochains](@entry_id:159583) from $X$ to $A$, and $j^\#$ is the inclusion of relative [cochains](@entry_id:159583) into the [cochains](@entry_id:159583) of $X$.

Let's trace the construction of $\delta^n: H^n(A; G) \to H^{n+1}(X, A; G)$:

1.  **Start with a class in $H^n(A; G)$**. Let $[\phi]$ be a cohomology class in $H^n(A; G)$, represented by an $n$-[cocycle](@entry_id:200749) $\phi \in C^n(A; G)$. A [cocycle](@entry_id:200749) is a [cochain](@entry_id:275805) whose coboundary is zero, so $d\phi = 0$.

2.  **Lift the representative [cocycle](@entry_id:200749)**. The map $i^\#: C^n(X; G) \to C^n(A; G)$ is surjective. This means we can always find an $n$-cochain $\Phi \in C^n(X; G)$ that restricts to $\phi$ on $A$, i.e., $i^\#(\Phi) = \phi$. This $\Phi$ is an extension of $\phi$ to the whole space $X$. Note that $\Phi$ itself is not necessarily a cocycle.

3.  **Take its coboundary**. We compute the coboundary of this extended [cochain](@entry_id:275805), $d\Phi \in C^{n+1}(X; G)$.

4.  **Show the result is a relative cocycle**. What is the restriction of $d\Phi$ to the subspace $A$? Using the fact that the [coboundary map](@entry_id:275313) $d$ commutes with the restriction map $i^\#$, we have $i^\#(d\Phi) = d(i^\#\Phi) = d\phi$. Since $\phi$ is a cocycle, $d\phi = 0$. This means that the cochain $d\Phi$ vanishes on all chains in $A$. By definition, this makes $d\Phi$ a **relative $(n+1)$-cocycle**, an element of $Z^{n+1}(X, A; G)$.

5.  **Define the image class**. The [connecting homomorphism](@entry_id:160713) $\delta^n$ is defined by mapping the original class $[\phi]$ to the class of this newly constructed relative [cocycle](@entry_id:200749): $\delta^n([\phi]) = [d\Phi] \in H^{n+1}(X, A; G)$.

One must verify that this construction is well-defined (i.e., independent of the choice of representative $\phi$ and extension $\Phi$), which is a standard result in [homological algebra](@entry_id:155139).

A core identity used in practical computations emerges from this construction. For any $(n+1)$-chain $c$ in $X$, the value of the [cocycle](@entry_id:200749) $d\Phi$ is given by Stokes' theorem for [cochains](@entry_id:159583): $(d\Phi)(c) = \Phi(\partial c)$. This provides a concrete method for calculating the effect of $\delta^*$.

Let's consider a practical example. Let $X$ be a solid 2-simplex $[v_0, v_1, v_2]$ and $A$ its boundary, a circle made of edges $e_0=[v_1, v_2]$, $e_1=[v_2, v_0]$, and $e_2=[v_0, v_1]$. Suppose we have a [1-cocycle](@entry_id:144864) $\phi \in Z^1(A; \mathbb{Z})$ defined by its values on the edges: $\phi(e_0)=2$, $\phi(e_1)=3$, and $\phi(e_2)=-1$. We want to find the image of its class $[\phi] \in H^1(A; \mathbb{Z})$ under the [connecting homomorphism](@entry_id:160713) $\delta^*: H^1(A; \mathbb{Z}) \to H^2(X, A; \mathbb{Z})$. Let $[\psi] = \delta^*([\phi])$. We can find the value of the representative [2-cocycle](@entry_id:146750) $\psi$ on the fundamental 2-chain $\sigma = [v_0, v_1, v_2]$.

Following the construction, $\psi$ is the coboundary $d\Phi$ of some 1-cochain $\Phi$ on $X$ that extends $\phi$. Using the Stokes' identity:
$$
\psi(\sigma) = (d\Phi)(\sigma) = \Phi(\partial \sigma)
$$
The boundary of the 2-[simplex](@entry_id:270623) is $\partial\sigma = [v_1, v_2] - [v_0, v_2] + [v_0, v_1]$. With the given edge definitions, this is $\partial\sigma = e_0 + e_1 + e_2$. Since $\Phi$ is an extension of $\phi$, its value on chains lying in $A$ is the same as $\phi$'s. Therefore:
$$
\psi(\sigma) = \Phi(e_0 + e_1 + e_2) = \Phi(e_0) + \Phi(e_1) + \Phi(e_2) = \phi(e_0) + \phi(e_1) + \phi(e_2)
$$
Substituting the given values, we find $\psi(\sigma) = 2 + 3 + (-1) = 4$. This calculation beautifully illustrates the mechanism of the [connecting homomorphism](@entry_id:160713), turning a question about a complex construction into a simple evaluation on a boundary.

### Properties and Applications of Exactness

The rigidity of the [long exact sequence](@entry_id:153438) is its main feature. The condition $\text{Im}(\text{in}) = \text{Ker}(\text{out})$ at each position leads to a host of powerful applications.

A map is an [isomorphism](@entry_id:137127) if and only if it is both injective (kernel is trivial) and surjective (image is the whole codomain). Using the property of [exactness](@entry_id:268999), we can establish a simple criterion for when a map in the sequence is an [isomorphism](@entry_id:137127). Consider the segment:
$$ \cdots \to H^k(X) \xrightarrow{i^*} H^k(A) \xrightarrow{\delta^*} H^{k+1}(X, A) \xrightarrow{j^*} H^{k+1}(X) \to \cdots $$
For $\delta^*: H^k(A) \to H^{k+1}(X, A)$ to be an isomorphism, it must be:
1.  **Injective**: $\text{Ker}(\delta^*) = \{0\}$. By [exactness](@entry_id:268999) at $H^k(A)$, $\text{Ker}(\delta^*) = \text{Im}(i^*)$. So, injectivity is equivalent to $\text{Im}(i^*) = \{0\}$, which means the map $i^*$ must be the zero map.
2.  **Surjective**: $\text{Im}(\delta^*) = H^{k+1}(X, A)$. By exactness at $H^{k+1}(X, A)$, $\text{Im}(\delta^*) = \text{Ker}(j^*)$. So, [surjectivity](@entry_id:148931) is equivalent to $\text{Ker}(j^*) = H^{k+1}(X, A)$, which means the map $j^*$ must be the zero map.

Thus, **the [connecting homomorphism](@entry_id:160713) $\delta^*$ is an isomorphism if and only if the two adjacent maps, $i^*$ and $j^*$, are both zero maps.** A common situation where this occurs is when the ambient space $X$ has trivial cohomology in the relevant degrees. For example, if $X$ is contractible, then $H^k(X; G) = 0$ for all $k > 0$. This immediately forces the adjacent maps $i^*$ and $j^*$ to be zero (as their domain or codomain is trivial), implying that $\delta^*$ is an [isomorphism](@entry_id:137127).

This provides a classic and fundamental computation. Consider the pair $(D^2, S^1)$, where $D^2$ is the [closed disk](@entry_id:148403) and $S^1$ is its boundary circle. The disk $D^2$ is contractible, so $H^1(D^2; \mathbb{Z}) = 0$ and $H^2(D^2; \mathbb{Z}) = 0$. The relevant segment of the [long exact sequence](@entry_id:153438) is:
$$ H^1(D^2; \mathbb{Z}) \to H^1(S^1; \mathbb{Z}) \xrightarrow{\delta^*} H^2(D^2, S^1; \mathbb{Z}) \to H^2(D^2; \mathbb{Z}) $$
Substituting the known groups gives:
$$ 0 \to \mathbb{Z} \xrightarrow{\delta^*} H^2(D^2, S^1; \mathbb{Z}) \to 0 $$
Exactness at $H^1(S^1)$ implies $\text{Ker}(\delta^*) = \text{Im}(0 \to \mathbb{Z}) = \{0\}$, so $\delta^*$ is injective. Exactness at $H^2(D^2, S^1)$ implies $\text{Im}(\delta^*) = \text{Ker}(H^2(D^2, S^1) \to 0) = H^2(D^2, S^1)$, so $\delta^*$ is surjective. Therefore, $\delta^*$ is an [isomorphism](@entry_id:137127), and we deduce the important result $H^2(D^2, S^1; \mathbb{Z}) \cong H^1(S^1; \mathbb{Z}) \cong \mathbb{Z}$.

The interplay between adjacent maps is a constant theme. For instance, if the restriction map $i^*: H^k(X) \to H^k(A)$ is surjective, then $\text{Im}(i^*) = H^k(A)$. By [exactness](@entry_id:268999), this means $\text{Ker}(\delta^k) = H^k(A)$, forcing the [connecting homomorphism](@entry_id:160713) $\delta^k$ to be the zero map. The sequence continues: if $\delta^k=0$, then at the next position, $\text{Ker}(j^*: H^{k+1}(X, A) \to H^{k+1}(X))$ must equal $\text{Im}(\delta^k) = \{0\}$. This implies that $j^*$ must be injective. Conversely, if $\delta^*$ is the zero map, its kernel is the entire domain, so exactness implies the preceding map $i^*$ must be surjective.

### Naturality and Structural Properties

The long exact sequence is not just a property of a single pair; it is a **natural** construction. This means that if we have a continuous map between pairs of spaces, $f: (X, A) \to (Y, B)$, which means $f(X) \subseteq Y$ and $f(A) \subseteq B$, then this map induces a "ladder" diagram connecting the two long [exact sequences](@entry_id:151503). Every square in this ladder commutes.

$$
\begin{array}{ccccccc}
\cdots \to  H^n(Y,B)  \to  H^n(Y)  \to  H^n(B)  \to \cdots \\
 \downarrow f_{rel}^*   \downarrow f_X^*   \downarrow f_A^*  \\
\cdots \to  H^n(X,A)  \to  H^n(X)  \to  H^n(A)  \to \cdots
\end{array}
$$

The commutativity of the square involving the [connecting homomorphism](@entry_id:160713), $\delta_X^* \circ f_A^* = f_{rel}^* \circ \delta_Y^*$, is a particularly powerful statement. It asserts that it does not matter whether we first map a class via $f$ and then cross the dimension bridge with $\delta^*$, or first cross the bridge and then map with $f^*$. This property ensures that the [connecting homomorphism](@entry_id:160713) is a geometric construction, not an arbitrary algebraic artifact. This can be verified, for instance, by considering the map $f(z) = \bar{z}$ on the pair $(S^1, \{1, -1\})$ and explicitly calculating the compositions.

A significant structural application of the [long exact sequence](@entry_id:153438) concerns **retracts**. A subspace $A$ is a retract of $X$ if there is a [continuous map](@entry_id:153772) $r: X \to A$ such that $r(a) = a$ for all $a \in A$. The composition $r \circ i$ is the identity on $A$. Applying the cohomology [functor](@entry_id:260898), we get $i^* \circ r^* = (r \circ i)^* = \text{id}$. This implies that the homomorphism $i^*: H^n(X; G) \to H^n(A; G)$ is surjective for all $n$ (it is a split epimorphism).

From our earlier analysis of [exactness](@entry_id:268999), if $i^*$ is surjective, the [connecting homomorphism](@entry_id:160713) $\delta^*$ must be the zero map. Since this holds for all degrees $n$, the entire [long exact sequence](@entry_id:153438) breaks apart into a collection of short [exact sequences](@entry_id:151503):
$$
0 \to H^n(X, A; G) \xrightarrow{j^*} H^n(X; G) \xrightarrow{i^*} H^n(A; G) \to 0
$$
For abelian groups, a [short exact sequence](@entry_id:137930) of this form that is "split" by the map $r^*$ implies that the middle group is a direct sum of the other two. We conclude that for a retract $A \subset X$,
$$
H^n(X; G) \cong H^n(A; G) \oplus H^n(X, A; G)
$$
This provides a profound connection between the topology of retraction and the algebraic structure of cohomology.

### Further Considerations

#### Reduced Cohomology
The long exact sequence can also be formulated for **[reduced cohomology](@entry_id:268050)**, denoted $\tilde{H}^*$. For a non-empty space $Y$, $\tilde{H}^n(Y) = H^n(Y)$ for $n > 0$, while $\tilde{H}^0(Y)$ is a subgroup of $H^0(Y)$. A key fact is that for a non-empty subspace $A \subset X$, the relative groups are unchanged, $H^n(X, A) \cong \tilde{H}^n(X, A)$. The sequence takes the form:
$$ \cdots \to \tilde{H}^{n-1}(A) \to H^n(X, A) \to \tilde{H}^n(X) \to \tilde{H}^n(A) \to \cdots $$
Since [reduced cohomology](@entry_id:268050) is trivial in negative degrees, $\tilde{H}^{-1}(A) = 0$. This means the sequence begins cleanly on the left:
$$ 0 \to H^0(X, A) \to \tilde{H}^0(X) \to \tilde{H}^0(A) \to H^1(X, A) \to \cdots $$

#### Cup Products and the Connecting Homomorphism
While the maps in the LES are group homomorphisms, they do not, in general, respect the ring structure given by the [cup product](@entry_id:159554). In particular, the [connecting homomorphism](@entry_id:160713) $\delta^*$ is **not a [ring homomorphism](@entry_id:153804)**. It is generally false that $\delta^*(u \cup v) = \delta^*(u) \cup \delta^*(v)$. A careful analysis shows this failure. For the pair $(X, A) = (D^2 \times T^2, S^1 \times T^2)$, one can find classes $u, v \in H^1(A)$ such that $\delta^*(u) \cup \delta^*(v) = 0$ while $\delta^*(u \cup v) \neq 0$. This happens because one of the classes, $v$, can be in the image of $i^*$, making $\delta^*(v)=0$, while the product $u \cup v$ is not, making $\delta^*(u \cup v)$ non-zero. The correct formula relating $\delta^*$ and the cup product is a Leibniz-type rule, which is more complex.

#### Relation to Homology
Finally, one might ask how the [long exact sequence](@entry_id:153438) in cohomology relates to its counterpart in homology. The Universal Coefficient Theorem (UCT) provides an algebraic formula connecting cohomology groups to homology groups, e.g., $H^n(X; R) \cong \text{Ext}_R(H_{n-1}(X; R), R) \oplus \text{Hom}_R(H_n(X; R), R)$ for a PID $R$. While this provides a group-by-group correspondence, it does not give rise to a natural map between the long [exact sequences](@entry_id:151503) themselves. The reason is that the isomorphism in the UCT relies on a "splitting" of a [short exact sequence](@entry_id:137930), and this splitting is **not natural**. This lack of [naturality](@entry_id:270302) prevents the construction of a functorial ladder diagram connecting the homology and cohomology long [exact sequences](@entry_id:151503), highlighting a deep and subtle aspect of the relationship between these two theories.