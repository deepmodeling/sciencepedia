## Introduction
Image texture, the spatial arrangement of intensities, provides crucial information about the structure of an object, from the heterogeneity of a tumor in a CT scan to the patterns of a forest in a satellite image. While human experts can qualitatively describe textures as "coarse," "fine," or "striated," modern science and medicine demand objective, reproducible, and quantitative metrics. The Gray-Level Run-Length Matrix (GLRLM) is a powerful statistical method designed to meet this need by capturing textural information related to contiguous, linear sequences of pixels or voxels with the same intensity. This article provides a foundational understanding of the GLRLM, bridging the gap between its mathematical theory and its practical application in quantitative image analysis.

This article is structured as follows. The first section, **"Principles and Mechanisms,"** delves into the core theory, explaining how the GLRLM is constructed from a discretized image and how its key quantitative features are mathematically derived and interpreted. The second section, **"Applications and Interdisciplinary Connections,"** explores the diverse utility of GLRLM, showing how it translates qualitative visual assessments into actionable data in fields like oncology, digital pathology, and remote sensing, while also discussing the critical impact of image acquisition and preprocessing. Finally, the **"Hands-On Practices"** section offers a series of computational exercises designed to solidify your knowledge, guiding you from calculating features to building an efficient GLRLM algorithm from scratch. We begin by exploring the fundamental principles that underpin this versatile method of [texture analysis](@entry_id:202600).

## Principles and Mechanisms

The analysis of texture, a fundamental characteristic of an image, provides invaluable information about the spatial arrangement of intensities and the underlying structure of the imaged object. The Gray-Level Run-Length Matrix (GLRLM) is a powerful tool for quantifying texture, designed to capture information about contiguous sequences of voxels with the same intensity. This chapter elucidates the principles behind the construction of the GLRLM and the derivation and interpretation of its associated quantitative features.

### Constructing the Gray-Level Run-Length Matrix

The foundation of the GLRLM is the concept of a **run**: a maximal, collinear sequence of consecutive voxels all having the same gray-level intensity. To construct the matrix, we must first define what constitutes a gray level and then formalize the process of counting these runs.

#### Intensity Discretization: A Prerequisite for Analysis

Medical images, such as those from Computed Tomography (CT), often have intensities represented as a continuous or near-continuous range of values (e.g., Hounsfield Units, HU). To analyze texture using matrix-based methods, these intensities must be discretized into a finite number of gray levels, $N_g$. A common and reproducible method for this is **fixed-bin-width quantization**.

In this scheme, each voxel's continuous intensity value $x$ is mapped to a discrete gray-level index $g(x)$. A robust mapping function is given by:

$$
g(x) = \lfloor \frac{x - \mu}{\Delta} \rfloor + 1
$$

Here, $\Delta$ is a fixed bin width (e.g., $25$ HU) and $\mu$ is a fixed anchor level. The choice of these parameters is critical for ensuring that the resulting radiomic features are reproducible and comparable across different patients, scanners, and studies. For calibrated modalities like CT, where intensity values have a direct physical meaning, it is standard practice to anchor $\mu$ to a physical reference (e.g., $\mu=0$ HU for water) and use a fixed $\Delta$. This ensures that a [specific intensity](@entry_id:158830) range, corresponding to a certain tissue property, is always mapped to the same gray-level index. In contrast, adaptive methods where $\mu$ and $\Delta$ are determined from the intensity range of each individual Region of Interest (ROI) should be avoided, as they discard the absolute intensity information and harm reproducibility [@problem_id:4564397].

The choice of bin width $\Delta$ directly influences the resulting [texture analysis](@entry_id:202600). A smaller $\Delta$ (finer quantization) results in a larger number of distinct gray levels. This increased sensitivity to small intensity fluctuations typically leads to the fragmentation of long runs into several shorter ones, thus shifting the run-length distribution towards smaller values [@problem_id:4564397].

#### The Formal Definition of the GLRLM

Once the image is discretized, the GLRLM, denoted as $P(i, j)$, can be constructed. The entry at row $i$ and column $j$ of the matrix, $P(i, j)$, represents the total number of runs of gray level $i$ with a run length of exactly $j$ voxels. Crucially, this counting process is performed along a specific direction in the image.

To define this with mathematical rigor, let us consider a 3D voxel lattice $\mathcal{L}$ and an intensity map $I:\mathcal{L}\to\{1, \dots, N_g\}$. For a chosen direction vector $\vec{d}$, a run is a *maximal* sequence of collinear voxels with the same intensity. A voxel $x \in \mathcal{L}$ is the starting point of a maximal run of gray level $i$ and length $j$ if and only if three conditions are met [@problem_id:4564411]:

1.  **Run Content Condition**: The sequence of $j$ voxels starting at $x$ along the direction $\vec{d}$ must all have gray level $i$. Formally, $\forall k \in \{0, \dots, j-1\}$, the voxel $x+k\vec{d}$ is in the ROI and $I(x+k\vec{d})=i$.

2.  **Start-of-Run Condition**: The run cannot be an extension of a preceding run. This means the voxel just before the start, $x-\vec{d}$, must either be outside the ROI or have a different gray level: $(x-\vec{d} \notin \mathcal{L}) \lor (I(x-\vec{d}) \neq i)$.

3.  **End-of-Run Condition**: The run cannot be extended further. The voxel immediately after the end of the run, $x+j\vec{d}$, must either be outside the ROI or have a different gray level: $(x+j\vec{d} \notin \mathcal{L}) \lor (I(x+j\vec{d}) \neq i)$.

The GLRLM entry $P_{\vec{d}}(i,j)$ is the total count of voxels $x$ that satisfy all three conditions. This precise definition, accounting for the maximality of runs, is essential for accurate and consistent texture quantification.

#### Directionality and Isotropic Aggregation

The GLRLM is inherently directional. A texture may be anisotropic, exhibiting different run-length characteristics in different directions. In 3D imaging, analysis is typically performed along multiple directions to capture a comprehensive view of the texture. On a standard cubic lattice, there are 26 adjacent neighbors, which form 13 unique, undirected directional axes (e.g., the axes, face diagonals, and space diagonals) [@problem_id:4564401].

To obtain a single, rotationally-invariant texture signature, the directional GLRLMs are often aggregated. A common method is to compute the GLRLM, $P_{\vec{d}}(i,j)$, for each of the 13 unique directions $\vec{d} \in \mathcal{D}$ and then sum them to create an isotropic GLRLM:

$$
P_{\text{iso}}(i,j) = \sum_{\vec{d} \in \mathcal{D}} P_{\vec{d}}(i,j)
$$

This summation ensures that each unique spatial direction contributes equally to the final texture matrix, yielding features that are insensitive to the orientation of the object within the scanner. For the remainder of this chapter, when we refer to a single GLRLM, it can be assumed to be either a matrix for a single direction or an aggregated isotropic matrix.

### From Counts to Features: Deriving Quantitative Metrics

The GLRLM itself is a rich descriptor of texture, but for use in clinical models, it must be condensed into a set of scalar feature values. Before defining these features, we introduce two fundamental quantities that can be derived from the matrix $P(i,j)$:

-   The **total number of runs** ($N_r$) in the ROI, which is simply the sum of all entries in the matrix:
    $$
    N_r = \sum_{i=1}^{N_g} \sum_{j=1}^{N_{rl}} P(i,j)
    $$
    where $N_g$ is the number of gray levels and $N_{rl}$ is the maximum run length.

-   The **total number of voxels** ($N_p$ or $N_v$) that constitute these runs. Since each run of length $j$ is composed of $j$ voxels, this is a weighted sum:
    $$
    N_p = \sum_{i=1}^{N_g} \sum_{j=1}^{N_{rl}} j \cdot P(i,j)
    $$

These two quantities serve as normalization factors for many GLRLM features, ensuring they are comparable across ROIs of different sizes [@problem_id:4554340].

#### The Probabilistic Viewpoint

A powerful way to interpret the GLRLM is through the lens of probability theory. By normalizing the count matrix $P(i,j)$ by the total number of runs $N_r$, we obtain a normalized matrix $p(i,j) = P(i,j)/N_r$. This matrix can be treated as an empirical [joint probability mass function](@entry_id:184238) for two [discrete random variables](@entry_id:163471): gray level $I$ and run length $J$. That is, $p(i,j)$ is the probability that a randomly selected run from the ROI will have gray level $i$ and length $j$ [@problem_id:4564390]. This probabilistic framework provides a rigorous basis for defining statistical features.

### A Catalogue of GLRLM Features

We now present a selection of standard GLRLM features, explaining their formulation and interpretation.

#### Run Length Emphasis Features

These features are designed to measure the prevalence of short or long runs.

-   **Short Run Emphasis (SRE)**: This feature gives higher weight to shorter runs. Each run is weighted by the inverse square of its length ($1/j^2$). A high SRE value indicates that the texture is fine-grained, with a predominance of short runs.
    $$
    \text{SRE} = \frac{1}{N_r} \sum_{i=1}^{N_g} \sum_{j=1}^{N_{rl}} \frac{P(i,j)}{j^2}
    $$

-   **Long Run Emphasis (LRE)**: Conversely, LRE gives higher weight to longer runs by using a weight of $j^2$. A high LRE value signifies a coarse, blotchy, or striated texture with a predominance of long runs.
    $$
    \text{LRE} = \frac{1}{N_r} \sum_{i=1}^{N_g} \sum_{j=1}^{N_{rl}} j^2 P(i,j)
    $$
    The definitions for SRE and LRE with normalization by $N_r$ are consistent with the Image Biomarker Standardisation Initiative (IBSI) [@problem_id:4554340].

-   **Run Percentage (RP)**: This feature measures the density of runs relative to the number of voxels. It is defined as the ratio of the total number of runs to the total number of voxels.
    $$
    \text{RP} = \frac{N_r}{N_p} = \frac{\sum_{i,j} P(i,j)}{\sum_{i,j} j \cdot P(i,j)}
    $$
    A high RP value implies that the image is composed of many short runs, characteristic of a fine-grained texture. Note that RP is the reciprocal of the average run length.

#### Non-Uniformity Features

These features measure the uniformity of the run distributions across gray levels and run lengths.

-   **Gray Level Non-Uniformity (GLNU)**: This feature measures the non-uniformity of run counts over the gray levels. It is calculated from the marginal sum of runs for each gray level. A low value indicates that runs are distributed uniformly across all gray levels, while a high value indicates that runs are concentrated in only a few gray levels.
    $$
    \text{GLNU} = \frac{1}{N_r} \sum_{i=1}^{N_g} \left( \sum_{j=1}^{N_{rl}} P(i,j) \right)^2
    $$

-   **Run Length Non-Uniformity (RLNU)**: Similarly, this feature measures the non-uniformity of run counts over the run lengths. A high value signifies that the run lengths are concentrated at a few specific lengths, indicating a more structured or periodic texture, while a low value suggests a wider, more uniform distribution of run lengths.
    $$
    \text{RLNU} = \frac{1}{N_r} \sum_{j=1}^{N_{rl}} \left( \sum_{i=1}^{N_g} P(i,j) \right)^2
    $$
    Both GLNU and RLNU are derived from assessing the concentration of the marginal distributions of the GLRLM. High values for these features indicate greater texture heterogeneity [@problem_id:4613025].

#### Variance and Joint Emphasis Features

-   **Run Length Variance (RV)**: Using the probabilistic interpretation, we can define the [marginal probability distribution](@entry_id:271532) for run length as $p_l(j) = \sum_i p(i,j)$. The mean run length is $\mu_j = \sum_j j \cdot p_l(j)$. The Run Length Variance measures the spread of the run lengths around this mean.
    $$
    \text{RV} = \sum_{i=1}^{N_g} \sum_{j=1}^{N_{rl}} p(i,j) (j-\mu_j)^2 = \sum_{j=1}^{N_{rl}} (j-\mu_j)^2 p_l(j)
    $$
    A high RV indicates that run lengths are highly variable, while a low RV suggests that most runs have a length close to the average [@problem_id:4564390].

-   **Joint Emphasis Features**: These features combine weighting for both gray level and run length. For instance, **Long Run High Gray-Level Emphasis (LRHGE)** is weighted by $i^2 j^2$ and is highly responsive to textures with long runs of bright pixels. Conversely, **Short Run Low Gray-Level Emphasis (SRLGE)** is weighted by $1/(i^2 j^2)$ and is most sensitive to short runs of dark pixels. By examining combinations of these features, one can deduce specific texture characteristics. For example, a texture composed of "coarse bright structures" would be characterized by a high LRHGE value and a low SRLGE value [@problem_id:4564382].

### Advanced Topics and Practical Considerations

#### Choice of Normalization

While the IBSI standard normalizes SRE and LRE by the number of runs ($N_r$), some software implementations may normalize by the number of voxels ($N_p$). It is important to understand the relationship between these choices. Let $\text{SRE}_{N_r}$ be the feature normalized by $N_r$ and $\text{SRE}_{N_p}$ be the feature normalized by $N_p$. Their relationship is simple:

$$
\text{SRE}_{N_p} = \left(\frac{N_r}{N_p}\right) \text{SRE}_{N_r}
$$

The proportionality factor, $f = N_r/N_p$, is the Run Percentage, or the inverse of the average run length. This means that if two textures have the same average run length, the two versions of the SRE feature are proportional. However, if the average run length differs, the features are no longer simply scaled versions of one another and may rank textures differently [@problem_id:4564412].

#### Correction for Anisotropic Voxel Spacing

A critical consideration in medical imaging is that voxels are often not perfect cubes. For example, a CT scan might have an in-plane resolution of $0.8 \times 0.8$ mm, but a slice thickness of $3$ mm. A run of length $j=2$ voxels in the in-plane direction has a different physical length than a run of $j=2$ voxels in the through-plane direction.

Standard GLRLM features, which depend on the voxel count $j$, are therefore biased by the acquisition's voxel spacing. To ensure features reflect true biological structure, they must be corrected for physical scale. This is achieved by replacing the run length in voxels, $j$, with the physical run length, $L_j = j \cdot s$, where $s$ is the physical distance between voxel centers along the direction of analysis.

For example, the physically corrected SRE becomes:
$$
\text{SRE}_{\text{corr}}(s) = \frac{1}{N_r} \sum_{i,j} \frac{P(i,j)}{L_j^2} = \frac{1}{N_r} \sum_{i,j} \frac{P(i,j)}{(j \cdot s)^2} = \frac{1}{s^2} \cdot \text{SRE}_{\text{uncorr}}
$$
This simple correction, which scales the uncorrected feature by the inverse square of the voxel spacing, transforms the dimensionless SRE into a physically meaningful quantity with units of inverse area (e.g., mm$^{-2}$). Applying such corrections is paramount for building robust and generalizable radiomic models [@problem_id:4564403].