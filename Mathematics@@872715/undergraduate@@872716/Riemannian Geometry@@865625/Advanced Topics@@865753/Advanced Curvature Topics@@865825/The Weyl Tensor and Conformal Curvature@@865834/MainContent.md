## Introduction
In Riemannian geometry, the Riemann curvature tensor offers a complete description of a manifold's curvature, yet its complexity can obscure fundamental geometric truths. To gain deeper insight, mathematicians decompose this tensor into simpler, [irreducible components](@entry_id:153033), each with a distinct geometric meaning. This article focuses on the most subtle of these components: the Weyl tensor, which captures the part of curvature that is invariant under local rescaling of the metric—a property known as [conformal invariance](@entry_id:191867). By exploring this concept, we uncover a powerful tool for understanding the structure of space, from abstract manifolds to the fabric of spacetime.

This exploration is structured into three parts. The first section, **Principles and Mechanisms**, will dissect the algebraic decomposition of the Riemann tensor to formally define the Weyl tensor and establish its fundamental property of [conformal invariance](@entry_id:191867). The second section, **Applications and Interdisciplinary Connections**, will demonstrate the profound impact of the Weyl tensor in general relativity, cosmology, and modern [geometric analysis](@entry_id:157700). Finally, the **Hands-On Practices** section will provide an opportunity to solidify these concepts through guided calculations on key geometric examples.

## Principles and Mechanisms

The Riemann [curvature tensor](@entry_id:181383), $\mathrm{Rm}$, provides a complete local description of the curvature of a Riemannian manifold. However, its complexity often obscures the underlying geometric structures. A powerful technique in [geometric analysis](@entry_id:157700) is to decompose the Riemann tensor into more fundamental, [irreducible components](@entry_id:153033), each with a distinct geometric meaning. This section explores this decomposition, focusing on the component that is invariant under conformal changes of the metric: the Weyl tensor.

### The Algebraic Decomposition of Curvature

On an $n$-dimensional Riemannian manifold $(M,g)$, the Riemann curvature tensor can be viewed at each point as an algebraic object—a tensor with specific symmetries. The space of all such algebraic curvature tensors can be decomposed into irreducible submodules under the action of the [orthogonal group](@entry_id:152531) $O(n)$. This decomposition separates curvature into three distinct types: scalar curvature, trace-free Ricci curvature, and [conformal curvature](@entry_id:637455).

To make this decomposition explicit, we first isolate the trace parts of the Riemann tensor. The first trace yields the **Ricci tensor**, $\mathrm{Ric}_{ik} = g^{jl}R_{jikl}$, and the second trace yields the **[scalar curvature](@entry_id:157547)**, $R = g^{ik}\mathrm{Ric}_{ik}$. These tensors represent averaged curvature information. To isolate the part of the Ricci tensor that is independent of the scalar curvature, we define the **trace-free Ricci tensor**:

$$
\mathrm{Ric}_0 = \mathrm{Ric} - \frac{R}{n} g
$$

By construction, the trace of $\mathrm{Ric}_0$ is zero: $g^{ij}(\mathrm{Ric}_0)_{ij} = R - \frac{R}{n} g^{ij}g_{ij} = R - \frac{R}{n}(n) = 0$. The condition $\mathrm{Ric}_0 \equiv 0$ is equivalent to the metric being an **Einstein metric**, i.e., $\mathrm{Ric} = \lambda g$ for some constant $\lambda = R/n$ (for $n \ge 3$). Thus, $\mathrm{Ric}_0$ measures the deviation of a metric from the Einstein condition. [@problem_id:2994685]

The full Riemann tensor can be reconstructed from these trace components plus a remaining, totally trace-free part. This is achieved using the **Kulkarni-Nomizu product**, denoted by $\owedge$. For two symmetric $(0,2)$-tensors $h$ and $k$, this product is a $(0,4)$-tensor with the same symmetries as the Riemann tensor, defined as:

$$
(h \owedge k)_{ijkl} = h_{ik} k_{jl} + h_{jl} k_{ik} - h_{il} k_{jk} - h_{jk} k_{il}
$$

For dimensions $n \ge 3$, the Riemann tensor decomposes uniquely into three orthogonal components [@problem_id:2994685]:

$$
\mathrm{Rm} = W + \frac{1}{n-2} \mathrm{Ric}_0 \owedge g + \frac{R}{2n(n-1)} g \owedge g
$$

Let us analyze each term in this fundamental decomposition:

1.  **The Scalar Component:** The term $\frac{R}{2n(n-1)} g \owedge g$ represents the part of the curvature determined entirely by the [scalar curvature](@entry_id:157547) $R$. In fact, a space of [constant sectional curvature](@entry_id:272200) $k$ has a Riemann tensor given by $\mathrm{Rm} = k(g \owedge g)/2$. Since for such a space $R = n(n-1)k$, this term is precisely the Riemann tensor of a [constant curvature](@entry_id:162122) space that has the same [scalar curvature](@entry_id:157547) as $(M,g)$. On a space of [constant sectional curvature](@entry_id:272200), both $\mathrm{Ric}_0$ and $W$ vanish identically. [@problem_id:2994685, 1652512]

2.  **The Trace-Free Ricci Component:** The term $\frac{1}{n-2} \mathrm{Ric}_0 \owedge g$ captures the curvature information contained in the trace-free Ricci tensor. It describes the way in which the Ricci curvature deviates from being proportional to the metric.

3.  **The Weyl Component:** The final term, $W$, is the **Weyl [curvature tensor](@entry_id:181383)**. It is defined as the part of the Riemann tensor that remains after the other two components are subtracted. By its very construction, it is **totally trace-free**, meaning that any contraction of it with the metric yields zero. It represents the part of the curvature that is independent of any local averaging process (i.e., taking traces). As we will see, its profound geometric significance lies in its connection to [conformal geometry](@entry_id:186351).

### Conformal Geometry and the Weyl Tensor

A **[conformal transformation](@entry_id:193282)** of a metric $g$ is a rescaling of the form $\tilde{g} = \Omega^2 g$, where $\Omega$ is a smooth, positive function on $M$ called the conformal factor. It is often convenient to write $\Omega^2 = e^{2\phi}$, so $\tilde{g} = e^{2\phi} g$. Such transformations preserve angles between tangent vectors but do not preserve lengths or volumes. The set of all metrics conformal to $g$ forms a **conformal class**.

A central question in [conformal geometry](@entry_id:186351) is to identify quantities that are invariant, or transform simply, under these changes. While the Riemann and Ricci tensors have very complicated transformation laws, the Weyl tensor exhibits a remarkably simple behavior. Under the conformal change $\tilde{g} = e^{2\phi}g$, the $(0,4)$-type Weyl tensor transforms as:

$$
\widetilde{W}_{ijkl} = e^{2\phi} W_{ijkl}
$$

This property is known as **[conformal covariance](@entry_id:189180)**. The Weyl tensor is not strictly invariant, but it scales in the simplest way possible. Even more strikingly, if we consider the Weyl tensor as a $(1,3)$-tensor, $W^i{}_{jkl} = g^{im}W_{mjkl}$, its transformation law is even simpler. Since the [inverse metric](@entry_id:273874) transforms as $\tilde{g}^{im} = e^{-2\phi}g^{im}$, we have:

$$
\widetilde{W}^i{}_{jkl} = \tilde{g}^{im} \widetilde{W}_{mjkl} = (e^{-2\phi}g^{im}) (e^{2\phi}W_{mjkl}) = g^{im}W_{mjkl} = W^i{}_{jkl}
$$

Thus, the $(1,3)$-type Weyl tensor is a true **conformal invariant**. [@problem_id:3078719, 3044697] This remarkable property is why the Weyl tensor is also known as the **[conformal curvature](@entry_id:637455) tensor**.

An immediate and crucial consequence of this invariance is that the condition $W \equiv 0$ is a conformal invariant. If the Weyl tensor of a metric $g$ is zero, it is also zero for any metric $\tilde{g}$ in the same conformal class. [@problem_id:2994685, 3048191] This observation is the key to understanding the geometric meaning of the Weyl tensor.

### The Weyl Tensor as an Obstruction: A Dimensional Story

A Riemannian manifold is said to be **locally conformally flat** if every point has a neighborhood where the metric is conformal to the flat Euclidean metric, i.e., $g = \Omega^2 \delta$ in some [local coordinates](@entry_id:181200). [@problem_id:1532135, 1496675] The flat metric has zero Riemann tensor, and therefore its Weyl tensor is also zero. Since the condition $W \equiv 0$ is a conformal invariant, any locally [conformally flat manifold](@entry_id:201155) must have a vanishing Weyl tensor. The fascinating question is whether the converse is true. The answer depends critically on the dimension of the manifold.

#### Dimension $n \geq 4$: The Realm of the Weyl Tensor

For dimensions four and higher, the Weyl tensor provides the complete answer. The celebrated **Weyl-Schouten theorem** states:

> For $n \geq 4$, a Riemannian manifold $(M,g)$ is locally conformally flat if and only if its Weyl tensor is identically zero ($W \equiv 0$).

Thus, in higher dimensions, the Weyl tensor is precisely the obstruction to a manifold being locally conformal to flat space. It measures the "non-conformally flat" part of the curvature. If $W \neq 0$, no amount of local rescaling can make the metric flat. [@problem_id:3078719, 3044697, 2994685, 1532135, 3048191] We can see this principle in action: any metric of the form $g_\alpha = \exp(2u_\alpha) g_0$ on $\mathbb{R}^n$, where $g_0$ is the flat Euclidean metric, is conformally flat by construction, and a direct calculation confirms that its Weyl tensor is indeed zero for any choice of function $u_\alpha$. [@problem_id:3004976]

#### Dimension $n = 3$: The Rise of the Cotton Tensor

The situation in three dimensions is entirely different and reveals a beautiful subtlety. In dimension $n=3$, an algebraic identity forces the Weyl tensor to be identically zero for *any* Riemannian metric. This can be understood by a dimension-counting argument: the space of algebraic curvature tensors has dimension $\frac{n^2(n^2-1)}{12}$, which for $n=3$ is 6. The space of symmetric 2-tensors (like the Ricci tensor) has dimension $\frac{n(n+1)}{2}$, which for $n=3$ is also 6. This means that, algebraically, the Riemann tensor is completely determined by the Ricci tensor, leaving no room for a trace-free component like the Weyl tensor. [@problem_id:3078719, 3004993]

Since $W \equiv 0$ is a tautology in 3D, it cannot serve as the criterion for [conformal flatness](@entry_id:159514). A new object is needed. This object is the **Cotton tensor**. To define it, we first introduce the **Schouten tensor**, defined for $n \ge 3$ as:

$$
A = \frac{1}{n-2} \left( \mathrm{Ric} - \frac{R}{2(n-1)} g \right)
$$

The Cotton tensor $C$ is then defined as a kind of "curl" of the Schouten tensor:

$$
C_{ijk} = \nabla_i A_{jk} - \nabla_j A_{ik}
$$

where $\nabla$ is the Levi-Civita connection. In dimension $n=3$, the Cotton tensor is conformally invariant. The condition for local [conformal flatness](@entry_id:159514) is then given by a theorem of Schouten:

> For $n=3$, a Riemannian manifold $(M,g)$ is locally conformally flat if and only if its Cotton tensor is identically zero ($C \equiv 0$). [@problem_id:3078719, 1496675, 3004964]

#### Dimension $n=2$

In two dimensions, the situation is simpler still. A classical result states that every 2-dimensional Riemannian metric is locally conformally flat (this is equivalent to the existence of [isothermal coordinates](@entry_id:272481)). There is no obstruction to local [conformal flatness](@entry_id:159514). The standard definitions of the Weyl, Schouten, and Cotton tensors are not applicable as they contain denominators of $(n-2)$. [@problem_id:3004964]

### Interplay of Curvature Tensors and Special Geometries

The relationships between the Weyl, Cotton, and Schouten tensors become particularly clear when examining manifolds with special geometric properties. A key identity, derivable from the second Bianchi identity, connects the divergence of the Weyl tensor to the Cotton tensor for $n \ge 3$:

$$
\nabla^i W_{ikjl} = (n-3) C_{jkl}
$$

where the indices have been arranged according to common conventions. This identity reveals that, up to a dimensional factor, the Cotton tensor *is* the divergence of the Weyl tensor. [@problem_id:3004964]

This has a profound implication for $n \ge 4$. In these dimensions, the condition $C \equiv 0$ is equivalent to the Weyl tensor being divergence-free ($\mathrm{div}(W) = 0$). This is a strictly weaker condition than $W \equiv 0$. Therefore, for $n \ge 4$, a vanishing Cotton tensor does **not** imply local [conformal flatness](@entry_id:159514). [@problem_id:3078719]

This distinction is highlighted by the geometry of **Einstein manifolds**. Recall that these are defined by $\mathrm{Ric} = \lambda g$.
- On an Einstein manifold, the Schouten tensor is simply a multiple of the metric: $A = c \cdot g$.
- Its [covariant derivative](@entry_id:152476) is $\nabla A = 0$, which immediately implies that the Cotton tensor vanishes: $C_{ijk} = 0 - 0 = 0$.
- From the identity above, this means that for any Einstein manifold with $n > 3$, the Weyl tensor is divergence-free. [@problem_id:3044697]

However, many Einstein manifolds are not conformally flat. Classic examples include the complex [projective spaces](@entry_id:157963) $\mathbb{C}P^m$ (for $m \ge 2$) and [product manifolds](@entry_id:270208) like $S^k \times S^k$ (for $k \ge 2$). These spaces have $C \equiv 0$ but $W \not\equiv 0$. This provides a concrete class of examples showing that being [divergence-free](@entry_id:190991) is not enough to force the Weyl tensor to vanish. [@problem_id:3044697]

The intricate transformation laws of the curvature components under a conformal change all conspire to produce the simple [scaling law](@entry_id:266186) for the Weyl tensor. A direct calculation demonstrates this "cancellation magic." If one starts with a general metric and computes its Weyl tensor, then applies a [conformal transformation](@entry_id:193282) and computes the new Riemann, Ricci, and scalar curvatures (which have complex transformation laws), and assembles the new Weyl tensor, the result will simply be the original Weyl tensor scaled by the conformal factor, validating its role as the fundamental object in [conformal geometry](@entry_id:186351). [@problem_id:1559766]