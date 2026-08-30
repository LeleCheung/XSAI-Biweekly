# Biweekly 110 XSAI PR 候选清单

## 查询口径

- 生成日期：2026-08-31（Asia/Shanghai）。
- 查询窗口：2026-08-18 至 2026-08-31，以 PR 的 `mergedAt` 为准。
- 基础仓库：XSAI、CUTE、difftest；XSAICache 仅因 XSAI #110 的 submodule 更新而列入待确认项。
- 已确认组员账号：`Wonicon`、`yu-yake2002`、`ecall73`。
- Biweekly 109 的最终发布见 [发布归档](../../biweekly-109/published.md)；其中已报道的 XSAI #93、CUTE #33、CUTE #35、difftest #920、difftest #923 不重复写入。

## 汇总

| 来源 | 已合入 PR | 已确认组员 PR | 涉及的候选成果 | 待确认 PR | 排除 PR |
| --- | ---: | ---: | ---: | ---: | ---: |
| XSAI | 10 | 8 | 5 | 2 | 2 |
| CUTE | 2 | 0 | 0 | 1 | 1 |
| difftest | 16 | 3 | 2 | 0 | 13 |

候选成果按正文条目计数；跨仓库成果会在多个来源行中出现，连续 CI 改动与同一验证主题会合并为一条。

## 建议写入

| 分类 | 主题 | PR | 作者 | 合入时间（Asia/Shanghai） | 依据 |
| --- | --- | --- | --- | --- | --- |
| 调试工具 | DiffTest 支持 AME `mcfg` 状态对比 | [XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107)、[difftest #944](https://github.com/OpenXiangShan/difftest/pull/944) | yu-yake2002 | 08-26 16:59；08-24 15:34 | XSAI 导出已提交的 `mcfg` 条目并传递 hart ID，DiffTest 同步、比较并报告 8 个 `mcfg` 状态；孙际儒个人周报亦记录该项。 |
| Bug 修复 | 修复 Mx 操作数延迟写回时遗漏唤醒，避免 MLS 指令永久阻塞 | [XSAI #111](https://github.com/OpenXiangShan/XSAI/pull/111) | ecall73 | 08-27 23:33 | 李智恒个人周报记录为“XSAI 核对于 Mx 相关指令唤醒机制 bug”；PR 说明覆盖根因与 DiffTest 验证。 |
| 调试工具 | 支持 16-byte store checker 事件 | [XSAI #112](https://github.com/OpenXiangShan/XSAI/pull/112) | yu-yake2002 | 08-28 14:31 | 对齐 16-byte store 地址，传递完整 128-bit 数据和 16-bit mask，统一标量、向量和整行 store 事件。 |
| 代码质量 | 清理未使用的矩阵提交与调度反馈接口 | [XSAI #113](https://github.com/OpenXiangShan/XSAI/pull/113) | yu-yake2002 | 08-28 20:37 | 移除废弃的矩阵提交记账、ROB/LSQ 转发和 scheduler 接口，保留仍用于 MLSQ 容量核算的路径。 |
| 代码质量 | 并行化 EMU 与 nightly 回归 | [XSAI #114](https://github.com/OpenXiangShan/XSAI/pull/114)、[XSAI #116](https://github.com/OpenXiangShan/XSAI/pull/116) | yu-yake2002 | 08-29 15:51；08-30 16:43 | 复用 DefaultMatrixConfig EMU，拆分 EMU 基础测试、nightly checkpoint 和 SPEC06 工作负载，隔离各 job 的 NFS 输出。 |
| 调试工具 | 增强 MMA 验证失败处理与 AMU 事件诊断 | [difftest #926](https://github.com/OpenXiangShan/difftest/pull/926)、[difftest #927](https://github.com/OpenXiangShan/difftest/pull/927) | yu-yake2002 | 08-18 19:08；08-18 19:18 | #926 在参考模型无法提供 MMA 操作数时中止验证并释放资源；#927 拒绝非法 AMU 操作并改进未匹配 AMU 事件的报错。两项在 109 截稿时尚未合入。 |

## 待负责人确认

| 主题 | PR | 作者 | 合入时间（Asia/Shanghai） | 原因 |
| --- | --- | --- | --- | --- |
| CUTE 的 MLCT/MSCT 转置访存修复集成 | [XSAI #106](https://github.com/OpenXiangShan/XSAI/pull/106)、[CUTE #38](https://github.com/OpenXiangShan/CUTE/pull/38) | Wonicon；Gs-ygc | 08-19 09:45；08-18 18:13 | XSAI #106 仅将 CUTE 指针前进到 CUTE #38；后者修复 MLCT 转置布局与 MatrixReg store 地址，但作者 `Gs-ygc` 不在当前确认名单。请确认是否以 Wonicon 的集成工作写入本期。 |
| XSAICache 子模块更新 | [XSAI #110](https://github.com/OpenXiangShan/XSAI/pull/110) | yu-yake2002 | 08-27 16:19 | PR 仅更新 XSAICache gitlink，尚未确认其指向的具体成果及其是否应作为 XSAI 独立进展报道。 |

## 已排除

| PR | 作者 | 合入时间（Asia/Shanghai） | 排除原因 |
| --- | --- | --- | --- |
| [XSAI #103](https://github.com/OpenXiangShan/XSAI/pull/103) | wakafa1 | 08-18 18:43 | 作者不在当前确认组员名单内。 |
| [XSAI #105](https://github.com/OpenXiangShan/XSAI/pull/105) | qihangGuo | 08-28 09:24 | 作者不在当前确认组员名单内。 |
| [CUTE #36](https://github.com/OpenXiangShan/CUTE/pull/36) | wakafa1 | 08-18 11:59 | 作者不在当前确认组员名单内。 |
| difftest #919、#931、#932、#933、#937、#940 至 #943、#945、#946、#948、#949 | 多人 | 08-18 至 08-26 | 作者不在当前确认组员名单内，或与 XSAI 工作无直接关联。 |

## 后续动作

1. 确认 XSAI #106 与 #110 是否纳入本期。
2. 截稿前再次扫描 2026-09-01 之后新合入的 PR。
3. 确认候选范围后，按分类写中文 `### XSAI` v1，再同步英文稿。
