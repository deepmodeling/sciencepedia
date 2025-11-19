## Introduction
The polarization of an electromagnetic wave is one of its most fundamental properties, yet its implications are remarkably far-reaching, influencing everything from the way we see the world to the frontiers of modern physics. It describes the geometric orientation of the oscillating electric field as the wave travels through space. A complete grasp of polarization is essential not just for understanding the nature of light itself, but also for harnessing it in countless technological applications. This article bridges the gap between the abstract theory of polarization and its tangible impact, providing a comprehensive journey through its core principles, mathematical descriptions, and diverse applications.

Across the following chapters, you will build a robust understanding of this fascinating phenomenon. We will begin in **Principles and Mechanisms** by dissecting the different types of polarization—linear, circular, and elliptical—and introducing the elegant mathematical frameworks, such as the Jones calculus and Stokes parameters, used to describe them. We will then explore the physical processes that naturally produce [polarized light](@entry_id:273160), from the glare off a lake to the blue of the sky. Following this, **Applications and Interdisciplinary Connections** will showcase how polarization serves as a powerful tool in fields as varied as [optical engineering](@entry_id:272219), materials science, quantum mechanics, and even cosmology, demonstrating its role in technologies like LCDs and in testing fundamental theories like general relativity. Finally, **Hands-On Practices** will provide an opportunity to apply these concepts to solve practical problems, solidifying your understanding through calculation and analysis.

## Principles and Mechanisms

An electromagnetic wave is characterized by oscillating electric and magnetic fields that are transverse to the direction of propagation. While the propagation direction defines the wave's path, the **polarization** of the wave describes the geometric orientation of the electric field's oscillation in the plane perpendicular to this path. A complete understanding of polarization is essential, as it governs the interaction of light with matter and is the basis for countless optical technologies. In this chapter, we will systematically develop the principles of polarization, from its basic mathematical description to the physical mechanisms that produce and modify it, and finally to the generalized formalisms required to describe any state of light.

### The Geometry of Polarization: From Lines to Ellipses

Let us consider a [monochromatic plane wave](@entry_id:263295) propagating in the positive $z$-direction. Its electric field, which lies in the $xy$-plane, can be expressed as the real part of a complex vector:
$$
\vec{E}(z, t) = \Re\left\{ \vec{E}_0 \exp[i(kz - \omega t)] \right\}
$$
where $\vec{E}_0$ is a complex vector amplitude, $k$ is the [wavenumber](@entry_id:172452), and $\omega$ is the angular frequency. The nature of the polarization is entirely encapsulated in the vector $\vec{E}_0$, which can be decomposed into its components along the $x$ and $y$ axes:
$$
\vec{E}_0 = E_{0x} \hat{x} + E_{0y} \hat{y}
$$
Here, $E_{0x} = |E_{0x}| \exp(i\delta_x)$ and $E_{0y} = |E_{0y}| \exp(i\delta_y)$ are complex numbers representing the amplitudes and initial phases of the electric field components. The key to understanding polarization lies in the relative amplitude, $|E_{0y}|/|E_{0x}|$, and the [relative phase](@entry_id:148120), $\delta = \delta_y - \delta_x$, between these two orthogonal components.

#### Linear Polarization

The simplest case of polarization occurs when the two orthogonal components of the electric field are in phase ($\delta=0$) or exactly out of phase ($\delta=\pi$). In this situation, the tip of the electric field vector at a fixed point in space oscillates back and forth along a straight line in the $xy$-plane. This is known as **linear polarization**.

The direction of this line depends on the relative amplitudes of the $x$ and $y$ components. If $\delta=0$, the components are $E_x(z, t) = |E_{0x}| \cos(kz - \omega t)$ and $E_y(z, t) = |E_{0y}| \cos(kz - \omega t)$. The ratio $E_y/E_x = |E_{0y}|/|E_{0x}|$ is constant, meaning the field vector is always aligned with the vector $|E_{0x}|\hat{x} + |E_{0y}|\hat{y}$.

Consider the superposition of two linearly polarized waves of equal amplitude $E_0$, one polarized along the $x$-axis and the other along the $y$-axis, with a relative phase shift of $\delta = \pi$ [@problem_id:1813453]. The fields are given by:
$$
\vec{E}_1(z, t) = E_0 \cos(kz - \omega t) \hat{x}
$$
$$
\vec{E}_2(z, t) = E_0 \cos(kz - \omega t + \pi) \hat{y} = -E_0 \cos(kz - \omega t) \hat{y}
$$
The resultant field is $\vec{E} = \vec{E}_1 + \vec{E}_2 = E_0 \cos(kz - \omega t) (\hat{x} - \hat{y})$. At any instant, the $y$-component of the field is the negative of the $x$-component ($E_y = -E_x$). This relationship defines a straight line with a slope of $-1$. Therefore, the resultant wave is linearly polarized along the line $y=-x$.

#### Circular Polarization

A more complex and fascinating state arises when the two orthogonal components have **equal amplitudes** ($|E_{0x}| = |E_{0y}| = E_0$) but are in phase quadrature, meaning their relative phase shift is $\delta = \pm \pi/2$. In this case, the tip of the electric field vector traces a perfect circle in the $xy$-plane over one [period of oscillation](@entry_id:271387). This is known as **circular polarization**.

Let's examine the case where the $y$-component leads the $x$-component by $\pi/2$ ($\delta = +\pi/2$). The electric field vector can be written as:
$$
\vec{E}(z, t) = E_0 \cos(kz - \omega t) \hat{x} + E_0 \cos(kz - \omega t + \pi/2) \hat{y}
$$
Using the identity $\cos(\theta + \pi/2) = -\sin(\theta)$, this becomes:
$$
\vec{E}(z, t) = E_0 \cos(kz - \omega t) \hat{x} - E_0 \sin(kz - \omega t) \hat{y}
$$
At a fixed position, say $z=0$, the components are $E_x = E_0 \cos(-\omega t) = E_0 \cos(\omega t)$ and $E_y = -E_0 \sin(-\omega t) = E_0 \sin(\omega t)$. The magnitude of the vector is $|\vec{E}| = \sqrt{E_x^2 + E_y^2} = \sqrt{E_0^2(\cos^2(\omega t) + \sin^2(\omega t))} = E_0$, a constant. As time $t$ increases, the vector tip moves from $(E_0, 0)$ at $t=0$ towards $(0, E_0)$ at $t=\pi/(2\omega)$, tracing a circle in the counter-clockwise direction for an observer looking towards the source (from $+z$). This is defined by convention as **left-circularly polarized (LCP)** light.

Conversely, if the $y$-component lags the $x$-component by $\pi/2$ ($\delta = -\pi/2$), the field is $\vec{E}(z, t) = E_0 \cos(kz - \omega t) \hat{x} + E_0 \sin(kz - \omega t) \hat{y}$ [@problem_id:1838505]. The vector rotates clockwise, which corresponds to **right-circularly polarized (RCP)** light. The direction of rotation, or **handedness**, is a crucial property of [circularly polarized light](@entry_id:198374).

#### Elliptical Polarization

The most general state of polarization is **[elliptical polarization](@entry_id:270497)**. This occurs in any case not covered by linear or circular polarization: either the amplitudes of the orthogonal components are unequal ($|E_{0x}| \neq |E_{0y}|$), or the [relative phase](@entry_id:148120) shift $\delta$ is not an integer multiple of $\pi$. In this state, the tip of the electric field vector traces an ellipse in the $xy$-plane. Linear and circular polarizations are, in fact, special degenerate cases of [elliptical polarization](@entry_id:270497) where the ellipse collapses to a line or becomes a circle, respectively.

Consider an electromagnetic wave described by [@problem_id:1813429]:
$$
\vec{E}(z,t) = E_0 \cos(kz - \omega t) \hat{x} + 2E_0 \cos(kz - \omega t - \frac{\pi}{4}) \hat{y}
$$
Here, the amplitudes are unequal ($|E_{0y}| = 2|E_{0x}|$) and the [phase difference](@entry_id:270122) is $\delta = -\pi/4$. This wave is elliptically polarized. To determine the handedness, we can examine the rotation at a fixed position, say $z=0$. At $t=0$, the field is $\vec{E} = E_0 \hat{x} + 2E_0 \cos(-\pi/4) \hat{y} = E_0 \hat{x} + \sqrt{2} E_0 \hat{y}$, a vector in the first quadrant. To visualize the rotation, let's analyze the velocity of the vector tip at $t=0$ and $z=0$:
$$
\frac{d\vec{E}}{dt} \bigg|_{t=0, z=0} = \left[ \omega E_0 \sin(kz-\omega t) \hat{x} + 2\omega E_0 \sin(kz-\omega t - \pi/4) \hat{y} \right]_{t=0, z=0} = -\sqrt{2}\omega E_0 \hat{y}
$$
The velocity vector at $t=0$ points purely in the $-y$ direction. So from its initial position in the first quadrant, the vector moves towards the $-y$ axis, indicating a clockwise rotation when viewed from $+z$. Thus, the polarization is **right-handed elliptical**.

### The Jones Calculus: A Formalism for Coherent Light

Analyzing polarization by manipulating trigonometric functions can be cumbersome. For fully polarized light, a more elegant and powerful mathematical framework is the **Jones calculus**. This formalism represents the polarization state of light as a two-component complex vector and optical elements as $2 \times 2$ matrices.

A **Jones vector** is a column vector whose elements are the complex amplitudes of the electric field components along the $x$ and $y$ axes.
$$
\mathbf{E} = \begin{pmatrix} E_{0x} \\ E_{0y} \end{pmatrix} = \begin{pmatrix} |E_{0x}| \exp(i\delta_x) \\ |E_{0y}| \exp(i\delta_y) \end{pmatrix}
$$
Some fundamental Jones vectors include:
-   Horizontal Linear Polarization: $|H\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$
-   Vertical Linear Polarization: $|V\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$
-   Linear Polarization at $45^\circ$: $\frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \end{pmatrix}$

We can express circular polarization states as a superposition of horizontal and vertical states with a specific phase relationship [@problem_id:1813457]. For [circular polarization](@entry_id:261702), the amplitudes must be equal. Normalizing the total intensity to unity ($|E_{0x}|^2 + |E_{0y}|^2 = 1$) gives $|E_{0x}| = |E_{0y}| = 1/\sqrt{2}$. The [phase difference](@entry_id:270122) must be $\pm \pi/2$. Setting the phase of the horizontal component to zero for simplicity ($\delta_x=0$), we have $E_{0x} = 1/\sqrt{2}$. The vertical component is then $E_{0y} = \frac{1}{\sqrt{2}} \exp(\pm i\pi/2) = \pm \frac{i}{\sqrt{2}}$.
-   Right-Circular Polarization (RCP), corresponding to a clockwise rotation for an observer looking toward the source, has the $y$-component lagging the $x$-component. This corresponds to the phase $\delta_y - \delta_x = -\pi/2$. The Jones vector is:
    $$
    |RCP\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -i \end{pmatrix}
    $$
-   Left-Circular Polarization (LCP), corresponding to a counter-clockwise rotation, has the $y$-component leading the $x$-component ($\delta_y - \delta_x = +\pi/2$). The Jones vector is:
    $$
    |LCP\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ i \end{pmatrix}
    $$
Optical components that modify the polarization state are represented by $2 \times 2$ **Jones matrices**. If an incident beam with Jones vector $\mathbf{E}_{\text{in}}$ passes through an optical element with Jones matrix $\mathbf{J}$, the emerging beam has a Jones vector $\mathbf{E}_{\text{out}} = \mathbf{J} \mathbf{E}_{\text{in}}$.

A common component is a **[wave plate](@entry_id:163853)** or **retarder**, which introduces a phase shift between the two orthogonal components. A **[quarter-wave plate](@entry_id:262260) (QWP)** introduces a phase shift of $\pi/2$. If its fast axis (the axis along which light travels faster) is aligned with the $y$-axis, it retards the phase of the $x$-component relative to the $y$-component by $\pi/2$. Its Jones matrix, ignoring a [global phase](@entry_id:147947) factor, is:
$$
\mathbf{J}_{\text{QWP, y-fast}} = \begin{pmatrix} \exp(-i\pi/2)  & 0 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} -i & 0 \\ 0 & 1 \end{pmatrix}
$$
More commonly, if the fast axis is along $x$, the $y$-component is retarded, and the matrix is $\mathbf{J}_{\text{QWP, x-fast}} = \begin{pmatrix} 1 & 0 \\ 0 & -i \end{pmatrix}$.

Let's illustrate the power of Jones calculus with an example [@problem_id:1813449]. Suppose a beam, linearly polarized at $30^\circ$ to the $x$-axis, passes through a QWP with its fast axis along the $y$-axis, and then through a [linear polarizer](@entry_id:195509) with its transmission axis at $60^\circ$ to the $x$-axis.
The initial Jones vector is $\mathbf{E}_0 = \begin{pmatrix} \cos(30^\circ) \\ \sin(30^\circ) \end{pmatrix} = \begin{pmatrix} \sqrt{3}/2 \\ 1/2 \end{pmatrix}$.
The QWP in this problem has its fast axis along the y-axis, meaning the x-component is retarded by $\pi/2$. Its matrix is $\begin{pmatrix} -i  & 0 \\ 0 & 1 \end{pmatrix}$. The state after the QWP is:
$$
\mathbf{E}_1 = \begin{pmatrix} -i & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} \sqrt{3}/2 \\ 1/2 \end{pmatrix} = \begin{pmatrix} -i\sqrt{3}/2 \\ 1/2 \end{pmatrix}
$$
This represents right-handed [elliptical polarization](@entry_id:270497). Now, this light passes through a [linear polarizer](@entry_id:195509) at $60^\circ$. A [linear polarizer](@entry_id:195509) projects the incident field onto its transmission axis. The final transmitted electric field amplitude is given by the projection of $\mathbf{E}_1$ onto the unit vector for the polarizer axis, $\hat{u} = \begin{pmatrix} \cos(60^\circ) \\ \sin(60^\circ) \end{pmatrix} = \begin{pmatrix} 1/2 \\ \sqrt{3}/2 \end{pmatrix}$. The [complex amplitude](@entry_id:164138) of the transmitted field is $A_f = \hat{u}^\dagger \mathbf{E}_1$:
$$
A_f = \begin{pmatrix} 1/2 & \sqrt{3}/2 \end{pmatrix} \begin{pmatrix} -i\sqrt{3}/2 \\ 1/2 \end{pmatrix} = -i\frac{\sqrt{3}}{4} + \frac{\sqrt{3}}{4}
$$
The final intensity $I_f$ is proportional to $|A_f|^2$. The initial intensity $I_0$ is proportional to $|\mathbf{E}_0|^2 = (\sqrt{3}/2)^2 + (1/2)^2 = 1$. The ratio of intensities is:
$$
\frac{I_f}{I_0} = |A_f|^2 = \left|-\frac{i\sqrt{3}}{4} + \frac{\sqrt{3}}{4}\right|^2 = \left(\frac{\sqrt{3}}{4}\right)^2 + \left(-\frac{\sqrt{3}}{4}\right)^2 = \frac{3}{16} + \frac{3}{16} = \frac{6}{16} = \frac{3}{8} = 0.375
$$
This step-by-step matrix multiplication provides a systematic way to track the evolution of a polarization state through a series of optical elements.

### Physical Mechanisms for Producing Polarized Light

While we can manipulate polarization with engineered devices, [polarized light](@entry_id:273160) is also commonly produced by fundamental physical processes. Understanding these mechanisms is key to both explaining natural phenomena and designing polarization-based instruments.

#### Polarization by Reflection: Brewster's Angle

When [unpolarized light](@entry_id:176162) is incident on the interface between two dielectric media, such as air and water or, in a more specialized case, seawater and sapphire [@problem_id:1813441], the reflected and transmitted light are generally partially polarized. This is because the [reflection coefficients](@entry_id:194350) for light polarized parallel to the plane of incidence ($p$-polarization) and perpendicular to it ($s$-polarization) are different.

There exists a special angle of incidence, known as **Brewster's angle** ($\theta_B$), at which the [reflection coefficient](@entry_id:141473) for $p$-polarized light is zero. Consequently, if [unpolarized light](@entry_id:176162) is incident at this angle, the reflected light is perfectly linearly polarized, with its electric field oscillating perpendicular to the plane of incidence ($s$-polarized). This phenomenon occurs when the reflected ray and the refracted (transmitted) ray are perpendicular to each other. By combining this condition ($\theta_B + \theta_t = \pi/2$) with Snell's Law ($n_1 \sin\theta_B = n_2 \sin\theta_t$), we arrive at Brewster's law:
$$
\tan \theta_B = \frac{n_2}{n_1}
$$
where $n_1$ is the refractive index of the incident medium and $n_2$ is the refractive index of the transmitting medium. For an underwater window made of sapphire ($n_2=1.768$) submerged in seawater ($n_1=1.341$), the angle for producing perfectly polarized reflected light is:
$$
\theta_B = \arctan\left(\frac{1.768}{1.341}\right) \approx \arctan(1.318) \approx 52.8^\circ
$$
This principle is exploited in polarizing sunglasses to reduce glare from horizontal surfaces like water or roads.

#### Polarization by Scattering: Rayleigh Scattering

The blue color of the sky is a result of sunlight scattering off atmospheric molecules. This process, known as **Rayleigh scattering**, occurs when light interacts with particles much smaller than its wavelength. Rayleigh scattering is also a potent source of polarization.

Imagine unpolarized sunlight traveling along the $x$-axis and scattering from a molecule at the origin. The electric field of the incident light oscillates in the $yz$-plane. These oscillations induce a dipole moment in the molecule, which also oscillates in the $yz$-plane. This oscillating dipole then re-radiates light in all directions. However, an [oscillating dipole](@entry_id:262983) does not radiate along its axis of oscillation. For an observer looking at the scattered light along the $y$-axis (a [scattering angle](@entry_id:171822) of $\theta=90^\circ$), they will only see radiation from the dipole's $z$-component of oscillation, as the $y$-component of oscillation points directly at them. The resulting scattered light is therefore perfectly linearly polarized along the $z$-axis.

For a general scattering angle $\theta$, the scattered light is partially linearly polarized. The **[degree of polarization](@entry_id:276690)** ($p$), a measure of how polarized the light is, for Rayleigh scattering of initially unpolarized light is given by:
$$
p = \frac{\sin^2\theta}{1+\cos^2\theta}
$$
This formula shows that polarization is zero for forward ($\theta=0$) and backward ($\theta=\pi$) scattering and is maximal ($p=1$) for scattering at $\theta = 90^\circ$. This is why the sky appears most strongly polarized when viewed at a right angle to the sun. In an astrophysical context, measuring the polarization of light scattered from an exoplanet's atmosphere can reveal information about the scattering process. For instance, if a probe measures the scattered light and finds a ratio of maximum to minimum intensity (as a [polarizer](@entry_id:174367) is rotated) of $I_{max}/I_{min} = 4.50$, we can deduce the [scattering angle](@entry_id:171822) [@problem_id:1813464]. The measured intensity ratio is related to the [degree of polarization](@entry_id:276690) by $I_{max}/I_{min} = (1+p)/(1-p)$. Solving for $p$ gives $p = (4.50-1)/(4.50+1) = 7/11$. We can then solve for the [scattering angle](@entry_id:171822):
$$
\frac{7}{11} = \frac{\sin^2\theta}{1+\cos^2\theta} = \frac{1-\cos^2\theta}{1+\cos^2\theta} \implies \cos^2\theta = \frac{1-7/11}{1+7/11} = \frac{4/11}{18/11} = \frac{2}{9}
$$
For an angle between $0^\circ$ and $90^\circ$, this gives $\theta = \arccos(\sqrt{2}/3) \approx 61.9^\circ$.

#### Polarization by Anisotropic Absorption: Dichroism

**Dichroism** is the property of certain materials to absorb light differently depending on its polarization. A material exhibiting [linear dichroism](@entry_id:182146) has a preferred axis; light polarized parallel to this axis is absorbed more strongly than light polarized perpendicular to it. This is the working principle of modern sheet [polarizers](@entry_id:269119).

Consider a dichroic material with an "easy" transmission axis (e.g., along $x$) and a "hard" transmission axis (e.g., along $y$). The amplitude [transmission coefficients](@entry_id:756126) are $\tau_x$ and $\tau_y$, with $\tau_x > \tau_y$ [@problem_id:1813465]. In the Jones formalism, this material is represented by the matrix:
$$
\mathbf{T} = \begin{pmatrix} \tau_x  & 0 \\ 0 & \tau_y \end{pmatrix}
$$
If [circularly polarized light](@entry_id:198374), represented by the Jones vector $\mathbf{E}_{\text{in}} = \frac{E_0}{\sqrt{2}} \begin{pmatrix} 1 \\ i \end{pmatrix}$, is incident on this material, the transmitted field will be:
$$
\mathbf{E}_{\text{out}} = \mathbf{T} \mathbf{E}_{\text{in}} = \frac{E_0}{\sqrt{2}} \begin{pmatrix} \tau_x \\ i\tau_y \end{pmatrix}
$$
The transmitted wave has components $E_x(t) \propto \tau_x \cos(\omega t)$ and $E_y(t) \propto \tau_y \sin(\omega t)$. Since the amplitudes are now unequal, the polarization has been transformed from circular to elliptical. The semi-axes of the polarization ellipse are aligned with the material's axes, and their lengths are proportional to $\tau_x$ and $\tau_y$. If $\tau_x = 0.96$ and $\tau_y = 0.60$, the ratio of the [semi-major axis](@entry_id:164167) to the semi-minor axis is simply the ratio of the [transmission coefficients](@entry_id:756126):
$$
\frac{\text{semi-major axis}}{\text{semi-minor axis}} = \frac{\max(\tau_x, \tau_y)}{\min(\tau_x, \tau_y)} = \frac{0.96}{0.60} = 1.6
$$

### Describing Partially Polarized Light: Stokes Parameters

The Jones calculus is a powerful tool, but it is fundamentally limited to describing **fully polarized** (coherent) light. Natural light sources, like the sun or an incandescent bulb, emit light that is a random, incoherent superposition of many different [polarization states](@entry_id:175130). Such light can be **unpolarized** or, more generally, **partially polarized**. To handle these cases, a more robust statistical description is needed. This is provided by the **Stokes parameters**.

The four real Stokes parameters, typically written as a vector $S = (S_0, S_1, S_2, S_3)$, provide a complete description of the polarization state of any beam of light. They are defined in terms of time-averaged correlations of the electric field components:
-   $S_0 = \langle E_x E_x^* \rangle + \langle E_y E_y^* \rangle$ (Total intensity)
-   $S_1 = \langle E_x E_x^* \rangle - \langle E_y E_y^* \rangle$ (Excess of horizontal over vertical polarization)
-   $S_2 = \langle E_x E_y^* \rangle + \langle E_y E_x^* \rangle$ (Excess of $+45^\circ$ over $-45^\circ$ polarization)
-   $S_3 = i(\langle E_y E_x^* \rangle - \langle E_x E_y^* \rangle)$ (Excess of right-circular over left-[circular polarization](@entry_id:261702))

The great utility of Stokes parameters is that they are directly related to measurable intensities. By passing an unknown beam through a series of [polarizers](@entry_id:269119) and [wave plates](@entry_id:275054), one can determine its Stokes vector. For instance, consider a set of four intensity measurements [@problem_id:576229]:
1.  $I_H$: Intensity through a horizontal [polarizer](@entry_id:174367) ($\theta=0^\circ$).
2.  $I_V$: Intensity through a vertical polarizer ($\theta=90^\circ$).
3.  $I_D$: Intensity through a $+45^\circ$ [polarizer](@entry_id:174367).
4.  $I_{RC}$: Intensity through a QWP (fast axis horizontal) followed by a $+45^\circ$ [polarizer](@entry_id:174367).

From these measurements, the Stokes parameters can be found:
$$
S_0 = I_H + I_V
$$
$$
S_1 = I_H - I_V
$$
$$
S_2 = 2I_D - (I_H + I_V)
$$
$$
S_3 = 2I_{RC} - (I_H + I_V)
$$
The **[degree of polarization](@entry_id:276690)** ($P$) is a scalar quantity that quantifies the fraction of the light's intensity that is in a polarized state. It is defined as:
$$
P = \frac{\sqrt{S_1^2 + S_2^2 + S_3^2}}{S_0}
$$
For fully polarized light, $S_0^2 = S_1^2 + S_2^2 + S_3^2$ and $P=1$. For unpolarized light, $S_1=S_2=S_3=0$ and $P=0$. For [partially polarized light](@entry_id:267467), $0  P  1$. Using the measurable intensities, the [degree of polarization](@entry_id:276690) can be expressed directly as [@problem_id:576229]:
$$
P = \frac{\sqrt{(I_H-I_V)^2 + (2I_D-I_H-I_V)^2 + (2I_{RC}-I_H-I_V)^2}}{I_H+I_V}
$$

An alternative but equivalent formalism for describing [partially polarized light](@entry_id:267467) is the $2 \times 2$ **[coherency matrix](@entry_id:192731)**, $\mathbf{J}$, also known as the polarization matrix. Its elements are the same time-averaged correlations that define the Stokes parameters:
$$
\mathbf{J} = \begin{pmatrix} \langle E_x E_x^* \rangle  \langle E_x E_y^* \rangle \\ \langle E_y E_x^* \rangle  \langle E_y E_y^* \rangle \end{pmatrix} = \begin{pmatrix} J_{xx}  J_{xy} \\ J_{yx}  J_{yy} \end{pmatrix}
$$
The [coherency matrix](@entry_id:192731) and Stokes parameters are linearly related. One can express the elements of $\mathbf{J}$ in terms of the Stokes parameters as [@problem_id:576155]:
$$
J_{xx} = \frac{1}{2}(S_0+S_1) \qquad J_{yy} = \frac{1}{2}(S_0-S_1)
$$
$$
J_{xy} = \frac{1}{2}(S_2 + iS_3) \qquad J_{yx} = \frac{1}{2}(S_2 - iS_3)
$$
A powerful connection between these formalisms is revealed by calculating the determinant of the [coherency matrix](@entry_id:192731):
$$
\det(\mathbf{J}) = J_{xx}J_{yy} - J_{xy}J_{yx} = \frac{1}{4}(S_0+S_1)(S_0-S_1) - \frac{1}{4}(S_2+iS_3)(S_2-iS_3)
$$
$$
\det(\mathbf{J}) = \frac{1}{4}(S_0^2 - S_1^2) - \frac{1}{4}(S_2^2 + S_3^2) = \frac{1}{4}(S_0^2 - S_1^2 - S_2^2 - S_3^2)
$$
This elegant result can be rewritten using the [degree of polarization](@entry_id:276690), $P^2 = (S_1^2+S_2^2+S_3^2)/S_0^2$:
$$
\det(\mathbf{J}) = \frac{S_0^2}{4}(1 - P^2)
$$
This relation shows that for fully polarized light ($P=1$), the determinant of the [coherency matrix](@entry_id:192731) is zero, indicating that the system is not random but deterministic. For unpolarized light ($P=0$), the determinant is maximal for a given intensity, reflecting the maximum possible randomness in the field components. This connection underscores the deep structural unity between the different mathematical frameworks developed to describe the rich and varied phenomenon of polarization.