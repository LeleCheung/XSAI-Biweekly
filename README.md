# XSAI Biweekly Workspace

This repository keeps the XSAI team's Biweekly working records: historical references, PR audits, Chinese and English drafts, and the publishing workflow. It does not mirror the published XiangShan documentation.

## Layout

```text
workplace/
  biweekly-{num}/     # Per-issue audits and drafts
  reference/          # Historical extracts and writing workflow
  meta/               # Task background and administrative records
```

`XiangShan-doc/` is intentionally ignored. Keep it as a separate clone of `OpenXiangShan/XiangShan-doc` alongside this repository. When the editor creates a `biweekly-{num}` aggregation branch, use that clone to commit the final Chinese and English XSAI sections to the upstream branch.

## Quick Start

On a new machine, clone this repository as `Biweekly`, then clone the upstream documentation repository inside it:

```bash
git clone git@github.com:LeleCheung/XSAI-Biweekly.git Biweekly
cd Biweekly
git clone git@github.com:OpenXiangShan/XiangShan-doc.git XiangShan-doc
```

The parent repository tracks only the working records. `XiangShan-doc/` remains an independent clone for publishing, and must not be added to the parent repository.

### Prepare an Issue

Start the agent from the `Biweekly/` directory with the current issue number and ask it to follow the workflow document. For example:

```text
按照 workplace/reference/writing/xsai-biweekly-workflow.md 为 Biweekly 110 准备 XSAI 供稿。先在 workplace/biweekly-110/ 中完成 PR 审计和中英文草稿；在我确认前，不修改 XiangShan-doc。
```

The agent should use the historical references and audit evidence in `workplace/`, then commit the new working records to this repository after the Chinese and English drafts are confirmed.

### Publish an Issue

Only enter the publishing stage after the editor has created the upstream `biweekly-{num}` aggregation branch and PR. Ensure the GitHub SSH account has write access to `OpenXiangShan/XiangShan-doc`, then ask the agent to perform the final rescan and publish only the XSAI section. For example:

```text
总编辑已创建 XiangShan-doc 的 biweekly-110 汇总分支和 PR。请按照工作流完成截稿前 PR 复查，将确认后的中英文 XSAI 段落提交到该分支；只修改两份 Biweekly 110 正式周报文件。
```

After the editor merges the aggregation PR, record the final PR URL and commit hash in `workplace/`, commit that archival record here, and update the local `XiangShan-doc` clone from `master`.

## Workflow

The operating workflow is maintained in [workplace/reference/writing/xsai-biweekly-workflow.md](workplace/reference/writing/xsai-biweekly-workflow.md). The index for the current records is [workplace/README.md](workplace/README.md).
