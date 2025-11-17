## Introduction
Building accurate mathematical models from experimental data is a cornerstone of modern science and engineering. However, the success of any [data-driven modeling](@entry_id:184110) effort rests upon two fundamental pillars: **[identifiability](@entry_id:194150)** and **[persistency of excitation](@entry_id:189029)**. These concepts address whether a model's parameters can be uniquely determined in principle and whether the experimental data collected is sufficiently informative to perform that determination in practice. Without a firm grasp of these principles, even the most sophisticated identification algorithms can fail, yielding ambiguous or entirely incorrect models from seemingly valid data.

This article provides a comprehensive exploration of these critical concepts, bridging theory and application. It is structured to guide you from foundational principles to real-world implementation challenges.
*   The first chapter, **Principles and Mechanisms**, will formally define [structural identifiability](@entry_id:182904) and [persistency of excitation](@entry_id:189029), exploring the mathematical conditions that govern them and their intimate relationship.
*   Next, **Applications and Interdisciplinary Connections** will demonstrate the profound impact of these concepts across various domains, including [system identification](@entry_id:201290), [adaptive control](@entry_id:262887), robust control design, and even [systems biology](@entry_id:148549).
*   Finally, **Hands-On Practices** will present a series of targeted problems designed to solidify your understanding by confronting common pitfalls and practical challenges in [experimental design](@entry_id:142447) and [parameter estimation](@entry_id:139349).

By navigating these chapters, you will gain the necessary knowledge to design informative experiments and confidently assess the reliability of data-driven models.

## Principles and Mechanisms

The successful estimation of a model's parameters from experimental data hinges on two fundamental concepts: **identifiability** and **[persistency of excitation](@entry_id:189029)**. Identifiability addresses whether the model's structure allows for the unique determination of its parameters in principle, assuming perfect, noise-free data. Persistency of excitation concerns the quality of the input signal used in the experiment, ensuring it is sufficiently "rich" to probe all relevant aspects of the system's dynamics. This chapter elucidates the principles and mechanisms governing these two intertwined concepts, establishing them as prerequisites for any meaningful system identification endeavor.

### Structural Identifiability: Can the Parameters Be Known?

The primary question of identifiability is one of uniqueness. Given a class of parameterized models, if two different sets of parameters produce the exact same input-output behavior for all possible experiments, then it is impossible to distinguish between them based on data. This intrinsic property of the model structure itself is known as [structural identifiability](@entry_id:182904).

#### Global and Local Identifiability

Let us formalize this notion. Consider a general nonlinear [state-space model](@entry_id:273798) where the parameter vector $\theta$ belongs to a parameter space $\Theta$. For a given initial state, this model defines an input-output map, $\mathcal{M}_{\theta}$, which transforms any admissible input signal $u(\cdot)$ into a corresponding output signal $y(\cdot)$.

A parameter vector $\theta$ is said to be **globally structurally identifiable** if the mapping from parameters to input-output maps, $\theta \mapsto \mathcal{M}_{\theta}$, is injective over the entire [parameter space](@entry_id:178581) $\Theta$. This means that for any two distinct parameter vectors $\theta_1, \theta_2 \in \Theta$, their corresponding input-output maps must be different. Equivalently, for any $\theta_1 \neq \theta_2$, there must exist at least one admissible input signal $u(\cdot)$ that produces a different output response for the two models [@problem_id:2876715]. It is not required that *every* input distinguish them, only that at least one such distinguishing input exists in the class of admissible signals.

In many cases, global [identifiability](@entry_id:194150) is too strong a requirement. A weaker but still useful concept is **local [structural identifiability](@entry_id:182904)**. A parameter vector $\theta_0$ is locally structurally identifiable if the mapping $\theta \mapsto \mathcal{M}_{\theta}$ is injective within a small neighborhood of $\theta_0$. This means that no other parameter vector in the immediate vicinity of $\theta_0$ produces the same input-output behavior.

A simple yet insightful example illustrates this distinction [@problem_id:2876781]. Consider a static model where the output $y(t)$ is related to an input $u(t)$ by the equation:
$$
y(t; \theta) = \theta_1^2 u(t) + \theta_2 u(t)^2
$$
with parameters $\theta = (\theta_1, \theta_2)$. Suppose we wish to identify $\theta$ from an experiment using a known input, for example, $u(t) = \cos(t) + \cos(2t)$. For two parameter vectors $\theta_a$ and $\theta_b$ to be indistinguishable, they must produce the same output for all time, meaning $(\theta_{1,a}^2 - \theta_{1,b}^2) u(t) + (\theta_{2,a} - \theta_{2,b}) u(t)^2 = 0$. If the functions $u(t)$ and $u(t)^2$ are linearly independent over the experimental interval (a condition related to [persistency of excitation](@entry_id:189029), which we will discuss shortly), this equality can only hold if the coefficients are zero: $\theta_{1,a}^2 = \theta_{1,b}^2$ and $\theta_{2,a} = \theta_{2,b}$.

The condition $\theta_{1,a}^2 = \theta_{1,b}^2$ implies $\theta_{1,a} = \pm \theta_{1,b}$. It does not require $\theta_{1,a} = \theta_{1,b}$. For instance, the parameter vectors $(1, 3)$ and $(-1, 3)$ are distinct yet produce the exact same output. Because we can find two different parameter vectors that are indistinguishable, the model is **not globally structurally identifiable**. However, at any nominal point $\theta_0 = (\theta_{1,0}, \theta_{2,0})$ where $\theta_{1,0} \neq 0$, we can find a small neighborhood (e.g., one where the sign of the first component does not change) in which $\theta_0$ is the unique solution. Thus, the model is **locally structurally identifiable** everywhere except at points where $\theta_{1,0} = 0$.

A standard method to assess local [identifiability](@entry_id:194150) is through sensitivity analysis. The sensitivity functions are the partial derivatives of the output with respect to the parameters, $\frac{\partial y(t;\theta)}{\partial \theta_i}$. If these sensitivity functions are linearly independent over the experimental interval, the model is locally identifiable. This linear independence is typically assessed by examining the **Fisher Information Matrix (FIM)**, which is, for many noise models, proportional to the Gramian of the sensitivity functions. A non-singular FIM at a point $\theta_0$ is a [sufficient condition](@entry_id:276242) for local [identifiability](@entry_id:194150) at that point. For the example model above, the FIM determinant can be calculated as $27\pi^2\theta_{1,0}^2$, confirming that local identifiability holds precisely when $\theta_{1,0} \neq 0$ [@problem_id:2876781].

### Persistency of Excitation: Is the Input Sufficiently Rich?

Structural identifiability tells us that it is possible in principle to determine the parameters. However, this often relies on the ability to apply a specific, distinguishing input signal. An arbitrary or poorly chosen input may fail to reveal the system's true nature. The property that an input signal must possess to guarantee [identifiability](@entry_id:194150) is called **[persistency of excitation](@entry_id:189029) (PE)**.

#### The Fundamental Problem: Insufficient Excitation

Let us consider a simple second-order Finite Impulse Response (FIR) model: $y(k) = \theta_1 u(k-1) + \theta_2 u(k-2)$. The model can be written in [linear regression](@entry_id:142318) form as $y(k) = \varphi(k)^\top \theta$, where $\varphi(k) = [u(k-1), u(k-2)]^\top$ is the **regressor** vector and $\theta = [\theta_1, \theta_2]^\top$ is the parameter vector.

Suppose we conduct an experiment using an exponentially decaying input, $u(k) = A\alpha^k$ [@problem_id:2876760]. The regressor at time $k$ is $\varphi(k) = [A\alpha^{k-1}, A\alpha^{k-2}]^\top = A\alpha^{k-2} [\alpha, 1]^\top$. Critically, for all time steps $k$, the regressor vector $\varphi(k)$ always points in the same direction, namely along the vector $[\alpha, 1]^\top$. The input signal is not rich enough to explore the two-dimensional space of regressors; it only excites a one-dimensional subspace.

What is the consequence? Suppose two different parameter vectors, $\theta$ and $\phi$, produce the same output. This requires $(\theta_1 - \phi_1) u(k-1) + (\theta_2 - \phi_2) u(k-2) = 0$. After substituting the input and simplifying, this reduces to a single linear constraint: $(\theta_1 - \phi_1)\alpha + (\theta_2 - \phi_2) = 0$. Any pair of distinct parameter vectors satisfying this constraint will be indistinguishable. For instance, if $\alpha=2$, the parameter vectors $\theta = (3, -1)$ and $\phi = (1, 3)$ both satisfy the constraint and will produce identical outputs, making unique identification impossible. The input signal failed to be persistently exciting.

#### Formal Definition of Persistency of Excitation

This example motivates the formal definition of PE. An input signal is PE if the corresponding regressor sequence is rich enough to span the entire parameter space over time. For a discrete-time regressor vector $\phi_n(k) \in \mathbb{R}^n$, the signal is said to be **persistently exciting of order $n$** if there exist an integer $N \ge n$ and a scalar $\alpha > 0$ such that for all time steps $t$, the windowed Gramian matrix is uniformly positive definite [@problem_id:2876713]:
$$
\sum_{k=t}^{t+N-1} \phi_n(k) \phi_n(k)^\top \succeq \alpha I_n
$$
Here, $I_n$ is the $n \times n$ identity matrix, and $\succeq$ denotes the Loewner [partial order](@entry_id:145467) (meaning the difference of the matrices is [positive semi-definite](@entry_id:262808)).

This condition has a direct operational meaning. The matrix on the left is the [information matrix](@entry_id:750640) for a [least-squares](@entry_id:173916) estimation problem over a window of length $N$. The condition guarantees that its smallest eigenvalue is bounded away from zero by $\alpha$. This ensures that the estimation problem is well-posed and that the parameters can be uniquely determined from any block of data of length $N$. The integer $N$ is the window length over which the excitation is guaranteed, and $\alpha$ quantifies the "strength" of this excitation.

The same principle applies to [continuous-time systems](@entry_id:276553). For a continuous-time regressor $\phi_n(t)$, the signal is PE of order $n$ if there exist $T > 0$ and $\alpha > 0$ such that for all $t$:
$$
\int_{t}^{t+T} \phi_n(\tau) \phi_n(\tau)^\top d\tau \succeq \alpha I_n
$$
This condition ensures the invertibility of the [information matrix](@entry_id:750640) in continuous-time estimation problems [@problem_id:2876752]. The regressor $\phi_n(t)$ is typically formed by convolving the input $u(t)$ with a set of fixed, stable, and linearly independent basis functions (e.g., Dirac impulses for FIR models, or Laguerre functions for more general LTI models) that span the space where the system's true impulse response is assumed to lie.

### PE Requirements for Common Model Structures

The required order of [persistency of excitation](@entry_id:189029) is determined by the number of parameters to be identified.

#### Linear Regression and ARX Models

For any system that can be written in the linear regression form $y(k) = \varphi(k)^\top \theta$ with $\theta \in \mathbb{R}^d$, unique identification of $\theta$ requires the regressor sequence $\{\varphi(k)\}$ to be persistently exciting of order $d$.

A cornerstone of system identification is the Auto-Regressive with eXogenous input (ARX) model. For a single-input, single-output (SISO) system, this model takes the form:
$$
y(k) + a_1 y(k-1) + \dots + a_{n_a} y(k-n_a) = b_0 u(k) + \dots + b_{n_b} u(k-n_b)
$$
This can be rearranged into a [linear regression](@entry_id:142318) with $n_a + n_b + 1$ parameters. The regressor vector $\varphi(k)$ consists of past outputs and past inputs: $\varphi(k) = [-y(k-1), \dots, -y(k-n_a), u(k), \dots, u(k-n_b)]^\top$. Consequently, for the parameters of a SISO ARX model to be identifiable, the regressor sequence must be **PE of order $n_a + n_b + 1$** [@problem_id:2876717]. This result assumes the polynomials describing the numerator and denominator of the system's transfer function are coprime (share no common factors), ensuring the [parameterization](@entry_id:265163) is minimal.

This principle extends directly to Multiple-Input Multiple-Output (MIMO) systems. For a MIMO ARX model with $p$ outputs, $m$ inputs, and model orders $n_a$ and $n_b$, the number of scalar parameters can be substantial. The PE condition on the input $\mathbf{u}(k) \in \mathbb{R}^m$ is typically stated by requiring that a block Toeplitz matrix formed from the input sequence has full column rank. A necessary condition for the [identifiability](@entry_id:194150) of all model parameters is that the input signal $\mathbf{u}(k)$ must be persistently exciting of an order $L \ge n_a + n_b$ [@problem_id:2876718].

#### From Regressor PE to Input Design

The PE condition is defined for the regressor, which contains both inputs and outputs. However, we can only directly design the input. A crucial question in experimental design is: what properties must the input $u(k)$ have to make the regressor $\varphi(k)$ persistently exciting?

The answer lies in the frequency domain. A loss of [identifiability](@entry_id:194150) occurs if the input signal can be completely annihilated by some non-zero linear filter whose structure depends on the model's polynomials. To prevent this, the input's spectrum must be sufficiently rich to avoid being a null input for any such filter.

A celebrated result provides a concrete guideline for ARX models: an input signal consisting of a sum of sinusoids is PE of an order related to the number of sinusoids. Specifically, a signal composed of $m$ distinct sinusoids is PE of order $2m$ [@problem_id:2876713]. To identify all $n_a + n_b$ parameters of a stable, open-loop ARX model (with $b_0=0$), the number of distinct frequency components in the input must be large enough. It can be shown that the minimum number of sinusoids, $L$, required in the input is [@problem_id:2876753]:
$$
L_{\min} = \left\lceil \frac{n_a + n_b}{2} \right\rceil
$$
This provides a powerful and practical tool for designing experiments that guarantee [identifiability](@entry_id:194150).

### Advanced Topics and Practical Challenges

While the core principles of [identifiability](@entry_id:194150) and PE provide a solid foundation, several practical challenges and nuances arise in real-world applications.

#### Practical Identifiability vs. Structural Identifiability

Structural [identifiability](@entry_id:194150) is a binary property: a model either is or is not identifiable. However, in practice, we deal with finite, noisy data. A model can be structurally identifiable, but so poorly conditioned that parameter estimates are extremely sensitive to noise. This leads to the concept of **[practical identifiability](@entry_id:190721)**.

Consider a model whose output is a sum of two exponentials with very close decay rates [@problem_id:2876778]:
$$
y(t; \theta) = \theta_1 \exp(-t) + \theta_2 \exp(-(1+\varepsilon)t)
$$
For any $\varepsilon > 0$, the two basis functions $\exp(-t)$ and $\exp(-(1+\varepsilon)t)$ are linearly independent, so the model is structurally identifiable. However, as $\varepsilon \to 0^+$, the two functions become nearly collinear. Trying to distinguish their respective contributions, $\theta_1$ and $\theta_2$, becomes an extremely [ill-conditioned problem](@entry_id:143128).

This [ill-conditioning](@entry_id:138674) is reflected in the Fisher Information Matrix. As $\varepsilon \to 0^+$, the FIM becomes nearly singular. Its **condition number**—the ratio of its largest to its [smallest eigenvalue](@entry_id:177333)—is a measure of this ill-conditioning. For the two-exponential problem, the condition number of the FIM based on samples at $t=0$ and $t=\tau$ can be shown to grow asymptotically as:
$$
\kappa \approx \frac{16\cosh^{2}(\tau)}{\varepsilon^{2}\tau^{2}}
$$
This explosion of the condition number as $1/\varepsilon^2$ quantifies the loss of [practical identifiability](@entry_id:190721). While theoretically possible, identifying the parameters for a very small $\varepsilon$ would require an unrealistic amount of noise-free data.

#### Identifiability in Closed-Loop Systems

A significant challenge arises when identifying systems operating under [feedback control](@entry_id:272052). In an open-loop experiment, the input $u(t)$ is independent of the process noise $v(t)$. In a closed-loop system, the controller generates the input based on the output, which is corrupted by noise. This creates a fundamental correlation between the input $u(t)$ and the noise $v(t)$.

This correlation confounds standard identification methods. The frequency-domain expression for the system's transfer function $G$ is:
$$
G(\mathrm{e}^{\mathrm{j}\omega}) = \frac{\Phi_{uy}(\omega) - \Phi_{uv}(\omega)}{\Phi_{uu}(\omega)}
$$
where $\Phi_{uy}$ is the cross-spectrum between input and output, $\Phi_{uu}$ is the input power spectrum, and $\Phi_{uv}$ is the cross-spectrum between the input and noise. In an open-loop experiment, $\Phi_{uv}(\omega) = 0$, and $G$ can be estimated directly from the measured input-output spectra. In a closed loop, $\Phi_{uv}(\omega) \neq 0$, and this term is unknown, preventing a direct solution for $G$ [@problem_id:2876710].

If the system is operating in a closed loop without any external excitation signal (i.e., for regulation), the input-output data will be driven solely by the [process noise](@entry_id:270644). In this scenario, the joint spectrum of the input and output generally does not contain enough information to distinguish the plant dynamics $G$ from the controller dynamics $K$. The experiment is not informative for $G$ [@problem_id:2876710].

The solution is to design the experiment to break this correlation. This is achieved by introducing an **exogenous reference signal** $r(t)$ into the control loop, such that the input is generated, for example, by $u(t) = K(q^{-1})(r(t) - y(t))$. If this external signal $r(t)$ is persistently exciting and is uncorrelated with the [process noise](@entry_id:270644) $v(t)$, it injects "fresh" excitation into the loop. This allows the influence of the plant to be separated from the influence of the feedback and the noise, rendering the plant parameters identifiable, provided the controller $K$ is known [@problem_id:2876710]. This demonstrates that careful [experimental design](@entry_id:142447) is paramount for successful identification of systems under feedback.