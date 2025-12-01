## Introduction
Medical images contain a wealth of information far beyond what is perceptible to the [human eye](@entry_id:164523). While radiologists expertly interpret macroscopic features, the subtle, microscopic variations in pixel intensity—collectively known as image texture—hold deep quantitative clues about underlying tissue pathophysiology. The field of quantitative [texture analysis](@entry_id:202600) aims to unlock this hidden information, transforming qualitative visual patterns into objective, reproducible, and actionable data. The core challenge it addresses is the need to move beyond subjective visual assessment toward the development of robust imaging biomarkers that can aid in diagnosis, predict prognosis, and guide personalized treatment.

This article provides a graduate-level guide to the theory and practice of [texture analysis](@entry_id:202600). It is structured to build your understanding from foundational concepts to advanced applications. In the first chapter, **Principles and Mechanisms**, we will establish a formal statistical basis for texture, explore the critical preprocessing steps that ensure analytical robustness, and systematically survey the major families of algorithms used to quantify texture. Next, the chapter on **Applications and Interdisciplinary Connections** will situate these methods within the broader radiomics pipeline, demonstrating how texture features are used to build predictive models and bridge the gap between imaging, machine learning, and molecular biology. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by working through concrete calculations for key texture features, translating abstract theory into practical skill.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that underpin quantitative [texture analysis](@entry_id:202600) in medical imaging. We will establish a formal basis for understanding texture, explore critical preprocessing steps necessary for robust analysis, and systematically survey the major families of methods used to transform qualitative visual patterns into quantitative, actionable biomarkers.

### Defining and Modeling Image Texture

Before we can measure texture, we must first define it. Visually, texture refers to the spatial arrangement of intensities or colors in an image, creating patterns of coarseness, smoothness, regularity, or randomness. To quantify this, we turn to the language of statistics and signal processing, modeling the image as a [random field](@entry_id:268702).

#### A Statistical Foundation: Texture as a Random Field

A powerful way to formalize texture is to model a two-dimensional image as a single realization of a **second-order stationary [random field](@entry_id:268702)**, denoted as $I(x,y)$. In this framework, the intensity at each pixel $(x,y)$ is a random variable. Texture is then defined not by individual pixel values, but by the statistical relationships between them. Specifically, we focus on second-[order statistics](@entry_id:266649), which describe how pixel intensities co-vary across space.

The key tool for this is the **[autocovariance function](@entry_id:262114)**, $C(\tau_x, \tau_y)$, which measures the covariance between pixel intensities separated by a spatial lag or [displacement vector](@entry_id:262782) $(\tau_x, \tau_y)$:

$C(\tau_x, \tau_y) = \operatorname{Cov}(I(x,y), I(x+\tau_x, y+\tau_y))$

For a second-order stationary field, this function depends only on the lag $(\tau_x, \tau_y)$ and not on the absolute position $(x,y)$. The nature of this function is what distinguishes a textured image from unstructured noise.

Consider the simplest case: a **[white noise](@entry_id:145248)** field. In such a field, every pixel's intensity is independent of its neighbors. This implies that the [autocovariance](@entry_id:270483) is zero for any non-zero lag. It is only non-zero at the origin, where it equals the variance of the field, $\sigma^2$. Mathematically, for a discrete image, this is $C(\tau_x, \tau_y) = \sigma^2 \delta_{\tau_x,0} \delta_{\tau_y,0}$, where $\delta$ is the Kronecker delta.

In contrast, a **textured field** exhibits spatial structure, meaning pixel values are correlated with their neighbors. This results in an [autocovariance function](@entry_id:262114) $C(\tau_x, \tau_y)$ that is non-zero for some non-zero lags. The way $C(\tau_x, \tau_y)$ decays as the magnitude of the lag, $\lVert (\tau_x, \tau_y) \rVert$, increases reveals the nature of the texture. A slow decay implies a coarse texture with long-range correlations, while a rapid decay suggests a fine texture. An oscillatory decay points to a regular, periodic pattern.

Furthermore, many biological textures are **anisotropic**, meaning their structure has a directional preference, such as in fibrous [muscle tissue](@entry_id:145481) or white matter tracts in the brain. This property is captured by an [autocovariance function](@entry_id:262114) whose decay rate depends on the direction of the lag vector $(\tau_x, \tau_y)$. For example, correlation may persist over longer distances along fibers than across them [@problem_id:4612969].

This spatial-domain view has a direct counterpart in the frequency domain. The **Wiener-Khinchin theorem** states that the [power spectral density](@entry_id:141002), $S(f_x, f_y)$, is the Fourier transform of the [autocovariance function](@entry_id:262114). A [white noise](@entry_id:145248) field, with its delta-like [autocovariance](@entry_id:270483), has a flat power spectrum, meaning all spatial frequencies are equally present. A textured field, with its structured [autocovariance](@entry_id:270483), has a non-uniform power spectrum, with energy concentrated in specific frequency bands or orientations that correspond to the characteristic scale and directionality of the texture [@problem_id:4612969].

#### The Assumption of Stationarity

The [random field](@entry_id:268702) model is most tractable under the assumption of **second-order [wide-sense stationarity](@entry_id:173765)** (WSS). As noted, this requires two conditions:
1.  The mean of the field, $\mathbb{E}[I(x,y)]$, is a constant $\mu$ for all locations $(x,y)$.
2.  The [autocovariance](@entry_id:270483), $\operatorname{Cov}(I(x,y), I(x+\tau_x, y+\tau_y))$, depends only on the [displacement vector](@entry_id:262782) $\boldsymbol{\tau}=(\tau_x, \tau_y)$ and not on the absolute position $(x,y)$.

This assumption allows us to characterize the texture of an entire region with a single, position-[independent set](@entry_id:265066) of statistics. However, in practice, a medical image ROI may not be perfectly stationary. For instance, a tumor may have a necrotic core and a hypervascular rim, violating the constant-mean assumption. It is therefore crucial to understand that [stationarity](@entry_id:143776) is an approximation.

One can design an empirical test to probe the validity of this assumption within a given ROI [@problem_id:4613032]. A statistically principled approach involves dividing the ROI, for example a $64 \times 64$ voxel patch, into smaller, non-overlapping subwindows (e.g., sixteen $8 \times 8$ subwindows). If the larger ROI is indeed stationary, then the statistical properties of these subwindows should be statistically indistinguishable. We can test this hypothesis formally:
-   **For the mean**: Compute the sample mean for each subwindow. A one-way Analysis of Variance (ANOVA) can then test the null hypothesis that all subwindows are drawn from populations with the same mean.
-   **For the [autocovariance](@entry_id:270483)**: For a fixed set of small lags, compute the sample [autocovariance](@entry_id:270483) vector for each subwindow. A one-way Multivariate Analysis of Variance (MANOVA) can test the null hypothesis that these vectors are statistically identical across all subwindows.

If both tests fail to reject the null hypothesis, we gain confidence that the [stationarity](@entry_id:143776) assumption is a reasonable approximation for that ROI. This process underscores the importance of critically evaluating the assumptions that underpin our analytical models [@problem_id:4613032].

### Preprocessing for Robust Texture Analysis

Before applying texture quantification methods, the image data must be properly prepared. The most critical step in this process is intensity discretization, which has profound implications for the reproducibility of results, especially in multi-center clinical trials.

#### Intensity Discretization: A Critical First Step

Most [texture analysis](@entry_id:202600) algorithms, particularly matrix-based methods like GLCM and GLRLM, are not computed on the raw intensity values (which could number in the thousands). Instead, they operate on a smaller, manageable number of discrete gray levels (typically 16, 32, or 64). This process of mapping the original intensity range to a smaller set of integer gray levels is called **intensity discretization** or quantization. The choice of discretization method is not trivial; it can significantly affect the final texture feature values.

The Image Biomarker Standardisation Initiative (IBSI) defines two primary, compliant methods for this task: Fixed Bin Number and Fixed Bin Width [@problem_id:4612963].

-   **Fixed Bin Number (FBN)**: This method takes the specific range of intensities within the ROI, $[I_{\min}, I_{\max}]$, and divides it into a predetermined number of bins, $N$. The width of each bin, $w = (I_{\max} - I_{\min}) / N$, is therefore dependent on the specific ROI. An intensity value $x$ is mapped to a gray level $g(x)$ by the formula:
    $g(x) = \left\lfloor \frac{x - I_{\min}}{(I_{\max} - I_{\min})/N} \right\rfloor + 1$

-   **Fixed Bin Width (FBW)**: This method uses a predefined, constant bin width $w$ that is applied universally. Given a fixed lower bound $I_L$, an intensity value $x$ is mapped to a gray level $g(x)$ according to its absolute value:
    $g(x) = \left\lfloor \frac{x - I_{L}}{w} \right\rfloor + 1$

The choice between these two methods hinges on the nature of the image's intensity scale. For imaging modalities with a **relative intensity scale**, like raw Magnetic Resonance Imaging (MRI) signals, the [absolute values](@entry_id:197463) are arbitrary and can vary dramatically between scanners and acquisition protocols. In such cases, FBN is often used as it normalizes the intensity range of each ROI.

However, for modalities with an **absolute physical scale**, such as the Hounsfield Unit (HU) scale in Computed Tomography (CT), the choice is clearer. The HU scale is calibrated to physical standards (air at $-1000$ HU, water at $0$ HU). A value of $+50$ HU represents the same tissue density regardless of the scanner. In this scenario, FBN is detrimental to [reproducibility](@entry_id:151299). Because the ROI-specific $I_{\min}$ and $I_{\max}$ are sensitive to noise and scanner differences, FBN would cause the bin boundaries to shift arbitrarily from scan to scan, mapping the same physical tissue density to different gray levels.

In contrast, **Fixed Bin Width (FBW) is the preferred method for absolute scales** like CT HU. By defining bin edges that are fixed on the absolute scale (e.g., bins of width 25 HU), we ensure that a given tissue density is always mapped to the same gray level, regardless of scanner or patient. This anchoring to physical reality removes a major source of technical variability and is crucial for building robust and reproducible radiomic models for clinical applications [@problem_id:4612963].

### Methods of Texture Quantification

Once the image is preprocessed, we can apply a vast array of algorithms to extract quantitative features. These methods can be broadly categorized into statistical approaches, which analyze the distribution and spatial relationships of gray levels, and transform-based approaches, which analyze the image in a different domain (e.g., frequency).

#### First-Order Features: The Intensity Histogram

The simplest features are **first-order statistics**, which are derived from the image's intensity [histogram](@entry_id:178776). These features describe the distribution of intensities within the ROI but completely disregard their spatial arrangement. A smooth image and a noisy image can have the exact same histogram. Despite this limitation, they provide a useful baseline summary of the tissue's composition.

Let the normalized [histogram](@entry_id:178776) of an ROI with $B$ bins be represented by a probability [mass function](@entry_id:158970) $\{p_i\}$, where $p_i$ is the probability of a pixel having an intensity corresponding to bin $i$ with center value $c_i$. The key first-order features are defined as follows [@problem_id:4613000]:

-   **Mean**: The average intensity level. $\hat{\mu} = \sum_{i=1}^{B} c_i p_i$
-   **Variance**: The spread of intensities around the mean. $\hat{\sigma}^2 = \sum_{i=1}^{B} (c_i - \hat{\mu})^2 p_i$
-   **Skewness**: A measure of the asymmetry of the [histogram](@entry_id:178776). $\hat{\gamma}_1 = \frac{\sum_{i=1}^{B} (c_i - \hat{\mu})^3 p_i}{\hat{\sigma}^3}$
-   **Kurtosis (Excess)**: A measure of the "tailedness" or "peakedness" of the histogram compared to a normal distribution. $\hat{\gamma}_2 = \frac{\sum_{i=1}^{B} (c_i - \hat{\mu})^4 p_i}{\hat{\sigma}^4} - 3$
-   **Energy**: A measure of the uniformity of the histogram; it is high when only a few gray levels are present. $\widehat{\text{energy}} = \sum_{i=1}^{B} p_i^2$
-   **Entropy**: A measure of the randomness or complexity of the intensity distribution. It is high for a flat, uniform [histogram](@entry_id:178776). $\widehat{\text{entropy}} = -\sum_{i=1}^{B} p_i \log p_i$

These are "plug-in" estimators, derived by substituting the empirical probabilities $p_i$ into the population formulas.

#### Second-Order and Higher-Order Statistical Methods

To capture the spatial arrangement of intensities, which is the essence of texture, we must move to second-order or [higher-order statistics](@entry_id:193349).

##### The Gray Level Co-occurrence Matrix (GLCM)

The **Gray Level Co-occurrence Matrix (GLCM)** is the classic method for quantifying second-order statistics. For a given [displacement vector](@entry_id:262782) $\mathbf{d} = (\tau_x, \tau_y)$, the GLCM is a matrix that tabulates how often different pairs of gray levels co-occur in pixels separated by $\mathbf{d}$.

Formally, after discretizing the image into $L$ gray levels, the unnormalized GLCM entry $P(i,j;\mathbf{d})$ is the count of all pixel pairs within the ROI $\mathcal{R}$ that have intensities $(i,j)$ and are separated by $\mathbf{d}$. The summation must only include pairs where both pixels lie within the ROI [@problem_id:4612975]:

$P(i,j;\mathbf{d}) = \sum_{\mathbf{x}\in\mathcal{R} : \mathbf{x}+\mathbf{d}\in\mathcal{R}} \mathbf{1}\{I(\mathbf{x})=i\} \, \mathbf{1}\{I(\mathbf{x}+\mathbf{d})=j\}$

where $\mathbf{1}\{\cdot\}$ is the [indicator function](@entry_id:154167).

To convert these counts into a joint probability distribution, the matrix is normalized by dividing every element by the total number of valid pairs considered, which is simply the sum of all elements in the unnormalized matrix:

$p_{ij} = \frac{P(i,j;\mathbf{d})}{\sum_{i=0}^{L-1}\sum_{j=0}^{L-1}P(i,j;\mathbf{d})}$

From this normalized GLCM, a host of texture features are computed, such as Contrast (measuring local variations), Correlation (measuring [linear dependency](@entry_id:185830)), Energy (measuring homogeneity), and Homogeneity. By computing these features for GLCMs generated with different displacement vectors $\mathbf{d}$, one can probe the texture's anisotropy.

##### The Gray Level Run Length Matrix (GLRLM)

While GLCM focuses on pixel pairs, the **Gray Level Run Length Matrix (GLRLM)** is designed to capture properties of contiguous, linear arrangements of pixels. It is particularly effective for describing coarse, directional textures.

A **run** is defined as a sequence of consecutive, collinear pixels having the same gray level. A key detail in the definition is that we only count **maximal** runs—that is, runs that cannot be extended in either direction [@problem_id:4613036]. For a given direction $\theta$, the GLRLM element $R(i,l;\theta)$ is the number of maximal runs of gray level $i$ with length $l$ found in the image along that direction.

Features derived from the GLRLM, such as Short Run Emphasis, Long Run Emphasis, and Run Length Non-uniformity, describe the distribution of run lengths and can effectively distinguish between fine, granular textures (many short runs) and coarse, streaky textures (many long runs).

##### The Neighborhood Gray-Tone Difference Matrix (NGTDM)

The **Neighborhood Gray-Tone Difference Matrix (NGTDM)** offers another perspective on texture, quantifying the spatial rate of change in intensity. For each gray level $i$ present in the ROI, it computes a score $s(i)$ representing the summed difference between pixels of that gray level and their local neighborhood average.

Formally, for each pixel $x$ in the ROI with intensity $I(x)=i$, we compute the average intensity $\bar{I}(x)$ of its neighbors. A critical and principled aspect of this calculation is the handling of border pixels: the average is computed only over the neighbors that are actually inside the ROI, and the normalization factor is the number of such available neighbors, $|\mathcal{N}_{\delta}(x)|$ [@problem_id:4612972]. This avoids the bias that would be introduced by padding or other forms of data fabrication. The NGTDM entry $s(i)$ is then:

$s(i) = \sum_{\substack{x\in\mathcal{R} \\ I(x)=i \\ |\mathcal{N}_{\delta}(x)|\ge 1}} \left| i - \frac{1}{|\mathcal{N}_{\delta}(x)|}\sum_{y\in \mathcal{N}_{\delta}(x)} I(y) \right|$

From the resulting matrix (or vector, as it is one-dimensional), features such as Coarseness, Contrast, and Busyness are calculated, which describe whether the texture is visually "busy" with rapid changes or smooth and "clean."

#### Model-Based and Transform-Based Methods

This class of methods analyzes texture by fitting a model to the image data or by projecting the data onto a basis of functions (filters).

##### Local Binary Patterns (LBP)

The **Local Binary Pattern (LBP)** is a powerful, computationally efficient, and widely used texture descriptor that characterizes the local structure around each pixel. The basic $LBP_{P,R}$ operator works as follows: for a center pixel, it samples $P$ neighbors on a circle of radius $R$. The intensity of each neighbor is compared to the center pixel's intensity. If a neighbor is brighter or equal, a '1' is recorded; otherwise, a '0' is recorded. This process generates a $P$-bit binary string [@problem_id:4612951].

For example, consider a center pixel $I_c = 120$ with $P=8$ neighbors $\{110, 130, 125, 119, 80, 75, 90, 121\}$. Comparing each to 120 yields the binary sequence $[0, 1, 1, 0, 0, 0, 0, 1]$.

The basic LBP codes are sensitive to image rotation. A significant innovation is the **rotation-invariant uniform mapping ($LBP^{riu2}$)**. This mapping achieves rotation invariance and dramatically reduces the feature space dimensionality. It operates in two steps:
1.  A pattern is classified as **uniform** if it contains at most two circular transitions from 0 to 1 or 1 to 0. Patterns with more than two transitions are deemed **non-uniform**. These non-uniform patterns typically correspond to noisy or complex local structures. In our example pattern $[0, 1, 1, 0, 0, 0, 0, 1]$, the circular transitions are at $0 \to 1$, $1 \to 0$, $0 \to 1$, and $1 \to 0$ (wrapping around), for a total of 4 transitions. The pattern is therefore non-uniform.
2.  The mapping assigns an index: uniform patterns are mapped to an index equal to their number of '1's. All non-uniform patterns, regardless of their specific form, are collapsed into a single, separate bin. For $P=8$, this results in $P+1=9$ bins for the uniform patterns (0 to 8 ones) and one bin for all non-uniform patterns, for a total of $P+2=10$ bins. Our example pattern, being non-uniform, would be mapped to the 10th bin (index 9) [@problem_id:4612951].

The histogram of these $LBP^{riu2}$ codes over an ROI serves as a compact and robust texture descriptor.

##### Gabor Filter Banks

Filter-based methods probe texture by convolving the image with a set of filters, or a **filter bank**, designed to be sensitive to patterns at specific scales and orientations. **Gabor filters** are a preeminent choice for this task, as they are optimally localized in both the spatial and frequency domains, mimicking the response properties of neurons in the human visual cortex.

A 2D Gabor filter is a complex sinusoid modulated by a Gaussian envelope. The real part, often used for [texture analysis](@entry_id:202600), is given by [@problem_id:4612953]:

$g(x,y) = \exp\left(-\frac{x'^2+\gamma^2 y'^2}{2\sigma^2}\right)\cos(2\pi f_0 x')$

where:
-   $(x', y')$ are coordinates rotated by an angle $\theta$ ($x' = x\cos\theta+y\sin\theta$, $y' = -x\sin\theta+y\cos\theta$), setting the filter's [preferred orientation](@entry_id:190900).
-   $f_0$ is the center frequency of the sinusoid, determining the preferred scale (or spatial frequency).
-   $\sigma$ controls the spatial spread of the Gaussian envelope.
-   $\gamma$ is the spatial aspect ratio, or anisotropy, controlling the filter's selectivity to orientation.

A single Gabor filter is insufficient to characterize a complex texture. Instead, a **[filter bank](@entry_id:271554)** is constructed with multiple filters spanning a range of scales and orientations. A principled design involves [@problem_id:4612953]:
1.  **Orientations**: Sampled uniformly in $[0, \pi)$, e.g., $\theta_k = k\pi/K$ for $K$ orientations.
2.  **Scales**: Center frequencies $f_s$ are spaced geometrically (e.g., $f_s = f_{\max}a^{-s}$), corresponding to a log-polar tiling of the frequency plane.
3.  **Bandwidth**: The spatial spread $\sigma_s$ is set inversely proportional to the center frequency ($\sigma_s \propto 1/f_s$). This ensures that the filters have a **constant relative bandwidth**, meaning each filter is equally "tuned" relative to its preferred frequency.
4.  **Normalization**: Filter amplitudes are scaled to ensure approximately constant energy across scales, preventing higher-frequency filters from dominating the response.

The image is convolved with each filter in the bank, and statistics (like the mean and standard deviation) of each filtered output image are used as texture features.

##### Fractal Analysis

A distinct paradigm for [texture analysis](@entry_id:202600) comes from [fractal geometry](@entry_id:144144). **Fractal analysis** quantifies the complexity of a texture by measuring how its measured properties change with the scale of observation. The **fractal dimension** ($D$) is a key feature, capturing the texture's space-filling capacity and [self-similarity](@entry_id:144952). A higher [fractal dimension](@entry_id:140657) corresponds to a more complex, irregular, or rugged texture.

The **[box-counting dimension](@entry_id:273456)** is a common method for estimation. Conceptually, one covers the texture with a grid of boxes of side length $\epsilon$ and counts the minimum number of boxes, $N(\epsilon)$, required to contain the texture. The fractal dimension is defined by the [scaling law](@entry_id:266186) as $\epsilon \to 0$ [@problem_id:4612954]:

$D = \lim_{\epsilon \to 0} \frac{\log N(\epsilon)}{\log(1/\epsilon)}$

This implies a power-law relationship: $N(\epsilon) \propto \epsilon^{-D}$. To estimate $D$ from a [digital image](@entry_id:275277), we measure $N(s)$ for a discrete set of box sizes $s$ and linearize the relationship by taking the logarithm:

$\log N(s) \approx \log k - D \log s \quad \text{or equivalently} \quad \log N(s) \approx \log k + D \log(1/s)$

We can then perform a linear regression of $\log N(s)$ on $\log(1/s)$ over a range of scales where this relationship holds (the "scaling region"). The slope of this regression line provides an estimate of the fractal dimension, $\widehat{D}$.

A statistically rigorous estimation requires further consideration. The box counts $N(s)$ are subject to Poisson-like counting noise, meaning the variance of the measurement is not constant across scales (a condition known as heteroscedasticity). Specifically, the variance of $\log N(s)$ is approximately proportional to $1/N(s)$. To account for this, **Weighted Least Squares (WLS)** regression should be used, with weights for each data point proportional to $N(s)$. This gives more influence to the more reliable counts at smaller box sizes and yields a more accurate and robust estimate of the [fractal dimension](@entry_id:140657) [@problem_id:4612954].