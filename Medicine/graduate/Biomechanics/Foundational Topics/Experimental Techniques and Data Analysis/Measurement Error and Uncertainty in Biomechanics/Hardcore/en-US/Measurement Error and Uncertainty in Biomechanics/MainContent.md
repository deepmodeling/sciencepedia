## Introduction
The pursuit of biomechanical knowledge is built upon the act of measurement. From quantifying human movement to modeling [cellular forces](@entry_id:1122181), our understanding is fundamentally limited by the fidelity of our data. To treat measured values as absolute truth is a critical scientific failing; a rigorous biomechanical analysis demands a deep and practical understanding of measurement error and uncertainty. This article addresses the gap between data collection and credible interpretation by providing a systematic framework for characterizing, quantifying, and managing uncertainty in biomechanical research.

Across the following chapters, you will build a comprehensive skill set for robust data analysis. The journey begins in **Principles and Mechanisms**, which lays the theoretical groundwork, defining fundamental concepts like accuracy, precision, bias, and [random error](@entry_id:146670), and introducing formal frameworks like the Guide to the Expression of Uncertainty in Measurement (GUM). Next, **Applications and Interdisciplinary Connections** demonstrates how these principles are applied in practice, from calibrating laboratory equipment and mitigating [soft tissue artifact](@entry_id:1131864) to validating complex computational models and fusing multimodal data. Finally, **Hands-On Practices** provides practical exercises to solidify your understanding, challenging you to calculate reliability, manage data instability, and implement formal uncertainty analysis. By navigating these topics, you will learn not just to identify error, but to control it, ensuring your scientific conclusions are both valid and defensible.

## Principles and Mechanisms

The pursuit of biomechanical knowledge is inextricably linked to the act of measurement. Whether quantifying the kinematics of human movement, the forces exchanged with the environment, or the physiological signals driving muscle contraction, our understanding is bounded by the fidelity of our measurements. An uncritical acceptance of measured values as truth is scientifically untenable. A rigorous biomechanical analysis, therefore, demands a deep understanding of the principles and mechanisms of measurement error and uncertainty. This chapter provides a systematic foundation for this understanding, moving from the fundamental [taxonomy](@entry_id:172984) of errors to their propagation through complex analyses and advanced frameworks for their characterization.

### Fundamental Taxonomy of Measurement Error

At the most basic level, measurement error describes the discrepancy between a measured value and the true value of the quantity of interest, or **measurand**. To formalize this, let us denote the true value of a quantity as $\theta_{\text{true}}$ and an estimate derived from a measurement process as $\hat{\theta}$. Because of various stochastic influences, we can treat $\hat{\theta}$ as a random variable. The total error, $\epsilon = \hat{\theta} - \theta_{\text{true}}$, can be decomposed into two fundamental, orthogonal components: systematic error and random error.

#### Accuracy, Precision, Bias, and Random Error

The concepts of accuracy, precision, bias, and random error form the cornerstone of [metrology](@entry_id:149309). Their precise definitions are rooted in probability theory.

**Bias**, or [systematic error](@entry_id:142393), is the difference between the expected value of our estimator and the true value. It represents a consistent, repeatable offset that does not diminish by simply taking more measurements under the same conditions. Mathematically, the bias is defined as:
$$
\text{Bias}[\hat{\theta}] = \mathbb{E}[\hat{\theta}] - \theta_{\text{true}}
$$
An estimator is said to be **unbiased** if its bias is zero. For example, in optical [motion capture](@entry_id:1128204), a small but consistent misplacement of a marker cluster on the thigh will produce a nearly constant offset in the estimated knee flexion angle throughout a [gait cycle](@entry_id:1125450). This offset, which persists across repeated trials, is a classic example of a measurement bias .

**Random error**, in contrast, is the stochastic deviation of a single measurement from the expected value of the measurement process. It is the unpredictable, zero-mean variability observed in repeated measurements. The [random error](@entry_id:146670) component, $\eta$, is given by:
$$
\eta = \hat{\theta} - \mathbb{E}[\hat{\theta}]
$$
By definition, the expected value of the [random error](@entry_id:146670) is zero, $\mathbb{E}[\eta] = 0$. In optical motion capture, sources like frame-to-frame electronic noise in the camera sensors and algorithmic variability in marker [centroid](@entry_id:265015) detection introduce "jitter" into the reconstructed marker positions. This jitter represents a random error; it increases the variability of the knee angle estimate, $\hat{\theta}(t)$, without systematically shifting its average value .

These two error components directly inform the concepts of [precision and accuracy](@entry_id:175101).

**Precision** refers to the consistency or reproducibility of a measurement, specifically the closeness of repeated measurements to each other. It is therefore a measure of the magnitude of **[random error](@entry_id:146670)**. High precision implies low [random error](@entry_id:146670). A common [quantifier](@entry_id:151296) for imprecision is the variance of the estimator, $\text{Var}[\hat{\theta}] = \mathbb{E}[(\hat{\theta} - \mathbb{E}[\hat{\theta}])^2] = \mathbb{E}[\eta^2]$. It is critical to recognize that precision is independent of bias. A measurement can be highly precise (low variance) yet highly biased, like a rifle that consistently hits the same spot 10 centimeters to the left of the bullseye.

**Accuracy** refers to the closeness of a measurement to the true value. It is a holistic concept that is affected by **both** systematic and random errors. A measurement cannot be accurate if it is biased, nor can it be accurate if it is imprecise. A common metric for inaccuracy is the **Mean Squared Error (MSE)**, which is the expected value of the squared total error:
$$
\text{MSE}[\hat{\theta}] = \mathbb{E}[(\hat{\theta} - \theta_{\text{true}})^2]
$$
A fundamental result in statistics, known as the [bias-variance decomposition](@entry_id:163867), shows that the MSE is the sum of the squared bias and the variance:
$$
\text{MSE}[\hat{\theta}] = (\text{Bias}[\hat{\theta}])^2 + \text{Var}[\hat{\theta}]
$$
This decomposition makes it clear that to achieve high accuracy (low MSE), one must minimize both bias and random error. A measurement with a large systematic offset (e.g., the misplaced marker cluster causing a $5^\circ$ bias) has poor accuracy, even if its trial-to-trial variability is negligible (high precision) .

#### Practical Separation of Systematic and Random Errors

The conceptual distinction between systematic and [random errors](@entry_id:192700) is made operational through experimental design. A canonical method involves repeated measurements of a known, stable quantity—a process central to instrument calibration. Consider the calibration of a force plate using a known static load . If a known weight $W$ is placed on the plate, the true vertical ground reaction force is $\mathbf{F}^{*} = (0, 0, W)$. If we perform $N$ repeated measurements, $\mathbf{Y}_i$, the systematic error (bias) can be estimated by comparing the [sample mean](@entry_id:169249) of the measurements, $\bar{\mathbf{Y}} = \frac{1}{N}\sum_{i=1}^{N}\mathbf{Y}_i$, to the true value $\mathbf{F}^{*}$. The estimated bias is $\hat{\mathbf{\beta}} = \bar{\mathbf{Y}} - \mathbf{F}^{*}$.

The magnitude of the [random error](@entry_id:146670) is estimated from the variability across the repeated trials. The [sample variance](@entry_id:164454) of the measurements, $s^2 = \frac{1}{N-1}\sum_{i=1}^{N}(\mathbf{Y}_i - \bar{\mathbf{Y}})^2$, provides an estimate of the variance of the random error component. This procedure highlights a crucial point: averaging $N$ independent measurements reduces the variance of the *average* by a factor of $N$ (and the standard deviation by $\sqrt{N}$), thereby improving precision. However, averaging has no effect on the systematic error; the bias of the average is the same as the bias of a single measurement.

Common sources of systematic error in biomechanics include instrument miscalibration (e.g., incorrect gain on a force plate amplifier), consistent errors in experimental setup (e.g., misalignment of a force plate's axes with the lab's coordinate system), or flaws in the underlying physical model. Common sources of [random error](@entry_id:146670) include thermal noise in electronics, [quantization noise](@entry_id:203074) from [analog-to-digital conversion](@entry_id:275944), and unpredictable biological fluctuations such as [soft tissue artifact](@entry_id:1131864) (STA) in motion capture, where skin-mounted markers move relative to the underlying bone in a way that varies from trial to trial  .

### Quantifying Measurement System Performance

Beyond the fundamental error types, we need standardized metrics to characterize and compare the performance of measurement systems, especially in clinical or multi-center studies. These metrics extend the concepts of [precision and accuracy](@entry_id:175101) to account for different sources of variability inherent in a complete measurement protocol.

#### Repeatability, Reproducibility, and Reliability

These three terms describe measurement consistency under increasingly variable conditions and are formally defined within a [variance components](@entry_id:267561) framework . Imagine a study measuring knee angles where multiple trials are collected within a session, and participants are re-tested in a second session on a different day, perhaps even by a different examiner. A [linear mixed-effects model](@entry_id:908618) can partition the total observed variance into its sources:
$$
\sigma_{\text{total}}^2 = \sigma_{\text{subject}}^2 + \sigma_{\text{rater}}^2 + \sigma_{\text{session}}^2 + \sigma_{\text{trial}}^2
$$
Here, $\sigma_{\text{subject}}^2$ represents the "true" biological variability between subjects, while the other terms represent different sources of measurement error.

**Repeatability** refers to the variability of measurements taken under the most constant conditions possible: the same subject, same instrument, same lab, same rater, over a short period. Under these conditions, the only source of variation is the within-session trial-to-trial noise, quantified by $\sigma_{\text{trial}}^2$. The repeatability limit, often defined as $1.96 \sqrt{2} \sigma_{\text{trial}}$, quantifies the expected difference between two single measurements taken under such conditions.

**Reproducibility** refers to the variability when one or more conditions are changed. For example, if measurements are taken on the same subject but on different days and by different raters, the relevant [error variance](@entry_id:636041) is the sum of the contributing variances: $\sigma_{\text{reproducibility}}^2 = \sigma_{\text{rater}}^2 + \sigma_{\text{session}}^2 + \sigma_{\text{trial}}^2$. The reproducibility limit will be correspondingly larger than the repeatability limit, reflecting the additional sources of uncertainty.

**Reliability** is a distinct concept that assesses the ability of a measurement to distinguish between subjects, despite the presence of measurement error. It is quantified as the proportion of the total observed variance that is attributable to true between-subject differences. The most common metric is the **Intraclass Correlation Coefficient (ICC)**:
$$
\text{ICC} = \frac{\sigma_{\text{subject}}^2}{\sigma_{\text{subject}}^2 + \sigma_{\text{error}}^2}
$$
The $\sigma_{\text{error}}^2$ term is composed of all [variance components](@entry_id:267561) considered to be measurement error for the specific protocol. For instance, for a test-retest protocol with the same rater, the error would include session and trial variability. The ICC ranges from 0 to 1, with higher values indicating that a greater fraction of the observed variation is "signal" (true differences between subjects) rather than "noise" (measurement error). An ICC of $0.94$, for instance, indicates excellent reliability, suggesting that 94% of the measured variance reflects genuine differences among individuals .

From the error variance, we can also derive clinically important metrics like the **Standard Error of Measurement (SEM)**, defined as $\text{SEM} = \sqrt{\sigma_{\text{error}}^2}$. The SEM quantifies the absolute measurement error in the original units of the measurement. This, in turn, is used to calculate the **Minimal Detectable Change (MDC)**, often at 95% confidence: $\text{MDC}_{95} = 1.96 \sqrt{2} \times \text{SEM}$. The MDC represents the smallest change in a measured score that can be considered a "real" change, beyond the expected noise of the measurement, providing a crucial benchmark for assessing interventions.

#### Uncertainty Evaluation according to GUM: Type A and Type B

The *Guide to the Expression of Uncertainty in Measurement (GUM)* provides an internationally recognized framework for classifying and combining uncertainty components. It distinguishes not between the nature of the uncertainties themselves, but by the *method of their evaluation*.

A **Type A evaluation of uncertainty** is performed by the statistical analysis of a series of observations. The standard uncertainty is typically the experimental standard deviation of the mean of a set of repeated measurements. In our force plate calibration example, the random fluctuations of the readings around their mean give rise to a Type A uncertainty component. If the standard deviation of $n=20$ readings is $s=0.30\,\text{N}$, the Type A standard uncertainty of the mean is $u_A = s/\sqrt{n} \approx 0.067\,\text{N}$ .

A **Type B evaluation of uncertainty** is performed by means other than direct statistical analysis of the current series of observations. This evaluation is based on available information, such as calibration certificates for reference standards, manufacturer's specifications, data from previous measurements, or physical models. In the force plate calibration, the reference force is generated by a calibrated mass ($m$) under local gravity ($g$). The uncertainty in the mass is stated on its NIST-traceable certificate, and the uncertainty in the local value of $g$ comes from a geodetic model. Both of these are Type B uncertainty components.

Once evaluated, all standard uncertainty components, regardless of their evaluation method, are treated as equivalent and combined to produce a **combined standard uncertainty**. For independent sources, this is done using a root-sum-of-squares approach. In a high-quality calibration, the Type B uncertainties from the reference standards often dominate. For instance, the combined uncertainty from the mass certificate and gravity model might be $u_B \approx 0.102\,\text{N}$, which is larger than the Type A repeatability of the force plate itself. This illustrates that the quality of the reference standards can set a fundamental floor on the best achievable measurement uncertainty .

### Error Propagation and Signal Processing Artifacts

In biomechanics, we rarely use raw measured data directly. Instead, data is processed through chains of calculations—differentiation, integration, filtering—to derive kinetic and kinematic variables. Understanding how errors arise and propagate through these pipelines is critical.

#### Noise Amplification through Numerical Differentiation

Many key biomechanical quantities, such as velocity, acceleration, and [joint power](@entry_id:1126840), are calculated by numerically differentiating [time-series data](@entry_id:262935) (e.g., marker positions). Differentiation is fundamentally a high-pass operation that amplifies high-frequency noise.

Consider estimating ankle [joint power](@entry_id:1126840) during the swing phase, modeled as $P(t) = I \alpha(t) \omega(t)$, where $I$ is the moment of inertia, $\omega$ is angular velocity, and $\alpha$ is angular acceleration. Both $\omega$ and $\alpha$ are estimated by numerically differentiating the measured joint angle, $\hat{\theta}_k$. If the measured angle at each time step $k$ has independent Gaussian noise with variance $\sigma_\theta^2$, we can analyze how this noise propagates through the common [second-order central difference](@entry_id:170774) formulas :
$$
\hat{\omega}_k = \frac{\hat{\theta}_{k+1} - \hat{\theta}_{k-1}}{2\Delta t}, \quad \hat{\alpha}_k = \frac{\hat{\theta}_{k+1} - 2\hat{\theta}_k + \hat{\theta}_{k-1}}{\Delta t^2}
$$
The variance of the resulting noise in the velocity and acceleration estimates can be shown to be:
$$
\text{Var}(\text{noise in } \hat{\omega}_k) = \frac{2\sigma_\theta^2}{(2\Delta t)^2} = \frac{\sigma_\theta^2}{2\Delta t^2}
$$
$$
\text{Var}(\text{noise in } \hat{\alpha}_k) = \frac{(1^2 + (-2)^2 + 1^2)\sigma_\theta^2}{(\Delta t^2)^2} = \frac{6\sigma_\theta^2}{\Delta t^4}
$$
This analysis reveals a critical vulnerability: the noise variance in the acceleration estimate scales inversely with the *fourth power* of the sampling interval, $\Delta t$. Halving the time step (doubling the [sampling frequency](@entry_id:136613)) increases the noise variance in the acceleration estimate by a factor of 16. This amplified noise propagates into the final power calculation, where the variance of the power error will have terms proportional to $1/\Delta t^2$ and $1/\Delta t^4$. This demonstrates the extreme sensitivity of inverse dynamics calculations to measurement noise and highlights the essential role of appropriate low-pass filtering of kinematic data before differentiation.

#### Error Accumulation through Numerical Integration

The inverse problem occurs with integration. While differentiation amplifies noise, integration suppresses it but accumulates [systematic errors](@entry_id:755765). This is a central challenge in inertial navigation, such as when using a foot-mounted Inertial Measurement Unit (IMU) to track position.

An IMU's accelerometer measures true acceleration $a(t)$ corrupted by a bias $b_a$ and random noise $n_a(t)$. To get position, this signal must be integrated twice. Even a small, constant bias $b_a$ will cause a velocity error that grows linearly in time ($e_v(t) = b_a t$) and a position error that grows quadratically ($e_p(t) = \frac{1}{2} b_a t^2$) . This rapid [error accumulation](@entry_id:137710) makes unaided inertial navigation impossible over long durations.

In pedestrian applications, the problem can be managed by exploiting the cyclical nature of gait. During the stance phase of walking, the foot is momentarily stationary. This provides a reliable event, known as a **Zero-Velocity Update (ZUPT)**, to correct the drift. A "hard ZUPT" that simply resets the estimated velocity to zero at each step can prevent quadratic error growth, but the position error will still grow linearly over time. A more sophisticated approach uses a **Kalman filter**. This [recursive algorithm](@entry_id:633952) maintains an estimate of the system's state (including position, velocity, and the bias itself) and uses the ZUPT as a periodic measurement to correct the state estimates. By estimating and subtracting the bias, the Kalman filter suppresses the deterministic drift, leaving only a residual random-walk-like error in position whose variance grows much more slowly (linearly with time).

#### Aliasing: The Peril of Undersampling

A particularly insidious signal processing artifact is **aliasing**. It occurs when a [continuous-time signal](@entry_id:276200) is sampled at a rate that is too low to capture its high-frequency content. The **Nyquist-Shannon [sampling theorem](@entry_id:262499)** states that to perfectly reconstruct a signal, the sampling frequency, $f_s$, must be strictly greater than twice the maximum frequency present in the signal, $f_{\text{max}}$. The frequency $f_s/2$ is known as the **Nyquist frequency**.

If a signal contains a frequency component $f_i$ that is higher than the Nyquist frequency, it will be "aliased"—it will masquerade as a lower-frequency component in the sampled data. This artifact is irreversible; once the signal is sampled, the aliased component is indistinguishable from a true signal at that lower frequency, and no amount of post-hoc [digital filtering](@entry_id:139933) can recover the original information .

A classic biomechanics example is the [ground reaction force](@entry_id:1125827) (GRF) during heel-strike in running. The initial impact can generate a high-frequency transient. For instance, a physical oscillation at $f_i=180\,\text{Hz}$ in the GRF, if sampled by a force plate at $f_s=200\,\text{Hz}$, will be aliased. The Nyquist frequency is $f_s/2=100\,\text{Hz}$. The $180\,\text{Hz}$ signal, being above the Nyquist frequency, will "fold" back into the baseband, appearing as a spurious signal at a frequency of $f_a = f_s - f_i = 200 - 180 = 20\,\text{Hz}$. This spurious $20\,\text{Hz}$ oscillation, which has no physiological basis, will then contaminate any subsequent inverse dynamics calculations, such as the ankle joint moment.

The only effective prevention for aliasing is to use an **analog [anti-aliasing filter](@entry_id:147260)** to remove all frequencies above the Nyquist frequency *before* the signal reaches the [analog-to-digital converter](@entry_id:271548).

### Advanced Perspectives on Uncertainty

As biomechanical models and analyses grow in complexity, so too must our frameworks for understanding uncertainty. The following sections introduce more nuanced perspectives that are essential for contemporary research.

#### Aleatory vs. Epistemic Uncertainty

A powerful conceptual distinction can be made between two fundamental types of uncertainty.

**Aleatory uncertainty** (also known as statistical uncertainty) is the inherent, irreducible randomness of a system or phenomenon. It reflects the variability that would remain even with perfect knowledge of the system's parameters. A canonical example is the stochastic nature of motor unit firing patterns. Even under identical isometric contraction conditions, the precise timing of inter-spike intervals will vary from trial to trial. This is a fundamental property of the neuromuscular system .

**Epistemic uncertainty** (also known as [systematic uncertainty](@entry_id:263952)) arises from a lack of knowledge. It is uncertainty about the true values of fixed model parameters or the correct form of the model itself. In optical [motion capture](@entry_id:1128204), the exact values of [camera calibration](@entry_id:1121998) constants are fixed during a trial but may be unknown to the experimenter; this lack of knowledge is epistemic uncertainty . Similarly, in surface EMG, the precise anatomical and electrical properties of the tissues that determine how signals from different muscles mix (cross-talk) are unknown parameters, contributing epistemic uncertainty .

The critical difference is that **epistemic uncertainty can, in principle, be reduced by acquiring more information**. Better calibration procedures reduce uncertainty in camera parameters. Using high-density EMG arrays or concurrent [ultrasound imaging](@entry_id:915314) can provide more information to better estimate the cross-talk mixing matrix. In contrast, [aleatory uncertainty](@entry_id:154011) cannot be reduced by gaining more knowledge about the system's fixed parameters. Averaging across many trials can reduce our uncertainty *about the mean* of the aleatory process, but it does not eliminate the inherent variability of any single trial.

This distinction can be formalized using the law of total variance. For an outcome $Y$ that depends on parameters $\theta$, the total variance is $\text{Var}(Y) = \mathbb{E}[\text{Var}(Y|\theta)] + \text{Var}[\mathbb{E}(Y|\theta)]$. The first term represents the aleatory uncertainty (the average intrinsic variance), while the second term represents the epistemic uncertainty (the variance in the mean prediction due to uncertainty in $\theta$).

#### Errors-in-Variables and Model Misspecification

Standard statistical models like Ordinary Least Squares (OLS) regression rest on a set of core assumptions. One of the most frequently violated assumptions in biomechanics is that the predictor variables (or regressors) are measured without error. When this assumption is false, we have an **[errors-in-variables](@entry_id:635892) (EIV)** problem.

Consider the estimation of a biomechanical scaling law, such as the relationship between muscle torque ($T$) and body mass ($M$), often linearized by taking logarithms: $\log(T) = \beta_0 + \beta_1 \log(M) + \epsilon$. Here, we regress log-torque on log-mass to estimate the [scaling exponent](@entry_id:200874) $\beta_1$. However, body mass is not measured perfectly; the measured mass has some error. When we perform OLS regression using the noisy log-mass measurement as our predictor, the resulting estimate of the slope $\beta_1$ will be biased .

Specifically, under the classical assumption that the measurement error is independent of the true value, the presence of error in the predictor variable causes **[attenuation bias](@entry_id:746571)**: the estimated slope will be systematically biased towards zero. The magnitude of this bias depends on the "reliability ratio," which is the ratio of the variance of the true predictor to the variance of the measured predictor. The more noise in the predictor, the more the slope estimate is attenuated. This bias is **inconsistent**, meaning it does not disappear even with an infinitely large sample size. This is a critical issue that can lead to erroneous scientific conclusions about [scaling relationships](@entry_id:273705). Overcoming it requires specialized statistical methods, such as Deming regression (if the error variances are known), [instrumental variables](@entry_id:142324) regression, or [total least squares](@entry_id:170210).

#### Structural vs. Practical Identifiability in Models

In complex physiological models, such as musculoskeletal models used to estimate muscle forces, we face the challenge of **parameter identifiability**. This concept asks whether it is possible to uniquely determine the values of a model's parameters from experimental data .

**Structural identifiability** is a theoretical property of the model and the experimental design, assessed assuming ideal, noise-free data. A parameter is structurally identifiable if it has a unique value that can reproduce the experimental outputs. It is structurally non-identifiable if multiple different parameter values (or combinations of values) produce the exact same model output. For example, in a simple musculoskeletal model used to predict isometric joint torque, if the only measurement is torque at a single joint angle, it may be impossible to uniquely distinguish the effects of tendon slack length ($L_{ts}$) and optimal fiber length ($L_0$). Infinitely many pairs of ($L_{ts}, L_0$) might produce the same torque output, making both parameters structurally non-identifiable from this experiment.

**Practical identifiability**, in contrast, is a practical concern related to the quality and quantity of real, noisy data. A parameter might be structurally identifiable in theory, but if the experimental data is very noisy, or if the model's output is very insensitive to changes in that parameter, it may be practically impossible to estimate it with any reasonable precision. Its [confidence interval](@entry_id:138194) will be enormous. Practical identifiability is typically assessed by examining the sensitivity of the model output to each parameter or by analyzing the curvature of the parameter estimation cost function, often formalized via the Fisher Information Matrix. An experimental design that makes a parameter structurally identifiable (e.g., adding ultrasound measurements to directly observe fiber length) is the first and most crucial step, but ensuring [practical identifiability](@entry_id:190721) requires careful consideration of measurement noise and experimental protocols.

#### Two Philosophies of Inference: Frequentist vs. Bayesian Intervals

Finally, when reporting the uncertainty of a parameter estimate, it is important to be aware of the two major schools of statistical inference—Frequentist and Bayesian—as they provide different types of [uncertainty intervals](@entry_id:269091) with fundamentally different interpretations .

A **Frequentist [confidence interval](@entry_id:138194)** is the most common type of interval reported in scientific literature. A 95% [confidence interval](@entry_id:138194) is an interval generated by a procedure that, over an infinite number of repeated experiments, would contain the true, fixed value of the parameter 95% of the time. The probability statement applies to the procedure, not the specific interval calculated from your data. Once calculated, a given interval either contains the true parameter or it does not. It is incorrect to say there is a 95% probability that the true parameter lies within your specific calculated confidence interval.

A **Bayesian [credible interval](@entry_id:175131)**, on the other hand, is a direct statement of probabilistic belief. The Bayesian framework treats the parameter itself as a random variable about which we can have a state of knowledge, described by a probability distribution. This "posterior" distribution is obtained by updating a "prior" belief distribution with the evidence from the data via Bayes' theorem. A 95% [credible interval](@entry_id:175131) is an interval that, given the data and the model, contains the parameter with 95% probability. It is perfectly valid to state that there is a 95% probability that the true parameter lies within a 95% [credible interval](@entry_id:175131).

Numerically, the two intervals can be identical in certain simple cases (e.g., for the mean in a Gaussian model with a "flat" or [non-informative prior](@entry_id:163915)). However, when an informative prior is used in the Bayesian analysis, the [credible interval](@entry_id:175131) will be "pulled" towards the [prior belief](@entry_id:264565) and will differ from the confidence interval, which is determined solely by the data. Recognizing this distinction is essential for the correct interpretation and communication of statistical uncertainty.