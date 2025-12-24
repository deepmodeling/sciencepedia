## Introduction
The accurate simulation of atmospheric flow in numerical weather and climate models is critically dependent on the chosen vertical coordinate system. While geometric height is intuitive, the presence of mountains and complex terrain complicates its use, leading to the development of sophisticated terrain-following and pressure-based coordinates. This article addresses the fundamental challenge of representing the lower boundary in [atmospheric models](@entry_id:1121200) and the evolution of coordinate systems designed to solve it. In the following chapters, you will embark on a comprehensive exploration of this topic. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, detailing the derivation and rationale behind pressure, log-pressure, sigma, and modern hybrid eta coordinates. The second chapter, "Applications and Interdisciplinary Connections," examines the practical consequences of these systems, focusing on the notorious [pressure gradient force error](@entry_id:1130148) and the diagnostic challenges they pose. Finally, "Hands-On Practices" provides an opportunity to apply these concepts, connecting the abstract theory to the concrete calculations performed within a numerical model.

## Principles and Mechanisms

The accurate representation of atmospheric processes in numerical models hinges on the choice of the vertical coordinate system. While geometric height, $z$, is the most intuitive vertical dimension, its direct use in global models is complicated by the presence of orography. A model with surfaces of constant geometric height would see its lower levels intersect mountains, creating complex boundary conditions that are difficult to handle numerically. Consequently, atmospheric models have adopted a variety of specialized vertical coordinates designed to address this issue while offering other computational advantages. This chapter explores the principles and mechanisms of the most common [vertical coordinate systems](@entry_id:1133787), from pressure-based coordinates to modern hybrid terrain-following systems.

### Pressure as a Vertical Coordinate

The use of **pressure** ($p$) as a vertical coordinate, rather than geometric height, has been a cornerstone of dynamical meteorology and numerical modeling for decades. This choice is deeply connected to the assumption of **hydrostatic balance**, a state where the downward force of gravity is balanced by the upward-directed pressure gradient force. For a fluid parcel of density $\rho$ and thickness $dz$, this balance is expressed as:

$$
\frac{\partial p}{\partial z} = -\rho g
$$

where $g$ is the [acceleration due to gravity](@entry_id:173411). The negative sign indicates that pressure decreases as height increases. A key consequence of this relationship is that pressure becomes a monotonic function of height, making it a valid vertical coordinate.

The most significant advantage of using [pressure coordinates](@entry_id:1130145) in a hydrostatic model arises from the simplification of the **mass continuity equation**. The mass of an atmospheric column per unit area between two pressure surfaces, $p_1$ and $p_2$, is given by integrating the density over height: $\int_{z_1}^{z_2} \rho \, dz$. Using the hydrostatic equation, we can write $\rho dz = -dp/g$, which allows us to find the mass simply by knowing the pressure at the top and bottom of the column:

$$
m = \int_{p_1}^{p_2} -\frac{dp}{g} = \frac{p_1 - p_2}{g}
$$

This demonstrates that, under hydrostatic balance, pressure functions as a **mass coordinate**: equal increments in pressure correspond to equal increments in atmospheric mass per unit area. This property allows for a profound simplification of the mass continuity equation. When transformed from height coordinates to pressure coordinates, the continuity equation takes the elegant form:

$$
\nabla_p \cdot \mathbf{v} + \frac{\partial \omega}{\partial p} = 0
$$

Here, $\mathbf{v}$ is the horizontal velocity vector, $\nabla_p$ is the horizontal [gradient operator](@entry_id:275922) on a constant pressure (isobaric) surface, and $\omega \equiv Dp/Dt$ is the vertical velocity in the pressure coordinate system. Notably, the air density $\rho$ does not appear explicitly in this equation. Eliminating density as a prognostic variable simplifies the governing equations and the numerical schemes required to solve them, a primary motivation for the widespread use of pressure-based coordinates in hydrostatic primitive-equation models .

### Log-Pressure Coordinates

While [pressure coordinates](@entry_id:1130145) simplify the continuity equation, the vertical spacing of constant-pressure surfaces in terms of geometric height is not uniform. Due to the exponential decay of pressure with height, a fixed pressure interval $\Delta p$ corresponds to a much larger height interval $\Delta z$ in the upper atmosphere than near the surface. To create a coordinate system that more closely resembles geometric height, the **[log-pressure coordinate](@entry_id:1127426)** is often used. It is typically defined as:

$$
\zeta = \ln\left(\frac{p_0}{p}\right) \quad \text{or sometimes as} \quad l = H \ln\left(\frac{p_0}{p}\right)
$$

where $p_0$ is a constant reference pressure, often set to mean sea level pressure (e.g., $1000$ hPa), and $H$ can be a representative scale height. To understand the "height-like" nature of this coordinate, we can derive the relationship between $z$ and $\zeta$. From the definition of $\zeta$, we find its differential: $d\zeta = -dp/p$. By combining the hydrostatic equation and the ideal gas law ($p = \rho R T$), we get:

$$
\frac{dp}{p} = -\frac{g}{RT} dz
$$

Substituting $d\zeta$ for $-dp/p$, we arrive at a fundamental relationship:

$$
d\zeta = \frac{g}{RT} dz \quad \implies \quad dz = \frac{RT}{g} d\zeta
$$

The term $H = RT/g$ is known as the **pressure scale height**. In a hypothetical [isothermal atmosphere](@entry_id:203207) where $T$ is constant, the scale height $H$ is also constant. The relationship integrates to $z - z_{\text{ref}} = H (\zeta - \zeta_{\text{ref}})$, revealing a linear mapping between geometric height and the [log-pressure coordinate](@entry_id:1127426). This means that equally spaced levels in $\zeta$ correspond to equally spaced levels in geometric height $z$. While the real atmosphere is not isothermal, this property makes log-pressure coordinates particularly useful for providing more uniform vertical resolution in modeling the middle atmosphere, where temperature variations are less pronounced than in the troposphere .

The practical utility of this coordinate can be seen in calculating the geometric thickness of an atmospheric layer. By integrating the differential relationship, the thickness $\Delta z = z_2 - z_1$ between two pressure levels $p_1$ and $p_2$ is found by integrating over the corresponding log-pressure levels $l_1$ and $l_2$:

$$
\Delta z = \int_{l_1}^{l_2} \frac{R_d T(l)}{g} dl
$$

For a given temperature profile $T(l)$, this integral can be evaluated analytically or numerically. For example, if we consider a layer between $p_1 = 800\,\text{hPa}$ and $p_2 = 400\,\text{hPa}$ with a reference pressure $p_0 = 1000\,\text{hPa}$ and a specified temperature profile, one can directly compute the geometric thickness, demonstrating how physical quantities are retrieved from the model's abstract coordinate system .

### The Challenge of Orography: The Sigma ($\sigma$) Coordinate

Neither pressure nor log-pressure coordinates solve the fundamental problem of how to represent topography. An isobaric surface at $p=900\,\text{hPa}$, for instance, would lie below the ground over high-elevation regions like the Tibetan Plateau. The first widely adopted solution to this was the **terrain-following sigma ($\sigma$) coordinate**, introduced by Norman Phillips. It is a normalized pressure coordinate defined as:

$$
\sigma = \frac{p - p_t}{p_s - p_t}
$$

Here, $p_s(x,y)$ is the pressure at the Earth's surface, which varies with location due to both weather systems and underlying topography, and $p_t$ is the pressure at the model's fixed top boundary, which is typically a small constant value (e.g., $p_t=0$ or a value near the stratopause). By this definition, $\sigma$ ranges from $\sigma=1$ at the surface ($p=p_s$) to $\sigma=0$ at the model top ($p=p_t$). The crucial feature of the $\sigma$-coordinate is that its lowest level, $\sigma=1$, always coincides with the ground, regardless of the terrain's elevation.

We can visualize the geometry of $\sigma$-surfaces by deriving an expression for the geometric height $z$ as a function of the model coordinates $(x, \sigma)$. Assuming for simplicity an [isothermal atmosphere](@entry_id:203207) with temperature $T$, the [hypsometric equation](@entry_id:1126310) gives the height $z$ corresponding to a pressure $p$ relative to a reference pressure $p_{\text{ref}}$ at height $z_{\text{ref}}$: $z - z_{\text{ref}} = -\frac{RT}{g} \ln(p/p_{\text{ref}})$. Using mean sea level as the reference ($z_{\text{ref}}=0, p_{\text{ref}}=p_0$), we have $z(p) = -\frac{RT}{g} \ln(p/p_0)$. To find $z(x, \sigma)$, we first express $p$ in terms of $\sigma$: $p(x,\sigma) = p_t + \sigma(p_s(x) - p_t)$. Substituting this into the [hypsometric equation](@entry_id:1126310) yields the absolute geometric height of a $\sigma$-surface:

$$
z(x,\sigma) = -\frac{RT}{g} \ln\left(\frac{p_t + \sigma(p_s(x) - p_t)}{p_0}\right)
$$

This expression  explicitly shows that the height of a $\sigma$-surface depends on the horizontal position $x$ through the surface pressure $p_s(x)$. Surfaces of constant $\sigma$ are not flat; they follow the terrain near the ground and become progressively flatter at higher altitudes (as $\sigma \to 0$).

### The Pressure Gradient Force Problem in Terrain-Following Coordinates

While the $\sigma$-coordinate system successfully incorporates orography, it introduces a severe numerical problem related to the calculation of the **horizontal pressure [gradient force](@entry_id:166847) (PGF)**. The PGF is the primary driver of atmospheric motion, and its accurate calculation is paramount. In height or [pressure coordinates](@entry_id:1130145), the PGF is simply the gradient of geopotential ($\phi=gz$) on an isobaric surface, $-\nabla_p \phi$.

However, surfaces of constant $\sigma$ are **not** isobaric, except in the trivial case of a flat surface with no weather systems ($p_s$ is constant). Pressure varies along a $\sigma$-surface. When the horizontal PGF is transformed into the $\sigma$-coordinate system, it takes the form of two terms (where $\alpha=1/\rho$ is specific volume):

$$
-\nabla_p \phi = -\nabla_\sigma \phi - \alpha \nabla_\sigma p
$$

The first term, $-\nabla_\sigma \phi$, represents the gradient of geopotential along the sloping $\sigma$-surface. The second term is a correction that accounts for the variation of pressure along that same surface. Over steep orography, the $\sigma$-surfaces are steeply sloped. This causes both terms in the PGF calculation to become very large in magnitude but nearly equal and opposite in sign. The physical PGF is the small residual that results from subtracting these two large quantities. This calculation is extremely susceptible to [truncation errors](@entry_id:1133459) in numerical models, leading to spurious (non-physical) horizontal forces that can generate unrealistic winds and degrade the forecast, especially in mountainous regions. This is often referred to as the **[pressure gradient force error](@entry_id:1130148)** .

### Hybrid Vertical Coordinates: The $\eta$ System

To mitigate the PGF error while retaining the terrain-following capability, modern numerical models predominantly use **hybrid terrain-following/[pressure coordinates](@entry_id:1130145)**, commonly denoted by $\eta$. The philosophy behind the hybrid coordinate is to combine the best features of the $\sigma$-coordinate and the pressure coordinate. The pressure on a [hybrid coordinate](@entry_id:1126227) surface is defined by a general formula:

$$
p(\eta) = A(\eta) p_r + B(\eta) p_s
$$

where $p_s$ is the surface pressure, $p_r$ is a constant reference pressure, and $A(\eta)$ and $B(\eta)$ are prescribed functions that define the structure of the coordinate system. Sometimes the formula is written as $p(\eta) = A(\eta) + B(\eta) p_s$, where the first term implicitly contains the reference pressure.

The functions $A(\eta)$ and $B(\eta)$ are designed to make the coordinate system behave like a $\sigma$-coordinate near the surface and smoothly transition to a pure pressure coordinate at higher altitudes . This is achieved through the following design:
-   **Near the surface** (e.g., as $\eta \to 1$): The coefficients are set such that $B(\eta) \to 1$ and $A(\eta) \to 0$. In this limit, $p(\eta) \approx p_s$, so the coordinate surfaces follow the terrain.
-   **High in the atmosphere** (e.g., as $\eta \to 0$): The coefficients are set such that $B(\eta) \to 0$. In this limit, $p(\eta) \approx A(\eta) p_r$. Since $A$ is a function of $\eta$ only, surfaces of constant $\eta$ become surfaces of constant pressure (isobaric).

By ensuring that the coordinate surfaces become isobaric in the upper troposphere and stratosphere, the steep slopes are eliminated where they are not needed. This drastically reduces the magnitude of the two competing terms in the PGF calculation aloft, thereby mitigating the numerical cancellation error.

The boundary conditions for the hybrid system are an important part of its definition. For a model with a fixed pressure top at $p=p_t$, the coordinate $\eta_t$ corresponding to the top must satisfy $p(\eta_t) = p_t$ for any surface pressure $p_s$. For the equation $p_t = A(\eta_t)p_r + B(\eta_t)p_s$ to hold for all $p_s$, the coefficient of $p_s$ must be zero. This requires $B(\eta_t) = 0$, which in turn implies $A(\eta_t) p_r = p_t$ .

### Coordinate Transformation and Metric Terms

To solve the governing equations of atmospheric motion (e.g., for momentum, heat, and mass) in a generalized vertical coordinate system like the $\eta$-coordinate, the equations must be formally transformed from physical space $(x,y,z)$ to the model's computational space $(x,y,\eta)$. This transformation involves geometric factors, or **metric terms**, that account for the non-orthogonal, curvilinear nature of the coordinate system.

A fundamental metric term is the **Jacobian of the coordinate transformation**, which relates a differential volume element in the model's coordinates, $dV_{\text{model}} = dx\,dy\,d\eta$, to the physical [volume element](@entry_id:267802), $dV_{\text{phys}} = dx\,dy\,dz$. The Jacobian determinant is defined as:

$$
J = \det\left(\frac{\partial(x,y,z)}{\partial(x,y,\eta)}\right) = \begin{vmatrix}
\frac{\partial x}{\partial x}  & \frac{\partial x}{\partial y}  & \frac{\partial x}{\partial \eta} \\
\frac{\partial y}{\partial x}  & \frac{\partial y}{\partial y}  & \frac{\partial y}{\partial \eta} \\
\frac{\partial z}{\partial x}  & \frac{\partial z}{\partial y}  & \frac{\partial z}{\partial \eta}
\end{vmatrix}
$$

Since the horizontal coordinates are the same in both systems ($x \leftrightarrow x$, $y \leftrightarrow y$), this determinant simplifies to the partial derivative of height with respect to the new vertical coordinate, holding the horizontal coordinates constant:

$$
J = \left(\frac{\partial z}{\partial \eta}\right)_{x,y}
$$

This term represents the physical thickness of a layer of unit thickness in $\eta$-space. To derive an expression for it, we can use the chain rule and the fundamental physical laws. We have $(\partial z / \partial \eta) = (\partial z / \partial p) (\partial p / \partial \eta)$. From the hydrostatic equation and [ideal gas law](@entry_id:146757), we know $(\partial z / \partial p) = -RT/(pg)$. From the definition of the hybrid coordinate, $p = A(\eta)p_r + B(\eta)p_s$, we can find the derivative with respect to $\eta$:

$$
\left(\frac{\partial p}{\partial \eta}\right)_{x,y} = A'(\eta) p_r + B'(\eta) p_s
$$

where $A' = dA/d\eta$ and $B' = dB/d\eta$. Combining these pieces, we obtain the expression for the Jacobian:

$$
J = \left(\frac{\partial z}{\partial \eta}\right)_{x,y} = -\frac{RT(\eta)}{p g} \left(A'(\eta) p_r + B'(\eta) p_s\right)
$$

Substituting the definition of $p$ back into the denominator gives the final, self-contained expression:

$$
J = -\frac{RT(\eta)}{g} \frac{A'(\eta) p_r + B'(\eta) p_s}{A(\eta) p_r + B(\eta) p_s}
$$

This expression  is a crucial component in the transformed set of governing equations. It demonstrates how the abstract definition of the [hybrid coordinate](@entry_id:1126227), through the functions $A(\eta)$ and $B(\eta)$, is rigorously connected to the physical geometry of the model's layers via the fundamental laws of atmospheric physics.