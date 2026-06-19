## 项目语言

项目正文默认使用中文；保留必要专业术语，例如 Codex、Claude Code、Skill、Goal Contract、Token、README、Graphify。

## 项目目标

GoalPro 是一个 `goal` Skill 项目，用来放大真实意图，并把模糊需求转成战略清楚、可执行、可验证的 Goal Contract。

写作优先级：

1. 放大意图：区分表面请求、真实意图、战略结果和最大跑偏风险。
2. 证据定战略：战略型、外部事实型、高风险任务必须先 deep research；证据不足只能给草案或研究计划。
3. 社区校准：GitHub / X / Reddit 只能作为实践信号；重复出现、能解释真实失败、能被官方或本地证据支撑时才吸收。
4. 标准清楚：说明成败标准、关键边界、证据标准、反证和取舍逻辑。
5. 可执行：让 Codex / Claude Code 知道先读什么、做什么、何时停止、怎么证明完成。
6. Inventory 优先：大改、重构、跨模块任务先列影响面和验证入口，再分片执行。
7. 表达经济：只删空话，不删关键判断、边界和验收。
8. 不把命令跑通当成用户目标完成。

触发规则：

- `SKILL.md` 的 frontmatter `description` 是触发表面，只写使用场景和能力。
- 不把缩短提示词、压缩表达这类次级目标写进 `description`。
- 需要战略判断时，先 Fetch / deep research，再写最终 Goal Contract。
- 需要社区经验时，明确来源类型和采纳理由，不把单个帖子当权威。

## Graphify

本项目有 Graphify 知识图谱，输出在 `graphify-out/`。

规则：

- 代码或项目结构问题，若 `graphify-out/graph.json` 存在，先运行 `graphify query "<问题>"`。
- 查关系用 `graphify path "<A>" "<B>"`，查概念用 `graphify explain "<概念>"`。
- `graphify-out/` 是生成产物，不提交。
- 修改项目文件后，运行 `graphify update .` 更新本地知识图谱。
