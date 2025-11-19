## Introduction
In abstract algebra and topology, the $\operatorname{Hom}$ [functor](@entry_id:260898), $\operatorname{Hom}(A, B)$, is an indispensable tool for studying the structure-preserving maps between algebraic objects. However, its power is limited by a fundamental property: it is only left-exact. This means that when applied to a [short exact sequence](@entry_id:137930), the $\operatorname{Hom}$ functor preserves exactness at the beginning of the sequence but not necessarily at the end. This failure of full [exactness](@entry_id:268999) represents a loss of information, raising a critical question: can we systematically measure and understand what is lost?

The $\operatorname{Ext}$ [functor](@entry_id:260898) emerges from the field of [homological algebra](@entry_id:155139) as the precise answer to this question. It is the first in a series of "derived [functors](@entry_id:150427)" designed to repair the inexactness of the $\operatorname{Hom}$ [functor](@entry_id:260898), turning its failure into a source of deep structural insight. This article provides a comprehensive introduction to the $\operatorname{Ext}$ [functor](@entry_id:260898) for undergraduate students of mathematics.

Across the following chapters, you will embark on a journey to understand this powerful concept.
* In **Principles and Mechanisms**, we will construct the $\operatorname{Ext}$ groups using projective resolutions, explore their connection to the classification of [module extensions](@entry_id:268265), and unpack the power of the [long exact sequence](@entry_id:153438) they generate.
* In **Applications and Interdisciplinary Connections**, we will see the $\operatorname{Ext}$ functor in action, revealing how it unlocks the torsion structure of cohomology groups in algebraic topology via the Universal Coefficient Theorem and serves as a foundation for [group cohomology](@entry_id:144845).
* Finally, **Hands-On Practices** will guide you through essential computations, solidifying your theoretical knowledge and building practical skill.

We begin by examining the core principles that motivate the construction of the $\operatorname{Ext}$ [functor](@entry_id:260898) and the mechanisms by which it is defined.

## Principles and Mechanisms

In the study of modules and chain complexes, the $\operatorname{Hom}$ [functor](@entry_id:260898), $\operatorname{Hom}_R(A, B)$, plays a central role. For a fixed $R$-module $B$, the [functor](@entry_id:260898) $\operatorname{Hom}_R(-, B)$ is contravariant and left-exact. This means that for any [short exact sequence](@entry_id:137930) of $R$-modules $0 \to A \to B \to C \to 0$, applying the [functor](@entry_id:260898) yields a sequence $0 \to \operatorname{Hom}_R(C, B) \to \operatorname{Hom}_R(B, B) \to \operatorname{Hom}_R(A, B)$ which is exact. However, this [exactness](@entry_id:268999) does not generally extend further; the map $\operatorname{Hom}_R(B, B) \to \operatorname{Hom}_R(A, B)$ is not always surjective. Homological algebra provides a systematic way to measure this failure of exactness through the construction of "derived functors." The $\operatorname{Ext}$ [functor](@entry_id:260898), $\operatorname{Ext}^n_R(A, B)$, is the collection of right derived functors of the $\operatorname{Hom}$ functor.

### The Construction of Ext via Projective Resolutions

The most common and direct method for defining the $\operatorname{Ext}$ groups involves the concept of a **[projective resolution](@entry_id:154686)**. For any $R$-module $A$, a [projective resolution](@entry_id:154686) is a long exact sequence of the form:
$$ \cdots \xrightarrow{d_3} P_2 \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} A \to 0 $$
where each $P_i$ is a projective $R$-module. The existence of such a resolution for any module is a foundational result in [homological algebra](@entry_id:155139).

To compute the groups $\operatorname{Ext}^n_R(A, B)$, we perform a three-step process:

1.  **Truncate:** We take the [projective resolution](@entry_id:154686) of $A$ and remove the module $A$ itself, leaving us with a [chain complex](@entry_id:150246) of [projective modules](@entry_id:149251), denoted $P_\bullet$:
    $$ \cdots \xrightarrow{d_3} P_2 \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \to 0 $$

2.  **Apply Hom:** We apply the contravariant [functor](@entry_id:260898) $\operatorname{Hom}_R(-, B)$ to this complex. Since the [functor](@entry_id:260898) is contravariant, it reverses the direction of all the maps, transforming our [chain complex](@entry_id:150246) into a **[cochain](@entry_id:275805) complex**:
    $$ 0 \to \operatorname{Hom}_R(P_0, B) \xrightarrow{d_1^*} \operatorname{Hom}_R(P_1, B) \xrightarrow{d_2^*} \operatorname{Hom}_R(P_2, B) \xrightarrow{d_3^*} \cdots $$
    The maps in this new complex are the **coboundary maps**, denoted $d_n^*$, which are induced by the original differentials $d_n$. Specifically, for a homomorphism $\phi: P_{n-1} \to B$, the map $d_n^*(\phi)$ is the composition $\phi \circ d_n$. The property $d_n \circ d_{n+1} = 0$ in the original resolution implies that $d_{n+1}^* \circ d_n^* = 0$, which is the necessary condition for this sequence to be a [cochain](@entry_id:275805) complex.

3.  **Take Cohomology:** The $n$-th $\operatorname{Ext}$ group, $\operatorname{Ext}^n_R(A, B)$, is defined as the $n$-th cohomology group of this [cochain](@entry_id:275805) complex. The **$n$-[cocycles](@entry_id:160556)** are the elements of $\operatorname{Ker}(d_{n+1}^*)$, and the **$n$-[coboundaries](@entry_id:159416)** are the elements of $\operatorname{Im}(d_n^*)$. The $n$-th cohomology group is the quotient of these two:
    $$ \operatorname{Ext}^n_R(A, B) = H^n(\operatorname{Hom}_R(P_\bullet, B)) = \frac{\operatorname{Ker}(d_{n+1}^*)}{\operatorname{Im}(d_n^*)} $$
    By convention, $d_0^*$ is the zero map originating from the zero module, so its image is $\{0\}$. This entire procedure is encapsulated in the definition of the derived [functor](@entry_id:260898) [@problem_id:1681297].

Let us examine the first two $\operatorname{Ext}$ groups. For $n=0$, the definition gives:
$$ \operatorname{Ext}^0_R(A, B) = \frac{\operatorname{Ker}(d_1^*)}{\operatorname{Im}(d_0^*)} = \operatorname{Ker}(d_1^*) $$
A homomorphism $\phi \in \operatorname{Hom}_R(P_0, B)$ is in $\operatorname{Ker}(d_1^*)$ if and only if $\phi \circ d_1 = 0$. This means $\phi$ vanishes on the image of $d_1$. From the exactness of the original resolution, we know $\operatorname{Im}(d_1) = \operatorname{Ker}(\epsilon)$. So, $\phi$ is a map from $P_0$ to $B$ that is zero on $\operatorname{Ker}(\epsilon)$. By the universal property of quotient modules, such a $\phi$ factors uniquely through the projection $\epsilon: P_0 \to A$. This means there is a unique homomorphism $g: A \to B$ such that $\phi = g \circ \epsilon$. This establishes a [natural isomorphism](@entry_id:276379) between $\operatorname{Ker}(d_1^*)$ and $\operatorname{Hom}_R(A, B)$. Therefore, the zeroth $\operatorname{Ext}$ functor is not a new construction, but rather recovers the original $\operatorname{Hom}$ [functor](@entry_id:260898) [@problem_id:1681288]:
$$ \operatorname{Ext}^0_R(A, B) \cong \operatorname{Hom}_R(A, B) $$

For $n=1$, the definition yields the first "interesting" $\operatorname{Ext}$ group:
$$ \operatorname{Ext}^1_R(A, B) = \frac{\operatorname{Ker}(d_2^*)}{\operatorname{Im}(d_1^*)} $$
This group measures the extent to which [cocycles](@entry_id:160556) (maps $\psi: P_1 \to B$ with $\psi \circ d_2 = 0$) fail to be [coboundaries](@entry_id:159416) (maps of the form $\phi \circ d_1$ for some $\phi: P_0 \to B$).

A crucial theorem in [homological algebra](@entry_id:155139) states that the groups $\operatorname{Ext}^n_R(A, B)$ are independent of the choice of [projective resolution](@entry_id:154686) for $A$. An alternative, dual construction defines the same groups by taking an **[injective resolution](@entry_id:156320)** of the *second* argument, $B$, and applying the covariant [functor](@entry_id:260898) $\operatorname{Hom}_R(A, -)$.

### The Role of Projective and Injective Modules

The $\operatorname{Ext}$ [functors](@entry_id:150427) provide a powerful characterization of projective and [injective modules](@entry_id:154413). A module $P$ is projective if and only if the [functor](@entry_id:260898) $\operatorname{Hom}_R(P, -)$ is exact. Similarly, a module $I$ is injective if and only if the [functor](@entry_id:260898) $\operatorname{Hom}_R(-, I)$ is exact. The derived functors $\operatorname{Ext}^n$ measure the failure of this exactness.

The condition that $\operatorname{Hom}_R(-, I)$ is an exact functor is precisely equivalent to the statement that all its right derived functors for $n \ge 1$ vanish. Thus, we have a concise characterization of injectivity [@problem_id:1681261]:

> An $R$-module $I$ is **injective** if and only if $\operatorname{Ext}^1_R(M, I) = 0$ for all $R$-modules $M$.

Dually, using the alternative construction of $\operatorname{Ext}$ via an [injective resolution](@entry_id:156320) of the second argument, one can show a corresponding characterization for [projective modules](@entry_id:149251):

> An $R$-module $P$ is **projective** if and only if $\operatorname{Ext}^1_R(P, M) = 0$ for all $R$-modules $M$.

Since [free modules](@entry_id:152514) are projective, this implies that for any [free module](@entry_id:150200) $F$, $\operatorname{Ext}^1_R(F, M) = 0$ for any module $M$. For example, consider the ring $R = \mathbb{Z}/4\mathbb{Z}$ and let $P$ be the module $R$ itself. As a [free module](@entry_id:150200) of rank one, $P$ is projective. Consequently, for any $R$-module $M$, we must have $\operatorname{Ext}^1_R(P, M) = 0$. In contrast, a module like $N = \mathbb{Z}/2\mathbb{Z}$ over this ring is not projective, and we can indeed find modules $M$ for which $\operatorname{Ext}^1_R(N, M)$ is non-zero. For instance, a direct calculation shows that $\operatorname{Ext}^1_{\mathbb{Z}/4\mathbb{Z}}(\mathbb{Z}/2\mathbb{Z}, \mathbb{Z}/2\mathbb{Z}) \cong \mathbb{Z}/2\mathbb{Z}$ [@problem_id:1681325].

### Ext¹ and the Classification of Extensions

Beyond its formal definition, the group $\operatorname{Ext}^1_R(C, A)$ has a profound and intuitive meaning: it classifies **extensions**. A [short exact sequence](@entry_id:137930) of $R$-modules
$$ 0 \to A \xrightarrow{i} B \xrightarrow{p} C \to 0 $$
is called an **extension of $C$ by $A$**. The module $B$ can be thought of as being "built" from $A$ and $C$. Two extensions, $E_1: 0 \to A \to B_1 \to C \to 0$ and $E_2: 0 \to A \to B_2 \to C \to 0$, are considered **equivalent** if there exists a homomorphism $\beta: B_1 \to B_2$ making the following diagram commute:
$$
\begin{matrix}
0  \to  A  \xrightarrow{i_1}  B_1  \xrightarrow{p_1}  C  \to  0 \\
  \downarrow \text{id}_A   & \downarrow \beta   & \downarrow \text{id}_C   \\
0  \to  A  \xrightarrow{i_2}  B_2  \xrightarrow{p_2}  C  \to  0
\end{matrix}
$$
The Five Lemma implies that if such a $\beta$ exists, it must be an [isomorphism](@entry_id:137127).

The fundamental result is that there is a one-to-one correspondence between the set of [equivalence classes](@entry_id:156032) of extensions of $C$ by $A$ and the elements of the group $\operatorname{Ext}^1_R(C, A)$.

This correspondence can be made explicit. Given an extension $E$, one can find its corresponding element in $\operatorname{Ext}^1_R(C, A)$ by using a [projective resolution](@entry_id:154686) of $C$. For example, let's take the standard [free resolution](@entry_id:266531) of $C = \mathbb{Z}/n\mathbb{Z}$, which is $0 \to \mathbb{Z} \xrightarrow{\times n} \mathbb{Z} \xrightarrow{\epsilon} \mathbb{Z}/n\mathbb{Z} \to 0$. By lifting the projection map $\epsilon$ to the middle module of the extension $E$, we can construct a [1-cocycle](@entry_id:144864) whose cohomology class represents the extension [@problem_id:1681317].

Even more remarkably, the set of equivalence classes can be endowed with an abelian group structure, and this structure coincides with the group structure of $\operatorname{Ext}^1_R(C, A)$. The addition operation on extensions is known as the **Baer sum**. The sum of two extensions $[E_1]$ and $[E_2]$ is constructed through a sequence of pullback and pushout operations [@problem_id:1681268]. The [identity element](@entry_id:139321) of this group corresponds to the [equivalence class](@entry_id:140585) of the **[split short exact sequence](@entry_id:159775)**:
$$ 0 \to A \xrightarrow{j} A \oplus C \xrightarrow{q} C \to 0 $$
where $j(a) = (a,0)$ and $q(a,c) = c$. An extension is in this class if and only if it is split, meaning the map $p$ has a [right inverse](@entry_id:161498) (a section) or, equivalently, $i$ has a left inverse (a retraction). Adding the [split extension](@entry_id:143915) to any other extension $[E]$ via the Baer sum yields an extension equivalent to $[E]$ itself [@problem_id:1681268].

From the perspective of derived [functors](@entry_id:150427), the zero element of $\operatorname{Ext}^1_R(C, A)$ is the class of the zero [cocycle](@entry_id:200749), which is the class of all [coboundaries](@entry_id:159416). The correspondence between these two pictures is precise: the [cocycle](@entry_id:200749) constructed from a [split short exact sequence](@entry_id:159775) is always a coboundary [@problem_id:1793095].

### The Long Exact Sequence and the Connecting Homomorphism

The true power of derived functors is realized through the **long exact sequence**. Given any [short exact sequence](@entry_id:137930) of modules $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$ and any other module $G$, there is an induced [long exact sequence](@entry_id:153438) of $\operatorname{Ext}$ groups:
$$ 0 \to \operatorname{Hom}_R(C, G) \to \operatorname{Hom}_R(B, G) \to \operatorname{Hom}_R(A, G) \xrightarrow{\delta} \operatorname{Ext}^1_R(C, G) \to \operatorname{Ext}^1_R(B, G) \to \cdots $$
This sequence continues indefinitely through all the higher $\operatorname{Ext}$ groups. The most critical part of this sequence is the **[connecting homomorphism](@entry_id:160713)** $\delta$.

The map $\delta: \operatorname{Hom}_R(A, G) \to \operatorname{Ext}^1_R(C, G)$ is constructed via a diagram-chasing argument, often called the Snake Lemma. Given a homomorphism $\phi: A \to G$, the construction of its image $\delta(\phi)$ proceeds as follows [@problem_id:1681294]:
1.  Take a [projective resolution](@entry_id:154686) of $C$, $\cdots \to P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} C \to 0$.
2.  Since $P_0$ is projective and $g: B \to C$ is surjective, we can lift $\epsilon$ to a map $\beta: P_0 \to B$ such that $g \circ \beta = \epsilon$.
3.  Consider the composition $\beta \circ d_1: P_1 \to B$. One can show that its image lies in $\operatorname{Ker}(g) = \operatorname{Im}(f)$.
4.  Since $f$ is injective, there is a unique map $\gamma: P_1 \to A$ such that $f \circ \gamma = \beta \circ d_1$.
5.  Now, form the composition $\psi = \phi \circ \gamma: P_1 \to G$. This map $\psi$ can be shown to be a [1-cocycle](@entry_id:144864) (i.e., $\psi \circ d_2 = 0$).
6.  The image $\delta(\phi)$ is defined as the [cohomology class](@entry_id:263961) $[\psi] \in \operatorname{Ext}^1_R(C, G)$.

The [connecting homomorphism](@entry_id:160713) $\delta$ has a clear conceptual meaning: it measures the obstruction to lifting homomorphisms. The sequence $0 \to \operatorname{Hom}_R(C, G) \to \operatorname{Hom}_R(B, G) \to \operatorname{Hom}_R(A, G) \to 0$ is exact if and only if the [connecting homomorphism](@entry_id:160713) $\delta$ is the zero map. In other words, a homomorphism $\phi: A \to G$ is in the image of the map $f^*: \operatorname{Hom}_R(B, G) \to \operatorname{Hom}_R(A, G)$—meaning $\phi$ can be "lifted" to a map from $B$—if and only if $\delta(\phi) = 0$.

A classic example illustrates this perfectly. Consider the [short exact sequence](@entry_id:137930) of $\mathbb{Z}$-modules $0 \to \mathbb{Z} \xrightarrow{\times 2} \mathbb{Z} \xrightarrow{\text{mod }2} \mathbb{Z}/2\mathbb{Z} \to 0$. Let $G = \mathbb{Z}/2\mathbb{Z}$. A homomorphism $\phi: \mathbb{Z} \to \mathbb{Z}/2\mathbb{Z}$ can be lifted to $\mathbb{Z}$ if there exists $\psi: \mathbb{Z} \to \mathbb{Z}/2\mathbb{Z}$ such that $\phi(n) = \psi(2n)$. But $\psi(2n) = 2\psi(n) = 0$ in $\mathbb{Z}/2\mathbb{Z}$. Thus, only the zero homomorphism can be lifted. The non-zero homomorphism $\phi_1(n) = n \pmod 2$ cannot be lifted. The [long exact sequence](@entry_id:153438) predicts that its image, $\delta(\phi_1)$, must be a non-zero element in $\operatorname{Ext}^1_\mathbb{Z}(\mathbb{Z}/2\mathbb{Z}, \mathbb{Z}/2\mathbb{Z})$. This non-zero element corresponds to the unique [non-split extension](@entry_id:137632) of $\mathbb{Z}/2\mathbb{Z}$ by $\mathbb{Z}/2\mathbb{Z}$, which is $0 \to \mathbb{Z}/2\mathbb{Z} \to \mathbb{Z}/4\mathbb{Z} \to \mathbb{Z}/2\mathbb{Z} \to 0$ [@problem_id:1681267].

### Higher Ext Groups and the Yoneda Product

The groups $\operatorname{Ext}^n_R(C, A)$ for $n > 1$ also have a concrete interpretation: they classify **$n$-extensions**, which are long [exact sequences](@entry_id:151503) of the form $0 \to A \to M_{n-1} \to \cdots \to M_0 \to C \to 0$.

Furthermore, the $\operatorname{Ext}$ groups are related by a product structure known as the **Yoneda product**. This is a pairing
$$ \circ: \operatorname{Ext}^p_R(B, A) \times \operatorname{Ext}^q_R(C, B) \to \operatorname{Ext}^{p+q}_R(C, A) $$
which can be visualized as "[splicing](@entry_id:261283)" extensions together. For the case $p=q=1$, we can take an extension $e_A$ in $\operatorname{Ext}^1_R(B, A)$ and an extension $e_B$ in $\operatorname{Ext}^1_R(C, B)$:
$$ e_A: 0 \to A \xrightarrow{j} F \xrightarrow{q} B \to 0 $$
$$ e_B: 0 \to B \xrightarrow{i} E \xrightarrow{p} C \to 0 $$
The Yoneda product $[e_B] \circ [e_A]$ is the class of the 2-extension formed by composing the maps around the shared module $B$. Since $q$ is surjective and $i$ is injective, we can "splice" the sequences at $B$ to form a new long exact sequence:
$$ 0 \to A \xrightarrow{j} F \xrightarrow{i \circ q} E \xrightarrow{p} C \to 0 $$
This sequence is exact and represents the product element in $\operatorname{Ext}^2_R(C, A)$ [@problem_id:1681301]. This product endows the collection of all $\operatorname{Ext}$ groups with a rich algebraic structure that is fundamental to advanced topics in algebra and topology.