## Introduction
Identifying dynamic systems from data is a cornerstone of modern engineering and science, enabling the design of controllers, prediction of behavior, and discovery of underlying mechanisms. However, a significant challenge arises when data is collected from a system operating under feedback control. The inherent correlation between system inputs and disturbances can systematically corrupt model estimates, leading to incorrect conclusions and poor performance. This article provides a comprehensive guide to navigating this complex landscape, focusing on two intertwined challenges: obtaining unbiased models from closed-loop data and selecting a model of appropriate complexity.

We will begin our exploration in **Principles and Mechanisms**, where we will dissect the theoretical foundations, from defining model order to understanding the feedback problem and how the Prediction Error Method (PEM) provides a consistent solution. We will also delve into the statistical tools, like AIC and BIC, that govern the crucial bias-variance trade-off in model selection. Following this, **Applications and Interdisciplinary Connections** will showcase these principles in action, illustrating their use in [robust control](@entry_id:260994) design, adaptive systems, and even unexpected domains like human physiology and [nanoscience](@entry_id:182334). Finally, **Hands-On Practices** will offer a chance to apply these concepts through targeted problems. This structured journey will equip you with the knowledge to confidently identify accurate and parsimonious models from closed-loop experiments, starting with the core principles that make it possible.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanisms that govern the identification of dynamic systems from data, with a specific focus on the challenges and solutions pertinent to closed-loop experiments and the critical task of [model order selection](@entry_id:181821). We will begin by formally defining what constitutes a model and its order, proceed to diagnose the core problem of bias in closed-loop identification, present the theoretical remedy offered by the Prediction Error Method (PEM), and culminate in a discussion of principled strategies for selecting an appropriate model structure and complexity.

### Defining the Model and Its Order

Before one can select a model's order, a precise definition of what "order" signifies is required. The concept of [system order](@entry_id:270351) is a measure of a model's complexity, fundamentally representing the minimum number of [state variables](@entry_id:138790) required to describe its internal dynamics.

#### State-Space and Transfer Function Representations

For a discrete-time Linear Time-Invariant (LTI) system, the order can be understood through two primary representations: the [state-space model](@entry_id:273798) and the transfer function.

A [state-space realization](@entry_id:166670) $(A,B,C,D)$ with a state vector $x(t) \in \mathbb{R}^n$ describes the system's evolution. However, the dimension $n$ of the [state vector](@entry_id:154607) for an arbitrary realization is not necessarily the **[system order](@entry_id:270351)**. The true [system order](@entry_id:270351) is the dimension of a **[minimal realization](@entry_id:176932)**, which is the smallest possible state dimension required to represent the system's input-output behavior. A fundamental theorem of [linear systems theory](@entry_id:172825) states that a [state-space realization](@entry_id:166670) is minimal if and only if it is both completely **controllable** and completely **observable** [@problem_id:2883889]. Controllability implies that any state can be reached from the origin via some input sequence, while [observability](@entry_id:152062) implies that any initial state can be uniquely determined from the output sequence. Non-minimal realizations contain states that are either uncontrollable, unobservable, or both; these states are extraneous to the input-output mapping and can be mathematically eliminated to yield a lower-dimensional, [minimal realization](@entry_id:176932). Consequently, any two minimal realizations of the same system are related by a [similarity transformation](@entry_id:152935) and thus share the same state dimension, making the [system order](@entry_id:270351) a unique, well-defined property [@problem_id:2883889].

In the frequency domain, a Single-Input Single-Output (SISO) LTI system is described by a rational transfer function $G(z) = \frac{N(z)}{D(z)}$. If the numerator polynomial $N(z)$ and the denominator polynomial $D(z)$ are **coprime** (i.e., they share no common roots), the transfer function contains no pole-zero cancellations. In this case, the [system order](@entry_id:270351) is equal to the degree of the denominator polynomial, $\deg D(z)$. This coprimeness condition is the transfer-function equivalent of the state-space condition of being controllable and observable. For Multiple-Input Multiple-Output (MIMO) systems, the concept is more complex. The order is not simply the highest degree of the denominators of the individual transfer function entries. Instead, the order is given by the **McMillan degree** of the [transfer function matrix](@entry_id:271746) $G(z)$, which is defined as the sum of the degrees of the invariant pole polynomials in the Smith-McMillan form of $G(z)$ [@problem_id:2883889].

#### Parametric Model Structures

In practice, we identify systems by fitting [parametric models](@entry_id:170911) to data. These models are structured according to specific families of transfer functions. The general representation for a SISO system with an additive disturbance is the **innovations model**:

$$y(t) = G(q^{-1})u(t) + H(q^{-1})e(t)$$

Here, $t$ is the [discrete time](@entry_id:637509) index, $u(t)$ is the input, $y(t)$ is the output, and $e(t)$ is a zero-mean, [white noise process](@entry_id:146877), often called the [innovation sequence](@entry_id:181232). The operator $q^{-1}$ is the backward [shift operator](@entry_id:263113), i.e., $q^{-1}x(t) = x(t-1)$. $G(q^{-1})$ represents the plant dynamics, and $H(q^{-1})$ is a stable and invertible filter that models the [colored noise](@entry_id:265434) affecting the system. Several common parametric model structures are special cases of this representation, distinguished by how they structure $G(q^{-1})$ and $H(q^{-1})$ using polynomials in $q^{-1}$ [@problem_id:2883893].

-   **ARX (AutoRegressive with eXogenous input)**:
    $$A(q^{-1})y(t) = B(q^{-1})u(t) + e(t)$$
    This structure implies $G(q^{-1}) = \frac{B(q^{-1})}{A(q^{-1})}$ and $H(q^{-1}) = \frac{1}{A(q^{-1})}$. A key characteristic is that the plant and noise models are constrained to share the same poles, determined by the roots of $A(q^{-1})$.

-   **ARMAX (AutoRegressive Moving-Average with eXogenous input)**:
    $$A(q^{-1})y(t) = B(q^{-1})u(t) + C(q^{-1})e(t)$$
    This implies $G(q^{-1}) = \frac{B(q^{-1})}{A(q^{-1})}$ and $H(q^{-1}) = \frac{C(q^{-1})}{A(q^{-1})}$. Like ARX, ARMAX models force the plant and noise to share common poles, but it adds parametric flexibility to the noise model numerator through $C(q^{-1})$.

-   **OE (Output-Error)**:
    $$y(t) = \frac{B(q^{-1})}{F(q^{-1})}u(t) + e(t)$$
    This implies $G(q^{-1}) = \frac{B(q^{-1})}{F(q^{-1})}$ and $H(q^{-1}) = 1$. The disturbance is modeled as additive white noise, completely separate from the plant dynamics.

-   **BJ (Box-Jenkins)**:
    $$y(t) = \frac{B(q^{-1})}{F(q^{-1})}u(t) + \frac{C(q^{-1})}{D(q^{-1})}e(t)$$
    This is the most flexible structure, with $G(q^{-1}) = \frac{B(q^{-1})}{F(q^{-1})}$ and $H(q^{-1}) = \frac{C(q^{-1})}{D(q^{-1})}$. It allows for completely independent parameterizations of the plant and noise dynamics.

Model order selection for these structures involves choosing the degrees of the polynomials (e.g., of $A, B, C, D, F$).

### The Challenge of Identification in Closed-Loop Systems

Identifying a system operating in a closed loop presents a fundamental difficulty that is absent in open-loop experiments. The core issue is a feedback-induced **correlation between the plant input and the process disturbance**, which leads to biased estimates if not handled correctly.

Consider a typical feedback loop where the plant output $y(t)$ is corrupted by a disturbance $v(t) = H_0(q^{-1})e(t)$, and the control input $u(t)$ is generated by a controller $K(q^{-1})$ based on the error between a reference $r(t)$ and the measured output $y(t)$:
$$y(t) = G_0(q^{-1})u(t) + v(t)$$
$$u(t) = K(q^{-1})(r(t) - y(t))$$

By substituting the expression for $y(t)$ into the controller equation, we can express the input $u(t)$ in terms of the external signals $r(t)$ and $v(t)$:
$$u(t) = K(q^{-1})(r(t) - [G_0(q^{-1})u(t) + v(t)])$$
Solving for $u(t)$ yields:
$$u(t) = S_0(q^{-1})K(q^{-1})r(t) - S_0(q^{-1})K(q^{-1})v(t)$$
where $S_0(q^{-1}) = (1 + G_0(q^{-1})K(q^{-1}))^{-1}$ is the [sensitivity function](@entry_id:271212).

This equation reveals a critical fact: the plant input $u(t)$ is not an [independent variable](@entry_id:146806) but is itself a function of the disturbance $v(t)$ [@problem_id:2883900]. Consequently, any estimation method that relies on the assumption of uncorrelated regressors and noise, such as [ordinary least squares](@entry_id:137121) (OLS) applied to a simple FIR or ARX model, will produce biased and inconsistent estimates. The OLS estimator's consistency requires the [exogeneity](@entry_id:146270) condition $E[\phi(t)v(t)] = 0$, where $\phi(t)$ is the vector of regressors (e.g., past values of $u(t)$ and $y(t)$). In a closed loop, this condition is violated because both $u(t)$ and $y(t)$ are correlated with $v(t)$. This bias persists asymptotically and is not remedied simply by using a high-power or persistently exciting reference signal $r(t)$ [@problem_id:2883900].

### The Prediction Error Method as a General Solution

The systematic solution to the problem of closed-loop bias is the **Prediction Error Method (PEM)**. PEM finds the parameters $\theta$ of a candidate model that minimize the variance of the one-step-ahead prediction errors. The power of PEM lies in its use of a noise model $H(q^{-1}, \theta)$ to "whiten" the residuals.

The one-step-ahead prediction error, or innovation, is given by:
$$\varepsilon(t, \theta) = y(t) - \hat{y}(t|t-1, \theta)$$

For the general innovations model, this can be computed as:
$$\varepsilon(t, \theta) = H(q^{-1}, \theta)^{-1} [y(t) - G(q^{-1}, \theta)u(t)]$$

The PEM [cost function](@entry_id:138681) to be minimized is typically the sum of squared innovations, $J_N(\theta) = \frac{1}{N}\sum_{t=1}^{N} \varepsilon(t, \theta)^2$. Under a Gaussian assumption for $e(t)$, minimizing $J_N(\theta)$ is equivalent to Maximum Likelihood Estimation.

The crucial insight is what happens when the model structure is correctly specified, i.e., it is capable of representing the true system $(G_0, H_0)$ for some parameter vector $\theta_0$. In this case, the innovations evaluated at the true parameters, $\varepsilon(t, \theta_0)$, become equal to the true underlying [white noise](@entry_id:145248) sequence $e(t)$ [@problem_id:2883905].
$$\varepsilon(t, \theta_0) = H_0(q^{-1})^{-1} [G_0(q^{-1})u(t) + H_0(q^{-1})e(t) - G_0(q^{-1})u(t)] = e(t)$$

Since $e(t)$ is white noise, it is by definition uncorrelated with all past information, including past inputs $u(t-k)$ and past outputs $y(t-k)$ from which the PEM regressors are constructed. This satisfies the necessary condition for consistency. The noise model $H(q^{-1})$ acts as a whitening filter, transforming the colored residual $y(t) - G(q^{-1})u(t)$ into the white [innovation sequence](@entry_id:181232) $\varepsilon(t)$. This mechanism effectively breaks the feedback-induced correlation that biases simpler methods, leading to consistent estimates of the plant parameters even in a closed-loop setting [@problem_id:2883905].

### Strategies and Prerequisites for Closed-Loop Experiments

While PEM provides a powerful theoretical framework, its successful application depends on both the chosen estimation strategy and the quality of the experimental data.

#### Identification Strategies

Three main strategies are used for closed-loop identification [@problem_id:2883929]:

1.  **Direct Approach**: This involves applying an identification method like PEM directly to the measured plant input and output data, $(u(t), y(t))$. A model for both the plant $G(q^{-1})$ and the noise $H(q^{-1})$ is estimated simultaneously. As discussed above, this approach yields consistent estimates provided the noise model is sufficiently parameterized to capture the true disturbance dynamics.

2.  **Indirect Approach**: This is a two-step procedure. First, one identifies a closed-[loop transfer function](@entry_id:274447) where the input is an external signal, like the reference $r(t)$, which is uncorrelated with the disturbance. For instance, one can estimate the transfer function from the reference to the output, $\hat{T}_{ry}(q^{-1}) = \frac{\hat{G} \hat{K}}{1 + \hat{G} \hat{K}}$. In the second step, knowing the controller $K(q^{-1})$, one can algebraically solve for the plant model $\hat{G}(q^{-1})$. This method avoids directly modeling the problematic $(u,y)$ relationship in the first stage.

3.  **Joint Approach**: This method treats the system as a MIMO process with external inputs $(r(t), e(t))$ and measured outputs $(u(t), y(t))$. A complete model of the closed-loop system, parameterized by the unknown plant $G$ and noise model $H$, is estimated in a single step.

#### Persistent Excitation

For any identification method to succeed, the data must be sufficiently informative. This requirement is formalized by the concept of **[persistent excitation](@entry_id:263834) (PE)**. An input signal $u(t)$ is said to be persistently exciting of order $n$ if the regressor correlation matrix, $R_n = \frac{1}{N}\sum_{t=1}^{N} \phi(t)\phi(t)^T$, is [positive definite](@entry_id:149459) for a regressor vector $\phi(t)$ of length $n$ (e.g., $\phi(t) = [u(t-1), \dots, u(t-n)]^T$). In frequency domain terms, this means the signal's spectrum must be non-zero at a sufficient number of frequencies (at least $n/2$ for a real signal to identify an $n$-parameter FIR model).

In closed-loop operation, the excitation seen by the plant is not the raw reference signal $r(t)$, but a filtered version of it. As derived earlier, the component of $u(t)$ driven by $r(t)$ is $u_r(t) = S(q^{-1})K(q^{-1})r(t)$. Therefore, the properties of the closed-[loop filter](@entry_id:275178) $S(q^{-1})K(q^{-1})$ are critical. If this filter has "notches" or deep attenuations at certain frequencies, it can reduce or destroy the [persistent excitation](@entry_id:263834) provided by $r(t)$, rendering certain [system modes](@entry_id:272794) unidentifiable. A well-designed closed-loop experiment thus requires a reference signal $r(t)$ that, after being filtered by the loop dynamics, still provides sufficient excitation at the plant input [@problem_id:2883939].

### The Bias-Variance Trade-off and Principles of Order Selection

Once a consistent estimation method like PEM is chosen, the next critical step is selecting the model order (i.e., the degrees of the polynomials in the chosen structure). This is not simply a matter of choosing the highest possible order. Doing so leads to **[overfitting](@entry_id:139093)**, a phenomenon where the model fits the noise and random fluctuations in the training data too closely, resulting in poor predictive performance on new, unseen data.

This is a manifestation of the fundamental **bias-variance trade-off**.
-   **Bias**: A [systematic error](@entry_id:142393) caused by a model that is too simple to capture the true underlying dynamics ([underfitting](@entry_id:634904)).
-   **Variance**: A random error caused by the model's sensitivity to the specific noise realization in the training data. Complex models (high order) tend to have high variance.

The goal of [model selection](@entry_id:155601) is to find an order that provides the best balance between low bias and low variance. A naive approach might be to choose the model that yields the lowest prediction error on the training data. However, this will almost always lead to selecting the most complex model. The in-sample maximized [log-likelihood](@entry_id:273783), $\ell_n(\hat{\theta})$, is an optimistically biased estimator of the model's true predictive performance on new data. The expected value of this **optimism**, defined as the difference between the in-sample and expected out-of-sample [log-likelihood](@entry_id:273783), is asymptotically equal to $k$, the number of estimated parameters in the model [@problem_id:2883894].
$$\mathbb{E}[\ell_n(\hat{\theta}) - \ell_n^{(0)}(\hat{\theta})] \approx k$$

To obtain an unbiased estimate of a model's predictive power, we must penalize the in-sample likelihood for its complexity. This is the guiding principle behind modern [information criteria](@entry_id:635818).

### Information Criteria for Model Selection

Information criteria are statistical tools that formalize the bias-variance trade-off by adding a penalty term to the maximized log-likelihood. For a model with $k$ estimated parameters based on $N$ data points, and a maximized [log-likelihood](@entry_id:273783) that results in a residual variance estimate of $\hat{\sigma}^2$, the most common criteria are defined as follows (up to additive constants) [@problem_id:2883908]:

-   **Akaike Information Criterion (AIC)**:
    $$\text{AIC} = N \ln(\hat{\sigma}^2) + 2k$$
    The term $N \ln(\hat{\sigma}^2)$ is proportional to $-2\ell_n(\hat{\theta})$. The penalty $2k$ is a direct result of correcting for the asymptotic bias (optimism) of the in-sample likelihood. AIC aims to select the model that minimizes the expected Kullback-Leibler divergence to the true data-generating process, making it a criterion focused on achieving the best **predictive accuracy**. For small sample sizes, a corrected version, **AICc**, is often preferred:
    $$\text{AICc} = \text{AIC} + \frac{2k(k+1)}{N-k-1}$$

-   **Bayesian Information Criterion (BIC)**, also known as **Minimum Description Length (MDL)**:
    $$\text{BIC} = N \ln(\hat{\sigma}^2) + k \ln(N)$$
    BIC has a different theoretical motivation, stemming from a Bayesian approximation to the model's [posterior probability](@entry_id:153467). Its penalty term, $k \ln(N)$, is much stronger than AIC's for any reasonable sample size $N$. This stronger penalty gives BIC a different and very important property: **consistency**. This means that if the true data-generating process has a finite order that is included in the set of candidate models, BIC will select the correct model order with a probability approaching 1 as the sample size $N \to \infty$.

The consistency of BIC can be understood by comparing two [nested models](@entry_id:635829), $\mathcal{M}_0$ (with $k$ parameters) and $\mathcal{M}_1$ (with $k+1$ parameters), where $\mathcal{M}_0$ is the true model. BIC will prefer the more complex model $\mathcal{M}_1$ only if $\text{BIC}(\mathcal{M}_1)  \text{BIC}(\mathcal{M}_0)$, which simplifies to $2(\ell(\hat{\theta}_1) - \ell(\hat{\theta}_0)) > \ln(N)$. The term on the left is the Likelihood Ratio (LR) statistic, which, by Wilks' theorem, converges in distribution to a $\chi^2_1$ random variable and is thus of order $O_p(1)$. The term on the right, $\ln(N)$, diverges to infinity. Therefore, as $N$ grows, the probability that the LR statistic exceeds the diverging threshold $\ln(N)$ goes to zero [@problem_id:2883901]. This ensures that BIC will eventually reject the unnecessary extra parameter. A practical calculation shows that for BIC to select a true, simpler model over a one-parameter-larger alternative with 95% probability, a minimum sample size of $N=47$ is required, highlighting the trade-off between statistical certainty and data requirements [@problem_id:2883901].

### A Practical Strategy for Order Selection in Closed-Loop PEM

Bringing these principles together, we can formulate a robust strategy for selecting the orders of both the plant model ($G$) and the noise model ($H$) in a closed-loop context, for instance, within a Box-Jenkins framework. The key challenge is that an undermodeled noise filter $H$ can lead to a biased plant estimate $\hat{G}$. This creates a specific interplay between bias and variance.

-   **Under-modeling the noise ($n_h$ too small)**: This fails to whiten the residuals properly, leaving correlation between regressors and prediction errors. The result is a **biased plant estimate $\hat{\theta}$**.
-   **Over-modeling the noise ($n_h$ too large)**: This increases the total number of parameters in the model. While it ensures the noise dynamics are captured (reducing bias), it increases the variance of all parameter estimates, including those of the plant, due to the finite amount of information in the data being spread more thinly [@problem_id:2883928].

This trade-off motivates a multi-stage, principled strategy:

1.  **Prioritize Bias Reduction**: To safeguard against a biased plant model, begin by fitting a model with a deliberately high-order noise model, $H(q^{-1})$. This ensures that the noise dynamics are captured with high probability, minimizing the primary source of bias in the plant estimate.

2.  **Select Plant Order**: With the high-order noise model fixed, focus on selecting the plant model order, $n_g$. Use an [information criterion](@entry_id:636495) like BIC or AIC to compare models with different plant orders. This step seeks a parsimonious yet accurate description of the plant dynamics, given that the disturbance effects have been properly accounted for.

3.  **Refine Noise Model and Validate**: Once a suitable plant order $n_g$ is determined, revisit the noise model. Now, with the plant model fixed, reduce the order of the noise model $n_h$ using [information criteria](@entry_id:635818). The goal is to find the most parsimonious noise model that is still consistent with the data.

4.  **Final Validation**: The final chosen model $(n_g, n_h)$ must be rigorously validated. This involves **[residual analysis](@entry_id:191495)**: the model's one-step-ahead prediction errors $\varepsilon(t, \hat{\theta})$ should be statistically indistinguishable from [white noise](@entry_id:145248). Standard tests include checking the autocorrelation of the residuals (to confirm whiteness) and the [cross-correlation](@entry_id:143353) between the residuals and past inputs (to confirm independence). If the residuals pass these tests, it provides strong evidence that the model has successfully captured both the system dynamics and the disturbance characteristics, even in a closed-loop setting [@problem_id:2883905]. Further validation can be performed using techniques like K-fold [cross-validation](@entry_id:164650) to assess the model's predictive performance on data not used for training.

This integrated strategy leverages the theoretical strengths of PEM while pragmatically navigating the bias-variance trade-off inherent in closed-loop system identification.