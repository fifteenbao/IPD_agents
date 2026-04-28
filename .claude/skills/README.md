---
name: Skills 索引
description: 智能硬件 IPD 体系的可复用框架/模板层。skill 不持有角色身份，只承载方法论，可被任意 agent 引用。
---

# Skills 索引

skill 是**可复用的框架/模板**，不绑定角色，不内嵌于 agent。任何 agent 在执行任务时都可引用 skill。

## 何时新增 skill
- 多个 agent 都用得上的方法论（如 pre-mortem、stakeholder-map）
- 长模板（如 Charter、PRD）—— 抽出后 agent 文件更精炼
- 行业标准框架（KANO、OST、JTBD）—— 与外部对齐

## 何时不新增 skill
- 单个 agent 内部、低频使用的逻辑
- 一次性的项目检查表

---

## 当前 skill 列表

### 跨域通用（cross-functional）
| Skill | 说明 | 主要使用方 |
|-------|------|-----------|
| [pre-mortem](pre-mortem.md) | 反向推演项目失败原因，DCP/TR 评审前必跑 | COO、Board、PM |
| [opportunity-solution-tree](opportunity-solution-tree.md) | Teresa Torres OST，从用户增量时间映射到方案与实验 | CMO ↔ CPO |
| [assumption-prioritization](assumption-prioritization.md) | 识别+排序关键假设，硬件验证成本高时尤其重要 | 全员，CTO/CFO 主用 |
| [stakeholder-map](stakeholder-map.md) | Power/Interest 矩阵，IPMT 内部博弈与外部沟通策略 | CEO、CMO |
| [job-stories](job-stories.md) | JTBD 风格用户故事，比传统 US 更适合硬件场景 | CPO、CMO |

### 市场域（market）
| Skill | 说明 | 主要使用方 |
|-------|------|-----------|
| [kano-model](kano-model.md) | 必备/期望/魅力/反向需求分层 | CMO |

### 产品域（product）
| Skill | 说明 | 主要使用方 |
|-------|------|-----------|
| [charter-template](charter-template.md) | 立项报告模板，PDCP 评审材料 | CPO |
| [prd-template](prd-template.md) | 产品需求文档模板，研发执行依据 | CPO |

### 治理域（governance）
| Skill | 说明 | 主要使用方 |
|-------|------|-----------|
| [dcp-scoring-rubric](dcp-scoring-rubric.md) | DCP 五维评分（25 分制）+ 一票否决清单 | Board |

---

## Skill 文件格式

每个 skill 文件需包含：
```yaml
---
name: skill-name
description: 一句话说明，决定何时被检索/引用
domain: cross | market | finance | product | tech | governance | pm
inputs: 该 skill 需要哪些输入
outputs: 产出什么
when-to-use: 触发条件
---
```
正文使用清晰的章节结构，提供模板/检查表/计算公式。
