# Biweekly 110 XSAI PR 候选清单

## 查询口径

- 生成日期：2026-08-31（Asia/Shanghai）。
- 查询窗口：2026-08-18 至 2026-08-31，以 PR 的 `mergedAt` 为准。
- 基础仓库：XSAI、CUTE、difftest、XSAICache。
- 已确认组员账号：`Wonicon`、`yu-yake2002`、`ecall73`、`Gs-ygc`、`Ivyfeather`、`zykucas`。
- Biweekly 109 的最终发布见 [发布归档](../../biweekly-109/published.md)；其中已报道的 XSAI #93、CUTE #33、CUTE #35、difftest #920、difftest #923 不重复写入。

## 汇总

| 来源 | 已合入 PR | 已确认组员 PR | 涉及的候选成果 | 待确认 PR | 排除 PR |
| --- | ---: | ---: | ---: | ---: | ---: |
| XSAI | 10 | 8 | 7 | 0 | 2 |
| CUTE | 2 | 1 | 1 | 0 | 1 |
| difftest | 16 | 3 | 2 | 0 | 13 |
| XSAICache | 1 | 1 | 1 | 0 | 0 |

候选成果按正文条目计数；跨仓库成果会在多个来源行中出现，连续 CI 改动与同一验证主题会合并为一条。

## 建议写入

| 分类 | 主题 | PR | 作者 | 合入时间（Asia/Shanghai） | 依据 |
| --- | --- | --- | --- | --- | --- |
| Bug 修复 | 修复 MLCT/MSCT 转置访存的数据布局和寄存器地址 | [XSAI #106](https://github.com/OpenXiangShan/XSAI/pull/106)、[CUTE #38](https://github.com/OpenXiangShan/CUTE/pull/38) | Wonicon；Gs-ygc | 08-19 09:45；08-18 18:13 | XSAI #106 集成 CUTE #38。后者保留乱序响应的转置信息，将 MLCT 响应写入正确的 C MatrixReg bank、entry 和 byte lane，并使用物理行组步长生成 MSC/MSCT 读地址；包含单元测试、编译、self-check 和 NEMU DiffTest 验证。 |
| 调试工具 | DiffTest 支持 AME `mcfg` 状态对比 | [XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107)、[difftest #944](https://github.com/OpenXiangShan/difftest/pull/944) | yu-yake2002 | 08-26 16:59；08-24 15:34 | XSAI 导出已提交的 `mcfg` 条目并传递 hart ID，DiffTest 同步、比较并报告 8 个 `mcfg` 状态；孙际儒个人周报亦记录该项。 |
| Bug 修复 | 修复矩阵响应与 HintQueue 状态不同步 | [XSAI #110](https://github.com/OpenXiangShan/XSAI/pull/110)、[XSAICache #6](https://github.com/OpenXiangShan/XSAICache/pull/6) | yu-yake2002；zykucas | 08-27 16:19；08-26 18:24 | XSAI #110 集成 XSAICache #6，使矩阵 `AccessAckData` 仅在实际响应发出时释放 HintQueue 条目，并保持其与普通 GrantBuffer 响应的顺序，避免混合流量导致队列失配、溢出或断言。 |
| Bug 修复 | 修复 Mx 操作数延迟写回时遗漏唤醒，避免 MLS 指令永久阻塞 | [XSAI #111](https://github.com/OpenXiangShan/XSAI/pull/111) | ecall73 | 08-27 23:33 | 李智恒个人周报记录为“XSAI 核对于 Mx 相关指令唤醒机制 bug”；PR 说明覆盖根因与 DiffTest 验证。 |
| 调试工具 | 支持 16-byte store checker 事件 | [XSAI #112](https://github.com/OpenXiangShan/XSAI/pull/112) | yu-yake2002 | 08-28 14:31 | 对齐 16-byte store 地址，传递完整 128-bit 数据和 16-bit mask，统一标量、向量和整行 store 事件。 |
| 代码质量 | 清理未使用的矩阵提交与调度反馈接口 | [XSAI #113](https://github.com/OpenXiangShan/XSAI/pull/113) | yu-yake2002 | 08-28 20:37 | 移除废弃的矩阵提交记账、ROB/LSQ 转发和 scheduler 接口，保留仍用于 MLSQ 容量核算的路径。 |
| 代码质量 | 并行化 EMU 与 nightly 回归 | [XSAI #114](https://github.com/OpenXiangShan/XSAI/pull/114)、[XSAI #116](https://github.com/OpenXiangShan/XSAI/pull/116) | yu-yake2002 | 08-29 15:51；08-30 16:43 | 复用 DefaultMatrixConfig EMU，拆分 EMU 基础测试、nightly checkpoint 和 SPEC06 工作负载，隔离各 job 的 NFS 输出。 |
| 调试工具 | 增强 MMA 验证失败处理与 AMU 事件诊断 | [difftest #926](https://github.com/OpenXiangShan/difftest/pull/926)、[difftest #927](https://github.com/OpenXiangShan/difftest/pull/927) | yu-yake2002 | 08-18 19:08；08-18 19:18 | #926 在参考模型无法提供 MMA 操作数时中止验证并释放资源；#927 拒绝非法 AMU 操作并改进未匹配 AMU 事件的报错。两项在 109 截稿时尚未合入。 |

## 跨仓库关联

- XSAI #106 将 CUTE 子模块从 `8fcc38d` 更新至 CUTE #38 的合入提交 `787255d`，因此两者合并为一项 MLCT/MSCT 转置访存修复。
- XSAI #110 将 XSAICache 子模块从 `89d33a3` 更新至 `50bf127`。该版本包含早于本期窗口合入的 XSAICache #1，以及本期的 XSAICache #6；正式正文只报道后者的矩阵响应队列修复，不将 #1 作为跨期独立成果。

## 已排除

| PR | 作者 | 合入时间（Asia/Shanghai） | 排除原因 |
| --- | --- | --- | --- |
| [XSAI #103](https://github.com/OpenXiangShan/XSAI/pull/103) | wakafa1 | 08-18 18:43 | 作者不在当前确认组员名单内。 |
| [XSAI #105](https://github.com/OpenXiangShan/XSAI/pull/105) | qihangGuo | 08-28 09:24 | 作者不在当前确认组员名单内。 |
| [CUTE #36](https://github.com/OpenXiangShan/CUTE/pull/36) | wakafa1 | 08-18 11:59 | 作者不在当前确认组员名单内。 |
| difftest #919、#931、#932、#933、#937、#940 至 #943、#945、#946、#948、#949 | 多人 | 08-18 至 08-26 | 作者不在当前确认组员名单内，或与 XSAI 工作无直接关联。 |

## 后续动作

1. 截稿前再次扫描 2026-09-01 之后新合入的 PR。
2. 按候选清单写中文 `### XSAI` v1，经负责人确认后再同步英文稿。
