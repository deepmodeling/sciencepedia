## Introduction
Solving inverse problems—the process of inferring underlying causes from indirect observations—is a fundamental challenge across science and engineering. Classical approaches often rely on iterative optimization algorithms to solve a regularized [objective function](@entry_id:267263), balancing data fidelity with prior knowledge about the solution. While powerful, these methods typically depend on handcrafted parameters and can suffer from slow convergence. In parallel, [deep learning](@entry_id:142022) has emerged as a revolutionary tool for [data-driven modeling](@entry_id:184110), yet its "black-box" nature can make it difficult to interpret or integrate with well-understood physical principles.

This article explores a powerful hybrid paradigm, known as [learned iterative schemes](@entry_id:751215) or [unrolled optimization](@entry_id:756343), that bridges this gap. It addresses the limitations of classical methods by retaining their interpretable, model-based structure while leveraging the learning capabilities of [deep neural networks](@entry_id:636170) to optimize their performance. By viewing the iterations of an [optimization algorithm](@entry_id:142787) as the layers of a network, we can train its parameters end-to-end, creating highly efficient and accurate solvers tailored to specific problem domains.

Across three chapters, this article provides a comprehensive overview of this exciting field. The first chapter, **Principles and Mechanisms**, deconstructs the core concepts, explaining how to transform a classical algorithm into a learnable network and the rationale for doing so. The second chapter, **Applications and Interdisciplinary Connections**, showcases the framework's versatility, from enhancing classical methods to enabling [physics-informed learning](@entry_id:136796) in fields like geophysics. Finally, the **Hands-On Practices** chapter provides concrete exercises to build practical skills in analyzing, implementing, and managing the computational trade-offs of these advanced models.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms that underpin [learned iterative schemes](@entry_id:751215). We begin by revisiting the classical optimization framework for solving [inverse problems](@entry_id:143129), establishing the need for iterative algorithms. We then deconstruct one such algorithm, the [proximal gradient method](@entry_id:174560), to understand its components. This forms the basis for the central concept of "unrolling," where we transform the iterative algorithm into a deep neural [network architecture](@entry_id:268981). We will explore the motivation for learning the parameters of this network, the methods for training it, and several advanced topics that address both theoretical and practical challenges in this rapidly evolving field.

### From Variational Problems to Iterative Solutions

Many [inverse problems](@entry_id:143129) in science and engineering are concerned with recovering an unknown state $x \in \mathbb{R}^{n}$ from a set of indirect observations $y \in \mathbb{R}^{m}$. A common model for this relationship is the linear system:

$y = A x + e$

where $A \in \mathbb{R}^{m \times n}$ is the **forward operator** that maps the state space to the observation space, and $e \in \mathbb{R}^{m}$ represents [measurement noise](@entry_id:275238) or model error. A direct inversion to find $x$ is often problematic because inverse problems are frequently **ill-posed**. An [ill-posed problem](@entry_id:148238), in the sense of Hadamard, fails to satisfy one or more of three crucial conditions: existence, uniqueness, and stability of the solution. The stability condition is particularly fragile; even if a unique solution exists, it may be exquisitely sensitive to small perturbations in the data $y$.

For linear problems, this instability is directly related to the singular value spectrum of the operator $A$. If $A$ has singular values that are very close to zero, its pseudoinverse $A^{\dagger}$ will have very large singular values. Consequently, any noise $e$ in the data can be dramatically amplified in the solution, rendering a naive [least-squares](@entry_id:173916) estimate useless .

To counteract [ill-posedness](@entry_id:635673), we employ **regularization**, which introduces prior knowledge about the expected properties of the solution $x$. Instead of solving the ill-posed problem directly, we solve a well-posed optimization problem. A widely used approach is the **[variational formulation](@entry_id:166033)**, where we seek to minimize an [objective function](@entry_id:267263) that balances two competing goals:

$J(x) = \underbrace{\frac{1}{2}\|A x - y\|_{2}^{2}}_{\text{Data Fidelity}} + \underbrace{\lambda R(x)}_{\text{Regularization}}$

The first term, $\frac{1}{2}\|A x - y\|_{2}^{2}$, is the **data fidelity** (or data-fit) term. It enforces consistency between the estimated state projected into the data space, $Ax$, and the actual observations, $y$. The second term, $R(x)$, is the **regularizer** or **prior**. It encodes our assumptions about the solution, such as smoothness ($R(x) = \|\nabla x\|_2^2$) or sparsity ($R(x) = \|x\|_1$). The **[regularization parameter](@entry_id:162917)**, $\lambda > 0$, controls the trade-off between these two terms .

For this optimization problem to be well-behaved, we desire a unique minimizer. This is guaranteed if the objective function $J(x)$ is **strictly convex**. The data fidelity term is convex, and it becomes strictly convex if the matrix $A^{\top}A$ is [positive definite](@entry_id:149459), which occurs when $A$ has full column rank. In this case, $J(x)$ is strictly convex for any convex regularizer $R(x)$ and $\lambda \ge 0$. However, even if $A$ is rank-deficient (meaning $A^{\top}A$ is only positive semidefinite), the entire objective $J(x)$ can be made strictly convex if the regularizer $R(x)$ is itself strictly convex and $\lambda > 0$. A canonical example is standard **Tikhonov regularization**, where $R(x) = \frac{1}{2}\|x\|_2^2$. The Hessian of $J(x)$ is then $A^{\top}A + \lambda I$, which is positive definite for any $A$ and any $\lambda > 0$, ensuring a unique, stable solution .

### The Proximal Gradient Method: A Foundational Algorithm

Solving the variational problem requires a suitable [optimization algorithm](@entry_id:142787), especially when the regularizer $R(x)$ is non-differentiable, as is the case for the sparsity-promoting $\ell_1$-norm. The **[proximal gradient method](@entry_id:174560)**, also known as **Forward-Backward Splitting (FBS)** or the **Iterative Shrinkage-Thresholding Algorithm (ISTA)**, is perfectly suited for such composite objective functions.

Let's consider the general composite problem of minimizing $F(x) = g(x) + h(x)$, where $g(x)$ is a smooth (differentiable) [convex function](@entry_id:143191) with an $L$-Lipschitz continuous gradient, and $h(x)$ is a convex but possibly [non-differentiable function](@entry_id:637544). In our running example, $g(x) = \frac{1}{2}\|A x - y\|_{2}^{2}$ and $h(x) = \lambda R(x)$.

The [proximal gradient method](@entry_id:174560) generates a sequence of estimates $\{x^k\}$ via the iteration:

$x^{k+1} = \mathrm{prox}_{\gamma h}\left(x^k - \gamma \nabla g(x^k)\right)$

Here, $\gamma > 0$ is a **step size**. The iteration consists of two main steps:
1.  A **Forward Step**: This is an explicit gradient descent step on the smooth part of the objective: $z^k = x^k - \gamma \nabla g(x^k)$.
2.  A **Backward Step**: This is an implicit step that involves the **proximal operator** of the non-smooth term $h$, applied to the result of the forward step: $x^{k+1} = \mathrm{prox}_{\gamma h}(z^k)$.

The proximal operator of a function $\phi$ is defined as:

$\mathrm{prox}_{\phi}(v) = \arg\min_{z \in \mathbb{R}^n} \left\{ \phi(z) + \frac{1}{2}\|z-v\|^2 \right\}$

It finds a point $z$ that is a trade-off between being close to the input $v$ and having a small value of $\phi(z)$. When $\phi(z) = \theta \|z\|_1$, the [proximal operator](@entry_id:169061) is the well-known **[soft-thresholding operator](@entry_id:755010)**, $S_{\theta}$. This elegant decomposition allows us to handle the smooth and non-smooth parts of the objective separately .

Convergence of this iterative scheme is not guaranteed for any choice of step size $\gamma$. A key result from convex analysis provides the necessary condition. The **Baillon-Haddad theorem** states that if a [convex function](@entry_id:143191) $g(x)$ has an $L$-Lipschitz gradient, then its [gradient operator](@entry_id:275922) $\nabla g$ is **$\frac{1}{L}$-cocoercive**. This property is crucial for analyzing the convergence of [gradient-based methods](@entry_id:749986). Using this fact, one can show that the forward-backward iteration converges to a minimizer of $g(x)+h(x)$ provided the step size $\gamma$ is chosen in the range $0  \gamma  2/L$. A common, slightly more restrictive choice is $0  \gamma \le 1/L$  . We can also introduce a **[relaxation parameter](@entry_id:139937)** $\theta_k \in (0, 2)$ to get a more general update, which converges under corresponding constraints on $\gamma_k$ and $\theta_k$ .

### Unrolling Optimization: The Birth of Learned Iterative Schemes

Classical iterative algorithms like ISTA use a fixed update rule with handcrafted parameters (e.g., $\gamma$ and $\lambda$). The core idea of **unrolling** is to view a fixed number of iterations, say $K$, of such an algorithm as the layers of a feed-forward neural network. Instead of using pre-defined parameters, we make them learnable and potentially different at each layer (iteration).

Let's take the ISTA update for minimizing $\frac{1}{2}\|A x - y\|_{2}^{2} + \lambda \|x\|_1$:

$x^{k+1} = S_{\lambda\gamma}\left(x^k - \gamma A^{\top}(A x^k - y)\right)$

By unrolling this for $K$ steps, and replacing the fixed parameters with layer-dependent learnable ones, we arrive at a basic learned iterative scheme:

$x^{k+1} = S_{\theta_k}\left(x^k - \gamma_k A^{\top}(A x^k - y)\right) \quad \text{for } k=0, \dots, K-1$

Here, the thresholds $\theta_k$ and step sizes $\gamma_k$ are parameters to be learned from data. A more powerful generalization, known as the **Learned ISTA (LISTA)**, replaces the scalar parameters and fixed matrices with learnable linear operators (matrices) :

$z_k = W_k x_{k-1} + U_k y$
$x_k = S_{\theta_k}(z_k)$

Here, $W_k$ can be seen as learning a combination of the identity matrix and the Gram matrix term $-A^{\top}A$ from the original ISTA, while $U_k$ learns a mapping from the measurements $y$. This architecture provides significantly more [expressive power](@entry_id:149863) than simply learning scalar parameters.

### The Rationale for Learning: Accelerating Convergence and Reducing Bias

Why should we expect learned parameters to outperform classical, fixed ones? There are two primary motivations: accelerating convergence and mitigating algorithmic bias.

**Convergence Acceleration:** A well-chosen sequence of parameters can guide the iterates to the solution much faster than a fixed-parameter scheme. In an idealized scenario, learning can achieve remarkable acceleration. For instance, consider a simplified one-layer LISTA network with specific parameter choices for a noiseless, [sparse signal recovery](@entry_id:755127) problem. Under ideal assumptions about the forward operator $A$, it is possible to derive parameters that allow for exact recovery of the sparse signal in a single step . While this relies on strong assumptions, it demonstrates the principle that learned parameters can effectively learn to invert the system operator, bypassing the slow, incremental progress of classical methods.

**Bias-Variance Trade-off:** The [soft-thresholding operator](@entry_id:755010), which is central to ISTA, introduces a systematic bias. For a true signal component $x_i^\star > \theta$, its estimate will be approximately $x_i^\star - \theta$, consistently underestimating the magnitude. A fixed threshold $\theta$ in classical ISTA leads to this bias even in the final converged solution. A learned iterative scheme with a finite number of layers, $K$, can manage this trade-off more effectively. By learning a schedule of decreasing thresholds $\theta_k$, the network can use larger thresholds in early layers to aggressively promote sparsity and ensure stability (strong contraction), and then use smaller thresholds in later layers to fine-tune the non-zero coefficients and reduce the final shrinkage bias. This dynamic adjustment is inaccessible to a fixed-parameter ISTA within the same computational budget of $K$ iterations .

While learning offers flexibility, the stability of the resulting network remains a concern. The classical convergence conditions provide a valuable guide. For example, the operator for each layer can be designed to be **nonexpansive** (Lipschitz constant of 1), which prevents the amplification of errors through the network. This can be achieved by constraining the learned step sizes $\gamma_k$ to respect the classical stability bounds, such as $\gamma_k \le 1/\|A\|_2^2$. The composition of nonexpansive layers is also nonexpansive, guaranteeing overall stability .

### Training Unrolled Networks: Backpropagation Through Iterations

To learn the parameters $(\{W_k, U_k, \theta_k\}_{k=1}^K)$, we employ a [supervised learning](@entry_id:161081) approach. Given a dataset of observation-ground truth pairs $\{(y^{(j)}, x^{\star(j)})\}$, we aim to minimize a loss function that measures the discrepancy between the network's final output $x_K$ and the ground truth $x^\star$. A common choice is the squared Euclidean distance:

$\mathcal{L} = \frac{1}{2} \|x_K - x^\star\|_2^2$

The parameters are then updated using [gradient-based optimization](@entry_id:169228) (e.g., SGD or Adam). This requires computing the gradient of the loss $\mathcal{L}$ with respect to every learnable parameter in the network. Since the network is a deep, sequential computation graph, this is achieved via the **backpropagation** algorithm, which is an efficient implementation of the [chain rule](@entry_id:147422) from [multivariable calculus](@entry_id:147547) .

The process involves two passes:
1.  **Forward Pass**: For a given input $y$ and initial state $x_0=0$, compute and store the intermediate variables $z_k$ and $x_k$ for all layers $k=1, \dots, K$.
2.  **Backward Pass**: The algorithm proceeds backward from the last layer to the first, computing "sensitivities" or error signals. Let's define the sensitivity at layer $k$ as the gradient of the loss with respect to the pre-activation variable $z_k$, i.e., $\delta_k \equiv \frac{\partial \mathcal{L}}{\partial z_k}$.

The [backpropagation](@entry_id:142012) starts by computing the gradient at the output: $\frac{\partial \mathcal{L}}{\partial x_K} = x_K - x^\star$. The sensitivity at the last layer is then:

$\delta_K = \frac{\partial \mathcal{L}}{\partial x_K} \odot \mathcal{S}'_{\theta_K}(z_K)$

where $\odot$ is the element-wise (Hadamard) product and $\mathcal{S}'_{\theta_K}(z_K)$ is the derivative of the [soft-thresholding](@entry_id:635249) function, which is simply an indicator vector whose elements are 1 if the corresponding component of $z_K$ is above the threshold in magnitude, and 0 otherwise (assuming [differentiability](@entry_id:140863)).

The error is then propagated backward through the layers. The sensitivity at layer $k-1$ is derived from the sensitivity at layer $k$:

$\delta_{k-1} = (W_k^\top \delta_k) \odot \mathcal{S}'_{\theta_{k-1}}(z_{k-1})$

Once the sensitivities $\delta_k$ are known for all layers, the gradients with respect to the parameters at each layer can be computed directly. For example, for a LISTA-style network :

$\frac{\partial \mathcal{L}}{\partial W_k} = \delta_k (x_{k-1})^\top$
$\frac{\partial \mathcal{L}}{\partial U_k} = \delta_k y^\top$
$\frac{\partial \mathcal{L}}{\partial \theta_k} = - \delta_k^\top \mathrm{sign}(z_k)$

These gradients are then accumulated over a batch of training data and used to update the network parameters.

### Advanced Topics in Learned Iterative Schemes

The basic framework of unrolling can be extended and refined in several important ways, addressing issues of [parameterization](@entry_id:265163), prior modeling, acceleration, and training efficiency.

#### Parameter Identifiability and Regularization

A subtle but critical issue in training models like LISTA is **parameter non-identifiability**. It is possible for different sets of parameters to produce the exact same network function. For instance, in a LISTA-like model involving an analysis transform $W$, one can scale the $i$-th row of $W$ by a non-zero scalar $p_i$ and simultaneously scale the corresponding threshold $\theta_i$ by $|p_i|$, and the overall layer mapping will remain unchanged. This ambiguity arises from the interaction between the linear transform $W$ and the element-wise, sign-symmetric nature of the [soft-thresholding operator](@entry_id:755010). This means that during training, the optimization can drift along a subspace of equivalent solutions, potentially leading to instability and making the learned parameters uninterpretable.

To resolve this, we must introduce constraints or regularization that break the symmetry. A principled approach is to fix the scale and sign of each row of the matrix $W$. For example, one can constrain each row vector of $W$ to have a unit Euclidean norm and enforce a sign convention (e.g., the first non-zero entry must be positive). This selects a unique, canonical representative from each [equivalence class](@entry_id:140585) of parameters, making the learning problem well-posed and rendering the learned thresholds $\theta$ directly interpretable as shrinkage levels in a normalized feature space .

#### Plug-and-Play Priors: Integrating Advanced Denoisers

The proximal operator in ISTA can be interpreted as a [denoising](@entry_id:165626) step. It takes a noisy-looking vector $z^k = x^k - \gamma \nabla g(x^k)$ and returns a "cleaner" version $x^{k+1}$ that conforms to the prior $h(x)$. The **Plug-and-Play (PnP)** framework generalizes this idea by replacing the specific proximal operator with a powerful, general-purpose [image denoising](@entry_id:750522) algorithm, often a pre-trained neural network denoiser $D(\cdot)$. The PnP-ISTA iteration becomes:

$x^{k+1} = D\left(x^{k} - \alpha A^{\top}(A x^{k} - y)\right)$

This approach allows the integration of state-of-the-art denoisers that can capture far more complex and realistic priors than simple analytical forms like the $\ell_1$-norm. A key theoretical question is under what conditions the resulting PnP algorithm converges. If the denoiser $D$ can be shown to be a [proximal operator](@entry_id:169061) of some (possibly implicit) convex regularizer $R(x)$, then the PnP iteration is equivalent to a [proximal gradient method](@entry_id:174560) for minimizing $\frac{1}{2}\|Ax-y\|^2 + R(x)$, and its convergence is guaranteed under standard conditions. From [monotone operator](@entry_id:635253) theory, a sufficient condition is that the operator $D$ is **firmly nonexpansive**. More rigorously, $D$ is a proximal map of a convex function if and only if it is firmly nonexpansive and the associated operator $D^{-1} - I$ is maximal cyclically monotone . Even if these conditions are not strictly met, PnP methods often perform remarkably well in practice.

#### Unrolling Accelerated Methods

Classical optimization offers accelerated versions of the [proximal gradient method](@entry_id:174560), such as **FISTA (Fast ISTA)**, which incorporate a "momentum" or "inertial" term. These algorithms often exhibit a much faster convergence rate than their non-accelerated counterparts. We can also unroll these accelerated schemes. A learned inertial forward-backward layer takes the form:

$x_{k+1} = \mathrm{prox}_{\tau h}\left(x_k - \tau \nabla g(x_k) + \beta (x_k - x_{k-1})\right)$

Here, both the step size $\tau$ and the momentum parameter $\beta$ can be learned on a per-layer basis. The analysis of such schemes is more complex. One powerful tool is the use of **Lyapunov functions**. By constructing an energy function $\Phi_k$ that depends on the state and the [objective function](@entry_id:267263) value, one can derive conditions on the learned parameters $(\tau, \beta)$ that guarantee this energy function decreases at every layer ($\Phi_{k+1} \le \Phi_k$), thereby ensuring a stable trajectory towards a solution. For the inertial step above, such an analysis reveals a trade-off between the step size and the maximum allowable momentum, for example, a condition of the form $\beta \le 1 - \frac{L\tau}{2}$ .

#### Implicit Differentiation for Training to Convergence

Unrolling for a fixed number of steps $K$ is a powerful but memory-intensive strategy, as the memory cost scales linearly with the depth $K$. An alternative paradigm, particularly for models where the layer is shared (i.e., parameters are fixed across iterations), is to train the algorithm to convergence. This gives rise to **deep equilibrium (DEQ) models**. The output is no longer $x_K$, but the fixed point $x^\star$ that satisfies $x^\star = \Phi_\theta(x^\star; y)$.

Computing gradients for such a model seems daunting, as it implies backpropagating through an infinite number of steps. However, the **Implicit Function Theorem** provides an elegant solution. At the fixed point, we can differentiate the [equilibrium equation](@entry_id:749057) $x^\star - \Phi_\theta(x^\star; y) = 0$ to find the Jacobian of the fixed point with respect to the parameters, $\frac{\partial x^\star}{\partial \theta}$, without ever backpropagating through the forward iterations. This involves solving a single linear system.

This leads to two distinct training strategies:
- **Strategy U (Unrolling)**: Compute cost $C_U \approx K(c_f + c_b)$, Memory cost $M_U = \Theta(K m_x)$.
- **Strategy I (Implicit Differentiation)**: Compute cost $C_I \approx K c_f + S c_{imp}$, Memory cost $M_I = \Theta(m_x)$.

Here, $K$ is the number of forward iterations, $c_f$ and $c_b$ are the forward and backward costs per layer, $S$ is the number of iterations for the linear system solver in the [implicit method](@entry_id:138537), and $c_{imp}$ is the cost per solver iteration.

The trade-off is clear: [implicit differentiation](@entry_id:137929) has a constant memory footprint, independent of the number of iterations required for convergence, making it suitable for very deep effective models. Unrolled backpropagation has a memory cost that grows with depth. In terms of computation, [implicit differentiation](@entry_id:137929) becomes cheaper than unrolling when the cost of [backpropagation](@entry_id:142012) through the layers ($K c_b$) exceeds the cost of solving the single linear system at the end ($S c_{imp}$). This occurs when the number of layers $K$ is sufficiently large . The choice between these strategies depends on the specific problem, available hardware, and desired model depth.