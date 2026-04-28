---
name: cdcp-review
description: 概念决策评审（CDCP）端到端工作流。完成市场/财务/技术初评 → COO 审核 → Board 决策。
trigger: 用户提出新项目立项构想，需要判断是否值得进入计划阶段
agents: [CMO, CFO, CTO, CEO, COO, Board]
skills: [kano-model, opportunity-solution-tree, pre-mortem, assumption-prioritization, dcp-scoring-rubric]
output: 【IPMT决策·CDCP】（批准 / 有条件批准 / 暂缓 / 终止）
---

# /cdcp-review — 概念决策评审

## 触发场景

用户：
- "想做一款 {新品类} 智能硬件，能不能立项？"
- "我们要不要做 {竞品} 的对标产品？"

## 整体编排

```
[用户输入项目构想]
       ▼
   ┌─────────┐
   │ CEO/主控 │ 制定 CDCP 执行计划
   └────┬────┘
        │ 并发分发
   ┌────┼────────────────┐
   ▼    ▼                ▼
 CMO   CFO             CTO
（市场） （财务初评）    （技术可行性）
   │    │                │
   ▼    ▼                ▼
[聚合输出 → 跨域综合]
        │
        ▼
  ┌──────────┐
  │ pre-mortem│ 反向推演失败场景
  └─────┬────┘
        │
        ▼
   ┌─────────┐
   │ COO/守门 │ 审核完整性、可行性
   └────┬────┘
        │
        ▼  通过
   ┌─────────┐
   │  Board  │ 五维评分 + 一票否决检查
   └────┬────┘
        │
        ▼
  【CDCP 决策】
```

---

## 步骤详解

### Step 1 — CEO 制定执行计划（5 min）
CEO 输出标准【执行计划】，明确分工与时间节点。

### Step 2 — CMO 市场分析（并发，主线）
引用 skill：
- `kano-model` — 候选功能的需求分层
- `opportunity-solution-tree` — 用户增量时间 → 机会 → 方案

输出：市场分析报告（参考 `cmo.md` 模板）
关键交付：
- TAM / SAM / SOM
- Top 3 用户痛点
- 差异化定位声明
- 时间增量逻辑判断（与 SOUL.md 时代命题对齐）

### Step 3 — CFO 初步商业可行性（并发）
注意：CDCP 阶段财务模型为**初步估算**，BOM 与销量假设容忍度较高（±30%）。
关键交付：
- 初步 BOM（基于参考品类）
- 初步财务预测（5 年 + 三种情景）
- 初步 ROI（NPV / 回收期）

### Step 4 — CTO 技术可行性（并发）
关键交付：
- TRL 评估表
- 技术路线比较（≥2 个方案）
- 技术风险与应对（高/中风险）
- 预计研发周期

### Step 5 — Pre-mortem（综合，跨域）
引用 skill：`pre-mortem`
参与：所有 C-Level 共同
产出：失败场景清单 + Top 5 必须应对项

### Step 6 — Assumption 识别（综合，跨域）
引用 skill：`assumption-prioritization`
产出：Top 5 必须验证假设 + 验证手段 + 截止时间

### Step 7 — COO 审核
COO 检查清单：
- [ ] 市场分析有数据支撑（不是空泛判断）
- [ ] 财务模型敏感性分析完整
- [ ] 技术风险有应对方案
- [ ] Pre-mortem 高分项已有应对
- [ ] 关键假设有验证计划

输出：【COO审核·通过/驳回/待补充】
- **驳回必须重做**对应步骤
- **通过**才能进入 Board 评审

### Step 8 — Board CDCP 评审
引用 skill：`dcp-scoring-rubric`
输出：【IPMT决策·CDCP】

**通过门槛**：≥ 15/25 + 任一维度不低于 2 + 无一票否决

---

## 时间预算

| 步骤 | 预计耗时 |
|------|---------|
| CEO 计划 | 5 min |
| 三方并发分析 | 30-45 min |
| Pre-mortem | 15-20 min |
| Assumption 识别 | 10-15 min |
| COO 审核 | 5-10 min |
| Board 评分 | 10-15 min |
| **总计** | **75-110 min** |

## 常见失败模式

1. **跳过 pre-mortem 直接送 Board** → 风险章节只有正向风险列表，缺乏盲点
2. **CFO 在 CDCP 就给出精确数字** → 制造虚假精度，应明确"初估 ±30%"
3. **CTO 报告"全部 TRL 9"** → 没认真评估，COO 应打回
4. **Board 评分讨论技术细节** → 越权，违反 board.md 的"不评论技术实现"原则
