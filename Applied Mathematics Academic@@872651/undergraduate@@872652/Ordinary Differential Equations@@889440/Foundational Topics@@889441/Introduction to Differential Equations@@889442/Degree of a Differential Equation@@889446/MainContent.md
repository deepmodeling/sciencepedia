## Introduction
In the study of [ordinary differential equations](@entry_id:147024) (ODEs), classification is the first step toward understanding and solving them. While the order—the highest derivative present—is straightforward to identify, the **degree** offers a more nuanced look into an equation's algebraic structure. The degree is defined as the power of the highest-order derivative, but this simple definition hides a critical precondition: the equation must first be expressed as a polynomial in its derivatives. This requirement often leads to confusion, as it necessitates algebraic manipulations like clearing radicals and simplifying complex expressions.

This article provides a comprehensive guide to mastering the concept of degree. In "Principles and Mechanisms," you will learn the formal procedure for determining the degree, including the crucial steps of rationalization and simplification. "Applications and Interdisciplinary Connections" will explore the practical significance of the degree, demonstrating how it arises naturally from geometric properties and physical models, often indicating underlying nonlinearity. Finally, "Hands-On Practices" will allow you to solidify your understanding by working through targeted problems. By starting with the fundamental rules, we can build a robust framework for classifying any differential equation we encounter.

## Principles and Mechanisms

In the classification of [ordinary differential equations](@entry_id:147024) (ODEs), two primary characteristics are of immediate importance: the **order** and the **degree**. The order, as previously discussed, refers to the highest-order derivative present in the equation. The degree, however, is a more subtle concept that describes the algebraic structure of the equation with respect to its derivatives. A precise understanding of the degree is essential for classifying equations and, in some contexts, for choosing appropriate solution methods.

### The Fundamental Precondition: Polynomial Form in Derivatives

The **degree** of an ordinary differential equation is defined as the highest power of the highest-order derivative that appears in the equation, but this definition is valid **only after** the equation has been expressed as a polynomial in all of its derivative terms ($y', y'', y''', \dots, y^{(n)}$). This is a critical precondition. The equation must be algebraically cleared of any radicals (e.g., square roots, cube roots) or fractional exponents that involve the derivative terms.

Let's formalize this. An ODE can be written in the general form $F(x, y, y', y'', \dots, y^{(n)}) = 0$. For the degree to be defined, the function $F$ must be a polynomial in the variables $y', y'', \dots, y^{(n)}$. The coefficients of this polynomial can be functions of $x$ and $y$. For instance, the equation given by:
$$ \left( \frac{d^3y}{dx^3} \right)^2 + 7 \left( \frac{d^2y}{dx^2} \right)^5 + y \frac{dy}{dx} = \exp(y) + \sin(x) $$
is already a polynomial in its derivatives. The terms $\exp(y)$ and $\sin(x)$ do not invalidate this condition, as they are functions of the dependent and independent variables, not the derivatives. They simply form part of the overall equation. The highest-order derivative is $\frac{d^3y}{dx^3}$, and its highest power is $2$. Therefore, the degree of this equation is $2$.

Similarly, consider a hypothetical model for a subatomic particle's path:
$$ \left(1 + \left(\frac{dy}{dx}\right)^2\right)^3 = k \left(\frac{d^2y}{dx^2} \right)^2 $$
This equation is also in polynomial form with respect to the derivatives $y'$ and $y''$. The highest-order derivative is $\frac{d^2y}{dx^2}$, and its power is $2$. Hence, the degree is $2$.

### The Process of Rationalization: Achieving Polynomial Form

Many differential equations do not initially appear in the required polynomial form. They may contain radicals or fractional powers of the derivatives. In such cases, we must perform an algebraic manipulation called **rationalization** to eliminate these features before we can determine the degree.

#### Clearing a Single Fractional Power

The simplest case involves an equation with a single derivative term raised to a fractional power. To rationalize the equation, we raise both sides to the smallest integer power that will clear the fraction.

For example, consider the equation:
$$ \left( \frac{d^2y}{dx^2} \right)^{3/2} = x + \frac{dy}{dx} $$
The highest-order derivative, $y''$, is raised to the fractional power $\frac{3}{2}$. To eliminate this, we square both sides of the equation:
$$ \left[ \left( \frac{d^2y}{dx^2} \right)^{3/2} \right]^2 = \left( x + \frac{dy}{dx} \right)^2 $$
This simplifies to:
$$ \left( \frac{d^2y}{dx^2} \right)^3 = \left( x + \frac{dy}{dx} \right)^2 $$
The equation is now a polynomial in the derivatives $y'$ and $y''$. The highest-order derivative is $\frac{d^2y}{dx^2}$, and its power is $3$. Thus, the degree of the differential equation is $3$.

#### Clearing Multiple Fractional Powers

When an equation involves multiple derivative terms with different fractional exponents, we must find a single operation that clears all of them simultaneously. This is achieved by raising both sides of the equation to the **[least common multiple](@entry_id:140942) (LCM)** of the denominators of the fractional exponents.

Consider a system described by the following relation:
$$ \left(\frac{d^3y}{dx^3}\right)^{1/2} = \left(\frac{dy}{dx}\right)^{1/3} $$
Here, we have powers of $\frac{1}{2}$ and $\frac{1}{3}$. The denominators are $2$ and $3$. The LCM of $2$ and $3$ is $6$. Raising both sides to the 6th power yields:
$$ \left[ \left(\frac{d^3y}{dx^3}\right)^{1/2} \right]^6 = \left[ \left(\frac{dy}{dx}\right)^{1/3} \right]^6 $$
Applying the exponent rule $(a^m)^n = a^{mn}$, we get:
$$ \left(\frac{d^3y}{dx^3}\right)^3 = \left(\frac{dy}{dx}\right)^2 $$
The equation is now in the required polynomial form. The highest-order derivative is $\frac{d^3y}{dx^3}$, and its power is $3$. Therefore, the degree of the equation is $3$.

A similar logic applies to a hypothetical complex system governed by the equation:
$$ \left( \left( y^{(4)} \right)^{7} + \sin(x) \left( y^{(3)} \right)^{3} - \left( y' \right)^{5} \right)^{1/3} = y'' $$
To clear the cube root (the power of $\frac{1}{3}$), we raise both sides to the power of $3$:
$$ \left( y^{(4)} \right)^{7} + \sin(x) \left( y^{(3)} \right)^{3} - \left( y' \right)^{5} = \left( y'' \right)^{3} $$
The highest-order derivative is $y^{(4)}$, and its power is $7$. The degree is therefore $7$.

### Expansion, Simplification, and Hidden Degrees

After rationalization, it is imperative to expand and simplify the entire equation before making a final determination of the degree. The apparent degree before full simplification can be misleading.

#### Expansion Revealing a Higher Degree

Consider this equation:
$$ \left( \frac{d^3y}{dx^3} \right)^2 + x^2 \left( \frac{dy}{dx} \right)^5 = \sqrt{1 + \left( \frac{d^2y}{dx^2} \right)^6} $$
First, we square both sides to eliminate the square root:
$$ \left[ \left(\frac{d^3y}{dx^3}\right)^{2}+x^{2}\left(\frac{dy}{dx}\right)^{5} \right]^{2} = 1+\left(\frac{d^{2}y}{dx^{2}}\right)^{6} $$
We must now expand the left side. The term of interest is the one containing the highest-order derivative, $\frac{d^3y}{dx^3}$. Using the [binomial expansion](@entry_id:269603) $(a+b)^2 = a^2 + 2ab + b^2$, where $a = (y''')^2$, the first term of the expansion is $((y''')^2)^2 = (y''')^4$. The full expansion is:
$$ \left(\frac{d^3y}{dx^3}\right)^{4} + 2x^2 \left(\frac{d^3y}{dx^3}\right)^2 \left(\frac{dy}{dx}\right)^5 + x^4 \left(\frac{dy}{dx}\right)^{10} = 1+\left(\frac{d^{2}y}{dx^{2}}\right)^{6} $$
The highest-order derivative is $y'''$, and its highest power in the fully expanded polynomial form is $4$. Thus, the degree is $4$, not $2$ as one might have mistakenly concluded before expansion.

#### Simplification Revealing a Lower Degree

Conversely, simplification can reveal that the apparent highest-power terms cancel out, leading to a lower degree than initially perceived. Let's analyze the following equation:
$$ (y'')^2 + y'' \sin(x) + (y')^3 = \left(y'' + \frac{\sin(x)}{2}\right)^2 + y' $$
At first glance, this equation appears to be of degree $2$, due to the $(y'')^2$ term on the left side. However, let's expand the right side:
$$ (y'')^2 + y'' \sin(x) + (y')^3 = (y'')^2 + 2(y'')\left(\frac{\sin(x)}{2}\right) + \left(\frac{\sin(x)}{2}\right)^2 + y' $$
$$ (y'')^2 + y'' \sin(x) + (y')^3 = (y'')^2 + y''\sin(x) + \frac{\sin^2(x)}{4} + y' $$
By subtracting the common terms $(y'')^2$ and $y''\sin(x)$ from both sides, the equation simplifies dramatically:
$$ (y')^3 = \frac{\sin^2(x)}{4} + y' $$
Rearranging into standard form gives:
$$ (y')^3 - y' - \frac{\sin^2(x)}{4} = 0 $$
After simplification, the highest-order derivative is now $y'$, and its highest power is $3$. Therefore, the actual degree of this equation is $3$. This example powerfully illustrates the necessity of algebraic simplification before determining the degree.

### When the Degree is Not Defined

The concept of degree is predicated on the ability to write the ODE as a polynomial in its derivatives. If this cannot be achieved through any algebraic manipulation, the degree is **not defined**.

This situation typically arises when a derivative appears as the argument of a **non-polynomial function**, such as a [transcendental function](@entry_id:271750) (e.g., trigonometric, exponential, logarithmic) or an [absolute value function](@entry_id:160606).

Consider the equation:
$$ \exp\left(\frac{d^3y}{dx^3}\right) - x \frac{dy}{dx} + y^2 = \sin(x) $$
Here, the highest-order derivative, $y'''$, is inside an [exponential function](@entry_id:161417). There is no algebraic way to isolate $y'''$ and its powers to form a polynomial. If we try to take the natural logarithm, we get $\frac{d^3y}{dx^3} = \ln\left( \sin(x) + x \frac{dy}{dx} - y^2 \right)$, which now involves a logarithm of a derivative. The equation cannot be expressed as a polynomial in its derivatives, so its degree is not defined.

The same principle applies to other non-polynomial functions. For the equations:
$$ y' + \cos(y'') = x $$
$$ x^2 \frac{d^2y}{dx^2} + \left|\frac{dy}{dx}\right| = 0 $$
In the first case, the second derivative $y''$ is the argument of the cosine function. In the second, the first derivative $y'$ is inside an absolute value function. Since both $\cos(z)$ and $|z|$ are not polynomial functions of $z$, the degree for both of these differential equations is not defined.

In summary, the degree provides a more refined classification of a differential equation beyond its order. Its determination requires a strict, systematic procedure: first, rationalize and simplify the equation into a polynomial in its derivatives, and only then identify the highest power of the highest-order derivative. If the equation cannot be written in this polynomial form, the degree is undefined.