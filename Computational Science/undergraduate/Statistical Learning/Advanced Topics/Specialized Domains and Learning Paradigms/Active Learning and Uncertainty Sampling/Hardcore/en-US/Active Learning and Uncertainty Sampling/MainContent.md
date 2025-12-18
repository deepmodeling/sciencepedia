## Introduction
In an era where machine learning models hunger for vast amounts of data, the process of labeling that data remains a significant bottleneck, being both expensive and time-consuming. This challenge gives rise to a critical question: if our labeling budget is limited, can we do better than simply labeling data at random? Active learning provides a powerful answer. It is a paradigm where the learning algorithm itself takes control, proactively identifying the most valuable data points from a pool of unlabeled examples to be sent to an expert for labeling.

This article addresses the central problem in [active learning](@entry_id:157812): how to devise a strategy that intelligently selects these informative instances to maximize model performance while minimizing labeling effort. We will navigate the landscape of [active learning](@entry_id:157812), beginning with the foundational **Principles and Mechanisms** that govern how to select valuable data, focusing on the widely-used family of [uncertainty sampling](@entry_id:635527) strategies. We will then explore the transformative impact of these techniques through a survey of **Applications and Interdisciplinary Connections**, demonstrating their use in fields from computational chemistry to [natural language processing](@entry_id:270274). Finally, you will have the opportunity to solidify your understanding through a series of **Hands-On Practices**, bridging the gap between theory and implementation.

## Principles and Mechanisms

Following the introduction to the paradigm of active learning, this chapter delves into the principles and mechanisms that drive the selection of informative data points for labeling. The central challenge in pool-based active learning is to devise a **query strategy**, an algorithm that, given a pool of unlabeled data, intelligently selects the most valuable instance to be labeled by an oracle. The definition of "value" is multifaceted, leading to a variety of sophisticated strategies. We will explore these strategies, beginning with the most intuitive notion of uncertainty, expanding to concepts of diversity and model impact, and concluding with the theoretical underpinnings and practical considerations that govern their application.

### Quantifying Uncertainty: Core Sampling Strategies

The most common family of query strategies is **[uncertainty sampling](@entry_id:635527)**. The core principle is that instances about which the model is least certain are the most informative to label. A model gains little by being told the label of an instance it already predicts with high confidence. Conversely, labeling an instance that lies near a decision boundary or is otherwise ambiguous can provide substantial information for refining the model's parameters. However, "uncertainty" itself can be quantified in several ways, each with distinct behaviors.

Let us consider a probabilistic classifier that, for any input $x$, produces a posterior probability distribution $p(y|x)$ over the set of possible classes $\mathcal{Y}$. We denote the size of the class set as $K=|\mathcal{Y}|$.

#### Least-Confidence Sampling

The most straightforward [measure of uncertainty](@entry_id:152963) is the **least-confidence** (LC) score. This strategy identifies the instance for which the classifier's most confident prediction is minimized. The uncertainty score is defined as:
$$
u_{\mathrm{LC}}(x) = 1 - \max_{y \in \mathcal{Y}} p(y|x)
$$
The active learner then selects the instance $x^*$ from the unlabeled pool that maximizes this score, which is equivalent to selecting the instance with the lowest maximum [posterior probability](@entry_id:153467):
$$
x^*_{\mathrm{LC}} = \arg\max_{x} \left( 1 - \max_{y \in \mathcal{Y}} p(y|x) \right) = \arg\min_{x} \max_{y \in \mathcal{Y}} p(y|x)
$$
The primary drawback of this method is its myopic nature; it considers only the probability of the most likely class, ignoring the distribution of probabilities among the remaining classes. For example, a prediction vector of $(0.4, 0.3, 0.15, 0.15)$ and one of $(0.4, 0.0, 0.3, 0.3)$ would be considered equally uncertain by this metric, even though the former represents ambiguity among two classes while the latter shows ambiguity among three.

#### Margin Sampling

To address the [myopia](@entry_id:178989) of least-confidence sampling, **margin sampling** (MS) considers the ambiguity between the two most likely classes. It aims to select the instance with the smallest difference, or margin, between the posterior probabilities of the first and second most likely classes. Let $p_{(1)}(x)$ be the posterior of the most likely class and $p_{(2)}(x)$ be that of the second most likely class. The margin score is:
$$
u_{\mathrm{margin}}(x) = p_{(1)}(x) - p_{(2)}(x)
$$
Since a smaller margin indicates greater ambiguity and thus higher uncertainty, the active learner selects the instance that *minimizes* this score:
$$
x^*_{\mathrm{margin}} = \arg\min_{x} \left( p_{(1)}(x) - p_{(2)}(x) \right)
$$
This strategy is more nuanced than least-confidence, as it directly targets instances where the model is struggling to differentiate between the top two candidate labels.

In the specific case of [binary classification](@entry_id:142257) ($K=2$), least-confidence and margin sampling are equivalent. If the two classes are $y_1$ and $y_2$, then $p(y_1|x) + p(y_2|x) = 1$. This means $p_{(2)}(x) = 1 - p_{(1)}(x)$. The margin score becomes $u_{\mathrm{margin}}(x) = p_{(1)}(x) - (1 - p_{(1)}(x)) = 2p_{(1)}(x) - 1$. Minimizing this score is equivalent to minimizing $p_{(1)}(x)$, which is precisely the objective of least-confidence sampling. Therefore, for $K=2$, the two strategies will always select the same instance.

For [multi-class classification](@entry_id:635679) ($K>2$), however, their selections can diverge. Consider a 3-class problem with two unlabeled points, $x_A$ and $x_B$, with the following [posterior probability](@entry_id:153467) vectors :
- $x_A$: $(0.60, 0.39, 0.01)$
- $x_B$: $(0.51, 0.26, 0.23)$

Let's compute their uncertainty scores:
- For $x_A$: $p_{(1)}(x_A)=0.60$, $p_{(2)}(x_A)=0.39$.
  - $u_{\mathrm{LC}}(x_A) = 1 - 0.60 = 0.40$
  - $u_{\mathrm{margin}}(x_A) = 0.60 - 0.39 = 0.21$
- For $x_B$: $p_{(1)}(x_B)=0.51$, $p_{(2)}(x_B)=0.26$.
  - $u_{\mathrm{LC}}(x_B) = 1 - 0.51 = 0.49$
  - $u_{\mathrm{margin}}(x_B) = 0.51 - 0.26 = 0.25$

Least-confidence sampling seeks to maximize $u_{\mathrm{LC}}$, so it would select $x_B$ ($0.49 > 0.40$). Margin sampling seeks to minimize $u_{\mathrm{margin}}$, so it would select $x_A$ ($0.21  0.25$). This divergence occurs because least-confidence is drawn to $x_B$'s lower top probability, while margin sampling is drawn to $x_A$'s smaller gap between its top two contenders.

#### Entropy-Based Sampling

The most comprehensive [uncertainty measure](@entry_id:270603) is based on **Shannon entropy**, which considers the entire probability distribution. The entropy of the predictive distribution for an instance $x$ is:
$$
H[Y|x] = - \sum_{y \in \mathcal{Y}} p(y|x) \log p(y|x)
$$
Entropy is maximized when the distribution is uniform (e.g., $(0.5, 0.5)$ in a binary case or $(1/K, \dots, 1/K)$ in a multi-class case), representing maximum uncertainty. It is minimized (to zero) when the distribution is deterministic (e.g., $(1, 0)$), representing perfect certainty. Entropy-based sampling selects the instance that maximizes this score:
$$
x^*_{\mathrm{entropy}} = \arg\max_{x} H[Y|x]
$$
This strategy naturally accounts for the confidence in all class predictions. Let's revisit the previous example and add a third instance, $x_C$, to demonstrate how all three strategies can differ . Consider a pool with points having these posteriors:
- $x_0$: $(0.39, 0.38, 0.23)$
- $x_1$: $(0.41, 0.295, 0.295)$
- $x_2$: $(0.50, 0.495, 0.005)$

Let's analyze their uncertainties (using natural logarithm):
- For $x_0$: $p_{(1)}=0.39$. Margin is $0.39 - 0.38 = 0.01$. Entropy is $1.074$.
- For $x_1$: $p_{(1)}=0.41$. Margin is $0.41 - 0.295 = 0.115$. Entropy is $1.084$.
- For $x_2$: $p_{(1)}=0.50$. Margin is $0.50 - 0.495 = 0.005$. Entropy is $0.722$.

- **Least-Confidence** selects $\arg\min_x p_{(1)}(x)$, which is $x_0$ (with $p_{(1)}=0.39$).
- **Margin Sampling** selects $\arg\min_x (p_{(1)}(x) - p_{(2)}(x))$, which is $x_2$ (with margin $0.005$).
- **Entropy Sampling** selects $\arg\max_x H[Y|x]$, which is $x_1$ (with entropy $1.084$).

Each strategy captures a different aspect of uncertainty: least-confidence sees the globally lowest confidence ($x_0$), margin sampling sees the tightest race between two front-runners ($x_2$), and [entropy sampling](@entry_id:634467) sees the most spread-out distribution overall ($x_1$).

### Beyond Uncertainty: The Role of Diversity

Uncertainty sampling, while powerful, has a potential flaw: it may select a batch of highly uncertain points that are all very similar to each other. If these points lie in the same small region of the feature space, labeling them all provides redundant information. This motivates a second major family of query strategies focused on **diversity**. The goal of diversity-based sampling is to select instances that are different from one another and from already labeled instances, thereby ensuring the labeled set is representative of the entire input space.

A prominent diversity-based method is **core-set selection**. The aim is to choose a "core-set" of points that "covers" the entire data pool as well as possible. One common implementation is a greedy algorithm based on the **k-center** objective . Starting with an initial set of labeled points $S_0$, the algorithm iteratively selects the unlabeled point that is farthest from its nearest neighbor in the currently labeled set $S$:
$$
x^*_{\mathrm{k-center}} = \arg\max_{x \notin S} \left( \min_{s \in S} \|z(x) - z(s)\|_2 \right)
$$
Here, $z(x)$ is a feature representation or embedding of the input $x$, and $\|\cdot\|_2$ is the Euclidean distance. By repeatedly adding the point that is least well-represented by the current labeled set, this approach seeks to reduce the **coverage radius**, defined as the largest distance any point in the pool has to its nearest labeled neighbor.

Core-set selection is fundamentally different from [uncertainty sampling](@entry_id:635527). It is driven by the geometry of the feature space, not the model's predictive uncertainty. For instance, in a scenario with two distinct clusters of points, [uncertainty sampling](@entry_id:635527) might concentrate all its queries near the decision boundary between them, whereas a core-set approach, once it has a point in one cluster, would be strongly incentivized to select a point from the far-away second cluster to improve coverage .

### Hybrid Strategies: Balancing Uncertainty and Diversity

Since uncertainty and diversity are both desirable properties for a query set, it is natural to develop hybrid strategies that combine them.

#### Information Density

A straightforward and effective heuristic is to reweight a point's uncertainty score by its density in the feature space. This approach, often called **[information density](@entry_id:198139)**, aims to select points that are not only uncertain but also representative of dense regions of the data distribution. The acquisition score can be formulated as:
$$
S(x) = H[Y|x] \cdot (\hat{p}(x))^\beta
$$
where $H[Y|x]$ is the predictive entropy, $\hat{p}(x)$ is an estimate of the data density at point $x$ (e.g., via Kernel Density Estimation), and $\beta \ge 0$ is a parameter controlling the influence of the density term .

When $\beta=0$, this method reduces to pure [entropy sampling](@entry_id:634467). As $\beta$ increases, more weight is given to the density term, biasing selection toward uncertain points that are also in high-density regions. This is particularly useful for avoiding the selection of outliers, which may have high uncertainty but are unrepresentative of the overall data distribution and could be noise.

#### Determinantal Point Processes (DPPs)

A more principled and elegant way to combine uncertainty (quality) and diversity is through **Determinantal Point Processes (DPPs)**. A DPP is a probabilistic model over subsets of a ground set, where the probability of selecting a particular subset is proportional to the determinant of a kernel matrix constructed from its elements.

For [active learning](@entry_id:157812), we can define a kernel $K$ that encodes both uncertainty and similarity. A common formulation is :
$$
K_{ij} = \alpha \cdot \mathrm{sim}(x_i, x_j) + \beta \cdot u(x_i) \cdot \delta_{ij}
$$
Here, $\mathrm{sim}(x_i, x_j)$ is a similarity function between items $i$ and $j$ (e.g., an RBF kernel), $u(x_i)$ is an uncertainty score for item $i$, $\delta_{ij}$ is the Kronecker delta, and $\alpha, \beta$ are weights. The probability of selecting a subset $S$ is then $P(S) \propto \det(K_S)$, where $K_S$ is the submatrix of $K$ corresponding to the indices in $S$.

The determinant has a beautiful geometric interpretation: it corresponds to the squared volume of the parallelepiped spanned by the feature vectors. Maximizing this volume inherently promotes diversity (by selecting vectors that are close to orthogonal) while also favoring items with high quality (uncertainty), which appears on the diagonal of the kernel. Setting $\alpha=0$ reduces the problem to selecting the $k$ items with the highest uncertainty scores. Setting $\beta=0$ reduces it to a pure diversity-based selection. By tuning $\alpha$ and $\beta$, a practitioner can smoothly trade off between these two objectives. Finding the subset that maximizes $\det(K_S)$ is NP-hard, but an efficient greedy algorithm with strong approximation guarantees can be used in practice.

### Alternative Formulations of Informativeness

The concept of "informativeness" can be framed in ways that go beyond label uncertainty and data diversity. An alternative is to consider the potential impact of a query on the model itself.

#### Expected Model Change

Instead of asking which point the model is most uncertain about, we can ask which point, when labeled, is expected to cause the greatest change to the model's parameters. This principle is known as **Expected Model Change**. For a model trained with Stochastic Gradient Descent (SGD), a large change corresponds to a large gradient. We can therefore select the point with the largest expected gradient magnitude.

For binary logistic regression with parameters $\theta$, the gradient of the loss for an input $x$ and label $y$ is $\nabla_\theta \ell = (\sigma(\theta^\top x) - y)x$. The expected model change can be defined as the expected norm of this gradient, where the expectation is over the model's own predictive distribution for the unknown label $y$ :
$$
\mathcal{M}(x) = \mathbb{E}_{y|x,\theta} [\|\nabla_\theta \ell(\theta; x, y)\|]
$$
Letting $p = \sigma(\theta^\top x)$, a short derivation reveals a [closed-form expression](@entry_id:267458) for this score:
$$
\mathcal{M}(x) = p(1-p)\|x\| + (1-p)p\|x\| = 2p(1-p)\|x\|
$$
This score is fascinating because it combines an uncertainty term, $p(1-p)$, which is maximized at the decision boundary ($p=0.5$), with a term that depends on the geometry of the input, $\|x\|$. This means that among points with equal uncertainty, this strategy will prefer the one with the largest norm, as it will induce a larger update to the model's parameters. This favors points that are not only uncertain but also have high leverage.

#### Expected Error Reduction

The most direct, albeit often intractable, query strategy is **Expected Error Reduction**. The goal is to select the instance that, once labeled and used for retraining, is expected to yield the greatest reduction in the model's [generalization error](@entry_id:637724) on the remaining unlabeled data. This requires averaging over all possible labels for the candidate point and all possible labels for the test points, making it computationally prohibitive for most models.

However, we can gain insight into this process through a simplified theoretical model . Assume we have a pool of points where for each point $i$, the true data-generating probability is $p_i$ and the model's current prediction is $q_i$. If we query point $s_k$ at step $k$, we can approximate the model update by assuming the model perfectly learns the true probability at that point (i.e., its new prediction $q'_{s_k}$ becomes $p_{s_k}$), while its predictions for other points remain unchanged. Under this "local-fit" approximation, the marginal reduction in the total expected [empirical risk](@entry_id:633993) from the $k$-th query can be derived as:
$$
\Delta_k = R_{k-1} - R_k = \frac{1}{N} \left( \mathrm{CE}(p_{s_k}, q_{s_k}) - H(p_{s_k}) \right)
$$
where $\mathrm{CE}(p,q)$ is the [cross-entropy](@entry_id:269529) and $H(p)$ is the [binary entropy](@entry_id:140897). The term $\mathrm{CE}(p,q) - H(p)$ is precisely the **Kullback-Leibler (KL) divergence** $\mathrm{D_{KL}}(\mathrm{Bern}(p) || \mathrm{Bern}(q))$. Thus, the risk reduction is directly proportional to the [information gain](@entry_id:262008), measured by the KL divergence between the true distribution and the model's predictive distribution at the queried point. This provides a deep information-theoretic justification for querying points where the model's beliefs are most "wrong".

### Theoretical Foundations and Practical Challenges

While the heuristics described above are intuitive, [active learning](@entry_id:157812) also rests on a solid theoretical foundation that explains why and when it can be more sample-efficient than passive learning. However, translating this theory into practice requires addressing several important challenges.

#### The Disagreement Coefficient and Label Complexity

A key theoretical concept is the **disagreement coefficient**, $\theta$. It quantifies the relationship between the error of a hypothesis and the volume of the feature space where it disagrees with other hypotheses. For a hypothesis class $\mathcal{H}$, let $B(h^\star, r)$ be the "ball" of hypotheses with an error of at most $r$ relative to the true hypothesis $h^\star$. The region of disagreement, $\mathrm{DIS}(B(h^\star, r))$, is the set of inputs where at least two hypotheses in this ball disagree. The disagreement coefficient is defined as:
$$
\theta(\mathcal{H}) = \sup_{h^\star \in \mathcal{H}} \sup_{r0} \frac{\Pr_X(\mathrm{DIS}(B(h^\star, r)))}{r}
$$
For many well-behaved hypothesis classes, $\theta$ is a finite constant. Theoretical analyses show that the number of queries needed by a disagreement-based active learner to achieve an excess error of $\epsilon$ scales as $\mathcal{O}(\theta(\mathcal{H}) \log(1/\epsilon))$. For comparison, passive learning requires $\mathcal{O}(1/\epsilon)$. The logarithmic dependence on $1/\epsilon$ demonstrates that active learning can be exponentially more sample-efficient. For the simple class of threshold classifiers on the unit interval, the disagreement coefficient can be computed exactly as $\theta(\mathcal{H})=2$ , leading to a label complexity bound of $\mathcal{O}(2 \ln(1/\epsilon))$.

#### Practical Challenge 1: Model Miscalibration

A critical assumption underlying [uncertainty sampling](@entry_id:635527) is that the model's predictive probabilities are well-calibrated, meaning that a prediction of $p=0.8$ corresponds to an actual event frequency of 80%. Modern machine learning models, particularly deep neural networks, are often poorly calibrated, outputting overconfident predictions.

Miscalibration can severely distort entropy-based sampling . For example, a model might systematically assign scores near $0.5$ (high entropy) to a group of outlier points for which the true conditional probability is actually near $0.9$ (low entropy). An uncalibrated active learner would be biased toward querying these uninformative outliers. This issue can be addressed by explicitly recalibrating the model's outputs before computing uncertainty scores. A standard non-parametric technique for this is **isotonic regression**, which fits a [non-decreasing function](@entry_id:202520) to map raw model scores to calibrated probabilities. Applying this calibration step can significantly change the distribution of entropy scores over the pool, reducing bias and leading to more effective query selections.

#### Practical Challenge 2: Stopping Criteria

An [active learning](@entry_id:157812) process cannot run indefinitely. A crucial practical question is: when do we stop labeling? A principled **stopping criterion** is needed to halt the process when the model's performance has converged or is unlikely to improve significantly with more labels.

A robust stopping criterion can be based on the confidence in the model's estimated risk on the true data distribution . Since the actively labeled set is not an i.i.d. sample from the data distribution, a simple average of the losses on this set is a biased estimate of the true risk. To obtain a consistent estimate, we must use a bias-corrected estimator, such as the **Hájek estimator**, which employs **inverse propensity scoring**:
$$
\hat{R} = \frac{\sum_{i=1}^n \ell_i / p_i}{\sum_{i=1}^n 1 / p_i}
$$
Here, $\ell_i$ is the loss on the $i$-th labeled instance and $p_i$ is its known probability of being selected by the [active learning](@entry_id:157812) policy.

The uncertainty of this estimate, $\hat{R}$, can be quantified by its standard error. The **nonparametric bootstrap** is a powerful technique for this: one repeatedly resamples the labeled set, recomputes $\hat{R}$ for each resample, and then calculates the standard deviation of the resulting distribution of estimates. This gives a bootstrap standard error, $\widehat{\text{SE}}_{\text{boot}}$. With this, we can construct a normal-approximate confidence interval for the true risk, $R$. A common stopping criterion is to terminate labeling when the width of this confidence interval becomes smaller than a predefined tolerance $\tau$. This ensures that we stop only when our estimate of the model's performance is sufficiently precise.