# Biweekly 100-108 XSAI 已报道贡献者

## 口径

本名单由 Biweekly 100-108 的 XSAI 专节中明确链接的 40 个 PR 反查得到。账号是 GitHub PR 的 `author.login`，不是合入人、reviewer 或实际贡献者的完整名单。它只能表示“该账号的 PR 曾被 XSAI 双周报报道”，不能证明其正式组织归属或当前仍是 XSAI 组成员。

2026-08-15 已由 XSAI 负责人确认的组员账号为：`Wonicon`、`ecall73`、`yu-yake2002`。这三个账号可作为后续 PR 初筛的人工确认 allowlist；表中其他账号仍仅保留“历史已报道贡献者”的含义。

| GitHub 用户名 | 已报道 PR 数 | 历史周报中的 PR |
| --- | ---: | --- |
| yu-yake2002 | 19 | XSAI #59、#64、#65、#68、#71、#75、#79、#81、#84、#86、#95、#97、#98；CUTE #12、#13、#24、#27、#34；NEMU #995 |
| ecall73 | 6 | XSAI #63、#70、#77；CUTE #11、#14、#18 |
| Wonicon | 3 | XSAI #61、#62、#83 |
| wakafa1 | 3 | XSAI #99、#100、#101 |
| Gs-ygc | 3 | XSAI #102；xsai-env #4、#11 |
| Ivyfeather | 2 | XSAI #85、#91 |
| physics1024 | 1 | XSAI #72 |
| he-sheng-jie | 1 | CUTE #19 |
| livypad | 1 | CUTE #20 |
| whujtz67 | 1 | HBL2 #3 |

## 对 Biweekly 109 候选的匹配

| 候选 PR | 作者 | 是否命中历史名单 | 结论 |
| --- | --- | --- | --- |
| XSAI #93、CUTE #33 | Wonicon | 是 | 与多通道矩阵访存和其 DiffTest 支持直接相关，保留为候选。 |
| XSAI #104 | yu-yake2002 | 是 | 参数缓存改动；后确认视为上游 XiangShan #6336 的实现，不作为 109 独立进展报道。 |
| CUTE #35 | ecall73 | 是 | 矩阵转置加载能力，保留为候选。 |
| difftest #920、#923 | yu-yake2002 | 是 | 合入 `xsai-v2r2a`，保留为候选。 |
| difftest #917 | Wonicon | 是 | 早于 Biweekly 108 的标题日期合入，决定不作为 109 补漏。 |
| difftest #922 | poemonsense | 否 | 不在当前已确认组员范围内，不纳入正式供稿。 |

## 建议的筛选规则

1. 先查目标仓库中本周期 `mergedAt` 非空的 PR，并排除已经报道的 PR。
2. 若作者命中本名单，提升为高优先级候选；若未命中，仍按标题、描述、目标分支和改动文件评估。
3. 仅当改动直接服务于 XSAI、CUTE、XSAICache、HBL2 或 XSAI 的 DiffTest/环境需求时，写入周报。
4. 合并同一项跨仓库工作，防止子模块升级、底层实现和顶层集成各写一遍。

正式的组员名单应由 XSAI 负责人或组织维护者确认；若后续拿到该名单，可在此基础上维护一份人工确认的 allowlist，作为自动筛选的附加条件。
