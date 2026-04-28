---
name: pdcp-review
description: 计划决策评审（PDCP）端到端工作流。基于 CDCP 通过后的深度方案，授权进入开发阶段。
trigger: CDCP 已通过，Charter 与 PRD 草稿完成，需要 IPMT 批准进入 TR1
agents: [CPO, CTO, CFO, CEO, COO, Board, PM]
skills: [charter-template, prd-template, job-stories, kano-model, assumption-prioritization, pre-mortem, dcp-scoring-rubric]
output: 【IPMT决策·PDCP】+ 已批准的 Charter + PRD + 项目计划
---

# /pdcp-review — 计划决策评审

## 触发场景

CDCP 已通过 → 项目进入计划阶段（约 4-8 周）→ 完成 Charter、PRD、详细技术方案 → 提交 PDCP

PDCP 是**最重要的投资决策点**：通过后将启动模具、采购长交期器件，决策成本极高。

## 整体编排

```
[CDCP 通过 → 项目启动计划阶段]
                ▼
        ┌──────────────┐
        │ CEO/主控      │ 制定 PDCP 计划阶段执行方案
        └──────┬───────┘
               │
       ┌───────┼─────────────────────────┐
       ▼       ▼                         ▼
     CPO     CTO                       CFO
      │      │                          │
      ▼      ▼                          ▼
  撰写 Charter   出技术方案+TR1预审    完整商业案例
  撰写 PRD      架构定型              BOM 锁定±15%
      │       │                          │
      └───────┴──────────┬───────────────┘
                         ▼
              ┌───────────────────┐
              │ Pre-mortem (二轮) │
              │ Assumption (深度) │
              └─────────┬─────────┘
                        │
              ┌─────────▼─────────┐
              │  PM 制定项目计划   │
              │  WBS + 风险登记册  │
              └─────────┬─────────┘
                        │
                ┌───────▼───────┐
                │  COO/守门     │ 审核 Charter 完整性、PRD 可测性
                └───────┬───────┘
                        │
                ┌───────▼───────┐
                │   Board IPMT  │ ≥18/25 通过门槛
                └───────────────┘
```

---

## 步骤详解

### Step 1 — CEO 制定计划阶段执行方案

明确：
- Charter 起草人 = CPO
- PRD 起草人 = CPO
- 技术方案 = CTO
- 商业案例（深度版）= CFO
- 时间节点：通常 4-8 周

### Step 2 — CPO 撰写 Charter
引用 skill：`charter-template`
输入：CMO/CFO/CTO 在 CDCP 阶段的产出（深化版）

### Step 3 — CPO 撰写 PRD
引用 skill：`prd-template` + `job-stories`
关键：
- 所有需求必须可测试
- 强制检查"智能硬件常见遗漏"清单
- 与 CTO 同步硬件规格章节

### Step 4 — CTO 技术方案
深化 CDCP 阶段的技术报告：
- 系统架构图（硬件 / 固件 / 云端）
- BOM 锁定（容差 ±15%）
- 关键器件备选方案
- TR1 预审检查表（参考 cto.md）

### Step 5 — CFO 完整商业案例
深化 CDCP 阶段的财务报告：
- BOM 量产成本（规模效应已计入）
- 5 年财务预测（模型已校准）
- NPV / IRR / 回收期 / 盈亏平衡销量
- 三情景敏感性分析
- 定价建议

### Step 6 — Pre-mortem（二轮）
引用 skill：`pre-mortem`
与 CDCP 的 pre-mortem 对比：
- 哪些风险已经规避？（验证应对方案）
- 哪些新风险浮现？（深度方案暴露的）

### Step 7 — Assumption Prioritization（深度版）
引用 skill：`assumption-prioritization`
**关键差异**：CDCP 阶段的假设此时应大部分已被验证或转为事实。
- 已验证 → 记录证据
- 未验证 → 必须给出 PDCP 通过后的验证计划

### Step 8 — PM 项目计划
- WBS 分解到周
- 关键路径识别
- 风险登记册（合并 pre-mortem 输出）
- 预算 vs CFO 投资预算的对账

### Step 9 — COO 审核
COO 检查清单：
- [ ] Charter ≤ 15 页，引用源齐全
- [ ] PRD 中无模糊词（"快速"、"流畅"等）
- [ ] PRD 第八章"常见遗漏"全部勾选
- [ ] BOM 偏差容差 ≤ 15%
- [ ] CDCP 阶段的关键假设全部有结论
- [ ] Pre-mortem Top 5 全部有应对方案
- [ ] PM 计划与 CFO 预算对齐

### Step 10 — Board PDCP 评审
引用 skill：`dcp-scoring-rubric`
**通过门槛**：≥ 18/25 + Charter+PRD 完整 + pre-mortem 已跑

---

## 时间预算

| 步骤 | 预计耗时 |
|------|---------|
| CEO 计划 | 10 min |
| CPO Charter+PRD | 60-90 min |
| CTO 技术方案 | 30-45 min |
| CFO 商业案例 | 30-45 min |
| Pre-mortem 二轮 | 20 min |
| Assumption 深度 | 15 min |
| PM 项目计划 | 30 min |
| COO 审核 | 15-20 min |
| Board 评分 | 15-20 min |
| **总计** | **3.5-5 小时** |

## 常见失败模式

1. **PRD 拷贝 Charter** → 没有展开到可测试粒度，COO 必须打回
2. **BOM 还是 CDCP 的初估** → 没做规模效应测算，财务模型失真
3. **PDT 团队还没组建就提交 PDCP** → 执行可信度评分必然 ≤ 2
4. **关键假设全部转为"待 EVT 验证"** → 逃避 PDCP 阶段的责任，COO 应严格把关
5. **Board 在 PDCP 才发现根本问题** → 说明 CDCP 放水，回归 CDCP 失败模式
