## Introduction
High-fidelity simulation is indispensable for the design and analysis of modern battery systems, yet the computational cost of solving the underlying coupled electrochemical-thermal equations presents a formidable bottleneck. To overcome this, researchers are increasingly turning to Graphics Processing Units (GPUs) for their massive parallel processing capabilities. However, unlocking this performance is not a simple matter of code porting; it demands a deep, first-principles understanding of the interplay between parallel hardware, [numerical algorithms](@entry_id:752770), and the physics of the problem. This article provides a comprehensive guide to GPU acceleration for battery solvers, bridging theory and practice.

The following chapters will guide you through this complex landscape. **Principles and Mechanisms** will deconstruct the GPU architecture, [memory model](@entry_id:751870), and execution paradigms that dictate performance. **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied to build robust solvers and integrate them into automated design workflows, highlighting connections to physics and sustainable computing. Finally, **Hands-On Practices** will offer concrete exercises to solidify your understanding of key optimization techniques. We begin by exploring the fundamental principles and mechanisms that govern computation on a GPU.

## Principles and Mechanisms

The acceleration of electrochemical-thermal solvers on Graphics Processing Units (GPUs) is not a matter of simple code porting. It requires a fundamental understanding of the architectural principles and execution mechanisms that differentiate GPUs from traditional central processing units (CPUs). Achieving high performance hinges on restructuring algorithms and data to align with the GPU's massively parallel design. This chapter delineates these core principles, from the hardware's execution model and [memory hierarchy](@entry_id:163622) to [performance modeling](@entry_id:753340), multi-GPU scaling, and crucial numerical considerations.

### The GPU Execution Model: Massively Parallel Processing

At the heart of the GPU's computational power is a design philosophy centered on executing the same operation across vast amounts of data in parallel. This philosophy is realized through a specific architectural and execution model.

#### Streaming Multiprocessors, Warps, and Threads

The fundamental processing unit on an NVIDIA GPU is the **Streaming Multiprocessor (SM)**. An SM is a sophisticated, independent processor equipped with numerous arithmetic logic units (ALUs), a large [register file](@entry_id:167290), and a dedicated, low-latency on-chip memory known as **[shared memory](@entry_id:754741)**. Each SM is capable of concurrently managing and executing hundreds or thousands of threads.

These threads are organized into a three-level hierarchy:
1.  **Thread**: The smallest unit of execution. A thread is a scalar process with its own private set of registers and a [program counter](@entry_id:753801). In the context of a finite-volume or [finite-difference](@entry_id:749360) solver for battery models, a common strategy is to map a single thread to a single grid cell or control volume.
2.  **Warp**: Threads are executed in groups of $32$, known as a warp. A warp is the [fundamental unit](@entry_id:180485) of scheduling on the SM. All $32$ threads in a warp execute the same instruction at the same time. This execution model is called **Single Instruction, Multiple Threads (SIMT)**.
3.  **Thread Block**: Warps are grouped into thread blocks. A thread block is a collection of threads (up to $1024$ in modern architectures) that can cooperate by sharing data through the fast on-chip [shared memory](@entry_id:754741) and can synchronize their execution. An SM can host one or more thread blocks simultaneously, resource permitting. 

The SIMT model is distinct from both the Single Instruction, Multiple Data (SIMD) model often found in CPU vector units and the Multiple Instruction, Multiple Data (MIMD) model of multi-core CPUs. In a pure SIMD model, all vector lanes share a single register context and cannot execute independent control-flow paths. In a MIMD model, each core executes its own instruction stream independently. SIMT offers a powerful abstraction: it presents a model of independent scalar threads, but the hardware implements it by executing these threads in lockstep warps. This provides programmability closer to MIMD while retaining the hardware efficiency of SIMD for data-parallel tasks. 

#### Warp Divergence: The Cost of Branching

The lockstep execution of threads within a warp has a profound performance implication known as **warp divergence**. When a conditional branch (an `if-else` statement) is encountered and threads within the same warp take different paths, the hardware must serialize the execution of these paths. All threads that take the `if` path execute their instructions while the others are idle. Then, all threads that take the `else` path execute their instructions while the first group is idle. The total time taken is the sum of the times for both paths.

Consider a kernel in a battery solver that applies a specific Robin boundary condition at electrode-separator interfaces but uses a different update rule for interior cells. If a warp contains a mix of threads corresponding to both boundary and interior cells, it will experience divergence. Suppose in a warp of $W=32$ threads, a fraction $q=0.25$ (i.e., $8$ threads) execute a boundary path of length $L_A=40$ instructions, while the remaining $1-q=0.75$ ($24$ threads) execute an interior path of $L_B=24$ instructions.

An ideal MIMD machine would execute a total of $W(q L_A + (1-q) L_B) = 32(0.25 \times 40 + 0.75 \times 24) = 32 \times 28 = 896$ useful instructions. The time taken would be proportional to the average path length, $28$ cycles (assuming one instruction per cycle). However, due to serialization under the SIMT model, the warp executes the first path (taking $L_A=40$ cycles) and then the second path (taking $L_B=24$ cycles), for a total of $L_A + L_B = 64$ cycles.

The **instruction throughput factor**, which measures the fraction of ideal throughput achieved, can be quantified as the ratio of the [average path length](@entry_id:141072) to the total serialized path length:
$$ \text{Throughput Factor} = \frac{q L_A + (1-q) L_B}{L_A + L_B} = \frac{28}{64} = 0.4375 $$
In this scenario, divergence reduces the warp's instruction throughput to just $43.75\%$ of the ideal. Consequently, a key principle for GPU performance is to organize data and thread mappings to minimize warp divergence, ensuring that threads within a warp follow the same control-flow path as much as possible. 

### The GPU Memory Hierarchy: The Path to High Throughput

The single greatest determinant of performance in most electrochemical-thermal solvers is memory access. GPU hardware provides a multi-level [memory hierarchy](@entry_id:163622), and effective use of this hierarchy is paramount.

The main levels are:
- **Registers**: The fastest memory, with single-cycle latency. Registers are private to each thread and are used to store local variables and intermediate computation results. The total number of registers on an SM is large but finite, and exceeding the per-thread limit causes **[register spilling](@entry_id:754206)**, where data is moved to the much slower global memory, severely degrading performance. 
- **Shared Memory**: A low-latency (tens of cycles) on-chip memory that is explicitly managed by the programmer. It is shared by all threads within a single thread block, enabling fast data exchange and cooperation. It functions as a programmable cache.
- **L2 Cache**: A larger, on-chip cache shared by all SMs on the GPU. It automatically caches data from global memory, helping to reduce off-chip traffic, especially when different thread blocks access adjacent data regions.
- **Global Memory**: The largest-capacity memory, residing on off-chip DRAM (e.g., GDDR6 or HBM). It has the highest latency (hundreds of cycles) but also massive bandwidth. The entire state of the battery simulation (temperature fields, concentrations, potentials) resides here.

The primary goal of memory optimization is to maximize the use of fast on-chip memory (registers and [shared memory](@entry_id:754741)) to minimize traffic to the slow off-chip global memory.

#### Data Layout: Structure of Arrays (SoA) for Coalescing

The way data is organized in global memory directly impacts access efficiency. Consider a typical multiphysics scenario where each grid cell holds multiple state variables, such as electrolyte concentration ($c_i$), potentials ($\phi_{s,i}, \phi_{e,i}$), and temperature ($T_i$).  There are two primary layouts:

- **Array of Structures (AoS)**: All fields for a single cell are stored contiguously in a struct. The overall data is an array of these structs: `[c₀, φₛ₀, φₑ₀, T₀], [c₁, φₛ₁, φₑ₁, T₁], ...`
- **Structure of Arrays (SoA)**: Each field is stored in its own separate, contiguous array: `[c₀, c₁, c₂, ...], [φₛ₀, φₛ₁, φₛ₂, ...], ...`

GPUs achieve high global [memory bandwidth](@entry_id:751847) through **coalesced access**. This occurs when the 32 threads of a warp access consecutive, aligned memory locations. The hardware can then service these 32 individual requests with a minimal number of large memory transactions.

Now, consider a kernel where each thread $t$ reads only the temperature $T_t$.
- With an **SoA** layout, the threads of a warp access `T[0], T[1], ..., T[31]`. These are contiguous memory locations, leading to a perfectly coalesced access. The memory hardware fetches a single, contiguous block of data, and all the data fetched is useful.
- With an **AoS** layout, the threads access `data[0].T, data[1].T, ...`. These memory locations are separated by the size of the entire struct. This is a **strided access**. To service these requests, the hardware must fetch multiple, disjoint memory segments, most of whose contents (the other fields like $c$ and $\phi$) are not needed by the kernel. This wastes [memory bandwidth](@entry_id:751847).

Quantitatively, let's analyze the access pattern from , where a warp of $W=32$ threads reads one $8$-byte double-precision temperature value per thread. The struct size in AoS is $48$ bytes (6 fields $\times$ 8 bytes/field), and memory transactions are $S=128$ bytes.
- In **SoA**, the $32$ threads request a contiguous block of $32 \times 8 = 256$ bytes. This is serviced by $256/128 = 2$ memory transactions. The payload efficiency (useful bytes / transferred bytes) is $\eta_{SoA} = \frac{256}{2 \times 128} = 1.0$.
- In **AoS**, the stride between requests is $48$ bytes. The first thread reads an address in the first $128$-byte segment, and the 32nd thread reads from an address $31 \times 48 = 1488$ bytes later, which falls into the 12th segment. This requires $12$ separate memory transactions, transferring $12 \times 128 = 1536$ bytes. The efficiency is $\eta_{AoS} = \frac{256}{1536} \approx 0.167$.

For [multiphysics](@entry_id:164478) solvers where kernels often operate on a subset of fields, the **SoA layout is unequivocally superior** for achieving high GPU throughput.

#### Shared Memory for Data Reuse and Bank Conflicts

For stencil-based computations, such as the discretization of diffusion terms ($\nabla \cdot (k \nabla T)$), each thread needs to read data from its neighboring cells. A naive implementation would have each thread fetch its own value and its neighbors' values directly from global memory. For a [7-point stencil](@entry_id:169441) in 3D, this would mean 7 loads per thread, with significant data overlap between adjacent threads.

A far more efficient strategy is **tiling using [shared memory](@entry_id:754741)**. A thread block collectively loads a tile of the input field from global memory into the on-chip [shared memory](@entry_id:754741). These loads are structured to be fully coalesced. Once the tile is in [shared memory](@entry_id:754741), threads can perform the stencil computations by reading from this low-latency memory. Because neighboring threads in the block need overlapping data, each value loaded into [shared memory](@entry_id:754741) is reused multiple times. This technique can reduce the number of global memory loads per output point from 7 to an amortized value close to 1, dramatically increasing the kernel's arithmetic intensity and performance. 

However, [shared memory](@entry_id:754741) has its own performance pitfalls, most notably **bank conflicts**. Shared memory is organized into a number of banks (typically 32). It can service one request per bank per cycle. A bank conflict occurs when two or more threads in a warp try to access *different* addresses that map to the same memory bank. This forces the accesses to be serialized, reducing the [effective bandwidth](@entry_id:748805) of [shared memory](@entry_id:754741).

This is a particular concern for multi-dimensional data layouts. Consider a 2D tile stored in [row-major order](@entry_id:634801) in [shared memory](@entry_id:754741), which has $32$ banks, each $4$ bytes wide. For double-precision data ($8$ bytes), an access to consecutive elements in a row will map to consecutive banks (e.g., banks 0-1, 2-3, 4-5...), which is conflict-free. However, if threads in a warp access elements in the same *column*, their addresses will be separated by the padded width of the tile, $L_x$. The bank index for an element is proportional to its address. For an access to row $j_t$ and column $i_t$, the bank index can be described as $b \equiv c_0 + 2(j_t L_x + i_t) \pmod{32}$. When threads access a column, $i_t$ is fixed and $j_t$ varies. The bank index changes by $2 L_x$ for each row. If the tile width $L_x$ is a multiple of 16, then $2L_x$ is a multiple of 32, and all threads accessing the column will target the same bank, causing a worst-case 32-way bank conflict. A common solution is to add padding to the tile width in [shared memory](@entry_id:754741) (e.g., use `double tile[HEIGHT][WIDTH+1]`) so that $L_x$ is not a multiple of 16, thus staggering the bank accesses and avoiding conflicts. 

### Performance Modeling and Optimization

To reason systematically about performance, we can use conceptual models that relate an algorithm's properties to the hardware's capabilities.

#### The Roofline Model

The **Roofline Model** provides an intuitive upper bound on the performance of a kernel. It states that the attainable [floating-point operations](@entry_id:749454) per second (FLOPS) is limited by the minimum of two factors: the machine's peak computational throughput ($\Pi_{peak}$) and the product of the machine's peak memory bandwidth ($B_{peak}$) and the kernel's **[arithmetic intensity](@entry_id:746514)** ($I$).
$$ P \le \min(\Pi_{peak}, I \cdot B_{peak}) $$
Arithmetic intensity is the crucial kernel-specific parameter, defined as the ratio of total [floating-point operations](@entry_id:749454) performed to the total bytes transferred from/to global memory.
$$ I = \frac{\text{Floating-point Operations}}{\text{Bytes Transferred}} $$
Kernels with low [arithmetic intensity](@entry_id:746514) are **[memory-bound](@entry_id:751839)**; their performance is dictated by how fast data can be supplied from memory. Kernels with high [arithmetic intensity](@entry_id:746514) are **compute-bound**; their performance is dictated by the speed of the arithmetic units. The crossover point occurs at the **machine balance**, $I_{knee} = \Pi_{peak} / B_{peak}$.

Let's apply this to representative kernels in a battery solver on a GPU with $\Pi_{peak} = 7.8$ TFLOPS (double-precision) and $B_{peak} = 1.5$ TB/s, giving $I_{knee} \approx 5.2$ FLOPs/byte. 
- A **Sparse Matrix-Vector (SpMV)** kernel using CSR format for an unstructured mesh is typically [memory-bound](@entry_id:751839). Per non-zero element, it performs 2 FLOPs (a multiply and an add) and requires reading the matrix value (8 bytes), the column index (4 bytes), and the corresponding input vector element (8 bytes), totaling 20 bytes. Its [arithmetic intensity](@entry_id:746514) is $I_{SpMV} = 2/20 = 0.1$ FLOPs/byte. Since $0.1 \ll 5.2$, it is deeply [memory-bound](@entry_id:751839). Its performance is capped by the [memory bandwidth](@entry_id:751847): $P_{bound} = 0.1 \text{ FLOP/byte} \times 1.5 \text{ TB/s} = 0.15$ TFLOPS.
- A tiled **[7-point stencil](@entry_id:169441)** kernel is more intense. For each output point, it might perform 13 FLOPs. With efficient tiling, the memory traffic is one read and one write per point, or 16 bytes. Its intensity is $I_{stencil} = 13/16 \approx 0.81$ FLOPs/byte. While higher than SpMV, this is still less than $I_{knee}$, so it is also [memory-bound](@entry_id:751839), but less severely.  

#### Occupancy and Latency Hiding

The Roofline model provides a theoretical upper bound. How close an implementation gets to this bound is determined by its ability to fully utilize the hardware. A key factor is **occupancy**, defined as the ratio of active warps per SM to the maximum number of warps the SM can support.

High occupancy is critical for hiding the high latency of global memory access. When one warp stalls waiting for data, the SM's warp scheduler can instantly switch to another resident, ready-to-execute warp. If there are enough active warps, the SM's arithmetic units can be kept busy, effectively hiding the [memory latency](@entry_id:751862) and achieving performance close to the Roofline bound.

Occupancy is limited by the per-block resource usage. An SM can only host as many blocks as fit within its [register file](@entry_id:167290) and [shared memory](@entry_id:754741) capacity. For instance, if a kernel uses many registers per thread or a large amount of [shared memory](@entry_id:754741) per block, the number of resident blocks per SM will be low, leading to low occupancy. While high occupancy is generally beneficial for [memory-bound](@entry_id:751839) kernels, it is not a goal in itself. If a kernel's performance is already saturating the memory bus, a further increase in occupancy may not yield any benefit. 

### Orchestrating Work: Asynchronous Execution and Programming Models

Beyond optimizing a single kernel, overall application performance depends on orchestrating multiple tasks—kernel executions and data transfers—efficiently.

#### Overlapping Tasks with Streams and Events

A **CUDA stream** is a sequence of operations (kernel launches, memory copies) that execute in order on the GPU. The key to task-level parallelism is that operations in *different* streams can execute concurrently, subject to hardware capabilities and data dependencies.

This allows for the powerful optimization of **overlapping computation with communication**. For example, while the GPU is busy executing a computational kernel (e.g., updating the electrolyte concentration), the CPU can issue an asynchronous memory copy in a separate stream to transfer boundary condition data for the *next* time step from host to device. 

To enable true asynchronous host-to-device or device-to-host memory copies that can overlap with kernel execution, the host-side memory must be **page-locked (pinned)**. This prevents the operating system from [paging](@entry_id:753087) the memory out, allowing the GPU's Direct Memory Access (DMA) engine to access it without CPU intervention.

When dependencies exist between tasks in different streams (e.g., Kernel B requires the output of Kernel A), synchronization is required. This is achieved with **CUDA events**. An event is a marker that can be recorded in a stream after an operation completes. Another stream can then be instructed to wait for that event before beginning its own operations, thus establishing a correct "happens-before" relationship. For an operator-split solver with a dependency chain $\mathcal{K}_{c} \to \mathcal{K}_{\phi} \to \mathcal{K}_{T}$, this can be enforced by placing all three kernels in the same stream or by using events to link them across different streams. An independent memory copy $\mathcal{H}_{BC}$ can be placed in its own stream to run concurrently with this chain. 

#### Programming Models: CUDA, HIP, and SYCL

While CUDA is the native programming model for NVIDIA GPUs, the landscape of [heterogeneous computing](@entry_id:750240) includes other important models aimed at [performance portability](@entry_id:753342):
- **CUDA (Compute Unified Device Architecture)**: NVIDIA's proprietary C++-based platform. It provides direct, low-level access to the hardware features discussed, such as [shared memory](@entry_id:754741), warps, and streams.
- **HIP (Heterogeneous-Compute Interface for Portability)**: An open-source C++ runtime API from AMD that allows developers to write portable GPU code that can be compiled for both AMD and NVIDIA hardware. Its API closely mirrors CUDA's to facilitate porting.
- **SYCL**: A Khronos Group open standard for single-source C++ programming of heterogeneous systems. It is more abstract than CUDA/HIP, using concepts like queues, command groups, and accessors to manage computation and data on devices from various vendors.

For [bandwidth-bound](@entry_id:746659) kernels, well-optimized implementations in CUDA, HIP, and SYCL can achieve very similar performance on the same hardware, as they all compile down to the native machine code and are ultimately limited by the hardware's [memory bandwidth](@entry_id:751847). The choice often involves a trade-off between vendor-specific optimization and cross-platform portability. A key challenge in portability is handling hardware differences, such as the SIMT execution width (32-thread warps on NVIDIA vs. 32- or 64-thread wavefronts on AMD). Abstractions like **SYCL sub-groups** provide a portable way to write code that adapts to the native hardware's execution width, for example, when using collective communication primitives within a warp/[wavefront](@entry_id:197956). 

### Scaling to Multiple GPUs: Distributed Simulation

For battery pack simulations or very high-resolution cell models, a single GPU may not be sufficient. The problem must be distributed across multiple GPUs, typically within a single compute node or across a cluster.

#### Domain Decomposition and Halo Exchange

The standard approach for structured-grid problems is **geometric domain decomposition**. The global computational domain is partitioned into smaller, contiguous subdomains, with each subdomain assigned to a single GPU. Each GPU is responsible for advancing the solution within its local domain.

Since stencil computations at the boundary of a subdomain require data from neighboring subdomains, a communication step is necessary. This is handled by **[halo exchange](@entry_id:177547)** (or [ghost cell](@entry_id:749895) exchange). Each GPU allocates extra memory layers, known as halo or ghost layers, around its local domain. Before the computation step, each GPU sends its boundary data to its neighbors, who receive it and populate their halo layers. For an explicit stencil of radius $w$, a halo of width $w$ is required to correctly compute all interior points of the local domain. For instance, a thermal update with a nearest-neighbor stencil ($w_{\theta}=1$) needs a halo of width 1, while a higher-order concentration scheme ($w_{c}=2$) would require a halo of width 2. 

#### Strong vs. Weak Scaling

The performance of a distributed solver is evaluated using two primary metrics:
- **Strong Scaling**: The total problem size is held fixed, while the number of processors (GPUs), $P$, is increased. The goal is to solve the same problem faster. Ideal speedup is linear ($P \times$). The efficiency is calculated as $E_{strong} = \frac{T_1}{P \cdot T_P}$, where $T_1$ is the runtime on a single GPU. Strong scaling is often limited by the **[surface-to-volume ratio](@entry_id:177477)**. As more GPUs are added, each subdomain becomes smaller, and the ratio of communication (surface) to computation (volume) increases, reducing efficiency.
- **Weak Scaling**: The problem size *per processor* is held fixed. As more processors are added, the total problem size increases. The goal is to solve a larger problem in the same amount of time. Ideal [weak scaling](@entry_id:167061) maintains a constant runtime ($T_P = T_1$). The efficiency is calculated as $E_{weak} = \frac{T_1}{T_P}$.

These metrics are essential for understanding the [scalability](@entry_id:636611) and limitations of a parallel solver for large-scale battery pack simulations. 

### Advanced Numerical Considerations on GPUs

The unique characteristics of GPU hardware intersect deeply with numerical analysis, raising important questions about precision and reproducibility.

#### Floating-Point Precision and Mixed-Precision Solvers

Modern GPUs support various [floating-point](@entry_id:749453) formats, each offering a different balance of precision, range, and throughput:
- **FP64 (Double Precision)**: IEEE 754 standard with a 53-bit significand. Provides high precision, but typically has much lower throughput than lower precisions on consumer and data-center GPUs.
- **FP32 (Single Precision)**: IEEE 754 standard with a 24-bit significand. Offers a good balance of precision and high throughput.
- **TF32 (TensorFloat-32)**: An NVIDIA format that uses an FP32 8-bit exponent for range but only a 10-bit significand for multiply operations, offering throughput much higher than FP32.

Many electrochemical models involve [ill-conditioned linear systems](@entry_id:173639), where the solution is highly sensitive to perturbations. The **condition number** $\kappa(A)$ of a matrix $A$ measures this sensitivity. Solving a linear system $Ax=b$ using arithmetic with [unit roundoff](@entry_id:756332) $u$ (a measure of the precision, e.g., $u_{32} \approx 2^{-24}$ for FP32) can lead to a loss of up to $\log_{10}(\kappa(A))$ digits of accuracy.

This presents a dilemma: high-precision FP64 is often needed for [solver convergence](@entry_id:755051), but high-throughput FP32/TF32 is desired for speed. **Mixed-precision algorithms**, particularly [iterative refinement](@entry_id:167032) for linear systems, offer a solution. In this approach, an inner solver (e.g., GMRES) runs in fast, low precision (FP32), and an outer loop computes the residual and solution update in high precision (FP64). This method can converge to an FP64-accurate solution provided the condition number of the (preconditioned) matrix is not too large relative to the low-precision format. A [sufficient condition](@entry_id:276242) for convergence is $\kappa(A) \cdot u_{low}  1$.

For a challenging battery simulation where the preconditioned Jacobian has $\kappa(A) \approx 5 \times 10^6$, an FP32-based inner solve is viable because $\kappa(A) \cdot u_{32} \approx (5 \times 10^6) \cdot (6 \times 10^{-8}) \approx 0.3  1$. However, attempting to use TF32, with $u_{TF32} \approx 10^{-3}$, would fail dramatically, as $\kappa(A) \cdot u_{TF32} \approx 5000 \gg 1$. Furthermore, if the desired linear solver tolerance $\eta_k=10^{-4}$ is stricter than the arithmetic precision itself ($u_{TF32} \approx 10^{-3}$), the solver will fail to converge simply because it cannot represent the target accuracy. 

#### Numerical Determinism

For scientific validation, debugging, and regression testing, it is often critical that a simulation produces bitwise identical results from run to run given the same inputs. This is **numerical [determinism](@entry_id:158578)**. On a massively [parallel architecture](@entry_id:637629) like a GPU, achieving [determinism](@entry_id:158578) is non-trivial due to a fundamental property of [floating-point arithmetic](@entry_id:146236): it is **not associative**. That is, $(a+b)+c$ is not always equal to $a+(b+c)$ due to intermediate rounding errors.

The primary sources of [nondeterminism](@entry_id:273591) in GPU solvers are:
1.  **Parallel Reductions**: Operations like summing the squared residuals ($\sum w_i r_i^2$) involve each thread block computing a partial sum, followed by a reduction of these [partial sums](@entry_id:162077). The order in which [partial sums](@entry_id:162077) are combined can vary between runs due to the non-deterministic scheduling of thread blocks. This change in summation order leads to bitwise different results.
2.  **Atomic Operations**: Floating-point atomic additions (e.g., `atomicAdd`) are commonly used to accumulate values like heat sources into a global array from many threads. While atomics prevent race conditions by serializing updates to a memory location, the hardware does *not* guarantee the order of that serialization. A different order of additions leads to a different final result.

To ensure determinism, the order of all [floating-point operations](@entry_id:749454) must be fixed. This can be achieved by avoiding floating-point atomics and implementing reductions using a fixed, deterministic algorithm, such as a static tree-based reduction where the order of operations is explicitly defined. 