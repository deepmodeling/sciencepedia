## Introduction
Restricted Boltzmann Machines (RBMs) are a foundational class of generative, energy-based neural networks that played a crucial role in the resurgence of deep learning. Their unique ability to learn a probability distribution over a set of inputs without supervision makes them a powerful tool for unsupervised [feature learning](@entry_id:749268) and [density estimation](@entry_id:634063). Despite their simple architecture, understanding the principles that govern their behavior—from the statistical mechanics-inspired energy function to the intricacies of the Contrastive Divergence training algorithm—presents a significant learning curve. This article aims to demystify the RBM, providing a clear and structured exploration of its core concepts and practical utility.

Over the next three chapters, you will build a comprehensive understanding of this versatile model. We will begin in "**Principles and Mechanisms**" by dissecting the mathematical framework of RBMs, deriving key quantities like free energy, and exploring the Contrastive Divergence algorithm that makes them trainable. Next, the "**Applications and Interdisciplinary Connections**" chapter will showcase the RBM's real-world impact, surveying its use in tasks from collaborative filtering and [anomaly detection](@entry_id:634040) to its surprising connections with fields like quantum physics and psychometrics. Finally, "**Hands-On Practices**" will offer practical exercises to solidify your knowledge and test your understanding of these concepts.

## Principles and Mechanisms

Following our introduction to the Restricted Boltzmann Machine (RBM) as a generative [energy-based model](@entry_id:637362), this chapter delves into the fundamental principles and mechanisms that govern its behavior and learning. We will dissect the mathematical framework of RBMs, starting from the energy function, deriving key quantities like the free energy, and exploring the conditional distributions that are the cornerstone of its operation. We will then examine how RBMs are trained using Contrastive Divergence and investigate the practical challenges and advanced concepts that are crucial for their successful application.

### The Energy-Based Formulation

At the heart of any Boltzmann machine lies the concept of an **energy function**, denoted by $E(\mathbf{v}, \mathbf{h})$, which assigns a scalar energy value to every possible joint configuration of the visible units $\mathbf{v}$ and hidden units $\mathbf{h}$. For a standard RBM with binary visible units $\mathbf{v} \in \{0,1\}^{n_v}$ and binary hidden units $\mathbf{h} \in \{0,1\}^{n_h}$, the energy function is defined as a linear model with a bilinear interaction term:

$E(\mathbf{v}, \mathbf{h}) = - \mathbf{b}^{\top} \mathbf{v} - \mathbf{c}^{\top} \mathbf{h} - \mathbf{v}^{\top} \mathbf{W} \mathbf{h}$

Here, $\mathbf{b} \in \mathbb{R}^{n_v}$ represents the biases of the visible units, $\mathbf{c} \in \mathbb{R}^{n_h}$ represents the biases of the hidden units, and $\mathbf{W} \in \mathbb{R}^{n_v \times n_h}$ is the matrix of weights connecting the visible and hidden units. The negative signs are conventional, implying that configurations where aligned units are active have lower energy.

The energy of a state is converted into a probability via the **Boltzmann distribution** (or Gibbs distribution) from statistical physics:

$p(\mathbf{v}, \mathbf{h}) = \frac{1}{Z} \exp(-E(\mathbf{v}, \mathbf{h}))$

This formula states that the probability of a configuration is exponentially proportional to the negative of its energy. Lower energy states are thus more probable. The [normalizing constant](@entry_id:752675), $Z$, is known as the **partition function**. It is the sum of the unnormalized probabilities over all possible configurations of visible and hidden units:

$Z = \sum_{\mathbf{v}, \mathbf{h}} \exp(-E(\mathbf{v}, \mathbf{h}))$

The partition function ensures that the probability distribution sums to one. However, computing $Z$ directly is intractable for all but the smallest models, as it requires summing over $2^{n_v} \times 2^{n_h}$ states. This intractability is a central challenge in training and using RBMs.

### The Free Energy Landscape

While the joint distribution $p(\mathbf{v}, \mathbf{h})$ is our starting point, we are ultimately interested in the model's ability to represent the distribution of the data, which corresponds to the [marginal probability](@entry_id:201078) of the visible units, $p(\mathbf{v})$. We obtain this by summing (or "marginalizing out") the hidden units:

$p(\mathbf{v}) = \sum_{\mathbf{h}} p(\mathbf{v}, \mathbf{h}) = \frac{1}{Z} \sum_{\mathbf{h}} \exp(-E(\mathbf{v}, \mathbf{h}))$

This expression introduces a crucial concept: the **free energy** of a visible configuration $\mathbf{v}$, denoted $F(\mathbf{v})$. It is defined as:

$F(\mathbf{v}) = -\ln \sum_{\mathbf{h}} \exp(-E(\mathbf{v}, \mathbf{h}))$

The term $\exp(-F(\mathbf{v}))$ neatly encapsulates the summation over all hidden configurations for a given $\mathbf{v}$. This allows us to express the [marginal probability](@entry_id:201078) in a more elegant form:

$p(\mathbf{v}) = \frac{\exp(-F(\mathbf{v}))}{Z}$

This equation provides a profound insight: the RBM defines a probability distribution over the visible data where the probability of a configuration $\mathbf{v}$ is exponentially related to the negative of its free energy. The learning process can thus be re-framed as adjusting the model parameters $(\mathbf{W}, \mathbf{b}, \mathbf{c})$ to shape the **[free energy landscape](@entry_id:141316)**, assigning low free energy (high probability) to data-like configurations and high free energy (low probability) to all other configurations.

A remarkable feature of the RBM's bipartite structure is that the free energy, unlike the partition function, can be computed analytically. Let us derive this [closed-form expression](@entry_id:267458)  .

Starting with the definition of $F(\mathbf{v})$ and substituting the energy function:
$F(\mathbf{v}) = -\ln \sum_{\mathbf{h}} \exp(\mathbf{b}^{\top}\mathbf{v} + \mathbf{c}^{\top}\mathbf{h} + \mathbf{v}^{\top}\mathbf{W}\mathbf{h})$

Since $\mathbf{b}^{\top}\mathbf{v}$ does not depend on $\mathbf{h}$, we can factor it out of the summation:
$F(\mathbf{v}) = -\mathbf{b}^{\top}\mathbf{v} - \ln \sum_{\mathbf{h} \in \{0,1\}^{n_h}} \exp\left( \sum_{j=1}^{n_h} h_j c_j + \sum_{j=1}^{n_h} \sum_{i=1}^{n_v} v_i W_{ij} h_j \right)$
$F(\mathbf{v}) = -\mathbf{b}^{\top}\mathbf{v} - \ln \sum_{\mathbf{h}} \exp\left( \sum_{j=1}^{n_h} h_j \left(c_j + \sum_{i=1}^{n_v} v_i W_{ij}\right) \right)$

Because there are no connections between hidden units, the sum over all $2^{n_h}$ hidden vectors $\mathbf{h}$ factorizes into a [product of sums](@entry_id:173171) for each individual hidden unit $h_j$:
$\sum_{\mathbf{h}} \exp(\dots) = \prod_{j=1}^{n_h} \sum_{h_j \in \{0,1\}} \exp\left(h_j \left(c_j + \sum_{i=1}^{n_v} v_i W_{ij}\right)\right)$

For each binary unit $h_j$, the inner sum is simple:
$\sum_{h_j \in \{0,1\}} \exp(\dots) = \exp(0) + \exp\left(c_j + \sum_{i=1}^{n_v} v_i W_{ij}\right) = 1 + \exp\left(c_j + \mathbf{v}^{\top}\mathbf{W}_{:,j}\right)$
where $\mathbf{W}_{:,j}$ is the $j$-th column of $\mathbf{W}$.

Substituting this back and using the property that $\ln(\prod x_j) = \sum \ln(x_j)$, we arrive at the final analytical expression for the free energy:

$F(\mathbf{v}) = -\sum_{i=1}^{n_v} b_i v_i - \sum_{j=1}^{n_h} \ln\left(1 + \exp\left(c_j + \sum_{i=1}^{n_v} v_i W_{ij}\right)\right)$

This tractable expression is fundamental to both understanding and training RBMs.

To make this concrete, let's compute the free energy for a tiny RBM with $n_v=2$, $n_h=1$ and a specific configuration $\mathbf{v}=(1,1)$ . Let the parameters be:
$b = \begin{pmatrix} \ln 2 \\ -\ln 3 \end{pmatrix}$, $c = (\ln 5)$, and $W = \begin{pmatrix} \ln 7 \\ -\ln 11 \end{pmatrix}$.

Using the formula with $\mathbf{v}=(1,1)$:
$F(1,1) = -(1 \cdot b_1 + 1 \cdot b_2) - \ln(1 + \exp(c_1 + 1 \cdot W_{11} + 1 \cdot W_{21}))$
$F(1,1) = -(\ln 2 - \ln 3) - \ln(1 + \exp(\ln 5 + \ln 7 - \ln 11))$
$F(1,1) = -(\ln(2/3)) - \ln(1 + \exp(\ln(35/11)))$
$F(1,1) = \ln(3/2) - \ln(1 + 35/11) = \ln(3/2) - \ln(46/11)$
$F(1,1) = \ln\left(\frac{3/2}{46/11}\right) = \ln\left(\frac{33}{92}\right)$
This exact calculation demonstrates the tangible nature of the free energy concept.

### Conditional Distributions and Gibbs Sampling

The defining architectural feature of an RBM is its **[bipartite graph](@entry_id:153947) structure**: connections exist only between the visible and hidden layers, not within them. This gives rise to a powerful property: **[conditional independence](@entry_id:262650)**.

1.  Given a visible vector $\mathbf{v}$, the hidden units are mutually independent.
2.  Given a hidden vector $\mathbf{h}$, the visible units are mutually independent.

This allows us to derive simple, factorized expressions for the conditional distributions $p(\mathbf{h}|\mathbf{v})$ and $p(\mathbf{v}|\mathbf{h})$.

For a binary-binary RBM, the probability of a single hidden unit $h_j$ being active (equal to 1) given a visible vector $\mathbf{v}$ is:

$p(h_j = 1 | \mathbf{v}) = \sigma\left(c_j + \sum_{i=1}^{n_v} v_i W_{ij}\right) = \sigma(c_j + \mathbf{v}^{\top}\mathbf{W}_{:,j})$

where $\sigma(x) = \frac{1}{1 + \exp(-x)}$ is the **[logistic sigmoid function](@entry_id:146135)**. This arises directly from the terms in the energy function involving $h_j$. Similarly, the probability of a single visible unit $v_i$ being active given a hidden vector $\mathbf{h}$ is:

$p(v_i = 1 | \mathbf{h}) = \sigma\left(b_i + \sum_{j=1}^{n_h} W_{ij} h_j\right) = \sigma(b_i + \mathbf{W}_{i,:}\mathbf{h})$

where $\mathbf{W}_{i,:}$ is the $i$-th row of $\mathbf{W}$.

These simple, local computation rules are the workhorse of the RBM. They allow for efficient **Gibbs sampling**, an iterative process used to generate samples from the model's joint distribution. Starting from an arbitrary state (e.g., a data point $\mathbf{v}^{(0)}$), we can alternate between sampling all hidden units in parallel given the visibles, and then all visible units in parallel given the hiddens:

1.  For each hidden unit $j$, sample $h_j^{(t)} \sim p(h_j | \mathbf{v}^{(t)})$.
2.  For each visible unit $i$, sample $v_i^{(t+1)} \sim p(v_i | \mathbf{h}^{(t)})$.

Repeating this process constitutes a Markov chain whose stationary distribution is the RBM's [joint distribution](@entry_id:204390) $p(\mathbf{v}, \mathbf{h})$.

### Variants of the RBM Architecture

The basic binary-binary RBM can be adapted to model different types of data by changing the nature of the units and their corresponding energy terms.

#### Gaussian-Bernoulli RBMs for Real-Valued Data

To model real-valued data, such as pixel intensities in images, we can replace the binary visible units with continuous, Gaussian units. A common energy function for a **Gaussian-Bernoulli RBM** is :

$E(\mathbf{v}, \mathbf{h}) = \sum_{i=1}^{n_v} \frac{(v_i - b_i)^2}{2\sigma_i^2} - \sum_{j=1}^{n_h} c_j h_j - \sum_{i=1}^{n_v} \sum_{j=1}^{n_h} \frac{v_i}{\sigma_i^2} W_{ij} h_j$

Here, each visible unit $v_i$ has its own variance $\sigma_i^2$. For simplicity, we often assume an isotropic variance, $\sigma_i^2 = \sigma^2$ for all $i$.

The conditional distributions change accordingly. The hidden unit conditional $p(h_j=1|\mathbf{v})$ remains a sigmoid, but now with a scaled input:

$p(h_j = 1 | \mathbf{v}) = \sigma\left(c_j + \frac{1}{\sigma^2} \mathbf{v}^{\top}\mathbf{W}_{:,j}\right)$

The visible unit conditional $p(\mathbf{v}|\mathbf{h})$ becomes a multivariate Gaussian distribution. Completing the square in the energy function reveals its mean and covariance:

$p(\mathbf{v} | \mathbf{h}) = \mathcal{N}(\mathbf{v} | \boldsymbol{\mu} = \mathbf{b} + \mathbf{W}\mathbf{h}, \boldsymbol{\Sigma} = \sigma^2 \mathbf{I})$

The mean of the reconstructed visible vector is the bias plus the weighted sum of hidden activations. The variance parameter $\sigma^2$ plays a critical role in training stability. From the conditional probabilities, we see that gradients with respect to the weights will scale with $1/\sigma^2$. A very small $\sigma^2$ can lead to [exploding gradients](@entry_id:635825) and learning instability, while a very large $\sigma^2$ can cause [vanishing gradients](@entry_id:637735) and training stagnation. A common and effective practice is to standardize the visible data to have approximately [zero mean](@entry_id:271600) and unit variance, and then fix $\sigma^2=1$, thereby matching the model's scale to the data's scale and improving the conditioning of the optimization problem .

#### RBMs with ReLU Hidden Units for Count Data

For non-negative data that can be unbounded, such as word counts in a document, binary hidden units are inefficient. A binary unit can only encode presence (1) or absence (0) of a feature. To model a count of $N$, one might need $N$ separate binary units. A more powerful alternative is to use hidden units whose activation can be any non-negative real value, such as a **Rectified Linear Unit (ReLU)**.

An RBM with ReLU-like hidden units (specifically, rectified Gaussian units) can be defined with the following energy function, where $h_j \ge 0$ :

$E(\mathbf{v}, \mathbf{h}) = -\mathbf{b}^{\top}\mathbf{v} - \mathbf{c}^{\top}\mathbf{h} - \mathbf{v}^{\top}\mathbf{W}\mathbf{h} + \frac{1}{2}\sum_{j=1}^{M} h_{j}^{2}$

The quadratic term $\frac{1}{2}h_j^2$ acts as a regularizer. The conditional distribution for a hidden unit $h_j$ given $\mathbf{v}$ is derived by examining the terms in the exponent of $p(h_j|\mathbf{v})$:

$\exp\left( -(\frac{1}{2}h_j^2 - (c_j + \mathbf{v}^{\top}\mathbf{W}_{:,j})h_j) \right) \propto \exp\left( -\frac{1}{2}(h_j - (c_j + \mathbf{v}^{\top}\mathbf{W}_{:,j}))^2 \right)$

This is the kernel of a Gaussian distribution with mean $\mu_j = c_j + \mathbf{v}^{\top}\mathbf{W}_{:,j}$ and unit variance. Combined with the constraint $h_j \ge 0$, the [conditional distribution](@entry_id:138367) $p(h_j|\mathbf{v})$ becomes a **rectified Gaussian**: a normal distribution $\mathcal{N}(\mu_j, 1)$ truncated to the non-negative real line $[0, \infty)$.

The key advantage of this architecture is its enhanced [representational capacity](@entry_id:636759). A single ReLU hidden unit can encode the multiplicity or intensity of a feature by scaling its activation. A larger input drive from the visible units results in a larger expected activation, allowing the model to efficiently represent count-like data without needing to duplicate features .

### Learning: Sculpting the Energy Landscape

Training an RBM means adjusting its parameters $\theta = \{\mathbf{W}, \mathbf{b}, \mathbf{c}\}$ to maximize the [log-likelihood](@entry_id:273783) of the observed data. The gradient of the log-likelihood for a single data sample $\mathbf{v}$ with respect to a parameter $\phi \in \theta$ has a remarkably elegant structure:

$\frac{\partial \ln p(\mathbf{v})}{\partial \phi} = -\frac{\partial F(\mathbf{v})}{\partial \phi} - \frac{\partial \ln Z}{\partial \phi}$

It can be shown that these two terms correspond to expectations:

$\frac{\partial \ln p(\mathbf{v})}{\partial \phi} = \mathbb{E}_{p(\mathbf{h}|\mathbf{v})} \left[-\frac{\partial E(\mathbf{v},\mathbf{h})}{\partial \phi}\right] - \mathbb{E}_{p(\mathbf{v}',\mathbf{h}')} \left[-\frac{\partial E(\mathbf{v}',\mathbf{h}')}{\partial \phi}\right]$

Let's look at the gradient for a single weight $W_{ij}$:
$\frac{\partial \ln p(\mathbf{v})}{\partial W_{ij}} = \mathbb{E}_{p(\mathbf{h}|\mathbf{v})} [v_i h_j] - \mathbb{E}_{p(\mathbf{v}',\mathbf{h}')} [v'_i h'_j]$

The update rule for gradient ascent is thus proportional to a difference between two terms:
1.  The **positive phase**: $\mathbb{E}_{p(\mathbf{h}|\mathbf{v})} [v_i h_j] = v_i \cdot p(h_j=1|\mathbf{v})$. This is the expectation of the unit co-activation, with the visible units clamped to a data point $\mathbf{v}$.
2.  The **negative phase**: $\mathbb{E}_{p(\mathbf{v}',\mathbf{h}')} [v'_i h'_j]$. This is the same expectation, but taken over the model's [equilibrium distribution](@entry_id:263943).

The positive phase is easy to compute. The negative phase is intractable because it requires generating samples from the model's [equilibrium distribution](@entry_id:263943), which is computationally expensive.

#### Contrastive Divergence (CD) Learning

**Contrastive Divergence (CD)**, introduced by Geoffrey Hinton, is a clever approximation that makes RBM training practical. Instead of running the Gibbs sampler until it reaches equilibrium for the negative phase, CD runs it for only a small number of steps, $k$. Typically, $k=1$ (CD-1) is used. The chain is initialized with a data sample $\mathbf{v}^{(0)}$. After $k$ steps of Gibbs sampling, we get a "fantasy" particle $\mathbf{v}^{(k)}$. The update rule is then approximated as:

$\Delta W_{ij} \propto v_i^{(0)} p(h_j=1|\mathbf{v}^{(0)}) - v_i^{(k)} p(h_j=1|\mathbf{v}^{(k)})$

This has a powerful geometric and biological interpretation  .
*   **Geometric Interpretation**: The positive phase term acts to increase the probability of the data by decreasing its free energy $F(\mathbf{v})$. Geometrically, this is like "carving down" the energy landscape at the location of the data sample. The negative phase term does the opposite: it increases the free energy at the location of the fantasy particle, "pushing up" on the energy landscape where the model currently generates samples. This prevents the energy wells from becoming infinitely deep and sharp, forcing the model to spread its probability mass.
*   **Biological Interpretation**: The update rule resembles Hebbian learning. The positive phase is **Hebbian**: "neurons that fire together (driven by data), wire together." The term increases the weight between co-active units. The negative phase is **anti-Hebbian**: "neurons that fire together (due to internal fantasy), unwire." This term decreases the weights for correlations that the model generates on its own. This creates a competitive dynamic, forcing the model's features to explain correlations in the external data rather than indulging in runaway self-reinforcement .

#### Challenges in CD Training: Mixing and Mode Collapse

While powerful, the CD-1 approximation has a significant weakness: its Gibbs chain may not **mix** well. If the true data distribution has multiple modes that are far apart in the state space (e.g., have a large Hamming distance), a 1-step Gibbs chain started at one mode is highly unlikely to generate a sample near another mode.

Consider a synthetic dataset with two modes, $\mathbf{v}^{(A)} = [1,1,1,0,0,0]$ and $\mathbf{v}^{(B)} = [0,0,0,1,1,1]$ . If the model is trained primarily on $\mathbf{v}^{(A)}$, the energy landscape will develop a deep well there. When a sample of $\mathbf{v}^{(B)}$ is finally presented, the negative phase particle started from $\mathbf{v}^{(B)}$ will likely be reconstructed back to a state close to $\mathbf{v}^{(A)}$, because that's where the model's probability mass is concentrated. The learning rule will then incorrectly try to increase the energy of a sample that is far from the true mode $\mathbf{v}^{(B)}$, potentially preventing the model from ever learning the second mode.

Two common solutions to this mixing problem are:
1.  **CD-k**: Increase the number of Gibbs sampling steps $k$ (e.g., to $k=10$). This gives the chain more time to move between modes, providing a better approximation of the true negative phase expectation.
2.  **Persistent Contrastive Divergence (PCD)**: Instead of re-initializing the Gibbs chain from a data point at every step, PCD maintains a persistent set of "fantasy particles" that are updated at each step. These chains are not tied to the current data point and can explore the energy landscape more freely, leading to better mixing and a more accurate estimate of the model distribution .

### Advanced Topics and Practical Considerations

#### The Vanishing Gradient Problem

A common failure mode in training RBMs is the **[vanishing gradient problem](@entry_id:144098)**, where learning stalls because the parameter gradients become negligible. In RBMs, this is often caused by the saturation of the sigmoid [activation functions](@entry_id:141784). The derivative of the sigmoid, $\sigma'(x) = \sigma(x)(1-\sigma(x))$, is maximal at $x=0$ and approaches zero as $|x|$ becomes large.

The pre-activation for a hidden unit $j$ is $x_j = c_j + \mathbf{v}^{\top}\mathbf{W}_{:,j}$. If the weights or biases grow too large during training, $|x_j|$ can become large for most data points $\mathbf{v}$, causing $\sigma'(x_j)$ to be near zero. Since the weight gradients are proportional to this derivative, learning grinds to a halt. One can derive the precise condition for saturation. For a small threshold $\varepsilon > 0$, the gradient becomes negligible ($\sigma'(x_j) \le \varepsilon$) when :

$|x_j| \ge \operatorname{arcosh}\left(\frac{1}{2\varepsilon} - 1\right)$

Several techniques can mitigate this:
*   **Weight Constraints**: Penalizing large weights using $\ell_2$ regularization ([weight decay](@entry_id:635934)) or explicitly clipping weights to a maximum value prevents them from growing uncontrollably.
*   **Temperature Scaling**: Using a "softened" sigmoid $\sigma_T(x) = \sigma(x/T)$ with a temperature $T > 1$ widens the effective linear region of the [activation function](@entry_id:637841), making it less likely to saturate for a given pre-activation value.
*   **Data Centering**: For real-valued visible units, centering the data (subtracting the mean) can help keep the average pre-activation closer to zero, where the sigmoid gradient is maximal .

A related problem is that of "stuck" or **dead units** . If a hidden bias $c_j$ becomes very large and positive, $p(h_j=1|\mathbf{v})$ will approach 1 for all inputs $\mathbf{v}$. The unit becomes permanently active and loses its ability to function as a feature detector. Similarly, a large negative bias will cause the unit to be permanently off. To prevent this, one can add a penalty to the objective function that encourages the average activation of each hidden unit over the dataset to stay within a target range (e.g., a sparsity target).

#### Symmetries and Model Identifiability

RBMs possess certain **symmetries** or **gauge freedoms**, meaning that multiple distinct parameter settings can produce the exact same [marginal distribution](@entry_id:264862) $p(\mathbf{v})$. This is a lack of **identifiability**.

For example, consider flipping the sign of all weights and the bias connected to a single hidden unit $j$: $W_{ij} \to -W_{ij}$ for all $i$, and $c_j \to -c_j$. This is equivalent to relabeling the hidden state $h_j$ as $1-h_j$. This transformation alone changes the distribution. However, if we also modify the visible biases according to $b_i \to b_i + W_{ij}$, the [marginal distribution](@entry_id:264862) $p(\mathbf{v})$ is provably invariant .

Since this flip can be done independently for each of the $n_h$ hidden units, there are at least $2^{n_h}$ distinct parameter configurations that result in the same observable model behavior. While this does not typically affect the model's generative performance, it is an important theoretical property to recognize, as it implies that interpreting individual learned weights can be ambiguous without fixing a "gauge" or [canonical representation](@entry_id:146693).

#### Beyond Gibbs Sampling: Metropolis-Hastings

While Gibbs sampling is the standard method for RBMs, it is just one type of Markov Chain Monte Carlo (MCMC) algorithm. The more general **Metropolis-Hastings (MH)** algorithm can also be used. In MH, one uses a proposal distribution $q(\mathbf{h}'|\mathbf{h})$ to suggest a new state, and then accepts or rejects this proposal with a specific probability designed to ensure the chain converges to the [target distribution](@entry_id:634522).

For an RBM, we could design a proposal that flips a subset of hidden units simultaneously. If the proposal mechanism is symmetric (i.e., the probability of proposing to flip a set $S$ is the same regardless of the current state), the acceptance probability for a move from $\mathbf{h}$ to $\mathbf{h}'$ simplifies to :

$\alpha(\mathbf{h} \to \mathbf{h}') = \min\left\{1, \exp(-\Delta E)\right\}$

where $\Delta E = E(\mathbf{v}, \mathbf{h}') - E(\mathbf{v}, \mathbf{h})$ is the change in energy. Due to the RBM's structure, this energy change is simply the sum of energy changes for each individual flipped unit. If a proposed move leads to a lower energy state ($\Delta E  0$), it is always accepted. If it leads to a higher energy state, it is accepted with a probability that decreases exponentially with the energy increase. This provides a flexible framework for exploring more complex or efficient sampling schemes beyond single-site Gibbs updates.