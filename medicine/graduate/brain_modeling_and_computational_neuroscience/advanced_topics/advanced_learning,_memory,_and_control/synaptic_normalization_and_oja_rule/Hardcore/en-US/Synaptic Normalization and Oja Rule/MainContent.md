## Introduction
The brain's remarkable ability to learn and adapt is fundamentally rooted in its capacity to modify the connections between neurons, a process known as [synaptic plasticity](@entry_id:137631). The most famous principle governing this process is Hebbian learning, often summarized as "cells that fire together, wire together." While this provides an intuitive mechanism for strengthening correlated pathways, the simplest mathematical forms of Hebbian learning harbor a critical flaw: they are inherently unstable, leading to a runaway positive feedback loop that causes synaptic weights to grow without bound. This computational and biological implausibility highlights a fundamental knowledge gap: how do neural systems maintain stability while remaining adaptive?

This article explores one of the most elegant and influential solutions to this problem: [synaptic normalization](@entry_id:1132773), as embodied by Erkki Oja's learning rule. Oja's rule introduces a simple, local, and activity-dependent subtractive term that constrains weight growth, transforming an unstable system into a powerful computational device. Over the following chapters, you will gain a comprehensive understanding of this canonical model. The first chapter, "Principles and Mechanisms," will guide you through the mathematical derivation of Oja's rule, revealing how it elegantly performs Principal Component Analysis (PCA). The second chapter, "Applications and Interdisciplinary Connections," will demonstrate its wide-ranging utility, from explaining how networks of neurons learn to represent sensory information to providing a mechanistic account of [brain development](@entry_id:265544) and clinical disorders. Finally, "Hands-On Practices" will offer you the chance to solidify your knowledge by actively engaging with the core concepts.

## Principles and Mechanisms

### The Instability of Classical Hebbian Learning

The principle of Hebbian plasticity, colloquially summarized as "cells that fire together, wire together," provides a compelling local mechanism for synaptic modification based on correlated activity. In its simplest mathematical form for a single linear neuron with output $y = \mathbf{w}^\top \mathbf{x}$ and weight vector $\mathbf{w}$, the change in synaptic weights, $\Delta \mathbf{w}$, is proportional to the product of the presynaptic input, $\mathbf{x}$, and the postsynaptic output, $y$. This gives the classical **Hebbian update rule**:

$$
\Delta \mathbf{w} = \eta y \mathbf{x}
$$

where $\eta$ is a small positive constant known as the **[learning rate](@entry_id:140210)**. Substituting the expression for the output $y$, we have:

$$
\Delta \mathbf{w} = \eta (\mathbf{w}^\top \mathbf{x}) \mathbf{x}
$$

At first glance, this rule elegantly strengthens synapses that contribute to firing the neuron. However, a closer analysis reveals a critical flaw: inherent instability. To see this, let us consider the effect of this update rule on the overall strength of the neuron's synaptic connections, as measured by the squared Euclidean norm of the weight vector, $\|\mathbf{w}\|^2$.

Consider the weight vector at time step $t+1$, given by $\mathbf{w}_{t+1} = \mathbf{w}_t + \Delta \mathbf{w}_t$. The squared norm is:

$$
\|\mathbf{w}_{t+1}\|^2 = (\mathbf{w}_t + \eta y_t \mathbf{x}_t)^\top (\mathbf{w}_t + \eta y_t \mathbf{x}_t) = \|\mathbf{w}_t\|^2 + 2\eta y_t (\mathbf{w}_t^\top \mathbf{x}_t) + \eta^2 y_t^2 \|\mathbf{x}_t\|^2
$$

Since $y_t = \mathbf{w}_t^\top \mathbf{x}_t$, this simplifies to:

$$
\|\mathbf{w}_{t+1}\|^2 - \|\mathbf{w}_t\|^2 = 2\eta ( \mathbf{w}_t^\top \mathbf{x}_t )^2 + \eta^2 ( \mathbf{w}_t^\top \mathbf{x}_t )^2 \|\mathbf{x}_t\|^2
$$

To understand the long-term trend, we examine the expected change over the distribution of input vectors $\mathbf{x}_t$, assuming they are drawn from a stationary distribution with [zero mean](@entry_id:271600) ($\mathbb{E}[\mathbf{x}] = \mathbf{0}$) and a covariance matrix $\mathbf{C} = \mathbb{E}[\mathbf{x}\mathbf{x}^\top]$. The expectation, treating $\mathbf{w}_t$ as fixed for the step, is:

$$
\mathbb{E}[\|\mathbf{w}_{t+1}\|^2 - \|\mathbf{w}_t\|^2] = 2\eta \mathbb{E}[(\mathbf{w}_t^\top \mathbf{x}_t)^2] + \eta^2 \mathbb{E}[(\mathbf{w}_t^\top \mathbf{x}_t)^2 \|\mathbf{x}_t\|^2]
$$

The first term can be rewritten as $\mathbb{E}[(\mathbf{w}_t^\top \mathbf{x}_t)(\mathbf{x}_t^\top \mathbf{w}_t)] = \mathbf{w}_t^\top \mathbb{E}[\mathbf{x}_t\mathbf{x}_t^\top] \mathbf{w}_t = \mathbf{w}_t^\top \mathbf{C} \mathbf{w}_t$. For a small [learning rate](@entry_id:140210) $\eta$, the behavior is dominated by the term of order $\eta$. Thus, to first order, the expected change is:

$$
\mathbb{E}[\|\mathbf{w}_{t+1}\|^2 - \|\mathbf{w}_t\|^2] \approx 2\eta (\mathbf{w}_t^\top \mathbf{C} \mathbf{w}_t)
$$

By definition, a covariance matrix $\mathbf{C}$ is positive semidefinite, meaning the quadratic form $\mathbf{v}^\top \mathbf{C} \mathbf{v} \ge 0$ for any vector $\mathbf{v}$. The term $\mathbf{w}_t^\top \mathbf{C} \mathbf{w}_t$ will be strictly positive as long as the inputs have some variance and the weight vector is not in the [nullspace](@entry_id:171336) of $\mathbf{C}$. Consequently, the expected change in the squared norm is always positive. This implies that the synaptic weights are subject to a positive feedback loop, leading to unbounded growth . This runaway potentiation is biologically implausible and computationally disastrous, as it would lead to saturated synaptic weights and loss of specificity. This fundamental instability necessitates a mechanism for **[synaptic normalization](@entry_id:1132773)** to constrain weight growth and maintain synaptic competition.

### Oja's Rule: Derivation and Interpretation

A particularly elegant and influential solution to the instability of Hebbian learning was proposed by Erkki Oja. **Oja's rule** introduces a subtractive, "forgetting" term that dynamically stabilizes the weight vector. The rule is:

$$
\Delta \mathbf{w} = \eta (y \mathbf{x} - y^2 \mathbf{w})
$$

This rule is remarkable because it can be derived from first principles as a [first-order approximation](@entry_id:147559) of a direct normalization procedure, and its implementation requires only information locally available to the synapse, plus a global signal from the postsynaptic neuron .

To derive Oja's rule, consider a two-step process. First, a standard Hebbian update is applied to get an intermediate weight vector $\mathbf{w}'$:

$$
\mathbf{w}' = \mathbf{w} + \eta y \mathbf{x}
$$

Second, this intermediate vector is explicitly renormalized back to a fixed length, say, unit norm:

$$
\mathbf{w}_{\text{new}} = \frac{\mathbf{w}'}{\|\mathbf{w}'\|} = \frac{\mathbf{w} + \eta y \mathbf{x}}{\|\mathbf{w} + \eta y \mathbf{x}\|}
$$

Assuming the [learning rate](@entry_id:140210) $\eta$ is small, we can approximate the denominator. Starting with the squared norm and assuming $\|\mathbf{w}\|^2=1$:

$$
\|\mathbf{w} + \eta y \mathbf{x}\|^2 = \|\mathbf{w}\|^2 + 2\eta y(\mathbf{w}^\top \mathbf{x}) + \eta^2 y^2 \|\mathbf{x}\|^2 = 1 + 2\eta y^2 + O(\eta^2)
$$

Using the binomial approximation $(1+z)^{-1/2} \approx 1 - z/2$ for small $z$, the reciprocal of the norm is approximately $1 - \eta y^2$. Substituting this back gives:

$$
\mathbf{w}_{\text{new}} \approx (\mathbf{w} + \eta y \mathbf{x})(1 - \eta y^2) = \mathbf{w} + \eta y \mathbf{x} - \eta y^2 \mathbf{w} - \eta^2 y^3 \mathbf{x}
$$

Neglecting terms of order $\eta^2$ and higher, the net change $\Delta \mathbf{w} = \mathbf{w}_{\text{new}} - \mathbf{w}$ is precisely Oja's rule :

$$
\Delta \mathbf{w} \approx \eta (y \mathbf{x} - y^2 \mathbf{w})
$$

The rule consists of two components. The term $\eta y \mathbf{x}$ is the classical Hebbian potentiation term. The new term, $-\eta y^2 \mathbf{w}$, is a [weight decay](@entry_id:635934) term. Crucially, this decay is not constant; it is proportional to the square of the postsynaptic activity, $y^2$. This activity-dependent decay is what stabilizes the norm. When activity is high, the "forgetting" is strong, counteracting the strong Hebbian potentiation. When activity is low, both terms are weak. This dynamic balance drives the norm of the weight vector towards a stable equilibrium.

From a biological perspective, the component-wise update $\Delta w_i = \eta (y x_i - y^2 w_i)$ is considered plausible. The Hebbian part, $y x_i$, depends on the local presynaptic input $x_i$ and the postsynaptic output $y$. The normalization part, $-y^2 w_i$, depends on the local synaptic weight $w_i$ and a signal proportional to the squared postsynaptic output, $y^2$. This latter signal could be broadcast to all synapses of the neuron, for instance via back-propagating action potentials or [calcium signaling](@entry_id:147341), making the rule implementable with only local and neuron-wide variables .

### The Dynamics of Oja's Rule: Principal Component Analysis

What computational function do these dynamics perform? To answer this, we analyze the average behavior of the system in the limit of a small learning rate. This is achieved by transitioning from the stochastic [difference equation](@entry_id:269892) to a deterministic [ordinary differential equation](@entry_id:168621) (ODE) that describes the evolution of the expected weight vector. This is often called the **[mean-field limit](@entry_id:634632)**. The ODE is given by:

$$
\frac{d\mathbf{w}}{dt} = \mathbb{E}[\Delta \mathbf{w}] / \eta = \mathbb{E}[y \mathbf{x} - y^2 \mathbf{w}]
$$

Assuming zero-mean inputs with covariance $\mathbf{C} = \mathbb{E}[\mathbf{x}\mathbf{x}^\top]$, we can evaluate the expectations:
$\mathbb{E}[y \mathbf{x}] = \mathbb{E}[(\mathbf{w}^\top \mathbf{x})\mathbf{x}] = \mathbb{E}[\mathbf{x}\mathbf{x}^\top]\mathbf{w} = \mathbf{C}\mathbf{w}$
$\mathbb{E}[y^2] = \mathbb{E}[(\mathbf{w}^\top \mathbf{x})^2] = \mathbf{w}^\top \mathbb{E}[\mathbf{x}\mathbf{x}^\top] \mathbf{w} = \mathbf{w}^\top \mathbf{C} \mathbf{w}$

Substituting these into the ODE yields the canonical flow for Oja's rule:

$$
\frac{d\mathbf{w}}{dt} = \mathbf{C}\mathbf{w} - (\mathbf{w}^\top \mathbf{C} \mathbf{w})\mathbf{w}
$$

The fixed points of this system, where $\frac{d\mathbf{w}}{dt} = \mathbf{0}$, satisfy $\mathbf{C}\mathbf{w} = (\mathbf{w}^\top \mathbf{C} \mathbf{w})\mathbf{w}$. This equation reveals that any non-zero fixed point must be an eigenvector of the covariance matrix $\mathbf{C}$. Furthermore, if $\mathbf{w}^*$ is an eigenvector with eigenvalue $\lambda$, i.e., $\mathbf{C}\mathbf{w}^* = \lambda \mathbf{w}^*$, the condition becomes $\lambda \mathbf{w}^* = \lambda \|\mathbf{w}^*\|^2 \mathbf{w}^*$, which implies that the squared norm must be $\|\mathbf{w}^*\|^2 = 1$. Thus, the fixed points are the unit-norm eigenvectors of the input covariance matrix. Later stability analysis will show that the system converges to the eigenvector associated with the largest eigenvalue.

This means that Oja's rule causes the neuron's weight vector to evolve until it aligns with the direction of maximum variance in the input data. This process is known as **Principal Component Analysis (PCA)**. The neuron effectively learns to detect the most prominent feature in its input stream.

It is critical to note that the dynamics are governed by the input's **second-moment matrix**, $\mathbf{S} = \mathbb{E}[\mathbf{x}\mathbf{x}^\top]$. The relation between the second-moment matrix and the covariance matrix $\mathbf{C} = \mathbb{E}[(\mathbf{x}-\boldsymbol{\mu})(\mathbf{x}-\boldsymbol{\mu})^\top]$ is $\mathbf{S} = \mathbf{C} + \boldsymbol{\mu}\boldsymbol{\mu}^\top$, where $\boldsymbol{\mu}=\mathbb{E}[\mathbf{x}]$ is the input mean. PCA is defined as finding the eigenvectors of the covariance matrix $\mathbf{C}$. Therefore, Oja's rule performs true PCA only when the inputs are centered, i.e., have [zero mean](@entry_id:271600) ($\boldsymbol{\mu}=\mathbf{0}$), in which case $\mathbf{S}=\mathbf{C}$. If the inputs have a non-[zero mean](@entry_id:271600), the weight vector will converge to the [principal eigenvector](@entry_id:264358) of $\mathbf{S}$, which is generally different from that of $\mathbf{C}$ . For instance, if the input consists of isotropic noise around a strong [mean vector](@entry_id:266544) ($\mathbf{C} = \sigma^2 \mathbf{I}$, $\boldsymbol{\mu} \neq \mathbf{0}$), the [principal eigenvector](@entry_id:264358) of $\mathbf{S} = \sigma^2 \mathbf{I} + \boldsymbol{\mu}\boldsymbol{\mu}^\top$ is simply $\boldsymbol{\mu}$. In this case, the neuron learns to represent the average input, not the direction of maximum variance around that average.

### Theoretical Foundations of Oja's Rule

The ability of Oja's rule to perform PCA can be understood from the perspective of [constrained optimization](@entry_id:145264). The problem of finding the principal component of a dataset can be framed as maximizing the output variance, $\mathbb{E}[y^2] = \mathbf{w}^\top \mathbf{C} \mathbf{w}$, subject to the constraint that the weight vector has a fixed norm, e.g., $\|\mathbf{w}\|^2 = 1$.

This constrained optimization problem can be solved using a **Lagrange multiplier** $\lambda$. We construct the Lagrangian:
$$
\mathcal{L}(\mathbf{w}, \lambda) = \mathbf{w}^\top \mathbf{C} \mathbf{w} - \lambda(\|\mathbf{w}\|^2 - 1)
$$
Setting the gradient with respect to $\mathbf{w}$ to zero gives the stationary condition $\nabla_{\mathbf{w}}\mathcal{L} = 2\mathbf{C}\mathbf{w} - 2\lambda\mathbf{w} = \mathbf{0}$, which simplifies to the eigenvector equation $\mathbf{C}\mathbf{w} = \lambda\mathbf{w}$. The solution that maximizes the objective is the eigenvector corresponding to the largest eigenvalue, $\lambda_{\max}$.

Oja's rule can be interpreted as a stochastic [online algorithm](@entry_id:264159) for solving this problem  . The Hebbian term, $\eta y \mathbf{x}$, is a stochastic gradient ascent step on the objective $\mathbf{w}^\top \mathbf{C} \mathbf{w}$. The normalization term, $-\eta y^2 \mathbf{w}$, acts as an estimate of the constraint term $-\eta\lambda\mathbf{w}$. At equilibrium, the optimal Lagrange multiplier $\lambda$ is equal to the output variance $\mathbf{w}^\top \mathbf{C} \mathbf{w} = \mathbb{E}[y^2]$. Oja's rule ingeniously uses the instantaneous sample $y^2$ as an online, adaptive estimate of this multiplier. This adaptive nature distinguishes it from simpler rules like Hebbian learning with fixed [weight decay](@entry_id:635934), $\Delta \mathbf{w} = \eta(y\mathbf{x} - \lambda_0\mathbf{w})$, where a constant $\lambda_0$ must be precisely tuned to the input statistics to achieve stability, and even then, it fails to robustly stabilize the norm .

Another powerful viewpoint arises by considering the dynamics on the unit sphere, where $\|\mathbf{w}\|=1$. Here, the objective function $\mathbf{w}^\top \mathbf{C} \mathbf{w}$ is known as the **Rayleigh quotient**, $R_{\mathbf{C}}(\mathbf{w})$. The gradient of the Rayleigh quotient is $\nabla R_{\mathbf{C}}(\mathbf{w}) = 2(\mathbf{C}\mathbf{w} - (\mathbf{w}^\top \mathbf{C} \mathbf{w})\mathbf{w})$. Comparing this to the Oja ODE, we see that on the unit sphere, the dynamics are precisely gradient ascent on the Rayleigh quotient: $\frac{d\mathbf{w}}{dt} = \frac{1}{2}\nabla R_{\mathbf{C}}(\mathbf{w})$. This confirms that the dynamics drive the weight vector towards the maximum of the Rayleigh quotient, which is attained when $\mathbf{w}$ is the [principal eigenvector](@entry_id:264358) of $\mathbf{C}$ .

### Convergence and Stability Analysis

#### Local Stability of the Mean-Field Dynamics

To formally prove that Oja's rule converges to the principal eigenvector, we must analyze the stability of the fixed points of the ODE. We do this by linearizing the dynamics around a fixed point $\mathbf{w}^* = \mathbf{u}_k$, a unit-norm eigenvector of $\mathbf{C}$. A perturbation $\delta\mathbf{w}$ away from this fixed point will evolve according to $\frac{d}{dt}\delta\mathbf{w} \approx J(\mathbf{u}_k) \delta\mathbf{w}$, where $J$ is the Jacobian matrix of the vector field evaluated at the fixed point.

The Jacobian of the Oja flow is given by:
$$
J(\mathbf{w}) = \mathbf{C} - (\mathbf{w}^\top \mathbf{C} \mathbf{w})\mathbf{I} - 2\mathbf{w}(\mathbf{C}\mathbf{w})^\top
$$
(Note: we absorb $\eta$ into the timescale). Evaluating at the fixed point $\mathbf{w}^* = \mathbf{u}_1$ (the [principal eigenvector](@entry_id:264358) with eigenvalue $\lambda_1$), we get:
$$
J(\mathbf{u}_1) = \mathbf{C} - \lambda_1 \mathbf{I} - 2\lambda_1(\mathbf{u}_1\mathbf{u}_1^\top)
$$
To determine stability, we examine the eigenvalues of this Jacobian, which are the **local Lyapunov exponents**. We apply the Jacobian to the other eigenvectors $\mathbf{u}_j$ (where $j > 1$):
$$
J(\mathbf{u}_1)\mathbf{u}_j = (\mathbf{C} - \lambda_1 \mathbf{I} - 2\lambda_1(\mathbf{u}_1\mathbf{u}_1^\top))\mathbf{u}_j = \lambda_j \mathbf{u}_j - \lambda_1 \mathbf{u}_j - 2\lambda_1\mathbf{u}_1(\mathbf{u}_1^\top\mathbf{u}_j)
$$
Since the eigenvectors are orthonormal, $\mathbf{u}_1^\top\mathbf{u}_j = 0$ for $j \neq 1$. The equation simplifies to:
$$
J(\mathbf{u}_1)\mathbf{u}_j = (\lambda_j - \lambda_1)\mathbf{u}_j
$$
The Lyapunov exponent for a perturbation in the direction of $\mathbf{u}_j$ is thus $\lambda_j - \lambda_1$. Since we assume a unique largest eigenvalue, $\lambda_1 > \lambda_j$ for all $j>1$, these exponents are all negative. This means any perturbation orthogonal to the [principal eigenvector](@entry_id:264358) will decay, proving that $\mathbf{u}_1$ is a stable fixed point of the dynamics . (The exponent for a perturbation parallel to $\mathbf{u}_1$ is zero, reflecting that the norm is fixed on the attractive unit sphere).

#### Convergence of the Stochastic Algorithm

The ODE analysis describes the average behavior. For the actual stochastic algorithm to converge, the noise introduced by individual samples must diminish appropriately. The theory of **[stochastic approximation](@entry_id:270652)** provides the necessary conditions for **[almost sure convergence](@entry_id:265812)**, meaning the algorithm converges with probability 1. For a learning rate sequence $\{\eta_t\}$, the standard conditions are :

1.  $\sum_{t=1}^{\infty} \eta_t = \infty$
2.  $\sum_{t=1}^{\infty} \eta_t^2  \infty$

The first condition ensures that the learning process has infinite "energy" to escape local minima and reach the true attractor. The second condition ensures that the accumulated variance of the updates is finite, causing the noise to eventually die out and allowing the iterates to settle at the fixed point. A canonical choice for the learning rate that satisfies these conditions is $\eta_t = 1/t$. In contrast, a small constant [learning rate](@entry_id:140210) $\eta$ violates the second condition, leading to persistent fluctuations around the fixed point rather than convergence to it.

### Advanced Topics and Extensions

#### Symmetry Breaking in Degenerate Subspaces

The analysis so far assumed a unique largest eigenvalue, $\lambda_1 > \lambda_2$. What happens if the input statistics are degenerate, for example, if $\lambda_1 = \lambda_2$? In this case, there is a two-dimensional principal subspace, and the ODE analysis suggests that any direction within this subspace is a [stable fixed point](@entry_id:272562). The deterministic dynamics provide no basis for selecting one direction over another.

However, the stochastic nature of the learning rule becomes crucial. In the perfectly degenerate case, the weight vector will execute a random walk, or diffusion, within this subspace. If a small anisotropy is introduced, such that the covariance is $\mathbf{S} = \lambda \mathbf{I} + \epsilon \mathbf{\Delta}$ with $|\epsilon| \ll \lambda$, a very weak deterministic drift emerges that pushes the weight vector towards the "true" principal eigenvector. The angular dynamics of the weight vector can be modeled by a [stochastic differential equation](@entry_id:140379) (SDE) that includes both this weak drift and a diffusion term arising from the [stochasticity](@entry_id:202258) of the input samples. For Gaussian inputs, the resulting stationary probability distribution for the weight vector's angle $\theta$ takes the form of a von Mises distribution, $p(\theta) \propto \exp\{\kappa \cos(2\theta)\}$, where the concentration $\kappa$ depends on the ratio of the anisotropy $\epsilon$ to the learning rate $\eta$ and noise level. This demonstrates a beautiful principle: the final selected direction is a "noise-broadened" preference for the higher-variance axis, emerging from the competition between a weak deterministic signal and stochastic fluctuations .

#### Generalized Oja's Rule for Nonlinear Neurons

The principles of Oja's rule can be extended to neurons with nonlinear activation functions, $y = \phi(z)$, where $z=\mathbf{w}^\top \mathbf{x}$. A natural generalization of the mean-field dynamics is:
$$
\frac{d\mathbf{w}}{dt} = \mathbb{E}[y \mathbf{x}] - \mathbb{E}[y^2]\mathbf{w}
$$
For a zero-mean Gaussian input, a powerful result known as **Stein's Lemma** can be used to relate the two expectation terms. The lemma allows us to write $\mathbb{E}[y \mathbf{x}] = \mathbb{E}[\phi(\mathbf{w}^\top \mathbf{x}) \mathbf{x}] = \mathbf{C}\mathbf{w} \mathbb{E}[\phi'(\mathbf{w}^\top \mathbf{x})]$. Using the identity $\phi' = 1 - \tanh^2$ for the hyperbolic tangent function $\phi = \tanh$, one can simplify the dynamics to:
$$
\frac{d\mathbf{w}}{dt} = \mathbf{C}\mathbf{w} - \mathbb{E}[y^2](\mathbf{C}\mathbf{w} + \mathbf{w})
$$
In the **small-signal regime**, where the neuron's input drive $z = \mathbf{w}^\top \mathbf{x}$ is small, we can use a Taylor [series approximation](@entry_id:160794) for $\mathbb{E}[y^2] = \mathbb{E}[\tanh^2(z)]$. This yields $\mathbb{E}[y^2] \approx ( \mathbf{w}^\top\mathbf{C}\mathbf{w}) - 2(\mathbf{w}^\top\mathbf{C}\mathbf{w})^2$. Substituting this into the dynamics shows how the nonlinearity introduces higher-order correction terms to the basic Oja flow :
$$
\frac{d\mathbf{w}}{dt} \approx [\mathbf{C}\mathbf{w} - (\mathbf{w}^\top \mathbf{C} \mathbf{w})\mathbf{w}] - (\mathbf{w}^\top \mathbf{C} \mathbf{w})\mathbf{C}\mathbf{w} + \dots
$$
The term in brackets is the original Oja rule, and the subsequent terms represent deviations due to the [compressive nonlinearity](@entry_id:1122764) of the activation function. This highlights how the core principles of Hebbian learning and [synaptic normalization](@entry_id:1132773) can operate and be analyzed in more complex and biologically realistic models.