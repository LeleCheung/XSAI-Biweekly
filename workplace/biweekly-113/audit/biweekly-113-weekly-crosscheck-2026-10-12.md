# Biweekly 113 个人周报核对与 PR 复查

## 本轮范围

2026-10-12 恢复 Yuque MCP 后成功认证为组账号，并读取七位确认成员的目录当级文档。本文更新初审中“语雀不可用”的状态；不归档完整私人文档。中文版更新为 [v2](../drafts/biweekly-113-xsai-zh-v2.md)，保留 v1 为历史记录。

复查六仓库的 `state=all&sort=updated&direction=desc&per_page=100` 列表，按确认成员及 `merged_at` 筛选。第一页最早更新时间如下，均早于本期窗口，覆盖本轮窗口内已合入项：

| 仓库 | 返回数 | 最早更新时间（UTC） |
| --- | ---: | --- |
| OpenXiangShan/XSAI | 100 | 2025-09-25T08:44:37Z |
| OpenXiangShan/CUTE | 43 | 2025-09-10T03:16:29Z |
| OpenXiangShan/difftest | 100 | 2026-05-26T04:22:09Z |
| OpenXiangShan/XSAICache | 9 | 2026-07-26T06:26:46Z |
| OpenXiangShan/NEMU | 100 | 2026-08-28T13:24:16Z |
| OurCompArchGroup/xsai-env | 23 | 2026-04-09T09:19:06Z |

本期窗口仍暂定从北京时间 09-29 00:00 开始。13 个已纳入 PR 无变化，合并为 7 条、3 类。另读取上游 master 的 112 中文发布正文，确认其中 XSAI 段仍为此前供稿的 9 个 PR；本期 13 个 PR 未被该段报道。

## 个人周报依据

| 成员 | 文档与核对范围 | 对正文的影响 |
| --- | --- | --- |
| 王诲喆 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/grs6dtuc8f09yn4e)，09-28～29、10-08～10 | 记录 Saturn 调研、poster 和 CUTE PR 合并/rebase；无新增已合入候选，不扩写成果。 |
| 孙际儒 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/hyzxo2bhpyxbi8hb)，09-26～10-02、10-03～09 | 直接链接 #1237、#1239、hash 四仓库 PR，统一列作调试工具；#976 在 09-19～25 段记录为 MinimalMatrixConfig stride 修复。正文改为这些成果的短句。 |
| 李智恒 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/qob4thmc864keqh2)，顶部两段 | 直接记录 #43 的双 buffer、引擎放在 AML、参数化多通道支持，以及 #131/#9 的同步。顶部两段重复标为 W24、09-20～24，因此不能用标题推断真实完成时间；以 PR 合入时间为准。正文不加入性能数字。 |
| 乐国春 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/zsdlyky6gsqcki51)，09-28～10-09 | 主要为软件材料、Agent 瓶颈和峰会报告准备，无新增已核实合入 PR。 |
| 陈熙 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/rthttaoitdoq35od)，10-08～10、09-20～22 | 最新段落为峰会准备；环境更新为此前进展，不能据此宣称 xsai-env 主线新增已合入成果。 |
| 张钰堃 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/ao1glf88i6qspe9l)，09-25～10-10 段 | 记录 stories15M checkpoint、无预取/BOP 对照和矩阵预取版本在测；cold-miss 新代码尚未接入测试。正文只写已合入的预取器集成，不宣称推理性能提升或 cold-miss 完成。标题结束年份写为 2025，按上下文识别为笔误，不用于判断合入窗口。 |
| 王凯帆 | [个人文档](https://bosc.yuque.com/up3wk0/twwy86/nc8tg448d2o5xt3h) | 当级文档仍为空，没有本期周报佐证；本轮仓库筛选无其新增已合入候选。 |

## v2 的表述与分类

- #976、#1237、#1239 为验证工具/参考模型修复，归入“调试工具”，与历史写法和孙际儒周报一致；#131/#9 仍按铁规则归入“Bug 修复”。
- “独立转置加载引擎”是 PR 中 TransposeLoadEngine 的中文概括；双组缓冲、多通道支持均有 PR 与周报依据。保持“RTL 新特性”分类，不在正文加入综合指标。
- “矩阵寄存器 hash 对比”沿用孙际儒周报措辞，四个链接保留用于追溯端到端成果。它针对已实现的矩阵加载/清零等结果检查，不能解读为所有矩阵指令都替换成 hash。
- zstd 条目压缩为大尺寸镜像读取修复；原 PR 的加载失败传播仍保留在初审证据中，不必在正文枚举。
- 初审预取段落称 #124 更新 XSAICache 子模块不准确：其文件 diff 更新的是 CUTE、utility 和顶层连线/配置。已进一步核对 XSAI master 树：XSAICache gitlink 为 `1186ab336ad130767f6e86fd6afc7cd1d24d1098`；与 #7 合入提交 `67480e73e978fc827b788250b8e811048fe145c2` 比较为 ahead 1、behind 0，确认当前固定版本包含 #7。因此“集成”有组件实现、顶层接线及当前 gitlink 依据，不承诺性能数字或默认启用。

## 跨期漏项与待观察

- [NEMU #1236](https://github.com/OpenXiangShan/NEMU/pull/1236)：作者 yu-yake2002，master 已合入，UTC `2026-09-28T04:55:48Z`，即北京时间 09-28 12:55:48。晚于 112 最后扫描时点、早于 113 暂定窗口；112 正式正文未收录。孙际儒周报记为暂时关闭矩阵 CSR 的 MS 检查。按既定规则仅列为跨期漏项，待负责人决定是否补报，不自动加入 v2。
- NEMU #1248（matrix hash 计算加速）、#1249（矩阵 dispatch 与 PMEM 访问分离）仍 open；不写正文。
- XSAI #109 / difftest #947、XSAICache #5、xsai-env #38/#32 仍 open。
- xsai-env #39 虽 merged，但目标是 feat-bitnet。个人周报提供 BitNet 工作背景，仍需负责人决定是否作为本期独立环境成果发布，当前不写正文。

中文确认后再翻译；实际供稿前复查新合入项。
