# XSAI Biweekly 100-108 Extracts

XSAI content extracted from the Chinese and English XiangShan Biweekly posts. Chinese is the source of truth. The scope is the dedicated `## XSAI` section in issue 100 and the `### XSAI` subsection in issues 101-108.

Source repository: `XiangShan-doc/docs/blog/posts/`. Extracted on 2026-08-14 from the local `master` branch, whose release commits are recorded in the writing notes. The two image paths from issue 100 are adjusted only so they render from `workplace/`; all other Markdown content is preserved.

## Biweekly 100 (20260413)

### 中文

#### XSAI

如果大家还记得，我们在 2025 年 RISC-V 中国峰会上有过 XSAI 的专题介绍（[《XSAI：以 CPU 的编程范式支持现代 LLM 核函数》](https://github.com/OpenXiangShan/Talks-and-Publications/blob/master/slides/20250716%260718-RVSC-XSAI%EF%BC%9A%E4%BB%A5CPU%E7%9A%84%E7%BC%96%E7%A8%8B%E8%8C%83%E5%BC%8F%E6%94%AF%E6%8C%81%E7%8E%B0%E4%BB%A3LLM%E6%A0%B8%E5%87%BD%E6%95%B0.pdf)），现在的 XSAI 正是这一报告持续演进的结果。

![XSAI architecture](../../../XiangShan-doc/docs/blog/posts/figs/biweekly-100/XSAI.png)

目前 XSAI 基于昆明湖 V2R2 开发，型号名称是昆明湖 V2R2A。相比昆明湖 V2R2，昆明湖 V2R2A 将会在以下几个方面新增特性：

- 向量：XSAI 的向量单元将积极支持 AI 常用的低精度数据类型以及特殊函数。V2R2A 计划支持 bf16 以及 fp8 数据类型，并且支持 exp2 运算以加速大模型中的 softmax。
- 矩阵：XSAI 的矩阵模块受昆明湖核的控制，直接与 L2 缓存交互，存取矩阵数据。V2R2A 的矩阵模块仍在迭代中，最终将会支持 bf16/fp8/int8 矩阵乘加运算。未来的 XSAI 还会支持 mxfp8/mxfp4 等数据类型。矩阵模块的指令大多属于异步指令，能够与昆明湖核内的向量运算同时执行，从而达到更高的算力利用率。
- 缓存：XSAI 面向矩阵计算与高性能 CPU 协同场景，引入了高带宽 L2 缓存（HBL2）设计。HBL2 的目标参数为 1-2MB 的容量以及 256-512 Bytes/cycle 的带宽。针对 coherent cache 与 GEMM 并行运行时的一致性开销，XSAI 进一步采用更贴合矩阵数据流的访问语义与权限策略，从而提高带宽的利用率。

XSAI 组近期进行了一些初步测试，这些测试意在验证 XSAI 的通算、智算功能。

我们使用 SPEC CPU 2006 测试 XSAI 的通算功能。本次测试使用的 checkpoint、处理器参数以及 SoC 参数与香山双周报 91 一致。

| SPECint 2006 @ 3GHz. | V2R2A  |  V2R2  | SPECfp 2006 @ 3GHz | V2R2A | V2R2  |
| :------------------- | :----: | :----: | :----------------- | :---: | :---: |
| 400.perlbench        | 36.03  | 36.18  | 410.bwaves         | 67.35 | 66.73 |
| 401.bzip2            | 25.75  | 25.46  | 416.gamess         | 40.61 | 40.99 |
| 403.gcc              | 48.15  | 48.00  | 433.milc           | 44.38 | 45.12 |
| 429.mcf              | 63.26  | 60.63  | 434.zeusmp         | 51.65 | 51.61 |
| 445.gobmk            | 30.30  | 30.32  | 435.gromacs        | 33.50 | 33.60 |
| 456.hmmer            | 41.35  | 41.62  | 436.cactusADM      | 46.06 | 46.19 |
| 458.sjeng            | 30.25  | 30.24  | 437.leslie3d       | 48.31 | 47.97 |
| 462.libquantum       | 126.54 | 122.43 | 444.namd           | 28.82 | 28.86 |
| 464.h264ref          | 56.49  | 56.58  | 447.dealII         | 73.37 | 73.55 |
| 471.omnetpp          | 42.32  | 41.77  | 450.soplex         | 52.85 | 52.50 |
| 473.astar            | 29.23  | 29.19  | 453.povray         | 53.05 | 53.46 |
| 483.xalancbmk        | 71.39  | 72.84  | 454.Calculix       | 16.35 | 16.37 |
| GEOMEAN              | 44.92  | 44.66  | 459.GemsFDTD       | 38.31 | 38.60 |
|                      |        |        | 465.tonto          | 36.65 | 36.66 |
|                      |        |        | 470.lbm            | 91.30 | 91.94 |
|                      |        |        | 481.wrf            | 40.25 | 40.70 |
|                      |        |        | 482.sphinx3        | 48.88 | 49.13 |
|                      |        |        | GEOMEAN            | 44.72 | 44.85 |

> 解读：V2R2A 频率 3GHz 仅代表仿真设置，该设置与 V2R2 的仿真对齐，以确认 XSAI 的修改没有导致性能显著倒退。我们预期的 XSAI 频率低于 3GHz。在通算场景下，导致性能差异的因素是高带宽 L2 的架构设计以及缓存替换算法的改变。上述测试结果表明，XSAI 对香山的修改没有显著影响香山原有的通算功能与性能。

在智算测试方面，我们在 XCVU19p FPGA 上，使用经过裁剪的 V2R2A 运行了 Llama-2 15M 模型的推理。XSAI 频率 50MHz，矩阵 int8 算力 4Tops/GHz，内存 DDR4-2400。测试得到的 Prefill/Decode 阶段性能分别是 343.61 toks/s 与 36.24 toks/s，输出符合预期。

![XSAI FPGA test](../../../XiangShan-doc/docs/blog/posts/figs/biweekly-100/XSAI-fpga.png)

> 解读：测试使用的内存频率为 2400MT/s，而 XSAI 的频率为 50MHz，利用 50MHz 的数据推算 2GHz 下的数据，会存在等效内存频率偏高的问题。从这方面来讲，本次测试的结果偏乐观。但是 V2R2A 为了部署在 XCVU19p 上做了不少裁剪，对性能不利，从这方面来讲，本次测试的结果又是偏悲观的。因此，本次测试仅作为功能方面的原型测试，证明 XSAI 在功能上支持大模型推理。

### English

#### XSAI

If you still remember, we presented a dedicated XSAI talk at the 2025 RISC-V China Summit ([XSAI(ξ): Hardware Support for Modern LLM Kernels in a CPU Paradigm](https://github.com/OpenXiangShan/Talks-and-Publications/blob/master/slides/20250716%260718-RVSC-XSAI%EF%BC%9A%E4%BB%A5CPU%E7%9A%84%E7%BC%96%E7%A8%8B%E8%8C%83%E5%BC%8F%E6%94%AF%E6%8C%81%E7%8E%B0%E4%BB%A3LLM%E6%A0%B8%E5%87%BD%E6%95%B0.pdf)); the current XSAI is the ongoing evolution of that work.

![XSAI architecture](../../../XiangShan-doc/docs/blog/posts/figs/biweekly-100/XSAI.png)

XSAI is currently developed on Kunming Lake V2R2, under the name Kunming Lake V2R2A. Compared with Kunming Lake V2R2, Kunming Lake V2R2A introduces the following features:

- Vector: The XSAI vector unit will support low-precision data types and special functions commonly used in AI workloads. V2R2A plans to support bf16 and fp8 data types, and also supports exp2 to accelerate softmax in LLMs.
- Matrix: The XSAI matrix unit is controlled by the Kunminghu core and directly interacts with the L2 cache to load/store matrix data. The V2R2A matrix unit is still under iteration and is expected to finally support bf16/fp8/int8 matrix multiply-accumulate operations. Future XSAI versions will also support data types such as mxfp8/mxfp4. Most matrix instructions are asynchronous and can execute in parallel with vector operations in the Kunminghu core, improving compute utilization.
- Cache: For matrix-compute and high-performance CPU co-execution scenarios, XSAI introduces a high-bandwidth L2 cache (HBL2). The HBL2 target parameters are 1-2MB capacity and 256-512 Bytes/cycle bandwidth. To reduce coherence overhead when coherent cache and GEMM run in parallel, XSAI further adopts access semantics and permission policies that better match matrix dataflow, thereby improving bandwidth utilization.

The XSAI group has recently run preliminary tests aimed at validating XSAI’s general-purpose and AI compute capabilities. This issue reports those test results to readers of the biweekly.

We used SPEC CPU 2006 to evaluate XSAI’s general-purpose compute capability. The checkpoints, processor parameters, and SoC parameters for this run match those in XiangShan Biweekly 91.

| SPECint 2006 @ 3GHz | V2R2A  |  V2R2  | SPECfp 2006 @ 3GHz | V2R2A | V2R2  |
| :------------------ | :----: | :----: | :----------------- | :---: | :---: |
| 400.perlbench       | 36.03  | 36.18  | 410.bwaves         | 67.35 | 66.73 |
| 401.bzip2           | 25.75  | 25.46  | 416.gamess         | 40.61 | 40.99 |
| 403.gcc             | 48.15  | 48.00  | 433.milc           | 44.38 | 45.12 |
| 429.mcf             | 63.26  | 60.63  | 434.zeusmp         | 51.65 | 51.61 |
| 445.gobmk           | 30.30  | 30.32  | 435.gromacs        | 33.50 | 33.60 |
| 456.hmmer           | 41.35  | 41.62  | 436.cactusADM      | 46.06 | 46.19 |
| 458.sjeng           | 30.25  | 30.24  | 437.leslie3d       | 48.31 | 47.97 |
| 462.libquantum      | 126.54 | 122.43 | 444.namd           | 28.82 | 28.86 |
| 464.h264ref          | 56.49  | 56.58  | 447.dealII         | 73.37 | 73.55 |
| 471.omnetpp          | 42.32  | 41.77  | 450.soplex         | 52.85 | 52.50 |
| 473.astar            | 29.23  | 29.19  | 453.povray         | 53.05 | 53.46 |
| 483.xalancbmk        | 71.39  | 72.84  | 454.Calculix       | 16.35 | 16.37 |
| GEOMEAN              | 44.92  | 44.66  | 459.GemsFDTD       | 38.31 | 38.60 |
|                      |        |        | 465.tonto          | 36.65 | 36.66 |
|                      |        |        | 470.lbm            | 91.30 | 91.94 |
|                      |        |        | 481.wrf            | 40.25 | 40.70 |
|                      |        |        | 482.sphinx3        | 48.88 | 49.13 |
|                      |        |        | GEOMEAN            | 44.72 | 44.85 |

> **Takeaway:** The 3GHz V2R2A frequency is only a simulation setting, chosen to match V2R2 simulation and check that XSAI changes do not cause large performance regressions. We expect XSAI silicon to run below 3GHz. For general-purpose workloads, differences mainly come from the high-bandwidth L2 design and changes to the cache replacement policy. Overall, these results suggest XSAI’s changes do not materially affect XiangShan’s baseline general-purpose behavior or performance.

For AI inference, we ran Llama-2 15M on an XCVU19p FPGA using a trimmed V2R2A. XSAI ran at 50MHz, matrix int8 throughput is 4 TOPS/GHz, memory DDR4-2400. Measured Prefill and Decode throughput were 343.61 tok/s and 36.24 tok/s respectively; outputs matched expectations.

![XSAI FPGA test](../../../XiangShan-doc/docs/blog/posts/figs/biweekly-100/XSAI-fpga.png)

> **Takeaway:** The memory frequency used in the test is 2400MT/s, while XSAI’s frequency is 50MHz, so extrapolating data at 50MHz to 2GHz would lead to an overly optimistic effective memory frequency. However, V2R2A has been heavily trimmed to fit on the XCVU19p, which hurts performance, making the results pessimistic. Therefore, this test serves only as a functional prototype test, demonstrating that XSAI supports LLM inference in terms of functionality.

## Biweekly 101 (20260427)

### 中文

#### XSAI

- RTL 新特性
  - 正在测试矩阵模块的 FP8 精度支持
  - 正在评估矩阵模块的 8 通道访存
  - 正在与后端组配合实现 BF16 标量与向量
- 代码质量
  - 优化了 XSAI 的参数系统（[XSAI #59](https://github.com/OpenXiangShan/XSAI/pull/59)）
- 调试工具
  - NEMU 新增 BF16 扩展支持（[NEMU #995](https://github.com/OpenXiangShan/NEMU/pull/995)）
  - HBL2 测试兼容多核环境

### English

#### XSAI

- RTL New features
  - Testing FP8 precision support in the matrix unit
  - Evaluating 8-channel cache access for the matrix unit
  - Co-developing BF16 scalar and vector support with the backend team
- Code quality
  - Optimized the XSAI parameter system ([XSAI #59](https://github.com/OpenXiangShan/XSAI/pull/59))
- Debugging tools
  - Added BF16 extension support in NEMU ([NEMU #995](https://github.com/OpenXiangShan/NEMU/pull/995))
  - HBL2 tests are now compatible with multi-core environments

## Biweekly 102 (20260511)

### 中文

#### XSAI

- RTL 新特性
  - 矩阵模块支持 FP8 精度（[XSAI #61](https://github.com/OpenXiangShan/XSAI/pull/61)）
  - 正在评估矩阵模块的 8 通道访存
  - 正在与后端组配合实现 BF16 标量与向量
- Bug 修复
  - 修复 CUTE 的一处调度错误（[XSAI #62](https://github.com/OpenXiangShan/XSAI/pull/62)）
- 代码质量
  - 添加 Makefile 对 CUTE 代码更改的跟踪（[XSAI #63](https://github.com/OpenXiangShan/XSAI/pull/63)）
  - firmware 编译加速（[xsai-env #4](https://github.com/OurCompArchGroup/xsai-env/pull/4)）
- 评估工具
  - checkpoint 并行仿真（[xsai-env #11](https://github.com/OurCompArchGroup/xsai-env/pull/11)）

### English

#### XSAI

- RTL features
  - The matrix unit supports FP8 precision ([XSAI #61](https://github.com/OpenXiangShan/XSAI/pull/61))
  - Evaluating 8-channel memory access for the matrix unit
  - Working with the backend team to implement BF16 scalar and vector support
- Bug fixes
  - Fixed a scheduling error in CUTE ([XSAI #62](https://github.com/OpenXiangShan/XSAI/pull/62))
- Code quality
  - Added Makefile tracking for changes in CUTE code ([XSAI #63](https://github.com/OpenXiangShan/XSAI/pull/63))
  - Accelerated firmware compilation ([xsai-env #4](https://github.com/OurCompArchGroup/xsai-env/pull/4))
- Evaluation tools
  - Parallel checkpoint simulation ([xsai-env #11](https://github.com/OurCompArchGroup/xsai-env/pull/11))

## Biweekly 103 (20260525)

### 中文

#### XSAI

- RTL 新特性
  - 拆分 C 矩阵访存模块的 load 与 store，使两种指令能够重叠执行（[CUTE #11](https://github.com/OpenXiangShan/CUTE/pull/11)）
- Bug 修复
  - 修复 XSAI 向 XSAI DiffTest 传递的错误常量（[XSAI #65](https://github.com/OpenXiangShan/XSAI/pull/65)）
  - 修复 HBL2 的 A 通道 Put Matrix 被 C 通道打断的错误（[XSAI #64](https://github.com/OpenXiangShan/XSAI/pull/64)）
- 代码质量
  - 加速 XSAI FIR elaboration，使 XSAI 生成 Verilog 的速度提高到原来的 4.75 倍（[CUTE #12](https://github.com/OpenXiangShan/CUTE/pull/12)）

### English

#### XSAI

- RTL features
  - Split load and store in the C matrix memory access module so that the two instruction types can overlap ([CUTE #11](https://github.com/OpenXiangShan/CUTE/pull/11))
- Bug fixes
  - Fixed an incorrect constant passed from XSAI to XSAI DiffTest ([XSAI #65](https://github.com/OpenXiangShan/XSAI/pull/65))
  - Fixed the issue where HBL2 A-channel Put Matrix was interrupted by the C channel ([XSAI #64](https://github.com/OpenXiangShan/XSAI/pull/64))
- Code quality
  - Accelerated XSAI FIR elaboration, making XSAI Verilog generation 4.75x faster than before ([CUTE #12](https://github.com/OpenXiangShan/CUTE/pull/12))

## Biweekly 104 (20260608)

### 中文

#### XSAI

- RTL 新特性
  - 添加用于关闭 mxfp8 等带缩放因子数据类型的选项，在关闭这些数据类型后，处理缩放因子的模块将不会被实例化（[CUTE #13](https://github.com/OpenXiangShan/CUTE/pull/13)）
  - 为 CUTE 添加一系列矩阵性能事件（[CUTE #18](https://github.com/OpenXiangShan/CUTE/pull/18)）
  - 正在推进 HBL2 对 CHI 总线协议的支持
- Bug 修复
  - 修复 XSAI V2R2A 的性能事件编号，与昆明湖 V2R2 的事件编号对齐（[XSAI #70](https://github.com/OpenXiangShan/XSAI/pull/70)）
  - 修复矩阵功能单元异常未被 ROB 处理的问题（[XSAI #71](https://github.com/OpenXiangShan/XSAI/pull/71)）
- 代码重构
  - 重构 CUTE 调度（[CUTE #14](https://github.com/OpenXiangShan/CUTE/pull/14)）

### English

#### XSAI

- RTL features
  - Add an option to disable data types with scaling factors, such as mxfp8. When these data types are disabled, modules that handle scaling factors will not be instantiated ([CUTE #13](https://github.com/OpenXiangShan/CUTE/pull/13))
  - Add a set of matrix performance events for CUTE ([CUTE #18](https://github.com/OpenXiangShan/CUTE/pull/18))
  - Continue advancing HBL2 support for the CHI bus protocol
- Bug fixes
  - Fix the performance event numbers of XSAI V2R2A and align them with the event numbers of Kunminghu V2R2 ([XSAI #70](https://github.com/OpenXiangShan/XSAI/pull/70))
  - Fix the issue where matrix functional unit exceptions were not handled by ROB ([XSAI #71](https://github.com/OpenXiangShan/XSAI/pull/71))
- Code refactoring
  - Refactor CUTE scheduling ([CUTE #14](https://github.com/OpenXiangShan/CUTE/pull/14))

## Biweekly 105 (20260623)

### 中文

#### XSAI

- RTL 新特性
  - 支持 RISC-V BF16 扩展（[XSAI #72](https://github.com/OpenXiangShan/XSAI/pull/72)）
  - 缩放因子存储改用香山的 SRAMTemplate，与香山统一（[CUTE #20](https://github.com/OpenXiangShan/CUTE/pull/20)）
  - 实现 TL-TL 与 TL-CHI 的 PutFullData（[HBL2 #3](https://github.com/OpenXiangShan/HBL2/pull/3)）

### English

#### XSAI

- RTL features
  - Support the RISC-V BF16 extension ([XSAI #72](https://github.com/OpenXiangShan/XSAI/pull/72))
  - Switch scaling factor storage to XiangShan's SRAMTemplate for consistency with XiangShan ([CUTE #20](https://github.com/OpenXiangShan/CUTE/pull/20))
  - Implement PutFullData for TL-TL and TL-CHI ([HBL2 #3](https://github.com/OpenXiangShan/HBL2/pull/3))

## Biweekly 106 (20260706)

### 中文

#### XSAI

- Bug 修复
  - 修复了 MMA 指令在 mtilen 过大时漏报非法指令异常的错误（[XSAI #79](https://github.com/OpenXiangShan/XSAI/pull/79)）
- RTL 新特性
  - 支持细粒度矩阵访存以及 8bit 元素的转置访存（[CUTE #19](https://github.com/OpenXiangShan/CUTE/pull/19)）
  - 指令扩展更新至 XSAI proposal 12（[XSAI #68](https://github.com/OpenXiangShan/XSAI/pull/68)）
- 代码质量
  - 重构 CUTE FPE 代码，拆分文件，清除符号链接（[XSAI #81](https://github.com/OpenXiangShan/XSAI/pull/81)）
- 调试工具
  - 将 DiffTest 中的 C++17 写法回退到 C++11，以增强兼容性（[XSAI #75](https://github.com/OpenXiangShan/XSAI/pull/75)）

### English

#### XSAI

- Bug fixes
  - Fixed the issue where MMA instructions missed illegal-instruction exceptions when `mtilen` was too large ([XSAI #79](https://github.com/OpenXiangShan/XSAI/pull/79))
- RTL features
  - Support fine-grained matrix memory access and transposed memory access for 8-bit elements ([CUTE #19](https://github.com/OpenXiangShan/CUTE/pull/19))
  - Update the instruction extension to XSAI proposal 12 ([XSAI #68](https://github.com/OpenXiangShan/XSAI/pull/68))
- Code quality
  - Refactor CUTE FPE code, split files, and remove symbolic links ([XSAI #81](https://github.com/OpenXiangShan/XSAI/pull/81))
- Debugging tools
  - Revert C++17 constructs in DiffTest to C++11 to improve compatibility ([XSAI #75](https://github.com/OpenXiangShan/XSAI/pull/75))

## Biweekly 107 (20260720)

### 中文

#### XSAI

- Bug 修复
  - 修复了 load/store whole C 指令的控制信号（[XSAI #86](https://github.com/OpenXiangShan/XSAI/pull/86)）
- RTL 新特性
  - 可配置的 CUTE 多通道访存（[XSAI #83](https://github.com/OpenXiangShan/XSAI/pull/83)）
  - 缓存系统使用 XSAICache 仓库替代原有的 coupledL2/huancun/openLLC（[XSAI #85](https://github.com/OpenXiangShan/XSAI/pull/85)）
- 代码质量
  - 对近期 CUTE 新增的调试输出添加控制开关（[CUTE #24](https://github.com/OpenXiangShan/CUTE/pull/24)、[CUTE #27](https://github.com/OpenXiangShan/CUTE/pull/27)）
- 调试工具
  - uop 的生命周期 trace 分析（[XSAI #84](https://github.com/OpenXiangShan/XSAI/pull/84)）

### English

#### XSAI

- Bug fixes
  - Fix the control signals for load/store whole C instructions ([XSAI #86](https://github.com/OpenXiangShan/XSAI/pull/86))
- RTL features
  - Support configurable multi-channel memory access in CUTE ([XSAI #83](https://github.com/OpenXiangShan/CUTE/pull/83))
  - Replace coupledL2/huancun/openLLC with the XSAICache repository for the cache system ([XSAI #85](https://github.com/OpenXiangShan/XSAI/pull/85))
- Code quality
  - Add switches to control recently added debug output in CUTE ([CUTE #24](https://github.com/OpenXiangShan/CUTE/pull/24), [CUTE #27](https://github.com/OpenXiangShan/CUTE/pull/27))
- Debugging tools
  - Analyze the lifecycle of a uop using traces ([XSAI #84](https://github.com/OpenXiangShan/XSAI/pull/84))

## Biweekly 108 (20260803)

### 中文

#### XSAI

- RTL 新特性
  - AME 版本更新至 XSAI AME proposal 14（[XSAI #77](https://github.com/OpenXiangShan/XSAI/pull/77)）
  - ZhuJiang LLC 的集成支持（[XSAI #91](https://github.com/OpenXiangShan/XSAI/pull/91)）
- Bug 修复
  - 修复了 mcsr 的别名 CSR 读写错误（[XSAI #98](https://github.com/OpenXiangShan/XSAI/pull/98)）
  - 修复 AmuCtrlBuffer 的 redirect 逻辑，与 ROB 对齐（[XSAI #99](https://github.com/OpenXiangShan/XSAI/pull/99)）
  - 修复 AmuCtrlBuffer 内部 PriorityEncoder 的未定义行为（[XSAI #100](https://github.com/OpenXiangShan/XSAI/pull/100)）
  - 修复 LSQ 对于缓冲溢出的过于严格的断言检查（[XSAI #101](https://github.com/OpenXiangShan/XSAI/pull/101)）
  - 修复 mfence 指令未阻塞后续指令导致的死锁（[XSAI #102](https://github.com/OpenXiangShan/XSAI/pull/102)）
- 代码质量
  - CUTE 提供 msync 数量配置接口（[XSAI #95](https://github.com/OpenXiangShan/XSAI/pull/95)）（[CUTE #34](https://github.com/OpenXiangShan/CUTE/pull/34)）
  - 移除冗余的 mtilem/n/k 重置逻辑（[XSAI #97](https://github.com/OpenXiangShan/XSAI/pull/97)）

### English

#### XSAI

- RTL features
  - Update the AME version to XSAI AME proposal 14 ([XSAI #77](https://github.com/OpenXiangShan/XSAI/pull/77))
  - Integrate ZhuJiang LLC ([XSAI #91](https://github.com/OpenXiangShan/XSAI/pull/91))
- Bug fixes
  - Fix read and write errors for mcsr alias CSRs ([XSAI #98](https://github.com/OpenXiangShan/XSAI/pull/98))
  - Fix the redirect logic in AmuCtrlBuffer to align with the ROB ([XSAI #99](https://github.com/OpenXiangShan/XSAI/pull/99))
  - Fix undefined behavior of the PriorityEncoder inside AmuCtrlBuffer ([XSAI #100](https://github.com/OpenXiangShan/XSAI/pull/100))
  - Relax overly strict assertion checks for buffer overflow in the LSQ ([XSAI #101](https://github.com/OpenXiangShan/XSAI/pull/101))
  - Fix a deadlock caused by `mfence` not blocking subsequent instructions ([XSAI #102](https://github.com/OpenXiangShan/XSAI/pull/102))
- Code quality
  - Provide a configurable msync count interface in CUTE ([XSAI #95](https://github.com/OpenXiangShan/XSAI/pull/95), [CUTE #34](https://github.com/OpenXiangShan/CUTE/pull/34))
  - Remove redundant mtilem/n/k reset logic ([XSAI #97](https://github.com/OpenXiangShan/XSAI/pull/97))
