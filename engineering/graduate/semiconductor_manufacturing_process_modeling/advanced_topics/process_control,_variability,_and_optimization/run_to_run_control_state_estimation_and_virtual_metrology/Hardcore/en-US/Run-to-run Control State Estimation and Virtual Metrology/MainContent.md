## Introduction
In modern semiconductor manufacturing, achieving high yields and consistent product quality requires stringent control over complex fabrication processes. As device features shrink and complexity grows, inherent process variability and slow drifts from factors like tool aging and consumable wear pose a significant challenge. Traditional methods like Statistical Process Control (SPC) are designed to monitor for stability but do not actively compensate for these continuous variations. This article addresses this gap by providing a comprehensive exploration of Run-to-Run (R2R) control, state estimation, and Virtual Metrology (VM)—a powerful suite of techniques for active process regulation.

This guide is structured to build a deep understanding from the ground up. The first chapter, **"Principles and Mechanisms"**, will lay the theoretical foundation, explaining the core concepts of R2R control, modeling process drift using state-space methods, and designing [optimal estimators](@entry_id:164083) like the Kalman filter. The second chapter, **"Applications and Interdisciplinary Connections"**, will expand on these fundamentals to tackle real-world complexities such as [multivariable systems](@entry_id:169616), tool-to-tool matching, and the crucial integration of machine learning-based VM to overcome metrology delays, also drawing connections to analogous problems in other scientific fields. Finally, the **"Hands-On Practices"** section will offer practical problems to solidify your understanding of process characterization, [controller design](@entry_id:274982), and robustness analysis. Through this structured journey, you will gain the expertise to design and implement advanced control systems that enhance stability, reduce variability, and drive manufacturing excellence.

## Principles and Mechanisms

This chapter delineates the fundamental principles and core mechanisms underpinning Run-to-Run (R2R) control, state estimation, and [virtual metrology](@entry_id:1133824). We will proceed from foundational concepts of [process modeling](@entry_id:183557) and control philosophy to the sophisticated techniques required for robust implementation in a manufacturing environment, such as state estimation under uncertainty and the integration of machine learning-based [metrology](@entry_id:149309).

### The Run-to-Run Control Paradigm

At its core, Run-to-Run (R2R) control is a specialized form of discrete-time [feedback control](@entry_id:272052) tailored to manufacturing processes that are executed in sequential batches, lots, or runs. In semiconductor fabrication, a "run" typically corresponds to the processing of a single wafer or a cassette of wafers. The fundamental premise of R2R control is to use information from completed runs to systematically adjust the recipe for subsequent runs, with the objective of maintaining process outputs at their desired targets despite inherent variability and drift.

#### Timescale and Scope

The operational timescale of R2R control is the discrete index of the run, denoted by $k \in \{0, 1, 2, \dots\}$. All actions and measurements are considered at this level. This contrasts with **within-run control**, which operates on a continuous or high-frequency discrete timescale, denoted by $t$, *during* the processing of a single run $k$. Within-run control, such as real-time [endpoint detection](@entry_id:192842) in an etch process using an [optical emission](@entry_id:1129160) signal, is designed to reject high-frequency disturbances that occur within the duration of a single run. R2R control, conversely, is blind to these intra-run dynamics; its purpose is to correct for slower, run-to-run variations, such as tool aging, chamber coating, or fluctuations in raw material properties .

#### Distinguishing R2R Control from Other Methodologies

It is crucial to distinguish R2R control from **Statistical Process Control (SPC)**. While both methodologies operate on run-level data, their philosophies are fundamentally different. SPC is a monitoring and diagnostic paradigm. It employs tools like control charts to track process outputs and determine if the process is in a state of statistical stability. An action, such as halting the process for maintenance, is typically triggered only when an "out-of-control" signal suggests the presence of a special cause of variation. SPC does not, as a matter of routine, perform automatic recipe adjustments .

In contrast, R2R control is an active feedback strategy. It presumes that the process is subject to inherent, unavoidable drift and actively manipulates the recipe inputs on a run-by-run basis to continuously compensate for this drift. The goal is not just to maintain stability, but to actively steer the process output towards a specific target value, $y^{\star}$.

### Modeling for Run-to-Run Control

Effective control requires a model of the process that, while simplified, captures the essential input-output relationship and the nature of the disturbances.

#### The Linear Process Model

For a single-input, single-output (SISO) process, a widely used model in R2R control linearizes the process behavior around a nominal operating point. The output of run $k$, denoted $y_k$, is related to the recipe input for that run, $u_k$, by the affine relationship:

$y_k = G u_k + d_k + v_k$

Here, $G$ is the **process gain**, representing the local sensitivity of the output to the input ($G = \frac{\partial y}{\partial u}$). The term $d_k$ represents the **unmeasured process drift** or bias. This term captures the net effect of all slowly varying factors that are not explicitly controlled, such as equipment aging, consumable degradation, or environmental changes. Finally, $v_k$ represents **measurement noise** or other sources of random, uncorrelated run-to-run variability. It is typically modeled as a zero-mean white noise sequence with variance $\sigma_v^2$ .

#### Modeling Process Drift: The Random Walk and Its Generalizations

The behavior of the drift term $d_k$ is central to R2R control design. A canonical and highly effective model for slow, cumulative drift is the **random walk**:

$d_{k+1} = d_k + w_k$

In this model, the drift at the next run is equal to the current drift plus a small, random increment $w_k$. The term $w_k$ is modeled as a zero-mean white noise sequence with variance $\sigma_w^2$, representing the incremental change per run. This model has a powerful physical interpretation: it describes a process where many small, independent changes (e.g., microscopic wear events) accumulate over time to produce a slowly varying bias .

A key property of a [random walk process](@entry_id:171699) is that it is **non-stationary**. Specifically, its variance grows linearly with time: $\text{Var}(d_k) = \text{Var}(d_0) + k \sigma_w^2$. This unbounded variance mathematically captures the notion of a process that "wanders" away from its starting point over long periods. Because its statistical properties change over time, the process $d_k$ is not [wide-sense stationary](@entry_id:144146) (WSS). However, its [first difference](@entry_id:275675), $\Delta d_k = d_k - d_{k-1} = w_{k-1}$, is a white noise sequence and is therefore WSS. This property is foundational to many [time-series analysis](@entry_id:178930) techniques used in R2R control.

The random walk is a specific instance of a more general **first-order autoregressive (AR(1)) model**:

$d_{k+1} = \alpha d_k + w_k$

Here, $\alpha$ is the autoregressive parameter. When $|\alpha|  1$, the process is [wide-sense stationary](@entry_id:144146), with its variance converging to $\frac{\sigma_w^2}{1-\alpha^2}$. It represents a drift that tends to revert to a mean. The random walk corresponds to the non-stationary boundary case where $\alpha = 1$ .

#### The State-Space Formulation

To apply standard tools from modern control theory, it is advantageous to express the process model in a [state-space representation](@entry_id:147149). For R2R control, the unmeasured drift is the natural choice for the system's **state**, $x_k = d_k$. With this definition, the random walk drift model and the linear output model can be written in the standard discrete-time linear state-space form:

$x_{k+1} = A x_k + B u_k + w_k$

$y_k = C x_k + D u_k + v_k$

By comparing these generic equations to our specific model ($d_{k+1} = d_k + w_k$ and $y_k = G u_k + d_k + v_k$), we can identify the corresponding scalar matrices:
-   $A = 1$: The [state transition matrix](@entry_id:267928), indicating the random walk nature of the state.
-   $B = 0$: The input matrix, indicating that the recipe input $u_k$ does not directly influence the drift dynamic.
-   $C = 1$: The output matrix, showing that the state (drift) adds directly to the output.
-   $D = G$: The feedthrough matrix, representing the direct process gain from input to output.

This formulation, $(A, B, C, D) = (1, 0, 1, G)$, provides a rigorous and standardized foundation for designing estimators and controllers .

### State Estimation: Observing the Unseen Drift

A fundamental challenge in R2R control is that the state—the process drift $d_k$—is not directly measurable. Therefore, it must be estimated using the available information: the sequence of applied inputs $\{u_i\}$ and measured outputs $\{y_i\}$ for $i \le k$.

#### The Estimation Problem

From the output equation, we can compute a **residual**, $e_k = y_k - G u_k$. This residual is a noisy measurement of the drift:

$e_k = d_k + v_k$

The problem of state estimation is thus to filter the sequence of noisy measurements $\{e_k\}$ to produce the best possible estimate of the underlying drift sequence $\{d_k\}$, given our knowledge of its random walk dynamics.

#### The Exponentially Weighted Moving Average (EWMA) Estimator

An intuitive and widely used [recursive filter](@entry_id:270154) for this problem is the **Exponentially Weighted Moving Average (EWMA) estimator**. The estimate for the drift at run $k$, denoted $\hat{d}_k$, is formed as a weighted average of the previous estimate, $\hat{d}_{k-1}$, and the new piece of information, $e_k$:

$\hat{d}_k = (1 - \lambda) \hat{d}_{k-1} + \lambda e_k = (1 - \lambda) \hat{d}_{k-1} + \lambda (y_k - G u_k)$

The parameter $\lambda \in (0, 1]$ is the **smoothing factor** or [forgetting factor](@entry_id:175644). It dictates the trade-off between responsiveness and noise immunity.
-   A **small $\lambda$** (e.g., $0.1$) gives more weight to the previous estimate, resulting in a heavily smoothed estimate that is robust to measurement noise $v_k$ but slow to react to real changes in the drift $d_k$.
-   A **large $\lambda$** (e.g., $0.9$) gives more weight to the current residual, allowing the estimate to track changes in drift rapidly, but at the cost of being more sensitive to measurement noise .

#### The Kalman Filter: An Optimal Estimation Framework

The EWMA filter is, in fact, a special case of the optimal linear estimator for this system: the **Kalman Filter**. For the state-space model defined previously, the Kalman filter provides a [recursive algorithm](@entry_id:633952) to compute the minimum mean squared error estimate of the state. In steady-state operation, the Kalman gain becomes a constant, and the filter equations simplify to the EWMA form. The optimal value of the smoothing factor, $\lambda$, is the steady-state Kalman gain, which is a function of the noise variances $\sigma_w^2$ and $\sigma_v^2$: $\lambda = \frac{-\lambda_0 + \sqrt{\lambda_0^2 + 4\lambda_0}}{2}$, where $\lambda_0 = \sigma_w^2 / \sigma_v^2$.

Critically, as the process drift becomes more volatile (increasing $\sigma_w^2$), the optimal Kalman gain $\lambda$ increases, placing more trust in the new measurement. Conversely, as the measurement noise increases (increasing $\sigma_v^2$), the gain decreases to smooth out the noise . The Kalman filter framework also allows us to quantify the performance of the estimator. For the [random walk model](@entry_id:144465), the filter reaches a finite steady-state posterior error variance, $P = \text{Var}(d_k - \hat{d}_k)$, which solves the algebraic Riccati equation $P^2 + \sigma_w^2 P - \sigma_w^2 \sigma_v^2 = 0$. This remarkable result shows that even though the drift process itself is non-stationary and its variance grows without bound, an [optimal filter](@entry_id:262061) can track it with a constant, finite [error variance](@entry_id:636041) .

### Designing the Run-to-Run Controller

Once an estimate of the drift, $\hat{d}_{k|k-1}$, is available before run $k$, the next step is to use this information to select the input $u_k$. A common strategy is **disturbance feedforward**, where the input is chosen to counteract the predicted effect of the drift. The ideal controller would set $G u_k + \hat{d}_{k|k-1} = y^{\star}$, yielding the control law $u_k = G^{-1}(y^{\star} - \hat{d}_{k|k-1})$.

Many practical R2R controllers can be analyzed from this perspective. For example, a simple **integral controller** takes the form:

$u_k = u_{k-1} + K (y^{\star} - y_{k-1})$

This can be shown to be equivalent to using the raw residual from the previous run as the drift estimate and applying the disturbance feedforward principle . While simple, this approach can be suboptimal as it does not allow for independent tuning of the estimation and control components.

#### Control Based on an Explicit Optimization Objective

A more rigorous approach is to define the control objective via a mathematical cost function and solve for the input $u_k$ that minimizes it. A common objective function balances two competing goals: minimizing the expected [tracking error](@entry_id:273267) and penalizing excessive changes in the recipe inputs. This is expressed as a quadratic cost function:

$J_k = \mathbb{E}\left[ (y_k - y^{\star})^2 \mid \mathcal{I}_{k-1} \right] + \rho (u_k - u_{k-1})^2$

Here, $\mathcal{I}_{k-1}$ represents all information available before run $k$, and $\rho  0$ is a **move suppression** weight. The first term penalizes deviations from the target, while the second term penalizes large, aggressive changes to the recipe, promoting smoother operation .

By substituting the process model into $J_k$ and minimizing with respect to $u_k$, we obtain the [optimal control](@entry_id:138479) law:

$u_k = u_{k-1} + \frac{G}{G^2 + \rho} \left( y^{\star} - (G u_{k-1} + \hat{d}_{k|k-1}) \right)$

This controller has an intuitive incremental form. The term $(y^{\star} - (G u_{k-1} + \hat{d}_{k|k-1}))$ represents the predicted error for run $k$ if the input were held at $u_{k-1}$. The controller applies a correction proportional to this predicted error.

#### The Trade-off between Tracking Performance and Input Smoothness

The analysis of this optimal controller reveals the fundamental trade-off governed by the tuning parameter $\rho$:
-   The [controller gain](@entry_id:262009), $K = \frac{G}{G^2 + \rho}$, decreases as $\rho$ increases.
-   The convergence rate of the controller is determined by the contraction factor $\alpha = \frac{\rho}{G^2 + \rho}$. As $\rho$ increases, $\alpha$ approaches 1, indicating slower convergence.
-   A large value of $\rho$ results in a small gain and slow correction, but it makes the controller less sensitive to noise in the drift estimate, leading to smoother input adjustments.
-   A small value of $\rho$ yields a high gain and fast tracking, but can cause the controller to overreact to measurement noise ("noise chasing"), resulting in volatile recipe changes.

This framework provides a principled way to tune the controller's aggressiveness based on the specific requirements of the process for stability, smoothness, and performance .

### Virtual Metrology: Bridging the Information Gap

The R2R control framework described so far assumes that a measurement $y_k$ is available shortly after run $k$ is completed. In many industrial settings, this assumption is violated.

#### The Challenge of Metrology Delay and Sparsity

Physical measurement (metrology) of wafer properties like [critical dimension](@entry_id:148910) (CD) can be time-consuming and expensive. Consequently, measurements may be **sparse** (only a subset of wafers are measured) or subject to significant **delay**. A metrology delay of $\tau$ runs means that at the time of choosing input $u_k$, the most recent available measurement is from run $k-\tau$, i.e., $\tilde{y}_k = y_{k-\tau}$.

Delay is highly detrimental to [feedback control](@entry_id:272052). It reduces the stability margins of the closed-loop system and degrades its ability to reject disturbances. For a simple integral controller, a delay of just one run ($\tau=1$) can shrink the range of stable gains by half or more. For a process with drift, this performance degradation is even more severe, as the controller is always acting on outdated information about the state of the process .

#### Defining Virtual Metrology as Supervised Learning

**Virtual Metrology (VM)** is a data-driven technique designed to overcome the limitations of sparse and delayed physical metrology. The goal of VM is to predict the post-process quality metric $y_k$ using in-situ sensor data, $z_k \in \mathbb{R}^p$, which are collected in real-time during run $k$. These sensor data can include variables like chamber pressure, gas flows, RF power, and [optical emission](@entry_id:1129160) spectra.

The task is formulated as a standard **supervised machine learning** problem. Given a historical training dataset of $N$ runs where both in-situ data and physical measurements are available, $\{(z_i, y_i)\}_{i=1}^N$, the goal is to learn a mapping function $f$:

$\hat{y}_k = f(z_k)$

The predicted value $\hat{y}_k$ serves as a "virtual" measurement that is available immediately after the run, effectively reducing the metrology delay to near zero .

#### Practical Aspects of VM Model Training: Loss Functions and Feature Standardization

The choice of model $f$ can range from [simple linear regression](@entry_id:175319) to complex nonlinear models like neural networks. Training involves minimizing a **loss function** that quantifies the prediction error. While Mean Squared Error (MSE) is common, **Mean Absolute Error (MAE)**, defined as $\frac{1}{N}\sum |y_i - f(z_i)|$, is often preferred. MAE is less sensitive to outlier measurements than MSE. Statistically, minimizing MAE corresponds to estimating the conditional median of the output, whereas MSE targets the conditional mean.

A critical, and often overlooked, step in training VM models is **[feature standardization](@entry_id:910011)**. In-situ sensor data typically have vastly different physical units and numerical scales (e.g., pressure in Pascals $\sim 10^2$, OES intensity in counts $\sim 10^6$). When training a model with [gradient-based optimization](@entry_id:169228), the update to a model parameter is proportional to the magnitude of the associated feature. Without standardization, features with large scales will dominate the learning process, leading to an ill-conditioned optimization problem and slow or unstable convergence. Furthermore, [regularization techniques](@entry_id:261393) (like $\ell_1$ or $\ell_2$ penalties) that penalize parameter magnitudes are rendered ineffective, as they unfairly penalize weights associated with large-scale features. Standardizing all features to have [zero mean](@entry_id:271600) and unit variance (Z-score normalization) is therefore essential for robust model training .

### Integrating Virtual Metrology into R2R Control

Once a VM model is trained, its predictions can be integrated into the R2R control loop to provide timely feedback.

#### Closing the Loop with VM

On runs where physical [metrology](@entry_id:149309) is not performed, the VM prediction $\hat{y}_k$ is used in place of a physical measurement in the controller and estimator update equations. For instance, the EWMA estimator becomes:

$\hat{d}_k = (1 - \lambda) \hat{d}_{k-1} + \lambda ( \hat{y}_k - G u_k )$

This allows the control system to track process drift on every run, rather than only on the sparsely measured runs, significantly improving [disturbance rejection](@entry_id:262021) performance .

#### The Critical Role of Model Bias and Adaptation

The performance of a VM-enabled R2R system hinges on the quality of the VM predictions. Of paramount importance is the **prediction bias**. If the VM model is biased, such that $\mathbb{E}[\hat{y}_k - y_k] = \beta \neq 0$, an integral-type R2R controller will force the true process output to a steady state that is offset from the target by $-\beta$. The controller cannot distinguish between a biased measurement and a true process error. Therefore, ensuring an unbiased VM predictor is critical for achieving accurate control.

Because the underlying process drifts, a static VM model trained on historical data will inevitably become biased over time. To maintain accuracy, the VM model must be **adaptive**. This typically involves periodically retraining or updating the model using the new physical [metrology](@entry_id:149309) data as it becomes available. This ensures the VM can track the same slow drifts that the R2R controller is designed to compensate for .

#### Advanced Control Strategies: Adapting to Measurement Quality

VM predictions are inherently more uncertain than physical measurements. A sophisticated R2R controller can account for this difference in quality. An optimal strategy involves adapting the [controller gain](@entry_id:262009) based on the source of the feedback.
-   When a precise physical measurement is available, a higher [controller gain](@entry_id:262009) can be used for aggressive [error correction](@entry_id:273762).
-   When a noisier VM prediction is used, a lower [controller gain](@entry_id:262009) is preferable to avoid amplifying the prediction error.

This gain-scheduling approach, which is analogous to how the Kalman filter gain adapts to measurement noise, can significantly reduce the overall output variance compared to using a single fixed gain for all runs . This highlights the deep synergy between estimation and control: the quality of the state information directly informs the [optimal control](@entry_id:138479) action. Similarly, advanced estimation schemes like the Kalman Filter can be designed to handle delayed measurements through techniques such as state augmentation or **Out-of-Sequence Measurement (OOSM)** processing, which retroactively update past state estimates when a delayed measurement arrives and propagate the correction forward to the present time .

Finally, it is important to recognize the challenge of **closed-loop identification**. The parameters of the process model itself (e.g., the drift parameter $\alpha$) are difficult to identify from output data alone, as the action of the controller masks the natural dynamics of the process. If the inputs $u_k$ are logged, however, it becomes possible to subtract their effect and analyze the residuals to identify the underlying disturbance dynamics, a crucial step for advanced [model-based control](@entry_id:276825) design .