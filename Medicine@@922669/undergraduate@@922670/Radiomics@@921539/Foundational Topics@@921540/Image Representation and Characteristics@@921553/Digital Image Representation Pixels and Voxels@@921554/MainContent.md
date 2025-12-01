## Introduction
Digital images are the cornerstone of modern quantitative fields, from medical radiomics to computational [geosciences](@entry_id:749876). Far from being simple pictures, they are complex data structures—discrete grids of numbers representing an underlying physical reality. A fundamental understanding of how this digital representation is created is crucial for anyone performing quantitative analysis, as misinterpretations of the data's nature can lead to flawed conclusions and non-[reproducible research](@entry_id:265294). This article addresses a critical knowledge gap by demystifying the transition from a continuous physical world to a discrete grid of pixels and voxels.

Across the following chapters, you will gain a comprehensive understanding of digital image representation. The first chapter, **"Principles and Mechanisms,"** will break down the core processes of [sampling and quantization](@entry_id:164742), explain the geometry of the voxel grid, and introduce the artifacts that arise from this discretization. Next, **"Applications and Interdisciplinary Connections"** will explore the real-world impact of these principles, showing how they govern [data standardization](@entry_id:147200) in medical imaging, enable physical simulations in [geosciences](@entry_id:749876), and affect feature stability in radiomics. Finally, **"Hands-On Practices"** will offer concrete exercises to solidify your grasp of concepts like padding, resolution, and connectivity. We begin by examining the fundamental principles that govern how every [digital image](@entry_id:275277) comes into being.

## Principles and Mechanisms

A digital medical image, such as one from Computed Tomography (CT) or Magnetic Resonance Imaging (MRI), is fundamentally a discrete, finite representation of an underlying physical reality. That reality can be modeled as a continuous scalar field, a function $f: \mathbb{R}^n \to \mathbb{R}$ that maps a spatial position $\mathbf{r}$ in $n$-dimensional space (typically $n=2$ for a single slice or $n=3$ for a volume) to a physical quantity. This quantity could be radiodensity in Hounsfield Units (HU) for CT, or signal intensity related to proton density and [relaxation times](@entry_id:191572) for MRI. The process of converting this continuous field into a digital image involves two fundamental steps: [sampling and quantization](@entry_id:164742).

### From Continuous Reality to Discrete Representation

The transition from a continuous physical field to a grid of numbers is the cornerstone of [digital imaging](@entry_id:169428). Understanding this process is critical, as it defines the properties and limitations of the data from which all subsequent radiomic features are derived.

#### Sampling: The Voxel as a Point Sample

**Sampling** is the process of measuring the continuous field $f(\mathbf{r})$ at a discrete set of spatial locations. In most medical imaging modalities, these locations form a regular Cartesian lattice. This lattice is defined by a set of sampling intervals, or spacings, $(\Delta x, \Delta y, \Delta z)$, along each axis. A mathematically precise view considers sampling as the evaluation of the field at discrete points $\mathbf{r}_{\mathbf{n}} = (n_x\Delta x, n_y\Delta y, n_z\Delta z)$, where $\mathbf{n}=(n_x,n_y,n_z)$ is a triplet of integers indexing the lattice positions.

This process transforms the continuous-domain function $f(\mathbf{r})$ into a discrete-domain sequence of real-valued samples, $f_s[\mathbf{n}] = f(\mathbf{r}_{\mathbf{n}})$. Each individual element of this sequence is a **sample**. In two dimensions, a sample is commonly called a **pixel** (picture element), and in three dimensions, it is called a **voxel** ([volume element](@entry_id:267802)). It is crucial to recognize that, from a signal processing perspective, a voxel represents the value of the field at a single point, not a small cube of uniform intensity. The common visualization of images as a mosaic of constant-intensity squares or cubes is technically a form of simple reconstruction (specifically, [zero-order hold](@entry_id:264751) or nearest-neighbor interpolation), not a depiction of the sampling process itself [@problem_id:4536934].

#### Quantization: Digitizing Intensity

After sampling, the value at each voxel is still a real number, which cannot be stored with finite [computer memory](@entry_id:170089). **Quantization** is the process that maps these continuous-valued samples to a finite set of discrete intensity levels. This is typically achieved using a fixed number of binary digits, or **bits**, a quantity known as the **bit depth**, $B$.

An unsigned integer representation with bit depth $B$ provides $2^B$ distinct codes, typically ranging from $0$ to $2^B - 1$. The imaging system or post-processing software defines a physical dynamic range, an interval of physical values $[I_{\min}, I_{\max}]$, that will be mapped to this set of integer codes. In a [uniform quantizer](@entry_id:192441), this physical range is divided into equal-sized bins. When $I_{\min}$ is mapped to the lowest code ($0$) and $I_{\max}$ is mapped to the highest code ($2^B - 1$), there are $2^B - 1$ intervals between the $2^B$ discrete levels. The physical size of each of these intervals, known as the **quantization step** $\Delta_I$, is therefore:

$$
\Delta_I = \frac{I_{\max} - I_{\min}}{2^B - 1}
$$

Any physical value that falls outside the specified dynamic range $[I_{\min}, I_{\max}]$ cannot be represented uniquely. Such values are typically clipped to the nearest representable extreme, a phenomenon known as **saturation**. For instance, any true value $x \lt I_{\min}$ is stored as code $0$, and any value $x \gt I_{\max}$ is stored as code $2^B - 1$. This results in a loss of information at the extremes of the intensity scale [@problem_id:4536961]. It is important to distinguish the bit depth $B$, which determines the precision of the intensity value, from the voxel size $(\Delta x, \Delta y, \Delta z)$, which determines the spatial sampling density. The two are independent parameters of the digitization process.

### The Geometry of the Voxel Grid

The spatial arrangement of voxels defines the geometric framework of the image. This geometry is characterized by the voxel spacings and the orientation of the grid in physical space.

A voxel grid is defined by three sampling intervals or **spacings**, $(\Delta x, \Delta y, \Delta z)$, which represent the physical distance between the centers of adjacent voxels along the grid's own orthogonal axes. The **voxel volume** is simply the product of these spacings: $V = \Delta x \Delta y \Delta z$. This volume is an intrinsic property of the sampling lattice and is independent of how the lattice is oriented in physical space, provided its axes remain orthogonal [@problem_id:4536930].

When all three spacings are equal ($\Delta x = \Delta y = \Delta z$), the sampling grid is **isotropic**. This is ideal for many analyses as the spatial resolution is uniform in all directions. However, in many clinical scenarios, particularly with CT, acquisitions are **anisotropic**. For example, a CT scan might have high in-plane resolution with spacings of $\Delta x = 0.8 \, \mathrm{mm}$ and $\Delta y = 0.8 \, \mathrm{mm}$, but a lower through-plane resolution with a larger slice thickness and spacing, such as $\Delta z = 1.6 \, \mathrm{mm}$. This anisotropy is an intrinsic property of the sampling distances and cannot be changed by simply rotating the image. It has significant practical consequences, most notably an increase in the **partial volume effect** along the axis with the largest spacing, where anatomical details are more likely to be averaged within a single voxel [@problem_id:4536930].

### Mapping Voxel Indices to Physical Space

For quantitative analysis and clinical interpretation, it is essential to relate the abstract integer indices $(i, j, k)$ of a voxel in a data array to its precise physical location $(x, y, z)$ within a patient-based coordinate system. This is accomplished via an affine transformation.

#### The DICOM Model

The Digital Imaging and Communications in Medicine (DICOM) standard provides a practical framework for this mapping. The transformation is defined by three key attributes:

1.  **Image Position (Patient) (0020,0032)**: A vector $\mathbf{o}$ specifying the $(x, y, z)$ coordinates in millimeters of the center of the first voxel in the image volume, typically corresponding to index $(i,j,k)=(0,0,0)$.

2.  **Image Orientation (Patient) (0020,0037)**: Two orthonormal 3D vectors, $\hat{\mathbf{r}}$ and $\hat{\mathbf{c}}$, that specify the direction of the rows and columns of the image slices in the patient coordinate system. The row direction corresponds to the direction of increasing row index $j$, and the column direction corresponds to increasing column index $i$.

3.  **Pixel Spacing (0028,0030)**: Two values, $(\Delta r, \Delta c)$, giving the physical distance between voxel centers along the row and column directions, respectively.

The direction of the third axis (the slice direction), $\hat{\mathbf{s}}$, is perpendicular to the image plane and can be found by taking the cross product of the row and column vectors: $\hat{\mathbf{s}} = \hat{\mathbf{r}} \times \hat{\mathbf{c}}$. With an additional parameter for the spacing between slices, $\Delta s$, the physical position $\mathbf{p}(i,j,k)$ of the center of the voxel at zero-based indices $(i,j,k)$ is given by:

$$
\mathbf{p}(i,j,k) = \mathbf{o} + j \Delta r \hat{\mathbf{r}} + i \Delta c \hat{\mathbf{c}} + k \Delta s \hat{\mathbf{s}}
$$

For example, consider a CT series with row/column spacing of $0.7 \, \mathrm{mm}$, slice spacing of $1.25 \, \mathrm{mm}$, an origin at $(-150, -150, -50)$, and an orientation where the rows align with the patient's x-axis ($\hat{\mathbf{r}}=(1,0,0)$) and columns with the y-axis ($\hat{\mathbf{c}}=(0,1,0)$). The slice direction would be $\hat{\mathbf{s}} = (0,0,1)$. The position of the voxel at index $(i=100, j=50, k=16)$ would be calculated as:
$\mathbf{p}(100,50,16) = (-150,-150,-50) + 50(0.7)(1,0,0) + 100(0.7)(0,1,0) + 16(1.25)(0,0,1) = (-115, -80, -30) \, \mathrm{mm}$ [@problem_id:4536948].

#### The General Affine Transformation

The DICOM model is a specific instance of a more general affine transformation, which can be elegantly represented by a single $4 \times 4$ matrix $\mathbf{A}$ in [homogeneous coordinates](@entry_id:154569):
$$
\begin{bmatrix}
x \\ y \\ z \\ 1
\end{bmatrix}
=
\mathbf{A}
\begin{bmatrix}
i \\ j \\ k \\ 1
\end{bmatrix}
=
\begin{bmatrix}
m_{11}  m_{12}  m_{13}  t_x \\
m_{21}  m_{22}  m_{23}  t_y \\
m_{31}  m_{32}  m_{33}  t_z \\
0  0  0  1
\end{bmatrix}
\begin{bmatrix}
i \\ j \\ k \\ 1
\end{bmatrix}
$$
The upper-left $3 \times 3$ submatrix $\mathbf{M}$ encodes scaling, rotation, and **shear**, while the last column $\mathbf{t}$ encodes translation. The physical origin (position of voxel $(0,0,0)$) is given directly by the translation vector $\mathbf{t} = (t_x, t_y, t_z)^T$.

The columns of $\mathbf{M}$ are particularly informative: the first column is the physical displacement vector corresponding to a unit step along the $i$-index axis, the second column corresponds to a step along the $j$-axis, and the third to the $k$-axis. The voxel spacings are the Euclidean norms (lengths) of these column vectors. If these column vectors are not mutually orthogonal (i.e., their dot products are non-zero), the grid is said to possess **shear**, meaning the grid axes are not perpendicular in physical space. For instance, the matrix $\mathbf{A}$ below defines a sheared grid with spacings $s_i=2$, $s_j=\sqrt{2.5}$, and $s_k=\sqrt{1.25}$, and an origin at $(10,20,30)$ [@problem_id:4536933].
$$
\mathbf{A}=\begin{bmatrix} 2  0.5  0  10 \\ 0  1.5  0.5  20 \\ 0  0  1  30 \\ 0  0  0  1 \end{bmatrix}
$$

### The Limits of Discretization: Resolution and Artifacts

The act of digitizing a continuous field inevitably introduces limitations and potential artifacts. The fidelity of the digital representation is constrained by the system's resolution and the effects of sampling.

#### Spatial Resolution and the Modulation Transfer Function

**Spatial resolution** refers to the ability of an imaging system to distinguish small, closely spaced objects. It is fundamentally limited by the inherent blurring of the system. In a linear, shift-invariant system, this blurring is completely characterized by the **Point Spread Function (PSF)**, which is the system's response to an idealized [point source](@entry_id:196698). A narrower PSF indicates less blur and better spatial resolution.

The **Line Spread Function (LSF)** is the response to an idealized line source and is equivalent to the integral of the 2D PSF in the direction perpendicular to the line. The Fourier transform of the PSF gives the Optical Transfer Function (OTF), and its magnitude is the **Modulation Transfer Function (MTF)**. The MTF describes how well the system transfers contrast from the object to the image as a function of [spatial frequency](@entry_id:270500). A system with better spatial resolution will have higher MTF values at higher spatial frequencies. The primary physical factors limiting resolution are modality-specific, including [x-ray](@entry_id:187649) focal spot and detector size in CT; k-space coverage and $T_2^*$ decay in MRI; and positron range and [detector physics](@entry_id:748337) in PET [@problem_id:4536935].

#### The Partial Volume Effect

The **partial volume effect (PVE)** is a crucial artifact where the intensity of a single voxel reflects an average of the properties of multiple underlying tissues. This occurs for two primary reasons:

1.  **Tissue-Fraction Mixing**: This occurs when a voxel's finite physical volume straddles a boundary between different tissue types. In an ideal system with no blurring (i.e., PSF is a Dirac delta function), the voxel's value would be the simple volume-fraction-weighted average of the tissues it contains. For example, a voxel half-filled with tissue A ($\mu_A=100$) and half-filled with tissue B ($\mu_B=0$) would record a value of $50$ [@problem_id:4536920].

2.  **PSF-Induced Blurring**: This is a more subtle effect caused by the system's inherent blur (a non-zero-width PSF). The signal from one tissue can "spill over" or blur into voxels that are geometrically located entirely within an adjacent tissue. This means that even an infinitesimally small voxel located just inside tissue A near a boundary with tissue B will record a value influenced by B, and thus different from the pure value $\mu_A$. This effect persists even as voxel size approaches zero [@problem_id:4536920].

PVE is a deterministic, [systematic error](@entry_id:142393) based on anatomy and imaging physics, not random noise. It can significantly impact the accuracy of radiomic features, especially texture features that are sensitive to local intensity variations.

#### Aliasing and Anti-Aliasing

The **Nyquist-Shannon [sampling theorem](@entry_id:262499)** states that to perfectly reconstruct a continuous signal from its samples, the [sampling frequency](@entry_id:136613) must be strictly greater than twice the maximum frequency present in the signal. The threshold, equal to half the [sampling frequency](@entry_id:136613) ($f_{Nyquist} = 1/(2\Delta x)$), is the Nyquist frequency. If the signal contains frequencies above this limit, they are not properly recorded; instead, they "fold over" and masquerade as lower frequencies in the sampled data. This artifact is known as **aliasing** [@problem_id:4536934].

This principle is critically important when [resampling](@entry_id:142583) an image to a coarser grid (downsampling). Downsampling from a fine grid with spacing $\Delta x$ to a coarse grid with spacing $\Delta'x > \Delta x$ effectively lowers the [sampling frequency](@entry_id:136613) and thus lowers the Nyquist limit. The original image may contain valid frequency components that are below its own Nyquist limit but are above the new, lower Nyquist limit of the coarse grid. If one simply discards samples (decimates) to achieve the downsampling, these high frequencies will cause aliasing, corrupting the image data.

To prevent this, it is mandatory to apply a low-pass **[anti-alias filter](@entry_id:746481)** to the image *before* downsampling. This filter removes any frequency components that are too high to be represented on the target grid. The cutoff frequency of this filter, $f_c$, must be less than or equal to the Nyquist frequency of the *target* grid: $f_c \le 1/(2\Delta'x)$. This procedure ensures that no aliasing occurs, at the cost of an intentional blurring that removes the finest details—a necessary trade-off to maintain the integrity of the remaining signal [@problem_id:4536955]. For instance, when downsampling from a $0.8\,\mathrm{mm}$ grid to a $1.6\,\mathrm{mm}$ grid, the pre-filter's cutoff should be no higher than $1 / (2 \times 1.6) = 0.3125 \, \mathrm{cycles/mm}$ [@problem_id:4536955].

### Working with Voxel Grids: Interpolation and Connectivity

Once an image exists as a discrete voxel grid, many radiomics operations, such as registration, resampling, or object analysis, require specific methods for working with this [discrete space](@entry_id:155685).

#### Interpolation: Reconstructing the Continuous Field

**Reconstruction**, the process of estimating the continuous field from its discrete samples, is practically achieved through **interpolation**. This is necessary whenever a value is needed at an off-grid location, such as when rotating an image or resampling it to an isotropic grid. The choice of interpolation method involves a trade-off between [computational efficiency](@entry_id:270255), smoothness of the result, and accuracy of the frequency content. Common methods are based on different 1D **interpolation kernels** $h(x)$, which are applied separably along each axis.

-   **Nearest-Neighbor Interpolation**: Uses a rectangular (box) kernel. It is computationally fastest, simply selecting the value of the nearest voxel. The result is piecewise constant and can exhibit severe blocky artifacts. Its frequency response is poor, leading to significant aliasing. In 3D, it uses 1 voxel per interpolated point.

-   **Linear (Tri-linear) Interpolation**: Uses a triangular kernel. It produces a continuous ($C^0$) result by taking a weighted average of the nearest neighbors. In 3D, this involves $2^3=8$ voxels. It is a good compromise between speed and quality, offering better [anti-aliasing](@entry_id:636139) performance than nearest-neighbor.

-   **Cubic B-spline Interpolation**: Uses a piecewise cubic kernel with a wider support. It yields a smoother result ($C^2$ continuous, meaning the first and second derivatives are continuous) and has excellent [anti-aliasing](@entry_id:636139) properties due to a frequency response that rapidly attenuates high frequencies. In 3D, it typically involves $4^3=64$ neighboring voxels.

-   **Sinc Interpolation**: Uses the [sinc function](@entry_id:274746) kernel, $\sin(\pi x)/(\pi x)$, which corresponds to an [ideal low-pass filter](@entry_id:266159) in the frequency domain. It provides perfect bandlimited reconstruction in theory but is computationally impractical due to its infinite spatial support. In practice, a windowed (truncated) version is used, which introduces its own artifacts (Gibbs phenomenon).

In general, kernels with larger spatial support and greater smoothness provide better approximations of the [ideal low-pass filter](@entry_id:266159), reducing artifacts at the cost of increased computation [@problem_id:4536939].

#### Connectivity: Defining Objects on the Grid

To analyze distinct objects within an image, such as tumors or organs from a segmentation mask, we must define what it means for two foreground voxels to be part of the same object. This is governed by the concept of **connectivity** or adjacency.

In a 2D grid, two common types of connectivity exist:
-   **4-connectivity**: Two pixels are connected if they share an edge. Each pixel has 4 such neighbors. This neighborhood is defined by the set of points $\mathbf{q}$ for which the Manhattan distance to the center pixel $\mathbf{p}$ is one: $\|\mathbf{q}-\mathbf{p}\|_1 = 1$.
-   **8-connectivity**: Two pixels are connected if they share an edge or a vertex. Each pixel has 8 such neighbors. This neighborhood corresponds to a Chebyshev distance of one: $\|\mathbf{q}-\mathbf{p}\|_\infty = 1$.

In 3D, this extends to three primary types:
-   **6-connectivity**: Voxels sharing a face ($\|\mathbf{q}-\mathbf{p}\|_1 = 1$).
-   **18-connectivity**: Voxels sharing a face or an edge ($\|\mathbf{q}-\mathbf{p}\|_\infty = 1$ and $1 \le \|\mathbf{q}-\mathbf{p}\|_1 \le 2$).
-   **26-connectivity**: Voxels sharing a face, an edge, or a vertex ($\|\mathbf{q}-\mathbf{p}\|_\infty = 1$).

A subtle but critical issue arises when defining connectivity for both the foreground (e.g., a lesion) and the background simultaneously. If the same connectivity is used for both (e.g., 8-connectivity for foreground and background), topological paradoxes can occur. A classic example is a 2D checkerboard pattern where both the black and white squares would be considered single, interpenetrating connected components, violating the Jordan Curve Theorem's analogue on a grid.

To ensure topologically consistent behavior, one must use **dual connectivity pairs** for the foreground and background. The standard valid pairs are:
-   In 2D: (4, 8) or (8, 4) for (foreground, background).
-   In 3D: (6, 26), (26, 6), or the self-dual pair (18, 18).

This choice ensures that digital objects behave in a way that is consistent with the topology of their continuous counterparts, which is essential for the robust calculation of topological features like the number of objects, holes, or surface area [@problem_id:4536936].