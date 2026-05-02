# myai

面向 Cursor 和 VSCode Copilot 的项目知识同步仓库。

这套仓库的核心目标是：把 `AGENTS.md` 作为**唯一项目 AI 记忆入口**，并在阶段收尾时通过 `/myai` 把 `AGENTS.md`、`README.md`、`docs/` 和代码事实重新对齐，减少 AI 在跨会话、跨工具协作时的跑偏和信息腐烂。仓库同时为 Cursor 和 VSCode Copilot 提供各自的默认规则文件与 `/myai` 触发入口。

## 仓库内容

- `SKILL.md`：`/myai` 的主执行流程源码。用于阶段收尾时同步 `AGENTS.md`、README、docs 和工具专属配置。
- `.cursor/skills/knowledge-sync/SKILL.md`：给 Cursor 使用的标准 skill 入口。
- `.cursor/rules/myai-core.mdc`：Cursor 的 `alwaysApply` 基础行为规则。用于日常编码时限制 AI 乱猜、过度设计、顺手乱改。
- `.github/copilot-instructions.md`：VSCode Copilot 的基础行为规则。和 Cursor 规则保持同一套核心原则。
- `.github/prompts/myai.prompt.md`：给 VSCode Copilot 使用的 `/myai` prompt file。
- `references/sync-matrix.md`：变更类型到文档修改位置的映射表。
- `references/agent-paths.md`：Cursor / VSCode Copilot 下 `AGENTS.md`、规则文件、README、docs 的分工。
- `references/examples.md`：好的 `AGENTS.md` 条目、坏示例、`/myai` 摘要示例。

## 推荐工作流

1. 平时编码时，让 Cursor 读取 `.cursor/rules/myai-core.mdc`，让 VSCode Copilot 读取 `.github/copilot-instructions.md`。
2. 项目级长期事实、命令、约定、坑点统一维护在 `AGENTS.md`。
3. 人类和下游系统要看的完整说明写在 `README.md` 和 `docs/`。
4. 在 Cursor 中通过 `.cursor/skills/knowledge-sync/SKILL.md` 使用 `/myai`。
5. 在 VSCode Copilot 中通过 `.github/prompts/myai.prompt.md` 使用 `/myai`。

## 核心约定

- 只有 `AGENTS.md` 承载项目通用 AI 记忆。
- `.cursor/rules/` 和 `.github/copilot-instructions.md` 只承载工具专属配置或默认行为，不承载通用项目记忆。
- 文档默认使用中文。
- 代码事实优先于 README / docs，README / docs 优先于 `AGENTS.md`，`AGENTS.md` 优先于工具专属规则文件。

## 使用建议

如果你把这套内容复制到其他仓库，最少带上这三样：

- `SKILL.md`
- `.cursor/skills/knowledge-sync/SKILL.md`
- `.cursor/rules/myai-core.mdc`
- `.github/copilot-instructions.md`
- `.github/prompts/myai.prompt.md`
- `references/`