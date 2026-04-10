# Optional Automation Guide / 可选自动化指南

这份文档讲的是“要不要开自动化”。如果你只想手动维护内容，可以完全跳过。

## 1. 自动化会改哪些文件

- 首页动态： [../content/updates.json](../content/updates.json)
- 项目星标： [../content/projects.json](../content/projects.json)

工作流文件： [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml)

脚本文件：

- [../scripts/update-recent-updates.mjs](../scripts/update-recent-updates.mjs)
- [../scripts/update-project-stars.mjs](../scripts/update-project-stars.mjs)

## 2. 什么时候建议开启

建议开启：

- 你经常提交代码，想自动更新 Recent Updates
- 你希望项目卡片上的 GitHub stars 自动刷新

建议关闭：

- 你希望所有内容都手动审核后再改
- 你不希望出现自动提交

## 3. 前置条件

- 仓库托管在 GitHub
- GitHub Actions 已启用
- 默认 `github.token` 具备 `contents: write`

默认模板配置不需要额外 Personal Access Token。

## 4. 触发方式

- 定时触发（schedule）
- 手动触发（workflow_dispatch）

你可以在 GitHub 的 Actions 页面手动执行一次，确认流程是否符合预期。

## 5. 自动更新逻辑说明

### 5.1 Recent Updates

脚本： [../scripts/update-recent-updates.mjs](../scripts/update-recent-updates.mjs)

行为：

- 读取近期提交
- 过滤掉机器人风格提交
- 写入中英文更新到 [../content/updates.json](../content/updates.json)

脚本依赖 `GITHUB_REPOSITORY` 环境变量。GitHub Actions 会自动提供；本地运行时要手动传入。

```bash
GITHUB_REPOSITORY=your-name/your-repo node scripts/update-recent-updates.mjs
```

### 5.2 项目 GitHub Stars

脚本： [../scripts/update-project-stars.mjs](../scripts/update-project-stars.mjs)

行为：

- 扫描项目链接中的 GitHub 仓库地址
- 调用 GitHub API 获取星标数
- 回写到 `metrics.stars`

只有填写了有效 GitHub 链接的项目条目才会被更新。

## 6. 常见自动提交信息

- `chore: refresh updates and project metrics`
- `chore: refresh recent updates`
- `chore: refresh project stars`
- `chore: refresh content data`

## 7. 故障排查

### 问题 1：工作流执行了，但没有新提交

通常是脚本运行后内容没有变化，不会创建空提交。

### 问题 2：Recent Updates 同步失败

检查：

- `GITHUB_REPOSITORY` 是否可用
- 仓库是否可访问
- Actions 权限是否可读取提交记录

### 问题 3：某个项目星标没有更新

检查：

- 项目是否填写了有效 GitHub 仓库链接
- 仓库是否公开，或 token 权限是否足够

### 问题 4：完全不想要自动提交

最简单做法：在 GitHub Actions 中禁用这个工作流。

## English Quick Notes

The automation workflow is optional. It updates:

1. Recent updates feed in [../content/updates.json](../content/updates.json)
2. GitHub stars in [../content/projects.json](../content/projects.json)

If you prefer full manual control, disable [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml).
