# Hi, I'm Sun Teng 👋

I'm an open-source contributor focused on **GPU/NPU compilers and heterogeneous runtimes**.

My recent work spans multiple layers of GPU/NPU compiler systems:

`IR analysis & transformation → code generation → JIT/runtime → on-device correctness & performance validation`

I enjoy working on compiler semantics, compilation and runtime systems, tensor computation, and heterogeneous execution.

## Technologies

- **Languages:** Rust, C++, Python, Java
- **Compiler:** MLIR, LLVM, Rust MIR, IR lowering and transformation, affine/indexing maps, NVPTX, AMDGPU
- **GPU Runtime:** CUDA Driver API, PTX/NVVM, CUDA streams, memory pools, JIT compilation, HIP/ROCm
- **Platforms:** NVIDIA GPU, Ascend NPU, AMD ROCm

## Looking for Opportunities

I'm currently exploring **full-time opportunities in GPU/NPU compiler engineering and heterogeneous runtime systems**.

I'm particularly interested in work involving:

- GPU/NPU compiler infrastructure
- MLIR / LLVM transformations and lowering
- GPU code generation and backend development
- JIT compilation and runtime systems
- Tensor compiler and hardware-aware optimization
- Open-source / upstream compiler development

Alongside my recent compiler and GPU/NPU open-source work, I have 7 years of prior Java backend engineering experience building production systems.

If your team is working on compiler infrastructure, GPU/NPU software, heterogeneous runtimes, or related open-source systems, I'd be happy to connect.

## Selected Open-Source Contributions

### [AscendNPU-IR](https://gitcode.com/Ascend/AscendNPU-IR)

An MLIR-based compiler infrastructure for Ascend NPU.

My contributions include:

- [CustomOp 1:2 TileAndBind](https://gitcode.com/Ascend/AscendNPU-IR/pull/1293): extended dimension analysis and slice propagation for `CustomOp` / `CustomMacroOp`, using `iterator_types` and `indexing_map` to derive tiled operands while preserving reduction semantics
- Added support for elementwise, broadcast, reduction, scalar-operand, and constrained multi-result cases, with conservative fallback for unsupported layouts, side effects, synchronization resources, and other unsafe cases
- Added memory-effect modeling for bufferized CustomOps to preserve execution ordering through compiler transformations
- Added MLIR/LIT and Ascend NPU E2E validation on **Ascend 910B2 / 950PR** hardware; **15 correctness cases passed**, and **6 Softmax performance cases achieved approximately 1.99× speedup** with 1:2 sub-block tiling

[E2E and performance validation — AscendNPU-IR-DT #88 →](https://gitcode.com/NPU-IR/AscendNPU-IR-DT/pull/88)

### [NVIDIA CUDA Rust](https://github.com/NVIDIA/cuda-rust)

#### cutile-rs

A Rust GPU DSL and asynchronous JIT runtime based on NVIDIA cuTile.

My contributions include:

- [Persistent Cubin cache](https://github.com/NVlabs/cutile-rs/pull/193) for content-addressed, cross-process JIT reuse, with atomic publication, integrity validation, eviction, and automatic recovery from invalid entries
  - Reduced GEMM preparation from **16.8 s to 98 ms** on `sm_89` and from **4.0 s to 54 ms** on `sm_120`
- [Single-flight Kernel Cache and Meta Tensor warmup](https://github.com/NVlabs/cutile-rs/pull/147), eliminating duplicate compilation for the same specialization and moving JIT cost out of the first production launch
  - Reduced a warmed first production launch from approximately **283 ms to 259 μs** on RTX 4090
- [Custom CUDA Memory Pool](https://github.com/NVlabs/cutile-rs/pull/96) with device ownership, asynchronous allocation, execution-context capture, and RAII lifetime management
- [Zero-copy Tensor views and reinterpretation](https://github.com/NVlabs/cutile-rs/pull/50) using shared storage ownership with shape, byte-size, contiguity, alignment, and aliasing validation
- [BF16 support](https://github.com/NVlabs/cutile-rs/pull/16) across the DSL, type system, and kernel execution path

#### cuda-oxide

A compiler that lowers Rust MIR directly to CUDA PTX.

My contributions include:

- Implemented Rust MIR `SetDiscriminant` lowering for direct-tag and niche-encoded enums while preserving Rust layout semantics on GPU
- Added 64-bit warp shuffle, `redux.sync`, lane-mask, and Hopper `elect.sync` intrinsics across the compiler pipeline
- Added LLVM `convergent` semantics for cooperative warp and barrier operations to prevent invalid compiler optimizations
- Added MIR, LLVM IR, and PTX code-generation tests for the new lowering and GPU primitives

[View my merged cuda-oxide PRs →](https://github.com/NVlabs/cuda-rust/pulls?q=is%3Apr+is%3Amerged+author%3Agoog00)

### [Prajna](https://github.com/prajna-lang/prajna)

A general-purpose programming language compiler with JIT and heterogeneous GPU support.

My contributions include:

- [LLVM-based NVPTX code generation #95](https://github.com/prajna-lang/prajna/pull/95): replaced the external `llc` invocation with LLVM `TargetMachine` APIs to generate PTX directly in-process
- [AMDGPU / ROCm backend #108](https://github.com/prajna-lang/prajna/pull/108): implemented the LLVM IR → AMDGPU object → HSACO compilation path and integrated HIP runtime loading and execution
- [Cross-platform GPU execution #144](https://github.com/prajna-lang/prajna/pull/144): separated host/device compilation paths and unified NVIDIA/AMD GPU kernel launch infrastructure
- Contributed IR/Codegen refactoring, tests, documentation, memory-lifetime fixes, and AMDGPU development environment support

[View my merged Prajna PRs →](https://github.com/prajna-lang/prajna/pulls?q=is%3Apr+is%3Amerged+author%3Agoog00)

### [Galois](https://github.com/galois-stack/galois)

A compilation framework for tensor computation and Tile-based programming.

My contributions include:

- [Hardware-aware GEMM tiling #85](https://github.com/galois-stack/galois/pull/85): derived cache- and SIMD-aware `MC`, `NC`, and `KC` blocking parameters using a BLIS-inspired model, improving FP32 single-core GEMM from **85–120 GFLOPS** to stable **130+ GFLOPS** on AMD Threadripper Pro 3955WX
- Contributed Visitor-based IR traversal, printing, and code-generation infrastructure across multiple compiler components
- Added IR ownership and memory-lifetime improvements, including fixes for cyclic references and allocation lifetime issues
- [Prefetch infrastructure #89](https://github.com/galois-stack/galois/pull/89): extended prefetch information through IR attributes, printing, and code generation
- Contributed parameterized tests, formatting, and CI infrastructure

[View my merged Galois PRs →](https://github.com/galois-stack/galois/pulls?q=is%3Apr+is%3Amerged+author%3Agoog00)

## Links

- Email: steng2009@163.com
- [GitHub](https://github.com/goog00)
- [GitCode](https://gitcode.com/sun_teng)
