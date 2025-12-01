## Introduction
In the field of medical imaging, raw pixel or voxel intensities hold a wealth of information about underlying tissue biology. However, translating this raw data into objective, quantifiable metrics for clinical decision-making presents a significant challenge. First-order radiomic features provide a foundational solution by summarizing the statistical distribution of voxel intensities within a defined region of interest. These features serve as powerful quantitative biomarkers, capable of characterizing tissue heterogeneity, tracking disease progression, and predicting treatment response, moving beyond subjective visual assessment. This article provides a comprehensive guide to the most common first-order histogram features: mean, variance, skewness, kurtosis, energy, and entropy. It aims to bridge the gap between their mathematical definitions and their practical application and interpretation in a clinical research context.

The journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct how these features are derived from the image intensity [histogram](@entry_id:178776), exploring the critical impact of data discretization and the statistical assumptions that underpin their validity. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these features are used to characterize tissue phenotypes and build predictive models, while also examining their sensitivity to technical variables in the imaging pipeline and strategies for ensuring reproducibility. Finally, the **Hands-On Practices** section offers practical exercises to solidify your understanding of how these statistical concepts manifest with real data. By the end of this article, you will have a robust understanding of how to calculate, interpret, and critically evaluate first-order radiomic features.

## Principles and Mechanisms

First-order radiomic features are derived from the statistical distribution of voxel intensities within a defined Region of Interest (ROI), without consideration for the spatial relationships between voxels. These features provide a quantitative summary of the tissue's appearance, capturing key aspects such as its average brightness, variability, symmetry, and textural complexity. The foundation for nearly all first-order features is the intensity [histogram](@entry_id:178776), a discrete representation of the underlying intensity distribution. This chapter elucidates the principles governing the construction of this histogram, the mathematical definitions and interpretations of the features derived from it, and the critical mechanisms and practical challenges that influence their calculation and reproducibility.

### From Voxel Intensities to the Histogram

The journey from a raw medical image to a set of first-order features begins with the delineation of an ROI. This process, known as segmentation, yields a binary mask, $m(\mathbf{r})$, where $\mathbf{r}$ represents the spatial coordinates of a voxel. The mask assigns a value of $1$ to voxels within the region and $0$ to those outside. The set of voxel intensities for analysis, $\{x_k\}_{k=1}^N$, is thus precisely the collection of intensity values at all locations $\mathbf{r}$ for which $m(\mathbf{r})=1$, where $N$ is the total number of voxels in the ROI [@problem_id:4541089].

The intensities $\{x_k\}$ often exist on a continuous or quasi-continuous scale (e.g., in Magnetic Resonance Imaging) or a very large discrete scale (e.g., Hounsfield Units in Computed Tomography). To analyze their distribution, we perform a process of **discretization**, which results in an **intensity histogram**. This process involves partitioning the full range of intensity values into a set of contiguous, non-overlapping intervals called **bins**. The histogram is a function that reports the number of voxels whose intensity values fall within each bin.

For a set of $B$ bins, the key components are:
- **Bin Edges**: The boundaries that define each interval. For a bin $i$, the interval might be represented as $[b_i, b_{i+1})$.
- **Bin Width ($h$)**: The size of the intensity interval for each bin. While bin widths can be variable, they are often fixed for simplicity.
- **Bin Center ($c_i$)**: A single representative intensity value for each bin $i$, typically the midpoint of the interval.
- **Bin Counts ($n_i$)**: The number of voxels from the ROI whose intensities $x_k$ fall into bin $i$. The sum of all bin counts equals the total number of voxels, $\sum_{i=1}^B n_i = N$.
- **Normalized Histogram Probabilities ($p_i$)**: By dividing the count for each bin by the total number of voxels, we obtain a [normalized frequency](@entry_id:273411), $p_i = n_i/N$. The set of these probabilities, $\{p_i\}_{i=1}^B$, forms an empirical **Probability Mass Function (PMF)**, as $\sum_{i=1}^B p_i = 1$. This PMF is the direct input for calculating most first-order features.

### The Histogram as an Approximation: The Impact of Quantization

It is crucial to recognize that the [histogram](@entry_id:178776) is an *approximation* of the true distribution of the raw voxel intensities $\{x_k\}$. The process of binning introduces what is known as **[quantization error](@entry_id:196306)**. This error arises because all the individual intensity values that fall within a single bin are subsequently represented by one single value—the bin center $c_i$. Information about the distribution of intensities *within* each bin is lost.

To understand this concretely, consider the calculation of the **mean** intensity. The true sample mean is calculated directly from the raw voxel values:
$$ \mu_{\text{raw}} = \frac{1}{N}\sum_{k=1}^N x_k $$
The histogram-based approximation of the mean is calculated as the expected value of the discrete PMF defined by the bin centers and their probabilities:
$$ \hat{\mu}_{\text{hist}} = \sum_{i=1}^B p_i c_i $$
Under what conditions would these two values be identical? The equality $\mu_{\text{raw}} = \hat{\mu}_{\text{hist}}$ holds exactly only under specific, and often unrealistic, conditions [@problem_id:4541082]. One such condition is if, for every bin, the chosen bin center $c_i$ happens to be the precise mean of all the raw voxel intensities $x_k$ that fall into that bin. Another scenario is when the raw data is already discrete and the binning scheme perfectly aligns, with each bin containing only one unique intensity value, which is also the bin center. In all other cases, $\hat{\mu}_{\text{hist}}$ is an approximation of $\mu_{\text{raw}}$, and the difference $\mu_{\text{raw}} - \hat{\mu}_{\text{hist}}$ represents the [quantization error](@entry_id:196306) for the mean.

This principle extends to all [higher-order moments](@entry_id:266936). For example, the variance calculated from the raw data, $\sigma^2_{\text{raw}} = \frac{1}{N}\sum(x_k - \mu_{\text{raw}})^2$, will generally differ from its histogram-based counterpart, $\hat{\sigma}^2_{\text{hist}} = \sum p_i (c_i - \hat{\mu}_{\text{hist}})^2$. The law of total variance shows that the true variance is the sum of the variance of the within-bin means (which is what the [histogram](@entry_id:178776) variance captures) and the mean of the within-bin variances (which the histogramming process ignores).

A detailed numerical example clarifies the magnitude and nature of these differences across various features [@problem_id:4541100]. Consider an ROI with $N=8$ voxels and intensities $\{0, 1, 1, 2, 2, 3, 3, 4\}$. The raw data mean is $\mu_{\text{raw}}=2$ and variance is $\sigma^2_{\text{raw}} = 1.5$. If we construct a 3-bin [histogram](@entry_id:178776) with centers $c_1=0.5, c_2=2.0, c_3=3.5$, we find the histogram-based mean is $\hat{\mu}_{\text{hist}}=2$ (by symmetry), but the variance is $\hat{\sigma}^2_{\text{hist}} \approx 1.6875$. This discrepancy, or [quantization error](@entry_id:196306), propagates through the calculation of all other features, including skewness, kurtosis, energy, and entropy. Understanding this error is the first step toward appreciating the importance of a standardized and well-justified discretization strategy.

### Statistical Validity: When Can We Trust Histogram Features?

Beyond merely approximating the sample in the ROI, the ultimate goal of radiomics is to infer properties of the underlying biological tissue. This moves the discussion from descriptive statistics to statistical inference. We wish for our calculated features to be **consistent estimators** of the true, unobserved population parameters of the tissue type. For this to hold, several statistical assumptions must be met [@problem_id:4541102].

First, a simple model of independent and identically distributed (i.i.d.) voxels is often inappropriate for image data, where [spatial correlation](@entry_id:203497) is significant. A more robust model treats the voxel intensities as a realization of a **stationary ergodic [random field](@entry_id:268702)**. **Stationarity** implies that the statistical properties of the distribution (like its mean and variance) do not change with spatial location within the tissue class. **Ergodicity** is the crucial property that ensures that a spatial average over a single large ROI converges to the ensemble average (the true population parameter). This allows us to make valid inferences from a single image.

Second, the ROI itself must constitute an **unbiased sample** of the tissue it purports to represent. If the segmentation systematically excludes or includes certain parts of a heterogeneous tissue, the resulting features will be biased estimators of the overall tissue properties.

Finally, the discretization scheme itself must be well-behaved as the sample size $N$ increases. For the histogram to converge to the true underlying probability density function, the bin width $h$ must shrink as $N$ grows ($h \to 0$), but not too quickly, so that the number of samples per bin remains large. The formal condition for consistent density and moment estimation from a histogram is that as $N \to \infty$, we must have $h \to 0$ and $N h \to \infty$. While these are asymptotic properties, they guide the practical choice of binning strategy, highlighting a fundamental trade-off between bias (from wide bins) and variance (from narrow bins with few samples).

### A Compendium of First-Order Features

Assuming a valid histogram has been constructed, we can compute a suite of features that summarize the intensity distribution.

#### Measures of Central Tendency and Dispersion

-   **Mean ($\mu$)**: The first raw moment of the distribution, $\mu = \sum_i p_i c_i$. It represents the average gray-level intensity in the ROI. While simple, it can be a powerful indicator of tissue properties, such as density in CT or water content in certain MRI sequences.

-   **Variance ($\sigma^2$)**: The [second central moment](@entry_id:200758), $\sigma^2 = \sum_i p_i (c_i - \mu)^2$. It measures the dispersion or spread of intensity values around the mean. A high variance suggests a wide range of intensities, indicating heterogeneity, while a low variance suggests homogeneity.

#### Measures of Distribution Shape

-   **Skewness ($\gamma_1$)**: The third standardized central moment, $\gamma_1 = \frac{1}{\sigma^3} \sum_i p_i (c_i - \mu)^3$. Skewness is a measure of the asymmetry of the intensity distribution.
    -   A **symmetric** distribution (like a Normal distribution) has a skewness of $0$.
    -   **Positive [skewness](@entry_id:178163)** ($\gamma_1 > 0$) indicates that the distribution has a long tail extending toward the higher intensity values. The mass of the distribution is concentrated on the left.
    -   **Negative [skewness](@entry_id:178163)** ($\gamma_1  0$) indicates a long tail toward the lower intensity values, with the mass concentrated on the right.
    
    Skewness can be a powerful differentiator of biological states. For instance, a necrotic tumor core, characterized by a high prevalence of low-intensity voxels, may exhibit a histogram with a long right tail of viable, higher-intensity cells, resulting in positive skewness. Conversely, a highly enhancing tumor region with few necrotic voxels may show a distribution concentrated at high intensities with a left tail, resulting in negative skewness [@problem_id:4541141]. For finite samples, the standard [skewness](@entry_id:178163) estimator is biased. In practice, a bias-corrected version, such as the adjusted Fisher-Pearson coefficient $G_1 = \frac{\sqrt{N(N-1)}}{N-2} g_1$ (where $g_1$ is the sample skewness), is often used to provide more accurate estimates, especially for smaller ROIs [@problem_id:4541113].

-   **Kurtosis ($\kappa$)**: The fourth standardized central moment, which quantifies the "tailedness" of the distribution. It is acutely sensitive to outliers. To facilitate interpretation, radiomics standards, such as the Image Biomarker Standardisation Initiative (IBSI), advocate for reporting **excess [kurtosis](@entry_id:269963)** [@problem_id:4541126]:
    $$ \kappa = \left( \frac{1}{\sigma^4} \sum_i p_i (c_i - \mu)^4 \right) - 3 $$
    This definition subtracts $3$, which is the kurtosis of a Normal distribution.
    -   **Mesokurtic** ($\kappa = 0$): The distribution has tails similar to a Normal distribution.
    -   **Leptokurtic** ($\kappa  0$): The distribution is "heavy-tailed" or "super-Gaussian". It has more outliers or extreme values than a Normal distribution. This results in a sharper peak and fatter tails.
    -   **Platykurtic** ($\kappa  0$): The distribution is "light-tailed" or "sub-Gaussian". It has fewer outliers than a Normal distribution. This often corresponds to a flatter, broader peak, such as in a [bimodal distribution](@entry_id:172497) [@problem_id:4541089].

    Kurtosis is exceptionally useful for detecting rare but significant intensity values. Consider two symmetric tumor ROIs with the same mean. One is largely uniform, while the other is mostly uniform but contains a few extremely bright voxels (e.g., calcifications) and a few extremely dark voxels (e.g., necrotic spots). The latter distribution will have a much higher [kurtosis](@entry_id:269963), signaling the presence of these biologically distinct outliers that may be missed by mean or variance alone [@problem_id:4541122].

#### Measures of Histogram Content and Heterogeneity

-   **Energy and Uniformity**: There is historical ambiguity in the term "energy." To resolve this, the IBSI standard distinguishes between two features [@problem_id:4541083]:
    -   **Total Energy**: This feature is computed from the *raw* voxel intensities as the sum of their squares, $\sum_{k=1}^N x_k^2$. It is not a [histogram](@entry_id:178776)-based feature and is dependent on both the ROI size and the absolute intensity scaling.
    -   **Uniformity**: This is the feature most commonly (and confusingly) referred to as "energy" in many software packages. It is computed from the histogram probabilities as the sum of their squares:
        $$ U = \sum_{i=1}^B p_i^2 $$
        Uniformity is a measure of histogram homogeneity. If all voxels fall into a single bin ($p_k=1$), $U$ reaches its maximum value of $1$. If the voxels are uniformly spread across all $B$ bins ($p_i=1/B$), $U$ reaches its minimum value of $1/B$. Thus, **higher uniformity implies a more homogeneous intensity distribution**. This property can be used to build classifiers to distinguish, for example, homogeneous healthy tissue from heterogeneous tumor tissue, by finding a statistically principled decision threshold based on the distributions of $U$ for each class [@problem_id:4541118].

-   **Entropy ($H$)**: Rooted in information theory, entropy is the quintessential [measure of uncertainty](@entry_id:152963), randomness, or complexity in a probability distribution. The Shannon entropy is defined as:
    $$ H = - \sum_{i=1}^B p_i \log_b p_i $$
    The base of the logarithm, $b$, is typically 2 (units of "bits") or $e$ (units of "nats"). The function is uniquely defined by a set of intuitive axioms: it is continuous, symmetric with respect to its inputs, maximized for a uniform distribution, and additive for independent systems [@problem_id:4541140].
    
    In radiomics, entropy quantifies the heterogeneity of the intensity distribution. It behaves inversely to uniformity. A homogeneous ROI with a highly peaked [histogram](@entry_id:178776) has very low entropy (low uncertainty). A heterogeneous ROI with a complex, flat [histogram](@entry_id:178776) has high entropy (high uncertainty).

### Practical Challenges in Feature Calculation and Comparability

The clinical utility of radiomic features hinges on their [reproducibility](@entry_id:151299) and comparability across patients, scanners, and institutions. Several practical challenges can undermine this goal.

#### The Impact of Segmentation: Partial Volume Effects

The definition of the ROI via the segmentation mask is a critical upstream step that profoundly influences all derived features. An ROI mask that only includes the "core" of a lesion will yield a different intensity distribution than an expanded mask that also includes the lesion's boundary. These boundary voxels are often subject to the **partial volume effect**, where a single voxel's volume encompasses multiple tissue types (e.g., tumor and adjacent healthy tissue). The resulting intensity of such a voxel is an average of the constituent tissues, leading to the emergence of new, intermediate intensity values.

Including these boundary voxels can introduce additional modes into the histogram, transforming a unimodal core distribution into a bimodal or multi-modal one. This systematically alters all first-order features: the mean may shift, the variance will typically increase, and the shape will change, affecting [skewness and kurtosis](@entry_id:754936). For example, adding low-intensity boundary voxels to a high-intensity core lesion can induce negative [skewness](@entry_id:178163) and decrease [kurtosis](@entry_id:269963) (making the distribution more platykurtic) [@problem_id:4541089]. This highlights that feature values reflect not only the biology but also the specific segmentation strategy employed.

#### The Crucial Role of Discretization

Perhaps the most significant source of non-[reproducibility](@entry_id:151299) in first-order features is the discretization method. Two common methods are Fixed Bin Number (FBN) and Fixed Bin Width (FBW).

In **Fixed Bin Number (FBN)** discretization, the intensity range within each patient's ROI, $[x_{\min}, x_{\max}]$, is divided into a constant number of bins, $B$. This means the physical bin width, $w = (x_{\max} - x_{\min})/B$, becomes dependent on the patient-specific dynamic range. This is highly problematic for cohort studies. Consider two patients with tumors of identical biological texture but imaged with different protocols, resulting in different dynamic ranges. For the patient with the larger [dynamic range](@entry_id:270472), the bins will be wider. A set of intensities that might be spread over several bins for the first patient could be compressed into a single, wider bin for the second patient. This would drastically change the resulting histogram PMF, leading to different values for features like entropy and uniformity, giving a false impression of a biological difference [@problem_id:4541136].

To mitigate this, **Fixed Bin Width (FBW)** discretization is strongly recommended. In this approach, the bin width $h$ is held constant (e.g., 25 HU) for all patients in a study. This ensures that an intensity interval of a given size is treated identically across all patients, making the resulting histogram features much more comparable. The choice of the bin width $h$ itself represents a critical trade-off between bias and variance, and it should be chosen carefully and reported clearly in any radiomics study.