## Introduction
In an expanding universe, the simple, static notion of distance we use in everyday life breaks down. The vast separations between galaxies are not fixed but stretch along with the fabric of spacetime itself, fundamentally altering how we measure the cosmos. To bridge the gap between theoretical models of the universe and tangible observations like the brightness and apparent size of distant objects, cosmologists rely on a sophisticated toolkit of [distance measures](@entry_id:145286). These concepts are the bedrock of observational cosmology, allowing us to translate measured quantities like redshift and flux into a coherent map of cosmic history and composition. This article serves as a graduate-level guide to this essential framework.

This exploration is divided into three core sections. In "Principles and Mechanisms," we will derive the key [cosmological distances](@entry_id:160000)—comoving, luminosity, and angular diameter—directly from the geometric foundation of the Friedmann–Lemaître–Robertson–Walker (FLRW) metric. Following this, "Applications and Interdisciplinary Connections" will demonstrate how these distances are employed in practice, using [standard candles](@entry_id:158109) and rulers to probe the [expansion history of the universe](@entry_id:162026), constrain [cosmological parameters](@entry_id:161338), and test fundamental physics. Finally, "Hands-On Practices" provides a series of computational exercises to solidify theoretical understanding and build practical skills in [numerical cosmology](@entry_id:752779). We begin by laying the theoretical groundwork, establishing the principles that govern how we define and calculate distance on a cosmic scale.

## Principles and Mechanisms

In the context of an expanding and dynamic universe, the familiar Euclidean concept of distance becomes inadequate. The separation between two points is not a static quantity but changes with cosmic time, and the path light travels between them is affected by the expansion and curvature of spacetime itself. Consequently, cosmologists employ several distinct yet interrelated [distance measures](@entry_id:145286), each tailored to a specific type of observation. This chapter elucidates the principles underlying these [distance measures](@entry_id:145286), deriving them from the fundamental geometry of the Friedmann–Lemaître–Robertson–Walker (FLRW) metric.

### Fundamental Concepts of Cosmological Distance

The foundation for all [cosmological distance measures](@entry_id:276511) is the FLRW metric, which describes a spacetime that is homogeneous and isotropic on large scales. In [spherical coordinates](@entry_id:146054), the line element is given by:

$$
ds^2 = -c^2 dt^2 + a(t)^2 \left[ \frac{dr^2}{1 - K r^2} + r^2 (d\theta^2 + \sin^2\theta d\phi^2) \right]
$$

Here, $c$ is the speed of light, $t$ is cosmic time, $a(t)$ is the dimensionless scale factor (normalized to $a(t_0) = 1$ at the present time $t_0$), $r$ is the comoving [radial coordinate](@entry_id:165186), and $K$ is the [spatial curvature](@entry_id:755140) parameter. The coordinates $(r, \theta, \phi)$ form a **comoving coordinate system**, a conceptual grid that expands along with the universe. Objects that are at rest with respect to the Hubble flow maintain constant [comoving coordinates](@entry_id:271238).

To measure the distance to a remote object, we typically observe photons that have traveled from it to us. Photons travel along **[null geodesics](@entry_id:158803)**, for which the [spacetime interval](@entry_id:154935) $ds^2$ is zero. For a photon traveling radially from a source at comoving coordinate $r_e$ to an observer at the origin ($r=0$), we have $d\theta = d\phi = 0$. The [null geodesic](@entry_id:261630) condition simplifies to:

$$
c^2 dt^2 = a(t)^2 \frac{dr^2}{1 - K r^2}
$$

Rearranging for a path where $r$ decreases as $t$ increases, we find the change in comoving coordinate with respect to time is $dr = -\frac{c \sqrt{1 - K r^2}}{a(t)} dt$. For pedagogical simplicity, we can introduce a new [radial coordinate](@entry_id:165186) $\chi$ such that $d\chi = \frac{dr}{\sqrt{1-Kr^2}}$. The [null geodesic](@entry_id:261630) condition then becomes $c \, dt = -a(t) \, d\chi$.

The total [comoving distance](@entry_id:158059) traversed by a photon emitted at time $t_e$ from a source at comoving coordinate $\chi_e$ and observed at time $t_0$ is:

$$
\chi_e = \int_{t_e}^{t_0} \frac{c \, dt}{a(t)}
$$

This quantity, often denoted as the **line-of-sight [comoving distance](@entry_id:158059)**, $D_C$, represents the [proper distance](@entry_id:162052) between the source and observer at the present time, $t_0$, if the expansion were to be hypothetically frozen. To make this expression more practical, we express it as an integral over the observable quantity, **redshift** ($z$). The [redshift](@entry_id:159945) is defined by the stretching of light's wavelength due to cosmic expansion, given by $1+z = a(t_0)/a(t_e) = 1/a(t_e)$. Differentiating this with respect to time gives $dz/dt = -(1/a^2) \dot{a} = -(1+z)H(z)$, where $H(z) \equiv \dot{a}/a$ is the **Hubble parameter**. This provides the crucial relation $dt = -dz/((1+z)H(z))$. Substituting this into the integral for $\chi_e$, we arrive at the standard formula for the line-of-sight [comoving distance](@entry_id:158059) as a function of [redshift](@entry_id:159945) :

$$
D_C(z) = \chi(z) = c \int_0^z \frac{dz'}{H(z')}
$$

An immediate and profound consequence of this formula is the monotonic nature of [comoving distance](@entry_id:158059). In any expanding universe model where $H(z)$ is positive (a condition for expansion), the derivative $dD_C/dz = c/H(z)$ is always positive. This signifies that a source observed at a higher [redshift](@entry_id:159945) is always at a greater [comoving distance](@entry_id:158059). The photons from more distant sources have simply traveled a longer path along the comoving grid to reach us .

### The Role of Spatial Curvature: Transverse Comoving Distance

The line-of-sight [comoving distance](@entry_id:158059), $D_C$, measures distance along our line of sight. However, the spatial geometry of the universe also affects distances perpendicular to the line of sight. This is captured by the **transverse [comoving distance](@entry_id:158059)**, $D_M$. In the FLRW metric, $D_M(z)$ is the quantity that relates the physical transverse size of an object at [comoving distance](@entry_id:158059) $\chi$ to its angular size on the comoving grid. It is defined as $D_M(z) \equiv r(z)$, where $r$ is the original comoving coordinate in the metric.

The relationship between $D_M$ and $D_C$ depends on the [spatial curvature](@entry_id:755140). Integrating $d\chi = dr/\sqrt{1-Kr^2}$ gives $\chi$ as a function of $r$. Inverting this relationship yields $r(\chi)$, or $D_M(D_C)$. The curvature parameter $K$ is often expressed in terms of the present-day curvature [density parameter](@entry_id:265044), $\Omega_{k0} \equiv -K c^2 / (a_0^2 H_0^2) = -K c^2 / H_0^2$. This leads to three distinct cases for the geometry of space  :

1.  **Spatially Flat Universe ($K=0, \Omega_{k0}=0$)**: In this case, $d\chi = dr$, so $\chi = r$. The transverse [comoving distance](@entry_id:158059) is equal to the line-of-sight [comoving distance](@entry_id:158059): $D_M(z) = D_C(z)$.

2.  **Spatially Closed Universe ($K>0, \Omega_{k0}0$)**: This corresponds to a hyperspherical geometry. The relation is $D_M(z) = \frac{c}{H_0\sqrt{|\Omega_{k0}|}} \sin\left(\frac{H_0\sqrt{|\Omega_{k0}|}}{c}D_C(z)\right)$. For a given line-of-sight distance, transverse distances are smaller than in a [flat universe](@entry_id:183782), causing light rays to reconverge.

3.  **Spatially Open Universe ($K0, \Omega_{k0}>0$)**: This corresponds to a hyperbolic geometry. The relation is $D_M(z) = \frac{c}{H_0\sqrt{\Omega_{k0}}} \sinh\left(\frac{H_0\sqrt{\Omega_{k0}}}{c}D_C(z)\right)$. In this case, transverse distances are larger than in a [flat universe](@entry_id:183782), causing [light rays](@entry_id:171107) to diverge.

These three cases can be summarized in a single expression:

$$
D_M(z) =
\begin{cases}
\dfrac{c}{H_0\sqrt{\Omega_{k0}}}\,\sinh\left(\sqrt{\Omega_{k0}}\,\dfrac{H_0 D_C(z)}{c}\right),  \Omega_{k0}0 \\
D_C(z),  \Omega_{k0}=0 \\
\dfrac{c}{H_0\sqrt{|\Omega_{k0}|}}\,\sin\left(\sqrt{|\Omega_{k0}|}\,\dfrac{H_0 D_C(z)}{c}\right),  \Omega_{k0}0
\end{cases}
$$

### Observable Distances: Luminosity and Angular Diameter Distance

While $D_C$ and $D_M$ are theoretically fundamental, they are not directly observable. We must relate them to quantities we can measure, namely the flux of light from a source and its apparent size on the sky.

The **[angular diameter distance](@entry_id:157817)**, $D_A$, is defined as the ratio of an object's physical transverse size, $\ell_\perp$, to its observed angular size, $\theta$. For a small angle, $D_A \equiv \ell_\perp / \theta$. The physical size $\ell_\perp$ is the proper distance at the time of light emission, $t_e$. From the metric, this is $\ell_\perp = a(t_e) D_M(z) \theta$. Substituting this into the definition gives:

$$
D_A(z) = a(t_e) D_M(z) = \frac{D_M(z)}{1+z}
$$

This relation shows that the [angular diameter distance](@entry_id:157817) is the transverse [comoving distance](@entry_id:158059) scaled by the factor $1/(1+z)$, accounting for the fact that the universe was smaller when the light was emitted  .

The **[luminosity distance](@entry_id:159432)**, $D_L$, is defined to preserve the Euclidean [inverse-square law](@entry_id:170450) for flux. For a source of intrinsic bolometric luminosity $L$, the observed bolometric flux $F$ is given by $F \equiv L / (4\pi D_L^2)$. The observed flux is diluted by two effects beyond the simple spreading of light over a sphere of area $4\pi D_M(z)^2$. First, the energy of each photon is reduced by a factor of $(1+z)$ due to redshift. Second, the rate at which photons arrive is also reduced by a factor of $(1+z)$ due to cosmic [time dilation](@entry_id:157877). Thus, the total received power is reduced by $(1+z)^2$. The flux is:

$$
F = \frac{L/(1+z)^2}{4\pi D_M(z)^2} = \frac{L}{4\pi [(1+z)D_M(z)]^2}
$$

Comparing this with the definition of $D_L$, we find  :

$$
D_L(z) = (1+z)D_M(z)
$$

Combining the expressions for $D_A(z)$ and $D_L(z)$, we find a simple and profound relationship between them:

$$
D_L(z) = (1+z)^2 D_A(z)
$$

This is the **Etherington distance-duality relation**. Its validity rests on two fundamental assumptions: that gravity is described by a metric theory and that photon number is conserved along the [null geodesic](@entry_id:261630) path. Remarkably, it is independent of the specific dynamics of the universe (i.e., the form of $H(z)$), the [spatial curvature](@entry_id:755140), and whether spacetime is homogeneous or inhomogeneous. It holds locally along each light path, even in the presence of gravitational lensing .

### Distances in Practice: The $\Lambda$CDM Model

To compute numerical values for these distances, we must specify the [expansion history of the universe](@entry_id:162026), $H(z)$. In the [standard cosmological model](@entry_id:159833), the universe contains several components: non-relativistic matter (cold dark matter and [baryons](@entry_id:193732), $\Omega_m$), radiation ($\Omega_r$), and a [dark energy](@entry_id:161123) component, often modeled as a [cosmological constant](@entry_id:159297) ($\Omega_\Lambda$). The evolution of the energy density $\rho_i$ of a component with a constant equation-of-state parameter $w_i = p_i/\rho_i$ follows $\rho_i \propto (1+z)^{3(1+w_i)}$. The first Friedmann equation then gives the full expression for the Hubble parameter :

$$
H(z) = H_0 \sqrt{ \Omega_m (1+z)^3 + \Omega_r (1+z)^4 + \Omega_k (1+z)^2 + \Omega_{\rm de} (1+z)^{3(1+w)} }
$$

where $\Omega_i$ are the present-day density parameters and $\Omega_k = 1 - \sum_i \Omega_i$. For the standard flat $\Lambda$CDM model, this simplifies to $H(z) = H_0 \sqrt{ \Omega_m (1+z)^3 + \Omega_\Lambda }$.

In the low-redshift limit ($z \ll 1$), these complex integral formulae simplify. By Taylor expanding $H(z)$ around $z=0$, we find that all [distance measures](@entry_id:145286) converge to the same leading-order behavior :

$$
D_L(z) \approx D_A(z) \approx D_C(z) \approx \frac{c}{H_0} z
$$

Rearranging gives $H_0 D_L \approx cz$. Using the low-redshift approximation for recession velocity $v \approx cz$, we recover the familiar **Hubble's Law**, $v \approx H_0 d$. This demonstrates how the sophisticated framework of [cosmological distances](@entry_id:160000) is consistent with early, local observations of the expanding universe.

At higher redshifts, numerical integration is required. For example, in a flat $\Lambda$CDM model with $\Omega_m=0.3$, $\Omega_\Lambda=0.7$, and $H_0=70 \text{ km s}^{-1}\text{Mpc}^{-1}$, the [angular diameter distance](@entry_id:157817) to a source at $z=2$ can be calculated. First, the [comoving distance](@entry_id:158059) is found by numerically integrating $D_C(2) = (c/H_0) \int_0^2 [0.3(1+z')^3 + 0.7]^{-1/2} dz'$, yielding $D_C(2) \approx 5.18 \text{ Gpc}$. Then, the [angular diameter distance](@entry_id:157817) is $D_A(2) = D_C(2)/(1+2) \approx 1.73 \text{ Gpc}$ . Similarly, the [luminosity distance](@entry_id:159432) to a very high [redshift](@entry_id:159945) source, say at $z=6$, would be $D_L(6) = (1+6) D_C(6) \approx 5.77 \times 10^4 \text{ Mpc}$ .

### Peculiar Behaviors and Advanced Applications

The interplay between the expanding comoving grid and the geometric factors leads to some non-intuitive behaviors, which can be harnessed for cosmological tests.

One of the most striking features is the non-[monotonicity](@entry_id:143760) of the [angular diameter distance](@entry_id:157817). While [comoving distance](@entry_id:158059) $D_C(z)$ always increases with redshift, $D_A(z) = D_C(z)/(1+z)$ is a product of an increasing function and a decreasing function. Consequently, $D_A(z)$ initially increases with $z$, reaches a maximum at a specific redshift $z_{\rm max}$, and then decreases at higher redshifts . This means that a standard-sized object will appear to have its smallest angular size at $z_{\rm max}$ and will appear larger at both lower and higher redshifts. The condition for this maximum, found by setting $dD_A/dz=0$, is :

$$
D_C(z_{\rm max}) = \frac{c(1+z_{\rm max})}{H(z_{\rm max})}
$$

For an Einstein-de Sitter universe ($\Omega_m=1, \Omega_\Lambda=0$), this equation can be solved analytically to find $z_{\rm max}=1.25$. For the standard $\Lambda$CDM model, it must be solved numerically, yielding values typically in the range of $z \approx 1.5 - 2.0$.

Furthermore, [cosmological distance measures](@entry_id:276511) provide a powerful tool to test fundamental physics by searching for violations of their underlying assumptions. For instance, the distance-duality relation, $D_L = (1+z)^2 D_A$, relies on photon number conservation. If some photons are lost along the line of sight, for example, through scattering by free electrons during the [epoch of reionization](@entry_id:161482) (quantified by [optical depth](@entry_id:159017) $\tau$) or by converting into other particles like axions, the observed flux will be attenuated: $F_{\rm obs} = F_{\rm true} e^{-\tau(z)}$ .

This attenuation does not change the geometric spacetime and thus leaves $D_A$ unaffected. However, an observer interpreting the diminished flux via the standard definition would infer an "observed" [luminosity distance](@entry_id:159432) $D_L^{\rm obs}(z)$ that is larger than the true geometric distance :

$$
D_L^{\rm obs}(z) = D_L(z) e^{\tau(z)/2}
$$

If such data were used to test a phenomenological deviation from distance duality, parameterized by $D_L/D_A = (1+z)^{2+\epsilon}$, the opacity would induce a non-zero bias in the measurement of $\epsilon$. The observed ratio would be $D_L^{\rm obs}/D_A = (D_L/D_A) e^{\tau/2} = (1+z)^2 e^{\tau/2}$. Equating this to $(1+z)^{2+\epsilon_{\rm bias}}$ and solving for the bias yields:

$$
\epsilon_{\rm bias}(z) = \frac{\tau(z)}{2 \ln(1+z)}
$$

Such analyses demonstrate the crucial role of [cosmological distance measures](@entry_id:276511) not just in mapping the [expansion history of the universe](@entry_id:162026), but also in probing the fundamental properties of light and spacetime itself.