## Introduction
The search for general formulas to solve polynomial equations is a central theme in the history of algebra. While the quadratic formula is a staple of secondary school mathematics, and more complex formulas exist for cubic and quartic equations, the pursuit of a similar formula for polynomials of degree five and higher led mathematicians down a path of discovery that reshaped the entire field. This quest culminated in the realization that no such general formula exists. The key to understanding this profound limitation lies in the formal study of what it means for a solution to be expressed "by radicals."

This article provides a rigorous introduction to **radical extensions**, the algebraic structures that formalize the process of solving equations using only basic arithmetic and root extractions. We will bridge the gap between the intuitive idea of a radical formula and its precise definition in field theory. By exploring these structures, you will understand the deep connection between the structure of a [field extension](@entry_id:150367) and the properties of a related algebraic object—the Galois group. This connection ultimately explains why some polynomials are [solvable by radicals](@entry_id:154609) while others are not.

Over the next three chapters, we will embark on a comprehensive exploration of this topic. In **Principles and Mechanisms**, we will define radical extensions, analyze their structure using the Tower Law, and clarify crucial properties like normality. Next, in **Applications and Interdisciplinary Connections**, we will apply these concepts to determine the solvability of specific polynomials, investigate the role of roots of unity, and connect the theory to classical problems in Euclidean geometry. Finally, **Hands-On Practices** will offer you the opportunity to solidify your understanding through concrete computational problems. We begin by laying the formal groundwork and defining the anatomy of a [radical extension](@entry_id:148058).

## Principles and Mechanisms

Having introduced the historical context and foundational questions surrounding the solvability of polynomial equations, we now turn to a rigorous, field-theoretic examination of the concepts involved. The intuitive notion of solving an equation "by radicals" must be translated into a precise mathematical framework. This framework is built upon the concept of a **[radical extension](@entry_id:148058)**, a special type of field extension that formally captures the process of adjoining roots.

### The Anatomy of a Radical Extension

At its core, expressing a number by radicals means constructing it from the elements of a base field (such as the rational numbers, $\mathbb{Q}$) using a finite sequence of field operations (addition, subtraction, multiplication, division) and the extraction of $n$-th roots. The algebraic structure that formalizes this constructive process is a [tower of fields](@entry_id:153606).

A [field extension](@entry_id:150367) $K/F$ is defined as a **[radical extension](@entry_id:148058)** if there exists a finite [tower of fields](@entry_id:153606)
$$
F = F_0 \subseteq F_1 \subseteq \dots \subseteq F_m = K
$$
such that for each step in the tower, from $i = 0$ to $m-1$, the field $F_{i+1}$ is obtained by adjoining a single radical to the preceding field $F_i$. More formally, for each $i$, there exists an element $\alpha_i \in F_{i+1}$ and an integer $n_i \ge 1$ such that $F_{i+1} = F_i(\alpha_i)$ and $\alpha_i^{n_i} = a_i$ for some element $a_i \in F_i$. Each step $F_{i+1}/F_i$ is called a **simple [radical extension](@entry_id:148058)**.

A crucial detail in this definition is that the element $a_i$, of which we are taking the $n_i$-th root, must belong to the field $F_i$ at that stage of the tower, not necessarily the original base field $F$. This provision is what allows for the construction of **nested radicals**. For instance, consider the number $\sqrt{1+\sqrt{2}}$. This number is expressed using radicals. The field $\mathbb{Q}(\sqrt{1+\sqrt{2}})$ is a [radical extension](@entry_id:148058) of $\mathbb{Q}$, demonstrated by the tower:
$$
\mathbb{Q} = F_0 \subseteq \mathbb{Q}(\sqrt{2}) = F_1 \subseteq \mathbb{Q}(\sqrt{1+\sqrt{2}}) = K
$$
Here, the first step is the simple [radical extension](@entry_id:148058) $F_1 = F_0(\alpha_0)$ with $\alpha_0 = \sqrt{2}$, where $\alpha_0^2 = 2 \in F_0 = \mathbb{Q}$. The second step is $K = F_1(\alpha_1)$ with $\alpha_1 = \sqrt{1+\sqrt{2}}$, where $\alpha_1^2 = 1+\sqrt{2} \in F_1$. Since $1+\sqrt{2}$ is in $F_1$ but not in $F_0$, this construction would be invalid under a more restrictive definition.

Constructing such towers is a straightforward exercise. For a field like $K = \mathbb{Q}(\sqrt{3}, \sqrt[5]{2})$, we can form a radical tower in multiple ways. For instance, we can first adjoin $\sqrt{3}$ and then $\sqrt[5]{2}$:
$$
\mathbb{Q} \subsetneq \mathbb{Q}(\sqrt{3}) \subsetneq \mathbb{Q}(\sqrt{3}, \sqrt[5]{2})
$$
This is a valid radical tower of length 2 because $\mathbb{Q}(\sqrt{3}) = \mathbb{Q}(\alpha_1)$ with $\alpha_1^2 = 3 \in \mathbb{Q}$, and $\mathbb{Q}(\sqrt{3}, \sqrt[5]{2}) = \mathbb{Q}(\sqrt{3})(\alpha_2)$ with $\alpha_2^5 = 2 \in \mathbb{Q} \subset \mathbb{Q}(\sqrt{3})$. Alternatively, we could adjoin the radicals in the reverse order. Both paths correctly demonstrate that $\mathbb{Q}(\sqrt{3}, \sqrt[5]{2})$ is a [radical extension](@entry_id:148058) of $\mathbb{Q}$.

### The Algebraic Structure of Radical Extensions

To understand radical extensions more deeply, we must analyze their structure, particularly their size or **degree**. A finite [field extension](@entry_id:150367) $K/F$ can be viewed as a vector space over the field $F$. The degree of the extension, denoted $[K:F]$, is the dimension of this vector space. This perspective provides powerful tools for computation.

The most fundamental tool is the **Tower Law**, which states that for a [tower of fields](@entry_id:153606) $F \subseteq L \subseteq K$, the degrees are multiplicative:
$$
[K:F] = [K:L] \cdot [L:F]
$$

Let's apply this to determine the degree and find a basis for a typical [radical extension](@entry_id:148058), $K = \mathbb{Q}(\sqrt[3]{7}, i)$, over $\mathbb{Q}$. We build the extension using the tower $\mathbb{Q} \subset \mathbb{Q}(\sqrt[3]{7}) \subset K$.
1.  **First step: $\mathbb{Q}(\sqrt[3]{7})/\mathbb{Q}$.** The minimal polynomial of $\sqrt[3]{7}$ over $\mathbb{Q}$ is $x^3-7$, which is irreducible by Eisenstein's criterion for the prime $p=7$. Therefore, $[\mathbb{Q}(\sqrt[3]{7}):\mathbb{Q}] = 3$. A basis for this extension as a $\mathbb{Q}$-vector space is $\{1, \sqrt[3]{7}, \sqrt[3]{49}\}$.
2.  **Second step: $K/\mathbb{Q}(\sqrt[3]{7})$.** The field $K$ is obtained by adjoining $i$ to $\mathbb{Q}(\sqrt[3]{7})$. The minimal polynomial of $i$ over $\mathbb{Q}(\sqrt[3]{7})$ is $x^2+1$. This polynomial is irreducible because its roots, $\pm i$, are not real, whereas $\mathbb{Q}(\sqrt[3]{7})$ is a subfield of the real numbers $\mathbb{R}$. Thus, $[K:\mathbb{Q}(\sqrt[3]{7})] = 2$. A basis for this extension is $\{1, i\}$.

By the Tower Law, the total degree is $[K:\mathbb{Q}] = 3 \cdot 2 = 6$. A basis for the entire extension $K/\mathbb{Q}$ can be constructed by taking all products of basis elements from each step. This yields the 6-element basis:
$$
\{1 \cdot 1, \sqrt[3]{7} \cdot 1, \sqrt[3]{49} \cdot 1, 1 \cdot i, \sqrt[3]{7} \cdot i, \sqrt[3]{49} \cdot i \} = \{1, \sqrt[3]{7}, \sqrt[3]{49}, i, i\sqrt[3]{7}, i\sqrt[3]{49}\}
$$
Any element in $\mathbb{Q}(\sqrt[3]{7}, i)$ can be uniquely written as a [linear combination](@entry_id:155091) of these basis elements with coefficients in $\mathbb{Q}$.

When a [radical extension](@entry_id:148058) is formed by adjoining multiple radicals to a base field, such as $K = F(\alpha, \beta)$, its degree is given by the formula for a **compositum** of fields:
$$
[F(\alpha, \beta):F] = \frac{[F(\alpha):F] \cdot [F(\beta):F]}{[F(\alpha) \cap F(\beta):F]}
$$
The most challenging part of this calculation is often determining the intersection of the two [intermediate fields](@entry_id:153550). Consider the extension $K = \mathbb{Q}(\sqrt[4]{2}, \sqrt[6]{3})$. We have $[\mathbb{Q}(\sqrt[4]{2}):\mathbb{Q}]=4$ (from the [irreducible polynomial](@entry_id:156607) $x^4-2$) and $[\mathbb{Q}(\sqrt[6]{3}):\mathbb{Q}]=6$ (from $x^6-3$). The degree of the compositum is $[K:\mathbb{Q}] = (4 \cdot 6) / [\mathbb{Q}(\sqrt[4]{2}) \cap \mathbb{Q}(\sqrt[6]{3}):\mathbb{Q}]$. A careful analysis shows that the only [subfield](@entry_id:155812) common to both $\mathbb{Q}(\sqrt[4]{2})$ and $\mathbb{Q}(\sqrt[6]{3})$ is $\mathbb{Q}$ itself. One way to see this is by examining their unique quadratic subfields: $\mathbb{Q}(\sqrt{2})$ is the unique quadratic [subfield](@entry_id:155812) of $\mathbb{Q}(\sqrt[4]{2})$, while $\mathbb{Q}(\sqrt{3})$ is the unique quadratic [subfield](@entry_id:155812) of $\mathbb{Q}(\sqrt[6]{3})$. Since these are different, the intersection can be no larger than $\mathbb{Q}$. Thus, the intersection has degree 1, and $[K:\mathbb{Q}] = 24$.

### Important Characteristics and Distinctions

While the definition of a [radical extension](@entry_id:148058) is straightforward, several subtleties are crucial for its correct application in Galois theory.

First, one must distinguish a general [radical extension](@entry_id:148058) from a **simple [radical extension](@entry_id:148058)**. A field like $K=\mathbb{Q}(\sqrt{p}, \sqrt{q})$ for distinct primes $p, q$ is clearly a [radical extension](@entry_id:148058) via the tower $\mathbb{Q} \subset \mathbb{Q}(\sqrt{p}) \subset K$. However, $K$ is not a simple [radical extension](@entry_id:148058) of $\mathbb{Q}$; it cannot be written as $\mathbb{Q}(\alpha)$ for some $\alpha$ with $\alpha^n \in \mathbb{Q}$. For example, the element $\beta = \sqrt{p}+\sqrt{q}$ is a [primitive element](@entry_id:154321), meaning $\mathbb{Q}(\beta) = \mathbb{Q}(\sqrt{p}, \sqrt{q})$. Its minimal polynomial is $x^4 - 2(p+q)x^2 + (p-q)^2 = 0$, which is not of the form $x^4 - c = 0$. The set of all radical extensions is far richer than the set of simple radical extensions.

Second, and most critically, a [radical extension](@entry_id:148058) is **not necessarily a [normal extension](@entry_id:155744)**. A finite extension $L/F$ is normal if every [irreducible polynomial](@entry_id:156607) in $F[x]$ that has one root in $L$ must have all its roots in $L$. The classic counterexample is $K = \mathbb{Q}(\sqrt[3]{7})$. This is a simple [radical extension](@entry_id:148058) of $\mathbb{Q}$. However, the minimal polynomial of its generator, $x^3-7$, has three roots in the complex numbers: $\sqrt[3]{7}$, $\sqrt[3]{7}\omega$, and $\sqrt[3]{7}\omega^2$, where $\omega = \exp(2\pi i / 3)$ is a primitive cube root of unity. The field $K$ is a subfield of $\mathbb{R}$ and thus cannot contain the two non-real roots. Since the polynomial does not split completely in $K$, the extension $K/\mathbb{Q}$ is not normal. This fact has profound consequences, as the Fundamental Theorem of Galois Theory applies to Galois extensions, which are by definition normal and separable.

The property of being radical is therefore distinct from other field properties. The [splitting field](@entry_id:156669) of $x^4-2$ over $\mathbb{Q}$, which is $\mathbb{Q}(\sqrt[4]{2}, i)$, is a [radical extension](@entry_id:148058). The biquadratic extension $\mathbb{Q}(\sqrt{5}, \sqrt{7})$ is another example; it is a Galois extension of degree 4 whose Galois group is the Klein four-group $V_4$. By the Galois correspondence, it has exactly three subgroups of order 2, which correspond to three distinct quadratic subfields: $\mathbb{Q}(\sqrt{5})$, $\mathbb{Q}(\sqrt{7})$, and $\mathbb{Q}(\sqrt{35})$. However, not all extensions are radical. A striking [counterexample](@entry_id:148660) is the field $K = \mathbb{Q}(\cos(2\pi/7))$. This is a real field, and it can be shown that $[K:\mathbb{Q}]=3$ and that the extension $K/\mathbb{Q}$ is Galois. If $K$ were a [radical extension](@entry_id:148058) of $\mathbb{Q}$, its prime degree would force it to be a simple [radical extension](@entry_id:148058), $K=\mathbb{Q}(\sqrt[3]{a})$ for some $a \in \mathbb{Q}$. But as we have seen, an extension of the form $\mathbb{Q}(\sqrt[3]{a})$ is not a [normal extension](@entry_id:155744) over $\mathbb{Q}$, which contradicts the fact that $K/\mathbb{Q}$ is a normal (Galois) extension. Therefore, $\mathbb{Q}(\cos(2\pi/7))$ is not a [radical extension](@entry_id:148058) of $\mathbb{Q}$.

### The Bridge to Solvability: Galois's Criterion

The entire purpose of developing the machinery of radical extensions is to formalize the notion of solving a polynomial by radicals. We can now state the precise definition.

A polynomial $p(x) \in F[x]$ is said to be **[solvable by radicals](@entry_id:154609)** if its [splitting field](@entry_id:156669), $E$, is contained in some [radical extension](@entry_id:148058) of $F$. That is, there exists a [radical extension](@entry_id:148058) $K/F$ such that $E \subseteq K$.

Note that the definition requires only that the [splitting field](@entry_id:156669) be a *[subfield](@entry_id:155812)* of a [radical extension](@entry_id:148058) ($E \subseteq K$), not that the [splitting field](@entry_id:156669) itself must be the endpoint of a radical tower ($E=K$). This flexibility is essential. In many proofs, it is convenient to first adjoin roots of unity to the base field to ensure that the subsequent simple radical extensions are Galois. This auxiliary construction may result in a [radical extension](@entry_id:148058) $K$ that is strictly larger than the [splitting field](@entry_id:156669) $E$.

This definition forms the bridge to the celebrated result at the heart of Galois theory. The **Galois Criterion for Solvability** states:

*A polynomial $p(x)$ over a field of characteristic zero is [solvable by radicals](@entry_id:154609) if and only if its Galois group is a [solvable group](@entry_id:147558).*

A group $G$ is **solvable** if it has a chain of subgroups $\{e\} = G_k \subseteq G_{k-1} \subseteq \dots \subseteq G_0 = G$ where each $G_{i+1}$ is a normal subgroup of $G_i$ and the [quotient group](@entry_id:142790) $G_i/G_{i+1}$ is abelian. This group-theoretic property, which appears purely abstract, perfectly mirrors the structure of a radical tower.

This criterion provides a definitive test for the solvability of any given polynomial equation. The general [quintic polynomial](@entry_id:753983) has the [symmetric group](@entry_id:142255) $S_5$ as its Galois group. The group $S_5$ is famously **not solvable** because its derived series terminates at the alternating group $A_5$, which is a non-abelian simple group.

Consider the specific polynomial $p(x) = x^5 - 4x + 2 \in \mathbb{Q}[x]$. Using techniques beyond the scope of this chapter, one can show that its Galois group over $\mathbb{Q}$ is isomorphic to $S_5$. Since $S_5$ is not a [solvable group](@entry_id:147558), the Galois Criterion allows us to conclude immediately that $p(x)$ is not [solvable by radicals](@entry_id:154609). This means there is no "formula" for the roots of this polynomial that uses only rational numbers, arithmetic operations, and root extractions. Consequently, its [splitting field](@entry_id:156669) cannot be contained within any [radical extension](@entry_id:148058) of $\mathbb{Q}$. This stunning conclusion, the insolvability of the general quintic, is the historical culmination of the theory of radical extensions and the crowning achievement of Evariste Galois.