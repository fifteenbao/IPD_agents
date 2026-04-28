---
name: opportunity-solution-tree
description: Teresa Torres 的 OST 框架。从用户的"增量时间去向"映射到机会、方案与验证实验，连接 CMO 的市场洞察与 CPO 的产品定义。
domain: cross
inputs: 用户增量时间分析（来自 SOUL.md 时代命题）+ 市场调研结果
outputs: 一棵树状结构，从 Outcome → Opportunities → Solutions → Experiments
when-to-use: 概念阶段（CDCP 之前），CMO 完成市场分析后，CPO 撰写 Charter 之前
---

# Opportunity Solution Tree（机会解决方案树）

## 框架本质

OST 把**抽象的用户痛点**结构化成**可执行的方案与实验**。它强制你回答：
- 我们的目标是什么？（顶层 Outcome）
- 用户在追求这个目标时遇到什么问题？（中层 Opportunities）
- 我们能提供什么？（下层 Solutions）
- 怎么知道方案有效？（叶层 Experiments）

**与 SOUL.md 时代命题的衔接**：顶层 Outcome 锚定在"用户的增量时间将流向哪个真实活动"，中下层映射"硬件如何深化体验（量化/辅助/连接/记录）"。

---

## 树状结构

```
                    ┌───────────────┐
                    │   OUTCOME     │  ← 业务目标（与战略对齐）
                    └───────┬───────┘
                            │
        ┌───────────────────┼───────────────────┐
        ▼                   ▼                   ▼
    ┌───────┐           ┌───────┐           ┌───────┐
    │ OPP A │           │ OPP B │           │ OPP C │  ← 用户痛点/机会
    └───┬───┘           └───┬───┘           └───┬───┘
        │                   │                   │
    ┌───┴───┐           ┌───┴───┐           ┌───┴───┐
    ▼       ▼           ▼       ▼           ▼       ▼
  Sol1    Sol2        Sol3    Sol4        Sol5    Sol6   ← 候选方案
    │                   │                   │
   Exp                 Exp                 Exp           ← 验证实验
```

---

## 使用步骤

### Step 1 — 锚定 Outcome
- 必须可量化、有时间窗
- ❌ "增加用户活跃度"  → ✅ "首发 6 个月内 SOM 达成 5000 万元"
- 应直接对应 CMO 市场分析中的 SOM 与差异化定位

### Step 2 — 发掘 Opportunities（机会层）
来源：用户访谈、痛点调研、竞品差评、客服记录。

每个 Opportunity 用 JBTD 风格描述：
> "When {情境}，用户感到 {挫败/未满足}，因为 {根因}。"

例（运动健康品类）：
- 跑步配速波动大但不知道为什么
- 训练计划无法根据状态自适应
- 跑后疲劳无客观恢复指标

**机会必须真实存在**——每条要有≥3 个用户证据来源。

### Step 3 — 生成 Solutions（方案层）
对每个 Opportunity 至少产出 3 个候选方案——避免过早收敛到一个想法。

例（针对"配速波动不知原因"）：
- Sol A：腕表内置 IMU + 步态分析算法
- Sol B：胸带心率 + 配速联动反馈
- Sol C：鞋内传感器 + 脚部触地分析

### Step 4 — 设计 Experiments（实验层）
每个 Solution 必须有**最低成本验证**手段，避免直接进入 EVT 才发现错误。

实验类型（智能硬件）：
- 用户访谈（脚本：参考 `interview-script` skill）
- 纸面原型 / Figma 演示
- 3D 打印外观件 + 表演式硬件
- 软件模拟（用手机替代未来腕表）
- 小批量众测（已有相似产品）

---

## 输出格式（Markdown 树）

```
【OST · {项目名}】
日期：{YYYY-MM-DD}

▶ OUTCOME
  首发 6 个月内 SOM 达成 5000 万元，复购率 ≥ 25%

  ├─ OPPORTUNITY 1: 跑步用户无法理解配速波动的原因
  │  证据：知乎搜索量 ↑200%、竞品差评 Top 3、用户访谈 12/15 提及
  │  ├─ Solution 1.1: 腕表 IMU + 步态分析（推荐 ★）
  │  │  └─ Experiment: 与 5 名跑者做 1 周纸面原型测试
  │  ├─ Solution 1.2: 胸带 + 联动反馈
  │  └─ Solution 1.3: 鞋内传感器
  │
  ├─ OPPORTUNITY 2: ...

━━━ 决策记录 ━━━
本轮选定推进的方案：{Sol 1.1, Sol 2.x, ...}
理由：{说明}
后续 Experiment 截止：{日期}
```

---

## 注意事项

1. **不要从 Solution 开始反推**——这是 PM 最容易犯的错误。先有 Opportunity，再有 Solution。
2. **机会层是 CMO 的输出，方案层是 CPO 的输出**——本 skill 是两者的协作交接界面。
3. **保留树而非剪枝**——被淘汰的分支也是宝贵资产，下个版本可能用上。
4. 与 `kano-model` 配合：必备需求通常来自 OST 中证据最强的 Opportunity。
