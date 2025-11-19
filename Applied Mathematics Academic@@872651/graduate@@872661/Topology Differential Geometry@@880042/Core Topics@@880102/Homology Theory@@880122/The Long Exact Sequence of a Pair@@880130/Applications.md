## Applications and Interdisciplinary Connections

Having established the algebraic machinery of the [long exact sequence of a pair](@entry_id:158857) in the preceding chapter, we now turn our attention to its applications. This sequence is far more than a formal curiosity; it is a powerful and versatile tool that lies at the heart of numerous computational methods and theoretical proofs in algebraic topology. Its utility extends across the discipline, from foundational calculations of the homology of simple spaces to proving deep structural theorems in [geometric topology](@entry_id:149613) and making connections to knot theory, Lie group theory, and homotopy theory. This chapter aims to demonstrate this breadth, illustrating how the abstract sequence of groups and homomorphisms provides concrete answers to geometric and topological questions.

### Foundational Computations and Structural Insights

One of the primary applications of the [long exact sequence](@entry_id:153438) is the calculation of homology groups that are otherwise difficult to access. By relating the homology of a space $X$ and a subspace $A$ to the more computable [relative homology](@entry_id:159348) of the pair $(X,A)$, the sequence often allows for an inductive or comparative approach to determining [topological invariants](@entry_id:138526).

#### The Suspension Isomorphism and the Homology of Spheres

A classic and fundamental application of the [long exact sequence](@entry_id:153438) is the recursive computation of the homology groups of spheres. The $n$-sphere, $S^n$, is the boundary of the $(n+1)$-disk, $D^{n+1}$. This naturally suggests studying the pair $(D^{n+1}, S^n)$. The disk $D^{n+1}$ is contractible, which implies that all of its [reduced homology](@entry_id:274187) groups are trivial: $\tilde{H}_k(D^{n+1}) = 0$ for all $k$.

Consider the portion of the [long exact sequence](@entry_id:153438) in [reduced homology](@entry_id:274187) for the pair $(D^n, S^{n-1})$:
$$ \dots \to \tilde{H}_k(D^n) \to \tilde{H}_k(D^n, S^{n-1}) \xrightarrow{\partial} \tilde{H}_{k-1}(S^{n-1}) \to \tilde{H}_{k-1}(D^n) \to \dots $$
Since $\tilde{H}_k(D^n) = 0$ for all $k$, this sequence contains long segments of zeros. Exactness forces the [connecting homomorphism](@entry_id:160713) $\partial$ to be an [isomorphism](@entry_id:137127) for all $k \ge 1$:
$$ \tilde{H}_k(D^n, S^{n-1}) \cong \tilde{H}_{k-1}(S^{n-1}) $$
Furthermore, for a "good pair" like $(D^n, S^{n-1})$, the [relative homology](@entry_id:159348) group is isomorphic to the [reduced homology](@entry_id:274187) of the [quotient space](@entry_id:148218) $D^n/S^{n-1}$. Geometrically, collapsing the boundary sphere $S^{n-1}$ of a disk $D^n$ to a point yields the sphere $S^n$. Thus, $\tilde{H}_k(D^n, S^{n-1}) \cong \tilde{H}_k(S^n)$.

Combining these isomorphisms yields the celebrated **[suspension isomorphism](@entry_id:156388)**:
$$ \tilde{H}_k(S^n) \cong \tilde{H}_{k-1}(S^{n-1}) $$
This powerful recurrence relation allows for the computation of the homology of all spheres by induction. Beginning with the [base case](@entry_id:146682) of the $0$-sphere $S^0$ (two points), for which $\tilde{H}_0(S^0) \cong \mathbb{Z}$, we can iteratively determine all other groups. For example, $\tilde{H}_2(S^2) \cong \tilde{H}_1(S^1) \cong \tilde{H}_0(S^0) \cong \mathbb{Z}$. In general, this leads to the result that for $n \ge 1$, $\tilde{H}_n(S^n) \cong \mathbb{Z}$ and $\tilde{H}_k(S^n)=0$ for $k \neq n$. [@problem_id:1687315]

This same structural principle holds in cohomology. The cone on a space $X$, denoted $CX$, is contractible. Considering the pair $(CX, X)$, the long exact sequence in [reduced cohomology](@entry_id:268050) provides an [isomorphism](@entry_id:137127) $\tilde{H}^k(X) \cong \tilde{H}^{k+1}(CX,X)$. Since the [quotient space](@entry_id:148218) $CX/X$ is the suspension $SX$, this leads to the [suspension isomorphism](@entry_id:156388) in cohomology: $\tilde{H}^k(X) \cong \tilde{H}^{k+1}(SX)$. [@problem_id:1661656]

#### Unraveling Relative Homology

The [long exact sequence](@entry_id:153438) is also the primary tool for computing [relative homology groups](@entry_id:159711) themselves. In many cases, the absolute homology groups of $X$ and $A$ are known, and the sequence can be used to solve for $H_n(X,A)$. Consider the elementary pair $(X, A)$ where $X$ is the closed interval $[0,1]$ and $A$ is its two-point boundary $\{0,1\}$. The relevant portion of the [long exact sequence](@entry_id:153438) is:
$$ H_1(X) \to H_1(X, A) \xrightarrow{\partial_1} H_0(A) \xrightarrow{i_*} H_0(X) \to \dots $$
Since $X$ is contractible, $H_1(X)=0$ and $H_0(X) \cong \mathbb{Z}$. The subspace $A$ is two discrete points, so $H_0(A) \cong \mathbb{Z} \oplus \mathbb{Z}$, with a basis given by the homology classes of the points, $[0]$ and $[1]$. The inclusion map $i: A \hookrightarrow X$ sends both points into the same path-component of $X$. Thus, the [induced map](@entry_id:271712) $i_*$ sends an element $n[0] + m[1]$ to $(n+m)[\text{pt}]$. By exactness, the image of the [connecting homomorphism](@entry_id:160713) $\partial_1$ must equal the kernel of $i_*$. The kernel of $i_*$ consists of all [linear combinations](@entry_id:154743) $n[0] + m[1]$ such that $n+m=0$. This is precisely the infinite [cyclic subgroup](@entry_id:138079) generated by the element $[1] - [0]$. Thus, the [long exact sequence](@entry_id:153438) gives us a precise algebraic description of how the boundary is identified within the larger space. [@problem_id:1687288]

A more subtle example is the pair $(S^2, A)$ where $A$ is the equator, a subspace homeomorphic to $S^1$. To compute $H_2(S^2, A)$, we examine the sequence:
$$ H_2(A) \to H_2(S^2) \to H_2(S^2, A) \xrightarrow{\partial_2} H_1(A) \to H_1(S^2) $$
Substituting the known homology groups for spheres and circles ($A \cong S^1$), we have:
$$ 0 \to \mathbb{Z} \to H_2(S^2, A) \xrightarrow{\partial_2} \mathbb{Z} \to 0 $$
This segment is a [short exact sequence](@entry_id:137930). The map $H_1(A) \to H_1(S^2)$ is zero because the equator, while a [non-trivial loop](@entry_id:267469) in $A$, is null-homologous in $S^2$ (it bounds the northern hemisphere, for instance). An important result in [homological algebra](@entry_id:155139) states that a [short exact sequence](@entry_id:137930) of abelian groups $0 \to K \to G \to F \to 0$ "splits" (meaning $G \cong K \oplus F$) if $F$ is a free abelian group. Since the group $\mathbb{Z}$ on the right is free, our sequence splits. This yields the somewhat surprising result that $H_2(S^2, A) \cong \mathbb{Z} \oplus \mathbb{Z}$. This computation would be considerably more difficult without the organizational power of the long exact sequence. [@problem_id:1687324]

### Applications in Geometric Topology

The long exact sequence is a key instrument for proving fundamental theorems about the properties of topological spaces and maps between them.

#### Proving the Non-Existence of Retractions

A subspace $A \subset X$ is a retract of $X$ if there exists a continuous map $r: X \to A$ such that $r(a)=a$ for all $a \in A$. If such a retraction exists, the [functoriality of homology](@entry_id:269512) implies that the composition of induced maps $r_* \circ i_*: H_n(A) \to H_n(X) \to H_n(A)$ must be the identity map on $H_n(A)$. A necessary consequence is that the map $i_*: H_n(A) \to H_n(X)$ must be injective for all $n$. The long exact sequence can be used to show that this condition fails in many important cases, thus proving that no retraction can exist.

The most famous example is showing that the sphere $S^{n-1}$ is not a retract of the disk $D^n$ for $n \ge 1$. If a retraction existed, the inclusion map $i_*: H_{n-1}(S^{n-1}) \to H_{n-1}(D^n)$ would have to be injective. However, we know $H_{n-1}(S^{n-1}) \cong \mathbb{Z}$ (for $n \ge 2$), while $H_{n-1}(D^n) = 0$ since the disk is contractible. A map from a non-[trivial group](@entry_id:151996) to the trivial group cannot be injective. This contradiction proves that no such retraction exists. This result is a crucial lemma in the proof of the Brouwer Fixed-Point Theorem. [@problem_id:1691857]

The same logic applies to more complex spaces. For instance, one can prove that the boundary circle $\partial M$ of a Möbius strip $M$ is not a retract of $M$. The argument is more subtle and requires the use of coefficients in $\mathbb{Z}_2$. By analyzing the long exact sequence for the pair $(M, \partial M)$ with $\mathbb{Z}_2$ coefficients, one can demonstrate that the [induced map](@entry_id:271712) $i_*: H_1(\partial M; \mathbb{Z}_2) \to H_1(M; \mathbb{Z}_2)$ is the zero map. Since $H_1(\partial M; \mathbb{Z}_2) \cong \mathbb{Z}_2$ is non-trivial, this map is not injective, and thus no retraction is possible. [@problem_id:1687306]

#### Knot Theory and Seifert Surfaces

The [long exact sequence of a pair](@entry_id:158857) provides a bridge between the intrinsic topology of a [knot complement](@entry_id:264989) and extrinsic invariants of the knot. Let $K$ be a knot in $S^3$, and let $X_K = S^3 \setminus N(K)$ be its exterior, where $N(K)$ is an open tubular neighborhood of $K$. The boundary $\partial X_K$ is a torus. The [connecting homomorphism](@entry_id:160713) in the [long exact sequence](@entry_id:153438) for the pair $(X_K, \partial X_K)$,
$$ \partial_*: H_2(X_K, \partial X_K) \to H_1(\partial X_K) $$
has a profound geometric interpretation. An element of the relative group $H_2(X_K, \partial X_K)$ is represented by an oriented surface properly embedded in the knot exterior. The map $\partial_*$ sends the class of this surface to the homology class of its boundary curve on the torus $\partial X_K$.

A key surface associated with any knot is its Seifert surface. A Seifert surface $S_K$ gives rise to a class $\gamma \in H_2(X_K, \partial X_K)$. The image $\partial_*(\gamma)$ is the homology class of the boundary of $S_K$ pushed off into $\partial X_K$. For the standard basis of $H_1(\partial X_K) \cong \mathbb{Z} \oplus \mathbb{Z}$, given by the meridian $[\mu]$ and longitude $[\lambda]$, this class can be explicitly calculated. For the right-handed trefoil knot, for example, the image is $3[\mu] + [\lambda]$. The coefficient of the meridian class corresponds to the writhe of the knot diagram from which the Seifert surface was constructed. This demonstrates a beautiful and deep connection between the algebraic structure of the long exact sequence and the [geometric invariants](@entry_id:178611) of knots. [@problem_id:1056347]

#### Decomposing and Constructing Spaces

The [long exact sequence](@entry_id:153438) is invaluable for understanding the homology of spaces that are constructed by gluing simpler pieces together. A common construction is the [mapping cone](@entry_id:261103) $C_f$ of a map $f: X \to Y$. The homology of $C_f$ is related to the homology of $X$ and $Y$ by a [long exact sequence](@entry_id:153438):
$$ \dots \to H_n(X) \xrightarrow{f_*} H_n(Y) \to H_n(C_f) \to H_{n-1}(X) \to \dots $$
This allows for the direct computation of $H_n(C_f)$ as the cokernel of one map and the kernel of another. For instance, if we consider a map $f: S^1 \to T^2$ that traces a $(p,q)$-torus knot, the [induced map](@entry_id:271712) on first homology sends the generator of $H_1(S^1) \cong \mathbb{Z}$ to the element representing the class $p[\mu] + q[\lambda]$ in $H_1(T^2) \cong \mathbb{Z} \oplus \mathbb{Z}$. The long exact sequence shows that $H_1(C_f)$ is the cokernel of this map, which is isomorphic to $\mathbb{Z} \oplus \mathbb{Z}_{\gcd(p,q)}$. [@problem_id:1056325]

This principle can be combined with other tools like the Excision Theorem. For a space $X$ formed by gluing a torus-with-a-hole $T_0$ to a Möbius strip $M$ along their boundaries, one might want to compute a relative group like $H_1(X, M)$. By excision, this group is isomorphic to $H_1(T_0, \partial T_0)$. One can then apply the long exact sequence to the pair $(T_0, \partial T_0)$ to compute this latter group, ultimately finding it to be isomorphic to $\mathbb{Z} \oplus \mathbb{Z}$. [@problem_id:1056346]

### Interdisciplinary Connections and Generalizations

The algebraic structure embodied by the [long exact sequence of a pair](@entry_id:158857) is not unique to [singular homology](@entry_id:158380). It appears in numerous other contexts within and beyond topology, reflecting a deep categorical principle.

#### The Long Exact Sequence in Homotopy Theory

An entirely analogous long exact sequence exists for the homotopy groups of a pair $(X, A)$:
$$ \dots \to \pi_n(A) \to \pi_n(X) \to \pi_n(X, A) \xrightarrow{\partial} \pi_{n-1}(A) \to \dots $$
This sequence serves as a primary computational tool in homotopy theory. For example, if the total space $X$ is contractible (meaning all its homotopy groups $\pi_k(X)$ are trivial for $k \ge 1$), the long exact sequence immediately collapses to provide an [isomorphism](@entry_id:137127) $\pi_n(X,A) \cong \pi_{n-1}(A)$ for all $n \ge 2$. [@problem_id:1687563]

A central application of this idea arises in the study of loop spaces. For a [pointed space](@entry_id:265918) $(X, x_0)$, the space $PX$ of all paths starting at $x_0$ is contractible. The [loop space](@entry_id:160867) $\Omega X$ is the subspace of $PX$ consisting of paths that also end at $x_0$. Applying the [long exact sequence](@entry_id:153438) of the pair $(PX, \Omega X)$ yields an isomorphism $\pi_n(PX, \Omega X) \cong \pi_{n-1}(\Omega X)$. Combined with the fundamental isomorphism $\pi_{k-1}(\Omega X) \cong \pi_k(X)$, this allows us to identify the relative homotopy group $\pi_n(PX, \Omega X)$ directly with the absolute homotopy group $\pi_n(X)$, providing a key insight into the structure of homotopy groups. [@problem_id:1687542]

#### Homology of Lie Groups and Homogeneous Spaces

The long exact sequence is a powerful tool for studying the topology of Lie groups and their associated [homogeneous spaces](@entry_id:271488), which are central objects in differential geometry and theoretical physics. For instance, consider the special orthogonal groups and the standard inclusion of $SO(4)$ into $SO(5)$. To compute the [relative homology](@entry_id:159348) group $H_4(SO(5), SO(4))$, we can analyze a portion of the long exact sequence for the pair $(SO(5), SO(4))$:
$$ \dots \to H_4(SO(5)) \to H_4(SO(5), SO(4)) \xrightarrow{\partial} H_3(SO(4)) \xrightarrow{i_*} H_3(SO(5)) \to \dots $$
It is known that $H_4(SO(5)) = 0$, $H_3(SO(4)) \cong \mathbb{Z} \oplus \mathbb{Z}$, and $H_3(SO(5)) \cong \mathbb{Z}$. From the sequence, exactness at $H_4(SO(5), SO(4))$ implies that the [connecting homomorphism](@entry_id:160713) $\partial$ is injective, since the map from $H_4(SO(5))$ is zero. Exactness at $H_3(SO(4))$ implies that the image of $\partial$ is equal to the kernel of $i_*$. Further analysis from Lie group theory shows that the map $i_*: H_3(SO(4)) \to H_3(SO(5))$ has a kernel isomorphic to $\mathbb{Z}$. Since $\partial$ is an [injective map](@entry_id:262763) with an image isomorphic to $\mathbb{Z}$, its domain must also be isomorphic to $\mathbb{Z}$. Therefore, $H_4(SO(5), SO(4)) \cong \mathbb{Z}$. This result agrees with the fact that the [quotient space](@entry_id:148218) $SO(5)/SO(4)$ is homeomorphic to the sphere $S^4$. [@problem_id:1056271]

#### Connections to Fiber Bundles

Fiber bundles are another class of geometric objects whose topology is often fruitfully studied using long [exact sequences](@entry_id:151503). The famous Hopf [fibration](@entry_id:162085) is a map $h: S^3 \to S^2$. The preimage of any point in $S^2$ is a circle, but the [preimage](@entry_id:150899) of a larger subspace can be more complex. For instance, the preimage of the equator of $S^2$ is a torus $T^2$ embedded in $S^3$. To compute the [relative homology](@entry_id:159348) group $H_2(S^3, T^2)$, the long exact sequence of the pair $(S^3, T^2)$ is ideal. Given that $H_2(S^3)=0$ and $H_1(S^3)=0$, the sequence simplifies dramatically to show that the [connecting homomorphism](@entry_id:160713) $\partial: H_2(S^3, T^2) \to H_1(T^2)$ is an [isomorphism](@entry_id:137127). Since $H_1(T^2) \cong \mathbb{Z} \oplus \mathbb{Z}$, we immediately find that $H_2(S^3, T^2) \cong \mathbb{Z} \oplus \mathbb{Z}$. [@problem_id:1056328]

### A Glimpse Towards Advanced Topics: Spectral Sequences

The [long exact sequence of a pair](@entry_id:158857) can be understood as the simplest case of a more powerful and general algebraic tool: the spectral sequence. A spectral sequence arises from a filtered [chain complex](@entry_id:150246), such as the [cellular chain complex](@entry_id:160435) $C_*(X)$ filtered by the [subcomplex](@entry_id:264130) $C_*(A)$. This filtration generates a sequence of "pages" $E^r$, each a collection of [abelian groups](@entry_id:145145), that successively approximate the homology of the total space.

For the filtration of $C_*(X)$ by $A$, the $E^1$ page has only two non-zero columns, which are precisely the homology groups of the building blocks: $E^1_{0,q} \cong H_q(A)$ and $E^1_{1,q} \cong H_{q+1}(X,A)$. The differential $d^1: E^1_{1,q} \to E^1_{0,q}$ on this page is exactly the [connecting homomorphism](@entry_id:160713) $\partial$ from the [long exact sequence](@entry_id:153438). The next page, $E^2$, is the homology of the $E^1$ page. A calculation shows that the non-zero terms on the $E^2$ page are exactly the images of the maps in the long exact sequence: $E^2_{0,q} \cong \text{im}(i_*: H_q(A) \to H_q(X))$ and $E^2_{1,q-1} \cong \text{im}(j_*: H_q(X) \to H_q(X,A))$. In this sense, the spectral sequence "rebuilds" the [long exact sequence](@entry_id:153438) and reveals it as a fundamental structural consequence of filtering a [chain complex](@entry_id:150246). [@problem_id:1659703]

In conclusion, the [long exact sequence of a pair](@entry_id:158857) is a unifying thread that runs through much of modern topology. It is a computational workhorse, a proof-writing engine, and a structural principle that reveals deep connections between a space and its subspaces. Its reappearance in homotopy theory, cohomology, and as a precursor to [spectral sequences](@entry_id:158626) underscores its fundamental importance in the algebraic toolkit of any topologist or geometer.