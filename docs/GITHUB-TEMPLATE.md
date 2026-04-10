# GitHub 与 Template 发布指南 / GitHub and Template Publishing Guide

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

### 0. 最简单 5 步

1. 在 GitHub 点 `Use this template`
2. 在你自己的仓库里先改 [../content/site.json](../content/site.json)、[../content/profile.json](../content/profile.json)、[../content/pages/home.json](../content/pages/home.json)
3. push 到你自己的仓库
4. 在 Vercel 选择该仓库并部署

可选补充（仅在你想本地预览时）：

```bash
git clone <你的仓库地址>
cd <你的仓库名>
npm ci
npm run dev
```

### 1. 根目录哪些文件要提交到 GitHub

要提交。下面这些文件属于项目配置，用户下载后需要它们才能正常运行：

- [../package.json](../package.json)
- [../package-lock.json](../package-lock.json)
- [../next.config.mjs](../next.config.mjs)
- [../eslint.config.mjs](../eslint.config.mjs)
- [../postcss.config.mjs](../postcss.config.mjs)
- [../tailwind.config.ts](../tailwind.config.ts)
- [../tsconfig.json](../tsconfig.json)
- [../proxy.ts](../proxy.ts)
- [../edgeone.json](../edgeone.json)
- [../next-env.d.ts](../next-env.d.ts)
- [../.nvmrc](../.nvmrc)
- [../.env.example](../.env.example)

一句话判断：只要是“项目运行或构建需要的配置文件”，就应该提交。

### 2. 哪些文件不要提交

这些文件应该留在本地，不要进仓库：

- `.env`
- `.env.local`
- `node_modules`
- `.next`
- `out`
- `dist`
- 编辑器临时文件（`.DS_Store`、`.swp` 等）

这些规则已经在 [../.gitignore](../.gitignore) 里配置。

### 3. `.gitignore` 现在是否齐全

当前项目的忽略规则是可用的，覆盖了常见本地产物和缓存目录。

补充说明：

- [../next-env.d.ts](../next-env.d.ts) 建议提交到仓库
- 本仓库已调整为不再忽略该文件

### 4. 如何把仓库设置成 GitHub Template

在 GitHub 仓库网页操作：

1. 打开仓库 `Settings`
2. 在 `General` 页面找到 `Template repository`
3. 勾选 `Template repository`
4. 保存

完成后，用户可以通过 `Use this template` 创建自己的仓库副本。

### 5. GitHub 建议设置

建议按下面配置：

1. `Settings > General`
: 仓库描述写清楚用途（双语主页模板、内容文件驱动）

2. `Settings > Branches`
: 保护默认分支，至少开启 PR 合并

3. `Settings > Actions > General`
: 允许仓库工作流运行（如果你要用自动更新）

4. `Settings > Actions > Workflow permissions`
: 选择 `Read and write permissions`（自动写回内容需要）

5. `Settings > Features`
: 建议开启 `Issues`，用于收集模板使用问题

### 6. workflows 要不要说明

要说明，而且建议在 README 和 docs 都给链接。

原因：

- 用户需要知道自动提交从哪里来
- 用户需要知道如何关闭自动更新
- 用户需要知道工作流会改哪些文件

可直接参考：

- [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)
- [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml)

### 7. 用户拿到模板后怎么改

给用户的最短路径：

1. 先改 [../content/site.json](../content/site.json)
2. 再改 [../content/profile.json](../content/profile.json)
3. 再改 [../content/pages/home.json](../content/pages/home.json)
4. 再改研究/成果/项目等内容文件
5. 最后跑 `npm run lint` 和 `npm run build`

完整说明看：

- [CONTENT-MANAGEMENT.md](./CONTENT-MANAGEMENT.md)
- [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md)

---

<a id="en-start"></a>

### 0. Simplest 5-step path

1. Click `Use this template` on GitHub
2. Edit [../content/site.json](../content/site.json), [../content/profile.json](../content/profile.json), and [../content/pages/home.json](../content/pages/home.json) in your own repository
3. Push to your own repository
4. Choose that repository in Vercel and deploy

Optional (only if you want local preview):

```bash
git clone <your-repository-url>
cd <your-repository-name>
npm ci
npm run dev
```

### 1. Which root files should be committed

Commit them. These files are required for running and building the project:

- [../package.json](../package.json)
- [../package-lock.json](../package-lock.json)
- [../next.config.mjs](../next.config.mjs)
- [../eslint.config.mjs](../eslint.config.mjs)
- [../postcss.config.mjs](../postcss.config.mjs)
- [../tailwind.config.ts](../tailwind.config.ts)
- [../tsconfig.json](../tsconfig.json)
- [../proxy.ts](../proxy.ts)
- [../edgeone.json](../edgeone.json)
- [../next-env.d.ts](../next-env.d.ts)
- [../.nvmrc](../.nvmrc)
- [../.env.example](../.env.example)

Rule of thumb: if a file is needed for build/runtime configuration, commit it.

### 2. Which files should not be committed

Keep these local:

- `.env`
- `.env.local`
- `node_modules`
- `.next`
- `out`
- `dist`
- editor temp files (`.DS_Store`, `.swp`, etc.)

These are already covered by [../.gitignore](../.gitignore).

### 3. Is `.gitignore` complete

The current ignore rules are practical and cover common local artifacts and caches.

Additional note:

- [../next-env.d.ts](../next-env.d.ts) should be committed for this project
- this repository has been updated to stop ignoring that file

### 4. How to turn this repository into a GitHub Template

In the GitHub repository UI:

1. Open `Settings`
2. In `General`, find `Template repository`
3. Enable `Template repository`
4. Save

After this, users can create their own repository via `Use this template`.

### 5. Recommended GitHub settings

1. `Settings > General`
: keep a clear repository description

2. `Settings > Branches`
: protect the default branch and require PR merge

3. `Settings > Actions > General`
: allow workflows if you need auto updates

4. `Settings > Actions > Workflow permissions`
: use `Read and write permissions` for content write-back workflows

5. `Settings > Features`
: enable `Issues` for user support

### 6. Should workflows be documented

Yes.

Users need to know:

- where auto commits come from
- how to disable automation
- which files are updated by workflows

References:

- [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)
- [../.github/workflows/update-content.yml](../.github/workflows/update-content.yml)

### 7. What users should edit first

Minimal path for users:

1. [../content/site.json](../content/site.json)
2. [../content/profile.json](../content/profile.json)
3. [../content/pages/home.json](../content/pages/home.json)
4. research/publications/projects content files
5. run `npm run lint` and `npm run build`

Full guides:

- [CONTENT-MANAGEMENT.md](./CONTENT-MANAGEMENT.md)
- [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md)
