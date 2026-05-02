# 示例

用于说明什么内容适合写进 `AGENTS.md`，什么内容不该写，以及 `/myai` 执行完成后的摘要应该长什么样。

## 好的 `AGENTS.md` 条目

### 运行命令

```markdown
## 运行命令

- 安装：`pnpm install`
- 开发：`pnpm dev`
- 测试：`pnpm test`
- Lint：`pnpm lint`
```

特点：

- 命令真实存在
- 名称清晰
- 没有“可能”“大概”“通常”

### 环境变量

```markdown
## 环境变量

- `DATABASE_URL`：数据库连接串，必需，由部署环境注入
- `OPENAI_API_KEY`：调用 OpenAI 接口时使用，按环境分别配置
```

特点：

- 写变量名、用途、是否必需、来源
- 不写不存在或未验证的变量

### 常见坑

```markdown
## 常见坑

- 本项目使用 `pnpm`，不要用 `npm install`
- 开发环境依赖本地 Redis；不启动时任务队列相关测试会失败
```

特点：

- 必须是已经验证过、重复出现过的问题
- 只保留现在仍然有效的坑

## 不该写进 `AGENTS.md` 的内容

### 反例 1：个人 TODO

```markdown
- 之后可以把认证逻辑重构一下
- 未来也许要把日志系统统一
```

问题：

- 不是当前真实状态
- 会污染项目 AI 记忆
- 容易让后续 AI 把猜测当事实

### 反例 2：一次性上下文

```markdown
- 这次聊天里先不动支付模块
- 刚刚调试发现有个奇怪问题，回头再看
```

问题：

- 只对当前会话有效
- 不是长期项目约定

### 反例 3：未验证猜测

```markdown
- 项目应该是通过 GitHub Actions 部署的
- 搜索接口大概走的是 Elasticsearch
```

问题：

- 没有证据
- 会把 AI 带到错误方向

## `/myai` 摘要示例

```markdown
## 同步完成

### AGENTS.md 变更
- 更新：补充 `运行命令` 和 `环境变量`，与当前代码和 README 对齐
- 删除：移除过期的“计划迁移到 npm”描述

### 文档变更
- `README.md` — 更新安装和启动方式，统一为 `pnpm`
- `docs/architecture.md` — 补充任务队列和 Redis 依赖

### 冲突修复
- `README.md` 写的是 `npm dev`，代码和 `package.json` 实际使用 `pnpm dev`；已统一改为 `pnpm dev`

### 未修改
- `docs/api.md` — 已与当前接口实现一致，无需调整

### 未处理
- 部署流程是否仍依赖旧的 Jenkins 未能从代码直接确认，需要用户确认
```

## 冲突处理示例

### 场景

- `README.md` 写：`npm run dev`
- `package.json` 实际只有 `pnpm dev`
- `AGENTS.md` 也写：`npm run dev`

### 正确处理

1. 以代码和配置文件为准
2. 把 `README.md` 和 `AGENTS.md` 一起改成真实命令
3. 在摘要里说明冲突来源和修复依据

## 改名清理示例

### 场景

把环境变量 `API_BASE_URL` 改成 `APP_API_BASE_URL`

### 正确处理

1. 更新代码中的变量名
2. 更新 `AGENTS.md` 的环境变量章节
3. 更新 README / docs 中的配置示例
4. 搜索旧变量名，确认没有遗漏

