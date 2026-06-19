# 优化 GoalPro `goal` Skill 的目标

## Goal Contract

### Goal

优化 GoalPro 的 `goal` Skill，使它在 Codex 和 Claude Code 中都能更稳定地把模糊、战略性、多步骤或证据不足的请求，转成可执行、可验证、可暂停的 Goal Contract。

### Intent

用户真正要的不是再写一份更长的提示词，而是让这个 Skill 在真实使用中减少三类失败：

- 把表面请求当真实意图，导致执行方向错。
- 写出看似完整但不可验收的目标，导致 Agent 假完成。
- 为了显得专业堆流程、来源、agent、eval 或复杂目录，反而增加跑偏成本。

### Strategic outcome

优化完成后，GoalPro 应该成为一个能稳定约束后续 Agent 执行的目标生成协议：

- 普通任务能快速给出清楚的执行目标。
- 战略任务会先要求 Fetch / deep research，而不是直接下结论。
- 大改或重构会先要求 inventory、影响面和分片验证。
- 修复跑偏时能指出旧目标错在哪里，并给出更小、更硬的修正版。
- Codex 与 Claude Code 两套 Skill 保持一致。

### Decision standard

优先级如下：

1. 意图完成度：是否抓住用户真正要推进的结果。
2. 成败可判：是否能判断做到了还是没做到。
3. 证据质量：战略、外部事实、社区信号是否有来源、反证和信心等级。
4. 执行约束：是否写清先读什么、做什么、不做什么、何时停。
5. 兼容性：Codex 与 Claude Code 使用同一套核心规则。
6. 表达经济：只删空话，不删判断、边界、证据和验收。

不得把“缩短提示词”当核心目标。

### Evidence standard

下一轮优化前必须读取：

- `README.md`
- `AGENTS.md`
- `CLAUDE.md`
- `.agents/skills/goal/SKILL.md`
- `.claude/skills/goal/SKILL.md`
- `.agents/skills/goal/references/source-rules.md`
- `.agents/skills/goal/references/examples.md`

如果优化涉及当前平台能力、官方规范、GitHub / X / Reddit 社区实践，必须先补 Fetch，并把来源分为：

- 官方文档
- GitHub 项目或 discussion
- Reddit 真实反馈
- X 实践信号
- 本地项目证据

社区来源只能作为候选信号，必须被官方文档、本地证据或多来源重复信号支撑后，才进入最终规则。

### Scope

本轮优化可以包含：

- 调整 `SKILL.md` 的触发说明、工作顺序、字段标准、输出模式、验收清单。
- 调整 `references/source-rules.md` 的方法依据、来源权重、反模式。
- 调整 `references/examples.md` 的示例，让关键场景更可执行。
- 同步 Codex 与 Claude Code 两套 Skill。
- 必要时更新 README / AGENTS / CLAUDE 中与 Skill 行为不一致的说明。

### Non-goals

本轮不做：

- 不新增 agents、evals、commands、MCP 或复杂目录，除非 Fetch 证明缺口真实存在。
- 不把所有方法论塞进 `SKILL.md` 主体。
- 不把付款码、联系方式、README 展示页作为本轮核心优化对象。
- 不改 `.codex/`、`.meta-kim/`、`graphify-out/` 等本机运行产物。
- 不为了显得完整引入无法验证的新机制。

### Context to read first

```text
README.md
AGENTS.md
CLAUDE.md
.agents/skills/goal/SKILL.md
.claude/skills/goal/SKILL.md
.agents/skills/goal/references/source-rules.md
.agents/skills/goal/references/examples.md
```

### Constraints

- 项目正文默认中文，保留必要专业术语。
- Codex 与 Claude Code 两套 Skill 内容必须保持一致。
- `description` 是触发表面，不得写入缩短提示词、压缩表达等次级目标。
- `SKILL.md` 主体保持短；细节放 `references/`。
- 不提交 ignored 目录和本机缓存。
- 修改前先读目标文件当前内容；修改后运行验证。

### Execution policy

按以下顺序执行：

1. Critical：找出当前 Skill 最可能导致跑偏的失败模式。
2. Fetch：读取本地项目材料；如果涉及外部最佳实践，再补官方 / GitHub / Reddit / X 证据。
3. Thinking：判断哪些规则会真实提升意图完成度，哪些只是装饰。
4. Inventory：列出要改的文件、每个文件承担的角色、同步关系和验证方式。
5. Execution：小批量修改，优先修最影响触发、成败标准、证据标准和验收的内容。
6. Review：检查有没有过度设计、触发污染、示例不可执行、字段不可判。
7. Verification：运行一致性、空白、图谱、git 状态检查。

### Checkpoints

1. **目标确认**：输出本文件，确认下一轮优化边界。
2. **现状盘点**：列出当前 Skill 的强项、缺口、反模式风险。
3. **改动计划**：明确改哪些文件、为什么改、如何验证。
4. **小批量修改**：先修核心规则，再修 references，再修 examples。
5. **一致性检查**：Codex / Claude Code 两套文件哈希一致。
6. **最终验收**：验证通过后提交 git，并说明剩余风险。

### Verification

必须运行或检查：

- `rg -n "description:.*(Token|token|压缩|降低|省)|降低token|降低 Token|低 Token|省 Token" -uu README.md AGENTS.md CLAUDE.md .agents .claude`
- Codex / Claude Code 对应文件哈希一致。
- `git diff --check`
- `graphify update . --force`
- `git status --short --ignored`

人工验收标准：

- 目标是否比“优化这个 Skill”更具体。
- 是否能约束下一轮 Agent 不乱改。
- 是否明确什么不做。
- 是否区分本地证据、外部证据、社区信号和验证证据。

### Stop conditions

出现以下情况必须暂停：

- 需要改变 Skill 的定位、名称、触发词或安装路径。
- 需要新增 agents、evals、commands、MCP、hook 或复杂目录。
- 需要删除付款码、联系方式或 README 展示信息。
- 外部来源互相冲突，且会影响核心规则。
- Codex 与 Claude Code 两套 Skill 无法保持一致。
- 验证命令无法运行，且没有替代证据。

### Final report

最终汇报必须包含：

- 改了什么文件。
- 为什么这些改动能提高意图完成度。
- 哪些内容明确没动。
- 验证命令和结果。
- git commit hash。
- 剩余风险或下一步建议。

## Codex `/goal` block

```markdown
/goal
优化 GoalPro 的 `goal` Skill，使它在 Codex 和 Claude Code 中都能更稳定地把模糊、战略性、多步骤或证据不足的请求，转成可执行、可验证、可暂停的 Goal Contract。

Intent:
减少真实使用中的跑偏：不再只复述表面请求，不再写不可验收目标，不再用复杂机制掩盖意图不清。

Strategic outcome:
GoalPro 成为一个稳定的目标生成协议：普通任务能快速成约束，战略任务会先 Fetch，大改会先 inventory，修复跑偏能重写更小更硬的目标。

Decision standard:
意图完成度 > 成败可判 > 证据质量 > 执行约束 > Codex/Claude Code 兼容性 > 表达经济。

Done when:
- `SKILL.md` 的触发说明、工作顺序、字段标准、输出模式和验收清单更能约束真实执行。
- `source-rules.md` 能解释方法依据、来源权重和反模式。
- `examples.md` 覆盖普通任务、战略研究、大改/重构、修复跑偏、Codex `/goal`、Claude Code 任务。
- `.agents` 与 `.claude` 对应文件保持一致。
- README / AGENTS / CLAUDE 与 Skill 行为不冲突。
- 验证命令通过，且 ignored 目录未提交。

Read first:
- README.md
- AGENTS.md
- CLAUDE.md
- .agents/skills/goal/SKILL.md
- .claude/skills/goal/SKILL.md
- .agents/skills/goal/references/source-rules.md
- .agents/skills/goal/references/examples.md

Work in checkpoints:
1. 盘点当前 Skill 强项、缺口和跑偏风险。
2. 列出要改的文件、每个文件职责和验证方式。
3. 小批量修改核心 Skill。
4. 同步 references 和 examples。
5. 检查 Codex / Claude Code 一致性。
6. 运行验证并提交 git。

Pause if:
- 需要改变 Skill 名称、定位、触发词或安装路径。
- 需要新增 agents、evals、commands、MCP 或 hook。
- 需要删除 README 的联系方式或付款码。
- 外部来源冲突且影响核心规则。
- 验证无法运行且没有替代证据。
```
