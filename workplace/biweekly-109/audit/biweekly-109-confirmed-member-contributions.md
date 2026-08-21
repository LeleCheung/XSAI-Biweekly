# Biweekly 109 XSAI 确认组员贡献梳理

## 口径

- 已确认组员账号：`Wonicon`、`ecall73`、`yu-yake2002`。
- 查询仓库：XSAI、CUTE、difftest。
- 时间范围：2026-07-27 至 2026-08-15 的已合入 PR。已排除 Biweekly 108 明确报道的 XSAI #77 和 #102。
- 只列出上述账号的贡献；没有符合条件的仓库不单列说明。

## XSAI

- Wonicon：修复多通道 CUTE 的 DiffTest 支持并优化面积。矩阵 store event 仅在 RTL 采集请求/响应信息，存储、匹配和事件生成移至仿真端，同时修正 `MultiChannelsAML` 和 `XSCuteTop` 的使用方式（[XSAI #93](https://github.com/OpenXiangShan/XSAI/pull/93)）。

## CUTE

- Wonicon：修复多通道 DiffTest event index 的登记，并通过参数化 FIFO 深度、拆分数据和控制位、移除默认 store-ack 路由网络来降低面积（[CUTE #33](https://github.com/OpenXiangShan/CUTE/pull/33)）。
- ecall73：`MemoryLoader` 支持 tile register 的 e8/e16/e32 多精度转置加载，并新增字节平面和集成测试（[CUTE #35](https://github.com/OpenXiangShan/CUTE/pull/35)）。

## difftest

- yu-yake2002：MMA 验证器支持将连续兼容请求收集为可配置大小的批次，以统一后端 API 执行验证，并支持 CUDA 每批一次 kernel 执行（[difftest #920](https://github.com/OpenXiangShan/difftest/pull/920)）。
- yu-yake2002：为 MMA 验证器增加可配置背压，限制排队和执行中的验证请求，并在批次完成或验证器退出时唤醒受阻生产者（[difftest #923](https://github.com/OpenXiangShan/difftest/pull/923)）。

## 跨仓库关联

XSAI #93 将 CUTE 子模块更新到 CUTE #33 的合入提交。因此，最终双周报应将这两项合并表述，避免把同一项多通道 DiffTest/面积优化重复写成两条。
