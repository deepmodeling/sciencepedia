## Introduction
In the study of [control systems](@entry_id:155291), achieving a desired output with minimal error is a primary objective. Steady-state error, the residual difference between the desired and actual output after all transients have settled, is a key metric of system performance. While introductory analyses often rely on the idealized [unity feedback](@entry_id:274594) model, real-world systems almost invariably employ sensors that have their own dynamic characteristics and gains. This reality necessitates the study of [non-unity feedback](@entry_id:274431) systems, where a failure to properly account for [sensor dynamics](@entry_id:263688) can lead to significant miscalculations and flawed designs. This article addresses this critical knowledge gap by providing a rigorous framework for understanding and analyzing steady-state error in these practical configurations. The following chapters will guide you from core theory to real-world application. "Principles and Mechanisms" will dissect the fundamental concepts, distinguishing between actuating and tracking error and introducing methods for their calculation. "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied in fields like chemical engineering, robotics, and aerospace. Finally, "Hands-On Practices" will provide guided problems to solidify your understanding and build practical design skills.

## Principles and Mechanisms

In the analysis of [feedback control systems](@entry_id:274717), the [unity feedback](@entry_id:274594) model, where the output is directly compared with the reference signal, serves as a foundational and convenient idealization. However, in most physical implementations, the sensor that measures the output variable possesses its own dynamic characteristics. This reality gives rise to the [non-unity feedback](@entry_id:274431) configuration, where the feedback signal is a dynamically modified version of the system output. This distinction is not merely a structural detail; it fundamentally alters the interpretation and calculation of [steady-state error](@entry_id:271143), a critical performance metric. This chapter will dissect the principles governing [steady-state error](@entry_id:271143) in [non-unity feedback](@entry_id:274431) systems, clarifying key definitions and providing systematic methods for analysis.

### The Duality of Error: Actuating Signal versus Tracking Error

The primary point of departure from [unity feedback](@entry_id:274594) analysis is the recognition that two distinct error signals exist within the loop. Consider a standard non-unity negative feedback system with a reference input $R(s)$, a [forward path](@entry_id:275478) transfer function $G(s)$, an output $Y(s)$, and a feedback path transfer function $H(s)$.

The first, and most immediate, error signal is the one generated at the [summing junction](@entry_id:264605). This signal, often called the **actuating signal** or **[actuating error](@entry_id:272192)**, is what literally drives the [forward path](@entry_id:275478) (the controller and plant). It is defined as:

$E_a(s) = R(s) - B(s)$

where $B(s) = H(s)Y(s)$ is the signal produced by the sensor. The controller's "view" of the error is entirely based on this signal, $E_a(s)$.

The second, and often more physically significant, [error signal](@entry_id:271594) is the **[tracking error](@entry_id:273267)**. This signal represents the true discrepancy between the desired state and the actual state of the system's output. It is defined as:

$E(s) = R(s) - Y(s)$

In a unity feedback system, $H(s) = 1$, and these two error signals become identical. In a [non-unity feedback](@entry_id:274431) system, they are different, and this difference is the source of many important behaviors and potential design pitfalls. For instance, in a robotic arm position control system, the [actuating error](@entry_id:272192) $E_a(s)$ is the difference between the desired angle command and the voltage from the position sensor, while the tracking error $E(s)$ is the actual difference in angle between the command and the arm's physical position [@problem_id:1616028]. Confusing these two signals can lead to incorrect conclusions about system performance.

### Direct Analysis of Steady-State Error

The steady-state value of any [error signal](@entry_id:271594), provided the closed-loop system is stable, can be determined using the Final Value Theorem: $e_{ss} = \lim_{t \to \infty} e(t) = \lim_{s \to 0} sE(s)$. To apply this, we must first derive the closed-loop [transfer functions](@entry_id:756102) for our error signals of interest.

The relationship between the output and the [actuating error](@entry_id:272192) is $Y(s) = G(s)E_a(s)$. Substituting this into the definition of $E_a(s)$ yields:

$E_a(s) = R(s) - H(s)Y(s) = R(s) - H(s)G(s)E_a(s)$

Solving for $E_a(s)$ gives the transfer function from the reference to the [actuating error](@entry_id:272192):

$\frac{E_a(s)}{R(s)} = \frac{1}{1 + G(s)H(s)}$

The product $L(s) = G(s)H(s)$ is known as the **loop gain**, and it plays a central role in the analysis of stability and performance. The steady-state [actuating error](@entry_id:272192), $e_{a,ss}$, is therefore:

$e_{a,ss} = \lim_{s \to 0} s \frac{R(s)}{1 + G(s)H(s)}$

Let us apply this to a simplified temperature control system for a [chemical reactor](@entry_id:204463), where the [forward path](@entry_id:275478) is $G(s) = G_c(s)G_p(s) = \frac{K_p K_{th}}{\tau s + 1}$ and the sensor is a simple gain, $H(s) = K_{sens}$ [@problem_id:1616023]. For a step input of magnitude $T_{set}$, $R(s) = T_{set}/s$. The steady-state [actuating error](@entry_id:272192) is:

$e_{a,ss} = \lim_{s \to 0} s \left( \frac{T_{set}}{s} \cdot \frac{1}{1 + \frac{K_p K_{th}}{\tau s + 1} K_{sens}} \right) = T_{set} \cdot \frac{1}{1 + G(0)H(0)} = \frac{T_{set}}{1 + K_p K_{th} K_{sens}}$

This result is a finite, non-zero error, which is expected for a Type 0 system (determined by the loop gain $G(s)H(s)$) responding to a step input.

Now, let us derive the transfer function for the [tracking error](@entry_id:273267), $E(s) = R(s) - Y(s)$. The overall closed-[loop transfer function](@entry_id:274447) is $\frac{Y(s)}{R(s)} = \frac{G(s)}{1 + G(s)H(s)}$. Therefore:

$E(s) = R(s) - \frac{G(s)}{1 + G(s)H(s)} R(s) = \left( 1 - \frac{G(s)}{1 + G(s)H(s)} \right) R(s)$

This simplifies to:

$\frac{E(s)}{R(s)} = \frac{1 + G(s)H(s) - G(s)}{1 + G(s)H(s)}$

The expression for the tracking error is visibly more complex than that for the [actuating error](@entry_id:272192). This complexity underscores the importance of specifying precisely which error is being analyzed.

### The Critical Role of Sensor DC Gain

The disparity between the [actuating error](@entry_id:272192) and the [tracking error](@entry_id:273267) reveals a crucial principle: perfect tracking is not guaranteed even if the [actuating error](@entry_id:272192) is driven to zero. This depends critically on the **DC gain of the feedback element**, $H(0) = \lim_{s \to 0} H(s)$.

Consider a system where the controller, through integral action in the [forward path](@entry_id:275478) $G(s)$, successfully eliminates the steady-state [actuating error](@entry_id:272192) for a step input, i.e., $e_{a,ss} = 0$. This implies:

$\lim_{t \to \infty} (r(t) - b(t)) = 0 \implies r_{ss} = b_{ss}$

where $r_{ss}$ is the steady-state value of the reference and $b_{ss}$ is the steady-state value of the feedback signal. From the definition of the feedback signal, we have $b_{ss} = \lim_{s \to 0} s H(s) Y(s) = H(0) y_{ss}$. Therefore, the condition $e_{a,ss} = 0$ forces the relationship:

$r_{ss} = H(0) y_{ss}$

This leads to a profound conclusion. The steady-state output is:

$y_{ss} = \frac{r_{ss}}{H(0)}$

The steady-state [tracking error](@entry_id:273267) is then:

$e_{ss} = r_{ss} - y_{ss} = r_{ss} - \frac{r_{ss}}{H(0)} = r_{ss} \left( 1 - \frac{1}{H(0)} \right)$

This equation demonstrates that for a system to achieve zero steady-state tracking error ($e_{ss}=0$) for a constant reference input, it is a necessary condition that the DC gain of the feedback element be exactly one ($H(0) = 1$). If the sensor has a gain other than unity (e.g., due to calibration or physical units conversion), there will be an inherent [tracking error](@entry_id:273267), even if the controller perfectly nullifies the [actuating error](@entry_id:272192).

For example, in a robotic arm control system with a Type 1 [forward path](@entry_id:275478) $G(s) = \frac{K}{s(s+p)}$ and a dynamic sensor $H(s) = \frac{\alpha}{s+\beta}$, the integrator in $G(s)$ ensures the [actuating error](@entry_id:272192) for a step input $\theta_0$ is zero [@problem_id:1616028]. Here, $H(0) = \alpha/\beta$. The steady-state output is $y_{ss} = \theta_0 / H(0) = \theta_0 (\beta/\alpha)$. The steady-state tracking error is thus $e_{ss} = \theta_0(1 - \beta/\alpha)$, which is only zero if $\alpha = \beta$.

Similarly, for a pH bioreactor with $G(s) = \frac{K}{s+a}$ and $H(s) = \frac{K_h}{s+b}$, the steady-state output for a step input $R_0$ is not simply $R_0$ minus some error term [@problem_id:1616043]. Using the Final Value Theorem on the closed-[loop transfer function](@entry_id:274447) $Y(s)/R(s)$, we find:

$y_{ss} = \lim_{s \to 0} s \left( \frac{G(s)}{1+G(s)H(s)} \frac{R_0}{s} \right) = R_0 \frac{G(0)}{1+G(0)H(0)} = R_0 \frac{K/a}{1 + (K/a)(K_h/b)} = R_0 \frac{Kb}{ab + KK_h}$

This confirms that the final output value depends intrinsically on the parameters of both the forward and feedback paths.

### Analysis via an Equivalent Unity Feedback System

While direct calculation is always possible, it is often insightful to transform a [non-unity feedback](@entry_id:274431) system into an equivalent [unity feedback](@entry_id:274594) structure. This allows the well-established framework of system types and [static error constants](@entry_id:265095) to be applied, provided it is done carefully. The goal is to find an equivalent [forward path](@entry_id:275478), $G_{eq}(s)$, such that a unity [feedback system](@entry_id:262081) with this path has the same closed-[loop transfer function](@entry_id:274447), $Y(s)/R(s)$, as the original system.

The original closed-[loop transfer function](@entry_id:274447) is $T(s) = \frac{G(s)}{1 + G(s)H(s)}$.
The [unity feedback](@entry_id:274594) closed-[loop transfer function](@entry_id:274447) is $T(s) = \frac{G_{eq}(s)}{1 + G_{eq}(s)}$.

Equating these and solving for $G_{eq}(s)$ gives [@problem_id:1616006]:

$G_{eq}(s) = \frac{G(s)}{1 + G(s)H(s) - G(s)} = \frac{G(s)}{1 + G(s)(H(s)-1)}$

This equivalent system is constructed such that its error signal, at the new [summing junction](@entry_id:264605), is precisely the tracking error $E(s) = R(s) - Y(s)$ of the original system. With this transformation, we can analyze the [tracking error](@entry_id:273267) of the non-unity system by analyzing the summing-junction error of the [equivalent unity feedback system](@entry_id:267954).

### System Type and Static Error Constants in Non-Unity Feedback

The concept of **[system type](@entry_id:269068)**—the number of pure integrators in the [open-loop transfer function](@entry_id:276280)—is the cornerstone of steady-state error analysis in unity feedback systems. It determines whether the [steady-state error](@entry_id:271143) for a given input (step, ramp, parabola) is zero, finite, or infinite.

For [non-unity feedback](@entry_id:274431) systems, this can be ambiguous. Which "[open-loop transfer function](@entry_id:276280)" should be used? The answer depends on which error signal is of interest.

1.  **Analysis based on Actuating Error ($E_a(s)$):** The steady-state properties of the [actuating error](@entry_id:272192) are determined by the loop gain, $L(s) = G(s)H(s)$. Therefore, the [system type](@entry_id:269068) and the conventional [static error constants](@entry_id:265095) ($K_p, K_v, K_a$) are defined from this loop gain [@problem_id:1616032]:
    *   Position Error Constant: $K_p = \lim_{s \to 0} G(s)H(s)$
    *   Velocity Error Constant: $K_v = \lim_{s \to 0} s G(s)H(s)$
    *   Acceleration Error Constant: $K_a = \lim_{s \to 0} s^2 G(s)H(s)$

    These constants are then used with the standard formulas to find the steady-state *actuating* error (e.g., $e_{a,ss} = \frac{1}{1+K_p}$ for a unit step input).

2.  **Analysis based on Tracking Error ($E(s)$):** To analyze the [tracking error](@entry_id:273267) using the [system type](@entry_id:269068) methodology, one must use the [equivalent transfer function](@entry_id:276656), $G_{eq}(s)$. The [system type](@entry_id:269068) is the number of integrators in $G_{eq}(s)$, and the [static error constants](@entry_id:265095) are defined from it ($K_{p,eq} = \lim_{s \to 0} G_{eq}(s)$, etc.). This allows for a direct calculation of the steady-state [tracking error](@entry_id:273267).

The observation that a stable satellite control system exhibits a finite, non-[zero steady-state error](@entry_id:269428) for a parabolic input tells us directly about its equivalent [system type](@entry_id:269068). For a parabolic input, a finite, non-zero error is the signature of a Type 2 system. Therefore, the equivalent [unity feedback](@entry_id:274594) representation of that system must be Type 2 [@problem_id:1616059].

A crucial point is that the type of $G_{eq}(s)$ can be very different from the types of $G(s)$ or $H(s)$. For instance, consider a system with $G(s) = \frac{K}{s^2+as+b}$ (Type 0) and $H(s) = \frac{1}{s}$ (Type 1) [@problem_id:1616044]. The [equivalent transfer function](@entry_id:276656) is:

$G_{eq}(s) = \frac{G(s)}{1+G(s)(H(s)-1)} = \frac{\frac{K}{s^2+as+b}}{1 + \frac{K}{s^2+as+b}(\frac{1}{s}-1)} = \frac{Ks}{s(s^2+as+b) + K - Ks}$

The denominator polynomial at $s=0$ is $K \neq 0$, so $G_{eq}(s)$ has no poles at the origin. Thus, the equivalent system is Type 0, even though the feedback path contained an integrator. This demonstrates that the interaction between $G(s)$ and $H(s)$ can create a fundamentally different [system type](@entry_id:269068) for tracking error analysis. This also explains a result from problem [@problem_id:15997], where for a Type 1 [forward path](@entry_id:275478) $G(s)$ to follow a [ramp input](@entry_id:271324) with finite [tracking error](@entry_id:273267), the condition on the feedback path is $H(0)=1$. This condition makes the term $(H(s)-1)$ have a zero at $s=0$, which prevents the integrator in $G(s)$ from being cancelled in the denominator of $G_{eq}(s)$, preserving a high [system type](@entry_id:269068).

### Effects of Disturbances

The analysis can be extended to find the [steady-state error](@entry_id:271143) caused by external disturbances. Consider a DC motor speed control system where a constant load disturbance $D(s) = D_0/s$ is added to the controller output, just before the plant $G_p(s)$ [@problem_id:1616020]. The reference input is zero ($R(s)=0$). The [actuating error](@entry_id:272192) is $E_a(s) = -B(s) = -H(s)Y(s)$. The output is $Y(s) = G_p(s)U(s) = G_p(s)(G_c(s)E_a(s) + D(s))$. Substituting $Y(s)$ into the error expression and solving for $E_a(s)$ yields:

$E_a(s) = -H(s)G_p(s)(G_c(s)E_a(s) + D(s))$

$\frac{E_a(s)}{D(s)} = \frac{-G_p(s)H(s)}{1 + G_c(s)G_p(s)H(s)}$

Applying the Final Value Theorem for a step disturbance, the steady-state [actuating error](@entry_id:272192) due to the disturbance is:

$e_{a,ss} = \lim_{s \to 0} s \left( \frac{-G_p(s)H(s)}{1 + G_c(s)G_p(s)H(s)} \frac{D_0}{s} \right) = \frac{-G_p(0)H(0)}{1 + G_c(0)G_p(0)H(0)} D_0$

This formula quantifies how the system rejects the disturbance at steady-state, showing that a high [loop gain](@entry_id:268715) at DC (large $G_c(0)G_p(0)H(0)$) is effective at reducing the error caused by the disturbance. For the specific [motor control](@entry_id:148305) problem with a proportional controller, this would yield a finite, non-zero error, indicating that the disturbance has a lasting effect on the system.

In summary, the presence of [sensor dynamics](@entry_id:263688) in [non-unity feedback](@entry_id:274431) systems requires a careful and precise approach to [steady-state error](@entry_id:271143) analysis. By distinguishing between actuating and tracking errors, understanding the critical role of the sensor's DC gain, and correctly applying either direct calculation or the equivalent [unity feedback](@entry_id:274594) model, a comprehensive and accurate picture of a system's long-term performance can be achieved.