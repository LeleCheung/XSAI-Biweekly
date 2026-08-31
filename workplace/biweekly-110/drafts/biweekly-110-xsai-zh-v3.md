### XSAI

- Bug 修复
  - 修复 MLCT 转置数据布局和 MSC/MSCT 的 C MatrixReg 读地址（[XSAI #106](https://github.com/OpenXiangShan/XSAI/pull/106)、[CUTE #38](https://github.com/OpenXiangShan/CUTE/pull/38)）
  - 修复 `msetcfg`/`mgetcfg` 误译码（[XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107)）
  - 修复矩阵访存 `AccessAckData` 响应与 HintQueue 状态不同步问题（[XSAI #110](https://github.com/OpenXiangShan/XSAI/pull/110)、[XSAICache #6](https://github.com/OpenXiangShan/XSAICache/pull/6)）
  - 修复 Mx 操作数延迟写回漏唤醒导致 MLS 指令永久阻塞的问题（[XSAI #111](https://github.com/OpenXiangShan/XSAI/pull/111)）
- 代码质量
  - 清理未使用的矩阵提交和调度反馈接口（[XSAI #113](https://github.com/OpenXiangShan/XSAI/pull/113)）
  - 优化 CI：并行化 EMU 与 nightly 回归（[XSAI #114](https://github.com/OpenXiangShan/XSAI/pull/114)、[XSAI #116](https://github.com/OpenXiangShan/XSAI/pull/116)）
- 调试工具
  - DiffTest 支持 AME `mcfg` 状态对比（[XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107)、[difftest #944](https://github.com/OpenXiangShan/difftest/pull/944)、[NEMU #1172](https://github.com/OpenXiangShan/NEMU/pull/1172)）
  - 支持 16-byte store checker 事件（[XSAI #112](https://github.com/OpenXiangShan/XSAI/pull/112)）
  - 处理 MMA 操作数获取失败，并改进 AMU 事件诊断（[difftest #926](https://github.com/OpenXiangShan/difftest/pull/926)、[difftest #927](https://github.com/OpenXiangShan/difftest/pull/927)）
