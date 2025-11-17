## Introduction
In the landscape of [scientific computing](@entry_id:143987), [solving partial differential equations](@entry_id:136409) (PDEs) that model complex physical phenomena remains a fundamental challenge. Traditional numerical methods, while powerful, often rely on structured meshes and can be computationally intensive, especially for problems in complex geometries or high dimensions. A new paradigm has emerged at the intersection of machine learning and computational science: Physics-Informed Neural Networks (PINNs). This innovative approach leverages the remarkable [function approximation](@entry_id:141329) capabilities of deep learning while embedding the governing laws of physics directly into the learning process. This article addresses the knowledge gap between traditional PDE solvers and this novel, data-driven yet physics-constrained methodology. It provides a comprehensive introduction to PINNs, moving from their theoretical underpinnings to their practical applications and implementation.

Across the following chapters, you will gain a robust understanding of this powerful technique. The first chapter, **"Principles and Mechanisms"**, will deconstruct the core components of a PINN, explaining how neural networks are transformed into differentiable function approximators and how physics is encoded within a composite [loss function](@entry_id:136784). Following this, **"Applications and Interdisciplinary Connections"** will showcase the versatility of PINNs by exploring their use in solving a wide array of forward and [inverse problems](@entry_id:143129) across disciplines like fluid dynamics, quantum mechanics, and finance. Finally, **"Hands-On Practices"** will bridge theory and practice, guiding you through the construction and implementation of PINNs to solve real-world physical problems.

## Principles and Mechanisms

At its core, a Physics-Informed Neural Network (PINN) leverages the remarkable capacity of neural networks as universal function approximators, but with a crucial distinction: the network is not trained solely on data. Instead, its training process is governed by a loss function that encodes the fundamental physical laws governing the system, typically expressed as partial differential equations (PDEs). This chapter will deconstruct the foundational principles and mechanisms that enable this fusion of machine learning and physics.

### The Neural Network as a Differentiable Function

A standard [feedforward neural network](@entry_id:637212) can be viewed as a highly flexible function, $\hat{u}(\mathbf{x}; \theta)$, that maps an input vector $\mathbf{x}$ (e.g., spatial and temporal coordinates) to an output scalar or vector $\hat{u}$. The behavior of this function is dictated by its trainable parameters, $\theta$, which consist of [weights and biases](@entry_id:635088) organized in layers. The network constructs its output through a sequence of [linear transformations](@entry_id:149133) and nonlinear [activation functions](@entry_id:141784). For instance, the output of a single neuron in a hidden layer might be $\sigma(\mathbf{w} \cdot \mathbf{v} + b)$, where $\mathbf{v}$ is the vector of outputs from the previous layer, $\mathbf{w}$ and $b$ are the neuron's weight vector and bias, and $\sigma$ is a nonlinear activation function.

The key mechanism that makes PINNs possible is **[automatic differentiation](@entry_id:144512) (AD)**. Because the neural network is a composition of elementary arithmetic operations and functions (like addition, multiplication, and [activation functions](@entry_id:141784)) for which derivatives are known, the [chain rule](@entry_id:147422) can be applied systematically to compute the exact analytical derivative of the network's output $\hat{u}$ with respect to its input coordinates $\mathbf{x}$. This process is not a [numerical approximation](@entry_id:161970) like [finite differences](@entry_id:167874); it is an algorithmic calculation of the exact derivative of the function represented by the network.

This capability is profound. It means we can supply the network's output, our candidate solution $\hat{u}(\mathbf{x}; \theta)$, to any [differential operator](@entry_id:202628) and compute the result. Consider the Korteweg-de Vries (KdV) equation, which involves first and third-order derivatives:

$$
\frac{\partial u}{\partial t} + 6u \frac{\partial u}{\partial x} + \frac{\partial^3 u}{\partial x^3} = 0
$$

If we represent the solution $u(x, t)$ with a neural network $\mathcal{N}(x, t; \theta)$, we can use AD to compute the terms $\frac{\partial \mathcal{N}}{\partial t}$, $\frac{\partial \mathcal{N}}{\partial x}$, and $\frac{\partial^3 \mathcal{N}}{\partial x^3}$ for any given input $(x, t)$. These derivatives are themselves functions of the network parameters $\theta$, and AD allows us to compute gradients of these derivative terms with respect to $\theta$, which is essential for training. [@problem_id:2126350]

The ability to compute [higher-order derivatives](@entry_id:140882) imposes a critical constraint on the choice of architecture, specifically the activation function. To evaluate a $k$-th order PDE, the network must be at least $k$ times differentiable with respect to its inputs. This necessitates the use of smooth ($C^k$-continuous) [activation functions](@entry_id:141784). For instance, if a PINN is designed to solve a second-order PDE like the heat equation, the calculation of the PDE residual requires computing second derivatives of the network's output. A popular [activation function](@entry_id:637841) in many machine learning contexts, the Rectified Linear Unit (ReLU), defined as $f(z) = \max(0, z)$, is unsuitable for this task. Its first derivative is a discontinuous [step function](@entry_id:158924), and its second derivative is mathematically undefined at the origin and zero elsewhere. Using ReLU would prevent the loss function from properly penalizing violations of the second-order terms in the PDE, crippling the training process. In contrast, smooth functions like the hyperbolic tangent, $\tanh(z)$, or the [sigmoid function](@entry_id:137244) are infinitely differentiable ($C^\infty$). Their derivatives are well-defined and continuous to any order, allowing AD to correctly compute the necessary terms for the PDE residual and their gradients for training. [@problem_id:2126336]

### The Physics-Informed Loss Function

The "intelligence" of a PINN lies in its [loss function](@entry_id:136784), which serves as the bridge between the mathematical description of a physical system and the optimization process of the neural network. Instead of solely minimizing the error against a large dataset of known solutions, a PINN minimizes a composite loss function that penalizes deviations from physical laws. This total loss, $\mathcal{L}(\theta)$, is typically a weighted sum of several components.

#### PDE Residual Loss

The primary component is the **PDE residual loss**, $\mathcal{L}_{PDE}$. For a general PDE written in the form $\mathcal{F}[u(\mathbf{x})] = 0$, the residual for the network's approximation $\hat{u}(\mathbf{x}; \theta)$ is defined as $r(\mathbf{x}; \theta) = \mathcal{F}[\hat{u}(\mathbf{x}; \theta)]$. The goal of training is to make this residual as close to zero as possible across the entire problem domain. As it is impossible to enforce this condition everywhere, it is instead enforced at a large set of sample points within the domain, known as **collocation points**. The PDE loss is then formulated as the [mean squared error](@entry_id:276542) of the residuals at these points:

$$
\mathcal{L}_{PDE}(\theta) = \frac{1}{N_r} \sum_{i=1}^{N_r} |r(\mathbf{x}_i^r; \theta)|^2
$$

where $\{\mathbf{x}_i^r\}_{i=1}^{N_r}$ is the set of $N_r$ collocation points.

#### Boundary and Initial Condition Loss

A PDE alone defines a family of solutions. To specify a unique solution, we need auxiliary information in the form of [initial conditions](@entry_id:152863) (ICs) and boundary conditions (BCs). These are incorporated into the PINN framework through additional loss terms. For a set of $N_{ic}$ points on the initial boundary and $N_{bc}$ points on the spatial boundary where the solution is known, the **IC loss** ($\mathcal{L}_{IC}$) and **BC loss** ($\mathcal{L}_{BC}$) are formulated as the [mean squared error](@entry_id:276542) between the network's prediction and the specified values:

$$
\mathcal{L}_{IC}(\theta) = \frac{1}{N_{ic}} \sum_{i=1}^{N_{ic}} |\hat{u}(\mathbf{x}_i^{ic}; \theta) - u_{IC}(\mathbf{x}_i^{ic})|^2
$$

$$
\mathcal{L}_{BC}(\theta) = \frac{1}{N_{bc}} \sum_{i=1}^{N_{bc}} |\hat{u}(\mathbf{x}_i^{bc}; \theta) - u_{BC}(\mathbf{x}_i^{bc})|^2
$$

Let's consider a concrete example: the one-dimensional [advection equation](@entry_id:144869), $\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = 0$, on a domain $x \in [X_0, X_1]$ with an initial condition $u(x, 0) = f(x)$ and [periodic boundary conditions](@entry_id:147809) $u(X_0, t) = u(X_1, t)$. The total loss function for a PINN $\hat{u}(x, t; \theta)$ would be a weighted sum $\mathcal{L}(\theta) = w_{PDE} \mathcal{L}_{PDE} + w_{IC} \mathcal{L}_{IC} + w_{BC} \mathcal{L}_{BC}$, explicitly written as:
[@problem_id:2126319]

$$
\mathcal{L}(\theta) = \frac{w_{PDE}}{N_r} \sum_{i=1}^{N_r} \left( \frac{\partial \hat{u}}{\partial t}(x_i^r, t_i^r) + c \frac{\partial \hat{u}}{\partial x}(x_i^r, t_i^r) \right)^2 + \frac{w_{IC}}{N_{ic}} \sum_{i=1}^{N_{ic}} \left( \hat{u}(x_i^{ic}, 0) - f(x_i^{ic}) \right)^2 + \frac{w_{BC}}{N_{bc}} \sum_{i=1}^{N_{bc}} \left( \hat{u}(X_0, t_i^{bc}) - \hat{u}(X_1, t_i^{bc}) \right)^2
$$

This formulation elegantly combines the enforcement of the governing law in the domain's interior with the enforcement of conditions on its boundaries.

#### Data-Driven Constraints

In many scientific problems, particularly inverse problems, the ICs and BCs may not be fully known. Instead, we might have a set of sparse and potentially noisy measurements of the solution $u$ at various points $\{(\mathbf{x}_i, u_i)\}_{i=1}^{N}$ within the domain. In this scenario, a **data loss** term, $\mathcal{L}_{data}$, is introduced:

$$
\mathcal{L}_{data}(\theta) = \frac{1}{N} \sum_{i=1}^{N} |\hat{u}(\mathbf{x}_i; \theta) - u_i|^2
$$

Here, the role of $\mathcal{L}_{data}$ is conceptually identical to that of $\mathcal{L}_{IC}$ and $\mathcal{L}_{BC}$. Minimizing the PDE residual $\mathcal{L}_{PDE}$ alone constrains the network's output to the family of functions that satisfy the physical law. The data loss term $\mathcal{L}_{data}$ then provides the specific constraints needed to select the one unique solution from this family that best agrees with the observed measurements. In this way, sparse data points serve to "anchor" the physically-constrained solution, much like boundary conditions do in a traditional [forward problem](@entry_id:749531). [@problem_id:2126334]

### Nuances of the Training Process

Training a PINN involves finding the parameters $\theta$ that minimize the total loss function $\mathcal{L}(\theta)$. This optimization is typically performed using [gradient-based algorithms](@entry_id:188266) like Adam. However, the multi-term nature of the [loss function](@entry_id:136784) introduces several challenges and nuances.

#### Balancing Loss Components

The relative magnitudes of the different loss terms ($\mathcal{L}_{PDE}$, $\mathcal{L}_{BC}$, etc.) can vary by orders of magnitude, and their gradients can have [complex dynamics](@entry_id:171192) during training. The weighting factors ($w_{PDE}, w_{BC}$, etc.) are therefore not just arbitrary constants but crucial hyperparameters that balance the trade-off between satisfying the physics and fitting the boundary/data constraints.

An improper balance can lead to pathological training outcomes. For instance, consider solving the heat equation. If the weight for the boundary conditions, $\lambda_{BC}$, is set significantly higher than the weight for the PDE, $\lambda_{PDE}$, the optimizer will prioritize matching the boundary values. This may result in a solution that fits the BCs perfectly but largely ignores the governing heat equation in the interior of the domain. Conversely, if $\lambda_{PDE} \gg \lambda_{BC}$, the network will learn a function that is an excellent solution to the PDE but may grossly violate the specified boundary conditions. [@problem_id:2126325] Finding an appropriate balance, which may even require adapting the weights during training, is a key practical challenge in the successful application of PINNs.

#### The Importance of Collocation Point Sampling

The PDE loss is an empirical average of the squared residual over the set of collocation points. This is a Monte Carlo approximation of the true integrated squared residual over the domain. The accuracy and efficiency of this approximation depend heavily on the distribution of these points.

A simple uniform sampling strategy may be inefficient. If the solution has regions of high complexity (e.g., sharp gradients, [boundary layers](@entry_id:150517)), the PDE residual will likely be largest in these areas. A uniform distribution may undersample these critical regions, leading the optimizer to believe the loss is low when, in fact, significant errors are being missed. This is illustrated by how the computed loss for a fixed approximate solution can change drastically depending on whether collocation points are placed uniformly or clustered in a specific region. [@problem_id:2126323]

This observation motivates the use of **adaptive sampling** strategies. A powerful and principled approach is to periodically update the set of collocation points during training. After a number of training epochs, the current network is used to evaluate the PDE residual $|r(\mathbf{x}; \theta)|$ over a large candidate set of points. New collocation points are then preferentially sampled from regions where the residual is highest. This strategy, inspired by importance sampling in [numerical integration](@entry_id:142553), focuses the network's "attention" on the areas where its approximation is worst, leading to more accurate and efficient training. [@problem_id:2126304]

### Advanced Formulations and Architectural Choices

Beyond the basic framework, several advanced techniques can significantly improve the performance and applicability of PINNs.

#### Hard vs. Soft Enforcement of Boundary Conditions

Enforcing boundary conditions via a loss term, as described above, is known as "soft" enforcement. The network is penalized for violating the BCs, but not strictly forbidden from doing so. An alternative is "hard" enforcement, where the [network architecture](@entry_id:268981) is designed such that the boundary conditions are satisfied by construction.

For a problem on $x \in [0, L]$ with Dirichlet boundary conditions $u(0)=A$ and $u(L)=B$, we can define the PINN's output not as the raw network output $\hat{u}_{NN}(x)$, but as a transformed function:
[@problem_id:2126300]

$$
u_{NN}(x) = g(x) + s(x) \hat{u}_{NN}(x)
$$

Here, $g(x)$ is a simple function that already satisfies the boundary conditions (e.g., the linear interpolant $g(x) = A(1-x/L) + B(x/L)$), and $s(x)$ is a function that is zero at the boundaries (e.g., $s(x) = x(L-x)$). By construction, $u_{NN}(0) = g(0) + s(0)\hat{u}_{NN}(0) = A + 0 = A$, and similarly $u_{NN}(L)=B$, regardless of the output of the underlying network $\hat{u}_{NN}(x)$. This approach forces the network to satisfy the BCs exactly and can lead to faster and more stable training, as the optimizer no longer needs to learn the boundary behavior and can focus entirely on satisfying the PDE in the interior.

#### Strong vs. Weak Formulations

The standard PINN formulation, which drives the pointwise PDE residual to zero, is known as the **strong form**. This approach requires computing high-order derivatives and implicitly assumes the solution is sufficiently smooth. However, many real-world problems, especially in fields like solid mechanics, involve solutions with limited regularity (e.g., at re-entrant corners or crack tips), where stresses may be singular and second derivatives of the [displacement field](@entry_id:141476) may not exist in a classical sense.

For such problems, it is advantageous to use the **weak (or variational) form** of the PDE. The [weak form](@entry_id:137295) is derived by multiplying the PDE by a set of "[test functions](@entry_id:166589)" and integrating by parts over the domain. This process reduces the order of derivatives required for the solution. For instance, in linear elasticity, the strong form involves second derivatives of the [displacement field](@entry_id:141476) (implying the solution should be in the Sobolev space $H^2$), whereas the [weak form](@entry_id:137295) only requires first derivatives (requiring only $H^1$ regularity). A weak-form PINN (often called a Variational PINN or VPINN) is trained to satisfy this integral identity rather than the pointwise residual. This makes it naturally suited for problems with singularities or discontinuities, where the strong-form residual is ill-defined. Furthermore, weak forms naturally incorporate certain types of boundary conditions (Neumann conditions) and [interface conditions](@entry_id:750725) in a more robust, integral sense. [@problem_id:2668902]

The choice is a trade-off: for problems with smooth solutions, the strong form can be computationally more efficient as it only requires pointwise evaluation of the residual, avoiding the expensive [numerical quadrature](@entry_id:136578) needed to compute integrals in the weak form. However, for low-regularity problems, the weak form is the more mathematically sound and robust approach. [@problem_id:2668902]

### Inherent Properties and Limitations: Spectral Bias

Finally, it is essential to understand an inherent property of neural networks that profoundly impacts PINN performance: **[spectral bias](@entry_id:145636)**. When trained with [gradient-based methods](@entry_id:749986), neural networks exhibit a strong preference for learning low-frequency functions over high-frequency functions.

Consider training a PINN to solve a differential equation whose solution is a superposition of a low-frequency and a high-frequency component, such as $u(x) = \sin(x) + \sin(25x)$. During the initial stages of training, the network will rapidly learn the smooth, low-frequency $\sin(x)$ component. However, it will struggle to capture the highly oscillatory, high-frequency $\sin(25x)$ component. The learned amplitudes of the two components will show that the low-frequency one dominates early in training. [@problem_id:2427229]

This [spectral bias](@entry_id:145636) has significant practical implications. It makes standard PINNs challenging to apply to problems involving complex, multi-scale phenomena, turbulence, or solutions with sharp, localized features, as these all contain significant high-frequency content. Overcoming [spectral bias](@entry_id:145636) is an active and important area of research in the field of [scientific machine learning](@entry_id:145555), with various techniques such as Fourier feature mapping and modified network architectures being developed to help networks better represent high-frequency functions.