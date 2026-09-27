### XSAI

- 代码质量
  - 将 CI nightly 随机回归切换至 RVA23 无向量 SPEC checkpoint 池（[XSAI #130](https://github.com/OpenXiangShan/XSAI/pull/130)）
- 调试工具
  - 增加 CUTE 与 L2 联合测试顶层，并提供写请求观测接口（[CUTE #40](https://github.com/OpenXiangShan/CUTE/pull/40)、[CUTE #41](https://github.com/OpenXiangShan/CUTE/pull/41)）
  - 完善 NEMU 的 CUTE 控制模式回调与矩阵同步支持（[NEMU #1225](https://github.com/OpenXiangShan/NEMU/pull/1225)）
  - 修复 DiffTest batch 模式下 AME 事件结构体与 NEMU 的布局不一致问题（[difftest #962](https://github.com/OpenXiangShan/difftest/pull/962)）
  - 修复 CUTE DiffTest 事件的 `coreid` 与 PC 采样问题（[CUTE #42](https://github.com/OpenXiangShan/CUTE/pull/42)）
  - 限制 NEMU 矩阵加载结果的对比范围，避免未写入区域引发误报（[NEMU #1217](https://github.com/OpenXiangShan/NEMU/pull/1217)）
  - 为 NEMU 增加矩阵访存同步缺失与矩阵寄存器未定义区域读取检查（[NEMU #1212](https://github.com/OpenXiangShan/NEMU/pull/1212)、[NEMU #1224](https://github.com/OpenXiangShan/NEMU/pull/1224)）
