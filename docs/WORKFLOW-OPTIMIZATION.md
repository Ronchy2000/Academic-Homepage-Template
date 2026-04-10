# 可选自动化指南 / Optional Automation Guide

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

### 1. 自动化会改哪些内容

- [../content/updates.json](../content/updates.json)
- [../content/projects.json](../content/projects.json)

工作流文件： [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml)

脚本文件：

- [../scripts/update-recent-updates.mjs](../scripts/update-recent-updates.mjs)
- [../scripts/update-project-stars.mjs](../scripts/update-project-stars.mjs)

### 2. 什么时候开，什么时候不开

建议开启：

- 你经常提交代码，想自动更新首页动态
- 你希望项目 stars 自动刷新

建议关闭：

- 你希望所有内容都手动维护
- 你不希望自动提交

### 3. 前置条件

- 仓库在 GitHub
- GitHub Actions 已启用
- `github.token` 有 `contents: write` 权限

### 4. 触发方式

- 定时触发
- 手动触发（workflow_dispatch）

### 5. 脚本行为

Recent Updates 脚本： [../scripts/update-recent-updates.mjs](../scripts/update-recent-updates.mjs)

- 读取近期提交
- 写入 [../content/updates.json](../content/updates.json)

项目 stars 脚本： [../scripts/update-project-stars.mjs](../scripts/update-project-stars.mjs)

- 读取项目里的 GitHub 仓库链接
- 回写 `metrics.stars`

本地执行 recent updates 示例：

```bash
GITHUB_REPOSITORY=your-name/your-repo node scripts/update-recent-updates.mjs
```

### 6. 常见问题

问题：工作流运行了但没有新提交  
原因：内容没有变化。  
处理：无需操作。

问题：Recent Updates 同步失败  
处理：检查 `GITHUB_REPOSITORY`、仓库可访问性、Actions 权限。

问题：某项目 stars 没更新  
处理：检查是否填写有效 GitHub 仓库链接。

问题：不想自动提交  
处理：禁用 [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml)。

---

<a id="en-start"></a>

### 1. What automation updates

- [../content/updates.json](../content/updates.json)
- [../content/projects.json](../content/projects.json)

Workflow file: [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml)

Scripts:

- [../scripts/update-recent-updates.mjs](../scripts/update-recent-updates.mjs)
- [../scripts/update-project-stars.mjs](../scripts/update-project-stars.mjs)

### 2. When to enable or disable

Enable if:

- you commit frequently and want auto-updated recent activity
- you want project stars refreshed automatically

Disable if:

- you want full manual control
- you do not want automation commits

### 3. Requirements

- repository is on GitHub
- GitHub Actions is enabled
- `github.token` has `contents: write`

### 4. Triggers

- schedule
- manual `workflow_dispatch`

### 5. Script behavior

Recent updates script: [../scripts/update-recent-updates.mjs](../scripts/update-recent-updates.mjs)

- reads recent commits
- writes [../content/updates.json](../content/updates.json)

Project stars script: [../scripts/update-project-stars.mjs](../scripts/update-project-stars.mjs)

- reads GitHub repository links in project items
- writes `metrics.stars`

Local example for recent updates:

```bash
GITHUB_REPOSITORY=your-name/your-repo node scripts/update-recent-updates.mjs
```

### 6. Common issues

Issue: workflow runs but no commit  
Cause: no content changes.  
Action: none.

Issue: recent updates sync fails  
Action: check `GITHUB_REPOSITORY`, repository access, and Actions permission.

Issue: stars not updated for one project  
Action: verify the project has a valid GitHub repository URL.

Issue: no bot commits wanted  
Action: disable [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml).
