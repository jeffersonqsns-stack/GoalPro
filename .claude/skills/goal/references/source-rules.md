# Goal Skill 方法依据

这个文件只在改进 Skill、解释方法来源、做质量复查时读取。普通使用不要加载。

## 采用的规则

- Goal 是完成契约，不只是提示词：必须写清结果、限制、done-when 和验证证据。
- Skill 的 `description` 是触发表面：只写“何时使用”和“做什么”，不能把次级优化目标写成触发词。
- Skill 正文要短；细节、来源、示例放 `references/`，靠 progressive disclosure 按需加载。
- 战略任务必须先证据后定论：没有 deep research 的战略只能标为草案。
- 复杂研究用 orchestrator-workers 思路拆源、拆观点、拆反证；有清晰评价标准时用 evaluator-optimizer 思路反复修正。
- 评测要拆开：意图识别、证据质量、路线判断、工具选择、执行遵守、最终状态不能混在一起。
- Meta_Kim：Critical -> Fetch -> Thinking -> Execution -> Review -> Verification；先取证再定路线；结构检查不能冒充用户目标完成。

## Deep Research 规则

当任务影响战略、路线、投入、长期标准，或依赖当前外部事实时，必须先做 deep research。

合格的 deep research 不是“搜很多链接”，而是形成可决策的证据地图：

1. 问题定义：这次研究要改变哪个判断。
2. 来源范围：哪些一手/权威/对照资料足以支撑判断。
3. 证据摘取：每条证据只记录与决策有关的 claim。
4. 反证检查：主动找能推翻当前路线的资料。
5. 信心等级：说明高/中/低信心和原因。
6. 决策影响：证据如何改变 Goal 的成败标准、边界或执行路线。

不能因为资料多就升级为“最终战略”。如果缺少关键证据，输出 `Research Plan` 或 `Draft Goal`。

## 质量原则

1. 意图放大优先：不能只复述用户原话，要说清真实意图和战略结果。
2. 完成度优先：成败标准、关键边界、证据路径和取舍逻辑必须清楚。
3. 证据优先：战略和外部事实任务必须有来源、反证、信心等级和决策影响。
4. 表达经济从属：只删空话，不删判断、边界、标准、验证。
5. 每个关键字段必须能判断合格/不合格。
6. 上下文读取只列会改变路线或验收的材料。
7. 验证必须区分：未验证、结构检查、本地验证、线上验证、人工验收。
8. 不因“看起来完整”增加机制；只为防真实失败加规则。

## 来源地图

- YAO Meta Skill: https://github.com/yaojingang/yao-meta-skill
- Agent Skills spec: https://agentskills.io/specification
- Agent Skills best practices: https://agentskills.io/skill-creation/best-practices
- OpenAI Codex prompting and goals: https://developers.openai.com/codex/prompting
- OpenAI Codex follow goals: https://developers.openai.com/codex/use-cases/follow-goals
- OpenAI Codex skills best practices: https://developers.openai.com/codex/skills
- OpenAI Deep Research API: https://developers.openai.com/api/docs/guides/deep-research
- OpenAI Deep Research cookbook: https://developers.openai.com/cookbook/examples/deep_research_api/introduction_to_deep_research_api
- OpenAI Academy Deep Research guide: https://academy.openai.com/public/clubs/work-users-ynjqu/resources/integrating-deep-research-into-your-workflow-2026-05-29
- Claude Code skills: https://code.claude.com/docs/en/skills
- Claude Agent Skills overview: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- Claude Agent Skills best practices: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
- Anthropic skill-creator: https://docs.anthropic.com/en/docs/claude-code/skill-creator
- Anthropic Building Effective Agents: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic agent evaluation: https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- PRISMA 2020: https://www.prisma-statement.org/prisma-2020
- GRADE approach: https://www.gradeworkinggroup.org/

## 来源抽象

- OpenAI Codex goal 文档：goal 要像“完成条件”一样写，包含具体结果、可测标准和验证面。
- OpenAI / Agent Skills / Claude Skills：Skill 触发主要依赖 frontmatter description；description 必须描述使用场景，不能塞次要目标。
- OpenAI Deep Research：适合陌生、高风险、证据密集的任务；输出应带引用、来源元数据和中间检索过程。
- Anthropic agents：复杂研究可拆成多个子问题；有明确评价标准时，应让评估反过来改进结果。
- PRISMA / GRADE：高质量研究要说明为什么做、怎么找、证据有多可靠，以及证据如何支持建议强度。
- Meta_Kim：Critical/Fetch/Thinking/Review 是路线约束；没有 Fetch 的战略判断不能假装完成。

## 反模式

- “做得更好”但没有用户、目标和验收。
- 不做 deep research 就给战略结论。
- 把表达成本写进 `description`，污染触发判断。
- 把缩短提示词当核心目标，牺牲意图放大和战略完成度。
- 列任务很多，却没有最终状态。
- 用户给了文件/错误/截图，却先问一堆问题。
- 小任务要求全仓库阅读。
- 测试通过就说完成，但用户要的行为没有证据。
- 为了显得高级创建 Skill、agent、command、eval。
