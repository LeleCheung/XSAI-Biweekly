### XSAI

- Bug 修复
  - 同步昆明湖 V2 的 bug-fix（[XSAI #131](https://github.com/OpenXiangShan/XSAI/pull/131)、[XSAICache #9](https://github.com/OpenXiangShan/XSAICache/pull/9)）
  - 修复 MinimalMatrixConfig 下 AME 完成事件步长兼容性问题（[difftest #976](https://github.com/OpenXiangShan/difftest/pull/976)）
  - 修复隐式状态更新后 DiffTest CSR shadow 未失效的问题（[NEMU #1237](https://github.com/OpenXiangShan/NEMU/pull/1237)）
  - 支持大尺寸 zstd 镜像读取并完善镜像加载失败处理（[NEMU #1239](https://github.com/OpenXiangShan/NEMU/pull/1239)）
- RTL 新特性
  - 集成矩阵引导的 L2 预取器（[XSAI #124](https://github.com/OpenXiangShan/XSAI/pull/124)、[XSAICache #7](https://github.com/OpenXiangShan/XSAICache/pull/7)）
  - 基于双组缓冲实现独立的 TransposeLoadEngine，支持多通道转置加载（[CUTE #43](https://github.com/OpenXiangShan/CUTE/pull/43)、[XSAI #132](https://github.com/OpenXiangShan/XSAI/pull/132)）
- 调试工具
  - 支持矩阵结果 hash 上报与 DiffTest 比较（[CUTE #45](https://github.com/OpenXiangShan/CUTE/pull/45)、[difftest #978](https://github.com/OpenXiangShan/difftest/pull/978)、[NEMU #1238](https://github.com/OpenXiangShan/NEMU/pull/1238)、[XSAI #133](https://github.com/OpenXiangShan/XSAI/pull/133)）
