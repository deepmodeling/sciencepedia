## Introduction
In the field of compressed sensing, signals are acquired through a small number of linear measurements, with the promise of perfect recovery enabled by [signal sparsity](@entry_id:754832). However, the transition from theoretical analog measurements to the practical digital domain introduces a significant hurdle: quantization. This necessary process of converting continuous values into a finite set of digital representations is inherently nonlinear and lossy, creating a fundamental challenge for traditional recovery algorithms. How can we accurately reconstruct a sparse signal when our measurements have been coarsely digitized, sometimes to a single bit of information?

This article provides a comprehensive guide to the algorithms and principles designed to solve this very problem. It navigates the complexities of recovering sparse signals from quantized data, offering a structured journey from foundational theory to practical application. The following chapters are designed to build upon one another, providing a complete picture of the field.

First, **"Principles and Mechanisms"** will lay the groundwork by formalizing the quantized measurement model for different quantizer types, including the extreme case of 1-bit sensing. We will explore the crucial geometric concept of consistency sets and analyze how their properties dictate the feasibility of recovery. This chapter also addresses the critical issues of robustness to noise and the stability of reconstruction.

Next, **"Applications and Interdisciplinary Connections"** will showcase how these foundational principles are used to construct powerful recovery algorithms. We will explore different algorithmic paradigms, from loss-minimization frameworks borrowed from machine learning to consistency-based geometric methods and sophisticated Bayesian approaches. This chapter highlights the rich interplay between [compressed sensing](@entry_id:150278), statistics, and optimization that drives modern [algorithm design](@entry_id:634229).

Finally, the **"Hands-On Practices"** section will bridge theory and practice. Through targeted exercises, you will have the opportunity to translate measurement models into optimization penalties, derive the update rules for [iterative algorithms](@entry_id:160288), and analyze critical system-level design trade-offs, solidifying your understanding of how to build and evaluate complete quantized sensing systems.

## Principles and Mechanisms

The transition from the continuous domain of ideal linear measurements to the discrete world of digital representation is the defining characteristic of [quantized compressed sensing](@entry_id:753930). This process, while a practical necessity, introduces a fundamental nonlinearity and information loss that must be carefully managed by recovery algorithms. This chapter delves into the principles governing this transformation and the mechanisms of algorithms designed to overcome its challenges. We will begin by formalizing the measurement model, analyze the geometric structure of the problem, explore various recovery paradigms, and conclude with a discussion of robustness, stability, and system design considerations.

### The Quantized Measurement Model

The canonical [linear measurement model](@entry_id:751316) posits that a signal $x \in \mathbb{R}^{n}$ is measured via a sensing matrix $A \in \mathbb{R}^{m \times n}$, often in the presence of [additive noise](@entry_id:194447) $w \in \mathbb{R}^{m}$. The resulting analog measurements are given by the vector $z = Ax + w$. In a practical system, this analog vector $z$ must be converted into a digital representation, a process accomplished by a quantizer. A quantizer $Q$ is a function that maps continuous-valued inputs to a finite or countably infinite set of output values. The final digital measurements are thus given by $y = Q(z)$, with the quantization typically applied component-wise, i.e., $y_i = Q(z_i)$ for each measurement $i=1, \dots, m$.

The nature of the recovery problem is critically dependent on the type of quantizer employed.

#### Uniform Scalar Quantization

A common and foundational model is the **uniform scalar quantizer**. This quantizer partitions the real line into a series of contiguous intervals, or **bins**, of equal width $\Delta > 0$, known as the **quantization step size**. All input values falling within a given bin are mapped to a single representative output value.

Two primary forms of uniform quantizers are the mid-rise and mid-tread quantizers. Their behavior is defined by the placement of their decision thresholds and reproduction levels [@problem_id:3472927].

-   A **mid-rise quantizer** has decision thresholds at integer multiples of the step size, $k\Delta$ for $k \in \mathbb{Z}$. The reproduction level for a bin is located at the midpoint between its thresholds. An input $t \in [k\Delta, (k+1)\Delta)$ is mapped to the value $\Delta(k + 1/2)$. This operation can be expressed compactly using the [floor function](@entry_id:265373):
    $$Q_{\Delta}^{\mathrm{mr}}(t) = \Delta \left( \left\lfloor \frac{t}{\Delta} \right\rfloor + \frac{1}{2} \right)$$

-   A **mid-tread quantizer** is distinguished by having a reproduction level at zero. Its decision thresholds are located at half-integer multiples of the step size, $(k + 1/2)\Delta$. An input $t \in [(k - 1/2)\Delta, (k + 1/2)\Delta)$ is mapped to the value $k\Delta$. This is equivalent to rounding the scaled input to the nearest integer multiple of $\Delta$:
    $$Q_{\Delta}^{\mathrm{mt}}(t) = \Delta \left\lfloor \frac{t}{\Delta} + \frac{1}{2} \right\rfloor = \Delta \cdot \operatorname{round}\left(\frac{t}{\Delta}\right)$$

In practical systems, quantizers have a finite [dynamic range](@entry_id:270472). Inputs that exceed this range are **saturated**, meaning they are mapped to the outermost reproduction level. For instance, a mid-rise quantizer with a symmetric range might map all inputs $s \ge M\Delta$ to a single code and all inputs $s \le -M\Delta$ to another, effectively creating unbounded saturation bins $(-\infty, -M\Delta)$ and $[M\Delta, \infty)$ [@problem_id:3472912].

#### 1-Bit Quantization

The most extreme form of coarse quantization is **1-bit quantization**, where each measurement is reduced to a single bit of information—its sign. The canonical 1-bit quantizer is the sign function, which we define as:
$$
\operatorname{sgn}(t) = \begin{cases} +1  \text{ if } t \ge 0 \\ -1  \text{ if } t  0 \end{cases}
$$
The measurement model becomes $y = \operatorname{sgn}(Ax+w)$, where $y \in \{-1, +1\}^m$. This model is of significant interest due to its low hardware complexity, but it presents unique challenges. Most notably, all magnitude information about the input is discarded. For any scalar $c > 0$ and a noiseless measurement $z=Ax$, we have $\operatorname{sgn}(cz) = \operatorname{sgn}(z)$. This means that the quantized measurements are invariant to any positive scaling of the original signal $x$ [@problem_id:3472950] [@problem_id:3472954]. This inherent **scale ambiguity** is a central theme in [1-bit compressed sensing](@entry_id:746138).

### Consistency Sets and Their Geometry

The act of quantization is a many-to-one mapping; it represents a loss of information. While the exact value of the pre-quantized measurement $z_i$ is lost, the observed output $y_i$ constrains $z_i$ to lie within a specific subset of the real line—the quantization bin corresponding to $y_i$. Let this bin be denoted $\mathcal{I}_i$. For the entire measurement vector, this implies $z = Ax+w$ must lie in the Cartesian product of these bins, $\mathcal{I} = \mathcal{I}_1 \times \mathcal{I}_2 \times \dots \times \mathcal{I}_m$.

In the noiseless case ($w=0$), this gives rise to the **quantization-consistent set** for the signal $x$:
$$
\mathcal{C} = \{ x \in \mathbb{R}^n : Ax \in \mathcal{I} \}
$$
This set contains all signals that could have produced the observed quantized measurements. The geometric properties of $\mathcal{C}$, particularly its convexity, are paramount for designing effective recovery algorithms [@problem_id:3472963].

A foundational result of convex analysis states that the preimage of a [convex set](@entry_id:268368) under a [linear transformation](@entry_id:143080) is convex. Here, $\mathcal{C}$ is the [preimage](@entry_id:150899) of $\mathcal{I}$ under the [linear map](@entry_id:201112) $x \mapsto Ax$. Therefore, the convexity of $\mathcal{C}$ depends entirely on the convexity of the set $\mathcal{I}$. The set $\mathcal{I}$, being a Cartesian product, is convex if and only if each constituent bin $\mathcal{I}_i$ is convex. The only convex subsets of the real line are intervals.

-   For **uniform scalar quantizers** (including those with saturation), each bin $\mathcal{I}_i$ is an interval, possibly unbounded. For example, a non-saturating mid-rise quantizer output implies a constraint of the form $k\Delta \le a_i^\top x  (k+1)\Delta$ [@problem_id:3472912]. Since each $\mathcal{I}_i$ is an interval and thus convex, their product $\mathcal{I}$ is a [convex set](@entry_id:268368) (a hyperrectangle). Consequently, the [consistency set](@entry_id:747726) $\mathcal{C}$ is a **[convex polyhedron](@entry_id:170947)**, defined by the intersection of linear [inequality constraints](@entry_id:176084).

-   For **1-bit quantization** with a threshold at $\tau_i$, the output $y_i \in \{-1,+1\}$ implies a constraint of the form $y_i((a_i^\top x) - \tau_i) \ge 0$. This defines a bin $\mathcal{I}_i$ that is a closed half-line (e.g., $[\tau_i, \infty)$), which is an interval and therefore convex. Thus, the [consistency set](@entry_id:747726) $\mathcal{C}$ is again a [convex polyhedron](@entry_id:170947), formed by the intersection of half-spaces [@problem_id:3472963]. In the special case where all thresholds are zero ($\tau_i=0$), each constraint $y_i(a_i^\top x) \ge 0$ defines a half-space passing through the origin. Their intersection forms a **convex cone**, which geometrically reflects the scale ambiguity of 1-bit sensing: if $x \in \mathcal{C}$, then $cx \in \mathcal{C}$ for any $c>0$ [@problem_id:3472950].

-   In contrast, other forms of quantization, such as **modulo quantization**, where a value is wrapped into a base period, result in bins that are a countable union of disjoint intervals. Such bins are not convex, leading to a non-convex [consistency set](@entry_id:747726) $\mathcal{C}$. Recovery from such measurements is generally an NP-hard problem, highlighting the algorithmic importance of quantizer designs that yield convex consistency sets.

### Signal Recovery from Quantized Data

Given that the quantization-consistent set $\mathcal{C}$ is often a large, multi-dimensional set, an additional principle is required to select a single, meaningful estimate of the signal. In [compressed sensing](@entry_id:150278), this principle is **sparsity**.

#### Consistency-Based Recovery

The most direct approach to recovery is to find the sparsest signal within the [consistency set](@entry_id:747726). Since minimizing the $\ell_0$-quasinorm is computationally intractable, it is replaced by its convex surrogate, the $\ell_1$-norm. This leads to the general [convex optimization](@entry_id:137441) problem:
$$
\min_{x \in \mathbb{R}^n} \|x\|_1 \quad \text{subject to} \quad x \in \mathcal{C}
$$
This formulation seeks a consistent signal that is also sparse. For quantizers that induce a polyhedral [consistency set](@entry_id:747726) $\mathcal{C}$, this is a standard [basis pursuit](@entry_id:200728)-type problem that can be solved efficiently.

#### Special Case: Recovery in 1-Bit Compressed Sensing

As established, 1-bit measurements are blind to the scale of the signal. Consequently, the recovery target is not the signal $x$ itself, but rather its **direction**, represented by the unit-norm vector $x/\|x\|_2$ [@problem_id:3472950]. The recovery problem must be reformulated to address this ambiguity.

One approach is to directly incorporate the scale invariance by optimizing over the unit sphere:
$$
\min_{x \in \mathbb{R}^n} \|x\|_1 \quad \text{subject to} \quad \|x\|_2 = 1 \text{ and } x \in \mathcal{C}
$$
where $\mathcal{C}$ is the conic feasible set. The unit-norm constraint is non-convex, making this a difficult optimization problem.

A more tractable alternative is to modify the consistency constraints to break the scale ambiguity. This is achieved by imposing a **positive margin** $\tau > 0$, requiring that the solution lie robustly on the correct side of each decision boundary. The constraints become $y_i(a_i^\top x) \ge \tau$ for all $i$. The feasible set is now an intersection of affine half-spaces, forming a [convex polyhedron](@entry_id:170947) that no longer contains the origin (unless $\tau=0$) [@problem_id:3472938]. This removes the scale ambiguity, as scaling a [feasible solution](@entry_id:634783) $x$ by a factor $c \neq 1$ will generally violate the constraints. With this modification, one can solve a convex problem to find, for instance, the minimum-energy solution consistent with the margin:
$$
\min_{x \in \mathbb{R}^n} \|x\|_2 \quad \text{subject to} \quad y_i(a_i^\top x) \ge \tau \text{ for all } i
$$
Under certain simplifying assumptions, such as when the vectors $\{y_i a_i\}_{i=1}^n$ form an [orthonormal basis](@entry_id:147779) for $\mathbb{R}^n$, the solution to this problem can be found analytically. The minimum norm is $\|x_{\min}\|_2 = \tau\sqrt{n}$ [@problem_id:3472938], illustrating the direct relationship between the enforced margin and the minimum norm of any consistent signal.

### Robustness: Handling Noise and Model Mismatch

The consistency-based recovery paradigm relies on the assumption that the set $\mathcal{C}$ is non-empty and contains the true signal (or a close approximation). In practice, this assumption can fail.

#### The Empty Feasibility Problem

A combination of measurement noise and mismatch between the true physical quantizer and the model used by the decoder can lead to a set of mutually contradictory constraints. In such cases, the [consistency set](@entry_id:747726) $\mathcal{C}$ is empty, and consistency-based recovery problems become infeasible.

Consider a simple 1-D example with two measurements. Let the true signal be $x^\star=0.2$, sensed by $A = [1, 1]^\top$. Let the true 1-bit quantizer have a threshold at $t_1=0$. Suppose noise $w=[0.4, -0.4]^\top$ is added, yielding unquantized measurements $y = Ax^\star + w = [0.6, -0.2]^\top$. The quantized outputs are $q_1 = \operatorname{sgn}(0.6)=+1$ and $q_2 = \operatorname{sgn}(-0.2)=-1$. Now, suppose the decoder mistakenly assumes a threshold of $\tilde{t}_1=0.5$. It will infer the constraints $a_1^\top x = x \ge 0.5$ (from $q_1=+1$) and $a_2^\top x = x  0$ (from $q_2=-1$). These two constraints are contradictory, and the feasible set is empty [@problem_id:3472943].

#### Loss-Minimization Recovery

To overcome the empty feasibility problem, we can reframe recovery as an [unconstrained optimization](@entry_id:137083) problem. Instead of enforcing hard consistency, we seek a sparse signal $x$ for which $Ax$ is "close" to the measurement bins $\mathcal{I}$. Closeness can be measured by a [loss function](@entry_id:136784) $L(Ax, y)$, leading to the regularized problem:
$$
\min_{x \in \mathbb{R}^n} L(Ax, y) + \lambda \|x\|_1
$$
where $\lambda>0$ is a parameter that balances data fidelity and sparsity. A natural choice for the loss is one that penalizes violations of the bin constraints. For interval bins $[\tilde{t}_{q_i}, \tilde{t}_{q_{i}+1}]$, a suitable penalty for the $i$-th measurement is the distance from $a_i^\top x$ to this interval. This distance can be expressed using hinge-loss terms. This leads to the robust convex objective function [@problem_id:3472943]:
$$
\min_{x \in \mathbb{R}^n} \sum_{i=1}^{m} \left( \max(0, \tilde{t}_{q_{i}} - a_{i}^{\top} x) + \max(0, a_{i}^{\top} x - \tilde{t}_{q_{i}+1}) \right) + \lambda \|x\|_{1}
$$
This formulation is always solvable and provides a meaningful estimate even when no signal is perfectly consistent with the mismatched model.

#### Ambiguity from Coherence and Dithering

Robustness issues can also arise from the sensing matrix itself. If columns of $A$ are highly correlated (i.e., the matrix has high **[mutual coherence](@entry_id:188177)**), distinct [sparse signals](@entry_id:755125) can become indistinguishable after quantization. For example, if two columns $a_1$ and $a_2$ are identical, then the signals $x^{(1)}=\alpha e_1$ and $x^{(2)}=\alpha e_2$ produce identical measurements $y = \alpha a_1$. Under coarse quantization like the sign function, even signals with different amplitudes, such as $\alpha e_1$ and $\beta e_2$, may map to the same quantized output, creating severe ambiguity [@problem_id:3472934].

A powerful technique to mitigate such ambiguities is **[dithering](@entry_id:200248)**. Dithering involves adding a small amount of random noise to the signal *before* quantization. For instance, the measurement could become $y = \operatorname{sgn}(Ax - \tau)$, where $\tau$ is a vector of random [dither](@entry_id:262829) values. This process effectively randomizes the quantizer's decision boundaries. For two distinct signals $x^{(1)}$ and $x^{(2)}$ that were previously indistinguishable, the [dither](@entry_id:262829) makes it highly probable that their quantized outputs will differ for at least one measurement, thereby resolving the ambiguity. For example, if two signals produce measurements that differ by a small amount $\Delta$, adding a uniform [dither](@entry_id:262829) of range $2\Lambda$ can reduce the probability of them having the same quantized output from 1 to $(1 - \Delta/(2\Lambda))^m$, which rapidly approaches zero as $m$ increases [@problem_id:3472934].

### Stability and System Design Considerations

A crucial property of any recovery algorithm is **stability**: the reconstruction error should be gracefully bounded by the level of imperfections in the measurement process, namely [additive noise](@entry_id:194447) and [quantization error](@entry_id:196306).

#### Reconstruction Error Bounds

For [sparse recovery algorithms](@entry_id:189308) based on $\ell_1$-minimization, stability guarantees are typically derived under the assumption that the sensing matrix $A$ satisfies the **Restricted Isometry Property (RIP)**. The RIP ensures that the matrix approximately preserves the Euclidean norm of all sparse vectors. Under this condition, it can be proven that the reconstruction error $\|\hat{x} - x^\star\|_2$ is bounded by a sum of the noise level and the [quantization error](@entry_id:196306). For a [uniform quantizer](@entry_id:192441) with step size $\Delta$, the total error from quantization across $m$ measurements can be shown to scale with $\Delta\sqrt{m}$. This leads to a canonical error bound of the form [@problem_id:3472958]:
$$
\|\hat{x} - x^\star\|_2 \le C_1 \|w\|_2 + C_2 \Delta\sqrt{m}
$$
where $C_1$ and $C_2$ are constants that depend on the RIP constant of the matrix $A$. This result formally establishes that the reconstruction error degrades gracefully as the noise level $\|w\|_2$ or the quantization coarseness $\Delta$ increases.

#### Architectural Trade-offs in Quantizer Design

The total reconstruction error depends on the total quantization noise power. For a fixed bit budget, the physical architecture of the quantization process can significantly impact this noise power. Consider the task of quantizing an inner product $y_i = \sum_{j \in S} a_{ij} x_j$, where $S$ is the support of a $k$-sparse signal, with a total per-measurement budget of $B$ bits.

-   One could quantize each of the $k$ products $a_{ij}x_j$ individually using $B/k$ bits and then sum the results digitally. This is **Per-Coordinate Quantization (PCQ)**.
-   Alternatively, one could sum pairs of products in analog, $(a_{ij_1}x_{j_1} + a_{ij_2}x_{j_2})$, quantize each of the $k/2$ sums using $2B/k$ bits, and then sum these digitally. This is **Pairwise Quantization (PWQ)**.

Under a standard dithered quantization model where the [error variance](@entry_id:636041) is proportional to the square of the step size, it can be shown that PWQ results in a strictly lower total quantization [mean squared error](@entry_id:276542) than PCQ. The reason is that variance of signals adds linearly, while the bit depth required to maintain a given [signal-to-quantization-noise ratio](@entry_id:185071) scales logarithmically with the signal's dynamic range. By summing in analog first, PWQ pools the available bits more effectively, allocating more bits per quantization step ($2B/k$ vs. $B/k$). This leads to a quadratic reduction in quantization error variance for each quantizer, an effect that more than compensates for the increased dynamic range of the summed inputs. The final [quantization error](@entry_id:196306) variance for PWQ is smaller than that for PCQ by a factor of $4^{-B/k}$ [@problem_id:3472908]. This demonstrates that system-level design choices about the order of summation and quantization have a direct and quantifiable impact on the performance of the overall recovery process.