# XSAI 涉及仓库：Biweekly 100-108

本表只梳理 Biweekly 100-108 的 XSAI 专节、XSAI 的发布介绍和其直接子模块配置。它不包含同一期中前端、后端、访存等其他组的仓库。PR 出现次数按中文 XSAI 专节统计；中英文稿的重复链接不重复计算。

## PR 收集主范围

| 仓库 | URL | 角色 | 周报证据 | 后续 PR 查询 |
| --- | --- | --- | --- | --- |
| XSAI | <https://github.com/OpenXiangShan/XSAI> | 总系统：CPU、矩阵单元集成、缓存及 XSAI 相关基础设施的顶层集成 | 101-108 共引用 26 个 XSAI PR；100 期正式公布该仓库 | 必须 |
| CUTE | <https://github.com/OpenXiangShan/CUTE> | 矩阵单元 | 102-108 共引用 10 个 CUTE PR | 必须 |
| difftest | <https://github.com/OpenXiangShan/difftest> | 协同仿真与差分测试基础设施 | 103 期提到“XSAI DiffTest”，106 期报道 DiffTest 的 C++11 兼容性修复；XSAI 的 `.gitmodules` 直接声明其 URL | 必须，符合既定范围 |

## 直接相关的补充仓库

| 仓库 | URL | 角色 | 周报证据 | 建议 |
| --- | --- | --- | --- | --- |
| XSAICache | <https://github.com/OpenXiangShan/XSAICache> | XSAI 缓存子系统 | 107 期称其替代 `coupledL2/huancun/openLLC`；XSAI PR #85 将其加入为子模块 | 建议纳入 PR 查询，否则会漏掉缓存子系统的独立改动 |
| HBL2 | <https://github.com/OpenXiangShan/HBL2> | 高带宽 L2 缓存 | 100 期介绍 HBL2；104 期推进 CHI；105 期引用 HBL2 #3 | 建议纳入 PR 查询，尤其在 HBL2 仍独立开发时 |
| xsai-env | <https://github.com/OurCompArchGroup/xsai-env> | 构建、firmware、checkpoint 和仿真环境 | 102 期引用 `xsai-env` #4 和 #11 | 按需查询：有环境、评估或工具链成果时纳入 |
| NEMU | <https://github.com/OpenXiangShan/NEMU> | 参考模型和调试支持 | 101 期引用 NEMU #995，用于 BF16 扩展支持 | 按需查询：只纳入直接服务于 XSAI 的改动 |

## 资料仓库

| 仓库 | URL | 证据 | 处理方式 |
| --- | --- | --- | --- |
| Talks-and-Publications | <https://github.com/OpenXiangShan/Talks-and-Publications> | 100 期链接至 2025 RISC-V 中国峰会的 XSAI 报告 | 仅用于引用演示材料，不纳入日常 PR 收集 |

## 边界与依据

- 上述 GitHub URL 均于 2026-08-14 通过 GitHub 仓库 API 返回 `200` 验证可访问。
- XSAI PR #85 的 `.gitmodules` 将 `XSAICache` 加入路径 `XSAICache`，URL 为 `https://github.com/OpenXiangShan/XSAICache`；同一配置中 `difftest` 的 URL 为 `https://github.com/OpenXiangShan/difftest`。
- XSAI 当前还依赖其他子模块，但它们未在 100-108 的 XSAI 专节中出现，故不列为本轮双周报采集范围。
- 下一轮 PR 汇总的最小集合是 XSAI、CUTE、difftest。为不遗漏历史周报已报道的独立缓存工作，推荐集合扩展为 XSAI、CUTE、difftest、XSAICache、HBL2；`xsai-env` 和 NEMU 根据本周期 PR 是否直接服务 XSAI 再加入。
