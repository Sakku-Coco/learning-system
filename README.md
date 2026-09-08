# AI Training Partner — a config-driven learning system for AI agents

> Turn a coding agent into a disciplined personal training partner: error-collection-driven drills, evidence-based skill calibration, layered reviewer personas, and anti-forgetting mechanics. No app, no database — just Markdown rules, a config file, and agent hooks.

**EN summary**: This repo is a framework for running long-term skill training inside an AI-agent IDE (Kiro, Claude Code, Cursor, or any tool that supports custom rule files). The agent follows a written "constitution" (the **core**), while everything personal — subjects, pass thresholds, cadence, known weak patterns — lives in a single **learner config**. Half of the mechanisms exist to fix the three chronic failures of using AI for learning: it forgets you between sessions, it flatters you, and it makes things up. 

---

## 这是什么

一套跑在 AI agent IDE 里的**通用训练框架**。核心思想是把"教练该怎么带人"写成规则文件让 agent 执行，把"带的是谁、练什么"抽成一份配置。两层严格分离：

```
┌─────────────────────────────────────────┐
│  core/（内核·对所有人一样）               │
│  训练引擎规则 · 评审角色说明书 · hooks     │
└──────────────┬──────────────────────────┘
               │ 读取
┌──────────────▼──────────────────────────┐
│  learner-config.md（配置·只有这个是你的） │
│  科目 · 及格线 · 节奏 · 场景域 · 弱点模式  │
└──────────────┬──────────────────────────┘
               │ 驱动
┌──────────────▼──────────────────────────┐
│  tracking/（数据·训练中长出来）           │
│  错题集 · 训练日志 · 校准表 · 断点 · 战绩  │
└─────────────────────────────────────────┘
```

学习者每天对 agent 说"继续训练"，agent 按内核规则报进度、复习旧内容、按配置出题、维护错题集和日志。**人负责练，agent 负责记忆、监督和校准。**

## 它解决什么问题

用 AI 学习最常见的三个失败，这套框架各有对应机制：

| AI 的病 | 对应机制 |
|---------|----------|
| **每次对话都失忆** | 断点文件 + 会话热启动/存档 hooks + 单一每日更新点 |
| **无脑夸人、凭感觉判断你的水平** | 能力校准表：每个等级挂判定证据，调难度必须引用"哪天哪题的表现" |
| **编造听起来很对的知识** | 真实性来源分级：所有事实性内容强制标 ✅可查 / ⚠️通用 / 🔧虚构 |

再加上针对"人"的病的机制：练了就忘（掌握度门槛+新板块前强制复习）、坚持不下去（三档练法+可持续红线）、干了活说不出价值（战绩日志3问）、不知道自己不知道（标杆视角+场景预演）。

完整设计理念见 [docs/design-philosophy.md](docs/design-philosophy.md)。

## 目录结构

```
.
├── core/                          ← 内核（不含任何个人信息，直接用）
│   ├── steering/training-rules.md ← 训练引擎规则（agent的宪法）
│   ├── config/learner-config.md   ← 配置模板（唯一需要你填的文件）
│   ├── frameworks/
│   │   ├── structure-coach.md     ← 🗜️结构教练：五步法+四把尺子（管开口第一秒）
│   │   └── communication-mentor.md← 🎓沟通导师：6维度评分+两轮审视（管语言层）
│   └── hooks/                     ← 3个agent hooks（热启动/存档/检查关卡）
├── templates/                     ← tracking 数据文件的空模板（7个）
├── examples/
│   └── data-analyst-career-switch/← 匿名化真实配置（跑了60+天）+ 机制演化时间线
└── docs/
    ├── design-philosophy.md       ← 每个机制治什么病 + 试过但删掉的反模式
    └── getting-started.md         ← 三步搭建指南
```

## 快速开始

1. `core/` 整个复制进你的 agent 规则/hooks 目录
2. 填 `learner-config.md`（照着 `examples/` 里的真实示例填），把 `templates/` 复制成你的 `tracking/`
3. 对 agent 说："我们开始第一次训练。先采访我，建立档案和校准表，然后出1道定位题探底。"

详细步骤和常见坑见 [docs/getting-started.md](docs/getting-started.md)。

## 设计上最重要的三个决定

1. **规则不靠 AI 自觉，靠机制强制**——最关键的一个 hook 在每条消息前把5问检查关卡注入上下文，把规则从"静态文件"变成"每回合的活性约束"
2. **证据链贯穿一切**——调难度要证据、立弱点模式要≥3个场景的重复证据、评审诊断要能引用错题集条目；人和 AI 对"我现在什么水平"有一份可审计的共识
3. **内核和配置分离**——机制是通用的，参数是个人的；换一个人、换一批科目，只改配置不改内核

## License

MIT
