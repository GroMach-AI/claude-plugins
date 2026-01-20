# Gromach Team Vibe - Claude Code 插件集

这是 Gromach 团队的 Claude Code 插件市场，提供标准化的开发工作流工具。

## 概述

本项目采用插件市场结构，目前包含以下插件：

| 插件名称  | 版本  | 描述                                 |
| --------- | ----- | ------------------------------------ |
| git-tools | 1.0.0 | Git 工作流工具：规范化提交和 PR 创建 |

## 安装

### 本地开发测试

使用 `--plugin-dir` 标志加载单个插件进行测试：

```bash
claude --plugin-dir /path/to/claude-plugins/plugins/git-tools
```

### 通过插件市场安装

安装分为两步：先添加插件市场，再安装具体插件。

**第一步：添加插件市场**

通过 GitHub 添加（推荐）：

```
/plugin marketplace add GroMach-AI/claude-plugins
```

或通过本地路径添加：

```
/plugin marketplace add /path/to/claude-plugins
```

**第二步：安装插件**

```
/plugin install git-tools@gromach-team-vibe
```

安装后可使用 `/help` 查看可用命令。

### 卸载

卸载插件：

```
/plugin uninstall git-tools@gromach-team-vibe
```

移除插件市场：

```
/plugin marketplace remove gromach-team-vibe
```

## 插件详情

### git-tools

提供两个核心命令，帮助团队遵循统一的 Git 工作流规范。

#### `/git-tools:commit` - 创建规范化提交

遵循 [Conventional Commits](https://www.conventionalcommits.org/)
格式创建高质量的 Git 提交。

**使用方法：**

```
/git-tools:commit
```

**提交格式：**

```
<type>(<scope>): <description>

[optional body]

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
```

**支持的提交类型：**

| 类型       | 说明                   | Changelog |
| ---------- | ---------------------- | --------- |
| `feat`     | 新功能或特性           | ✅        |
| `fix`      | 错误修复               | ✅        |
| `perf`     | 性能改进               | ✅        |
| `refactor` | 代码重构（无行为改变） | ❌        |
| `docs`     | 文档变更               | ❌        |
| `style`    | 代码格式化             | ❌        |
| `test`     | 测试相关               | ❌        |
| `chore`    | 日常维护任务           | ❌        |
| `build`    | 构建系统或依赖         | ❌        |
| `ci`       | CI/CD 配置             | ❌        |

**示例：**

```
feat(auth): add OAuth2 login support
fix(api): resolve null pointer exception in user service
refactor(core): extract common validation logic
```

#### `/git-tools:pr` - 创建 Pull Request

创建符合团队规范的 GitHub Pull Request。

**使用方法：**

```
/git-tools:pr
```

**PR 标题格式：**

```
<type>(<scope>): <Summary>
```

**验证规则：**

- 摘要必须以大写字母开头
- 摘要不能以句号结尾
- Scope 可选但推荐使用
- 支持 `!` 标记 breaking change
- 支持 `(no-changelog)` 后缀排除 changelog

**推荐的 Scope：**

- `API` - API 相关变更
- `core` - 核心功能
- `editor` - 编辑器相关
- `Node` - Node.js 特定

**示例：**

```
feat(editor): Add dark mode support
fix(API): Handle empty response gracefully
feat!: Remove deprecated authentication method
docs(readme): Update installation instructions (no-changelog)
```

## 安全规则

git-tools 插件内置以下安全措施：

- 禁止提交敏感文件（`.env`、`credentials.json` 等）
- 禁止执行危险的 Git 操作（`--force`、硬重置等）
- 禁止修改 Git 配置
- 禁止跳过 Git hooks

## 贡献

欢迎提交 Issue 和 Pull Request。请确保：

1. 遵循 Conventional Commits 规范
2. PR 标题符合验证规则
3. 更新相关文档

## 许可证

MIT License

## 联系方式

- **团队**: Gromach Team
- **邮箱**: zhengminghui@gromach.com
