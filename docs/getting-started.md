# Getting Started — 三步搭建指南

> 前提：你在用一个支持"自定义规则文件 + hooks"的 AI agent IDE（Kiro、Claude Code、Cursor 等）。下面以通用步骤描述，各家的规则目录名不同，对号入座即可。

## 第 1 步：铺目录

```
your-workspace/
├── <agent规则目录>/              # Kiro: .kiro/steering/   Claude Code: CLAUDE.md 或 .claude/
│   └── training-rules.md        # ← core/steering/ 原样复制，不用改
├── <agent hooks目录>/            # Kiro: .kiro/hooks/
│   ├── pre-action-checklist.json
│   ├── session-warm-start.json
│   └── end-of-session.json      # ← core/hooks/ 原样复制
└── tracking/
    ├── learner-config.md        # ← core/config/ 模板复制后【填你自己的】
    ├── 00-dashboard.md          # ← 以下全部从 templates/ 复制
    ├── training-log.md
    ├── error-collection.md
    ├── expression-structure-collection.md
    ├── study-notes.md
    ├── last-session-context.md
    ├── weekly-wins.md
    └── reference/
        ├── structure-coach.md        # ← core/frameworks/ 原样复制
        └── communication-mentor.md
```

**只有 `learner-config.md` 需要填写**，其他文件要么原样用，要么由训练自动长出内容。

## 第 2 步：填配置

打开 `tracking/learner-config.md`，8 个小节逐个填。

填写建议：
- **第2节科目**：先只放 1-2 个核心科目。科目多了前两周会顾此失彼，跑顺后再加
- **第3节及格线**：不确定就用示例值（7/10 + 连续2次），这是实测过的
- **第4节角色开关**：**起步时建议只开🎓沟通导师**，结构教练等你攒了一些表达样本后再开
- **第8节弱点模式**：留空。这个表由错题集慢慢长出来，一开始填是拍脑袋

## 第 3 步：第一次会话

对 agent 说：

> 我们开始第一次训练。先读 tracking/learner-config.md，然后采访我补全档案，建立能力校准表的初始行，再出 1 道定位题探底。

之后每天只需要说"**继续训练**"。

## 日常节奏（参考）

| 频率 | 动作 | 更新的文件 |
|------|------|-----------|
| 每天 | "继续训练" → 练核心项 | training-log.md（唯一每日更新点） |
| 会话结束 | "结束会话" | last-session-context.md |
| 每周固定日 | 写战绩日志（3件事×3问） | weekly-wins.md |
| 每周 | 小结 + 各文件一致性核对 | 00-dashboard.md |
| 每月 | 能力校准表通盘重打分 | training-log.md 顶部 |

## 常见坑

1. **规则写了 agent 不执行** → 检查 pre-action-checklist hook 是否生效；规则太长时把最重要的 5 条做成检查关卡
2. **agent 又开始凭感觉夸你** → 引用规则反问它："证据是哪天哪题？"——校准表机制需要你前几周帮 agent 养成习惯
3. **tracking 文件开始互相矛盾** → 回到"单一每日更新点"，其他文件降为周更
4. **一次开满所有机制觉得规则在打架** → 收缩到三件套：错题集驱动 + 热启动/存档 + 采访先行，跑顺再逐个加
5. **坚持不下去** → 启用三档练法，状态差的日子完成 10 分钟底线档就算赢
