# creater-agent — 智能硬件 IPD 多 Agent 协作体系

> 把华为 IPD（集成产品开发）流程与现代企业治理结构融合，在AI时代背景下，专为智能硬件产品**从立项到量产**的全周期协作设计。

## 这是什么

一个跑在 Claude Code 上的多 agent 体系。当你想做一款智能硬件产品时，它会扮演 **Board / CEO / COO / CTO / CMO / CFO / CPO / PM** 八个角色，按照 IPD 决策门（CDCP → PDCP → TR1-6 → GA）协作推进，并在每个关键节点产出可被投资委员会审阅的标准化文件。

它不是一个"AI 助手"，而是一支**有职责分工、有制衡机制、有工作流的 AI 团队**。

---

## 时代命题（为什么要做这件事）

AI 正系统性压缩白领工作时间，**人均可支配时间结构性增加且不可逆**。这部分增量时间不会回流到屏幕里——数字娱乐已接近饱和——而更可能流向线下与身体参与的活动：跑步、爬山、园艺、养宠、手工艺，以及任何以慢节奏回馈与可量化进步为核心的体验。

在这种时代结构下，智能硬件的角色是“体验基础设施”：在现实活动与长期习惯之间建立可被量化、可被理解的桥梁。它通过可靠的传感、直观的反馈、与设计良好的积累路径来降低进入门槛，让用户看见成长的痕迹，从而把零散的时间转化为有意义的练习与社交资本。

更深一层的命题是：如果有一天 AI 可以替代大量认知劳动与工具性任务，人类“还剩下什么”？我们的回答不是回避技术进步，而是识别并放大那些机器难以替代的方面：身体性（感受、技艺、汗水）、关系性（照料、共同体、教学）、叙事性（意义的构建与传承）、审美与判断（价值选择与风格）。这些是慢、模糊、有层次感的体验，正好与线下活动与可穿戴/环境硬件的价值相契合。

因此，本体系设计决策的锚点并非“把更多工作自动化”，而是“把人从机械重复中解放出来，让人有更多真实体验可供塑造与度量”。我们的 agent 在每一步分析与建议时，都以这一张力为中心：如何用技术去放大人的能动性、维护体验的丰饶、并在商业上寻找可持续的积累路径。

详见 [`.claude/agents/SOUL.md`](.claude/agents/SOUL.md) 的"时代命题"章节。

---

## 三层架构

```
┌─────────────────────────────────────────┐
│ Agent 层（角色身份）— 谁来做              │
│   Board / CEO / COO / CTO / CMO         │
│   CFO / CPO / PM                        │
└────────────────┬────────────────────────┘
                 │ 引用
                 ▼
┌─────────────────────────────────────────┐
│ Skill 层（可复用方法论）— 怎么做           │
│   pre-mortem / OST / KANO / Charter…    │
└────────────────┬────────────────────────┘
                 │ 编排
                 ▼
┌─────────────────────────────────────────┐
│ Command 层（端到端工作流）— 何时跑       │
│   /cdcp-review、/pdcp-review、…         │
└─────────────────────────────────────────┘
```

| 层 | 触发方式 | 文件位置 |
|----|---------|---------|
| Agent | 任务匹配自动调用 | `.claude/agents/` |
| Skill | Agent 内部引用 | `.claude/skills/` |
| Command | 用户显式 `/command` | `.claude/commands/` |

设计原则：**角色 ≠ 方法论**。CMO 是身份，KANO 是方法。把 KANO 焊在 cmo.md 里，会让其他 agent 无法复用。

---

## 组织架构与权力体系

```
用户（董事长）
    │
    ▼
Board / IPMT（战略决策层）
    │  DCP 投资决策、资源授权
    ▼
CEO / 主控（执行编排层）
    │  制定执行方案、跨域协调
    ▼
COO / 守门（审核把关层）  ← 有权打回 CEO 方案
    │  方案完整性、可行性、风险覆盖
    ▼
C-Level 执行层
   CTO（技术）  CMO（市场）  CFO（财务）
   CPO（产品）  PM（项目管理）
```

**制衡类比**：
- CEO （草拟方案）
- COO（审核驳回）
- Board/IPMT（最终裁决）

---

## IPD 阶段 × Agent 协作

| 阶段 | 决策门 | 主导 Agent | 输入提供 | 审核 |
|-----|--------|-----------|---------|------|
| 概念 | CDCP | CEO | CMO + CFO + CTO | COO → Board |
| 计划 | PDCP | CPO | CPO（Charter+PRD） + CTO + CFO | COO → Board |
| 开发 | TR1-4 | CTO | PM + CTO | COO |
| 验证 | TR5-6 | CTO | CTO + PM | COO → Board |
| 发布 | GA | CEO | PM | Board |
| 生命周期 | — | PM | CMO | CEO |

---

## 快速开始

### 1. 克隆并打开
```bash
git clone <repo-url> creater-agent
cd creater-agent
```

### 2. 用 Claude Code 进入此目录
本体系完全跑在 Claude Code 之上，不需要额外依赖。打开 Claude Code 切到本目录即可，agent 与 skill 会被自动识别。

### 3. 创建你的项目
在 `projects/` 下建立子目录（参见 [projects/README.md](projects/README.md)）：
```bash
mkdir -p projects/my-product
```

### 4. 启动 IPD 流程
向 Claude Code 发起请求，例如：
- "我想做一款 {新品类}，跑一遍 CDCP 评审" → 触发 `/cdcp-review`
- "把 CDCP 的输出整合成 Charter" → 触发 `/write-charter`
- "做 PDCP 评审" → 触发 `/pdcp-review`

CEO 会先制定执行计划，按角色分发给 C-Level，最终经 COO 审核后由 Board 评分决策。

---

## 目录结构

```
creater-agent/
├── README.md                    ← 本文件
├── .gitignore
├── .claude/
│   ├── agents/                  ← 角色身份层（8 个 + SOUL 总图）
│   │   ├── SOUL.md              ← 体系总图、时代命题、权力结构
│   │   ├── board.md             ← Board/IPMT 战略决策
│   │   ├── ceo.md               ← CEO/主控 执行编排
│   │   ├── coo.md               ← COO/守门 审核把关
│   │   ├── cto.md               ← CTO/技术
│   │   ├── cmo.md               ← CMO/市场
│   │   ├── cfo.md               ← CFO/财务
│   │   ├── cpo.md               ← CPO/产品
│   │   └── pm.md                ← PM/项目管理
│   ├── skills/                  ← 可复用方法论层
│   │   ├── README.md            ← skill 索引
│   │   ├── pre-mortem.md
│   │   ├── opportunity-solution-tree.md
│   │   ├── assumption-prioritization.md
│   │   ├── stakeholder-map.md
│   │   ├── job-stories.md
│   │   ├── kano-model.md
│   │   ├── charter-template.md
│   │   ├── prd-template.md
│   │   └── dcp-scoring-rubric.md
│   └── commands/                ← 端到端工作流层
│       ├── README.md            ← command 索引
│       ├── cdcp-review.md
│       ├── pdcp-review.md
│       └── write-charter.md
└── projects/                    ← 你的项目实例（已在 .gitignore）
    └── README.md                ← 用法说明
```

---

## 设计借鉴

本体系的**三层架构**（agent / skill / command）受 [phuryn/pm-skills](https://github.com/phuryn/pm-skills) 启发，但聚焦智能硬件 IPD 而非通用 SaaS PM：

| 维度 | phuryn/pm-skills | creater-agent |
|------|------------------|---------------|
| 适用场景 | 数字产品/SaaS PM 通用 | 智能硬件 IPD 全周期 |
| 流程脊梁 | 平铺的 PM 域（discovery / execution / GTM） | IPD 阶段轴（CDCP→PDCP→TR1-6→GA） |
| 治理结构 | 无 governance 层 | 三省制衡（CEO / COO / Board） |
| 硬件特化 | 无 | BOM / 认证 / EVT-DVT-PVT / 模具 / 长交期器件 |

跨域 skill（pre-mortem / OST / assumption-prioritization / stakeholder-map / job-stories）是从 pm-skills 借鉴并按硬件场景重写的版本。

---

## 扩展路线（roadmap）

- [ ] `/tr-review` — TR1-6 技术评审 command
- [ ] `/write-prd` — 独立的 PRD 生成 command
- [ ] `/pre-launch-check` — GA 前发布就绪检查
- [ ] 抽取 CFO 的 BOM / NPV-IRR 模板为独立 skill
- [ ] 多语言支持（当前仅中文）

欢迎通过 PR 贡献新的 skill / command。

---

## 许可

[MIT License](LICENSE)。可自由使用、修改、分发，包括商用。如使用本体系产出商业产品，欢迎在 README 中署名引用本仓库。
