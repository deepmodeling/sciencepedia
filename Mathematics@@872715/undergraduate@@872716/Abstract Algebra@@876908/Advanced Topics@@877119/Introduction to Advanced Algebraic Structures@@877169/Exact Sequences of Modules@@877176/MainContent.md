## Introduction
While the theory of modules over a ring generalizes the familiar structure of vector spaces, it introduces a landscape of far greater complexity. To navigate this intricate world, mathematicians have developed elegant and powerful tools, with the concept of an [exact sequence](@entry_id:149883) being among the most fundamental. An [exact sequence](@entry_id:149883) provides a concise language for describing the relationships between submodules, quotient modules, and the internal structure of modules themselves. It addresses the core problem of how to precisely articulate and analyze the ways a module can be built from or broken down into simpler components.

This article serves as a comprehensive introduction to this vital concept. Across the following chapters, you will gain a deep understanding of both the theory and its practical applications.
*   **Chapter 1: Principles and Mechanisms** lays the groundwork, starting with the definition of [exactness](@entry_id:268999), the central role of short [exact sequences](@entry_id:151503), and pivotal results like the Splitting Lemma and the Snake Lemma.
*   **Chapter 2: Applications and Interdisciplinary Connections** demonstrates the power of [exact sequences](@entry_id:151503) in action, showing how they are used for the structural analysis of modules, the development of [homological algebra](@entry_id:155139) through derived functors like Ext and Tor, and how they forge connections to fields like representation theory and algebraic geometry.
*   **Chapter 3: Hands-On Practices** offers curated problems to solidify your understanding, guiding you from verifying basic definitions to applying the theory to prove structural properties of modules.

## Principles and Mechanisms

The theory of modules over a ring generalizes the familiar structure of [vector spaces](@entry_id:136837) over a field. However, the landscape of modules is vastly richer and more complex. To navigate this landscape, algebraists have developed powerful tools, among which the concept of an [exact sequence](@entry_id:149883) stands out for its elegance and utility. An [exact sequence](@entry_id:149883) is a sequence of modules and homomorphisms that provides a framework for relating submodules, quotient modules, and the structure of modules themselves. This chapter will lay out the fundamental principles of [exact sequences](@entry_id:151503), from their basic definition to their more profound applications in [homological algebra](@entry_id:155139).

### The Definition of Exactness

At its heart, an [exact sequence](@entry_id:149883) is a chain of module homomorphisms linked by a simple but powerful condition. Consider a sequence of $R$-modules and $R$-module homomorphisms:

$$ \dots \xrightarrow{f_{i-2}} M_{i-1} \xrightarrow{f_{i-1}} M_i \xrightarrow{f_i} M_{i+1} \xrightarrow{f_{i+1}} \dots $$

For any module $M_i$ in this sequence, there is an incoming homomorphism $f_{i-1}$ and an outgoing homomorphism $f_i$. The **kernel** of the outgoing map, $\ker(f_i)$, is the submodule of $M_i$ consisting of elements that are mapped to the zero element in $M_{i+1}$. The **image** of the incoming map, $\text{im}(f_{i-1})$, is the submodule of $M_i$ consisting of all elements that are the image of some element from $M_{i-1}$.

A fundamental property linking these maps is that the composition of any two consecutive homomorphisms in a [chain complex](@entry_id:150246) is the zero map. That is, $f_i \circ f_{i-1} = 0$. This is equivalent to the statement that the image of the incoming map is a submodule of the kernel of the outgoing map: $\text{im}(f_{i-1}) \subseteq \ker(f_i)$. While this condition is important, it is not sufficient for exactness.

The sequence is defined to be **exact at $M_i$** if the image of the incoming homomorphism is precisely equal to the kernel of the outgoing homomorphism:

$$ \text{im}(f_{i-1}) = \ker(f_i) $$

A sequence is called an **exact sequence** if it is exact at every module where the condition can be checked (i.e., at every module that has both an incoming and an outgoing map).

The distinction between $\text{im}(f) \subseteq \ker(g)$ and $\text{im}(f) = \ker(g)$ is crucial. The former simply states that applying two successive maps annihilates every element. The latter, exactness, implies that the only elements annihilated by the second map are precisely those that arrived from the first map. It signifies a perfect "hand-off" of information between the maps.

To illustrate this, consider a sequence $A \xrightarrow{f} B \xrightarrow{g} C$ where $g \circ f = 0$. This condition is met, for instance, in the sequence of $\mathbb{Z}$-modules ([abelian groups](@entry_id:145145)) $\mathbb{Z} \xrightarrow{f} \mathbb{Z} \xrightarrow{g} \mathbb{Z}$, where $f(n) = 2n$ and $g$ is the zero homomorphism, $g(n) = 0$ for all $n$. Here, $\text{im}(f)$ is the set of all even integers, $2\mathbb{Z}$. The kernel of $g$ is the entire domain, $\mathbb{Z}$. Since $2\mathbb{Z}$ is a [proper subset](@entry_id:152276) of $\mathbb{Z}$, we have $\text{im}(f) \subsetneq \ker(g)$, and the sequence is not exact at the middle $\mathbb{Z}$ module [@problem_id:1792265]. Exactness demands a tighter connection.

### Short Exact Sequences: The Atomic Units of Module Theory

Among all possible [exact sequences](@entry_id:151503), one particular form is of paramount importance: the **[short exact sequence](@entry_id:137930)**. This is a sequence of the form:

$$ 0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0 $$

Here, $0$ denotes the zero module, which contains only the identity element. The homomorphisms to and from the zero module are unique. Let us dissect the conditions for exactness at each position.

*   **Exactness at $A$**: The sequence is $0 \to A \xrightarrow{f} B$. The incoming map is the zero map from the zero module, whose image is the zero submodule $\{0_A\} \subseteq A$. Exactness at $A$ requires $\ker(f) = \{0_A\}$. This is precisely the definition of an **injective** homomorphism. Thus, the first non-trivial map in a [short exact sequence](@entry_id:137930) is always an injection. This allows us to view $A$ as being embedded as a submodule within $B$ (or, more precisely, $A$ is isomorphic to $\text{im}(f) \subseteq B$). The simple sequence $0 \to M \xrightarrow{f} N$ is exact if and only if $f$ is injective [@problem_id:1792294].

*   **Exactness at $C$**: The sequence is $B \xrightarrow{g} C \to 0$. The outgoing map is the zero map to the zero module. Its kernel is the entire module $C$. Exactness at $C$ requires $\text{im}(g) = C$. This is the definition of a **surjective** homomorphism. Thus, the last non-trivial map in a [short exact sequence](@entry_id:137930) is always a [surjection](@entry_id:634659).

*   **Exactness at $B$**: This is the central condition: $\text{im}(f) = \ker(g)$.

Taken together, a [short exact sequence](@entry_id:137930) provides a concise and powerful description of a fundamental algebraic structure. The map $f$ embeds $A$ into $B$ as a submodule $\text{im}(f)$. The map $g$ then projects $B$ onto $C$. The condition $\text{im}(f) = \ker(g)$ tells us that the elements of $B$ which are "killed" by $g$ are precisely those which came from $A$ via $f$. This directly relates to the First Isomorphism Theorem for modules, which states that $B/\ker(g) \cong \text{im}(g)$. Substituting the properties of the [short exact sequence](@entry_id:137930), we find $B/\text{im}(f) \cong C$. Since $f$ is injective, $A \cong \text{im}(f)$, so we have the profound relationship:

$$ B/A \cong C $$
(up to isomorphism). A [short exact sequence](@entry_id:137930) expresses the idea that $B$ contains a submodule isomorphic to $A$, and the corresponding [quotient module](@entry_id:155903) is isomorphic to $C$.

The canonical example of a [short exact sequence](@entry_id:137930) is built from [integer division](@entry_id:154296). For any integer $n > 1$, consider the submodule $n\mathbb{Z} \subseteq \mathbb{Z}$ and the [quotient module](@entry_id:155903) $\mathbb{Z}_n = \mathbb{Z}/n\mathbb{Z}$. Let $i: n\mathbb{Z} \to \mathbb{Z}$ be the inclusion map and $\pi: \mathbb{Z} \to \mathbb{Z}_n$ be the canonical projection. This gives the sequence:

$$ 0 \to n\mathbb{Z} \xrightarrow{i} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_n \to 0 $$

This is a [short exact sequence](@entry_id:137930) [@problem_id:1792279]. The inclusion $i$ is clearly injective. The projection $\pi$ is surjective by definition. The image of the inclusion is $\text{im}(i) = n\mathbb{Z}$. The kernel of the projection consists of all integers that are congruent to $0$ modulo $n$, so $\ker(\pi) = n\mathbb{Z}$. Since $\text{im}(i) = \ker(\pi)$, the sequence is exact at $\mathbb{Z}$. This sequence is the algebraic embodiment of the [division algorithm](@entry_id:156013). In contrast, a sequence like $0 \to 2\mathbb{Z} \xrightarrow{i} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_3 \to 0$ is not exact, because $\text{im}(i) = 2\mathbb{Z}$ while $\ker(\pi) = 3\mathbb{Z}$ [@problem_id:1792279]. Similarly, for the sequence $\mathbb{Z} \xrightarrow{f} \mathbb{Z} \xrightarrow{g} \mathbb{Z}_k \to 0$ with $f(x)=13x$ and $g$ being projection modulo $k$, [exactness](@entry_id:268999) at the middle $\mathbb{Z}$ forces $\text{im}(f) = \ker(g)$, which means $13\mathbb{Z} = k\mathbb{Z}$, implying $k=13$ [@problem_id:1792314].

### The Splitting Lemma: When is a Sum Direct?

Given a [short exact sequence](@entry_id:137930) $0 \to A \to B \to C \to 0$, we know that $B$ is an "extension" of $C$ by $A$. A natural question arises: is $B$ simply the [direct sum](@entry_id:156782) of $A$ and $C$? That is, is $B \cong A \oplus C$? The answer is, not always. When this is the case, the sequence is said to **split**. The **Splitting Lemma** provides precise conditions for this to occur.

A [short exact sequence](@entry_id:137930) $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$ of $R$-modules splits if and only if any of the following equivalent conditions hold:

1.  There exists a homomorphism $r: B \to A$, called a **retraction**, such that $r \circ f = \text{id}_A$. This means $f$ has a left inverse.
2.  There exists a homomorphism $s: C \to B$, called a **section**, such that $g \circ s = \text{id}_C$. This means $g$ has a [right inverse](@entry_id:161498).
3.  The module $B$ is isomorphic to the [direct sum](@entry_id:156782) $A \oplus C$.

The existence of such a retraction or section provides a way to "disassemble" $B$ back into its constituent parts, $A$ and $C$. For instance, if a retraction $r$ exists, one can show that any element $b \in B$ can be uniquely written as a sum of an element from the image of $f$ and an element from the kernel of $r$. These two submodules have trivial intersection and span $B$, leading to the [direct sum decomposition](@entry_id:263004) $B \cong \text{im}(f) \oplus \ker(r)$, which in turn implies $B \cong A \oplus C$ [@problem_id:1792313]. As a concrete application, if we have a [short exact sequence](@entry_id:137930) $0 \to \mathbb{Z}_2 \to B \to \mathbb{Z}_2 \to 0$ that is known to split (e.g., by the existence of a retraction), then $B$ must be isomorphic to $\mathbb{Z}_2 \oplus \mathbb{Z}_2$ [@problem_id:1792313].

However, many important sequences do not split. The canonical example $0 \to \mathbb{Z} \xrightarrow{\times n} \mathbb{Z} \to \mathbb{Z}_n \to 0$ for $n>1$ is a prime example of a non-split sequence [@problem_id:1792302]. If this sequence were to split, there would have to exist a section, a homomorphism $s: \mathbb{Z}_n \to \mathbb{Z}$ such that $\pi \circ s = \text{id}_{\mathbb{Z}_n}$. Consider the generator $\overline{1} \in \mathbb{Z}_n$. Since $\mathbb{Z}_n$ is a [torsion group](@entry_id:144787) ($n \cdot \overline{1} = \overline{0}$), its image under any homomorphism must also consist of [torsion elements](@entry_id:148301). Let $s(\overline{1}) = z \in \mathbb{Z}$. Then $s(n \cdot \overline{1}) = n \cdot s(\overline{1}) = nz$. But $s(n \cdot \overline{1}) = s(\overline{0}) = 0$. So we must have $nz = 0$. In the [ring of integers](@entry_id:155711) $\mathbb{Z}$, the only element of finite order is $0$. Thus, $z=0$. This implies $s(\overline{1}) = 0$, and consequently $\pi(s(\overline{1})) = \pi(0) = \overline{0}$. This contradicts the requirement that $\pi \circ s = \text{id}_{\mathbb{Z}_n}$, which demands $\pi(s(\overline{1})) = \overline{1}$. Therefore, no such section $s$ can exist, and the sequence does not split. This corresponds to the structural fact that $\mathbb{Z}$ is not isomorphic to $\mathbb{Z} \oplus \mathbb{Z}_n$, as the latter has non-zero elements of finite order while the former does not.

### Functors and the Failure of Exactness

Functors are maps between categories, such as the category of $R$-modules. Applying a [functor](@entry_id:260898) to all modules and maps in an [exact sequence](@entry_id:149883) produces a new sequence. A crucial question in [homological algebra](@entry_id:155139) is whether this new sequence is also exact.

An **exact functor** is one that preserves all [exact sequences](@entry_id:151503). However, most [functors](@entry_id:150427) are not fully exact. More common are **left-exact** and **right-exact** [functors](@entry_id:150427).

*   The functor $\text{Hom}_R(M, -)$, for a fixed module $M$, is **left-exact**. This means that if $0 \to A \to B \to C$ is exact, then the resulting sequence $0 \to \text{Hom}_R(M, A) \to \text{Hom}_R(M, B) \to \text{Hom}_R(M, C)$ is also exact. However, this [functor](@entry_id:260898) is not necessarily right-exact; it may fail to preserve surjections. To see this, let us apply the [functor](@entry_id:260898) $F(-) = \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, -)$ to our canonical non-split sequence $0 \to \mathbb{Z} \xrightarrow{\mu_n} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_n \to 0$. The resulting sequence is:
    $$ \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}) \xrightarrow{(\mu_n)_*} \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}) \xrightarrow{\pi_*} \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}_n) $$
    Any homomorphism from $\mathbb{Z}_n$ to $\mathbb{Z}$ must be the zero map, since $\mathbb{Z}$ has no non-zero [torsion elements](@entry_id:148301). So, $\text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}) = 0$. In contrast, a homomorphism from $\mathbb{Z}_n$ to itself is determined by where it sends the generator $\overline{1}$, leading to the [isomorphism](@entry_id:137127) $\text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}_n) \cong \mathbb{Z}_n$. The sequence becomes $0 \to 0 \to \mathbb{Z}_n$. This sequence is not exact at the final term, as the map $\pi_*: 0 \to \mathbb{Z}_n$ has image $\{0\}$, which is not all of $\mathbb{Z}_n$. The failure of [exactness](@entry_id:268999) here gives rise to the theory of Ext functors. In this case, the cokernel of $\pi_*$ is $\mathbb{Z}_n / \{0\} \cong \mathbb{Z}_n$ [@problem_id:1792298].

*   The functor $- \otimes_R M$, for a fixed module $M$, is **right-exact**. This means that if $A \to B \to C \to 0$ is exact, then $A \otimes_R M \to B \otimes_R M \to C \otimes_R M \to 0$ is also exact. This [functor](@entry_id:260898) is not necessarily left-exact; it may fail to preserve injections. Consider applying the [functor](@entry_id:260898) $- \otimes_{\mathbb{Z}} \mathbb{Z}_2$ to the exact sequence $0 \to \mathbb{Z} \xrightarrow{f} \mathbb{Z} \to \mathbb{Z}_2 \to 0$, where $f$ is multiplication by 2. The new sequence begins with:
    $$ \mathbb{Z} \otimes_{\mathbb{Z}} \mathbb{Z}_2 \xrightarrow{\bar{f}} \mathbb{Z} \otimes_{\mathbb{Z}} \mathbb{Z}_2 \to \dots $$
    Using the general [isomorphism](@entry_id:137127) $R \otimes_R M \cong M$, we have $\mathbb{Z} \otimes_{\mathbb{Z}} \mathbb{Z}_2 \cong \mathbb{Z}_2$. The map $\bar{f} = f \otimes \text{id}$ acts on a [simple tensor](@entry_id:201624) $z \otimes \overline{a}$ as $f(z) \otimes \overline{a} = 2z \otimes \overline{a}$. By the properties of the [tensor product](@entry_id:140694), this is equal to $z \otimes 2\overline{a}$. Since $2\overline{a} = \overline{0}$ in $\mathbb{Z}_2$, the map $\bar{f}$ sends every element to $0$. It is the zero map. The original map $f$ was injective, but $\bar{f}$ is not. Its kernel is the entire domain, $\mathbb{Z}_2$. The failure of left-[exactness](@entry_id:268999) here gives rise to the theory of Tor functors [@problem_id:1792310].

### The Snake Lemma and Long Exact Sequences

The true power of [exact sequences](@entry_id:151503) becomes apparent when we consider maps between them. A commutative diagram with two exact rows can reveal a hidden, deeper exact sequence. The most fundamental result of this type is the **Snake Lemma**. It states that given a commutative diagram of modules with exact rows:
$$
\begin{array}{ccccccccc}
0  \longrightarrow  A  \xrightarrow{f}  B  \xrightarrow{g}  C  \longrightarrow  0 \\
  \downarrow \alpha   \downarrow \beta   \downarrow \gamma   \\
0  \longrightarrow  A'  \xrightarrow{f'}  B'  \xrightarrow{g'}  C'  \longrightarrow  0
\end{array}
$$
there exists a canonical **[long exact sequence](@entry_id:153438)** that connects the kernels and cokernels of the vertical maps:
$$ 0 \to \ker(\alpha) \to \ker(\beta) \to \ker(\gamma) \xrightarrow{\delta} \text{coker}(\alpha) \to \text{coker}(\beta) \to \text{coker}(\gamma) \to 0 $$
The most remarkable part of this is the **[connecting homomorphism](@entry_id:160713)** $\delta$, which "jumps" from the top row to the bottom row. Its construction is a classic example of a technique called **[diagram chasing](@entry_id:263851)**. To find $\delta(z)$ for an element $z \in \ker(\gamma)$:
1.  Since $g$ is surjective, pull $z$ back to an element $b \in B$ such that $g(b) = z$.
2.  Push $b$ down to $\beta(b) \in B'$.
3.  By commutativity, $g'(\beta(b)) = \gamma(g(b)) = \gamma(z) = 0$. So $\beta(b)$ is in the kernel of $g'$.
4.  By [exactness](@entry_id:268999) of the bottom row, $\ker(g') = \text{im}(f')$. So, there is a unique $a' \in A'$ such that $f'(a') = \beta(b)$.
5.  The image of $z$ under the [connecting homomorphism](@entry_id:160713) is the [coset](@entry_id:149651) of this $a'$ in the cokernel of $\alpha$: $\delta(z) = a' + \text{im}(\alpha)$.

This abstract procedure can be made concrete. Consider the diagram where $A=A'=B=B'=\mathbb{Z}$, $C=C'=\mathbb{Z}_2$, the horizontal maps are multiplication by 2 and projection, and the vertical maps are $\alpha(x)=2x$, $\beta(y)=2y$, and $\gamma=0$ [@problem_id:1792316]. Let's trace the element $z = 1+2\mathbb{Z} \in \ker(\gamma) = C$. We pull it back to $b=1 \in B$. We push this down to $\beta(1)=2 \in B'$. This element is in $\ker(g')$. We find the element $a' \in A'$ such that $f'(a') = 2a' = 2$, which is $a'=1$. Thus, $\delta(1+2\mathbb{Z}) = 1 + \text{im}(\alpha) = 1+2\mathbb{Z} \in \text{coker}(\alpha) = \mathbb{Z}/2\mathbb{Z}$. The snake lemma reveals a non-trivial connection between the two rows.

This principle extends to a more general and powerful tool: the **long exact sequence in homology**. A [short exact sequence](@entry_id:137930) of chain complexes, $0 \to \mathcal{A} \to \mathcal{B} \to \mathcal{C} \to 0$, gives rise to a long exact sequence of their homology groups:
$$ \dots \to H_n(\mathcal{A}) \to H_n(\mathcal{B}) \to H_n(\mathcal{C}) \xrightarrow{\delta_n} H_{n-1}(\mathcal{A}) \to H_{n-1}(\mathcal{B}) \to \dots $$
The [connecting homomorphism](@entry_id:160713) $\delta_n$ again arises from a diagram chase, linking the homology of the complexes in a profound way. These sequences are a cornerstone of algebraic topology and [homological algebra](@entry_id:155139), allowing for the computation of complex invariants by breaking them down into simpler, related pieces [@problem_id:1792315].

In summary, [exact sequences](@entry_id:151503) provide a unifying language to describe module structures, their relationships, and the behavior of functors between them. From the simple definition of exactness at a point, we build up to the versatile [short exact sequence](@entry_id:137930), the structural insights of the Splitting Lemma, and finally to the powerful machinery of long [exact sequences](@entry_id:151503), which form the bedrock of modern homological methods.