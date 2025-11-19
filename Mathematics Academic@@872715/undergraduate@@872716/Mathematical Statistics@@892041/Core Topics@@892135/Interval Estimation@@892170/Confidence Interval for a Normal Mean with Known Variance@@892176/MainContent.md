## Introduction
In [statistical inference](@entry_id:172747), a single [point estimate](@entry_id:176325) like the [sample mean](@entry_id:169249) provides our best guess for a population parameter, but it fails to convey the uncertainty inherent in that estimate. To quantify this uncertainty and provide a plausible range for the true value, we turn to [interval estimation](@entry_id:177880). The [confidence interval](@entry_id:138194) is the most fundamental tool for this purpose, offering a rigorous way to express the precision of our findings. This article addresses the core problem of how to construct and interpret such an interval for a [population mean](@entry_id:175446).

This article provides a comprehensive guide to the confidence interval for a normal mean under the foundational assumption that the population variance is known. First, in "Principles and Mechanisms," you will learn the theoretical underpinnings, including the [pivotal quantity](@entry_id:168397) approach for deriving the interval, the correct [frequentist interpretation](@entry_id:173710), and the factors that control the interval's width. Next, "Applications and Interdisciplinary Connections" will bridge theory and practice, exploring how this tool is used for quality control, experimental design, and evidence synthesis across fields from engineering to medicine, and revealing its deep connection to hypothesis testing. Finally, "Hands-On Practices" will allow you to solidify your understanding by actively calculating, interpreting, and validating [confidence intervals](@entry_id:142297) in realistic scenarios.

## Principles and Mechanisms

In the pursuit of statistical inference, our objective often transcends the mere calculation of a single point estimate for an unknown parameter. While a point estimate, such as the sample mean, provides a "best guess" for a population parameter like the true mean $\mu$, it offers no information about the uncertainty or precision associated with that guess. To address this, we turn to [interval estimation](@entry_id:177880), and specifically, the construction of a **confidence interval**. This chapter delineates the fundamental principles and mechanics of constructing a confidence interval for the mean of a [normal distribution](@entry_id:137477) under the simplifying, yet foundational, assumption that the population variance is known.

### The Pivotal Quantity Approach

The cornerstone of constructing a confidence interval in a frequentist framework is the identification of a **[pivotal quantity](@entry_id:168397)**, or simply a **pivot**. A pivot is a function of the observable sample data and the unknown parameter of interest whose probability distribution is completely known and does not depend on the unknown parameter itself. This property allows us to make precise probability statements that can be inverted to yield an interval for the parameter.

Let us consider a random sample $X_1, X_2, \ldots, X_n$ drawn from a normal population with an unknown mean $\mu$ and a known variance $\sigma^2$, denoted as $X_i \sim \mathcal{N}(\mu, \sigma^2)$. The most intuitive estimator for $\mu$ is the [sample mean](@entry_id:169249), $\bar{X} = \frac{1}{n} \sum_{i=1}^{n} X_i$. From the [properties of the normal distribution](@entry_id:273225), we know that the [sampling distribution](@entry_id:276447) of $\bar{X}$ is also normal:
$$
\bar{X} \sim \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right)
$$
This distribution, however, still depends on the unknown $\mu$, so $\bar{X}$ itself is not a pivot. To create one, we standardize $\bar{X}$. By subtracting its mean ($\mu$) and dividing by its standard deviation ($\sigma/\sqrt{n}$), we obtain the quantity $Z$:
$$
Z = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}}
$$
This [transformed random variable](@entry_id:198807) $Z$ follows the [standard normal distribution](@entry_id:184509), $\mathcal{N}(0, 1)$, regardless of the true value of $\mu$. Thus, $Z$ is a perfect [pivotal quantity](@entry_id:168397) for this problem.

### Constructing the Confidence Interval

With the pivot $Z \sim \mathcal{N}(0, 1)$ established, we can construct an interval for $\mu$. The goal is to create an interval that will contain $\mu$ with a specified probability, known as the **[confidence level](@entry_id:168001)**, denoted by $1-\alpha$. The value $\alpha$ represents the probability of error, or the chance that our interval will *fail* to capture the true mean [@problem_id:1906423].

For a symmetric, two-sided confidence interval, we seek values that bound the central $1-\alpha$ portion of the [standard normal distribution](@entry_id:184509). We denote the upper critical value as $z_{\alpha/2}$, which is the value such that the area in the upper tail is $\alpha/2$; that is, $\mathbb{P}(Z > z_{\alpha/2}) = \alpha/2$. By the symmetry of the [standard normal distribution](@entry_id:184509), the lower critical value is $-z_{\alpha/2}$, with $\mathbb{P}(Z  -z_{\alpha/2}) = \alpha/2$. This leads to the central probability statement:
$$
\mathbb{P}(-z_{\alpha/2} \leq Z \leq z_{\alpha/2}) = 1 - \alpha
$$
Substituting our pivot into this expression gives:
$$
\mathbb{P}\left(-z_{\alpha/2} \leq \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \leq z_{\alpha/2}\right) = 1 - \alpha
$$
The crucial step is to algebraically rearrange the inequalities to isolate the parameter $\mu$ in the center. This process does not change the probability of the event.
$$
-z_{\alpha/2} \frac{\sigma}{\sqrt{n}} \leq \bar{X} - \mu \leq z_{\alpha/2} \frac{\sigma}{\sqrt{n}}
$$
$$
-\bar{X} - z_{\alpha/2} \frac{\sigma}{\sqrt{n}} \leq - \mu \leq -\bar{X} + z_{\alpha/2} \frac{\sigma}{\sqrt{n}}
$$
Multiplying by $-1$ reverses the inequalities:
$$
\bar{X} - z_{\alpha/2} \frac{\sigma}{\sqrt{n}} \leq \mu \leq \bar{X} + z_{\alpha/2} \frac{\sigma}{\sqrt{n}}
$$
This gives us the formula for the $100(1-\alpha)\%$ [confidence interval](@entry_id:138194) for $\mu$:
$$
\left[ \bar{X} - z_{\alpha/2} \frac{\sigma}{\sqrt{n}}, \; \bar{X} + z_{\alpha/2} \frac{\sigma}{\sqrt{n}} \right]
$$
This interval can also be written concisely as $\bar{X} \pm z_{\alpha/2} \frac{\sigma}{\sqrt{n}}$. From this structure, we can identify its key components. The center of the confidence interval is determined solely by the **[sample mean](@entry_id:169249)**, $\bar{X}$. It is the point estimate around which we build our interval of uncertainty [@problem_id:1906367]. The second component, $z_{\alpha/2} \frac{\sigma}{\sqrt{n}}$, is known as the **[margin of error](@entry_id:169950)**. It represents the "half-width" of the interval and quantifies the precision of our estimate at the given [confidence level](@entry_id:168001).

### Interpretation: The Frequentist Perspective

A correct interpretation of a [confidence interval](@entry_id:138194) is paramount and is one of the most subtle concepts in [frequentist statistics](@entry_id:175639). Once we collect our sample data—for instance, measuring the lifetimes of subatomic particles—and compute a specific interval, say $[87.324, 89.676]$ ps, this interval is no longer random. It is a fixed range of numbers. The true mean, $\mu$, is also a fixed, albeit unknown, constant. Therefore, the true mean $\mu$ is either inside this specific interval or it is not. A statement like "there is a 95% probability that $\mu$ lies in $[87.324, 89.676]$" is incorrect from a frequentist viewpoint, as it implies $\mu$ is a random variable [@problem_id:1906400].

The [confidence level](@entry_id:168001), such as 95%, refers to the reliability of the **procedure** used to generate the interval. The probability statement $\mathbb{P}(\text{Interval contains } \mu) = 1-\alpha$ applies *before* the data is observed, when the interval's endpoints, which depend on the random variable $\bar{X}$, are still random.

The correct interpretation is based on the concept of **coverage probability** under repeated sampling. If we were to repeat our entire experimental procedure—sampling commuter times, measuring the speed of light, or testing OLED lifespans—a very large number of times, and for each experiment we constructed a 95% confidence interval, we would find that approximately 95% of these constructed intervals would successfully contain the true, fixed mean $\mu$ [@problem_id:1906394] [@problem_id:1906426]. The remaining 5% of the intervals would fail to capture $\mu$. We do not know whether the single interval we have calculated is one of the 95% that "work" or one of the 5% that "fail." Our "confidence" is therefore in the long-run performance of the method, not in any single outcome.

### Properties of the Confidence Interval

The utility of a [confidence interval](@entry_id:138194) is determined by its location, its width, and the confidence we have in its construction. Analyzing the formula reveals how different factors influence the interval's properties.

#### The Length of the Interval

The total length (or width) of the confidence interval is the difference between its [upper and lower bounds](@entry_id:273322):
$$
L = \left(\bar{X} + z_{\alpha/2} \frac{\sigma}{\sqrt{n}}\right) - \left(\bar{X} - z_{\alpha/2} \frac{\sigma}{\sqrt{n}}\right) = 2 z_{\alpha/2} \frac{\sigma}{\sqrt{n}}
$$
This expression makes it clear that the length of the interval does not depend on the sample mean $\bar{X}$, but rather on three key factors [@problem_id:1906368]:

1.  **Confidence Level ($1-\alpha$):** A higher [confidence level](@entry_id:168001) requires a greater degree of certainty. This translates to a larger critical value $z_{\alpha/2}$ (e.g., $z_{0.005} \approx 2.576$ for a 99% interval versus $z_{0.05} \approx 1.645$ for a 90% interval). A larger $z_{\alpha/2}$ results in a wider interval. This illustrates the fundamental trade-off between confidence and precision: to be more confident that our interval contains the true mean, we must make the interval wider and thus less precise [@problem_id:1906406].

2.  **Sample Size ($n$):** The length is inversely proportional to the square root of the sample size, $\sqrt{n}$. As the sample size increases, the [standard error of the mean](@entry_id:136886) ($\sigma/\sqrt{n}$) decreases, and the interval becomes narrower. This is intuitive: more data leads to a more precise estimate. To halve the width of a [confidence interval](@entry_id:138194), one must quadruple the sample size, as the ratio of widths for two sample sizes $n_1$ and $n_2$ is $\sqrt{n_2}/\sqrt{n_1}$ [@problem_id:1906370].

3.  **Population Standard Deviation ($\sigma$):** A population with greater intrinsic variability (larger $\sigma$) will naturally lead to more uncertainty in the estimate of its mean, resulting in a wider confidence interval. The interval's length is directly proportional to $\sigma$.

#### Optimality: The Shortest-Length Interval

The symmetric interval we have constructed is not merely a matter of convention; it is optimal in the sense that it is the shortest possible interval for a given [confidence level](@entry_id:168001) $1-\alpha$. To see this, consider a more general interval of the form $[\bar{X} - c_1 \sigma/\sqrt{n}, \bar{X} + c_2 \sigma/\sqrt{n}]$. The coverage probability requirement is $\mathbb{P}(-c_1 \leq Z \leq c_2) = 1-\alpha$, and we wish to minimize the length, which is proportional to $c_1 + c_2$. The standard normal probability density function $\phi(z)$ is symmetric and unimodal, with its maximum at $z=0$. To capture a fixed area $1-\alpha$ with the shortest possible horizontal segment, we must center that segment over the peak of the density. This implies the endpoints of the segment on the Z-axis must be symmetric, i.e., $-c$ and $c$. This corresponds to setting $c_1 = c_2$. Any other choice, say $c_1 \neq c_2$, would require "stretching" the interval into the tails of the distribution where the probability density is lower, necessitating a longer total interval to capture the same area $1-\alpha$. Thus, the symmetric interval, where the error probability $\alpha$ is split equally into two tails of size $\alpha/2$, is the most precise (shortest) [confidence interval](@entry_id:138194) for a given [confidence level](@entry_id:168001) [@problem_id:1906379].

### The Criticality of the "Known Variance" Assumption

The entire derivation presented in this chapter hinges on one crucial assumption: the [population standard deviation](@entry_id:188217) $\sigma$ is known. In many practical applications, this assumption is unrealistic. It is worth exploring the consequences of violating this assumption to appreciate its importance.

Suppose the true, unknown standard deviation is $\sigma_1$, but an analyst mistakenly uses an incorrect value, $\sigma_0$, to construct a nominal $100(1-\alpha)\%$ [confidence interval](@entry_id:138194). The interval is calculated as $\bar{X} \pm z_{\alpha/2} \frac{\sigma_0}{\sqrt{n}}$. What is the *actual* probability that this interval covers $\mu$?

The coverage event is $|\bar{X} - \mu| \leq z_{\alpha/2} \frac{\sigma_0}{\sqrt{n}}$. To find its probability, we must standardize using the *true* standard deviation of $\bar{X}$, which is $\sigma_1/\sqrt{n}$:
$$
\mathbb{P}\left(\left|\frac{\bar{X} - \mu}{\sigma_1/\sqrt{n}}\right| \leq z_{\alpha/2} \frac{\sigma_0/\sqrt{n}}{\sigma_1/\sqrt{n}}\right) = \mathbb{P}\left(|Z| \leq z_{\alpha/2} \frac{\sigma_0}{\sigma_1}\right)
$$
where $Z \sim \mathcal{N}(0,1)$. The actual coverage probability is therefore $2\Phi\left(z_{\alpha/2} \frac{\sigma_0}{\sigma_1}\right) - 1$, where $\Phi$ is the standard normal CDF [@problem_id:1906421].

This result reveals a critical vulnerability. If the analyst underestimates the true standard deviation ($\sigma_0  \sigma_1$), the ratio $\sigma_0/\sigma_1$ is less than 1, and the actual coverage probability will be *less* than the nominal level $1-\alpha$. The analyst will be overconfident in an interval that is too narrow and misses the true mean more often than claimed. Conversely, overestimating the standard deviation ($\sigma_0 > \sigma_1$) leads to a conservative interval that is wider than necessary, with an actual coverage greater than $1-\alpha$. This underscores the importance of the known variance assumption and sets the stage for methods that account for an [unknown variance](@entry_id:168737), which will be the subject of a subsequent chapter.