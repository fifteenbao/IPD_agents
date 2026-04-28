# projects/ — 你的项目实例

本目录用于存放**你自己的智能硬件产品案例**。每个子目录对应一个产品项目，由 multi-agent 体系按 IPD 阶段产出标准化文件。

> ⚠️ 实际的产品案例文件（市场分析、Charter、PRD、TR 报告等）通常包含商业敏感信息或未发布的产品策略，**已在仓库根目录的 `.gitignore` 中排除**，不会被推送到远程。

---

## 推荐目录结构

```
projects/
└── <product-name>/
    ├── project_board.md            ← 项目工作台（PM 维护）
    │
    ├── 01-market-analysis.md       ← CMO 输出
    ├── 02-tech-feasibility.md      ← CTO 输出
    ├── 03-financial-feasibility.md ← CFO 输出
    │
    ├── 10-cdcp-review.md           ← CDCP 决策记录
    │
    ├── 20-charter.md               ← CPO 立项报告
    ├── 21-prd.md                   ← CPO 产品需求文档
    ├── 22-pdcp-review.md           ← PDCP 决策记录
    │
    ├── 30-tr1-review.md            ← TR1 技术评审
    ├── 31-tr2-review.md
    ├── ...
    │
    └── 90-pre-mortem-reports/      ← 各阶段 pre-mortem 归档
        ├── pre-mortem-cdcp.md
        └── pre-mortem-pdcp.md
```

文件名前缀（`01-`, `10-`, `20-`…）用于在文件管理器中按 IPD 阶段排序。

---

## 工作流示例

```bash
# 1. 创建新项目
mkdir -p projects/smart-running-watch
cd projects/smart-running-watch

# 2. 让 multi-agent 启动概念阶段
#    在 Claude Code 中输入：
#    "在 projects/smart-running-watch/ 下，跑一次 CDCP 评审。
#     产品构想：面向半马 / 全马跑者的智能腕表，
#     差异化定位 = 步态分析 + 训练自适应。"
#
# CEO 会调起 CMO/CFO/CTO 完成市场/财务/技术分析，
# 经 pre-mortem → COO 审核 → Board 评分，
# 在 projects/smart-running-watch/ 内输出标准化文件。

# 3. 通过后进入计划阶段
#    "基于已通过的 CDCP，启动 PDCP 流程，
#     产出 Charter + PRD"
```

---

## 项目工作台（project_board.md）

每个项目应该维护一个 `project_board.md`，作为 PM 视角的"驾驶舱"。建议字段：

```markdown
# 项目工作台 · {产品名}

| 字段 | 内容 |
|------|------|
| 产品名称 |  |
| 启动日期 |  |
| 当前阶段 | 概念 / 计划 / 开发 / 验证 / 发布 |
| 当前 PRD 版本 |  |
| 下一决策门 | CDCP / PDCP / TR{X} / GA |
| 整体状态 | 🟢 健康 / 🟡 需关注 / 🔴 阻塞 |

## 里程碑看板
| # | 里程碑 | 计划日期 | 状态 |

## 活跃风险
（引用 pre-mortem 输出 + PM 风险登记册）

## 关键假设
（引用 assumption-prioritization 输出，标注是否已验证）

## 决策记录
（DCP 通过条件、未决问题清单）
```

---

## 不要把什么放进来

- ❌ 个人身份信息、合作方未公开的资料
- ❌ 已签 NDA 的供应商报价单原件
- ❌ 第三方专利文档
- ❌ 客户访谈录音（脱敏摘要可以）

如果你 fork 本仓库后想分享某个项目作为示例，请先做脱敏处理（替换公司名、模糊具体数字）。
