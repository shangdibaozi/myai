# 变更影响矩阵

遇到不确定"这次改动要同步哪些文件"时查这张表。

## 读取范围策略


| 项目规模 / 请求类型     | 推荐读取方式                                                                             |
| --------------- | ---------------------------------------------------------------------------------- |
| 任意项目规模          | 枚举并读取 `README.md`、`AGENTS.md`、`docs/*.md`；同时检查 `.cursor/rules/` 和 `.github/copilot-instructions.md` 是否与 `AGENTS.md` 冲突 |
| 大项目的一次功能收尾      | 仍然全量读取文档；读完后再按下方矩阵判断哪些文件需要改                                                        |
| 跨项目变更           | 每个项目都全量读取 `README.md`、`AGENTS.md` 和 docs，再搜索共享 API、SDK、环境变量、子域、协议名                 |
| 只更新 `AGENTS.md` | 仍需全量读取 README / docs，并抽查相关代码；以代码事实为准，不能只根据聊天记录改项目 AI 指令                            |


## 代码层变更 → 文档层变更


| 本次对话发生的事      | 要改的文件(按受众)                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------- |
| 新增 API / 路由   | `AGENTS.md` 路由清单 · `docs/integration-guide.md` API 速查表 · `docs/architecture.md` Routes 小节   |
| 新增 / 改名 环境变量  | `AGENTS.md` 环境变量表 · `docs/operator-runbook.md` 环境变量章节 · `docs/integration-guide.md`(如果下游要配) |
| 新增数据库表 / 列    | `AGENTS.md` 数据库表 · `docs/architecture.md` Data Model                                        |
| 新增 / 改动 用户流程  | `AGENTS.md` 用户流程 · README 相关命令行示例 · `docs/handoff.md` What Exists Today                     |
| 新增大特性(能跨多文件)  | 以上全部 + `docs/architecture.md` 新增章节 + `docs/handoff.md` 已完成清单                                |
| 新增术语 / 改命名    | `docs/integration-guide.md` 术语表(如果有)+ 全局搜索旧术语替换                                             |
| 部署参数 / 基础设施变化 | `docs/operator-runbook.md` · `AGENTS.md` 部署章节                                               |
| 下游项目接入方式变化    | 下游项目的 `docs/<integration>.md` · 上游项目的 `integration-guide.md`                                |


## 项目 AI 指令变更


| 情况                 | 处理方式                                       |
| ------------------ | ------------------------------------------ |
| `AGENTS.md` 里的过期事实 | 直接改成当前真实状态，并确认 README / docs / 工具专属规则是否也需要同步 |
| 相对时间("今天"、"最近")    | 全部转成绝对日期(`2026-04-29` 而非"今天")              |
| 重复规则(多条说同一件事)      | 合并为一条，以 `AGENTS.md` 为准，Cursor / Copilot 专属文件只保留差异 |
| 已完成的临时待办           | 删除——项目 AI 指令不是历史档案                         |
| 推翻的决策              | 删除旧决策，只保留当前决策                              |
| 跨会话只用一次的临时上下文      | 删除，不写入 `AGENTS.md`、`.cursor/rules/`、`.github/copilot-instructions.md` 或 docs |


## 不要写入的内容

这些内容不要写进 `AGENTS.md`、`.cursor/rules/`、`.github/copilot-instructions.md`、README 或 docs：

- 临时会话记录
- 个人 TODO
- 未确认猜测
- 一次性调试过程
- 只对当前对话有用的上下文
- 与项目无关的个人偏好

## 跨项目影响检查

最容易漏改的场景:

- **上游 API 变了 → 下游 SDK 文档**:协议变化必须两边对齐
- **共享子域 / 路由 / 环境变量改了 → 所有 consumer 项目的 setup 文档**
- **认证中台变更 → 所有接入应用的 integration guide**
- **公共组件 / 基础设施 升级 → 各项目的 operator-runbook 提及版本号的地方**

判断方法:这次改的东西有没有 SDK、子域、共享配置、跨进程协议?有就要在所有依赖项目里搜一遍提到这件事的文档。

## 文档结构通用约定

新增一个能力(API、flow、特性)的标准动作是**四处都补**:

1. **integration-guide / 外部视角文档**:怎么用(curl / SDK 示例 / 错误码)
2. **architecture**:怎么工作(数据流、状态机、设计取舍)
3. **runbook**:怎么运维(冒烟命令、故障排查、环境变量)
4. **handoff / CHANGELOG**:已完成

API 速查表、环境变量表、术语表是高频查询的结构化信息,**必须保持"所见即最新"**。

## 修改优先级

修改顺序固定为：

1. 先改 `docs/` 和 `README.md`，保证人类读者看到的是最新事实
2. 再改 `AGENTS.md`，让 Cursor 和 VSCode Copilot 共享同一份项目 AI 记忆
3. 最后检查 `.cursor/rules/` 和 `.github/copilot-instructions.md`，只修正工具专属配置与 `AGENTS.md` 的冲突，不把通用项目记忆写进去

