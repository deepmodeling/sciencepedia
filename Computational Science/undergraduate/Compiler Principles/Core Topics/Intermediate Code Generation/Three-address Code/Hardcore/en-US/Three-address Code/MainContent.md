## Introduction
In the intricate process of transforming human-readable source code into efficient machine-executable instructions, compilers rely on a crucial intermediate step. This middle ground is occupied by Intermediate Representation (IR), and among the most fundamental and influential forms of IR is Three-Address Code (TAC). TAC acts as a universal language within the compiler, abstracting away from both the complexities of the source language and the specifics of the target machine. This abstraction is the key that unlocks the potential for powerful, machine-independent analysis and optimization. This article bridges the gap between high-level language theory and low-level implementation by providing a deep dive into the world of TAC.

Across the following chapters, you will gain a comprehensive understanding of this pivotal compiler component. The first chapter, **Principles and Mechanisms**, demystifies the structure of TAC, exploring its various representations like quadruples and triples, and detailing the systematic processes for translating expressions and control flow. Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates the true power of TAC, showcasing its central role in classic code optimizations and its surprising relevance in fields ranging from database systems to hardware design. Finally, the **Hands-On Practices** section provides opportunities to apply this knowledge through targeted exercises. We begin by examining the foundational principles that govern the structure of TAC and the core mechanisms used to translate high-level language constructs into this versatile representation.

## Principles and Mechanisms

Three-Address Code (TAC) serves as a refined, machine-independent Intermediate Representation (IR) that is amenable to analysis and transformation. Its structure is designed to be close enough to machine language to allow for straightforward [code generation](@entry_id:747434), yet abstract enough to hide machine-specific details and facilitate high-level optimizations. This chapter elucidates the fundamental principles governing the structure of TAC and the core mechanisms used to translate high-level language constructs into this representation.

### The Structure of Three-Address Code

At its core, a three-address instruction is a statement that involves at most three "addresses"—typically two operands and one destination. These addresses can refer to program variables, constants, or compiler-generated temporary variables.

#### Defining Three-Address Instructions

The [canonical form](@entry_id:140237) of a three-address instruction is an assignment statement of the form:
$x := y \ \text{op} \ z$

Here, $x$ is the destination address that receives the result of applying the binary operator `op` to the operand addresses $y$ and $z$. This simple, [uniform structure](@entry_id:150536) is powerful because it decomposes complex, nested expressions found in high-level languages into a linear sequence of elementary operations. For example, the expression `$a * b + c * d$` would be broken down into:

$t_1 := a * b$
$t_2 := c * d$
$t_3 := t_1 + t_2$

This decomposition introduces **temporary variables** ($t_1$, $t_2$, $t_3$) to hold intermediate results. The management of these temporaries and the representation of the instructions themselves are key design choices in a compiler. Other common forms of TAC include unary operations ($x := \text{op} \ y$), copy statements ($x := y$), unconditional jumps (`goto L`), and [conditional jumps](@entry_id:747665) (`if x \text{ relop } y \text{ goto } L`).

#### Representing TAC: Quadruples, Triples, and Indirect Triples

There are several common data structures for representing TAC instructions in memory, each with distinct trade-offs regarding storage space and ease of manipulation during optimization. The most common are quadruples and triples.

A **quadruple**, or "quad," is a record with four fields: `(op, arg1, arg2, result)`. This representation is explicit and self-contained. The `result` field contains a direct reference to the destination, typically a pointer to the symbol table entry for the named temporary or variable. For instance, the instruction $t_1 := a + b$ would be stored as a record containing the operator `+`, pointers to `a` and `b`, and a pointer to `t_1`.

A **triple** omits the explicit result field, consisting of only three fields: `(op, arg1, arg2)`. The result of an instruction is implicitly defined by its position in the instruction sequence. For example, if the instruction `(+, a, b)` is at index $0$ in an array of triples, any subsequent instruction that needs to use this result refers to it by its position, `pos 0`.

Let's consider the translation of the expression $x := (a + b) \times (c - d) + (a + b)$ to illustrate the difference .

A quadruple representation might look like this:
1. $(+, a, b, t_1)$
2. $(-, c, d, t_2)$
3. $(*, t_1, t_2, t_3)$
4. $(+, t_3, t_1, t_4)$
5. $(:=, t_4, \text{null}, x)$

Notice that the common subexpression $(a + b)$ is computed once, and its result is stored in the named temporary $t_1$, which is then reused. The key advantage of quadruples becomes apparent during [code optimization](@entry_id:747441). If a compiler decides to move an instruction (a form of **[code motion](@entry_id:747440)**), the symbolic references remain valid. For example, moving instruction 3 to a different location in the code does not require changing the operand `t_1` in instruction 4, as long as the definition of `t_1` still precedes its use.

A triple representation for the same expression would use positional references:
0. $(+, a, b)$
1. $(-, c, d)$
2. $(*, \text{pos }0, \text{pos }1)$
3. $(+, \text{pos }2, \text{pos }0)$
4. $(:=, \text{pos }3, x)$

Here, the result of the addition at index $0$ is referenced by `pos 0` in instruction 3. The main drawback of triples is that [code motion](@entry_id:747440) becomes difficult. If the instruction at index $i$ is moved to a new position $j$, all other instructions that refer to `pos i` must be found and updated to refer to `pos j`. This ripple effect of updates complicates many optimizations.

To combine the space efficiency of triples with the flexibility of quadruples, compilers can use **indirect triples**. This approach maintains two data structures: the array of triple records themselves and a separate array of pointers (or indices) that list the order in which the triples should be executed. Code motion is achieved by simply reordering the pointers in the execution list, leaving the triple records and their internal positional references untouched. This provides a level of indirection that decouples the logical instruction order from the physical storage order.

### Translating Expressions into Three-Address Code

The translation process systematically deconstructs high-level expressions into a linear sequence of TAC instructions. This process is sensitive to [operator precedence](@entry_id:168687), data types, and the structure of data in memory.

#### Arithmetic Expressions

The structure of an arithmetic expression directly influences the resulting TAC and, consequently, resource requirements such as the number of temporary variables. For an associative operator like addition, different parenthesizations such as $(a + b) + c$ and $a + (b + c)$ are mathematically equivalent but can lead to different TAC sequences.

For $(a + b) + c$, the generated code is:
$t_1 := a + b$
$t_2 := t_1 + c$
$x := t_2$

For $a + (b + c)$, the sequence is:
$t_1 := b + c$
$t_2 := a + t_1$
$x := t_2$

In both of these cases, the operations form a simple chain where the result of one temporary is immediately consumed by the next instruction. As we will see later, this results in a low peak requirement for registers . In contrast, an expression like $(p+q)*(r-s)$ from  requires computing two independent subexpressions first:

$t_1 := p + q$
$t_2 := r - s$
$t_3 := t_1 \times t_2$
$w := t_3$

Here, the values of $t_1$ and $t_2$ must be kept alive simultaneously before they can be used in the final multiplication. This structural difference has direct implications for [register allocation](@entry_id:754199).

#### Accessing Complex Data Structures

Translating expressions involving pointers, arrays, and structures requires generating TAC that correctly computes memory addresses based on base pointers and offsets.

Consider a C-like pointer arithmetic statement: $q = p + i \times \operatorname{sizeof}(T)$ . A compiler must respect several rules during translation. First, if $\operatorname{sizeof}(T)$ is a compile-time constant (e.g., if type $T$ is a struct with a fixed layout of three 4-byte integers, its size is $12$), the compiler can perform **[constant folding](@entry_id:747743)** and substitute the value directly. The expression becomes $q = p + i \times 12$. The TAC generation then proceeds according to [operator precedence](@entry_id:168687):

$t_1 := i \times 12$
$q := p + t_1$

This translation must also respect the language's type system. If $i$ is a 16-bit integer and pointer arithmetic is performed with 64-bit values, the compiler must emit code to handle the **type promotion** of $i$ to a 64-bit integer (typically via sign-extension) before the arithmetic operations. For example, if $p$ is address $4096$ and $i$ is $-3$, the TAC would compute $t_1 = -36$, and the final address in $q$ would be $4096 + (-36) = 4060$.

Accessing fields within a structure, as in $x = p \rightarrow f + p \rightarrow g$, also involves address computation . The address of a field is calculated by adding its compile-time offset to the base address of the structure, which is held in the pointer $p$. The expression is equivalent to $\mathrm{load}(p + off_f) + \mathrm{load}(p + off_g)$. A straightforward TAC translation is:

$t_1 := p + off_f$  (address of field f)
$t_2 := \mathrm{load}(t_1)$ (value of field f)
$t_3 := p + off_g$  (address of field g)
$t_4 := \mathrm{load}(t_3)$ (value of field g)
$t_5 := t_2 + t_4$
$x := t_5$

An [optimizing compiler](@entry_id:752992) might notice that both addresses are derived from the same base pointer $p$. If the fields are located near each other, it can generate more efficient [address arithmetic](@entry_id:746274). For example, it could compute the second address relative to the first:

$t_1 := p + off_f$
$t_2 := \mathrm{load}(t_1)$
$\Delta := off_g - off_f$ (compile-time constant)
$t_3 := t_1 + \Delta$  (computes $p + off_f + (off_g - off_f) = p + off_g$)
$t_4 := \mathrm{load}(t_3)$
$t_5 := t_2 + t_4$
$x := t_5$

This alternative sequence still performs two address calculations and two loads but may be more amenable to certain machine instruction sets that have [addressing modes](@entry_id:746273) with a base register and a small offset.

#### Memory Operations and Alias Analysis

The use of `load` and `store` instructions highlights a critical challenge for compilers: **[memory aliasing](@entry_id:174277)**. Two pointers are said to alias if they can refer to the same memory location. The possibility of [aliasing](@entry_id:146322) imposes strict constraints on instruction reordering.

Consider the program fragment $x = *p + *q; *p = 0;$. The natural translation involves loading from the locations pointed to by $p$ and $q$, performing the addition, and then storing $0$ to the location pointed to by $p$. A key question for an [optimizing compiler](@entry_id:752992) is whether it can reorder these operations, for instance, by delaying the load from `*q` until after the store to `*p` .

The safety of this transformation depends entirely on whether $p$ and $q$ can alias.
- **Case 1: No Alias.** If the compiler can prove that $p$ and $q$ will *never* point to the same memory location ($\ell(p) \neq \ell(q)$), the operations $\mathrm{load}(\ell(q))$ and $\mathrm{store}(\ell(p), 0)$ are independent. Reordering them does not change the program's behavior.
- **Case 2: May Alias.** If $p$ and $q$ *might* point to the same location, the reordering is unsafe. If they do alias, the original code reads the value from $\ell(q)$, then overwrites it. The reordered code would first overwrite the value, and the subsequent load from $\ell(q)$ would read the newly stored value ($0$), producing a different result.

Because correctness is paramount, a compiler must be conservative. In the absence of a definitive proof of **no-alias**, it must assume a **may-alias** condition exists and preserve the original program order. This dependence between a load and a store to potentially the same address is known as a memory-based dependency, and **alias analysis** is the set of techniques compilers use to disambiguate these memory references to enable more aggressive optimization.

### Translating Control Flow Statements

Control flow constructs like `if-then-else`, loops, and [boolean expressions](@entry_id:262805) are translated into TAC using conditional and unconditional jump instructions.

#### Boolean Expressions and Short-Circuiting

High-level languages often feature **[short-circuit evaluation](@entry_id:754794)** for boolean operators. For a conjunction $a \land b$, if $a$ is false, the entire expression is false, and $b$ is not evaluated. Similarly, for a disjunction $a \lor b$, if $a$ is true, the entire expression is true, and $b$ is not evaluated. This logic is implemented in TAC using a pattern of [conditional jumps](@entry_id:747665).

For an expression like $a \land b \land c$, the generated code checks each condition in sequence. If any check fails, control immediately branches to a common failure label .

```
      if a == 0 goto L_fail
      if b == 0 goto L_fail
      if c == 0 goto L_fail
t_bool := 1
      goto L_end
L_fail:
t_bool := 0
L_end:
      ...
```
This structure ensures that operands are evaluated only when necessary. The performance of this code can even be modeled probabilistically. If the probabilities of $a$, $b$, and $c$ being true are $p_a$, $p_b$, and $p_c$ respectively, the expected number of instructions executed can be derived, demonstrating how code structure impacts runtime efficiency.

For more complex [boolean expressions](@entry_id:262805), such as $b = (a > b) \lor (c > d \land e == f)$, generating this jump-based code becomes intricate. A systematic method called **[backpatching](@entry_id:746635)** is used . During a first pass, TAC is generated for the relational tests, but the jump targets are left as placeholders. For each subexpression, the compiler maintains a `[truelist](@entry_id:756190)` (a list of jumps taken if the expression is true) and a `falselist`.

As larger expressions are parsed, these lists are merged according to the [logical operators](@entry_id:142505)' semantics.
- For $E_1 \land E_2$, the `[truelist](@entry_id:756190)` of $E_1$ is backpatched to point to the start of $E_2$'s code. The combined `falselist` is the union of $E_1$'s and $E_2$'s falselists.
- For $E_1 \lor E_2$, the `falselist` of $E_1$ is backpatched to point to the start of $E_2$'s code. The combined `[truelist](@entry_id:756190)` is the union of their truelists.

After parsing the entire expression, all jumps in the final `[truelist](@entry_id:756190)` are backpatched to the code block for the "true" outcome (e.g., `b := 1`), and all jumps in the final `falselist` are patched to target the "false" outcome (e.g., `b := 0`). This two-pass process elegantly handles nested logic and forward jumps without requiring complex fix-ups. For the expression above, this systematic process generates exactly 9 TAC instructions to implement the logic, assignments, and control flow.

#### Looping Constructs

Loops are translated into a combination of [conditional jumps](@entry_id:747665) and unconditional jumps that form the loop's control structure. A canonical `for` loop like `for(i = 0; i  n; i++)` is typically lowered into a structure with an initialization, a header, a body, and an update section .

```
      i := 0
L_loop_header:
      if i >= n goto L_exit
      // ... TAC for loop body ...
      i := i + 1
      goto L_loop_header
L_exit:
      ...
```

Understanding this structure allows for precise analysis of a loop's execution cost. If the loop body consists of 6 TAC statements, each full iteration executes $1$ (conditional jump) $+ 6$ (body) $+ 1$ (increment) $+ 1$ (unconditional jump) $= 9$ instructions. For a loop that runs $n$ times, the total executed instructions would be the initialization ($1$), the $n$ successful iterations ($9n$), and the final conditional jump to exit the loop ($1$), for a total of $9n + 2$ instructions. This kind of analysis is fundamental to performance estimation and optimization.

### Foundations of Optimization on Three-Address Code

The regular, explicit nature of TAC makes it an ideal substrate for [program analysis](@entry_id:263641) and optimization. Two of the most important foundational concepts are [liveness analysis](@entry_id:751368) and Static Single Assignment form.

#### Liveness Analysis and Register Allocation

To make efficient use of the CPU's fast registers, the compiler must determine which variables or temporaries can share the same register. Two variables can share a register if their lifetimes do not overlap. The process of determining these lifetimes is called **[liveness analysis](@entry_id:751368)**.

A variable is **live** at a program point if its current value may be used in the future. The **liveness interval** of a variable is the span of program points from its definition to its last use. Two variables **interfere** if their liveness intervals overlap.

Let's revisit the expression $w = (p+q) \times (r-s)$ and its TAC :
1. $t_1 := p + q$
2. $t_2 := r - s$
3. $t_3 := t_1 \times t_2$
4. $w := t_3$

Analyzing the liveness of the temporaries:
- $t_1$ is defined at instruction 1 and last used at instruction 3. It must remain alive during instruction 2. Its liveness interval spans from after instruction 1 to after instruction 3's use.
- $t_2$ is defined at instruction 2 and last used at instruction 3. Its liveness interval spans from after instruction 2 to after instruction 3's use.
- $t_3$ is defined at instruction 3 and last used at instruction 4. Its interval is from after instruction 3 to after instruction 4's use.

At the program point between instructions 2 and 3, both $t_1$ and $t_2$ are live. This means their liveness intervals overlap, so they interfere and cannot be allocated to the same register. However, the interval for $t_3$ does not overlap with that of $t_1$ or $t_2$. A valid [register allocation](@entry_id:754199) could therefore be: assign $t_1$ to register $R_1$, assign $t_2$ to register $R_2$, and then reuse $R_1$ for $t_3$.

The maximum number of variables that are simultaneously live at any single point in the program is called the **[register pressure](@entry_id:754204)**. For this code, the pressure is 2. This value determines the minimum number of registers required to execute the code without **spilling** (storing a temporary back to [main memory](@entry_id:751652)). In contrast, the chained expressions from  had a [register pressure](@entry_id:754204) of only 1.

#### Static Single Assignment (SSA) Form

A particularly powerful refinement of TAC is **Static Single Assignment (SSA) form**. In SSA, every variable is assigned a value exactly once in the program text. To achieve this, each time a variable is redefined, a new version of it is created, typically denoted with a subscript (e.g., $y_0, y_1, y_2$).

When different control flow paths that define the same original variable merge at a join point, a special **[phi-function](@entry_id:753402) (φ)** is inserted. The φ-function selects the appropriate version of the variable based on which path was taken to reach the join point.

Consider a [control-flow graph](@entry_id:747825) where block $B_0$ defines $x_1$, then branches. Path 1 goes through block $B_1$, which redefines $y$ to $y_1$ and $x$ to $x_2$. Path 2 goes through block $B_2$, which does nothing. Both paths join at $B_3$ .

- **In $B_0$**: $x_1 := y_0 + z_0$
- **In $B_1$**: $y_1 := y_0 + 1$; $x_2 := y_1 + z_0$
- **At the join point $B_3$**:
  $y_2 := \phi(y_1, y_0)$ (Selects $y_1$ if from $B_1$, $y_0$ if from $B_2$)
  $x_3 := \phi(x_2, x_1)$ (Selects $x_2$ if from $B_1$, $x_1$ if from $B_2$)

The key benefit of SSA is that data-flow dependencies become explicit in the naming scheme. A use of $y_1$ can only be reached by the single definition of $y_1$. This simplifies numerous optimizations, such as [constant propagation](@entry_id:747745) and [dead code elimination](@entry_id:748246). The semantics of SSA also lend themselves to powerful algebraic reasoning. If the choice to take the path through $B_1$ is encoded by a variable $p=1$ (and $p=0$ for the path through $B_2$), the final value $x_3$ can be expressed as an algebraic formula: $x_3 = p \cdot x_2 + (1-p) \cdot x_1$. Substituting the definitions of $x_1$ and $x_2$ yields $x_3 = y_0 + z_0 + p$, elegantly capturing the entire control-flow logic in a single expression. This analytical power is a primary reason for SSA's prevalence in modern optimizing compilers.