# Biweekly 112 XSAI PR 初步审计

## 查询边界与完成度

- 查询日期：2026-09-24（Asia/Shanghai）。本轮开始核查约为 20:10；所有状态均为查询时点快照。
- 暂定窗口起点：2026-09-15 00:00 +08:00，即 `2026-09-14T16:00:00Z`。当前仅准备截至查询时点的 v1；09-25 至实际截稿的新贡献仍需复查。
- 六位确认成员均按[当前名单](../../reference/team/xsai-member-directory.md)筛选；本轮没有新增成员。
- 核心范围：OpenXiangShan/XSAI、CUTE、difftest、XSAICache。因个人周报中的直接关联线索，补查 OpenXiangShan/NEMU 与 OurCompArchGroup/xsai-env。xsai-env 的真实仓库归属是 OurCompArchGroup，不能沿用此前对话中误写的 OpenXiangShan/xsai-env。
- **尚未完成全量扫描**：本地 GitHub API 经配置代理连接失败，尝试直连也超时；网页方式能读取单个 PR、提交 diff 和部分开放列表，但 closed/merged 筛选列表、提交历史及 API 未成功获取。以下是已核实候选，不是全部 PR 的穷举清单；不能将未获取的仓库统计写为零。
- 本轮以 PR 页明确的 Merged 状态、目标分支及合入事件日期确认候选资格；尚未获得 API 精确 `mergedAt`。下表日期是 GitHub 页面显示日期，不冒充北京时间的精确合入时间。最终提交前必须补齐 API 时间及分页覆盖。
- 正文保持历史分类与精简风格；中文未经负责人确认，暂不翻译或提交上游。

## 上一期去重基线

已对照上游 master 的 [111 期正文](https://github.com/OpenXiangShan/XiangShan-doc/blob/master/docs/blog/posts/biweekly-111.md) 的 XSAI 段、本地供稿提交 `8c80115` 和中英文稿。已报道项为：CUTE #39；XSAI #120、#121、#122、#123、#126、#128、#129；XSAICache #8；difftest #953、#955、#958；NEMU #1189、#1197、#1200。本期不重复报道这些成果。

正式发布的 XSAI 段保留相同 PR 集合，将本地草稿的“退休”改为“退役”；后续同类术语参考正式发布用词。上一轮 09-14 查询之后、09-15 窗口之前如有未报道合入项，需恢复 API 后单列核实，不能自动补漏。

## 已核实候选

以下六个 PR 的作者均为 `yu-yake2002`，目标分支均为相应仓库的 `master`。标题、描述和合入事件已核对；部分提交 diff 页面获取失败，未宣称完成逐行代码审查。

| 分类 | PR | 页面合入日期 | 合入提交 | 正文概括与事实边界 |
| --- | --- | --- | --- | --- |
| 代码质量 | [XSAI #130](https://github.com/OpenXiangShan/XSAI/pull/130) | 2026-09-15 | `10737a9` | CI nightly 随机回归改用单核 RVA23 无向量 SPEC CPU2006/CPU2017 checkpoint 池。属于 CI 测试输入更新，不能表述为 XSAI 新增 RVA23 RTL 支持。 |
| 调试工具 | [difftest #962](https://github.com/OpenXiangShan/difftest/pull/962) | 2026-09-18 | `c41ad09` | batch 输出 packed AMU control/Msync 事件，NEMU 需要自然对齐的结构体；在 checker 调用参考模型前做字段转换。111 时仍 open，本期已合入，可正常纳入。 |
| 调试工具 | [CUTE #42](https://github.com/OpenXiangShan/CUTE/pull/42) | 2026-09-23 | `a992585` | 接受 A/B/C microtask 的 valid/ready 握手时锁存 PC 与 coreid，C load/store 保持独立元数据。修复的是 DiffTest 事件采样，不能写成新增多核计算能力。 |
| 调试工具 | [NEMU #1217](https://github.com/OpenXiangShan/NEMU/pull/1217) | 2026-09-18 | `7e06731` | 部分矩阵加载仅比较有效写入区域，避免 untouched bytes 的误报；mzero 仍保留整寄存器检查，不能概括为所有矩阵指令都缩小比较范围。 |
| 调试工具 | [NEMU #1212](https://github.com/OpenXiangShan/NEMU/pull/1212) | 2026-09-15 | `8578032` | 检查 matrix load 消费尚未经过有效可见性屏障的标量/向量 store。保留原有反方向检查；选项默认关闭，仅告警。mfence 之外还识别符合条件的其他屏障，不写成只能由 mfence 同步。 |
| 调试工具 | [NEMU #1224](https://github.com/OpenXiangShan/NEMU/pull/1224) | 2026-09-20 | `a0105e4` | 记录矩阵寄存器最近写入的有效区域，检查 MMA/mstore 是否读取区域外的未定义值；由默认关闭的配置项控制，不宣称修复了硬件结果或默认启用检查。 |

## 表述来源与合并方式

- #130 的“RVA23 无向量 SPEC checkpoint 池”来自 PR 描述；“CI nightly 随机回归”沿用项目语境。
- #962 的“布局不一致”来自 PR 的 packed/naturally aligned 解释，个人周报直接确认 batch 报错根因。
- #42 的“coreid 与 PC 采样”来自 PR 描述和提交说明；个人周报重点写多核配置下 coreid 取值错误。正文补充 PC 有 PR 依据，不是推测。
- #1217 的“避免未写入区域误报”来自 PR 描述。其范围与未定义行为读取诊断不同，因此单独列一条。
- #1212 和 #1224 合并为一条 NEMU 矩阵使用合法性检查成果，保留两个链接；两项不同检查在上表分别留证。
- 本轮不假设上述 CUTE/DiffTest 修复已被 XSAI 子模块集成；目前没有核实到相应集成 PR。后续查到集成 PR 后核对 gitlink，再并列链接。

### 后续代码复核入口

1. [XSAI #130 合入提交](https://github.com/OpenXiangShan/XSAI/commit/10737a9)
2. [difftest #962 合入提交](https://github.com/OpenXiangShan/difftest/commit/c41ad09)
3. [CUTE #42 合入提交](https://github.com/OpenXiangShan/CUTE/commit/a992585)
4. [NEMU #1217 合入提交](https://github.com/OpenXiangShan/NEMU/commit/7e06731)
5. [NEMU #1212 合入提交](https://github.com/OpenXiangShan/NEMU/commit/8578032)
6. [NEMU #1224 合入提交](https://github.com/OpenXiangShan/NEMU/commit/a0105e4)

## 个人周报核对

已读取下列六人的目录当级文档本身，并核对近期段落；只归纳本任务相关信息，不归档完整个人文档。

| 成员 | 读取文档与日期段 | 对本期的影响 |
| --- | --- | --- |
| 王诲喆 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/grs6dtuc8f09yn4e)，09-14～09-18、09-20～09-24 | CUTE 访存代码整理与可配置化仍处于准备提交阶段；ARA 评估暂无已核实合入 PR，不写正文。 |
| 孙际儒 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/hyzxo2bhpyxbi8hb)，09-12～09-18、09-19～09-25 | 直接对应 #962、#42、#1212、#1217、#1224。文档标记到 09-25 的一周，但本次只能确认 09-24 读取到的内容。MinimalMatrixConfig stride 修复与 hash 比较仍在推进，不当作已合入成果。#130 未见近期周报直接链接，以 PR 为准。 |
| 李智恒 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/qob4thmc864keqh2)，09-14～09-18、09-20～09-24 | #129 已在 111 报道；#131、XSAICache #9 虽在周报中列作工作进展，但 PR 仍 open。周报不能替代合入状态。 |
| 乐国春 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/zsdlyky6gsqcki51)，09-13～09-18、09-20～09-24 | FPGA 演示、软件部署与 PPA 评估作为背景，未核实到对应已合入 PR，不据此扩写发布成果。 |
| 陈熙 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/rthttaoitdoq35od)，09-12～09-18、09-20～09-24 | 记录 xsai-env 配置更新，因此扩查 OurCompArchGroup/xsai-env；尚不能确认对应合入 PR，标记待补查。 |
| 张钰堃 | [个人周报](https://bosc.yuque.com/up3wk0/twwy86/ao1glf88i6qspe9l)，09-12～09-18、09-19～09-24 | 内容主要为预取调研与后续方案。日期标题的结束年份写作 2025，按上下文识别为笔误；不据此推断 PR 时间或新增已合入预取成果。 |

## 待观察、排除与扫描缺口

| 对象 | 核对结果 | 本轮处理 |
| --- | --- | --- |
| [XSAI #131](https://github.com/OpenXiangShan/XSAI/pull/131)、[XSAICache #9](https://github.com/OpenXiangShan/XSAICache/pull/9) | PR 页面均为 Open；#131 要求先合入 #9 | 不写正文。合入后按铁规则合并为“同步昆明湖 V2 的 bug-fix”，不逐项展开。 |
| [XSAI #124](https://github.com/OpenXiangShan/XSAI/pull/124)、[XSAICache #7](https://github.com/OpenXiangShan/XSAICache/pull/7) | 开放列表/PR 页仍显示 Open | 矩阵预取集成继续观察，不重复报道上期 CUTE #39。 |
| [XSAI #109](https://github.com/OpenXiangShan/XSAI/pull/109)、[difftest #947](https://github.com/OpenXiangShan/difftest/pull/947) | 开放列表仍显示 Open | BUILD_DIR 隔离尚不能列为已完成。 |
| [XSAICache #5](https://github.com/OpenXiangShan/XSAICache/pull/5) | PR 页面显示 Open | ReadOnce 改动不写入。 |
| [CUTE #40](https://github.com/OpenXiangShan/CUTE/pull/40)、[CUTE #41](https://github.com/OpenXiangShan/CUTE/pull/41) | 作者 wakafa1，不在当前确认名单 | 不以组员成果写入，不据此自行修改成员名单。 |
| OurCompArchGroup/xsai-env | 仓库及开放列表可读；#38、#32 仍 open，closed 列表无法获取 | 陈熙周报提及的配置更新需查清是直接提交还是已合入 PR，不将“尚未查到”等同于“没有贡献”。 |
| 核心四仓库及 NEMU 的全量 closed/merged 分页 | API/筛选列表未成功获取 | 需要恢复连接后补查，包括较早创建但本期才合入的 PR；不能只按 PR 编号扫新号。 |

## 截稿前必做

1. 恢复 GitHub API 后，以实际 `mergedAt` 和 base 分支重跑完整分页；保存查询时点，补齐时区转换与去重检查。
2. 补查 111 最后查询之后的边界遗漏；如属上期漏项，单列请负责人决定，不直接加入本期。
3. 检查 09-25 至实际截稿新合入项，重点观察 #131/#9、预取集成和 MinimalMatrixConfig stride 修复。
4. 审阅当前 [中文 v1](../drafts/biweekly-112-xsai-zh-v1.md)；确认后再生成英文及提交汇总分支。
