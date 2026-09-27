# Biweekly 112 XSAI PR 复查

## 边界与扫描覆盖

- 查询时点：北京时间 2026-09-27 23:59 至 09-28 00:01 左右；状态为该轮快照，不代表最终截稿状态。
- 本期窗口起点：2026-09-15 00:00 +08:00（`2026-09-14T16:00:00Z`）。沿用 [09-24 审计](biweekly-112-pr-inventory-2026-09-24.md) 的上一期去重基线。
- GitHub API 已恢复。本轮各仓库查询 `pulls?state=all&sort=updated&direction=desc&per_page=100&page=1`，按 `merged_at`、作者及工作相关性筛选。各仓库第一页最早更新时间均早于窗口起点，因此无需继续翻页才能覆盖本窗口已合入项。
- 另查上一期 #129 合入后至本期窗口前的边界，未发现确认成员的待补报合入项。
- 09-28 负责人确认 `wakafa1 → 王凯帆`，当前按[七名确认成员](../../reference/team/xsai-member-directory.md)筛选。不自动补报其往期贡献。

| 仓库 | 返回 PR 数 | 页内最早更新时间日期 | 本窗口组员相关已合入 PR |
| --- | ---: | --- | --- |
| OpenXiangShan/XSAI | 100 | 2025-09-18 | #130 |
| OpenXiangShan/CUTE | 40 | 2025-09-10 | #40、#41、#42 |
| OpenXiangShan/difftest | 100 | 2026-05-15 | #962 |
| OpenXiangShan/XSAICache | 9 | 2026-07-26 | 无 |
| OpenXiangShan/NEMU | 100 | 2026-08-25 | #1212、#1217、#1224、#1225 |
| OurCompArchGroup/xsai-env | 22 | 2026-04-09 | 无 |

此表仅列组员相关成果，不等同于仓库所有合入项。difftest 本窗口另有 #968、#971、#972、#974；NEMU 本窗口共 24 个合入 PR，均经过成员筛选。

## 纳入清单与精确合入时间

以下 PR 目标分支均为各仓库 master；北京时间为 UTC +08:00。

| PR | 作者 | merged_at（UTC） | 北京时间 | 合入提交 |
| --- | --- | --- | --- | --- |
| [XSAI #130](https://github.com/OpenXiangShan/XSAI/pull/130) | yu-yake2002 | 2026-09-15T08:58:26Z | 09-15 16:58:26 | `10737a9` |
| [CUTE #40](https://github.com/OpenXiangShan/CUTE/pull/40) | wakafa1 | 2026-09-17T02:22:35Z | 09-17 10:22:35 | `48950fe` |
| [CUTE #41](https://github.com/OpenXiangShan/CUTE/pull/41) | wakafa1 | 2026-09-17T06:15:47Z | 09-17 14:15:47 | `e95cf31` |
| [CUTE #42](https://github.com/OpenXiangShan/CUTE/pull/42) | yu-yake2002 | 2026-09-23T01:07:00Z | 09-23 09:07:00 | `a992585` |
| [difftest #962](https://github.com/OpenXiangShan/difftest/pull/962) | yu-yake2002 | 2026-09-18T06:57:23Z | 09-18 14:57:23 | `c41ad09` |
| [NEMU #1212](https://github.com/OpenXiangShan/NEMU/pull/1212) | yu-yake2002 | 2026-09-15T02:10:12Z | 09-15 10:10:12 | `8578032` |
| [NEMU #1217](https://github.com/OpenXiangShan/NEMU/pull/1217) | yu-yake2002 | 2026-09-18T05:40:38Z | 09-18 13:40:38 | `7e06731` |
| [NEMU #1224](https://github.com/OpenXiangShan/NEMU/pull/1224) | yu-yake2002 | 2026-09-20T04:47:52Z | 09-20 12:47:52 | `a0105e4` |
| [NEMU #1225](https://github.com/OpenXiangShan/NEMU/pull/1225) | wakafa1 | 2026-09-24T11:06:01Z | 09-24 19:06:01 | `e9b6749` |

## 新增成员贡献的事实与写法

### CUTE #40、#41：合并为一条调试工具成果

- #40 标题为 `feat(testtop): support wrapping cute & hbl2 as DUT wholly`，描述为 `Add support for CHI+HBL2 testtop`。新增 TestTopWithL2，通过 Cute2TL 连接 CUTE 和 CoupledL2，提供 CHI 下游接口，并增加对应生成目标。
- #41 标题为 `fix(testtop): add probe for cute-l2 interface for IT env`，没有正文描述。diff 在测试顶层加入 TLIdentityNode 和各 bank 的 `l2Write` 观测输出，包括握手、地址、数据和首末拍等信号；不是新增缓存功能，也不是改变访存握手行为。
- 中文压缩为“增加 CUTE 与 L2 联合测试顶层，并提供写请求观测接口”。“联合测试顶层”来自 #40，“写请求观测接口”来自 #41 的代码，属于编辑概括，有直接事实依据。
- 两者归入调试工具，不写成 RTL 新特性；同一验证成果只写一条。

### NEMU #1225：单列调试工具成果

- 标题为 `feat(share-ctrl): complete CUTE AMU callbacks and optimize controller mode`。PR 描述明确针对 CONFIG_SHARE_CTRL 与 CUTE 验证框架的集成。
- diff 补充 MMA 回调的舍入模式与实际操作数符号属性，修正 mzero 回调编码，增加 `ctrl_mtok_advance` 以推进矩阵 token，并调整控制模式编译与日志配置。
- 中文压缩为“完善 NEMU 的 CUTE 控制模式回调与矩阵同步支持”。回调和同步分别对应上述回调字段/编码及 token 推進接口；不暗示完成整个验证框架，也不宣称量化性能提升。
- 这是控制模式验证接口改进，不与普通 DiffTest 参考模型修复混为一条。

### 个人周报依据

已读取语雀 [王凯帆](https://bosc.yuque.com/up3wk0/twwy86/nc8tg448d2o5xt3h) 当级文档，返回正文 `<p></p>`、字数 0，更新时间 2026-07-13。本次没有获得可对应这三个 PR 的个人周报表述；不据此断言不存在其他周报文档。成员身份以负责人确认为准，成果内容以 PR 描述及 diff 为准。

原六个候选的 PR diff 也已补查，事实范围沿用 09-24 审计：#130 是 CI 输入更新；#962 是 packed 事件向自然布局转换；#42 锁存握手时的 PC/coreid；#1217 仅缩小部分加载的有效比较区域；#1212 和 #1224 的诊断选项默认关闭。中文 v2 保留原五条表述，新增上述两条，共 9 个 PR、7 条正文、2 类。

## 集成状态与剩余边界

- XSAI master 为 `10737a92e798783516c4bdd91ea8888330a56e93`，其中 CUTE gitlink 为 `787255d48b6f49209de3fa4ef59876eac4221705`，difftest gitlink 为 `b5cc8fcce2160a4923f7ecfe38e02fff2891a59e`。比较结果显示 #42、#962 的合入版本分别比对应固定版本领先 7、3 个提交；组件已合入不等于 XSAI 已集成，正文不作整体集成承诺。
- XSAI #131 / XSAICache #9、XSAI #124 / XSAICache #7、XSAI #109 / difftest #947、XSAICache #5、xsai-env #38 / #32 均仍 open，不写正文。#131/#9 合入后按铁规则合并概括为“同步昆明湖 V2 的 bug-fix”，归入 Bug 修复。
- xsai-env 默认分支自窗口起点的提交查询返回空列表；陈熙周报中的配置更新尚未对应到该分支的已合入成果，不推断为已发布。
- MinimalMatrixConfig stride 与 hash 比较等个人周报进展，仍无本轮确认的已合入 PR。
- 尚待中文审阅和实际截稿时间确认；提交前需再检查新增合入项。本轮不生成英文、不修改 XiangShan-doc、不提交上游。

当前审阅入口：[中文 v2](../drafts/biweekly-112-xsai-zh-v2.md)。09-24 审计与 v1 保留为历史快照，其扫描缺口和成员排除结论以本记录更新。
