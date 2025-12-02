## Introduction
In the pursuit of scientific discovery and engineering innovation, we increasingly rely on computational models to simulate complex realities. However, we constantly face a fundamental trade-off: the choice between highly accurate, "high-fidelity" simulations that consume immense computational resources, and fast, "low-fidelity" approximations that are quick but inherently biased. Simply choosing one over the other is often insufficient, creating a knowledge gap where we need both accuracy and speed. Multifidelity modeling provides the solution, offering a powerful framework to strategically combine information from these disparate sources. It treats the fast, biased model not as a poor substitute for the truth, but as a valuable scaffold upon which to build a more accurate, computationally affordable understanding.

This article explores the core concepts and widespread applications of this transformative methodology. In the "Principles and Mechanisms" chapter, we will dissect the mathematical and statistical engine that drives multifidelity modeling, from learning the model's error to making economically optimal decisions about [data acquisition](@entry_id:273490). Subsequently, the "Applications and Interdisciplinary Connections" chapter will showcase how these principles are applied in diverse fields, from quantum chemistry and [materials discovery](@entry_id:159066) to [climate science](@entry_id:161057) and the development of digital twins, illustrating the universal power of fusing information for smarter, faster science.

## Principles and Mechanisms

Imagine you are an explorer charting a vast, unknown mountain range. You have two tools at your disposal. The first is a blurry, low-resolution satellite map of the entire region. It’s cheap and fast to use, giving you a general sense of the terrain, but it misses all the crucial details—the cliffs, the crevices, the precise mountain peaks. Your second tool is a high-powered telescope. It’s incredibly expensive and time-consuming to set up, but wherever you point it, you see the landscape in perfect, crisp detail. How do you combine these two tools to create the best possible map of the entire range in the least amount of time?

This is the central question of **multifidelity modeling**. We live in a world of approximations. From forecasting the weather to designing a jet engine or discovering a new material, we rely on computational models. These models exist on a spectrum. **High-fidelity (HF)** models, like our telescope, are rooted in complex, fundamental physics—solving the full Navier-Stokes equations for fluid flow or running a quantum-mechanical simulation of a molecule. They are accurate but computationally ravenous, sometimes taking weeks or months for a single run. On the other end are **low-fidelity (LF)** models, like our blurry map. They use simplified physics, coarser computational grids, or empirical relationships. They are lightning-fast but systematically biased; they get the general trends right but are often quantitatively wrong.

The naive approach of simply averaging their outputs is doomed to fail. The low-fidelity model isn't just a noisy version of the high-fidelity one; it has its own inherent, [systematic errors](@entry_id:755765). The true art lies not in trusting the low-fidelity model's answers, but in exploiting its structure. The secret is to use the cheap model to quickly sketch the landscape's broad features and then use the expensive, high-fidelity model to learn and correct the cheap model's specific errors.

### Learning the Error: The First Principle of Fusion

The most powerful idea in multifidelity modeling is this: instead of trying to build a machine learning model that predicts the complex high-fidelity output $y_H$ from scratch, we build a model that predicts the *difference*, or **residual**, between the two models. We model the error itself.

Let's define this correction, often called $\Delta$ (delta), as:
$$
\Delta(\mathbf{x}) = y_H(\mathbf{x}) - y_L(\mathbf{x})
$$
where $\mathbf{x}$ represents the input parameters to our models. Our multifidelity prediction for the high-fidelity output, $\hat{y}_H$, then becomes:
$$
\hat{y}_H(\mathbf{x}) = y_L(\mathbf{x}) + \hat{\Delta}(\mathbf{x})
$$
where $\hat{\Delta}(\mathbf{x})$ is the output of our correction model. This approach, sometimes called **$\Delta$-learning** [@problem_id:3464186], transforms the problem. Instead of learning the full, complex physics of $y_H$, our machine learning task is to learn the much simpler structure of the error.

In some cases, this error can be captured by a very simple model. For instance, we might find that the high-fidelity result is roughly a scaled and shifted version of the low-fidelity one. This leads to a simple linear **[autoregressive model](@entry_id:270481)**:
$$
\hat{y}_H(\mathbf{x}) = \rho y_L(\mathbf{x}) + \delta(\mathbf{x})
$$
Here, $\rho$ is a scaling factor, and the new correction term $\delta(\mathbf{x})$ might be a simple polynomial function of the inputs, like $\delta(\mathbf{x}) = \beta_0 + \beta_1 x + \beta_2 x^2$ [@problem_id:2383126]. We can use a handful of paired $(y_L, y_H)$ simulations to find the best-fit values for $\rho$ and the $\beta$ coefficients using standard methods like linear regression.

However, the world is rarely so simple. In many real-world problems, especially in materials science or complex physics, the error is not a simple linear function. When we plot the true error $\Delta$ against the low-fidelity prediction $y_L$, we might see tell-tale signs of structure: curvature, clustering of data points by chemical family, or an error that grows larger as the prediction value increases [@problem_id:3464186]. These patterns are fingerprints of the "missing physics" in the low-fidelity model. In these cases, a simple linear correction is not enough. We need a more flexible, nonlinear machine learning model—like a neural network or a Gaussian process—to learn this complex error landscape.

It's crucial to understand what this approach is *not*. It is fundamentally different from a popular technique called **[transfer learning](@entry_id:178540)**, where a model trained on low-fidelity data is simply used as a starting point for [fine-tuning](@entry_id:159910) on high-fidelity data. In our fusion model, the low-fidelity prediction $y_L(\mathbf{x})$ remains an active and essential input to the final prediction at all times [@problem_id:3513277].

### The Statistician's Hammer: Control Variates and Co-Kriging

We can sharpen our "learning the error" intuition with the rigor of statistics. Suppose our goal is not to predict the entire function $y_H(\mathbf{x})$, but something simpler: its average value, or mean, $\mu_H = \mathbb{E}[H]$. The standard way is to run the expensive HF model $m$ times and take the average, $\bar{H}_m$. The uncertainty of this estimate decreases slowly, proportional to $1/\sqrt{m}$.

Here is where the low-fidelity model becomes a powerful statistical lever. We know that the LF model is biased, so $\mathbb{E}[L] \neq \mu_H$. However, because it captures some of the same underlying physics, its output $L$ is correlated with the HF output $H$. We can exploit this correlation.

Consider a quantity like $(\bar{L}_{m+n} - \bar{L}_m)$, where we've used $m$ LF runs that are paired with our HF runs, plus an extra $n$ cheap LF-only runs. Since both $\bar{L}_{m+n}$ and $\bar{L}_m$ are estimates of the same mean $\mathbb{E}[L]$, their difference has an average of zero. This means we can add it to our HF estimate without introducing any bias. This gives rise to the **[control variate](@entry_id:146594)** estimator [@problem_id:3581740]:
$$
\hat{\mu}_H = \bar{H}_m + \alpha(\bar{L}_{m+n} - \bar{L}_m)
$$
This looks like magic. How can adding a zero-mean term help? The term we added, $(\bar{L}_{m+n} - \bar{L}_m)$, is correlated with our original estimator $\bar{H}_m$. By choosing the coefficient $\alpha$ cleverly, we can make it so that when $\bar{H}_m$ happens to be a high-side error, the correction term is likely to be negative, and vice-versa. We use the randomness in the cheap model to cancel out the randomness in the expensive one. The optimal choice for $\alpha$ turns out to be $\alpha^\star = \operatorname{Cov}(H, L) / \operatorname{Var}(L)$. With this choice, the variance of our new estimate is reduced by a factor of approximately $(1 - \rho^2)$, where $\rho$ is the [correlation coefficient](@entry_id:147037) between the high- and low-fidelity models. If the models are highly correlated ($\rho \to 1$), the uncertainty in our estimate collapses dramatically. We get a much more precise answer for the same number of expensive simulations.

This idea can be generalized from estimating a single mean value to learning the entire function. This is the domain of **[co-kriging](@entry_id:747413)**, which uses **Gaussian Processes (GPs)** to put the [autoregressive model](@entry_id:270481) $f_H(\mathbf{x}) = \rho f_L(\mathbf{x}) + \delta(\mathbf{x})$ on a fully probabilistic footing [@problem_id:3352833]. In this framework, we treat the low-fidelity function $f_L(\mathbf{x})$ and the discrepancy function $\delta(\mathbf{x})$ as random functions drawn from a GP prior. A GP is a flexible model that can define a distribution over functions, characterized by a mean and a [covariance kernel](@entry_id:266561) that describes how smooth the function is and how its values at different points are related.

By combining the HF and LF data within this single probabilistic model, we can make predictions for $f_H(\mathbf{x})$ at new, untried locations. The information from the dense, cheap LF data helps "fill in the gaps" between the sparse, expensive HF data points, dramatically reducing our uncertainty. This is not just a theoretical benefit; in practical applications like predicting nuclear mass properties, adding low-fidelity data can slash the predictive variance of the model [@problem_id:3568164].

A key insight from this framework is the importance of having at least some **co-located samples**—input points where we have run *both* the low- and high-fidelity simulations. These paired data points are essential for the model to learn the crucial scaling parameter $\rho$. Without them, the model can get confused, unable to distinguish whether a change in the high-fidelity output is due to the influence of the low-fidelity function or the discrepancy term. Co-located points anchor the relationship between the two fidelities and allow for a robust fusion of the information [@problem_id:3352833] [@problem_id:3369157].

### The Economic Engine: Smart Data Acquisition

So far, we have seen how to combine existing data from different models. But in many scientific endeavors, we are actively deciding what to do next. Should we run another expensive DFT simulation, or should we run a thousand fast classical potential calculations? This is a question of economics.

Multifidelity models provide a rational basis for making this decision. The goal of a new simulation is to gain information—to reduce the uncertainty in our model. But each simulation has a cost. The optimal strategy, therefore, is to choose the simulation that provides the maximum **[expected information gain](@entry_id:749170) per unit cost** [@problem_id:2837946].

Using a probabilistic model like [co-kriging](@entry_id:747413), we can mathematically calculate the expected reduction in our predictive variance at a target location that would result from acquiring a new piece of data—either a new low-fidelity point or a new high-fidelity point. For example, the expected reduction in variance of $f_H(\mathbf{x}_\star)$ from observing $y_L(\mathbf{x}_c)$ is given by:
$$
\mathcal{V}_{L}(\mathbf{x}_{c}) = \frac{\operatorname{Cov}(f_H(\mathbf{x}_\star), y_L(\mathbf{x}_c))^{2}}{\operatorname{Var}(y_L(\mathbf{x}_c))}
$$
We can compute a similar value, $\mathcal{V}_{H}(\mathbf{x}_{c})$, for a high-fidelity observation. We then simply compare the ratios $\mathcal{V}_{L}/c_{L}$ and $\mathcal{V}_{H}/c_{H}$, where $c_L$ and $c_H$ are the respective costs. We choose the fidelity that offers the biggest "bang for the buck." This logic forms the core of multifidelity **Bayesian optimization** and **[active learning](@entry_id:157812)** algorithms, which intelligently guide the search for new materials or optimal designs by always making the most economically sound choice about what data to acquire next.

### A Unified View of Reality and Models

The principles of multifidelity modeling extend far beyond just combining two computer simulations. They offer a profound, unified framework for thinking about the relationship between models and reality itself.

Think of the hierarchy of information we deal with in science:
1.  **Physical Reality**: The ultimate, infinitely complex "high-fidelity" truth.
2.  **Physics Model**: Our best mathematical description of reality (e.g., a set of PDEs). This is a low-fidelity approximation of reality. The difference between its predictions and reality is the **structural [model discrepancy](@entry_id:198101)**.
3.  **Numerical Solution**: The solution of our physics model on a computer with a finite mesh. A coarse mesh is a lower-fidelity approximation of the continuum PDE solution on a fine mesh. The difference is the **[discretization error](@entry_id:147889)**.
4.  **Experimental Data**: Our noisy measurements of physical reality. The difference between a measurement and the true physical quantity is **instrument noise**.

A comprehensive **Uncertainty Quantification (UQ)** framework must account for all these sources of error and uncertainty. And it does so using the very same principles we have just explored [@problem_id:3618097]. We can use replicate measurements to characterize the instrument noise. We can use [mesh refinement](@entry_id:168565) studies (treating coarse and fine meshes as different fidelities) to characterize and extrapolate away the discretization error. And we can use a rich set of experimental data to calibrate our physics model's parameters while simultaneously modeling the remaining structural discrepancy.

Viewed through this lens, multifidelity modeling is not just a clever computational trick. It is a fundamental scientific methodology for navigating the inescapable ladder of approximations that connects our abstract theories to concrete, messy reality. It provides a disciplined, quantitative language for understanding what our models know, what they don't know, and how to combine all sources of information—from the fastest, cheapest approximation to the most expensive experiment—into our single best picture of the world.