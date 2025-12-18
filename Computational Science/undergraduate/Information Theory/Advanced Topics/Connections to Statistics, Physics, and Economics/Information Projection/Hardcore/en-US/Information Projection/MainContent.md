## Introduction
In [scientific modeling](@entry_id:171987) and data analysis, a central challenge is updating our knowledge in a logically consistent manner as new evidence emerges. We often start with a prior model of the world, expressed as a probability distribution, and must then refine it to incorporate new observations or constraints. The question is: how do we select the best possible updated model without introducing extraneous assumptions? Information Projection provides a rigorous and powerful answer to this fundamental problem. It is a framework rooted in information theory that formalizes the process of [belief updating](@entry_id:266192) based on the principle of minimum discrimination information.

This article provides a comprehensive exploration of Information Projection, designed to take you from its theoretical foundations to its practical applications. Across three chapters, you will gain a deep understanding of this versatile tool. The first chapter, "Principles and Mechanisms," will unpack the core mathematical concepts, including the Kullback-Leibler divergence, the geometric properties of projections, and the connection to the [principle of maximum entropy](@entry_id:142702). Next, "Applications and Interdisciplinary Connections" will demonstrate the remarkable utility of I-projection across fields such as machine learning, statistical physics, and engineering, showing how it solves real-world problems. Finally, "Hands-On Practices" will provide guided exercises to help you apply these concepts and solidify your knowledge. Let us begin by examining the core principles that make Information Projection such an elegant and essential tool for modern science.

## Principles and Mechanisms

The process of scientific inquiry and [statistical modeling](@entry_id:272466) often involves refining our understanding in light of new evidence. We begin with a prior model of a system, represented by a probability distribution, and subsequently acquire new information in the form of constraints or observations. The fundamental challenge is to update our prior belief to a new distribution that both respects the new information and is minimally perturbed from our original model. This chapter explores the principles and mechanisms of **information projection**, a powerful framework for performing such updates in a logically consistent and mathematically rigorous manner.

### The Principle of Minimum Discrimination Information

Imagine we have a prior probability distribution $q(x)$ over a set of outcomes $\mathcal{X}$. This distribution represents our best knowledge about a system before new evidence is available. Subsequently, we learn that the true distribution $p(x)$ must belong to a specific set of distributions $\mathcal{C}$, which represents our new constraints. For instance, an experiment might reveal the precise average value of some observable quantity, thereby restricting the set of valid models.

How do we select a single distribution $p(x)$ from the set $\mathcal{C}$? The **principle of minimum discrimination information** provides a compelling answer. It postulates that we should choose the distribution $p(x)$ that is "closest" to our prior $q(x)$, thereby incorporating the new constraints while introducing the minimum amount of additional, unsupported information. To quantify this "closeness," we employ the **Kullback-Leibler (KL) divergence**, or [relative entropy](@entry_id:263920).

The KL divergence from a [prior distribution](@entry_id:141376) $q$ to a [posterior distribution](@entry_id:145605) $p$ is defined as:

$$
D(p||q) = \sum_{x \in \mathcal{X}} p(x) \ln\left(\frac{p(x)}{q(x)}\right)
$$

This quantity measures the [information gain](@entry_id:262008), in nats, when one revises one's beliefs from the [prior distribution](@entry_id:141376) $q$ to the [posterior distribution](@entry_id:145605) $p$. The principle of minimum discrimination information thus directs us to solve the following optimization problem:

$$
p^* = \arg\min_{p \in \mathcal{C}} D(p||q)
$$

The resulting distribution $p^*$ is known as the **information projection**, or **I-projection**, of the prior distribution $q$ onto the constraint set $\mathcal{C}$.

### Fundamental Properties of the Information Projection

The KL divergence is not a true distance metric, as it is asymmetric ($D(p||q) \neq D(q||p)$) and does not satisfy the triangle inequality. However, the projection operation it defines possesses elegant geometric properties, particularly when the constraint set $\mathcal{C}$ is convex. A set of distributions is **convex** if for any two distributions $p_1, p_2 \in \mathcal{C}$, their mixture $p_\lambda = \lambda p_1 + (1-\lambda) p_2$ for any $\lambda \in [0,1]$ is also in $\mathcal{C}$.

#### Uniqueness

For a convex constraint set $\mathcal{C}$, the I-projection $p^*$ is unique. This can be proven by considering the [strict convexity](@entry_id:193965) of the KL divergence. The function $f(p) = D(p||q)$ is a strictly [convex function](@entry_id:143191) of the distribution $p$. If we assume, for the sake of contradiction, that two distinct distributions $p_1$ and $p_2$ in $\mathcal{C}$ both achieve the minimum divergence value $d_{min}$, their mixture $p_{mix} = \frac{1}{2}p_1 + \frac{1}{2}p_2$ would also be in $\mathcal{C}$ due to [convexity](@entry_id:138568). By the property of strictly [convex functions](@entry_id:143075), we would have:

$$
D(p_{mix}||q) \lt \frac{1}{2}D(p_1||q) + \frac{1}{2}D(p_2||q) = d_{min}
$$

This result, where the [mixture distribution](@entry_id:172890) has a strictly lower divergence than the supposed minimum, is a contradiction. Therefore, the minimizer must be unique . This uniqueness is critical, as it guarantees a single, unambiguous answer to our inference problem.

#### The Pythagorean Theorem

The I-projection exhibits a remarkable geometric property analogous to the Pythagorean theorem in Euclidean space. For a prior distribution $q$, its I-projection $p^*$ onto a convex set $\mathcal{C}$, and any other distribution $r \in \mathcal{C}$, the following inequality holds:

$$
D(r||q) \ge D(r||p^*) + D(p^*||q)
$$

This relationship is known as the **generalized Pythagorean theorem** for information projections. It establishes a "right-angle" relationship where the information divergence from any point in the set to the prior is at least the sum of the divergences along the path through the projection.

Crucially, when the constraint set $\mathcal{C}$ is not just convex but is an **affine set**—a set defined by linear constraints of the form $\sum_x p(x) T_i(x) = c_i$—this inequality becomes an exact equality:

$$
D(r||q) = D(r||p^*) + D(p^*||q)
$$

This identity reveals the profound structure of information projections. It implies that the process of projecting onto $\mathcal{C}$ decomposes the total divergence into two orthogonal components: the divergence from the projection to the prior, $D(p^*||q)$, and the divergence from any other point in the set to the projection, $D(r||p^*)$. As demonstrated in a specific numerical instance , the "inequality gap" in such cases is precisely zero, confirming the exactness of the Pythagorean identity.

### Calculating the I-Projection

The most common and practical applications of information projection involve constraint sets $\mathcal{C}$ defined by a collection of known [expectation values](@entry_id:153208). That is, $\mathcal{C}$ is the set of all probability distributions $p$ for which the expectations of certain functions (observables) $T_1(x), \dots, T_k(x)$ match experimentally determined values $\mu_1, \dots, \mu_k$:

$$
\mathcal{C} = \left\{ p \mid \sum_{x \in \mathcal{X}} p(x) = 1, p(x) \ge 0, \text{ and } \sum_{x \in \mathcal{X}} p(x) T_i(x) = \mu_i \text{ for } i=1, \dots, k \right\}
$$

To find the I-projection of a prior $q$ onto such a set, we use the method of Lagrange multipliers. The solution $p^*$ that minimizes $D(p||q)$ is found to have a characteristic exponential form:

$$
p^*(x) = \frac{1}{Z(\lambda)} q(x) \exp\left( \sum_{i=1}^k \lambda_i T_i(x) \right)
$$

Here, the $\lambda_i$ are Lagrange multipliers chosen to satisfy the constraints, and $Z(\lambda) = \sum_x q(x) \exp(\sum_i \lambda_i T_i(x))$ is the [normalization constant](@entry_id:190182), or partition function. This solution reveals that the updated distribution is a multiplicative "tilting" of the prior distribution $q(x)$.

#### The Principle of Maximum Entropy

A particularly important special case arises when we have no prior knowledge to prefer any outcome over another. In this scenario, we adopt a **uniform prior**, $q(x) = 1/|\mathcal{X}|$. Minimizing the KL divergence $D(p||q)$ under these conditions becomes:

$$
\min_p \sum_x p(x) \ln\left(\frac{p(x)}{1/|\mathcal{X}|}\right) = \min_p \left( \sum_x p(x) \ln p(x) + \ln|\mathcal{X}| \right)
$$

Since $\ln|\mathcal{X}|$ is a constant, this is equivalent to minimizing $\sum_x p(x) \ln p(x)$, which is the same as maximizing the **Shannon entropy**, $H(p) = -\sum_x p(x) \ln p(x)$. Thus, the I-projection from a uniform prior is equivalent to finding the distribution with the maximum possible entropy that satisfies the given constraints. This is the celebrated **[principle of maximum entropy](@entry_id:142702)**.

For example, consider a quantum system with three energy levels ($E_0=0, E_1=\epsilon, E_2=2\epsilon$) for which our [prior belief](@entry_id:264565) is uniform, $q = \{1/3, 1/3, 1/3\}$. If an experiment reveals the average energy to be $\langle E \rangle = 1.2\epsilon$, the maximum entropy principle (or, equivalently, minimizing $D(p||q)$) yields a new distribution of the form $p_i \propto \exp(-\beta E_i)$, known as the Gibbs distribution. By solving for the parameter $\beta$ that enforces the energy constraint, we can find the explicit updated probabilities for each state .

Similarly, if a classifier must assign probabilities to 26 categories, subject to the constraint that a specific subset of 5 categories must have a total probability of $0.4$, the maximum entropy distribution will assign uniform probability within each partition. All probabilities within the 5-category group will be equal ($0.4/5=0.08$), and all probabilities within the remaining 21-category group will also be equal ($(1-0.4)/21 \approx 0.0286$) .

### Alternative Projections: The Euclidean Case

The choice of KL divergence as the measure of "distance" is not arbitrary, but it is also not the only possibility. What if we chose to minimize the squared Euclidean distance instead? Consider again the problem of updating a prior $Q$ to a distribution $P$ that satisfies a linear constraint $\sum P_i g_i = E^*$. If we seek to minimize $D_E(P, Q) = \sum_i (P_i - Q_i)^2$, the method of Lagrange multipliers yields a solution of the form:

$$
P_i = Q_i + \lambda_1 + \lambda_2 g_i
$$

After solving for the multipliers, the solution can be expressed as an **additive update** to the prior :

$$
P_i = Q_i + \left( \frac{E^* - E_Q[g]}{N \sigma_g^2} \right) (g_i - \mu_g)
$$

where $E_Q[g]$ is the expectation of $g$ under the prior, and $\mu_g$ and $\sigma_g^2$ are the mean and variance of the values $\{g_i\}$. This contrasts sharply with the **multiplicative update** obtained from minimizing KL divergence. The additive nature of the Euclidean solution can sometimes produce invalid results (e.g., negative probabilities) if the constraints are far from the prior's expectations, whereas the multiplicative nature of the I-projection naturally preserves the non-negativity of probabilities. This provides a strong motivation for the central role of KL divergence in [statistical inference](@entry_id:172747).

### The Dual Problem: M-Projection and Moment Matching

We have focused on minimizing $D(p||q)$, where we find a new distribution $p$ in a set $\mathcal{C}$ that is close to a prior $q$. The [dual problem](@entry_id:177454) is to find a model $p \in \mathcal{C}$ that is close to an observed [empirical distribution](@entry_id:267085) $q_{emp}$, where closeness is measured by $D(q_{emp}||p)$. This is known as an **M-projection**.

$$
p^* = \arg\min_{p \in \mathcal{C}} D(q_{emp}||p)
$$

Minimizing this quantity is equivalent to maximizing the expected [log-likelihood](@entry_id:273783) of the model, $\sum_x q_{emp}(x) \ln p(x)$, which is the cornerstone of maximum likelihood estimation. A profound connection exists between M-projections and I-projections when the model class $\mathcal{C}$ is an **[exponential family](@entry_id:173146)**.

An [exponential family](@entry_id:173146) $\mathcal{E}$ is a set of distributions of the form $p_\theta(x) = \frac{1}{Z(\theta)} h(x) \exp\left(\sum_i \theta_i T_i(x)\right)$. A fundamental theorem states that the M-projection of an [empirical distribution](@entry_id:267085) $q_{emp}$ onto an [exponential family](@entry_id:173146) $\mathcal{E}$ is precisely the unique distribution $p^* \in \mathcal{E}$ whose expected [sufficient statistics](@entry_id:164717) match those of the [empirical distribution](@entry_id:267085) . In other words:

$$
\arg\min_{p \in \mathcal{E}} D(q_{emp}||p) \quad \text{is the distribution } p^* \in \mathcal{E} \text{ such that } \mathbb{E}_{p^*}[T_i(x)] = \mathbb{E}_{q_{emp}}[T_i(x)] \text{ for all } i.
$$

This duality is exceptionally powerful. It connects the geometric concept of projection with the practical, algebraic procedure of **[moment matching](@entry_id:144382)**. For instance, if we want to approximate an observed [joint distribution](@entry_id:204390) $Q(X,Y,Z)$ with a simpler model that assumes a Markov chain structure $X \to Y \to Z$, we are seeking the M-projection of $Q$ onto the set of Markov chains. The solution is the distribution $P(x,y,z)$ that matches the marginals of $Q$ over the cliques of the Markov structure, namely $P(x,y)=Q(x,y)$ and $P(y,z)=Q(y,z)$, which gives $P(x,y,z) = Q(x,y) Q(z|y)$ .

### Projections and Iterative Algorithms

The elegant properties of information projection rely heavily on the [convexity](@entry_id:138568) of the constraint set $\mathcal{C}$. When $\mathcal{C}$ is not convex, the problem becomes more complex, and the solution may not be unique. A classic example is projecting a [prior distribution](@entry_id:141376) $Q$ onto the set of distributions whose support is limited to at most $k$ outcomes. This set is not convex. The I-projection in this case involves a two-step process: first, identify the subset of $k$ outcomes from the original distribution $Q$ that has the largest total probability mass. Second, the projected distribution $P$ sets the probability of these $k$ outcomes to be the renormalized probabilities from $Q$, and all other probabilities to zero . The solution is intuitive: keep the most likely events and discard the rest.

Another advanced application arises when we need to project onto the intersection of several [convex sets](@entry_id:155617), $\mathcal{C} = \mathcal{C}_1 \cap \mathcal{C}_2 \cap \dots$. Finding the I-projection directly can be difficult. However, a simple and powerful iterative algorithm often converges to the correct solution. This method involves starting with the prior $q$ and alternately projecting it onto each of the constraint sets in sequence.

For example, to find the distribution $P(x,y)$ that is closest to a prior $Q(x,y)$ while satisfying specific target marginals $P_X^*(x)$ and $P_Y^*(y)$, we can use an iterative procedure. Let $\mathcal{C}_X$ be the set of distributions with marginal $P_X^*$ and $\mathcal{C}_Y$ be the set with marginal $P_Y^*$. We begin with $P_0 = Q$ and iterate:

$$
P_{2k+1} = \text{I-projection of } P_{2k} \text{ onto } \mathcal{C}_X
$$
$$
P_{2k+2} = \text{I-projection of } P_{2k+1} \text{ onto } \mathcal{C}_Y
$$

This algorithm, a form of the **Csiszár-Tusnády algorithm** and related to **Iterative Proportional Fitting (IPF)**, converges to a unique limit distribution $P_\infty$ . This limit is the I-projection of the original prior $Q$ onto the intersection $\mathcal{C}_X \cap \mathcal{C}_Y$. The resulting distribution has a specific log-[linear form](@entry_id:751308), $P_\infty(x,y) = u_x v_y Q(x,y)$, where the scaling factors $u_x$ and $v_y$ are chosen to meet the marginal constraints. This iterative approach transforms a complex, multi-constraint problem into a sequence of simpler, single-constraint projections.