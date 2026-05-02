---
name: myai
description: 执行项目知识同步流程，对齐 AGENTS.md、README、docs 和工具专属规则。
agent: agent
---

执行项目知识同步流程。

严格按以下文件中的规则和流程工作：

- [主流程](../../SKILL.md)
- [变更影响矩阵](../../references/sync-matrix.md)
- [路径与分工](../../references/agent-paths.md)
- [示例](../../references/examples.md)

要求：

1. 读取并检查 `AGENTS.md`、`README.md`、`docs/`、`.cursor/rules/`、`.github/copilot-instructions.md`
2. 以代码和配置文件事实为准，不要根据聊天内容猜测
3. 文档默认使用中文
4. 不要把通用项目记忆写进工具专属规则文件
5. 最后按主流程中的摘要模板输出结果

如果用户在 `/myai` 后补充了额外要求，把这些要求当作本次同步的附加约束一起执行。
