## Introduction
While [deep neural networks](@entry_id:636170) are defined by deterministic architectures, their training and behavior are fundamentally [stochastic processes](@entry_id:141566). From the random initialization of weights to the sampling of mini-batches and the use of explicit regularization like dropout, randomness is not a bug but a feature of modern [deep learning](@entry_id:142022). To harness this stochasticity effectively, we need a rigorous mathematical language. The core concepts of **expectation**, **variance**, and **covariance** provide this essential toolkit, allowing us to move beyond heuristic design and towards a principled understanding of model dynamics. This article addresses the critical gap between observing random behavior in networks and being able to mathematically analyze, predict, and control it.

Across three chapters, you will gain a comprehensive understanding of these statistical pillars. The journey begins with **Principles and Mechanisms**, where we will explore how [expectation and variance](@entry_id:199481) govern the stability of [signal propagation](@entry_id:165148) and form the basis of optimizers and initialization schemes. Next, in **Applications and Interdisciplinary Connections**, we will see how these concepts are actively employed to build powerful tools like [normalization layers](@entry_id:636850), [variance reduction techniques](@entry_id:141433), and methods for uncertainty quantification, even extending to societal concerns like fairness. Finally, **Hands-On Practices** will provide opportunities to implement these ideas and observe phenomena like neural collapse and Monte Carlo dropout firsthand. By mastering these concepts, you will be equipped to design, debug, and innovate in the complex and stochastic world of [deep learning](@entry_id:142022).

## Principles and Mechanisms

The behavior of [deep neural networks](@entry_id:636170), despite their deterministic architecture, is profoundly governed by principles of probability and statistics. This [stochasticity](@entry_id:202258) arises from multiple sources: the random initialization of weights, the sampling of mini-batches from a larger data distribution, and explicit [regularization techniques](@entry_id:261393) like dropout. To navigate this landscape of uncertainty, the foundational concepts of **expectation**, **variance**, and **covariance** are not merely descriptive tools but essential mechanisms for analysis, design, and optimization. This chapter will systematically explore how these statistical moments provide a rigorous framework for understanding and controlling the dynamics of [deep learning models](@entry_id:635298).

### Fundamental Moments and Their Role in Optimization

At the core of our statistical toolkit are the first and second [moments of a random variable](@entry_id:174539) or vector. The **expectation**, denoted as $\mathbb{E}[X]$, represents the mean or average value of a random variable $X$. It provides a measure of its central tendency. The **variance**, $\operatorname{Var}(X)$, measures the spread or dispersion of the variable around its mean. It is formally defined as $\operatorname{Var}(X) = \mathbb{E}[(X - \mathbb{E}[X])^2]$, which can be conveniently calculated using the identity $\operatorname{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2$. This shows that variance is the difference between the average of the squares (the uncentered second moment) and the square of the average. The **covariance**, $\operatorname{Cov}(X, Y) = \mathbb{E}[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])]$, measures the degree to which two variables move together.

These concepts are immediately relevant in the design of modern adaptive optimizers like Adam or RMSProp. These algorithms normalize the gradient update for each parameter by an estimate of its second moment. A crucial design choice is whether to use a **centered second moment** (the variance) or an **uncentered second moment** ($\mathbb{E}[g^2]$). While variance measures the magnitude of random fluctuations around the mean gradient, the uncentered second moment also incorporates the magnitude of the mean gradient itself.

Consider a mini-batch gradient $g$ for a single parameter, which is the average of $B$ independent per-example gradients, each with mean $\mu$ and variance $\sigma^2$. The mini-batch gradient $g$ will have a mean $\mathbb{E}[g] = \mu$ and a variance $\operatorname{Var}(g) = \sigma^2/B$. The uncentered second moment is therefore $\mathbb{E}[g^2] = \operatorname{Var}(g) + (\mathbb{E}[g])^2 = \frac{\sigma^2}{B} + \mu^2$.

The ratio of the square roots of these quantities, used in normalization, reveals a potentially significant inflation factor. Let's define this factor as $R \equiv \frac{\sqrt{\mathbb{E}[g^{2}]}}{\sqrt{\operatorname{Var}(g)}}$. Substituting our derived expressions yields:
$$
R = \frac{\sqrt{\frac{\sigma^2}{B} + \mu^2}}{\sqrt{\frac{\sigma^2}{B}}} = \sqrt{1 + \frac{B\mu^2}{\sigma^2}}
$$
This result  shows that when the true gradient has a consistent non-[zero mean](@entry_id:271600) ($\mu \neq 0$), using the uncentered second moment $\mathbb{E}[g^2]$ leads to a larger normalization term than using the variance alone. This "inflation" is more pronounced for larger batch sizes $B$ and for gradients where the signal ($\mu$) is strong relative to the per-example noise ($\sigma$). This distinction highlights a subtle but important aspect of how adaptive optimizers behave, particularly in later stages of training where the gradient mean might be consistently small.

### Signal Propagation Dynamics

The stability of a deep neural network hinges on how signals—activations in the forward pass and gradients in the [backward pass](@entry_id:199535)—propagate through its layers. If the variance of these signals grows exponentially with depth, they can saturate or explode; if it shrinks exponentially, they vanish, and the network becomes untrainable. Expectation and variance provide the tools to analyze and prevent these issues.

#### Forward Propagation and Initialization

A simple yet insightful model is a deep linear network with scalar weights, where the output is $y = W_{L} W_{L-1} \cdots W_{1} x$. If we assume the weights $W_{\ell}$ and input $x$ are independent, zero-mean random variables with variances $\sigma_{W_{\ell}}^2$ and $\sigma_x^2$ respectively, the expectation of the output is trivially zero. The variance, however, propagates multiplicatively:
$$
\operatorname{Var}(y) = \mathbb{E}[y^2] - (\mathbb{E}[y])^2 = \mathbb{E}[(W_{L} \cdots W_{1} x)^2] = \mathbb{E}[W_L^2] \cdots \mathbb{E}[W_1^2] \mathbb{E}[x^2]
$$
Since each variable has [zero mean](@entry_id:271600), its variance is equal to its second moment. Thus:
$$
\operatorname{Var}(y) = \sigma_{W_L}^2 \cdots \sigma_{W_1}^2 \sigma_x^2 = \sigma_x^2 \prod_{\ell=1}^{L} \sigma_{W_{\ell}}^2
$$
This analysis  clearly shows that if the weight variances are consistently greater than $1$, the output variance will explode, and if they are less than $1$, it will vanish. To maintain stability, we need the product of variances to be near unity.

This principle generalizes to non-linear networks and forms the basis of modern [weight initialization](@entry_id:636952) schemes. Consider a fully-connected layer where a pre-activation is $h_i^{(l)} = \sum_{j=1}^{n_{l-1}} w_{ij}^{(l)} x_{j}^{(l-1)}$. Assume the weights $w_{ij}^{(l)}$ and inputs $x_j^{(l-1)}$ are independent and zero-mean. The variance of the pre-activation is:
$$
\operatorname{Var}(h_i^{(l)}) = \sum_{j=1}^{n_{l-1}} \operatorname{Var}(w_{ij}^{(l)} x_j^{(l-1)}) = \sum_{j=1}^{n_{l-1}} \mathbb{E}[(w_{ij}^{(l)})^2] \mathbb{E}[(x_j^{(l-1)})^2] = n_{l-1} \operatorname{Var}(w) \operatorname{Var}(x^{(l-1)})
$$
Here, $x^{(l-1)} = \phi(h^{(l-1)})$ is the output of the previous layer's [activation function](@entry_id:637841) $\phi$. To keep the variance stable, i.e., $\operatorname{Var}(h^{(l)}) = \operatorname{Var}(h^{(l-1)})$, we need to set the weight variance $\operatorname{Var}(w)$ carefully.

For a linear [activation function](@entry_id:637841) $\phi(z) = z$, we have $\operatorname{Var}(x^{(l-1)}) = \operatorname{Var}(h^{(l-1)})$. The stability condition $\operatorname{Var}(h^{(l)}) = \operatorname{Var}(h^{(l-1)})$ then implies $n_{l-1} \operatorname{Var}(w) = 1$, or $\operatorname{Var}(w) = \frac{1}{n_{l-1}}$. This is the well-known **Xavier/Glorot initialization**.

For the Rectified Linear Unit (ReLU), $\phi(z) = \max(0,z)$, if we assume the pre-activations $h^{(l-1)}$ are symmetrically distributed around zero, then $\mathbb{E}[(\phi(h^{(l-1)}))^2] = \frac{1}{2}\mathbb{E}[(h^{(l-1)})^2] = \frac{1}{2}\operatorname{Var}(h^{(l-1)})$. The stability condition becomes $n_{l-1} \operatorname{Var}(w) (\frac{1}{2}\operatorname{Var}(h^{(l-1)})) = \operatorname{Var}(h^{(l-1)})$, which simplifies to $n_{l-1} \operatorname{Var}(w) = 2$, or $\operatorname{Var}(w) = \frac{2}{n_{l-1}}$. This is the popular **He initialization** .

#### Backward Propagation and the Edge of Chaos

The same principle of variance preservation applies to the [backward pass](@entry_id:199535). Gradients must propagate from the output layer back to the input layer without exploding or vanishing. We can analyze this by modeling the propagation of the gradient signal. In a simplified model for a deep network with ReLU activations, the variance of the backpropagated signal at layer $l$, denoted $v_l$, relates to the variance at layer $l+1$ by $v_l = \chi v_{l+1}$, where $\chi$ is a scaling factor.

A detailed derivation  shows that for a network of width $n$ with weights initialized with variance $\sigma_w^2/n$, this scaling factor is $\chi = n \cdot \operatorname{Var}(W) \cdot \mathbb{E}[(\phi'(z))^2]$. For ReLU, we found $\mathbb{E}[(\phi'(z))^2] = 1/2$. Thus, $\chi = n \cdot (\sigma_w^2/n) \cdot (1/2) = \frac{\sigma_w^2}{2}$.

For the gradient variance to remain constant ($v_l = v_{l+1}$), we must have $\chi=1$. This requires $\frac{\sigma_w^2}{2} = 1$, or $\sigma_w^2=2$. This corresponds exactly to the He initialization variance (where $\operatorname{Var}(W) = \sigma_w^2/n_{in} = 2/n_{in}$), providing a complementary justification from the perspective of [gradient stability](@entry_id:636837). This critical point, where signals are maintained, is sometimes referred to as the **[edge of chaos](@entry_id:273324)**.

### Understanding and Controlling Stochasticity in Training

The training process itself is inherently stochastic due to the use of mini-batches and, in some cases, stochastic [regularization methods](@entry_id:150559). Statistical moments are crucial for analyzing and controlling this randomness.

#### Stochastic Gradients: Signal, Noise, and Optimization

Stochastic Gradient Descent (SGD) uses a mini-batch gradient $g_B$ as an estimate of the true gradient $\nabla L(\mathbf{w})$. We can decompose this estimator into a **signal** component, its mean $\mathbb{E}[g_B] = \nabla L(\mathbf{w})$, and a **noise** component, captured by its covariance matrix $\operatorname{Cov}(g_B)$.

Averaging is a powerful variance reduction technique. In **gradient accumulation**, we average $K$ consecutive [gradient estimates](@entry_id:189587) to form an update. If the [gradient estimates](@entry_id:189587) $\{g_t\}$ are independent, each with variance $\sigma^2$, the variance of their average $\bar{g}$ is simply $\operatorname{Var}(\bar{g}) = \sigma^2/K$. However, in practice, consecutive mini-batch gradients are often correlated. Assuming an exponentially decaying correlation, $\operatorname{Cov}(g_i, g_j) = \sigma^2 \rho^{|i-j|}$, a more detailed analysis  reveals a more complex reduction in variance. This highlights that while larger batches or accumulation always reduce noise, the exact benefit depends on the statistical dependencies between samples.

The trade-off between [signal and noise](@entry_id:635372) can be formalized using the **gradient signal-to-noise ratio (SNR)**, defined as $S = \frac{\|\mathbb{E}[\mathbf{g}]\|^2}{\operatorname{Tr}(\operatorname{Cov}[\mathbf{g}])}$ . A high SNR indicates a reliable [gradient estimate](@entry_id:200714). Analyzing the one-step progress of SGD for a smooth [loss function](@entry_id:136784) reveals that the optimal [learning rate](@entry_id:140210) $\eta^{\star}$ is directly tied to this SNR:
$$
\eta^{\star} = \frac{1}{L}\,\frac{S}{S+1}
$$
where $L$ is the smoothness constant of the loss. When the SNR is very high ($S \to \infty$), this approaches the deterministic optimum $\eta^\star \to 1/L$. When the noise is overwhelming ($S \to 0$), the optimal learning rate approaches zero. This elegantly shows that the [learning rate](@entry_id:140210) must be attenuated in the presence of noise. Increasing the batch size $B$ reduces the trace of the covariance by a factor of $B$, thus scaling the SNR linearly with $B$ (i.e., $S_B = B \cdot S_1$). This explains why larger batch sizes can often tolerate larger learning rates.

A related concept is the **[gradient noise](@entry_id:165895) scale**, $\mathcal{G} = \frac{\operatorname{Tr}(\Sigma)}{\|\mathbf{g}\|^2}$, where $\Sigma$ is the per-example gradient covariance and $\mathbf{g}$ is the mean gradient . This quantity, which is simply the inverse of the single-sample SNR, represents the effective number of samples at which the magnitude of [gradient noise](@entry_id:165895) equals the magnitude of the signal. It defines a **critical [batch size](@entry_id:174288)** $B_{\text{crit}} = \mathcal{G}$. For batch sizes $B \ll B_{\text{crit}}$, the optimization is noise-dominated, whereas for $B \gg B_{\text{crit}}$, it behaves more deterministically. The optimal learning rate can be expressed in these terms as $\eta^{\star}(B) = \frac{B}{h(B+\mathcal{G})}$, where $h$ is the loss curvature. This framework provides a powerful lens for understanding the interplay between batch size, learning rate, and the statistical properties of the gradient.

#### Stochastic Regularization: The Case of Dropout

**Dropout** is a regularization technique that works by injecting multiplicative noise into the network's activations during training. In **[inverted dropout](@entry_id:636715)**, each activation $a_i$ is multiplied by a random mask variable that is $1/p$ with probability $p$ (the keep probability) and $0$ with probability $1-p$. Let the post-dropout activation be $h_i$.

A statistical analysis  reveals its key properties.
1.  **Preserved Expectation**: The expectation of the post-dropout activation is $\mathbb{E}[h_i] = a_i$. This is a crucial feature, as it means the expected [forward pass](@entry_id:193086) is unchanged, and no modifications are needed at test time (when dropout is turned off).
2.  **Injected Variance**: Dropout introduces variance, a form of noise. The variance of the post-dropout activation is $\operatorname{Var}(h_i) = a_i^2 \frac{1-p}{p}$. This injected noise prevents the network from relying too heavily on any single feature, forcing it to learn more robust representations. The amount of noise is directly controlled by the keep probability $p$.
3.  **Zero Covariance**: If dropout masks are applied independently to different units, the covariance between their post-dropout activations is zero: $\operatorname{Cov}(h_i, h_j) = 0$ for $i \neq j$. This decorrelates the features within a layer, preventing complex co-adaptations and encouraging each unit to learn independently useful features.

### Advanced Applications and Information-Theoretic Perspectives

The concepts of expectation and covariance extend to more advanced topics, providing insight into complex phenomena like oversmoothing in Graph Neural Networks and the geometric foundations of optimization.

#### Covariance in Graph Neural Networks: The Oversmoothing Problem

Graph Neural Networks (GNNs) operate by iteratively aggregating and updating node representations based on a graph structure. This process can be viewed as a form of smoothing, which, if repeated too many times, leads to **oversmoothing**: the embeddings of all nodes in a connected component become indistinguishable.

We can analyze this phenomenon by tracking the covariance of node [embeddings](@entry_id:158103). Consider a simple two-node graph where [embeddings](@entry_id:158103) are updated via a combination of a residual connection and [message passing](@entry_id:276725). Let the initial embeddings be independent with variance $\sigma^2$. After $l$ layers, the covariance between the embeddings of the two nodes, $h_1^{(l)}$ and $h_2^{(l)}$, can be derived as :
$$
\operatorname{Cov}(h_{1}^{(l)}, h_{2}^{(l)}) = \frac{\sigma^{2}}{2} (1 - \alpha^{2l})
$$
where $\alpha \in (0,1)$ is a parameter from the residual connection. As the number of layers $l$ grows, $\alpha^{2l} \to 0$, and the covariance approaches $\frac{\sigma^2}{2}$. Simultaneously, the variance of each embedding, $\operatorname{Var}(h_i^{(l)}) = \frac{\sigma^2}{2}(1+\alpha^{2l})$, also converges to $\frac{\sigma^2}{2}$. As the covariance converges to the variance, the correlation coefficient between the two embeddings approaches $1$. This implies that the [embeddings](@entry_id:158103) become linearly dependent and, since they are zero-mean, effectively identical. The variance of their difference, $\operatorname{Var}(h_1^{(l)} - h_2^{(l)})$, converges to zero, rigorously demonstrating that the nodes have become indistinguishable.

#### The Fisher Information Matrix: Covariance and Geometry

In probabilistic models parameterized by $\theta$, such as those used for classification, the **[score function](@entry_id:164520)** is defined as the gradient of the log-likelihood with respect to the parameters: $s(y, x; \theta) = \nabla_{\theta} \log p(y \mid x, \theta)$. Under standard regularity conditions, the [score function](@entry_id:164520) has an expectation of zero when averaged over the model's predictions .

This has a profound consequence. The **Fisher Information Matrix (FIM)**, $F(\theta)$, is defined as the expected [outer product](@entry_id:201262) of the score, $F(\theta) = \mathbb{E}[s s^T]$. Because the score has [zero mean](@entry_id:271600), this is precisely the definition of the **covariance matrix of the [score function](@entry_id:164520)**.
$$
F(\theta) = \operatorname{Cov}(s(y, x; \theta))
$$
The FIM thus measures the variability of the gradient of the log-likelihood. A large eigenvalue of the FIM indicates a direction in [parameter space](@entry_id:178581) where the [log-likelihood](@entry_id:273783) is highly sensitive to parameter changes, corresponding to high curvature in the space of probability distributions.

This insight is the foundation of the **Natural Gradient** algorithm, which preconditions the standard gradient with the inverse of the FIM: $\Delta \theta \propto -F(\theta)^{-1} \nabla L(\theta)$. This update rule is invariant to reparameterizations of the model, a desirable property not held by standard SGD. This invariance arises because the FIM transforms as a Riemannian metric tensor, providing a bridge between the statistical concept of covariance and the geometric structure of the learning problem . Using the covariance of the score to precondition the gradient allows the optimizer to navigate the landscape of probability distributions in a more principled manner.