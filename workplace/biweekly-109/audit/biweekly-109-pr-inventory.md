# Biweekly 109 XSAI PR 候选清单

> 2026-08-15 已确认组员账号后，正式供稿应以 [确认组员贡献梳理](biweekly-109-confirmed-member-contributions.md) 为准。本文件保留全量查询和非组员 PR 的审计记录；后续变动见 [本次复查记录](biweekly-109-pr-rescan-2026-08-15.md)。

## 查询范围

- 生成日期：2026-08-15（Asia/Shanghai）。
- 查询窗口：2026-07-27 至 2026-08-15，使用 GitHub Search 的 `is:pr is:merged merged:2026-07-27..2026-08-15` 条件；随后以 PR 详情中的 `mergedAt` 和目标分支复核。
- 这是与 Biweekly 108 重叠的窗口。108 期标题日期为 2026-08-03，而发布提交直到 2026-08-10 才合入；重叠查询并排除 108 已报道 PR，能够避免漏报或重报。
- 查询仓库：XSAI、CUTE、difftest、XSAICache、HBL2。`xsai-env` 和 NEMU 本期暂不查询，除非候选 PR 需要引用环境或参考模型改动。
- 只保留已合入 PR，即 `mergedAt` 非空；未合入即关闭的 PR 不在结果中。

## 汇总

| 仓库 | 已合入 PR | 适合写入 | 待确认 | 排除 | 备注 |
| --- | ---: | ---: | ---: | ---: | --- |
| XSAI | 4 | 1 | 0 | 3 | #77、#102 已在 108 期报道；#104 视为上游 XiangShan #6336 的实现，不单独报道 |
| CUTE | 2 | 2 | 0 | 0 | 均为矩阵单元能力或多通道路径改动 |
| difftest | 6 | 2 | 1 | 3 | #920、#923 合入 `xsai-v2r2a` 分支；#917 不作为 109 补漏 |
| XSAICache | 0 | 0 | 0 | 0 | 窗口内无已合入 PR |
| HBL2 | 0 | 0 | 0 | 0 | 窗口内无已合入 PR |

## 建议写入的候选成果

| 主题 | PR | 作者 | 合入时间（Asia/Shanghai） | 依据 |
| --- | --- | --- | --- | --- |
| 多通道 CUTE 的 DiffTest 支持与面积优化 | [XSAI #93](https://github.com/OpenXiangShan/XSAI/pull/93), [CUTE #33](https://github.com/OpenXiangShan/CUTE/pull/33) | Wonicon；Wonicon | 08-12 19:38；08-10 09:17 | XSAI #93 集成 CUTE #33，并调整矩阵 store event 在 RTL 与仿真端的职责；CUTE #33 修复多通道 DiffTest event index，同时缩减 FIFO 和 store-ack 网络面积。作为一条跨仓库成果，避免拆成重复条目。 |
| 多精度转置矩阵加载 | [CUTE #35](https://github.com/OpenXiangShan/CUTE/pull/35) | ecall73 | 08-13 00:31 | `MemoryLoader` 支持 tile register 的 e8/e16/e32 转置加载，并补充字节平面和集成测试。 |
| MMA 验证批处理与可配置背压 | [difftest #920](https://github.com/OpenXiangShan/difftest/pull/920), [difftest #923](https://github.com/OpenXiangShan/difftest/pull/923) | yu-yake2002；yu-yake2002 | 08-11 18:53；08-11 21:57 | 两者均合入 `xsai-v2r2a`：前者批量处理连续兼容的 MMA 验证请求，后者限制队列和执行中的验证请求并唤醒受阻生产者。可归为一条验证工具成果。 |

## 待负责人确认

| PR | 作者 | 合入时间（Asia/Shanghai） | 原因 |
| --- | --- | --- | --- |
| [difftest #922](https://github.com/OpenXiangShan/difftest/pull/922) | poemonsense | 08-12 11:27 | 为雁栖湖、南湖、昆明湖 V2/V3 拆分兼容性目标，并涉及 KMHV2；对基于昆明湖 V2R2 的 XSAI 可能有用，但 PR 本身未明确提及 XSAI。作者不在 100-108 的已报道贡献者名单中。XSAI #93 的 DiffTest 子模块指针也前进到该 PR 的合入提交。建议由 XSAI/DiffTest 负责人确认是否作为本组进展报道。 |

## 已排除的 PR

| PR | 作者 | 合入时间（Asia/Shanghai） | 排除原因 |
| --- | --- | --- | --- |
| [XSAI #77](https://github.com/OpenXiangShan/XSAI/pull/77) | ecall73 | 07-27 09:19 | 已在 Biweekly 108 报道为“AME 版本更新至 XSAI AME proposal 14”。 |
| [XSAI #102](https://github.com/OpenXiangShan/XSAI/pull/102) | Gs-ygc | 07-30 13:52 | 已在 Biweekly 108 报道为修复 `mfence` 未阻塞后续指令导致的死锁。 |
| [XSAI #104](https://github.com/OpenXiangShan/XSAI/pull/104) | yu-yake2002 | 08-15 09:29 | 视为上游 [XiangShan #6336](https://github.com/OpenXiangShan/XiangShan/pull/6336) 的实现，不作为 109 的独立进展报道。 |
| [difftest #917](https://github.com/OpenXiangShan/difftest/pull/917) | Wonicon | 07-29 09:06 | 合入时间早于 Biweekly 108 的标题日期；虽未被 108 期报道，但决定不作为 109 的补漏项。 |
| [difftest #918](https://github.com/OpenXiangShan/difftest/pull/918) | Ruomio | 07-28 10:44 | Zabha 支持，与 XSAI、矩阵单元或 XSAI 验证无直接关联。 |
| [difftest #921](https://github.com/OpenXiangShan/difftest/pull/921) | Copilot | 08-11 21:41 | 修复 `test-fuzzing-rocket` 的夜间 CI 分支固定，与 XSAI 无直接关联。 |

## 跨仓库关系

- XSAI #93 将其 CUTE 子模块从 `d3b96a8` 前进到 `8fcc38d`，后者是 CUTE #33 的合入提交，因此二者应在周报中合并叙述。
- 同一 XSAI #93 将 DiffTest 子模块前进到 `3e06679`，即 DiffTest #922 的合入提交；这解释了 #922 的待确认状态，但不等同于 #922 必须写入周报。
- CUTE #35 发生在 XSAI #93 之后，尚未由该 XSAI 集成 PR 带入，因此独立列为候选。

## 历史作者匹配

建议写入的 5 个 PR 的作者均出现在 [Biweekly 100-108 已报道贡献者名单](../../reference/history/xsai-biweekly-100-108-contributors.md) 中：Wonicon、ecall73 和 yu-yake2002。该匹配提高了候选可信度，但不是自动收录规则；仍须检查仓库范围、已合入状态、改动内容和与已报道 PR 的重复关系。

## 正式正文范围

已确认组员账号后，DiffTest #922 与 XSAI #104 均不纳入正式供稿。请以 [确认组员贡献梳理](biweekly-109-confirmed-member-contributions.md) 中的 5 个 PR 为来源，先合并跨仓库的重复成果，再整理成中文 `### XSAI` 段落并按双周报翻译规范生成英文对应段落。
