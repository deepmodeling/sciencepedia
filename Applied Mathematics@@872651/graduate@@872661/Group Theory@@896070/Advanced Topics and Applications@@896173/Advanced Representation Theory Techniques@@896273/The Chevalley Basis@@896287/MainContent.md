## Introduction
The Chevalley basis stands as a cornerstone in the theory of Lie algebras, providing a powerful and elegant framework for understanding their structure. Conceived by Claude Chevalley, this special basis offers a [canonical representation](@entry_id:146693) for any complex semisimple Lie algebra, distinguished by the remarkable property that its [structure constants](@entry_id:157960) are integers. This "integrality" is not a mere technicality; it forms the crucial bridge between the continuous symmetries described by Lie groups over the complex numbers and the discrete [algebraic structures](@entry_id:139459) of groups over other fields, especially finite fields. This article provides a comprehensive exploration of this foundational concept, from its theoretical underpinnings to its far-reaching applications.

The first chapter, "Principles and Mechanisms," will delve into the construction of the Chevalley basis, explaining the roles of the Cartan subalgebra, roots, and [coroots](@entry_id:193338), and detailing how the defining commutation relations, including the Chevalley-Serre relations, result in integer structure constants. Following this, "Applications and Interdisciplinary Connections" will showcase the utility of the basis in [representation theory](@entry_id:137998), the construction of Chevalley groups over [finite fields](@entry_id:142106), and its influence on modern topics like [quantum groups](@entry_id:146711) and theoretical physics. Finally, "Hands-On Practices" will offer practical exercises to solidify the reader's understanding by applying these principles to concrete computational problems.

## Principles and Mechanisms

Following the introduction to the study of Lie algebras, we now delve into the foundational principles and structural mechanisms of the **Chevalley basis**. This special basis, conceived by Claude Chevalley, provides a [canonical representation](@entry_id:146693) for any complex semisimple Lie algebra. Its most remarkable feature is that its [structure constants](@entry_id:157960) are not merely complex numbers but integers. This "integrality" is not a mere technical convenience; it is the cornerstone for constructing analogues of Lie groups over arbitrary fields, most notably [finite fields](@entry_id:142106), thereby connecting continuous symmetry with discrete algebraic structures.

### The Building Blocks of the Chevalley Basis

A complex semisimple Lie algebra $\mathfrak{g}$ admits a Cartan decomposition, $\mathfrak{g} = \mathfrak{h} \oplus \bigoplus_{\alpha \in \Phi} \mathfrak{g}_\alpha$, where $\mathfrak{h}$ is a maximal abelian subalgebra (the **Cartan subalgebra**), and $\Phi \subset \mathfrak{h}^*$ is the [root system](@entry_id:202162). Each **root space** $\mathfrak{g}_\alpha$ is a one-dimensional eigenspace for the [adjoint action](@entry_id:141823) of $\mathfrak{h}$. The Chevalley basis provides a canonical set of generators for $\mathfrak{h}$ and each $\mathfrak{g}_\alpha$.

#### Coroots and the Cartan Subalgebra

For each root $\alpha \in \Phi$, its corresponding negative root $-\alpha$ is also in $\Phi$. The root spaces $\mathfrak{g}_\alpha$ and $\mathfrak{g}_{-\alpha}$, together with their [commutators](@entry_id:158878), form a subalgebra isomorphic to $\mathfrak{sl}_2(\mathbb{C})$. Within this subalgebra, we can select generators $e_\alpha \in \mathfrak{g}_\alpha$ and $e_{-\alpha} \in \mathfrak{g}_{-\alpha}$. The Chevalley basis normalizes these generators such that their commutator defines an element of the Cartan subalgebra called the **coroot**:
$$
[e_\alpha, e_{-\alpha}] = h_\alpha \in \mathfrak{h}
$$
The set of all [coroots](@entry_id:193338) spans $\mathfrak{h}$. More specifically, a basis for $\mathfrak{h}$ can be constructed from the **simple [coroots](@entry_id:193338)** $\{h_i \equiv h_{\alpha_i}\}$, corresponding to a chosen set of [simple roots](@entry_id:197415) $\{\alpha_1, \dots, \alpha_l\}$. These simple [coroots](@entry_id:193338) are uniquely defined by their interaction with the [simple roots](@entry_id:197415), governed by the Cartan matrix $A = (A_{ij})$ of the Lie algebra:
$$
\alpha_j(h_i) = A_{ij}
$$
Here, $\alpha_j(h_i)$ denotes the action of the [linear functional](@entry_id:144884) $\alpha_j \in \mathfrak{h}^*$ on the vector $h_i \in \mathfrak{h}$. This relationship provides a powerful abstract definition that can be translated into concrete [matrix representations](@entry_id:146025).

To illustrate, let us determine the explicit matrix form for the simple coroot $H_{\alpha_1}$ in the defining representation of $\mathfrak{g} = \mathfrak{sl}_3(\mathbb{C})$. The Cartan subalgebra $\mathfrak{h}$ consists of traceless diagonal $3 \times 3$ matrices. An element is $H = \text{diag}(d_1, d_2, d_3)$ with $d_1+d_2+d_3=0$. The [simple roots](@entry_id:197415) can be defined as functionals on $\mathfrak{h}$: $\alpha_1(H) = d_1 - d_2$ and $\alpha_2(H) = d_2 - d_3$. The Cartan matrix for $\mathfrak{sl}_3(\mathbb{C})$ (type $A_2$) is $A = \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}$. We seek the matrix $H_{\alpha_1} = \text{diag}(a, b, c)$ that satisfies the defining relations:
$$
\alpha_1(H_{\alpha_1}) = A_{11} = 2 \implies a - b = 2
$$
$$
\alpha_2(H_{\alpha_1}) = A_{12} = -1 \implies b - c = -1
$$
Along with the traceless condition $a+b+c=0$, we have a system of linear equations. Substituting $c = -a-b$ into the second equation gives $b - (-a-b) = a+2b = -1$. From the first equation, $a = 2+b$, which we substitute into the modified second equation: $(2+b) + 2b = -1$, yielding $3b = -3$, or $b = -1$. Consequently, $a = 2+(-1) = 1$, and $c = -1- (-1) = 0$. Thus, the coroot is represented by the matrix:
$$
H_{\alpha_1} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & -1 & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$
This demonstrates how the abstract algebraic structure of roots and [coroots](@entry_id:193338) manifests in a tangible matrix form [@problem_id:800051].

#### Root Vectors and the Serre Construction

The elements $e_\alpha$ are the **root vectors** or **Chevalley generators** for the root spaces $\mathfrak{g}_\alpha$. For [simple roots](@entry_id:197415) $\alpha_i$, the choice of $e_{\alpha_i}$ and $e_{-\alpha_i}$ sets the foundation for the entire basis. The root vectors for non-[simple roots](@entry_id:197415) are then constructed systematically through commutation. If $\alpha$ and $\beta$ are [positive roots](@entry_id:199264) such that $\alpha+\beta$ is also a root, a standard convention (part of the Serre construction) defines the corresponding root vector via the Lie bracket:
$$
e_{\alpha+\beta} = \pm [e_\alpha, e_\beta]
$$
The sign is a matter of convention, but often fixed to be positive. Let us examine this construction for $\mathfrak{g} = \mathfrak{sl}_4(\mathbb{C})$ in its defining $4 \times 4$ [matrix representation](@entry_id:143451). The [simple roots](@entry_id:197415) can be taken as $\alpha_1 = \epsilon_1 - \epsilon_2$, $\alpha_2 = \epsilon_2 - \epsilon_3$, and $\alpha_3 = \epsilon_3 - \epsilon_4$, where $\epsilon_i$ extracts the $i$-th diagonal entry. A standard choice for the [simple root](@entry_id:635422) vectors is $e_{\alpha_1} = E_{12}$, $e_{\alpha_2} = E_{23}$, and $e_{\alpha_3} = E_{34}$, where $E_{ij}$ is the [elementary matrix](@entry_id:635817) with a 1 in the $(i,j)$ position and zeros elsewhere.

To find the root vector for the non-[simple root](@entry_id:635422) $\phi = \alpha_1+\alpha_2$, we compute the commutator of the corresponding [simple root](@entry_id:635422) vectors:
$$
e_{\alpha_1+\alpha_2} = [e_{\alpha_1}, e_{\alpha_2}] = [E_{12}, E_{23}] = E_{12}E_{23} - E_{23}E_{12}
$$
The [product of elementary matrices](@entry_id:155132) $E_{ij}E_{kl}$ is $\delta_{jk}E_{il}$. Therefore, $E_{12}E_{23} = E_{13}$, and $E_{23}E_{12} = 0$ since the inner indices do not match. The result is:
$$
e_{\alpha_1+\alpha_2} = E_{13} = \begin{pmatrix} 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}
$$
This calculation [@problem_id:799978] exemplifies the constructive nature of the Chevalley basis, where the entire structure is built from the generators associated with [simple roots](@entry_id:197415).

### The Integral Structure Constants

The defining feature of the Chevalley basis is its set of [commutation relations](@entry_id:136780), which are governed by integer coefficients. These **Chevalley-Serre relations** constitute a presentation of the Lie algebra:
1.  $[h_i, h_j] = 0$
2.  $[h_i, e_j] = A_{ij} e_j$
3.  $[e_i, f_j] = \delta_{ij} h_i$, where $e_i \equiv e_{\alpha_i}$ and $f_i \equiv e_{-\alpha_i}$.
4.  $(\text{ad } e_i)^{1-A_{ij}}(e_j) = 0$ for $i \neq j$ (Serre relations).
5.  $(\text{ad } f_i)^{1-A_{ij}}(f_j) = 0$ for $i \neq j$ (Serre relations).

From these, one can derive the general commutation relation for any two root vectors:
$$
[e_\alpha, e_\beta] = N_{\alpha, \beta} e_{\alpha+\beta} \quad (\text{if } \alpha+\beta \in \Phi)
$$
where $N_{\alpha, \beta}$ are the integer **[structure constants](@entry_id:157960)**. If $\alpha+\beta$ is not a non-zero root, the commutator is zero. The fact that these constants are integers is a deep result. Their magnitudes are fixed by the geometry of the [root system](@entry_id:202162), while their signs depend on a consistent set of choices.

A fundamental formula for the magnitude of these constants is derived from the [representation theory](@entry_id:137998) of $\mathfrak{sl}_2(\mathbb{C})$. For any two roots $\alpha, \beta \in \Phi$, the set of roots of the form $\beta + k\alpha$ (where $k \in \mathbb{Z}$) is an unbroken sequence called the **$\alpha$-string through $\beta$**. Let this string be $\{\beta - r\alpha, \dots, \beta, \dots, \beta + q\alpha\}$. Then the magnitude of the structure constant is given by:
$$
|N_{\alpha, \beta}| = r+1
$$
Let's apply this to find a structure constant in the exceptional Lie algebra $\mathfrak{g}_2$. The [positive roots](@entry_id:199264) are $\Phi^+ = \{ \alpha_1, \alpha_2, \alpha_1+\alpha_2, 2\alpha_1+\alpha_2, 3\alpha_1+\alpha_2, 3\alpha_1+2\alpha_2 \}$, where $\alpha_1$ is short and $\alpha_2$ is long. We want to compute $N_{\alpha, \beta}$ for $\alpha = \alpha_1$ and $\beta = \alpha_1+\alpha_2$. We must find the $\alpha_1$-string through $\beta$.
- For $k=1$, $\beta - \alpha_1 = \alpha_2$, which is a root.
- For $k=2$, $\beta - 2\alpha_1 = \alpha_2 - \alpha_1$, which is not a root (its coefficients, relative to the [simple root](@entry_id:635422) basis, are not all of the same sign).
Thus, the string only extends one step back, meaning $r=1$. The magnitude is $|N_{\alpha_1, \alpha_1+\alpha_2}| = r+1 = 2$. With a standard sign convention (e.g., $N_{\alpha, \beta} > 0$ if $\alpha$ has smaller height than $\beta$), we find $N_{\alpha_1, \alpha_1+\alpha_2} = 2$ [@problem_id:799938].

The structure constants obey certain symmetries. One is antisymmetry, $[e_\alpha, e_\beta] = -[e_\beta, e_\alpha]$, which implies $N_{\alpha, \beta} = -N_{\beta, \alpha}$. Another important relation, $N_{-\alpha, -\beta} = -N_{\alpha, \beta}$, can be elegantly demonstrated using the **Chevalley antiautomorphism** $\sigma$, a linear map on $\mathfrak{g}$ defined by $\sigma(e_\alpha) = -e_{-\alpha}$ and $\sigma(h_i)=-h_i$. It is an *anti*-automorphism because it reverses the order of products: $\sigma([X,Y]) = [\sigma(Y), \sigma(X)]$. Applying this to a commutator:
$$
\sigma([e_\alpha, e_\beta]) = \sigma(N_{\alpha,\beta} e_{\alpha+\beta}) = N_{\alpha,\beta} \sigma(e_{\alpha+\beta}) = -N_{\alpha,\beta} e_{-(\alpha+\beta)}
$$
On the other hand, using the antiautomorphism property:
$$
\sigma([e_\alpha, e_\beta]) = [\sigma(e_\beta), \sigma(e_\alpha)] = [-e_{-\beta}, -e_{-\alpha}] = [e_{-\beta}, e_{-\alpha}] = N_{-\beta, -\alpha} e_{-(\alpha+\beta)}
$$
Comparing the two expressions, we find $N_{-\beta, -\alpha} = -N_{\alpha,\beta}$. As an example, given the relation $[e_{\alpha_1}, e_{\alpha_1+\alpha_2}] = 2e_{2\alpha_1+\alpha_2}$ in the Lie algebra of type $C_2$, we find that $\sigma([e_{\alpha_1}, e_{\alpha_1+\alpha_2}]) = -2 e_{-(2\alpha_1+\alpha_2)}$ [@problem_id:799896]. This showcases the internal consistency and rich symmetry of the algebraic structure.

### Advanced Mechanisms and Symmetries

The relations defining the Chevalley basis are not arbitrary; they are deeply constrained by the fundamental axioms of Lie algebras, primarily the **Jacobi identity**: $[X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0$.

#### The Jacobi Identity as a Computational Tool

The Jacobi identity is the engine that drives the algebra's structure. It can be used to derive non-trivial relations between basis elements. A classic result is the expression for the coroot of a sum of roots. For $\mathfrak{g} = A_2 = \mathfrak{sl}_3(\mathbb{C})$, let's find $h_{\alpha_1+\alpha_2}$. Let $e_3 = [e_1, e_2]$ and $f_3 = -[f_1, f_2]$ be the root vectors for $\alpha_3 = \alpha_1+\alpha_2$ and $-\alpha_3$. The corresponding coroot is $h_3 = [e_3, f_3] = -[[e_1,e_2], [f_1, f_2]]$. Applying the Jacobi identity to the nested [commutators](@entry_id:158878):
$$
[[e_1,e_2], [f_1, f_2]] = [e_1, [e_2, [f_1, f_2]]] - [e_2, [e_1, [f_1, f_2]]]
$$
We evaluate the inner terms, again using the Jacobi identity and Serre relations:
$$
[e_2, [f_1, f_2]] = [[e_2, f_1], f_2] + [f_1, [e_2, f_2]] = [0, f_2] + [f_1, h_2] = -[h_2, f_1] = -(-A_{21}f_1) = -f_1
$$
$$
[e_1, [f_1, f_2]] = [[e_1, f_1], f_2] + [f_1, [e_1, f_2]] = [h_1, f_2] + [f_1, 0] = -A_{21}f_2 = f_2
$$
Substituting these back, we get:
$$
[[e_1,e_2], [f_1, f_2]] = [e_1, -f_1] - [e_2, f_2] = -[e_1,f_1] - [e_2,f_2] = -h_1 - h_2
$$
Therefore, $h_3 = -(-h_1-h_2) = h_1+h_2$. This fundamental result, that the coroot of a sum of two [simple roots](@entry_id:197415) is the sum of the simple [coroots](@entry_id:193338), is a direct consequence of the Jacobi identity [@problem_id:800089].

More complex calculations follow the same principle. In the non-simply laced algebra $\mathfrak{sp}_4(\mathbb{C})$ (type $C_2$), where $A_{12}=-1$ and $A_{21}=-2$, the Jacobi identity allows us to navigate a chain of commutators to find that $[e_{2\alpha_1+\alpha_2}, f_1] = -1 \cdot e_{\alpha_1+\alpha_2}$, revealing a structure constant through systematic application of the defining relations [@problem_id:800013]. These examples underscore that the entire structure is tightly interwoven and determined by the Cartan matrix and the Jacobi identity.

#### The Killing Form and Basis Normalization

The **Killing form**, $K(X,Y) = \text{tr}(\text{ad}(X)\text{ad}(Y))$, is a symmetric, non-degenerate, and associative (or invariant) [bilinear form](@entry_id:140194) on $\mathfrak{g}$. Its invariance property, $K([X,Y], Z) = K(X, [Y,Z])$, provides a powerful constraint on the [structure constants](@entry_id:157960).

Consider the triple of roots $(-\alpha_1, \alpha_1+\alpha_2, -\alpha_2)$ in $A_2$. Their sum is zero. Using the invariance of the Killing form:
$$
K([e_{-\alpha_1}, e_{\alpha_1+\alpha_2}], e_{-\alpha_2}) = K(e_{-\alpha_1}, [e_{\alpha_1+\alpha_2}, e_{-\alpha_2}])
$$
The left side becomes $K(N_{-\alpha_1, \alpha_1+\alpha_2}e_{\alpha_2}, e_{-\alpha_2}) = N_{-\alpha_1, \alpha_1+\alpha_2} K(e_{\alpha_2}, e_{-\alpha_2})$. The right side becomes $K(e_{-\alpha_1}, N_{\alpha_1+\alpha_2, -\alpha_2}e_{\alpha_1}) = N_{\alpha_1+\alpha_2, -\alpha_2} K(e_{-\alpha_1}, e_{\alpha_1})$. Assuming a standard normalization $K(e_\alpha, e_{-\alpha})=1$ (valid for simply-laced algebras like $A_2$), this simplifies to an equality of structure constants: $N_{-\alpha_1, \alpha_1+\alpha_2} = N_{\alpha_1+\alpha_2, -\alpha_2}$. By applying this logic cyclically, one can relate many [structure constants](@entry_id:157960) and determine their values from a few initial choices [@problem_id:799963].

The value $K(e_\alpha, e_{-\alpha})$ itself holds important information, especially in non-simply-laced algebras where roots have different lengths. A careful analysis shows that under the standard Chevalley basis conventions, this value is not uniform, but depends on the root length:
$$
K(e_\alpha, e_{-\alpha}) = \frac{2}{(\alpha, \alpha)}
$$
Here, $(\cdot, \cdot)$ is the inner product on the root space $\mathfrak{h}^*$, induced by the Killing form. By convention, for any [root system](@entry_id:202162), the inner product is normalized such that **long roots** $\alpha$ satisfy $(\alpha, \alpha) = 2$. For a simply-laced algebra, all roots are long, so $(\alpha, \alpha) = 2$ for all $\alpha$, and $K(e_\alpha, e_{-\alpha}) = 1$.

However, in a non-simply-laced algebra like $\mathfrak{f}_4$, there are both long and short roots. The ratio of squared lengths is 2. So, for a long root $\alpha$, we have $(\alpha,\alpha)=2$, which gives $K(e_\alpha, e_{-\alpha}) = 1$. For a short root $\beta$, we have $(\beta, \beta) = 1$, which gives $K(e_\beta, e_{-\beta}) = 2$. Therefore, the ratio is:
$$
\frac{K(e_\alpha, e_{-\alpha})}{K(e_\beta, e_{-\beta})} = \frac{1}{2}
$$
This demonstrates that the normalization of the Chevalley basis is intrinsically tied to the geometry of the root system [@problem_id:800072]. While the [structure constants](@entry_id:157960) $N_{\alpha,\beta}$ are integers, the normalization constants with respect to the Killing form may be rational.

It is also important to recognize that the choice of root vectors is unique only up to scaling. One could choose $e'_\alpha = c e_\alpha$ and $e'_{-\alpha} = c^{-1} e_{-\alpha}$, and the relation $[e'_\alpha, e'_{-\alpha}] = h_\alpha$ would still hold. This affects the [structure constants](@entry_id:157960): $[e'_\alpha, e'_\beta] = c_\alpha c_\beta c_{\alpha+\beta}^{-1} N_{\alpha,\beta} e'_{\alpha+\beta}$. While specific choices, like using complex numbers of unit modulus, can simplify some relations, the fundamental integrality of the $N_{\alpha,\beta}$ is a property of the algebra that can be achieved by *some* choice of basis [@problem_id:800018].

### The Chevalley Basis over Other Fields

The true power of the Chevalley basis lies in its integrality. Since the basis elements $\{h_i, e_\alpha\}$ have integer [structure constants](@entry_id:157960), their integer linear span forms a Lie algebra over the ring of integers $\mathbb{Z}$, denoted $\mathfrak{g}_{\mathbb{Z}}$.
$$
\mathfrak{g}_{\mathbb{Z}} = \bigoplus_{i=1}^l \mathbb{Z}h_i \oplus \bigoplus_{\alpha \in \Phi} \mathbb{Z}e_\alpha
$$
This integral form is a lattice inside the complex Lie algebra $\mathfrak{g}$. It acts as a universal template. By taking the tensor product of $\mathfrak{g}_{\mathbb{Z}}$ with any field $k$, we obtain a Lie algebra over that field:
$$
\mathfrak{g}_k = \mathfrak{g}_{\mathbb{Z}} \otimes_{\mathbb{Z}} k
$$
This process allows the construction of **Chevalley groups**, which are analogues of Lie groups defined over any field $k$, including finite fields $\mathbb{F}_p$. The structure of the resulting Lie algebra $\mathfrak{g}_k$ is determined by the integer structure constants $N_{\alpha,\beta}$ reduced modulo the characteristic of the field.

This reduction can have profound consequences. A non-zero integer structure constant may become zero in a field of finite characteristic. For instance, we found that for $\mathfrak{g}_2$, the constant $N_{\alpha_1, \alpha_1+\alpha_2}$ has magnitude 2. If we construct the corresponding Lie algebra over the [finite field](@entry_id:150913) $\mathbb{F}_2$, this structure constant vanishes. Similarly, in the exceptional algebra $\mathfrak{f}_4$, let's consider the structure constant $N_{\alpha, \beta}$ for $\alpha = \alpha_3$ and $\beta = \alpha_2+\alpha_3$. The $\alpha_3$-string through $\alpha_2+\alpha_3$ is $\{\alpha_2, \alpha_2+\alpha_3\}$, meaning $\beta-\alpha_3$ is a root but $\beta-2\alpha_3$ is not. So, the integer $r$ is 1. This gives $|N_{\alpha_3, \alpha_2+\alpha_3}| = r+1=2$. When we reduce this integer modulo a prime $p$, it becomes zero if and only if $p$ divides 2. The smallest such prime is $p=2$. Therefore, over a field of characteristic 2, the commutator $[e_{\alpha_3}, e_{\alpha_2+\alpha_3}]$ vanishes, a structural change from the original complex algebra [@problem_id:799995]. Primes for which such structural changes occur are known as **bad primes** for the corresponding group type.

In summary, the Chevalley basis provides a rigid, integral backbone for semisimple Lie algebras. Its principles and mechanisms, governed by the Jacobi identity and the geometry of the [root system](@entry_id:202162), not only furnish a canonical description over the complex numbers but also pave the way for exporting the rich theory of Lie groups and their representations to the vast and varied landscapes of number theory and finite geometry.