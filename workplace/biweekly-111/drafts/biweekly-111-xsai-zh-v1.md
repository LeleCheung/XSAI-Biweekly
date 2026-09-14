### XSAI

- RTL 新特性
  - 为 CUTE 访存请求传递矩阵预取描述信息（[CUTE #39](https://github.com/OpenXiangShan/CUTE/pull/39)）
- Bug 修复
  - 同步昆明湖 V2 的 bug-fix（[XSAI #123](https://github.com/OpenXiangShan/XSAI/pull/123)）
  - 同步昆明湖 V2 的 bug-fix（[XSAI #129](https://github.com/OpenXiangShan/XSAI/pull/129)）
  - 修复预取 RequestBuffer 活锁（[XSAI #126](https://github.com/OpenXiangShan/XSAI/pull/126)、[XSAICache #8](https://github.com/OpenXiangShan/XSAICache/pull/8)）
- 代码质量
  - 更新 nightly 回归 checkpoint 池并固定 matrix jobs 使用 node runner（[XSAI #120](https://github.com/OpenXiangShan/XSAI/pull/120)、[XSAI #122](https://github.com/OpenXiangShan/XSAI/pull/122)）
- 调试工具
  - 完善 AME DiffTest 的 `mrelease` 退休与旧 `mstore` 顺序检查（[XSAI #121](https://github.com/OpenXiangShan/XSAI/pull/121)、[difftest #953](https://github.com/OpenXiangShan/difftest/pull/953)、[XSAI #128](https://github.com/OpenXiangShan/XSAI/pull/128)、[difftest #958](https://github.com/OpenXiangShan/difftest/pull/958)）
  - 为 AME 错误路径记录正确的指令 PC（[XSAI #121](https://github.com/OpenXiangShan/XSAI/pull/121)、[difftest #955](https://github.com/OpenXiangShan/difftest/pull/955)）
  - 优化 NEMU 浮点 MMACC 参考模型并完善 BF16 路径（[NEMU #1189](https://github.com/OpenXiangShan/NEMU/pull/1189)、[NEMU #1197](https://github.com/OpenXiangShan/NEMU/pull/1197)、[NEMU #1200](https://github.com/OpenXiangShan/NEMU/pull/1200)）
