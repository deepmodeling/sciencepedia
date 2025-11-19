## Introduction
In the world of digital computing, the ability to represent and manipulate both positive and negative numbers is a cornerstone of arithmetic. While modern systems predominantly use [two's complement](@entry_id:174343), understanding alternative schemes like [one's complement](@entry_id:172386) is essential for a complete education in computer architecture and digital logic. This representation, though historically older, offers valuable insights into the design trade-offs of [arithmetic circuits](@entry_id:274364) and maintains relevance in specialized applications, most notably in network communications. This article addresses the need for a thorough understanding of this system beyond a superficial comparison with its two's complement successor.

By exploring [one's complement](@entry_id:172386), you will gain a deeper appreciation for the nuances of [binary arithmetic](@entry_id:174466). The following chapters will guide you through its core concepts, practical uses, and hands-on application. The first chapter, **Principles and Mechanisms**, breaks down the fundamental rules for representing numbers, the unique "[end-around carry](@entry_id:164748)" method for addition, and the system's inherent limitations, such as the [dual representation](@entry_id:146263) of zero. Next, **Applications and Interdisciplinary Connections** reveals how these principles are implemented in hardware, from simple [logic gates](@entry_id:142135) to complex ALUs, and explores its enduring role in the Internet Checksum algorithm. Finally, **Hands-On Practices** will allow you to solidify your understanding by working through targeted problems on conversion, arithmetic, and [overflow detection](@entry_id:163270).

## Principles and Mechanisms

In the study of digital logic and [computer architecture](@entry_id:174967), the representation of signed integers is a foundational concept. While modern systems have largely standardized on two's complement representation, understanding historical and alternative schemes like [one's complement](@entry_id:172386) is crucial. It not only provides historical context but also illuminates the design trade-offs inherent in computer arithmetic. This chapter delves into the principles of the one's [complement system](@entry_id:142643), its methods for representation, its arithmetic mechanisms, and its characteristic properties and limitations.

### Representing Numbers in One's Complement

The one's complement system defines a straightforward rule for encoding signed integers within a fixed number of bits, or **word length**, denoted by $n$. The scheme bifurcates based on the sign of the number.

- **Positive Numbers and Zero:** Non-negative integers are represented using their standard binary equivalent, with leading zeros added to fill the $n$-bit word. The most significant bit (MSB) for any positive number is, by this convention, always $0$.

- **Negative Numbers:** A negative integer, $-x$, is represented by taking the **[one's complement](@entry_id:172386)** of its positive counterpart, $+x$. The [one's complement](@entry_id:172386) operation is a simple **bitwise NOT**, where every bit in the representation of $+x$ is inverted (0s become 1s, and 1s become 0s). Consequently, the MSB for any negative number is always $1$.

For example, within an 8-bit system, the decimal number $5$ is represented as $00000101$. To find the representation of $-5$, we perform a bitwise NOT on this pattern:

$$
\text{NOT}(00000101) = 11111010
$$

Thus, $11111010$ is the 8-bit [one's complement](@entry_id:172386) representation of $-5$. This operation is an **[involution](@entry_id:203735)**, meaning that applying it twice returns the original number. If a communication protocol were to invert data for transmission and the receiver were to invert it again upon receipt, the original data would be perfectly recovered. For instance, taking the [one's complement](@entry_id:172386) of $-5$ ($11111010$) yields $00000101$, which is $+5$. This self-inverting property is a fundamental characteristic of the system. [@problem_id:1949355]

### Numerical Range and the Duality of Zero

The structure of [one's complement](@entry_id:172386) representation dictates the range of values that can be expressed. For an $n$-bit word, one bit (the MSB) is reserved for the sign. This leaves $n-1$ bits to represent the magnitude. The largest positive magnitude corresponds to a pattern where all $n-1$ magnitude bits are $1$.

The maximum positive value is therefore $2^{n-1} - 1$. For example, in a 6-bit system ($n=6$), the largest positive value is $2^{6-1}-1 = 31$, represented as $011111$. The most negative value is the complement of this, which is $-(2^{n-1}-1)$, represented as $100000$. [@problem_id:1949308]

Generally, the range of integers representable in an $n$-bit one's complement system is symmetric around zero:

$$
[-(2^{n-1} - 1), \quad 2^{n-1} - 1]
$$

For a 12-bit system, this range would be $[-(2^{11}-1), 2^{11}-1]$, which evaluates to $[-2047, 2047]$. [@problem_id:1949363]

A significant and peculiar consequence of the [one's complement](@entry_id:172386) definition is the existence of two distinct representations for the number zero.
- **Positive Zero ($+0$):** Represented as a word of all zeros: $000...0$.
- **Negative Zero ($-0$):** Following the rule for negation, we find the representation of $-0$ by taking the [one's complement](@entry_id:172386) of $+0$. This results in a word of all ones: $111...1$.

In an 8-bit system, this means both $00000000$ and $11111111$ represent the integer zero. While numerically equivalent, these distinct bit patterns introduce complications in hardware design. Logic circuits that check for a zero value must be designed to recognize both patterns, for example, by using a large NOR gate for `+0` and a large AND gate for `-0`. This requirement for special handling of zero is a notable disadvantage compared to the two's [complement system](@entry_id:142643), which has a single, unambiguous representation for zero. [@problem_id:1949327] [@problem_id:1949369]

### One's Complement Arithmetic

Arithmetic operations in the one's complement system are based on standard [binary arithmetic](@entry_id:174466) but require a unique corrective step to ensure correctness.

#### Addition and the End-Around Carry

The addition of two [one's complement](@entry_id:172386) numbers is performed using a standard binary adder. However, if the addition produces a carry-out from the most significant bit, this carry bit must be "carried around" and added to the least significant bit (LSB) of the intermediate sum. This step is known as the **[end-around carry](@entry_id:164748)**.

Mathematically, this procedure correctly implements addition modulo $2^n - 1$. A standard $n$-bit adder computes the sum $S = A + B \pmod{2^n}$. The [end-around carry](@entry_id:164748) corrects this to be modulo $2^n - 1$, since $2^n \equiv 1 \pmod{2^n-1}$. Therefore, whenever a carry-out of $1$ occurs (representing a value of $2^n$), adding $1$ to the result completes the [modular arithmetic](@entry_id:143700). In hardware, this is elegantly achieved by feeding the carry-out ($C_{out}$) terminal of the [parallel adder](@entry_id:166297) back to its carry-in ($C_{in}$) terminal. [@problem_id:1949309]

Let's consider an example: adding $-3$ and $-4$ in a 4-bit system.
1.  Represent the operands: $+3$ is $0011$, so $-3$ is $1100$. $+4$ is $0100$, so $-4$ is $1011$.
2.  Perform [binary addition](@entry_id:176789):
    $$
    \begin{array}{@{}c@{\,}c@{}c@{}c@{}c@{}l}
     1  1  0  0  &(-3) \\
    +  1  0  1  1  &(-4) \\
    \hline
    \mathbf{1}  0  1  1  1  \\
    \end{array}
    $$
    The addition yields a 4-bit sum of $0111$ and a carry-out of $1$.
3.  Apply [end-around carry](@entry_id:164748): Add the carry bit to the sum.
    $$
    0111 + 1 = 1000
    $$
4.  Interpret the result: The pattern $1000$ has an MSB of 1, indicating a negative number. Its magnitude is found by complementing it: $\text{NOT}(1000) = 0111$, which is $7$. Thus, the result is $-7$. This matches the expected mathematical sum. [@problem_id:1949332]

This principle holds for all [one's complement](@entry_id:172386) additions that generate a carry. For instance, in an 8-bit system, adding $-19$ ($11101100$) and $-45$ ($11010010$) results in an intermediate sum of $10111110$ with a carry-out of $1$. Adding the [end-around carry](@entry_id:164748) yields $10111111$, which is the [one's complement](@entry_id:172386) representation of $-64$. [@problem_id:1949362]

#### Subtraction

Subtraction in [one's complement](@entry_id:172386), like in other systems, is defined as addition with the negative of the subtrahend. That is, $A - B$ is computed as $A + (-B)$. Since finding the negative of a number in [one's complement](@entry_id:172386) is a simple bitwise NOT operation, subtraction is implemented as $A + \text{NOT}(B)$. The resulting addition then follows the standard rule, including the [end-around carry](@entry_id:164748) if necessary.

Consider a legacy system calculating a temperature change, $\Delta T = 37 - 90$, using 8-bit [one's complement](@entry_id:172386).
1.  Represent the operands: $T_{final} = 37$ is $00100101$. $T_{initial} = 90$ is $01011010$.
2.  Find the [one's complement](@entry_id:172386) of the subtrahend: $-90$ is $\text{NOT}(01011010) = 10100101$.
3.  Perform the addition $37 + (-90)$:
    $$
    00100101 + 10100101 = 11001010
    $$
    In this case, there is no carry-out from the MSB, so no [end-around carry](@entry_id:164748) is needed. The result is $11001010$.
4.  To verify, we can find the decimal value of this result. It is a negative number, and its complement is $\text{NOT}(11001010) = 00110101$, which is $32 + 16 + 4 + 1 = 53$. The result is therefore $-53$, which correctly matches $37 - 90$. [@problem_id:1949339]

### Bitwise Shifts and Division

In [binary systems](@entry_id:161443), a right shift is often used as a fast, low-cost method for [integer division](@entry_id:154296) by two. An **arithmetic right shift (ARS)** is designed for [signed numbers](@entry_id:165424); it shifts all bits one position to the right, but instead of filling the vacated MSB with a 0 (as in a logical shift), it replicates the original MSB. This preserves the number's sign.

However, in the one's complement system, using an ARS for division is not always accurate. Let's examine the behavior for negative numbers. Consider the number $-1$ in an 8-bit system, which is represented as $11111110$. Performing a single ARS:
- The bits are shifted right: `_1111111`.
- The original MSB (1) is copied into the new MSB position.
- The result is $11111111$.

This resulting pattern is the representation of [negative zero](@entry_id:752401) ($-0$), which has a numerical value of $0$. The correct mathematical result of $\lfloor -1 / 2 \rfloor$ is $-1$. Thus, the ARS operation produced an error. [@problem_id:1949306]

This is not an isolated case but a [systematic error](@entry_id:142393) for a specific class of numbers. When an ARS is performed on the [one's complement](@entry_id:172386) representation of any **negative odd integer**, the result is consistently incorrect. Let the negative odd integer be $v = -m$, where $m$ is a positive odd integer. The [one's complement](@entry_id:172386) bit pattern for $v$ will have an LSB of $0$ (since the LSB of $m$ is $1$). The ARS operation discards this $0$. A detailed analysis shows that the value produced by the ARS is $-(\lfloor m/2 \rfloor)$. The mathematically correct [integer division](@entry_id:154296), however, is $\lfloor v/2 \rfloor = \lfloor -m/2 \rfloor = -(\lceil m/2 \rceil)$.

For any odd $m$, we have $\lceil m/2 \rceil = (m+1)/2$ and $\lfloor m/2 \rfloor = (m-1)/2$. The error is the difference between the ARS result and the correct value:
$$
\text{Error} = \left( - \frac{m-1}{2} \right) - \left( - \frac{m+1}{2} \right) = \frac{-m+1+m+1}{2} = \frac{2}{2} = 1
$$
This demonstrates that for any negative odd integer, division by two via a single arithmetic right shift in a one's [complement system](@entry_id:142643) produces a result that is exactly $1$ greater than the correct mathematical value. This systemic flaw, along with the [dual representation](@entry_id:146263) of zero, illustrates the complexities that led to the widespread adoption of two's complement as the dominant standard for signed integer arithmetic in modern computers. [@problem_id:1949359]