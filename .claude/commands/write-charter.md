---
name: write-charter
description: 立项报告（Charter）生成工作流。聚合 CMO + CFO + CTO 输出，由 CPO 整合为 PDCP 评审材料。
trigger: CDCP 已通过，进入计划阶段，需要正式立项文件
agents: [CPO, CMO, CFO, CTO]
skills: [charter-template, kano-model, opportunity-solution-tree, pre-mortem, assumption-prioritization]
output: 完整 Charter 文档（10-15 页），可直接用于 PDCP 评审
---

# /write-charter — 立项报告生成

## 触发场景

- "PDCP 评审在两周后，需要把 CDCP 阶段的输出整合成 Charter"
- "从市场+技术+财务的报告，生成立项文件"

## 工作流

```
[CMO 市场报告]   [CFO 财务报告]   [CTO 技术报告]
       │              │                │
       └──────────────┴────────────────┘
                      │ 聚合
                      ▼
              ┌──────────────┐
              │   CPO 整合    │
              │ 引用 charter- │
              │   template    │
              └──────┬───────┘
                     │
                     ▼
              ┌──────────────┐
              │ pre-mortem   │ → 注入第七章
              │ (跨 C-Level) │
              └──────┬───────┘
                     │
                     ▼
              ┌──────────────┐
              │ assumption-  │ → 注入第八章
              │ prioritization│
              └──────┬───────┘
                     │
                     ▼
              ┌──────────────┐
              │  COO 审核     │
              └──────┬───────┘
                     │
                     ▼
                Charter v1.0
```

---

## 步骤

### Step 1 — CPO 收集输入
**必备输入**：
- CMO 市场分析报告（含 TAM/SAM/SOM、KANO、定位）
- CFO 商业可行性报告（含投资、NPV/IRR、定价）
- CTO 技术可行性报告（含 TRL、风险、研发周期）

**前置检查**：
- [ ] 三份报告均为正式版本（非草稿）
- [ ] 关键数字之间无矛盾（如 CMO 的 SOM 与 CFO 的销量预测一致）

发现矛盾 → 退回对应 C-Level 修订，不强行整合。

### Step 2 — 引用 charter-template
按 9 章结构填充：

| Charter 章节 | 主要数据来源 |
|------------|-------------|
| 一、市场机会 | CMO 报告 + SOUL.md 时代命题 |
| 二、产品定义 | CMO 定位 + `kano-model` + `opportunity-solution-tree` |
| 三、商业案例 | CFO 报告 |
| 四、可行性摘要 | CTO 技术 + 供应链 + 认证评估 |
| 五、项目计划 | PM 里程碑 |
| 六、PDT 团队 | CEO 团队组建结果 |
| 七、风险清单 | `pre-mortem` 输出 |
| 八、关键假设 | `assumption-prioritization` 输出 |
| 九、立项建议 | CPO 综合判断 |

### Step 3 — 跨域 Pre-mortem
**所有 C-Level 共同参与**，不只是 CPO 独立完成。
产出注入第七章。

### Step 4 — Assumption Prioritization
列出 Charter 中所有"假设性陈述"，按矩阵排序，Top 5 注入第八章。

### Step 5 — CPO 写执行摘要
最后写，但放在文档最前。
原则：**3 句话内涵盖核心结论**——市场机会、商业回报、推荐建议。

### Step 6 — COO 审核
检查清单：
- [ ] 篇幅 ≤ 15 页
- [ ] 所有数字有引用源（标明 CMO 报告版本号 / CFO 报告版本号 / CTO 报告版本号）
- [ ] 第七章风险与第八章假设不重复（风险=已知问题，假设=未验证前提）
- [ ] 第九章建议与前八章逻辑一致

---

## 输出物

```
deliverables/
└── charter-v1.0.md
    ├── 引用：market-analysis-v1.0.md
    ├── 引用：financial-feasibility-v1.0.md
    ├── 引用：tech-feasibility-v1.0.md
    ├── 嵌入：pre-mortem-report.md
    └── 嵌入：assumption-list.md
```

## 常见失败模式

1. **CPO 在 CDCP 阶段就开始写 Charter** → CDCP 还没通过的项目不应有 Charter
2. **Charter 包含技术实现细节** → 那是 PRD 的职责，违反"投资文件"定位
3. **关键假设清单为空** → 不可能没有假设，要么没识别，要么伪装成事实
4. **跳过 pre-mortem 直接交 COO** → 第七章风险只有正向列表，盲点未挖
