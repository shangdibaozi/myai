# Agent 记忆与配置路径速查

这里只保留 Cursor 和 VSCode Copilot 的项目指令、规则与文档位置。

## 推荐默认策略

如果主要在 Cursor 和 VSCode Copilot 里使用 AI，把项目通用 AI 记忆和指令统一放在项目根 `AGENTS.md`。它最适合承载长期稳定的项目事实、代码规范、运行命令、测试命令和禁止事项。

不要把 `AGENTS.md` 当私人流水账。临时上下文、个人 TODO、未确认猜测、只对某一次会话有用的信息，不应写进仓库。`.cursor/rules/` 和 `.github/copilot-instructions.md` 只放工具必须依赖的专属配置，不承载项目 AI 记忆。

## Cursor


| 用途        | 路径                                           |
| --------- | -------------------------------------------- |
| 个人 Skills | `~/.cursor/skills/<name>/SKILL.md`           |
| 项目 Skills | `.cursor/skills/<name>/SKILL.md`             |
| 项目规则      | `.cursor/rules/`                             |
| 项目级指令     | 项目根 `AGENTS.md`                              |
| 会话转录      | Cursor 管理的 agent transcripts（只读参考，不当作项目文档维护） |


Cursor 没有统一暴露给所有环境的"记忆文件 + 索引"机制。同步时只把稳定的项目 AI 记忆和通用指令写进 `AGENTS.md`；面向人的完整说明写进 `README.md` 或 `docs/`；`.cursor/rules/` 只放 Cursor 专属的规则触发、文件匹配或工具配置。

## VSCode Copilot


| 用途         | 路径                                                      |
| ---------- | ------------------------------------------------------- |
| 项目通用 AI 指令 | 项目根 `AGENTS.md`                                         |
| 项目文档       | `README.md`、`docs/`                                     |
| Copilot 专属规则 | `.github/copilot-instructions.md`                         |
| `/myai` prompt file | `.github/prompts/myai.prompt.md`                             |


VSCode Copilot 使用 `.github/copilot-instructions.md` 承载默认行为规则。项目级 AI 规则优先维护在 `AGENTS.md`；Copilot 专属文件只写 Copilot 独有的行为要求，并尽量与 `AGENTS.md` 和 Cursor 规则保持一致，避免重复维护。

## 使用建议

- **项目根优先维护 `AGENTS.md`**，作为 Cursor 和 VSCode Copilot 的唯一项目 AI 记忆入口
- Cursor 的 `/myai` 入口放 `.cursor/skills/knowledge-sync/SKILL.md`
- Cursor 专属配置放 `.cursor/rules/`，只保留规则触发、文件匹配或工具约束；通用项目记忆仍写 `AGENTS.md`
- Copilot 的 `/myai` 入口放 `.github/prompts/myai.prompt.md`
- Copilot 专属配置放 `.github/copilot-instructions.md`，只保留 Copilot 的默认行为规则；通用项目记忆仍写 `AGENTS.md`
- docs/ 和 README 是平台中立的，不需要为 Cursor 和 VSCode 分两份