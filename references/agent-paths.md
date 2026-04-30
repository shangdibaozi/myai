# Agent 记忆与配置路径速查

这里只保留 Cursor 和 VSCode AI 的项目指令、规则与文档位置。

## 推荐默认策略

如果主要在 Cursor 和 VSCode 里使用 AI，把项目通用 AI 记忆和指令统一放在项目根 `AGENTS.md`。它最适合承载长期稳定的项目事实、代码规范、运行命令、测试命令和禁止事项。

不要把 `AGENTS.md` 当私人流水账。临时上下文、个人 TODO、未确认猜测、只对某一次会话有用的信息，不应写进仓库。`.cursor/rules/` 和 VSCode 扩展配置只放工具必须依赖的专属配置，不承载项目 AI 记忆。

## Cursor


| 用途        | 路径                                           |
| --------- | -------------------------------------------- |
| 个人 Skills | `~/.cursor/skills/<name>/SKILL.md`           |
| 项目 Skills | `.cursor/skills/<name>/SKILL.md`             |
| 项目规则      | `.cursor/rules/`                             |
| 项目级指令     | 项目根 `AGENTS.md`                              |
| 会话转录      | Cursor 管理的 agent transcripts（只读参考，不当作项目文档维护） |


Cursor 没有统一暴露给所有环境的"记忆文件 + 索引"机制。同步时只把稳定的项目 AI 记忆和通用指令写进 `AGENTS.md`；面向人的完整说明写进 `README.md` 或 `docs/`；`.cursor/rules/` 只放 Cursor 专属的规则触发、文件匹配或工具配置。

## VSCode AI 扩展


| 用途         | 路径                                                      |
| ---------- | ------------------------------------------------------- |
| 项目通用 AI 指令 | 项目根 `AGENTS.md`                                         |
| 项目文档       | `README.md`、`docs/`                                     |
| 扩展专属规则     | 按具体扩展约定，例如 `.github/copilot-instructions.md` 或扩展自己的配置文件 |


VSCode 里的 AI 扩展生态不完全统一。为了通用，项目级 AI 规则优先维护在 `AGENTS.md`；扩展专属文件只写该扩展独有的行为要求，并尽量指向 `AGENTS.md`，避免重复维护。

## 使用建议

- **项目根优先维护 `AGENTS.md`**，作为 Cursor 和 VSCode AI 的唯一项目 AI 记忆入口
- Cursor 专属配置放 `.cursor/rules/`，只保留规则触发、文件匹配或工具约束；通用项目记忆仍写 `AGENTS.md`
- VSCode 扩展专属文件只写扩展要求的内容，并尽量指向 `AGENTS.md`
- docs/ 和 README 是平台中立的，不需要为 Cursor 和 VSCode 分两份