## Introduction
Cyber-Physical Systems (CPS) represent a new generation of engineered systems, characterized by the tight integration of computational intelligence and physical processes. From [smart grids](@entry_id:1131783) and autonomous vehicles to [industrial control systems](@entry_id:1126469) and medical devices, CPS are becoming foundational to modern infrastructure. However, this deep coupling of the cyber and physical worlds creates a complex and critical attack surface. An adversary who compromises the cyber components can directly manipulate physical processes, potentially leading to equipment damage, operational failure, or even threats to human safety. This reality presents a significant knowledge gap and a pressing challenge: how do we design security systems that can effectively detect and prevent intrusions in this hybrid domain?

This article addresses this challenge by providing a graduate-level exploration of [intrusion detection](@entry_id:750791) and prevention for CPS. It builds a rigorous, model-based framework for understanding, identifying, and mitigating cyber-physical threats. Over the course of three chapters, you will gain a deep understanding of this [critical field](@entry_id:143575).

*   **Principles and Mechanisms** will lay the theoretical groundwork. We will formalize the CPS attack surface, define security violations like integrity and availability, and delve into the statistical principles of [model-based detection](@entry_id:1128000) using Digital Twins. We will explore key concepts such as the innovation residual, [hypothesis testing](@entry_id:142556), and the threat of stealthy attacks.

*   **Applications and Interdisciplinary Connections** will bridge theory and practice. We will examine how these principles are applied to secure real-world systems like power grids and industrial protocols. This chapter also highlights the crucial connections to fields such as control theory, [formal methods](@entry_id:1125241), and the legal and ethical dimensions governed by regulations like GDPR.

*   **Hands-On Practices** will offer an opportunity to apply these concepts. Through guided coding exercises, you will design a basic detector, simulate a stealthy attack, and evaluate detector performance, solidifying your understanding of the practical challenges in CPS security.

By navigating these chapters, you will develop a comprehensive perspective on how to secure the next generation of engineered systems against sophisticated adversarial threats.

## Principles and Mechanisms

### The Cyber-Physical Attack Surface: A Foundational Model

To design effective [intrusion detection](@entry_id:750791) and prevention systems (IDPS) for Cyber-Physical Systems (CPS), we must first establish a precise and comprehensive model of the system itself, with a particular focus on identifying all points of vulnerability. A CPS is fundamentally a **hybrid system**, characterized by the tight coupling of a continuous-time physical process (the "plant") and a discrete-time computational controller. The security of such a system is predicated on understanding every pathway through which an adversary might influence its behavior.

Let us formalize this. The physical plant's state, denoted by a vector $x(t) \in \mathbb{R}^n$, evolves continuously over time according to a set of differential equations, which can be expressed in [state-space](@entry_id:177074) form as $\dot{x}(t) = f(x(t), u(t), w(t))$. Here, $u(t) \in \mathbb{R}^m$ represents the control inputs applied by actuators, and $w(t)$ represents exogenous physical disturbances or [unmodeled dynamics](@entry_id:264781).

The computational part of the system operates in [discrete time](@entry_id:637509) steps, indexed by $k$. At sampling instants $t_k$, sensors measure the plant's state, producing measurements $y[k]$. These measurements are invariably corrupted by noise, $v[k]$, and are often a function of only a subset of the [state variables](@entry_id:138790). The controller, which possesses its own internal state $z[k] \in \mathbb{R}^p$, processes these measurements to update its state according to a rule $z[k+1] = g(z[k], y[k])$. Based on its current state, it then computes and issues new control commands via an output law $u[k] = h(z[k])$.

The **attack surface** of a CPS is the minimal set of all state variables, interfaces, and timing parameters that an adversary can manipulate to alter the physical [state evolution](@entry_id:755365) $x(t)$. A rigorous characterization of this surface is the first principle of CPS security . It can be partitioned into three fundamental domains:

1.  **State Variables**: The complete state of a CPS is not merely the physical state $x(t)$ and the controller's software state $z[k]$. Crucially, it also includes the state of **time** itself. The clocks and schedulers that govern the timing of sampling, computation, and actuation are dynamic variables. We can denote this time-base state as $\theta$. An adversary who can compromise time synchronization protocols (e.g., NTP) or manipulate hardware clocks is directly attacking this component of the system state. Thus, the minimal set of state variables an adversary can target is $(x, z, \theta)$.

2.  **Interfaces and Channels**: An adversary acts upon the system by manipulating signals that cross its trust boundary. These interfaces include:
    *   **Cyber Interfaces**: The sensor data channel carrying $y[k]$ and the actuator command channel carrying $u[k]$ are primary targets for data integrity and availability attacks. An adversary can intercept, modify, or block these signals. Furthermore, other [digital communication](@entry_id:275486) channels, such as maintenance ports, debugging interfaces, and network management protocols (collectively denoted $\nu$), provide additional entry points.
    *   **Physical Interfaces**: The CPS is not isolated from its environment. An adversary can act on the physical process directly, for instance by using a heat source, an acoustic generator, or an electromagnetic pulse. Such actions are equivalent to maliciously controlling the exogenous disturbance channel $w(t)$. Similarly, sensor measurements can be disrupted by injecting physical noise into the environment, effectively manipulating the measurement noise channel $v[k]$.

3.  **Timing Parameters**: The real-time nature of CPS means their stability and performance depend on a set of critical [timing constraints](@entry_id:168640). Each of these parameters is a potential attack vector. An adversary can seek to induce failure by violating these assumed bounds. Key parameters include the [sampling period](@entry_id:265475) ($T_s$), worst-case execution time ($C$), control loop deadlines ($D$), sensor and actuator network latencies ($L_y, L_u$), jitter in sampling and actuation ($J_y, J_u$), and clock drift ($\delta$). An attack that subtly increases network delay or jitter can destabilize a control system just as effectively as one that directly falsifies sensor data.

Therefore, any model-based [intrusion detection](@entry_id:750791) scheme, such as one employing a Digital Twin, must be built upon a model that encompasses this complete attack surface: the states $(x, z, \theta)$, the interfaces $(y, u, \nu, w, v)$, and the timing parameters $(T_s, C, D, L_y, L_u, J_y, J_u, \delta)$.

### A Taxonomy of Security Violations

With a clear understanding of the attack surface, we can now define the goals of an IDPS by categorizing the types of harm an adversary seeks to inflict. In the context of CPS, security goals are typically articulated in terms of three canonical properties: **Integrity**, **Availability**, and **Safety**. A violation of any of these constitutes a security incident. These concepts can be formalized as predicates over a system's execution trace, which records the evolution of states, signals, and timing parameters over time .

Consider a system trace $\tau$ containing the true physical state $x_t$, the delivered sensor measurement $y_t$, the issued control command $u_t$, and timing information such as measurement age $\Delta^y_t$ and dropped packets $m^y_t$ at each [discrete time](@entry_id:637509) step $t$.

*   **Integrity Violation**: An integrity violation occurs when the information within the system no longer accurately reflects the physical reality or the intended commands. This can manifest as a discrepancy between a sensor measurement and the true state it represents, or between the actual physical evolution and what is predicted by the system's dynamic model. Formally, if we have bounded process noise $\|w_t\| \le \epsilon$ and measurement noise $\|v_t\| \le \eta$, we can define residuals for the process dynamics, $\rho^u_t = \|x_{t+1} - f(x_t, u_t)\|$, and for the measurement, $\rho^y_t = \|y_t - h(x_t)\|$. An integrity violation can be declared if, at any time $t$, either of these residuals exceeds its corresponding bound:
    $$ \mathsf{IntViol}(\tau) \equiv \exists t : \left( \rho^y_t > \eta \right) \lor \left( \rho^u_t > \epsilon \right) $$
    This predicate captures data spoofing, tampering, or manipulation attacks that are inconsistent with the system's known physical and noise characteristics.

*   **Availability Violation**: An availability violation occurs when essential services, data, or actuation are delayed beyond functional deadlines or are denied altogether. In a CPS, timely delivery of sensor data and control commands is paramount for stability. Given maximum admissible delays $D^y_{\max}$ for sensing and $D^u_{\max}$ for actuation, and indicators for missed packets ($m^y_t=1$ or $m^u_t=1$), an availability violation can be formally defined as:
    $$ \mathsf{AvailViol}(\tau) \equiv \exists t : (m^y_t = 1) \lor (m^u_t = 1) \lor (\Delta^y_t > D^y_{\max}) \lor (\Delta^u_t > D^u_{\max}) $$
    This predicate captures Denial-of-Service (DoS) attacks, network delay attacks, and scheduling attacks that disrupt the real-time operation of the control loop.

*   **Safety Violation**: A safety violation is the most critical failure mode in many CPS, occurring when the system's physical state enters a forbidden or hazardous region. If we define a safe set of states $\mathcal{S} \subset \mathbb{R}^n$, a safety violation is simply the event that the state trajectory leaves this set:
    $$ \mathsf{SafeViol}(\tau) \equiv \exists t : x_t \notin \mathcal{S} $$
    While integrity and availability violations pertain to the cyber and timing domains, a safety violation is a direct statement about a failure in the physical domain. A primary goal of CPS security is to prevent integrity and availability attacks from causing safety violations.

### Principles of Model-Based Intrusion Detection

The central principle of model-based [intrusion detection](@entry_id:750791) is to leverage a model of the system's expected behavior to identify deviations indicative of an anomaly. This process can be systematically broken down into a statistical decision-making framework.

#### The Role of the Digital Twin and the Innovation Residual

A **Digital Twin** is a high-fidelity, synchronized computational model of a physical system. In the context of [intrusion detection](@entry_id:750791), its role is to act as a reference for nominal behavior . The Digital Twin receives the same control inputs $u_k$ as the physical plant and, using a state estimator, produces a prediction of the expected sensor measurements, $\hat{y}_k$.

The cornerstone of this detection approach is the **innovation residual**, defined as the difference between the actual measurement and the predicted measurement:
$$
r_k = y_k - \hat{y}_k
$$
Under normal, non-attacked conditions, if the model is accurate, this residual $r_k$ will be a small, zero-mean stochastic signal, reflecting only the inherent [process noise](@entry_id:270644) ($w_k$) and measurement noise ($v_k$). An attack, however, will perturb the system in a way not anticipated by the model, causing the residual to exhibit statistically significant deviations from its nominal behavior.

#### Detection as Statistical Hypothesis Testing

Intrusion detection can be formally cast as a binary [hypothesis testing](@entry_id:142556) problem. We observe the residual $r_k$ and must decide between two competing hypotheses:

*   **Hypothesis $H_0$ (Normal Operation)**: The system is operating as expected. The residual $r_k$ follows a known nominal probability distribution, often modeled as a zero-mean Gaussian, $r_k \sim \mathcal{N}(0, S)$, where $S$ is the nominal innovation covariance.

*   **Hypothesis $H_1$ (Attack)**: The system is under attack. The attack manifests as a change in the statistical properties of the residual. For example, a bias injection attack might shift the mean, $r_k \sim \mathcal{N}(\mu_a, S)$, while an attack that increases sensor noise might change the covariance, $r_k \sim \mathcal{N}(0, \Sigma_a)$ with $\Sigma_a \succ S$.

This framework can also distinguish between different types of anomalies. For instance, a physical **fault** might manifest as a constant bias in a sensor, leading to a mean shift in the residual ($H_f: r_k \sim \mathcal{N}(\mu_f, S)$), whereas a sophisticated adversary might inject noise-like signals to mask their activity, leading to a change in covariance ($H_a: r_k \sim \mathcal{N}(0, \Sigma_a)$) .

The optimal decision rule for distinguishing between two hypotheses, say $H_a$ and $H_f$, is the **[likelihood ratio test](@entry_id:170711) (LRT)**. This test compares the ratio of the likelihoods of observing the residual $r_k$ under each hypothesis to a threshold determined by the prior probabilities of each event, $\pi_a = \mathbb{P}(H_a)$ and $\pi_f = \mathbb{P}(H_f)$. We decide in favor of an attack ($H_a$) if:
$$
\frac{p(r_k | H_a)}{p(r_k | H_f)} > \frac{\pi_f}{\pi_a}
$$
Taking the logarithm, this becomes a comparison of the [log-likelihood ratio](@entry_id:274622) to a threshold. For the Gaussian fault-versus-attack example, the decision rule for declaring an attack is :
$$
-\tfrac{1}{2} r_k^{\top}\Sigma_a^{-1} r_k + \tfrac{1}{2}(r_k - \mu_f)^{\top} S^{-1} (r_k - \mu_f) - \tfrac{1}{2}\ln\left(\frac{\det \Sigma_a}{\det S}\right) > \ln\left(\frac{\pi_f}{\pi_a}\right)
$$
This inequality elegantly demonstrates how the decision balances the evidence from the observation $r_k$ against the [prior belief](@entry_id:264565). If faults are considered much more likely a priori (large $\pi_f / \pi_a$), the evidence for an attack must be correspondingly stronger to overcome this prior bias.

#### Performance Evaluation: The ROC Curve and AUC

No detector is perfect. It will inevitably make two types of errors: **false positives** (false alarms) and **false negatives** (missed detections). The performance of a detector is characterized by its ability to trade off these two error types.

*   **False Positive Rate (FPR)**: The probability of declaring an attack when none is present, $FPR = P(\text{decide } H_1 | H_0)$.
*   **True Positive Rate (TPR)**: The probability of correctly detecting an attack when one is present, $TPR = P(\text{decide } H_1 | H_1)$. This is also known as **sensitivity** or **recall**.

For a simple detector that raises an alarm if a scalar residual $r$ exceeds a threshold $\tau$, both TPR and FPR are functions of $\tau$. As we lower the threshold $\tau$ to catch more attacks (increasing TPR), we also increase the likelihood of flagging benign noise as an attack (increasing FPR). The **Receiver Operating Characteristic (ROC) curve** is a parametric plot of $(FPR(\tau), TPR(\tau))$ for all possible values of the threshold $\tau$. It provides a complete picture of the detector's performance trade-off .

A single scalar metric to summarize the performance shown in an ROC curve is the **Area Under the Curve (AUC)**. The AUC ranges from $0.5$ (for a random guesser) to $1.0$ (for a perfect classifier). A higher AUC indicates better overall performance. The AUC has a remarkable probabilistic interpretation: it is the probability that a randomly drawn residual from the attack distribution ($R_1 \sim \mathcal{N}(\mu_1, \sigma^2)$) will be larger than a randomly drawn residual from the nominal distribution ($R_0 \sim \mathcal{N}(\mu_0, \sigma^2)$). For the case of two Gaussian distributions with the same variance, the AUC can be derived in [closed form](@entry_id:271343) :
$$
\text{AUC} = P(R_1 > R_0) = \Phi\left(\frac{\mu_1 - \mu_0}{\sigma\sqrt{2}}\right)
$$
where $\Phi(\cdot)$ is the [cumulative distribution function](@entry_id:143135) (CDF) of the [standard normal distribution](@entry_id:184509). This elegant result shows that the inherent distinguishability of the two hypotheses depends on the separation of their means relative to their standard deviation.

#### Bayesian Risk Minimization

The choice of an operating point on the ROC curve (i.e., the choice of a threshold) can be formalized by considering the costs associated with misclassification. Let $C_{10}$ be the cost of a false alarm and $C_{01}$ be the cost of a missed detection. A rational approach is to choose the decision rule that minimizes the total expected cost, known as the **Bayes risk**.

The Bayes-optimal decision rule chooses the hypothesis that has the lower posterior expected loss. This leads to a [likelihood ratio test](@entry_id:170711) where the threshold is no longer just a function of priors, but also of the costs :
$$
\frac{p(r | H_1)}{p(r | H_0)} > \frac{C_{10}(1-\pi)}{C_{01}\pi}
$$
where $\pi = P(H_1)$ is the [prior probability](@entry_id:275634) of an attack. This rule shows that if the cost of a missed detection ($C_{01}$) is very high compared to a false alarm ($C_{10}$), the threshold will be lower, making the detector more sensitive at the expense of more false alarms. The minimum achievable risk, or **Bayes risk**, is a function of the priors, costs, and the statistical separability of the hypotheses, providing a complete theoretical characterization of the best possible performance for a given problem .

### Key Detection Mechanisms and Attack Vectors

Building on these principles, we can examine specific mechanisms for implementing [intrusion detection](@entry_id:750791) and the corresponding attack strategies adversaries might employ.

#### Mechanism: State Estimation and Residual Monitoring

A Digital Twin-based detector relies on a causal, stable [state estimator](@entry_id:272846) (such as a Kalman filter) to generate predictions. For this mechanism to be effective, several critical conditions must be met :

1.  **Observability**: The system, described by the [state-space](@entry_id:177074) pair $(A,C)$, must be **observable**. Observability is a fundamental property that guarantees the internal state $x_k$ can be reconstructed from the history of measurements $y_k$. If a system is not observable, there are "hidden" internal state dynamics that do not affect the output, making it impossible for any estimator to track them. An attack targeting these unobservable subspaces would be inherently undetectable through output monitoring.

2.  **Synchronization**: The Digital Twin must be tightly time-synchronized with the physical plant. The comparison $r_k = y_k - \hat{y}_k$ is meaningful only if the measurement $y_k$ and the prediction $\hat{y}_k$ correspond to the same instant in the physical process's evolution. Significant [clock skew](@entry_id:177738) or network delay between the plant and the twin will generate large residuals even in the absence of an attack, leading to a flood of false alarms.

3.  **Robustness to Model Mismatch**: Real-world Digital Twins are never perfect. There will always be some degree of [model mismatch](@entry_id:1128042) between the twin's parameters ($A_M, B_M, C_M$) and the true plant's parameters ($A, B, C$). A practical IDPS must be robust to this uncertainty. This involves characterizing the effect of bounded [model mismatch](@entry_id:1128042) on the nominal residual distribution and setting detection thresholds accordingly to achieve a desired false alarm rate.

#### Attack Vector: Stealthy False Data Injection

A sophisticated adversary will not launch a crude attack that creates large, obvious residuals. Instead, they will attempt to design an attack that is **stealthy**, meaning it manipulates the system's state while keeping the residual distribution statistically identical to its nominal form. The canonical example of such a threat is the **False Data Injection (FDI) attack** .

In an FDI attack, the adversary injects a malicious additive signal $a_k$ into the sensor measurements, so the estimator receives $y_k = C x_k + v_k + a_k$. An attack is perfectly stealthy if the innovation under attack, $\tilde{y}_k^{\text{att}}$, is statistically indistinguishable from the nominal innovation, $\tilde{y}_k^{\text{nom}}$. This requires the effect of the attack injection $a_k$ to be completely cancelled out within the innovation equation. This cancellation occurs if the attack vector $a_k$ is designed to perfectly mimic the effect of a change in the plant's state from the estimator's perspective.

This leads to two precise conditions for a perfectly stealthy FDI attack:
1.  **Subspace Condition**: The attack vector $a_k$ must lie within the [column space](@entry_id:150809) of the measurement matrix $C$. That is, there must exist some fictitious state error vector $\delta_k$ such that $a_k = C \delta_k$. This ensures the injected data is consistent with a physically possible (though non-existent) state change.

2.  **Dynamical Consistency Condition**: To remain stealthy over time, the sequence of fictitious state errors $\delta_k$ must evolve according to the system's own dynamics, i.e., $\delta_{k+1} = A \delta_k$.

Combining these, a stealthy attack sequence must take the form $a_k = C A^k \delta_0$ for some initial (adversarially chosen) fictitious error $\delta_0$ . The adversary initiates an attack that looks to the estimator exactly like the free evolution of the system from some non-zero initial state error. The existence of such attacks underscores the need for detection mechanisms that go beyond simple residual monitoring, such as authentication, or detectors that monitor [physical invariants](@entry_id:197596) not captured in the standard control model.

#### Mechanism: Specification-Based Monitoring

An alternative and complementary approach to statistical, [model-based detection](@entry_id:1128000) is **specification-based monitoring**. This method leverages [formal logic](@entry_id:263078) to define system requirements and detects any behavior that violates them. **Metric Temporal Logic (MTL)** is a powerful formalism for expressing complex real-time properties.

For instance, a critical safety requirement can be expressed as "the state $x(t)$ must always remain within the safe set $\mathcal{S}$". In MTL, this is written as :
$$ \varphi := \Box_{[0,\infty)}(x \in \mathcal{S}) $$
The satisfaction of such a formula can be given a quantitative or **robust semantics** using a [signed distance function](@entry_id:144900) $d_{\mathcal{S}}(x)$, which is positive inside $\mathcal{S}$ and negative outside. The robustness of the formula $\varphi$ for a trajectory $x(t)$ is the minimum distance to the unsafe region over all time: $\rho(x, \varphi) = \inf_{t \ge 0} d_{\mathcal{S}}(x(t))$. A positive robustness means the specification is satisfied.

In practice, we only have noisy measurements $y(t) = x(t) + w(t)$ with bounded noise, $\|w(t)\| \le \epsilon$. We can still make definitive statements about safety violations. Using the properties of the [distance function](@entry_id:136611), we can guarantee that a safety violation has occurred ($d_{\mathcal{S}}(x(t))  0$) if the measured value is sufficiently far into the unsafe region:
$$ d_{\mathcal{S}}(y(t))  -\epsilon $$
This provides a sound rule for declaring an intrusion based on a direct violation of a formal safety specification. This can be combined with a Digital Twin-based anomaly detector to create a more powerful, composite detection system that flags intrusions based on either explicit specification violations or statistically significant deviations from the nominal model .

### Advanced Topics and Long-Term Operation

#### Adapting to Concept Drift

A major challenge in the long-term deployment of an IDPS is **concept drift**. The statistical properties of a real-world CPS are not stationary; they change over time due to component aging, environmental variations, or changes in operational modes. This causes the distribution of the features $x_t$ and the relationship between features and labels $y_t$—the [joint distribution](@entry_id:204390) $P_t(x,y)$—to vary. A static detector trained on data from one time period will suffer a severe degradation in performance as the system drifts .

An effective IDPS must therefore be an adaptive, [online learning](@entry_id:637955) system. A robust architecture for handling concept drift involves three integrated components:

1.  **Online Learning with Forgetting**: The classifier parameters $\theta_t$ must be continuously updated to track the changing data distribution. This is often accomplished by minimizing an exponentially weighted [risk function](@entry_id:166593), which places more emphasis on recent data. Algorithms like Follow-the-Regularized-Leader (FTRL) are well-suited for this streaming setting.

2.  **Explicit Drift Detection**: To react quickly to abrupt changes, the system should incorporate a drift detector. This involves monitoring the statistics of the data stream (e.g., the distribution of classifier scores on benign data) and using a statistical test, such as the two-sample Kolmogorov-Smirnov (KS) test, to detect significant changes between recent and past data windows. When a drift is detected, the learning algorithm can be made more adaptive, for example by increasing its [learning rate](@entry_id:140210) or its [forgetting factor](@entry_id:175644).

3.  **Adaptive Thresholding for FPR Control**: Just as the classifier must adapt, so too must the decision threshold $\tau_t$. To maintain a constant target False Positive Rate (FPR), the threshold must be continuously adjusted to be the appropriate empirical quantile of the *current* distribution of scores from benign data. Finite-sample statistical guarantees, such as the Dvoretzky-Kiefer-Wolfowitz (DKW) inequality, can be used to bound the deviation of the true FPR from the target rate.

#### A Unified Dependability Perspective

Finally, it is instructive to situate the problem of [intrusion detection](@entry_id:750791) within the broader field of **dependability engineering**. The classic Laprie taxonomy provides a causal chain for system failures: a **fault** (the root cause) may lead to an **error** (an incorrect internal state), which may in turn lead to a **failure** (an externally observable deviation from correct service).

This framework provides a powerful lens for unifying the analysis of [system reliability](@entry_id:274890) (concerning benign, random faults) and security (concerning malicious, directed faults) .
*   An **adversarial attack attempt** is classified as a **fault**, just as a random component failure is.
*   A **compromised state** within the controller or a corrupted data value is an **error**.
*   An **unsafe physical state** or deviation from the specified service is a **failure**.

This unified view allows us to combine models from [reliability theory](@entry_id:275874) and security analysis. For instance, we can model the total instantaneous risk of a service failure, known as the **total [hazard rate](@entry_id:266388)** $\lambda_{\text{tot}}(t)$, as the sum of contributions from independent benign and adversarial causes. If benign faults contribute a [hazard rate](@entry_id:266388) of $\lambda_b(t)$, and adversarial attempts arrive with an intensity of $\alpha(t)$, the total hazard rate is:
$$
\lambda_{\text{tot}}(t) = \lambda_b(t) + \alpha(t) (1 - c(t)) q(t) p_s(t)
$$
Here, the adversarial contribution is the product of the attack arrival rate $\alpha(t)$ and the probability that a single attack succeeds, which is itself a chain of probabilities: the probability of evading detection $(1 - c(t))$, the probability of causing an error given evasion $q(t)$, and the probability of that error propagating to a failure $p_s(t)$. This holistic model provides a quantitative basis for making design trade-offs between improving component reliability and enhancing security measures to achieve a desired overall level of system dependability.