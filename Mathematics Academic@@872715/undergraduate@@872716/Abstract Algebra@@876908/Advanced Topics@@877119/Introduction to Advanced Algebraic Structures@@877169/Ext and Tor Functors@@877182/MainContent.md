## Introduction
In the study of abstract algebra, the Hom and tensor product functors are essential tools for understanding the relationships between modules. However, a crucial observation is that these [functors](@entry_id:150427) are not fully "exact"—they do not perfectly preserve the structure of short [exact sequences](@entry_id:151503). This apparent "failure" is, in fact, a gateway to a deeper level of algebraic insight. The Ext and Tor functors provide the precise mathematical language to measure and harness this inexactness, revealing hidden properties of modules and rings.

This article provides a comprehensive introduction to these powerful tools of [homological algebra](@entry_id:155139). It addresses the knowledge gap left by the inexactness of basic [functors](@entry_id:150427) and demonstrates how their "derived" counterparts, Ext and Tor, offer a solution.

First, in **Principles and Mechanisms**, we will construct the Ext and Tor functors from the ground up, starting with the foundational concept of a [projective resolution](@entry_id:154686). We will explore their core definitions and fundamental properties, establishing the mechanical framework for their computation. Next, in **Applications and Interdisciplinary Connections**, we will see these abstract tools in action, exploring how they solve concrete problems in [module theory](@entry_id:139410), classify [group extensions](@entry_id:195070), and forge profound links to [commutative algebra](@entry_id:149047) and algebraic topology. Finally, our **Hands-On Practices** will guide you through explicit calculations, solidifying your theoretical understanding and building practical skill in applying these essential [functors](@entry_id:150427).

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental functors of [module theory](@entry_id:139410), namely the tensor product and the Hom functor. We observed that while these [functors](@entry_id:150427) are invaluable, they are not, in general, fully exact. The tensor product functor, $A \otimes_R -$, is right-exact, meaning it preserves the exactness of the right-hand side of a [short exact sequence](@entry_id:137930). Dually, the Hom functors, $\mathrm{Hom}_R(A, -)$ and $\mathrm{Hom}_R(-, B)$, are left-exact. This "failure" of [exactness](@entry_id:268999) is not a deficiency but rather a source of deep structural information about the modules involved. The principles and mechanisms we explore in this chapter, centered on the **Tor** and **Ext** functors, provide the [formal language](@entry_id:153638) to measure, understand, and utilize this failure. These are the **derived functors** of the [tensor product](@entry_id:140694) and Hom [functors](@entry_id:150427), respectively.

### Projective Resolutions: The Foundational Construction

To define Tor and Ext, we first require a standard "measuring stick" against which we can compare other modules. In [homological algebra](@entry_id:155139), this role is played by **[projective modules](@entry_id:149251)**. An $R$-module $P$ is called **projective** if it satisfies a certain [lifting property](@entry_id:156717): for any surjective $R$-[module homomorphism](@entry_id:148144) $f: M \to N$ and any homomorphism $g: P \to N$, there exists a lift, a homomorphism $h: P \to M$, such that $f \circ h = g$. While this definition is abstract, a more concrete and immensely useful fact is that all **[free modules](@entry_id:152514)** are projective.

The core construction for defining derived functors is the **[projective resolution](@entry_id:154686)**. A [projective resolution](@entry_id:154686) of an $R$-module $A$ is a long exact sequence of [projective modules](@entry_id:149251) that "terminates" at $A$:
$$ \cdots \xrightarrow{d_{n+1}} P_n \xrightarrow{d_n} P_{n-1} \xrightarrow{d_{n-1}} \cdots \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} A \to 0 $$
Here, each $P_i$ is a projective $R$-module, and the sequence is exact, meaning $\mathrm{Im}(d_{i+1}) = \ker(d_i)$ for all $i \ge 1$ and $\mathrm{Im}(d_1) = \ker(\epsilon)$. Such a resolution can always be constructed for any module $A$. One begins by finding a surjective map $\epsilon: P_0 \to A$ from a [projective module](@entry_id:149393) $P_0$ (e.g., a [free module](@entry_id:150200) mapping onto the generators of $A$). Its kernel, $\ker(\epsilon)$, is then the target of a new surjective map from another [projective module](@entry_id:149393) $P_1$, and this process is iterated.

For modules over the integers $\mathbb{Z}$, which are simply abelian groups, a common and important example is the resolution of a [cyclic group](@entry_id:146728) $\mathbb{Z}/n\mathbb{Z}$. The natural projection $\epsilon: \mathbb{Z} \to \mathbb{Z}/n\mathbb{Z}$ is a [surjection](@entry_id:634659) from the [free module](@entry_id:150200) $\mathbb{Z}$. Its kernel is the submodule of integers divisible by $n$, which is isomorphic to $\mathbb{Z}$ via the multiplication-by-$n$ map, $d_1(x) = nx$. This gives a very short and elegant [projective resolution](@entry_id:154686):
$$ 0 \to \mathbb{Z} \xrightarrow{d_1} \mathbb{Z} \xrightarrow{\epsilon} \mathbb{Z}/n\mathbb{Z} \to 0 $$
This two-step resolution is a recurring tool in our calculations.

### The Tor Functors: Quantifying Tensor Product Behavior

The Tor functors, denoted $\mathrm{Tor}_n^R(A, B)$, are designed to measure the failure of the [tensor product](@entry_id:140694) functor to be exact. The mechanism for their construction is systematic and revealing.

**Construction and Definition**

To compute $\mathrm{Tor}_n^R(A, B)$, one performs the following steps:
1.  Construct a [projective resolution](@entry_id:154686) of the module $A$: $ \cdots \to P_1 \to P_0 \to A \to 0 $.
2.  Remove the module $A$ to obtain the **[chain complex](@entry_id:150246)** of [projective modules](@entry_id:149251), which we denote $P_\bullet$.
3.  Apply the right-exact [functor](@entry_id:260898) $- \otimes_R B$ to this complex. This yields a new [chain complex](@entry_id:150246):
    $$ \cdots \to P_1 \otimes_R B \xrightarrow{d_1 \otimes 1} P_0 \otimes_R B \to 0 $$
4.  The Tor groups are defined as the **homology groups** of this new complex. Recall that the $n$-th homology group of a [chain complex](@entry_id:150246) is given by the quotient $\ker(\text{outgoing map}) / \mathrm{Im}(\text{incoming map})$. Specifically:
    $$ \mathrm{Tor}_n^R(A, B) = H_n(P_\bullet \otimes_R B) = \frac{\ker(d_n \otimes 1)}{\mathrm{Im}(d_{n+1} \otimes 1)} $$

By convention, $\mathrm{Tor}_0^R(A, B) = H_0(P_\bullet \otimes_R B) = (P_0 \otimes_R B) / \mathrm{Im}(d_1 \otimes 1)$. Since the original sequence is exact, $\mathrm{Im}(d_1) = \ker(\epsilon)$, and since the tensor functor is right-exact, we have the [isomorphism](@entry_id:137127) $\mathrm{Tor}_0^R(A, B) \cong A \otimes_R B$. The higher Tor [functors](@entry_id:150427), for $n \ge 1$, capture the "hidden" algebraic information that the simple tensor product misses.

A key insight comes from applying the tensor [functor](@entry_id:260898) to a [short exact sequence](@entry_id:137930) $0 \to K \xrightarrow{f} L \to M \to 0$. This yields a sequence that is only guaranteed to be right-exact:
$$ K \otimes_R B \xrightarrow{f \otimes 1} L \otimes_R B \to M \otimes_R B \to 0 $$
The map $f \otimes 1$ is not generally injective. The long exact sequence in homology reveals that its kernel is precisely $\mathrm{Tor}_1^R(M, B)$. For instance, consider the multiplication-by-$n$ map $f: \mathbb{Z} \to \mathbb{Z}$. When we tensor with $\mathbb{Z}/m\mathbb{Z}$, we get an [induced map](@entry_id:271712) $\tilde{f}: \mathbb{Z} \otimes_{\mathbb{Z}} (\mathbb{Z}/m\mathbb{Z}) \to \mathbb{Z} \otimes_{\mathbb{Z}} (\mathbb{Z}/m\mathbb{Z})$. This is isomorphic to the multiplication-by-$n$ map on $\mathbb{Z}/m\mathbb{Z}$. The kernel of this map measures the failure of [injectivity](@entry_id:147722). As it turns out, this kernel is precisely $\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z}/m\mathbb{Z})$, which can be computed to be isomorphic to $\mathbb{Z}/\gcd(n,m)\mathbb{Z}$. For $n=42$ and $m=70$, this kernel is $\mathbb{Z}/\gcd(42, 70)\mathbb{Z} \cong \mathbb{Z}/14\mathbb{Z}$ [@problem_id:1793085].

**Fundamental Properties of Tor**

1.  **Vanishing for Projective Modules:** If $A$ is a [projective module](@entry_id:149393), we can choose a trivial [projective resolution](@entry_id:154686) for it: $0 \to A \xrightarrow{\mathrm{id}} A \to 0$. After truncating and tensoring with $B$, the resulting complex has non-zero terms only in degree 0. Consequently, all its homology groups for $n \ge 1$ are trivial. Thus, **$\mathrm{Tor}_n^R(A, B) = 0$ for all $n \ge 1$ if $A$ is projective**. This explains, for example, why $\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}^3, \mathbb{Q}/\mathbb{Z})$ is the zero group, since $\mathbb{Z}^3$ is a free (and therefore projective) $\mathbb{Z}$-module [@problem_id:1793110].

2.  **Vanishing over Principal Ideal Domains:** The ring of integers $\mathbb{Z}$ is a Principal Ideal Domain (PID). A cornerstone theorem of [module theory](@entry_id:139410) states that over a PID, any submodule of a [free module](@entry_id:150200) is also free. This has a profound consequence: every module $A$ over a PID admits a [projective resolution](@entry_id:154686) of length at most 1, of the form $0 \to P_1 \to P_0 \to A \to 0$ [@problem_id:1793097]. When we use this resolution to compute Tor, the resulting [chain complex](@entry_id:150246) $P_\bullet \otimes_R B$ is also short, with terms only in degrees 1 and 0. This immediately implies that its homology is zero for all higher degrees. Therefore, for any PID $R$ (such as $\mathbb{Z}$ or the polynomial ring $k[x]$ over a field), **$\mathrm{Tor}_n^R(A, B) = 0$ for all $n \ge 2$** and any modules $A, B$ [@problem_id:1793097] [@problem_id:1793110]. The maximum $n$ for which $\mathrm{Tor}_n^R(A, B)$ can be non-zero for some $A, B$ is related to the **global dimension** of the ring $R$. For PIDs, this dimension is 1.

### The Ext Functors: From Homomorphisms to Extensions

Dually to Tor, the Ext functors, denoted $\mathrm{Ext}_R^n(A, B)$, arise from the Hom [functor](@entry_id:260898). They are contravariant in the first argument and covariant in the second. We will focus on their construction by resolving the first argument.

**Construction and Definition**

The procedure for constructing $\mathrm{Ext}_R^n(A, B)$ mirrors that for Tor, but with a crucial twist. [@problem_id:1681297]
1.  Take a [projective resolution](@entry_id:154686) of $A$: $ \cdots \to P_1 \to P_0 \to A \to 0 $.
2.  Truncate it by removing $A$, yielding the complex $P_\bullet$.
3.  Apply the **contravariant** functor $\mathrm{Hom}_R(-, B)$. Because it is contravariant, it reverses the direction of all the maps, producing a **cochain complex**:
    $$ 0 \to \mathrm{Hom}_R(P_0, B) \xrightarrow{d_1^*} \mathrm{Hom}_R(P_1, B) \xrightarrow{d_2^*} \mathrm{Hom}_R(P_2, B) \to \cdots $$
    where $d_n^* = \mathrm{Hom}_R(d_n, B)$.
4.  The Ext groups are defined as the **[cohomology groups](@entry_id:142450)** of this cochain complex. The $n$-th cohomology group is given by $\ker(\text{outgoing map}) / \mathrm{Im}(\text{incoming map})$. Specifically:
    $$ \mathrm{Ext}_R^n(A, B) = H^n(\mathrm{Hom}_R(P_\bullet, B)) = \frac{\ker(d_{n+1}^*)}{\mathrm{Im}(d_n^*)} $$

The zeroth Ext group, $\mathrm{Ext}_R^0(A, B)$, is the kernel of $d_1^*$. By the left-[exactness](@entry_id:268999) of $\mathrm{Hom}_R(-, B)$, this is precisely the group of homomorphisms $\mathrm{Hom}_R(A, B)$. For instance, a direct calculation shows that $\mathrm{Ext}_{\mathbb{Z}}^0(\mathbb{Z}/4\mathbb{Z}, \mathbb{Z}/6\mathbb{Z}) \cong \mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}/4\mathbb{Z}, \mathbb{Z}/6\mathbb{Z})$, which is isomorphic to $\mathbb{Z}/\gcd(4,6)\mathbb{Z} \cong \mathbb{Z}/2\mathbb{Z}$ [@problem_id:1793105].

**Fundamental Properties of Ext**

1.  **Vanishing for Projective Modules:** Just as with Tor, if $A$ is a [projective module](@entry_id:149393), its trivial resolution $0 \to A \to A \to 0$ leads to a cochain complex for Ext with terms only in degree 0. This means **$\mathrm{Ext}_R^n(A, B) = 0$ for all $n \ge 1$ if $A$ is projective**. For example, since $\mathbb{Z} \oplus \mathbb{Z}$ is a free (hence projective) $\mathbb{Z}$-module, $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z} \oplus \mathbb{Z}, \mathbb{Z}/30\mathbb{Z})$ must be the [trivial group](@entry_id:151996) [@problem_id:1793091].

2.  **Non-Symmetry:** Unlike the [tensor product](@entry_id:140694), which is commutative up to [isomorphism](@entry_id:137127), the Ext functor is not symmetric in its arguments. A stark demonstration is provided by comparing $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}, \mathbb{Z}/n\mathbb{Z})$ and $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z})$ [@problem_id:1793080]. The first group is 0 because its first argument, $\mathbb{Z}$, is projective. For the second group, we use the resolution $0 \to \mathbb{Z} \xrightarrow{\times n} \mathbb{Z} \to \mathbb{Z}/n\mathbb{Z} \to 0$ and the associated [long exact sequence](@entry_id:153438) for Ext, which shows that $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}/n\mathbb{Z}$. The two groups are clearly not isomorphic.

3.  **Vanishing over Principal Ideal Domains:** The same property of PIDs that simplifies Tor also applies to Ext. Since any module $A$ over a PID $R$ has a [projective resolution](@entry_id:154686) of length at most 1, the [cochain](@entry_id:275805) complex used to compute Ext is short. This implies that **$\mathrm{Ext}_R^n(A, B) = 0$ for all $n \ge 2$** [@problem_id:1793061].

### Application: The Classification of Group Extensions

Perhaps the most celebrated application of the first Ext group is in the classification of **[module extensions](@entry_id:268265)**. An $R$-module $E$ is called an **extension** of $C$ by $A$ if it fits into a [short exact sequence](@entry_id:137930):
$$ 0 \to A \xrightarrow{i} E \xrightarrow{p} C \to 0 $$
This means that $A$ is isomorphic to a submodule of $E$, and $C$ is isomorphic to the corresponding [quotient module](@entry_id:155903) $E/i(A)$. A central question is: for given modules $A$ and $C$, how many non-isomorphic modules $E$ can exist in such a sequence?

The fundamental theorem of this subject states that the set of [equivalence classes](@entry_id:156032) of such extensions forms an [abelian group](@entry_id:139381) that is canonically isomorphic to $\mathrm{Ext}_R^1(C, A)$.

The [identity element](@entry_id:139321) of this group, the zero in $\mathrm{Ext}_R^1(C, A)$, corresponds to the simplest possible extension: the **[split extension](@entry_id:143915)**. A [short exact sequence](@entry_id:137930) is said to split if the middle term $E$ is isomorphic to the [direct sum](@entry_id:156782) $A \oplus C$. The canonical split sequence is:
$$ 0 \to A \xrightarrow{i} A \oplus C \xrightarrow{p} C \to 0 $$
where $i(a) = (a, 0)$ and $p(a, c) = c$.

The correspondence between extensions and elements of Ext can be made explicit. An extension sequence gives rise to a [1-cocycle](@entry_id:144864) in the complex $\mathrm{Hom}_R(P_\bullet, A)$, where $P_\bullet$ is a [projective resolution](@entry_id:154686) of $C$. This cocycle is a coboundary if and only if the extension splits [@problem_id:1793095]. Proving a sequence splits is equivalent to showing its corresponding [cocycle](@entry_id:200749) lies in the image of the map $d_1^*: \mathrm{Hom}_R(P_0, A) \to \mathrm{Hom}_R(P_1, A)$. In the context of a split sequence involving $A = \mathbb{Z}/9\mathbb{Z}$ and $C = \mathbb{Z}/6\mathbb{Z}$, we can explicitly find a homomorphism $\phi: P_0 \to A$ such that the [cocycle](@entry_id:200749) $\alpha$ is given by $\alpha = \phi \circ d_1$, demonstrating that it is a coboundary [@problem_id:1793095].

This powerful correspondence turns an abstract classification problem into a concrete calculation. To find the number of non-isomorphic abelian [group extensions](@entry_id:195070) of $G = \mathbb{Z}/n\mathbb{Z}$ by $N$, we simply need to compute the order of the group $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, N)$. Using the standard resolution of $\mathbb{Z}/n\mathbb{Z}$, one can show that $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, N) \cong N/nN$. For example, the number of non-isomorphic [abelian extensions](@entry_id:152984) of $\mathbb{Z}/12\mathbb{Z}$ by $\mathbb{Z}/18\mathbb{Z}$ is the order of $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/12\mathbb{Z}, \mathbb{Z}/18\mathbb{Z})$, which is isomorphic to $(\mathbb{Z}/18\mathbb{Z}) / (12 \cdot \mathbb{Z}/18\mathbb{Z})$. This [quotient group](@entry_id:142790) has order $\gcd(12, 18) = 6$. Thus, there are exactly 6 such non-isomorphic extensions [@problem_id:1793064]. This result beautifully showcases how the abstract machinery of [homological algebra](@entry_id:155139) solves concrete and fundamental problems in [module theory](@entry_id:139410).