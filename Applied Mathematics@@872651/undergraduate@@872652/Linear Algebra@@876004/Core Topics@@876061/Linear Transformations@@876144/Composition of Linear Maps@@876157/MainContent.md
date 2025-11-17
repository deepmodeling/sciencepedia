## Introduction
In linear algebra, [linear maps](@entry_id:185132) are the fundamental tools for transforming vectors between spaces while preserving their core structure. But what happens when we apply one transformation after another? This sequential process, known as the **composition of linear maps**, is a powerful concept that allows us to construct complex, multi-stage operations from simpler building blocks. Understanding how to combine these maps and what properties the resulting composite map inherits is crucial for a deeper understanding of [linear systems](@entry_id:147850). This article systematically unpacks this operation, addressing how it is defined, how its properties are determined, and where it finds application.

The following chapters will guide you through this topic. In **Principles and Mechanisms**, we will establish the formal definition of composition, its connection to [matrix multiplication](@entry_id:156035), and its key algebraic properties. Next, **Applications and Interdisciplinary Connections** will showcase how this concept is applied in diverse fields from computer graphics to quantum physics. Finally, **Hands-On Practices** will provide concrete problems to solidify your understanding and apply these principles in practice.

## Principles and Mechanisms

In the study of linear algebra, linear maps transform vectors from one vector space to another while preserving the underlying structure of [vector addition and scalar multiplication](@entry_id:151375). A powerful concept emerges when we consider applying multiple transformations in sequence. This process, known as the **composition of linear maps**, allows us to construct complex operations from simpler ones and reveals deep algebraic and geometric properties. This chapter will systematically explore the principles governing composition, its representation by matrices, and its impact on the fundamental characteristics of [linear transformations](@entry_id:149133).

### The Definition and Condition for Composition

Let us consider three [vector spaces](@entry_id:136837), $U$, $V$, and $W$, over a common field $\mathbb{F}$. Suppose we have a [linear map](@entry_id:201112) $S: U \to V$ and another linear map $T: V \to W$. The output of the map $S$ is a vector in the space $V$, which is precisely the domain of the map $T$. This compatibility allows us to apply $T$ to the result of $S$.

The **composition** of $T$ and $S$, denoted $T \circ S$ (read as "T composed with S" or "T after S"), is the map from $U$ to $W$ defined by:
$$(T \circ S)(\mathbf{u}) = T(S(\mathbf{u})) \quad \text{for all } \mathbf{u} \in U$$

This definition implies a sequential process: for any vector $\mathbf{u}$ in $U$, we first apply the transformation $S$ to get a vector $S(\mathbf{u})$ in $V$. We then apply the transformation $T$ to this intermediate vector to obtain the final result, $T(S(\mathbf{u}))$, in $W$.

The most critical prerequisite for the composition $T \circ S$ to be well-defined is that the **codomain of $S$ must be identical to the domain of $T$**. If this condition is not met, the output of $S$ cannot serve as a valid input for $T$, and the composition is undefined.

For instance, consider a map $T: \mathbb{R}^2 \to \mathbb{R}^3$ and a map $S: \mathbb{R}^3 \to \mathbb{R}^3$ [@problem_id:1355107]. The composition $S \circ T$ is well-defined because the codomain of $T$, which is $\mathbb{R}^3$, matches the domain of $S$. The resulting composite map $S \circ T$ takes vectors from $\mathbb{R}^2$ and maps them to vectors in $\mathbb{R}^3$. However, the reverse composition, $T \circ S$, is not defined. The output of $S$ is a vector in $\mathbb{R}^3$, but the map $T$ requires an input from $\mathbb{R}^2$. This dimensional mismatch makes the sequence of operations impossible.

To see composition in action, consider a map $S$ from the space of quadratic polynomials $P_2(\mathbb{R})$ to $\mathbb{R}^3$, and a map $T$ from $\mathbb{R}^3$ to the space of linear polynomials $P_1(\mathbb{R})$ [@problem_id:1355092]. Let $p(x) = a_0 + a_1x + a_2x^2$ be a polynomial in $P_2(\mathbb{R})$ and $\mathbf{v} = (v_1, v_2, v_3)$ be a vector in $\mathbb{R}^3$. Suppose the maps are defined as:
$$S(p(x)) = (a_0 - a_2, 2a_1, a_0 + a_2)$$
$$T(\mathbf{v}) = v_3 + (v_1 + v_2)x$$

The composition $T \circ S$ maps a polynomial in $P_2(\mathbb{R})$ to a polynomial in $P_1(\mathbb{R})$. We can find a general formula for this composite map. For any $p(x) = a_0 + a_1x + a_2x^2$, the intermediate vector is $S(p(x)) = (a_0 - a_2, 2a_1, a_0 + a_2)$. Letting $v_1 = a_0 - a_2$, $v_2 = 2a_1$, and $v_3 = a_0 + a_2$, we apply $T$:
$$(T \circ S)(p(x)) = T(v_1, v_2, v_3) = v_3 + (v_1 + v_2)x = (a_0 + a_2) + ((a_0 - a_2) + 2a_1)x$$
Using this formula for a specific polynomial, such as $q(x) = 2 - 4x + 3x^2$ (where $a_0=2, a_1=-4, a_2=3$), we find the resulting polynomial is $(2+3) + ((2-3) + 2(-4))x = 5 - 9x$.

### Linearity and Matrix Representation of Compositions

A cornerstone result is that the composition of two [linear maps](@entry_id:185132) is itself a linear map. Let $S: U \to V$ and $T: V \to W$ be linear. To prove their composition $L = T \circ S$ is linear, we must verify that it preserves [vector addition and scalar multiplication](@entry_id:151375).

1.  **Additivity**: For any vectors $\mathbf{u}_1, \mathbf{u}_2 \in U$:
    \begin{align*}
    L(\mathbf{u}_1 + \mathbf{u}_2)  &= T(S(\mathbf{u}_1 + \mathbf{u}_2))  \quad \text{(by definition of } L\text{)} \\
     &= T(S(\mathbf{u}_1) + S(\mathbf{u}_2))  \quad \text{(since } S \text{ is linear)} \\
     &= T(S(\mathbf{u}_1)) + T(S(\mathbf{u}_2))  \quad \text{(since } T \text{ is linear)} \\
     &= L(\mathbf{u}_1) + L(\mathbf{u}_2)
    \end{align*}

2.  **Homogeneity**: For any vector $\mathbf{u} \in U$ and scalar $c \in \mathbb{F}$:
    \begin{align*}
    L(c\mathbf{u})  &= T(S(c\mathbf{u}))  \quad \text{(by definition of } L\text{)} \\
     &= T(c S(\mathbf{u}))  \quad \text{(since } S \text{ is linear)} \\
     &= c T(S(\mathbf{u}))  \quad \text{(since } T \text{ is linear)} \\
     &= c L(\mathbf{u})
    \end{align*}

Since both conditions hold, $T \circ S$ is a linear map. This [closure property](@entry_id:136899) is fundamental, ensuring that building complex maps from simple linear ones retains the desirable structure of linearity.

This theoretical result has a powerful computational counterpart. If we represent [linear maps](@entry_id:185132) between [finite-dimensional vector spaces](@entry_id:265491) by matrices, the composition of maps corresponds to the multiplication of their matrices. Specifically, if $S: U \to V$ is represented by matrix $M_S$ and $T: V \to W$ is represented by matrix $M_T$ (with respect to some chosen bases), then the composite map $L = T \circ S: U \to W$ is represented by the matrix product $M_L = M_T M_S$. The order of matrix multiplication is crucial and is the reverse of the order of application of the maps. This is not an arbitrary convention; it arises directly from the definition of composition. Applying $S$ to a vector $\mathbf{u}$ is equivalent to the [matrix-vector product](@entry_id:151002) $M_S \mathbf{u}$. Applying $T$ to the result is $M_T (M_S \mathbf{u})$. Due to the [associativity](@entry_id:147258) of matrix multiplication, this is equal to $(M_T M_S) \mathbf{u}$, revealing that the matrix for the composite map is indeed $M_T M_S$.

This principle allows us to analyze complex chains of transformations. Consider a signal processing system where a signal in $\mathbb{R}^2$ passes through three stages: $R: \mathbb{R}^2 \to \mathbb{R}^3$, $S: \mathbb{R}^3 \to \mathbb{R}^2$, and $T: \mathbb{R}^2 \to \mathbb{R}^2$, with the final transformation being $L = T \circ S \circ R$ [@problem_id:1355078]. If the matrices for these maps are $M_R$, $M_S$, and $M_T$, respectively, the matrix for the overall transformation $L$ is given by $M_L = M_T M_S M_R$.

The principle extends to [abstract vector spaces](@entry_id:155811), provided we fix bases for them. For example, let's find the [matrix representation](@entry_id:143451) of a composite map $L = T \circ S$, where $S: \mathbb{R}^2 \to \mathcal{P}_3$ (space of cubic polynomials) and $T: \mathcal{P}_3 \to M_{2 \times 2}$ (space of $2 \times 2$ matrices) [@problem_id:1355130]. We can find the matrix for $L$ by determining its action on the [standard basis vectors](@entry_id:152417) of the initial domain, $\mathbb{R}^2$. For each [basis vector](@entry_id:199546) $\mathbf{e}_i$, we compute the final output $L(\mathbf{e}_i) = T(S(\mathbf{e}_i))$ and express this output matrix as a [coordinate vector](@entry_id:153319) with respect to the standard basis of the final codomain, $M_{2 \times 2}$. These coordinate vectors then form the columns of the [matrix representation](@entry_id:143451) of $L$.

### Key Algebraic Properties

The operation of composition endows sets of [linear maps](@entry_id:185132) with a rich algebraic structure, characterized by several key properties.

#### Associativity
Composition of [linear maps](@entry_id:185132) is **associative**. Given three compatible linear maps, $R: U \to V$, $S: V \to W$, and $T: W \to Z$, the following equality holds:
$$T \circ (S \circ R) = (T \circ S) \circ R$$
This means that when composing three or more maps, the order in which we group them for computation does not affect the final result. For any $\mathbf{u} \in U$, both sides of the equation yield $T(S(R(\mathbf{u})))$. This property is directly inherited by [matrix multiplication](@entry_id:156035), which is also associative: $M_T (M_S M_R) = (M_T M_S) M_R$ [@problem_id:1355078]. This is extremely useful, as it allows us to pre-calculate the matrix for a portion of a transformation chain, simplifying subsequent computations.

#### Non-Commutativity
While associative, composition is **not commutative** in general. That is, for two maps $S: V \to V$ and $T: V \to V$, it is typically the case that $T \circ S \neq S \circ T$. The order of operations matters profoundly.

A clear demonstration of this can be found in 2D computer graphics [@problem_id:1355097]. Let $S$ be a horizontal [shear transformation](@entry_id:151272) defined by $S(x, y) = (x + 2y, y)$, and let $T$ be a counter-clockwise rotation by $90$ degrees, $T(x, y) = (-y, x)$. Let's apply these transformations to the point $\mathbf{v} = (1, 1)$.

1.  Applying $T$ then $S$ (composition $S \circ T$):
    - First, rotation: $T(1, 1) = (-1, 1)$.
    - Then, shear: $S(-1, 1) = (-1 + 2(1), 1) = (1, 1)$.
    The result is $(S \circ T)(\mathbf{v}) = (1, 1)$.

2.  Applying $S$ then $T$ (composition $T \circ S$):
    - First, shear: $S(1, 1) = (1 + 2(1), 1) = (3, 1)$.
    - Then, rotation: $T(3, 1) = (-1, 3)$.
    The result is $(T \circ S)(\mathbf{v}) = (-1, 3)$.

The final points are different, confirming that $S \circ T \neq T \circ S$. This non-commutativity is a crucial feature in many applications, from robotics to quantum mechanics, where the sequence of operations determines the outcome.

#### Inverses of Compositions
If a [linear map](@entry_id:201112) $T: V \to V$ is invertible, its inverse $T^{-1}: V \to V$ "undoes" its action, such that $T \circ T^{-1} = T^{-1} \circ T = I_V$, where $I_V$ is the identity map on $V$. What, then, is the inverse of a composition of two invertible maps, $S$ and $T$?

The inverse of the composition $T \circ S$ is given by the composition of the inverses in the reverse order:
$$(T \circ S)^{-1} = S^{-1} \circ T^{-1}$$

This is often called the "socks and shoes rule": to undo the process of putting on socks then shoes, you must first take off the shoes, then the socks. We can verify this formula by checking that it acts as a true inverse [@problem_id:1355103]:
$$(S^{-1} \circ T^{-1}) \circ (T \circ S) = S^{-1} \circ (T^{-1} \circ T) \circ S = S^{-1} \circ I_V \circ S = S^{-1} \circ S = I_V$$
A similar calculation shows that $(T \circ S) \circ (S^{-1} \circ T^{-1}) = I_V$. This property is essential for [solving systems of linear equations](@entry_id:136676) and for understanding groups of transformations.

### Composition, Subspaces, and Dimensionality

The act of composition has profound implications for the [fundamental subspaces](@entry_id:190076) associated with [linear maps](@entry_id:185132)—the image (range) and the kernel ([null space](@entry_id:151476))—and consequently affects properties like [injectivity](@entry_id:147722), [surjectivity](@entry_id:148931), and rank.

#### Injectivity and Surjectivity
The properties of injectivity (one-to-one) and [surjectivity](@entry_id:148931) (onto) of a composite map are related to those of its constituent maps.

- **Surjectivity**: If $S: U \to V$ and $T: V \to W$ are both surjective, their composition $L = T \circ S$ is also surjective. To prove this, we must show that for any vector $\mathbf{w} \in W$, there exists a vector $\mathbf{u} \in U$ such that $L(\mathbf{u}) = \mathbf{w}$. Since $T$ is surjective, there is a $\mathbf{v} \in V$ such that $T(\mathbf{v}) = \mathbf{w}$. Since $S$ is surjective, there is a $\mathbf{u} \in U$ such that $S(\mathbf{u}) = \mathbf{v}$. Combining these, we find $L(\mathbf{u}) = T(S(\mathbf{u})) = T(\mathbf{v}) = \mathbf{w}$, proving $L$ is surjective [@problem_id:1355116].

- **Injectivity**: If $S: U \to V$ and $T: V \to W$ are both injective, their composition $T \circ S$ is also injective. Furthermore, if a composition $T \circ S$ is known to be injective, then the first map applied, $S$, must be injective. This is because if $S(\mathbf{u}_1) = S(\mathbf{u}_2)$, then applying $T$ gives $T(S(\mathbf{u}_1)) = T(S(\mathbf{u}_2))$, which means $(T \circ S)(\mathbf{u}_1) = (T \circ S)(\mathbf{u}_2)$. By the [injectivity](@entry_id:147722) of $T \circ S$, it must be that $\mathbf{u}_1 = \mathbf{u}_2$.

#### Rank of a Composition
The dimension of the [image of a linear map](@entry_id:204818) is its **rank**. The rank of a composition is constrained by the ranks of the individual maps. The image of the composition $T \circ S$ is the set of all vectors $T(S(\mathbf{u}))$ for $\mathbf{u} \in U$. This is simply the image under $T$ of the subspace $\text{Im}(S)$. Therefore, $\text{Im}(T \circ S) = T(\text{Im}(S))$.

From this, it follows that the dimension of the image of the composition cannot exceed the dimension of the image of $S$: $\text{rank}(T \circ S) \le \text{rank}(S)$. Also, since the image of $T \circ S$ is a subspace of the image of $T$, its dimension cannot exceed the rank of $T$: $\text{rank}(T \circ S) \le \text{rank}(T)$. Combining these gives a powerful inequality:
$$\text{rank}(T \circ S) \le \min\{\text{rank}(T), \text{rank}(S)\}$$

This result has important consequences. For example, if we compose a map $T: \mathbb{R}^2 \to \mathbb{R}^3$ with a map $S: \mathbb{R}^3 \to \mathbb{R}^2$ whose rank is known to be 1, the composite map $L = T \circ S: \mathbb{R}^3 \to \mathbb{R}^3$ must have a rank of at most 1 [@problem_id:1355083]. A [linear map](@entry_id:201112) from $\mathbb{R}^3$ to itself with a rank less than 3 cannot be invertible. A key property of square matrices is that a matrix is invertible if and only if its determinant is non-zero. Therefore, the [matrix representation](@entry_id:143451) of $L$ must have a determinant of zero, regardless of the specific map $T$.

#### Image and Kernel Relationship
A particularly insightful relationship emerges when the composition of two non-zero maps results in the zero map. Suppose $S: U \to V$ and $T: V \to W$ are linear maps such that $T \circ S = 0$, meaning $(T \circ S)(\mathbf{u}) = \mathbf{0}_W$ for all $\mathbf{u} \in U$.

Let's analyze what this implies [@problem_id:1355132]. Take any vector $\mathbf{v}$ in the image of $S$, denoted $\text{Im}(S)$. By definition of the image, there exists some $\mathbf{u} \in U$ such that $\mathbf{v} = S(\mathbf{u})$. Now, let's apply the map $T$ to this vector $\mathbf{v}$:
$$T(\mathbf{v}) = T(S(\mathbf{u})) = (T \circ S)(\mathbf{u})$$
Since we are given that $T \circ S$ is the zero map, we have $(T \circ S)(\mathbf{u}) = \mathbf{0}_W$. Thus, $T(\mathbf{v}) = \mathbf{0}_W$. But the condition $T(\mathbf{v}) = \mathbf{0}_W$ is precisely the definition of $\mathbf{v}$ being in the kernel of $T$, denoted $\text{Ker}(T)$. Since we chose an arbitrary vector $\mathbf{v}$ from $\text{Im}(S)$ and showed it must belong to $\text{Ker}(T)$, we have established a fundamental inclusion:
$$\text{Im}(S) \subseteq \text{Ker}(T)$$

This relationship states that the entire output space of the first map $S$ is "annihilated" or "killed" by the second map $T$. This concept is a cornerstone of advanced topics in mathematics such as homology theory, where sequences of maps with this property, known as chain complexes, are used to study the structure of topological spaces.

In summary, the composition of linear maps is a fundamental operation that builds complexity from simplicity. Its properties—[associativity](@entry_id:147258), [non-commutativity](@entry_id:153545), and its interplay with matrices, inverses, and [fundamental subspaces](@entry_id:190076)—provide a rich framework for understanding and manipulating linear systems across science and engineering.