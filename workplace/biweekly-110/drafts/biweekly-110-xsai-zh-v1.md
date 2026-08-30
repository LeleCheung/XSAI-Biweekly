### XSAI

- Bug 修复
  - 修复 MLCT/MSCT 转置访存的数据布局和 MatrixReg 地址（[XSAI #106](https://github.com/OpenXiangShan/XSAI/pull/106)、[CUTE #38](https://github.com/OpenXiangShan/CUTE/pull/38)）
  - 修复矩阵 `AccessAckData` 与 HintQueue 状态不同步问题（[XSAI #110](https://github.com/OpenXiangShan/XSAI/pull/110)、[XSAICache #6](https://github.com/OpenXiangShan/XSAICache/pull/6)）
  - 修复 Mx 操作数延迟写回漏唤醒导致 MLS 指令阻塞的问题（[XSAI #111](https://github.com/OpenXiangShan/XSAI/pull/111)）
- 代码质量
  - 清理未使用的矩阵提交和调度反馈接口（[XSAI #113](https://github.com/OpenXiangShan/XSAI/pull/113)）
  - 并行化 EMU 和 nightly 回归（[XSAI #114](https://github.com/OpenXiangShan/XSAI/pull/114)、[XSAI #116](https://github.com/OpenXiangShan/XSAI/pull/116)）
- 调试工具
  - DiffTest 支持 AME `mcfg` 状态对比（[XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107)、[difftest #944](https://github.com/OpenXiangShan/difftest/pull/944)）
  - 支持 16-byte store checker 事件（[XSAI #112](https://github.com/OpenXiangShan/XSAI/pull/112)）
  - 改进 MMA 验证失败处理和 AMU 事件诊断（[difftest #926](https://github.com/OpenXiangShan/difftest/pull/926)、[difftest #927](https://github.com/OpenXiangShan/difftest/pull/927)）
