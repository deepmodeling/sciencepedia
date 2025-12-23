## Introduction
Image registration, the process of geometrically aligning one image to another or to a map, is a cornerstone of remote sensing and geospatial science. It is the fundamental step that transforms raw sensor data into geographically accurate and analyzable information products, enabling critical applications from [urban planning](@entry_id:924098) to monitoring global environmental change. However, achieving robust and precise alignment is a complex challenge that requires a deep understanding of [geodesy](@entry_id:272545), sensor physics, mathematics, and statistics. This article addresses the knowledge gap between a simple conceptual understanding of registration and the rigorous implementation needed for scientific analysis.

Across the following chapters, you will embark on a comprehensive journey through the theory and practice of [image registration](@entry_id:908079). The first chapter, "Principles and Mechanisms," lays the groundwork, detailing the geodetic reference systems, the mathematical transformation models, and the statistical methods that ensure geometric and statistical rigor. Next, "Applications and Interdisciplinary Connections" demonstrates how these principles are deployed in the real world, exploring solutions for sensor-specific errors, complex terrain, multi-modal data, and the measurement of dynamic Earth processes. Finally, "Hands-On Practices" will provide you with the opportunity to apply these concepts to solve concrete problems in georeferencing and feature matching. We begin by establishing the geodetic and mathematical foundations that underpin all registration tasks.

## Principles and Mechanisms

The process of [image registration](@entry_id:908079), whether to a map or to another image, is fundamentally one of establishing a precise geometric correspondence between two [coordinate systems](@entry_id:149266). This chapter delves into the core principles and mechanisms that govern this process. We will begin by establishing the geodetic foundations necessary for absolute referencing, then explore the mathematical models used to describe geometric distortions, and finally examine the algorithms for implementing these transformations and the statistical methods required for their rigorous estimation.

### Foundations of Geometric Referencing

Before an image can be registered to a map, we must first have an unambiguous understanding of the map's coordinate system itself. Remotely sensed data, particularly from satellite platforms, are often initially located in a global, three-dimensional system. However, national or regional maps are built upon specific local or regional reference frameworks. The reconciliation of these different systems is a foundational step in image-to-map registration.

At the heart of this reconciliation are **geodetic datums**, which provide the formal definition for a coordinate system and its realization on the Earth. A modern **horizontal datum** is not merely a reference shape but a complete system comprising:
1.  A **reference [ellipsoid](@entry_id:165811)**, a mathematically simple surface (an [ellipsoid](@entry_id:165811) of revolution) that approximates the Earth's shape, defined by parameters such as its semi-major axis ($a$) and flattening ($f$). The World Geodetic System 1984 (WGS84) uses such an ellipsoid.
2.  An **origin, orientation, and scale** for a three-dimensional coordinate system, typically realized as an Earth-Centered, Earth-Fixed (ECEF) frame. This frame is defined by the positions and velocities of a network of ground control stations.

Similarly, a **vertical datum** defines the reference surface for elevations, or heights. Unlike the mathematically smooth ellipsoid, elevations on maps are typically reckoned with respect to a physically meaningful surface that approximates mean sea level. This surface is known as the **geoid**. The [geoid](@entry_id:749836) is an [equipotential surface](@entry_id:263718) of the Earth's gravity field, meaning that the force of gravity is perpendicular to it at every point. Due to the non-[uniform distribution](@entry_id:261734) of mass within the Earth, the geoid is an irregular, undulating surface.

This distinction gives rise to two primary types of height:
-   The **ellipsoidal height**, denoted by $h$, is the geometric height of a point above the reference ellipsoid, measured along the line normal (perpendicular) to the ellipsoid's surface. Satellite positioning systems like GPS and the direct output of physical sensor models for satellite imagery typically produce ellipsoidal heights.
-   The **orthometric height**, denoted by $H$, is the height of a point above the geoid, measured along the local plumb line (the direction of gravity). This is what is commonly understood as "elevation" on [topographic maps](@entry_id:202940). For instance, a map referenced to the North American Vertical Datum 1988 (NAVD88) uses orthometric heights.

The vertical distance between the [geoid](@entry_id:749836) and the reference [ellipsoid](@entry_id:165811) at any given location is known as the **[geoid](@entry_id:749836) separation** or **[geoid](@entry_id:749836) undulation**, denoted by $N$. The relationship between these three height quantities is given by the fundamental equation of geodesy:

$h = H + N$

This equation is paramount in image-to-map registration. When an image provides ellipsoidal heights ($h$) relative to an ellipsoid like WGS84, and the target map uses orthometric heights ($H$) relative to a vertical datum like NAVD88, a direct comparison is not possible. One must first convert between height systems by accounting for the geoid separation. Rearranging the equation, the orthometric height is found by:

$H = h - N$

The value of $N$ is provided by a **[geoid](@entry_id:749836) model**, which is a high-resolution grid of [geoid](@entry_id:749836) separation values for a specific region. For example, to register a WGS84-geolocated image to a map on the NAD83/NAVD88 datums, if a ground control point has an image-derived ellipsoidal height of $h = 52.3\,\mathrm{m}$ and the local [geoid](@entry_id:749836) model indicates the geoid is $28.7\,\mathrm{m}$ *below* the ellipsoid ($N = -28.7\,\mathrm{m}$), the corresponding orthometric height on the map would be $H = 52.3\,\mathrm{m} - (-28.7\,\mathrm{m}) = 81.0\,\mathrm{m}$ . Neglecting this conversion introduces a systematic vertical error equal in magnitude to the local geoid separation.

Furthermore, horizontal datums like WGS84 and NAD83 are not identical. While both are geocentric, they are fixed to different [tectonic plates](@entry_id:755829) (the global average plate motion for WGS84 vs. the North American plate for NAD83). Rigorous registration requires transforming coordinates between these frames using an epoch-consistent, multi-parameter transformation, typically a **7-parameter Helmert transformation**, which accounts for shifts in origin, rotations of the axes, and a scale difference between the two systems .

### Geometric Transformation Models

Once the target coordinate system is well-defined, the next step is to select a mathematical model to describe the geometric distortion present in the source image. The choice of model depends on the nature of the sensor, the viewing geometry, the terrain, and the desired accuracy. These models range from simple 2D empirical functions to rigorous, physically based 3D models.

#### Empirical 2D Transformations

In many applications, especially with airborne imagery of relatively flat terrain or when the rigorous sensor model is unavailable, the geometric relationship between the image and the map can be approximated by a 2D planar transformation. These models are defined by a set of parameters estimated from a set of corresponding points, known as **Ground Control Points (GCPs)**. Three common models form a hierarchy of increasing complexity .

1.  **Similarity (Conformal) Transform**: This is the simplest model, composed of [isotropic scaling](@entry_id:267671), rotation, and translation. It has **4 degrees of freedom (DoF)**: one [scale factor](@entry_id:157673), one rotation angle, and two translation components. Its key **geometric invariant** is the preservation of angles, and consequently, the shapes of objects. It also preserves parallelism and ratios of distances. A similarity transform can be uniquely determined from a minimum of **2 distinct GCPs**.

2.  **Affine Transform**: This transform adds differential scaling and shear to the similarity model. It is represented by a general linear transformation followed by a translation and has **6 DoF**. Its invariants include **[collinearity](@entry_id:163574)** (straight lines remain straight), **parallelism** ([parallel lines](@entry_id:169007) remain parallel), and **ratios of distances along a single line**. However, it does not preserve angles or general distance ratios. An affine transform requires a minimum of **3 non-collinear GCPs** for its determination. This model is very common for correcting satellite imagery over small areas where terrain effects are minimal.

3.  **Projective Transform (Homography)**: This is the most general linear transformation of [homogeneous coordinates](@entry_id:154569), with **8 DoF**. It accurately models the perspective distortion that occurs when a planar surface is viewed from an arbitrary perspective. Its only key invariants are **[collinearity](@entry_id:163574)** and the **[cross-ratio](@entry_id:176420)** of four collinear points. It does not preserve parallelism; [parallel lines](@entry_id:169007) can be mapped to intersecting lines (e.g., vanishing points). A projective transform requires a minimum of **4 GCPs** (with no three of them being collinear) to be uniquely determined.

#### Rigorous Sensor Models

For high-accuracy registration and for sensors viewing variable terrain, empirical 2D models are insufficient. A more powerful approach is to use a **rigorous sensor model** that physically describes the imaging process from the 3D world to the 2D image plane. The foundational principle for such models is the **[collinearity principle](@entry_id:1122641)**, which states that the sensor's perspective center, a point on the ground, and its corresponding image point all lie on a single straight line .

To formalize this, we define two sets of parameters:
-   **Extrinsic Parameters**: These define the camera's position and orientation in 3D object space. They consist of the perspective center's coordinates $(X_s, Y_s, Z_s)$ and a rotation matrix $\mathbf{R}$ that orients the camera's coordinate system relative to the object coordinate system.
-   **Intrinsic Parameters**: These define the internal geometry of the camera. For a simple pinhole model, they include the **principal distance** $f$ (often called [focal length](@entry_id:164489)) and the coordinates of the **principal point** $(x_0, y_0)$, which is the location where the optical axis intersects the image plane.

The derivation of the **collinearity equations** proceeds by transforming a ground point's coordinates into the camera's reference frame and then applying a perspective projection. Let a ground point have object coordinates $\mathbf{P} = (X,Y,Z)^{\top}$. The vector from the perspective center $\mathbf{P}_s = (X_s,Y_s,Z_s)^{\top}$ to this point is $\mathbf{P} - \mathbf{P}_s$. This vector is transformed into the camera's coordinate system using the rotation matrix $\mathbf{R}$:

$\begin{pmatrix} U \\ V \\ W \end{pmatrix} = \mathbf{R} \begin{pmatrix} X - X_s \\ Y - Y_s \\ Z - Z_s \end{pmatrix}$

Here, $(U,V,W)^{\top}$ are the coordinates of the ground point in the camera's frame, where the $W$ component is along the optical axis. By similar triangles, the projection onto an image plane at a distance $f$ from the center gives the image coordinates $(x,y)$ relative to the principal point $(x_0,y_0)$:

$x = x_0 - f \frac{U}{W}$
$y = y_0 - f \frac{V}{W}$

Substituting the expressions for $U$ and $W$ (which contain the elements of $\mathbf{R}$) yields the full collinearity equations, which analytically link 3D object coordinates $(X,Y,Z)$ to 2D image coordinates $(x,y)$ . These equations are the bedrock of [photogrammetry](@entry_id:1129621) and are central to rigorous processes like [orthorectification](@entry_id:1129216).

#### Generic Sensor Models: Rational Polynomial Cameras (RPCs)

While physical sensor models are rigorous, their parameters may be complex or proprietary. For many modern high-resolution satellite systems, a **generic sensor model** known as the **Rational Polynomial Camera (RPC)** model is provided instead . RPCs are not physical models but are highly accurate empirical approximations of the physical model over a specific geographic area.

The RPC model defines the mapping from 3D object coordinates $(X,Y,Z)$ to 2D image coordinates (line $l$, sample $s$) as a ratio of polynomials. To ensure numerical stability, all coordinates are first normalized to a range of approximately $[-1, 1]$ using offset and scale parameters provided in the image metadata:

$x = \frac{X - X_0}{S_X}, \quad y = \frac{Y - Y_0}{S_Y}, \quad z = \frac{Z - Z_0}{S_Z}$

The normalized image coordinates $(r,c)$ are then computed as:

$r = \frac{\text{Num}_l(x,y,z)}{\text{Den}_l(x,y,z)}, \quad c = \frac{\text{Num}_s(x,y,z)}{\text{Den}_s(x,y,z)}$

The final pixel coordinates are recovered by inverse normalization (e.g., $l = l_0 + S_l \cdot r$). The numerators (Num) and denominators (Den) are typically third-degree polynomials in three variables, which contain 20 terms each (e.g., $1, x, y, z, xy, xz, yz, x^2, \dots, xyz$).

A critical aspect of [rational functions](@entry_id:154279) is an inherent scale ambiguity: multiplying both the numerator and denominator by the same non-zero constant does not change the result. To ensure a unique set of coefficients, a **coefficient normalization** constraint is imposed. The standard convention is to divide all coefficients in both the numerator and denominator by the constant term of the denominator, forcing the denominator's constant term to become 1. This makes the remaining 78 coefficients per mapping (20 for the numerator, 19 for the denominator) unique and identifiable .

### The Registration Process: Algorithms and Implementation

With a transformation model chosen, the next challenge is to apply it to create a geometrically correct output image. This involves two key processes: correcting for complex distortions like those from terrain, and then resampling the original pixel values onto a new, regular grid.

#### Orthorectification: Correcting for Terrain Distortion

A raw satellite or aerial image is a perspective projection of the three-dimensional world. This means that objects at higher elevations are displaced in the image relative to objects at lower elevations, an effect known as **terrain-induced parallax**. An **orthoimage** is an image that has been geometrically corrected to remove this parallax, resulting in a product with the uniform scale and geometric accuracy of a map. The process of creating an orthoimage is called **[orthorectification](@entry_id:1129216)** .

True [orthorectification](@entry_id:1129216) requires a rigorous sensor model and a **Digital Elevation Model (DEM)**, which provides the elevation of the ground surface. The process is fundamentally a per-pixel ray-tracing operation. For each pixel in the source image, the sensor model defines its line-of-sight—a ray in 3D space originating from the sensor's perspective center. The [collinearity](@entry_id:163574) equation can be written as:

$\mathbf{X} = \mathbf{S}(t) + \lambda \mathbf{d}(r,c,t)$

where $\mathbf{X}$ is the unknown ground point, $\mathbf{S}(t)$ is the sensor position at time $t$, $\mathbf{d}(r,c,t)$ is the looking direction for pixel $(r,c)$, and $\lambda$ is an unknown scalar distance. To solve for the correct ground location of this pixel, we must find the unique point $\mathbf{X}$ that simultaneously lies on this ray *and* on the terrain surface defined by the DEM. This intersection point provides the true 3D ground coordinates $(X,Y,Z)$ for that pixel.

Once the correct ground coordinates are found, they are projected into the desired map coordinate system. This process is repeated for every pixel, explicitly modeling and removing the horizontal displacement caused by elevation variations. Simpler methods, such as applying a global affine transform, cannot model this spatially varying distortion and thus do not produce a [true orthoimage](@entry_id:1133458) .

#### Resampling: Creating the Final Image Grid

Whether performing a simple 2D transformation or a full [orthorectification](@entry_id:1129216), the final step is to create the output image on a new, regular grid. The process of determining the pixel values for this new grid is called **[resampling](@entry_id:142583)**. There are two main strategies for [resampling](@entry_id:142583) .

1.  **Forward Mapping**: This approach iterates through each pixel of the *source* image, applies the [geometric transformation](@entry_id:167502) $T$ to find its corresponding location in the *target* grid, and places the source pixel's value at that location. A major drawback of simple point-based forward mapping is that the projected source pixels will be irregularly spaced on the target grid, which can result in **holes** (target pixels that receive no data) and **overlaps** (target pixels that receive data from multiple source pixels). A more sophisticated approach, known as "splatting," involves mapping the entire footprint of the source pixel and distributing its energy across all the target pixels it covers. This area-based method avoids holes and helps conserve the total radiometric energy.

2.  **Inverse Mapping**: This is the more common and generally preferred approach. It iterates through each pixel of the *target* grid, applies the *inverse* transformation $T^{-1}$ to find its corresponding sub-pixel location in the *source* image, and then calculates a value for this location. Because every target pixel is explicitly assigned a value, this method inherently avoids holes and overlaps. The value for the sub-pixel location is determined by **interpolation** from the surrounding source pixels. Common interpolation methods include:
    -   **Nearest Neighbor**: Assigns the value of the closest source pixel. This is fast and preserves original pixel values but can result in a blocky appearance.
    -   **Bilinear Interpolation**: Averages the values of the four nearest source pixels, weighted by distance. This produces a smoother image but alters original pixel values.
    -   **Cubic Convolution**: Uses a larger neighborhood (16 pixels) to fit a smoother curve, yielding sharper results than [bilinear interpolation](@entry_id:170280) but with a risk of introducing "ringing" artifacts.

When [resampling](@entry_id:142583), it is crucial to consider both geometric and radiometric fidelity. Simple pointwise interpolation does not inherently preserve areal radiometric quantities like reflectance. The area of a target pixel projected back into the source image may be larger or smaller than the source pixel area, a distortion quantified by the **Jacobian determinant** of the transformation. Rigorous [resampling methods](@entry_id:144346) must account for this to ensure radiometric consistency. Furthermore, if the output grid is coarser than the input grid (downsampling), the **Nyquist-Shannon sampling theorem** dictates that the source image must be low-pass filtered before [resampling](@entry_id:142583) to prevent **aliasing**, where high-frequency details from the source image are misinterpreted as lower-frequency patterns in the output . Both area-based forward mapping and appropriate [inverse mapping](@entry_id:1126671) kernels (like integration over the projected pixel footprint) act as implicit low-pass filters.

### Methods for Finding Correspondences

The successful application of any transformation model depends on our ability to determine its parameters. This requires finding correspondences between the source image and the target map or reference image. Methods for finding these correspondences fall into two broad categories: area-based and feature-based.

#### Area-Based Matching: Cost Functions

Area-based methods work by directly comparing the intensity values of small patches (windows) of pixels between two images. A candidate transformation is evaluated by a **cost function** (or similarity metric) that measures the discrepancy or statistical dependence between the reference patch and the warped source patch. The optimal transformation is the one that minimizes this cost (or maximizes the similarity). The choice of cost function is critical, especially when registering multi-temporal or multi-sensor imagery where the radiometric relationship is not simple identity .

-   **Sum of Squared Differences (SSD)**: This metric computes the sum of the squared differences in intensity values between corresponding pixels. It is computationally simple but highly sensitive to radiometric differences. SSD assumes that pixel intensities are nearly identical, making it unsuitable for images with different sensor gains, offsets, or seasonal illumination changes.

-   **Normalized Cross-Correlation (NCC)**: This metric computes the correlation coefficient between the intensity values of the two patches. By subtracting the mean intensity from each patch (centering) and dividing by the standard deviation (normalizing), NCC becomes invariant to linear (affine) radiometric changes, i.e., changes in brightness ($b$) and contrast ($a$). If the intensity relationship is $I_2 \approx a \cdot I_1 + b$, NCC will still provide a strong match. This makes it far more robust than SSD for many remote sensing applications.

-   **Mutual Information (MI)**: This is an information-theoretic measure that quantifies the [statistical dependence](@entry_id:267552) between the intensity distributions of the two patches, estimated from their joint histogram. MI does not assume any particular functional form for the relationship between intensities. It simply measures how much information one image's intensity value provides about the other's. As long as a consistent (e.g., monotonic) relationship exists, MI will be maximized at the correct alignment. This makes MI exceptionally robust for registering images with complex, non-linear radiometric differences or even images from entirely different modalities (e.g., optical and thermal) where NCC would fail .

#### Feature-Based Matching: Keypoint Descriptors

Instead of comparing all pixels in a window, feature-based methods identify a sparse set of salient **keypoints** (e.g., corners, blobs) in both images, compute a descriptive [feature vector](@entry_id:920515) for the neighborhood of each keypoint, and then match keypoints based on the similarity of their descriptors. An effective keypoint descriptor must be robust to the geometric and photometric variations expected between the images.

The goal is to achieve **invariance**. A descriptor should be invariant to changes in scale, rotation, and illumination. Three of the most well-known descriptors are SIFT, SURF, and ORB .

-   **Scale-Invariant Feature Transform (SIFT)**: SIFT is widely regarded as a benchmark for its robustness. It achieves [scale invariance](@entry_id:143212) by detecting keypoints at their characteristic scale in a Gaussian scale-space. Rotation invariance is achieved by assigning a canonical orientation to each keypoint based on its local gradient distribution and rotating the descriptor to match. The descriptor itself is a histogram of gradient orientations within a $16 \times 16$ neighborhood, which provides robustness to non-linear illumination changes. The final 128-element descriptor vector is normalized to be invariant to affine changes in illumination contrast.

-   **Speeded-Up Robust Features (SURF)**: SURF was designed as a faster approximation of SIFT. It uses integral images to rapidly compute box-filter approximations of Hessian matrix [determinants](@entry_id:276593) for scale-space keypoint detection. Like SIFT, it finds a characteristic scale and orientation to achieve scale and rotation invariance. Its descriptor is based on sums of Haar wavelet responses in a local neighborhood. While faster than SIFT, its lower-dimensional summary is sometimes considered slightly less distinctive and less robust to complex, spatially varying illumination changes .

-   **Oriented FAST and Rotated BRIEF (ORB)**: ORB is designed for extreme speed, making it popular in real-time applications. It uses the FAST corner detector, which is not scale-invariant, but applies it across an image pyramid to provide scale robustness over discrete levels. Its key innovation is the use of the BRIEF descriptor, a binary string created from simple intensity comparison tests (e.g., is pixel $p$ brighter than pixel $q$?). Because it relies on raw intensity comparisons, BRIEF is very fast to compute and match. However, its performance degrades significantly in [multi-modal registration](@entry_id:895098) (e.g., optical-to-SAR), where the intensity relationship is not monotonic, causing the outcomes of the binary tests to become uncorrelated . In contrast, [gradient-based methods](@entry_id:749986) like SIFT and SURF, which capture structural information, are more robust in these challenging scenarios.

### Statistical Rigor in Parameter Estimation

Once a set of corresponding control points has been established, either manually or through automated matching, the parameters of the chosen [geometric transformation](@entry_id:167502) model are typically estimated using a least-squares adjustment. For high-accuracy applications, it is crucial to understand the statistical properties of this estimation process.

#### Uncertainty Propagation from Control Points

Ground Control Points are never perfectly known; their coordinates have measurement uncertainty. This uncertainty propagates through the least-squares estimation and results in uncertainty in the estimated transformation parameters. To model this correctly, we use **Weighted Least Squares (WLS)** .

Consider the linear model $\mathbf{z} = \mathbf{H} \boldsymbol{\theta} + \boldsymbol{\varepsilon}$, where $\mathbf{z}$ is the vector of observed GCP map coordinates, $\mathbf{H}$ is the design matrix derived from the image coordinates, $\boldsymbol{\theta}$ is the vector of unknown transformation parameters, and $\boldsymbol{\varepsilon}$ is the vector of observation errors. The uncertainty in the GCPs is described by the covariance matrix $\boldsymbol{\Sigma} = \operatorname{Cov}(\boldsymbol{\varepsilon})$. The WLS estimator, which minimizes the weighted [sum of squared errors](@entry_id:149299), is given by:

$\hat{\boldsymbol{\theta}} = (\mathbf{H}^{\top} \boldsymbol{\Sigma}^{-1} \mathbf{H})^{-1} \mathbf{H}^{\top} \boldsymbol{\Sigma}^{-1} \mathbf{z}$

The power of this method lies in its ability to properly weight the observations. Points with high uncertainty (large variance) receive less weight in the solution. The law of [covariance propagation](@entry_id:747989) can be applied to find the covariance matrix of the estimated parameters:

$\operatorname{Cov}(\hat{\boldsymbol{\theta}}) = (\mathbf{H}^{\top} \boldsymbol{\Sigma}^{-1} \mathbf{H})^{-1}$

This matrix is essential. Its diagonal elements give the variances of the estimated parameters (e.g., variance of the [scale factor](@entry_id:157673) or a rotation parameter), and its off-diagonal elements give their covariances. This allows for rigorous statistical analysis of the registration quality, such as computing confidence ellipses for the parameters. The technique of **[pre-whitening](@entry_id:185911)**, where the observation equations are transformed by $\boldsymbol{\Sigma}^{-1/2}$ to create a new system with identity [error covariance](@entry_id:194780), provides an equivalent way to derive this result and is a cornerstone of [statistical estimation theory](@entry_id:173693) .

#### Handling Correlated Residuals

A fundamental assumption of Ordinary Least Squares (OLS) is that the observation errors are [independent and identically distributed](@entry_id:169067) (iid). In remote sensing, this assumption is often violated. Residual errors at GCPs can exhibit **[spatial correlation](@entry_id:203497)** due to systematic effects that vary smoothly across an image, such as unmodeled lens distortion or [atmospheric refraction](@entry_id:202193) .

When errors are correlated, their covariance matrix $\boldsymbol{\Sigma}$ is not diagonal. In this case, the OLS estimator, while remaining **unbiased**, is no longer the Best Linear Unbiased Estimator (BLUE); that is, it is not the estimator with the minimum possible variance. The standard OLS variance formula becomes incorrect, leading to invalid statistical tests.

The correct approach is **Generalized Least Squares (GLS)**, which is identical in form to the WLS discussed above. The challenge lies in determining the [error covariance matrix](@entry_id:749077) $\boldsymbol{\Sigma}$. In practice, a **Feasible GLS (FGLS)** procedure is often used:
1.  An initial OLS fit is performed to obtain a set of residuals.
2.  The spatial structure of these residuals is analyzed by computing an **empirical semivariogram**, which plots the average squared difference between residuals as a function of their separation distance.
3.  A theoretical covariance model (e.g., exponential, spherical) is fitted to the empirical [semivariogram](@entry_id:1131466) to obtain a functional description of the covariance structure.
4.  This model is used to construct the estimated covariance matrix $\hat{\boldsymbol{\Sigma}}$.
5.  The GLS estimate is then computed using this $\hat{\boldsymbol{\Sigma}}$.

This rigorous geostatistical approach properly accounts for the correlated nature of the errors, yielding parameter estimates that are not only unbiased but also have the minimum achievable variance, along with a valid estimate of their uncertainty .