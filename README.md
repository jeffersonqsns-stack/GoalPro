# GoalPro

GoalPro 是一个给 Codex 和 Claude Code 共用的 `goal` Skill 项目。

它的核心作用是：放大并锁定真实意图，把模糊、宏大、容易跑偏的需求，整理成战略清楚、可执行、可验收、适合编码智能体执行的 Goal Contract。

说人话就是：先把“我要什么、做到什么算完、哪些不能做、怎么验证”讲清楚，再让智能体动手，减少瞎做、过度规划、假装完成。

本项目的质量重点是战略意图完成度：先把真实意图、证据标准、成败边界和执行验收讲清楚，再做表达经济。

- 先放大真实意图，不只复述用户原话。
- 战略型任务必须先 deep research；没有证据只能给草案，不能给最终战略。
- 先讲清成败标准、关键边界、证据标准、反证和取舍逻辑。
- 复杂代码任务先做影响面 inventory，再分片执行和验证。
- GitHub、X、Reddit 的经验只作社区信号，必须交叉验证后吸收。
- 表达压缩只能删除空话，不能删除关键判断。
- 不用流程包装弥补战略意图不清。

## 项目现在包含什么

```text
AGENTS.md                         Codex 项目说明
CLAUDE.md                         Claude Code 项目说明
.agents/skills/goal/              Codex 使用的 goal Skill
.claude/skills/goal/              Claude Code 使用的 goal Skill
.codex/hooks.json                 Codex 本地 hook 配置
.claude/settings.json             Claude Code 本地 hook 配置
```

其中最重要的是两份 Skill：

- `.agents/skills/goal/SKILL.md`
- `.claude/skills/goal/SKILL.md`

它们内容保持一致，分别服务 Codex 和 Claude Code。

## 这个 Skill 什么时候用

当用户提出这些需求时使用：

- 写一个高质量 goal / prompt
- 把模糊需求变成可执行任务
- 明确意图、范围、验收标准
- 做 deep research 后制定战略或执行目标
- 给大改、重构、跨模块任务制定 inventory 和分片验证计划
- 给 Codex 准备 `/goal`
- 给 Claude Code 准备执行提示词
- 修复之前智能体输出跑偏、太复杂、假完成的问题

## Goal Contract 输出字段和标准

Skill 默认按这个顺序整理任务：

```markdown
Goal:
Intent:
Strategic outcome:
Decision standard:
Evidence standard:
Scope:
Non-goals:
Context to read first:
Constraints:
Execution policy:
Checkpoints:
Verification:
Stop conditions:
Final report:
```

核心字段标准：

- `Goal`：一句话说清任务对象、动作和方向；不写愿景口号。
- `Intent`：写放大后的真实意图；不能只复述用户原话。
- `Strategic outcome`：写完成后局面发生什么变化；不能只写交付物。
- `Decision standard`：写路线判断、优先级、取舍和失败条件。
- `Evidence standard`：写需要哪些来源、验证、反证和信心等级。
- `Scope`：列本次做什么；避免把未来计划塞进来。
- `Non-goals`：明确不做什么；用来防止过度发挥。
- `Context to read first`：只写会改变执行判断的文件、日志、截图、文档。
- `Execution policy`：大改先 inventory，小改直接做；高风险先问。
- `Constraints`：写硬限制，例如不删除、不发布、不改接口、不泄露密钥。
- `Verification`：写证据类型，例如测试、diff、截图、线上状态、人工验收。
- `Stop conditions`：写必须暂停的风险点。

## 哪些文件不算项目核心

这些通常是本机运行产物或工具缓存，已经放进 `.gitignore`：

- `graphify-out/`：Graphify 生成的知识图谱输出
- `.meta-kim/`：Meta_Kim 当前运行状态、缓存、临时记录
- `.codex/`：Codex 本机 hook、绝对路径配置和排障脚本
- Python / Node 的缓存、虚拟环境、构建输出
- `.env`、编辑器配置、系统临时文件

注意：忽略不是删除。文件还在本机，只是以后不应该当成项目源码提交。

## 维护原则

- 优先改 `SKILL.md` 的触发说明和核心流程。
- 细节、来源、例子放到 `references/`，不要把 `SKILL.md` 写得过长。
- 如果改了 Codex 版本，也要同步 Claude Code 版本。
- `description` 是触发表面，只写使用场景和能力，不写表达成本这种次级目标。
- 战略任务必须先 deep research，证据不足时只能输出草案或研究计划。
- GitHub / X / Reddit 可以补充真实失败模式，但不能替代官方文档、本地证据和验证。
- 表达经济从属于意图完成度，不允许本末倒置。
- 不要因为“看起来完整”就增加复杂机制；只有能防止真实失败时才加规则。
- 最终完成不能只看命令是否跑通，还要看用户目标是否真的达成。

## 当前状态

这个项目目前不是普通应用项目，没有 `package.json`、启动命令或测试框架。

它现在更像一个可复用 Skill 包：核心交付物是 `goal` Skill 本身，以及让 Codex / Claude Code 能正确识别和使用它的项目说明。
