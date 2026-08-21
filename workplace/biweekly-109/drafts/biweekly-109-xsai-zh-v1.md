### XSAI

- RTL 新特性
  - 支持 tile register 的 e8/e16/e32 多精度转置 load（[CUTE #35](https://github.com/OpenXiangShan/CUTE/pull/35)）
- Bug 修复
  - 修复多通道 CUTE 的 DiffTest 支持并优化面积（[XSAI #93](https://github.com/OpenXiangShan/XSAI/pull/93)、[CUTE #33](https://github.com/OpenXiangShan/CUTE/pull/33)）
- 调试工具
  - 在 DiffTest 中实现 MMA batching，减少 kernel launch 次数（[difftest #920](https://github.com/OpenXiangShan/difftest/pull/920)）
  - 实现反压，避免 MMA backend 吞吐不足时队列无限增长（[difftest #923](https://github.com/OpenXiangShan/difftest/pull/923)）
