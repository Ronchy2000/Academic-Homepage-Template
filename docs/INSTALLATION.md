# 安装指南 / Installation Guide

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

### 1. 先确认环境

- Node 版本看 [../.nvmrc](../.nvmrc)
- 依赖看 [../package.json](../package.json)
- 锁文件看 [../package-lock.json](../package-lock.json)

建议统一 Node `22.x`。

### 2. 首次启动命令

```bash
nvm install
nvm use
npm ci
npm run dev
```

本地地址：`http://localhost:3000`

### 3. `npm ci` 和 `npm install` 怎么选

| 场景 | 命令 |
| --- | --- |
| 只拉代码并运行 | `npm ci` |
| 你改了依赖 | `npm install` |
| 只刷新 lockfile | `npm install --package-lock-only` |

### 4. `npm ci` 失败时怎么处理

常见报错：

- `package.json and package-lock.json are not in sync`
- `Invalid: lock file's ... does not satisfy ...`

处理：

```bash
npm install --package-lock-only
npm ci
```

如果你维护仓库，请提交更新后的 [../package-lock.json](../package-lock.json)。

### 5. 启动后检查

```bash
npm run lint
npm run build
npm run dev
```

### 6. 常见问题

问题：`eslint: command not found`  
原因：依赖没装完。  
处理：重新执行 `npm ci`。

问题：Node 23/24 有 engine warning  
原因：模板基线是 Node 22。  
处理：切回 Node 22。

问题：不知道语言配置在哪改  
处理：改 [../content/site.json](../content/site.json)，说明见 [CONTENT-MANAGEMENT.md](./CONTENT-MANAGEMENT.md)。

---

<a id="en-start"></a>

### 1. Check environment files first

- Node version: [../.nvmrc](../.nvmrc)
- Dependencies and scripts: [../package.json](../package.json)
- Lockfile: [../package-lock.json](../package-lock.json)

Use Node `22.x`.

### 2. First run commands

```bash
nvm install
nvm use
npm ci
npm run dev
```

Local URL: `http://localhost:3000`

### 3. Command choice

| Scenario | Command |
| --- | --- |
| Fresh clone and run | `npm ci` |
| You changed dependencies | `npm install` |
| Refresh lockfile only | `npm install --package-lock-only` |

### 4. If `npm ci` fails

Common errors:

- `package.json and package-lock.json are not in sync`
- `Invalid: lock file's ... does not satisfy ...`

Fix:

```bash
npm install --package-lock-only
npm ci
```

If you maintain the repository, commit updated [../package-lock.json](../package-lock.json).

### 5. Verify startup

```bash
npm run lint
npm run build
npm run dev
```

### 6. Common issues

Issue: `eslint: command not found`  
Cause: dependencies not installed.  
Fix: run `npm ci` again.

Issue: engine warning on Node 23/24  
Cause: baseline is Node 22.  
Fix: switch to Node 22.

Issue: where to configure locale mode  
Fix: edit [../content/site.json](../content/site.json), details in [CONTENT-MANAGEMENT.md](./CONTENT-MANAGEMENT.md).
