## Introduction
The ability to train increasingly [deep neural networks](@entry_id:636170) has unlocked remarkable achievements across countless domains. However, this depth comes with a fundamental challenge: the signals, whether activations propagating forward or gradients propagating backward, can become unstable, either shrinking to nothing (vanishing) or growing uncontrollably (exploding). This instability can completely halt the learning process. He initialization, also known as Kaiming initialization, provides a theoretically grounded and elegant solution specifically tailored for networks that use the popular Rectified Linear Unit (ReLU) [activation function](@entry_id:637841). By carefully setting the initial weights, it creates a stable environment where information can flow freely, enabling effective training from the very first step.

This article delves into the theory and practice of He initialization across three chapters. In **Principles and Mechanisms**, we will derive the method from first principles, analyzing how it preserves signal variance in both the forward and backward passes. Next, in **Applications and Interdisciplinary Connections**, we will explore how this principle is adapted for modern architectures like CNNs and Transformers and how it connects to broader topics in optimization, hardware, and scientific computing. Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding, from empirical verification to advanced theoretical derivations. Let us begin by examining the core principles that make He initialization a cornerstone of modern [deep learning](@entry_id:142022).

## Principles and Mechanisms

The successful training of [deep neural networks](@entry_id:636170) is critically dependent on the careful initialization of their parameters. A poorly chosen initialization can lead to the pathological problems of vanishing or exploding signals, where the activations or gradients in the network either shrink to zero or grow uncontrollably as they propagate through the layers. This phenomenon stalls the learning process, as the updates to the weights become either negligible or so large as to cause instability. He initialization, also known as Kaiming initialization, is a principled strategy specifically designed to address this issue in networks employing Rectified Linear Unit (ReLU) [activation functions](@entry_id:141784) and their variants. This chapter will derive its core principles, analyze its behavior in both forward and backward propagation, and explore its extensions and deeper implications.

### The Core Principle: Preserving Signal Variance

The central idea behind modern initialization schemes is to ensure that the statistical properties of the signals—activations in the [forward pass](@entry_id:193086) and gradients in the [backward pass](@entry_id:199535)—remain stable as they traverse the network. A key metric for this stability is the **variance**. If the variance of activations remains constant from layer to layer, the signal is unlikely to vanish or explode.

Let us consider a single neuron in a [fully connected layer](@entry_id:634348). Its pre-activation, $z$, is computed as a linear combination of the outputs, $x_j$, from the previous layer:
$$
z = \sum_{j=1}^{n_{\text{in}}} w_j x_j
$$
Here, $n_{\text{in}}$ is the **[fan-in](@entry_id:165329)**, or the number of input connections to the neuron. To analyze the variance of $z$, we make a few standard assumptions common at initialization:
1.  The weights $w_j$ and inputs $x_j$ are [independent random variables](@entry_id:273896).
2.  All weights are drawn from a distribution with mean $\mathbb{E}[w_j] = 0$ and variance $\mathrm{Var}(w_j) = \sigma_w^2$.
3.  All inputs are identically distributed with mean $\mathbb{E}[x_j] = 0$ and variance $\mathrm{Var}(x_j) = \sigma_x^2$.

Under these assumptions, the mean of the pre-activation $z$ is zero. The variance of $z$ can be calculated as the sum of the variances of the independent terms $w_j x_j$:
$$
\mathrm{Var}(z) = \sum_{j=1}^{n_{\text{in}}} \mathrm{Var}(w_j x_j)
$$
For two independent, zero-mean random variables $A$ and $B$, the variance of their product is $\mathrm{Var}(AB) = \mathbb{E}[A^2]\mathbb{E}[B^2] - (\mathbb{E}[A]\mathbb{E}[B])^2 = \mathrm{Var}(A)\mathrm{Var}(B)$. Applying this, we get:
$$
\mathrm{Var}(z) = \sum_{j=1}^{n_{\text{in}}} \mathrm{Var}(w_j) \mathrm{Var}(x_j) = \sum_{j=1}^{n_{\text{in}}} \sigma_w^2 \sigma_x^2 = n_{\text{in}} \sigma_w^2 \sigma_x^2
$$
This equation links the pre-activation variance to the input variance and the weight variance. Our goal is to make the *post-activation* variance, $\mathrm{Var}(\phi(z))$, equal to the input variance $\sigma_x^2$, where $\phi$ is the [activation function](@entry_id:637841).

For the **Rectified Linear Unit (ReLU)**, defined as $\phi(z) = \max(0, z)$, the analysis requires an additional step. In wide layers, the Central Limit Theorem suggests that the pre-activation $z$, being a sum of many independent random variables, approaches a Gaussian distribution. Assuming $z$ follows a symmetric, zero-mean distribution (like a Gaussian), the output of the ReLU, $y = \phi(z)$, will be non-negative, and thus its mean will not be zero. This complicates a direct variance calculation. However, a common and effective approximation is to analyze the second moment, $\mathbb{E}[y^2]$, as a proxy for [signal power](@entry_id:273924). Since the input $x_j$ is zero-mean, its variance and second moment are identical: $\sigma_x^2 = \mathbb{E}[x_j^2]$. We thus aim to enforce $\mathbb{E}[y^2] = \mathbb{E}[x_j^2]$.

The second moment of the ReLU output is:
$$
\mathbb{E}[y^2] = \mathbb{E}[(\max(0, z))^2]
$$
For a symmetric, zero-mean distribution of $z$, exactly half of the probability mass is on the positive side. Therefore, the expectation of $z^2$ for $z>0$ is half of the total expectation of $z^2$:
$$
\mathbb{E}[(\max(0, z))^2] = \int_0^\infty z^2 p(z) dz = \frac{1}{2} \int_{-\infty}^\infty z^2 p(z) dz = \frac{1}{2} \mathbb{E}[z^2]
$$
Since $\mathbb{E}[z]=0$, we have $\mathbb{E}[z^2] = \mathrm{Var}(z)$. This gives us the crucial relationship for ReLU:
$$
\mathbb{E}[y^2] = \frac{1}{2} \mathrm{Var}(z)
$$
Now we can assemble the pieces. We want the output second moment to equal the input variance (which is also its second moment): $\mathbb{E}[y^2] = \sigma_x^2$.
$$
\sigma_x^2 = \frac{1}{2} \mathrm{Var}(z) = \frac{1}{2} (n_{\text{in}} \sigma_w^2 \sigma_x^2)
$$
Assuming a non-trivial input signal ($\sigma_x^2 \neq 0$), we can solve for the weight variance $\sigma_w^2$ :
$$
1 = \frac{1}{2} n_{\text{in}} \sigma_w^2 \implies \sigma_w^2 = \frac{2}{n_{\text{in}}}
$$
This is the celebrated **He initialization** formula. It dictates that for ReLU-based networks, the variance of the weights in a layer should be inversely proportional to its [fan-in](@entry_id:165329), with a factor of 2.

### Forward and Backward Propagation in Deep Networks

The true power of a proper initialization scheme is revealed in its ability to maintain signal stability across many layers. Let's analyze the propagation of activation variance, $q^{(\ell)} = \mathrm{Var}(y^{(\ell)})$, through a deep network.

Using the [recurrence relations](@entry_id:276612) derived above, the variance of activations in layer $\ell$ is related to that of layer $\ell-1$ by:
$$
q^{(\ell)} \approx \mathbb{E}[(y^{(\ell)})^2] = \frac{1}{2} \mathrm{Var}(z^{(\ell)}) = \frac{1}{2} (n_{\text{in}} \sigma_w^2 q^{(\ell-1)})
$$
If we apply He initialization, $\sigma_w^2 = 2/n_{\text{in}}$, the recurrence simplifies beautifully:
$$
q^{(\ell)} = \frac{1}{2} \left(n_{\text{in}} \left(\frac{2}{n_{\text{in}}}\right) q^{(\ell-1)}\right) = q^{(\ell-1)}
$$
This demonstrates that with He initialization, the activation variance is preserved across all ReLU layers in the forward pass, effectively preventing the signal from vanishing or exploding .

It is instructive to contrast this with **Xavier (or Glorot) initialization**, which proposes $\sigma_w^2 = 1/n_{\text{in}}$. This scheme was derived under the assumption of a linear activation function (or a symmetric one operating in its linear regime, like $\tanh(z) \approx z$). If we mistakenly apply Xavier initialization to a ReLU network, the variance propagation becomes:
$$
q^{(\ell)} = \frac{1}{2} \left(n_{\text{in}} \left(\frac{1}{n_{\text{in}}}\right) q^{(\ell-1)}\right) = \frac{1}{2} q^{(\ell-1)}
$$
The variance is halved at every layer, leading to an [exponential decay](@entry_id:136762) $q^{(L)} = (1/2)^L q^{(0)}$. The activations rapidly shrink to zero, stalling training. This highlights that the choice of initialization is intrinsically linked to the choice of [activation function](@entry_id:637841) . Conversely, applying He initialization to a `tanh` network is also suboptimal, as it tends to push pre-activations into the saturated regions of the `tanh` function, which in turn causes [vanishing gradients](@entry_id:637735) .

A robust initialization must also ensure stability in the [backward pass](@entry_id:199535). The backpropagated error signal, $\delta^{(l)} = \frac{\partial L}{\partial z^{(l)}}$, follows the recurrence:
$$
\delta^{(l)} = (W^{(l+1)})^\top \delta^{(l+1)} \odot \phi'(z^{(l)})
$$
where $\odot$ is the elementwise product. By performing a similar variance analysis, one can derive the relationship for the gradient variances :
$$
\mathrm{Var}(\delta^{(l)}) \approx n_{\text{out}} \sigma_w^2 \mathbb{E}[(\phi'(z^{(l)}))^2] \mathrm{Var}(\delta^{(l+1)})
$$
Here, $n_{\text{out}}$ is the [fan-out](@entry_id:173211) of the layer. For ReLU, the derivative $\phi'(z)$ is $1$ if $z>0$ and $0$ otherwise. Under the symmetric pre-activation assumption, $\mathbb{E}[(\phi'(z))^2] = \frac{1}{2}(1^2) + \frac{1}{2}(0^2) = \frac{1}{2}$. Plugging in He initialization, $\sigma_w^2 = 2/n_{\text{in}}$:
$$
\mathrm{Var}(\delta^{(l)}) \approx n_{\text{out}} \left(\frac{2}{n_{\text{in}}}\right) \left(\frac{1}{2}\right) \mathrm{Var}(\delta^{(l+1)}) = \frac{n_{\text{out}}}{n_{\text{in}}} \mathrm{Var}(\delta^{(l+1)})
$$
This result shows that if layers have roughly equal [fan-in](@entry_id:165329) and [fan-out](@entry_id:173211) (i.e., $n_{\text{in}} \approx n_{\text{out}}$), the variance of the gradients is also preserved during [backpropagation](@entry_id:142012). He initialization thus stabilizes the network in both forward and backward passes.

### Extensions and Practical Implementations

The principled derivation of He initialization allows it to be readily adapted to various architectures and [activation functions](@entry_id:141784).

**Convolutional Layers:** In a 2D convolutional layer with a kernel of size $k \times k$ and $C_{\text{in}}$ input channels, each pre-activation value is computed from a patch of the input. The number of weights involved in this computation is $k \times k \times C_{\text{in}}$. This becomes the effective [fan-in](@entry_id:165329) for the layer. Therefore, the He initialization rule for convolutional weights is :
$$
\sigma_w^2 = \frac{2}{k^2 C_{\text{in}}}
$$

**Parametric ReLU (PReLU):** The same principles apply to variants of ReLU. For instance, the PReLU activation is defined as $\phi(z) = \max(z, az)$, where $a$ is a small, learnable parameter. Re-deriving the second moment of the output gives $\mathbb{E}[\phi(z)^2] = \frac{1+a^2}{2} \mathrm{Var}(z)$. The variance preservation condition becomes:
$$
\sigma_x^2 = \frac{1+a^2}{2} (n_{\text{in}} \sigma_w^2 \sigma_x^2) \implies \sigma_w^2 = \frac{2}{(1+a^2) n_{\text{in}}}
$$
This generalized formula gracefully reduces to standard He initialization when $a=0$ (standard ReLU) and suggests how to initialize networks with more complex activations . In practice, weights are drawn from a distribution, such as a zero-mean normal distribution $\mathcal{N}(0, \sigma_w^2)$ or a symmetric [uniform distribution](@entry_id:261734) $U[-\sqrt{3\sigma_w^2}, \sqrt{3\sigma_w^2}]$, with the variance $\sigma_w^2$ set according to the derived formula.

### Deeper Implications of He Initialization

The principle of variance preservation has consequences that extend beyond mere signal magnitude stability.

**Mean Shift and Optimization:** While He initialization preserves variance, it does not preserve the mean. A zero-mean pre-activation $z \sim \mathcal{N}(0, \sigma_z^2)$ is transformed by ReLU into a strictly non-negative output with a positive mean :
$$
\mathbb{E}[\text{ReLU}(z)] = \frac{\sigma_z}{\sqrt{2\pi}}
$$
This positive mean shift can accumulate through layers, pushing subsequent pre-activations away from the origin. This can be suboptimal for learning. One can counteract this by initializing biases to a negative value, $b = -\sigma_z/\sqrt{2\pi}$, to re-center the features. This line of reasoning is a conceptual precursor to more sophisticated techniques like Batch Normalization, which dynamically re-centers and re-scales activations during training.

**The Optimization Landscape:** Weight initialization directly shapes the loss landscape at the beginning of training. The curvature of this landscape, described by the eigenvalues of the Hessian matrix $\nabla^2 L$, affects the ease of optimization. For a simple two-layer network, the expected largest eigenvalue of the loss Hessian with respect to the output layer weights can be shown to be proportional to $n_{\text{in}} \sigma_w^2$. With He initialization ($\sigma_w^2 = 2/n_{\text{in}}$), this expected curvature is twice as large as it would be with Xavier initialization ($\sigma_w^2 = 1/n_{\text{in}}$) . This illustrates a direct, quantifiable link between the choice of initialization scheme and the initial geometry of the optimization problem.

**Geometric Interpretation:** He initialization also has an elegant geometric interpretation. The Jacobian matrix of a layer's mapping, $J(x)$, describes how the layer transforms infinitesimal input perturbations. An ideal transformation would not systematically shrink or expand these perturbations. For a ReLU layer with He initialization, it can be shown that the expected squared norm of the transformed input vector is preserved :
$$
\mathbb{E}\left[\frac{\|\mathbf{J}(\mathbf{x})\,\mathbf{x}\|_{2}^{2}}{\|\mathbf{x}\|_{2}^{2}}\right] = 1
$$
This means that, on average, the network mapping acts as an **[isometry](@entry_id:150881)** on the input signal, preserving its norm. This property of being a "near-isometry" is a powerful guarantee for [signal integrity](@entry_id:170139) in deep networks.

**Sensitivity to Input Scaling:** The entire derivation of He initialization relies on certain assumptions about the input statistics, namely that they are zero-mean and have a well-behaved variance. If these assumptions are violated, for instance by a [data preprocessing](@entry_id:197920) error that scales the input by a large factor $c$, the carefully balanced dynamics can break down. The activation variances will be scaled by $c^2$, and the gradient magnitudes will be similarly inflated. This can cause the SGD weight updates to become so large that they overwhelm the initial weights, leading to [training instability](@entry_id:634545). There exists a critical scaling factor, $c_{\text{crit}}$, beyond which the network destabilizes, and this factor depends on network parameters like width and [learning rate](@entry_id:140210) . This underscores the critical importance of proper [data normalization](@entry_id:265081) (e.g., to [zero mean](@entry_id:271600) and unit variance) as a prerequisite for initialization schemes to function correctly.

In conclusion, He initialization is not merely a heuristic but a theoretically grounded principle for enabling the training of deep ReLU networks. By ensuring the preservation of signal variance through both forward and backward passes, it creates a stable environment for learning to commence, profoundly influencing [signal propagation](@entry_id:165148), gradient flow, and the initial geometry of the [loss landscape](@entry_id:140292).