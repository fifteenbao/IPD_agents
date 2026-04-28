---
name: Commands 索引
description: 智能硬件 IPD 体系的工作流编排层。command 是用户触发的端到端流程，按序串联多个 skill 与 agent。
---

# Commands 索引

command 是**显式触发的工作流**，按顺序调用一组 skill 与 agent，对应 IPD 中的关键决策点或交付动作。

## Command vs Skill vs Agent

| 层级 | 角色 | 触发方式 |
|------|------|---------|
| **Agent** | 角色身份（CMO、CTO…） | 任务匹配自动调用 |
| **Skill** | 可复用方法论/模板 | Agent 内部引用 |
| **Command** | 端到端工作流 | 用户显式调用 `/command-name` |

---

## 当前 command 列表

### 决策评审类（DCP）
| Command | 触发场景 | 编排链路 |
|---------|---------|---------|
| [/cdcp-review](cdcp-review.md) | 概念阶段决策评审 | CMO → CFO → CTO → COO → Board |
| [/pdcp-review](pdcp-review.md) | 计划阶段决策评审 | CPO（Charter+PRD）→ CTO → CFO → COO → Board |

### 文档生成类
| Command | 触发场景 | 编排链路 |
|---------|---------|---------|
| [/write-charter](write-charter.md) | 立项报告生成 | CMO + CFO + CTO 输入 → CPO 整合 |

---

## 待补充（roadmap）

- `/tr-review` — TR1-6 技术评审：CTO 主导 + PM 协同 + COO 审核
- `/write-prd` — PRD 生成：CPO 主导，引用 prd-template + job-stories
- `/pre-launch-check` — GA 前发布就绪检查
- `/lifecycle-monitor` — 上市后市场反馈聚合

---

## Command 文件格式

```yaml
---
name: command-name
description: 这个工作流做什么、何时用
trigger: 用户在什么场景下调用
agents: [涉及的 agent 列表]
skills: [引用的 skill 列表]
output: 最终交付物
---
```
正文按步骤展开：每步说明谁做什么、引用哪个 skill、产出什么、交给谁审核。
