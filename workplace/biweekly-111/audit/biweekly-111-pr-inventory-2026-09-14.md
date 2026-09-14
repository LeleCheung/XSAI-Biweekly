# Biweekly 111 XSAI PR 候选清单

## 查询口径

- 生成日期：2026-09-14（Asia/Shanghai）。
- 查询窗口：2026-09-01 至 2026-09-14；以 PR 的 `mergedAt` 为准。
- 核心仓库：XSAI、CUTE、difftest、XSAICache；因直接服务于 AME 验证，补查 NEMU。
- 已确认组员账号及语雀映射见[成员名单](../../reference/team/xsai-member-directory.md)。
- Biweekly 110 已报道的 PR 不重复写入：XSAI #106、#107、#110、#111、#112、#113、#114、#116，CUTE #38，XSAICache #6，difftest #926、#927、#944，NEMU #1172。

## 建议写入

| 分类 | 主题 | PR | 作者 | 合入时间（Asia/Shanghai） | 依据 |
| --- | --- | --- | --- | --- | --- |
| 代码质量 | 更新 nightly 回归 checkpoint 池并固定节点运行 | [XSAI #120](https://github.com/OpenXiangShan/XSAI/pull/120)、[XSAI #122](https://github.com/OpenXiangShan/XSAI/pull/122) | yu-yake2002 | 09-03 13:40；09-04 08:58 | 切换到 GCC16 RV64GCB 的 SPEC checkpoint 与兼容 restorer，显式报告缺失 checkpoint；nightly matrix jobs 固定到 node runner，避免构建与回归落到不同集群。 |
| 调试工具 | 完善 AME DiffTest 的 `mrelease` 退休与旧 `mstore` 顺序检查 | [XSAI #121](https://github.com/OpenXiangShan/XSAI/pull/121)、[difftest #953](https://github.com/OpenXiangShan/difftest/pull/953)、[XSAI #128](https://github.com/OpenXiangShan/XSAI/pull/128)、[difftest #958](https://github.com/OpenXiangShan/difftest/pull/958) | yu-yake2002 | 09-03 13:01；09-03 12:50；09-11 10:30；09-10 15:04 | `mrelease` 在 DUT 完成事件到达时立即更新 REF 的 `msync`，并检查其退休前所有更早的 `mstore` 已完成，避免异步完成造成状态或顺序错误。XSAI #128 同时带入非组员的 Replay 修复，但不单独报道。 |
| 调试工具 | 为 AME 错误路径记录正确的指令 PC | [XSAI #121](https://github.com/OpenXiangShan/XSAI/pull/121)、[difftest #955](https://github.com/OpenXiangShan/difftest/pull/955) | yu-yake2002 | 09-03 13:01；09-03 10:43 | 为 AMU ctrl/exec 和 `msync` 错误统一记录出错指令 PC，使异步矩阵错误的 Abort 信息指向正确位置。 |
| Bug 修复 | 同步昆明湖 V2 的四项适配修复 | [XSAI #123](https://github.com/OpenXiangShan/XSAI/pull/123) | ecall73 | 09-06 08:49 | 同步向量异常 GPA、PMM 规范化触发器地址、CBO LT/GE 地址匹配和 DRAMSim3 DPI 边沿采样修复，并保留 XSAI 本地封装适配。 |
| Bug 修复 | 同步昆明湖 V2 的计数器溢出和 XSPDB 适配修复 | [XSAI #129](https://github.com/OpenXiangShan/XSAI/pull/129) | ecall73 | 09-14 10:48 | 保持 LCOFIP counter-overflow 请求，避免 CSR 读改写期间中断丢失；同时补入 XSPDB picker 的 `-S` include-path 修复。 |
| Bug 修复 | 修复预取 RequestBuffer 活锁 | [XSAI #126](https://github.com/OpenXiangShan/XSAI/pull/126)、[XSAICache #8](https://github.com/OpenXiangShan/XSAICache/pull/8) | yu-yake2002；zykucas | 09-09 00:26；09-08 18:31 | 取消已进入 `chosenQ` 的预取请求时只检查缓存的就绪状态变化，避免瞬时节流信号反复取消请求并触发 `ReqBuf Leak`。 |
| RTL 新特性 | 为 CUTE 访存请求传递矩阵预取描述信息 | [CUTE #39](https://github.com/OpenXiangShan/CUTE/pull/39) | zykucas | 09-10 16:25 | 为 A/B/C loader 传递 task/stream 预取标签，区分矩阵 demand 与 prefetch 请求，保留 C-store 的 debug trace 标签，并补充 trace 验证；PR 依赖的 XSAICache #7 仍未合入，不单独列为成果。 |
| 调试工具 | 优化 NEMU 浮点 MMACC 参考模型并完善 BF16 路径 | [NEMU #1189](https://github.com/OpenXiangShan/NEMU/pull/1189)、[NEMU #1197](https://github.com/OpenXiangShan/NEMU/pull/1197)、[NEMU #1200](https://github.com/OpenXiangShan/NEMU/pull/1200) | ecall73；yu-yake2002 | 09-01 09:36；09-06 11:51；09-07 22:24 | 修复 BF16×BF16→FP32 MMACC，增加 FP16/BF16/FP32 浮点 MMACC 自动向量化路径，并校验操作数编码、tile 边界、类型组合和舍入语义；标量/SoftFloat 路径保留为回退。 |

## 跨仓库关联

- XSAI #121 将 difftest 从 `2e146c604` 更新到 `8b8032bfc`，带入本期已合入的 difftest #953、#955，以及非组员 difftest #956 的 VCS DRAMsim3 链接支持。正文只突出组员负责且与 AME 验证直接相关的两项修复。
- XSAI #128 将 difftest 从 `8b8032bfc` 更新到 `b5cc8fcce`，带入组员 difftest #958 和非组员 difftest #957；正文只报道 #958 的 mrelease 顺序检查。
- XSAI #126 将 XSAICache 从 `50bf1272` 更新到 `1681c85c`，对应 XSAICache #8 的预取活锁修复。
- CUTE #39 的 XSAICache 子模块指向包含预取器开发提交的 `9398f79f`，但 XSAICache #7 尚未合入主分支；本期只依据已合入的 CUTE #39 报道 CUTE 侧接口和请求标签改动。

## 待观察或排除

| PR | 作者 | 状态/合入时间 | 原因 |
| --- | --- | --- | --- |
| [XSAI #124](https://github.com/OpenXiangShan/XSAI/pull/124) | zykucas | open | 矩阵预取 RTL 集成尚未合入。 |
| [XSAICache #7](https://github.com/OpenXiangShan/XSAICache/pull/7) | zykucas | open | 矩阵引导预取器尚未合入；其提交作为 CUTE #39 的依赖被引用。 |
| [difftest #962](https://github.com/OpenXiangShan/difftest/pull/962) | yu-yake2002 | open（09-12 创建） | NEMU ABI 适配尚未合入，留待下期复查。 |
| XSAI #119 | wakafa1 | 09-02 00:31 | 作者不在当前确认组员名单内。 |
| XSAI #127 | qihangGuo | 09-10 09:21 | 作者不在当前确认组员名单内。 |
| difftest #950、#956、#957、#959 | 多人 | 09-03 至 09-11 | 作者不在当前确认组员名单内；其中 #956、#957 已由 XSAI 子模块 bump 间接带入，但不作为组员独立成果报道。 |

## 后续动作

1. 负责人确认分类、跨仓库合并方式和 NEMU 条目后，审阅中文 `biweekly-111-xsai-zh-v1.md`。
2. 中文确认后再按翻译规范生成英文稿；在总编辑创建 `biweekly-111` 汇总分支前不修改 `XiangShan-doc/`。
