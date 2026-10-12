# Biweekly 113 XSAI PR 审计

## 查询边界

- 查询时点：2026-10-12（Asia/Shanghai）。本记录是当前快照，截稿前仍需复查。
- 暂定窗口起点：2026-09-29 00:00 +08:00，即 `2026-09-28T16:00:00Z`。上一期窗口和去重基线见 [Biweekly 112 复查记录](../../biweekly-112/audit/biweekly-112-pr-rescan-2026-09-28.md)。
- 按 `merged_at` 和目标分支筛选已合入 PR；作者必须在[确认成员名单](../../reference/team/xsai-member-directory.md)中，且改动与 XSAI CPU、矩阵单元、缓存或验证基础设施直接相关。
- 查询仓库：OpenXiangShan/XSAI、CUTE、difftest、XSAICache、NEMU，以及有直接线索时的 OurCompArchGroup/xsai-env。
- GitHub API 查询了各仓库按更新时间倒序的第一页；各页最早更新时间早于窗口起点，覆盖本窗口的已合入项。所有时间均由 API `merged_at` 转换为北京时间。
- 本轮语雀 MCP 暂不可用，未将个人周报作为本轮证据来源；技术事实以 PR 描述、合入提交和文件 diff 为准。

## 通过筛选的 PR

| 分类 | PR | 作者 | merged_at（UTC） | 北京时间 | 合入提交 |
| --- | --- | --- | --- | --- | --- |
| Bug 修复 | [XSAI #131](https://github.com/OpenXiangShan/XSAI/pull/131) | ecall73 | 2026-10-08T11:19:50Z | 10-08 19:19:50 | `4c5eaad` |
| Bug 修复 | [XSAICache #9](https://github.com/OpenXiangShan/XSAICache/pull/9) | ecall73 | 2026-10-08T10:01:03Z | 10-08 18:01:03 | `1186ab3` |
| Bug 修复 | [difftest #976](https://github.com/OpenXiangShan/difftest/pull/976) | yu-yake2002 | 2026-10-01T03:45:35Z | 10-01 11:45:35 | `fbff3cf` |
| Bug 修复 | [NEMU #1237](https://github.com/OpenXiangShan/NEMU/pull/1237) | yu-yake2002 | 2026-09-30T06:15:51Z | 09-30 14:15:51 | `274a9ea` |
| Bug 修复 | [NEMU #1239](https://github.com/OpenXiangShan/NEMU/pull/1239) | yu-yake2002 | 2026-10-04T06:39:31Z | 10-04 14:39:31 | `44420dd` |
| RTL 新特性 | [XSAI #124](https://github.com/OpenXiangShan/XSAI/pull/124) | zykucas | 2026-10-09T07:04:08Z | 10-09 15:04:08 | `b08396d` |
| RTL 新特性 | [XSAICache #7](https://github.com/OpenXiangShan/XSAICache/pull/7) | zykucas | 2026-10-08T09:09:38Z | 10-08 17:09:38 | `67480e7` |
| RTL 新特性 | [CUTE #43](https://github.com/OpenXiangShan/CUTE/pull/43) | ecall73 | 2026-10-09T16:44:48Z | 10-10 00:44:48 | `d27b93d` |
| RTL 新特性 | [XSAI #132](https://github.com/OpenXiangShan/XSAI/pull/132) | ecall73 | 2026-10-10T19:40:22Z | 10-11 03:40:22 | `e8fb1a1` |
| 调试工具 | [CUTE #45](https://github.com/OpenXiangShan/CUTE/pull/45) | yu-yake2002 | 2026-10-09T10:53:37Z | 10-09 18:53:37 | `bd27de4` |
| 调试工具 | [difftest #978](https://github.com/OpenXiangShan/difftest/pull/978) | yu-yake2002 | 2026-10-07T04:37:54Z | 10-07 12:37:54 | `8c1ec98` |
| 调试工具 | [NEMU #1238](https://github.com/OpenXiangShan/NEMU/pull/1238) | yu-yake2002 | 2026-10-03T19:48:24Z | 10-04 03:48:24 | `e1f8a61` |
| 调试工具 | [XSAI #133](https://github.com/OpenXiangShan/XSAI/pull/133) | yu-yake2002 | 2026-10-10T10:02:20Z | 10-10 18:02:20 | `67eae40` |

共 13 个 PR；其中跨仓库成果合并后为 7 条正文。所有纳入 PR 的目标分支均为各仓库 `master`。

## 事实核对与合并依据

### 昆明湖 V2 bug-fix 同步

XSAI #131 同步上游 correctness fixes，覆盖内存完成、replay/异常、虚拟地址、向量状态、L2 错误等路径，并更新 XSAICache gitlink。XSAICache #9 将其中三项 HBL2 error-path 修复移植到 XSAICache。按铁规则只写“同步昆明湖 V2 的 bug-fix”，不在正文展开具体修复。

### 矩阵预取集成

XSAICache #7 新增分 bank 的矩阵引导 L2 prefetcher，包括矩阵请求 tag、预取来源和统计路径；XSAI #124 更新 CUTE/XSAICache/utility 子模块及顶层连线，增加预取配置。二者是一个端到端 RTL 集成成果，合并为一条。

### TransposeLoadEngine

CUTE #43 将转置加载从普通 loader 中拆出为独立引擎，接入 AML，支持八通道参数化加载及 e8/e16/e32。XSAI #132 更新 CUTE 子模块指针并集成该实现。PR 描述含性能和综合数据，但正文 v1 不写数字，避免未经负责人确认的性能承诺。

### 矩阵结果 hash 比较

CUTE #45 将矩阵加载写回接入 MatrixHash 并发出紧凑完成事件；difftest #978 生成带位置和写入字节数的 128 位指纹并在退休时与 NEMU 比较；NEMU #1238 增加对应参考端 hash ABI 和比较逻辑；XSAI #133 更新 CUTE、difftest 和 ready-to-run 子模块。四者合并为一条调试工具成果。#133 还移除了 CI 中禁用 Verilator 向量化的临时覆盖，正文按主要成果归类，不单独扩写。

### 其他 Bug 修复

- difftest #976 根据选定矩阵寄存器的 entry width 计算 AMU finish-event stride，修复 MinimalMatrixConfig 兼容性。
- NEMU #1237 在向量、浮点、矩阵隐式状态更新及 `minit` 后使 CSR shadow 失效，避免 SHARE REF 导出过期 CSR 值。
- NEMU #1239 将 zstd 文件大小和读取计数改为适合 64 位文件的类型，处理短读/中断读，并向上层传播镜像加载失败。

## 排除项与边界

| PR | 结果 | 理由 |
| --- | --- | --- |
| [OurCompArchGroup/xsai-env #39](https://github.com/OurCompArchGroup/xsai-env/pull/39) | 不写正文 | 作者 ecall73，但目标分支为 `feat-bitnet`，不是默认主线；内容是 BitNet 环境的多仓库 branch/submodule pin 更新，当前无法证明是本期 XSAI 主线供稿成果。 |
| difftest #979 | 不写正文 | 作者 HeiHuDie 不在确认名单。 |
| difftest #954、#977 | 不写正文 | 作者不在确认名单。 |
| NEMU #1245 | 不写正文 | 作者 whujtz67 不在确认名单。 |

开放 PR、上一期已报道 PR 和非成员 PR 均不纳入正文。截止实际截稿前需重新扫描；若 #131/#9 等成果在 112 已被报道，应由负责人决定是否去重，本轮按 112 审计记录视为未报道。

## 待确认

1. 负责人确认“矩阵引导的 L2 预取器”与“TransposeLoadEngine”是否按 RTL 新特性发布。
2. 负责人确认是否保留矩阵 hash 比较条目的四仓库链接，或进一步压缩为更短表述。
3. 截稿前复查 2026-10-12 之后的新合入 PR，再生成英文稿并提交 `XiangShan-doc` 的 `biweekly-113` 分支。
