# Installation Guide / 安装指南

这份文档给第一次接触仓库的用户使用。目标只有一件事：你能稳定跑起来，并知道报错时该怎么处理。

## 1. 先看这几个文件

- Node 版本： [../.nvmrc](../.nvmrc)
- 依赖与脚本： [../package.json](../package.json)
- 锁文件： [../package-lock.json](../package-lock.json)

建议统一使用 Node `22.x`，这样和 Vercel、EdgeOne 的默认部署基线一致。

## 2. 第一次启动（推荐命令）

```bash
nvm install
nvm use
npm ci
npm run dev
```

本地访问： `http://localhost:3000`

如果你刚刚新增了依赖，或者明确在维护锁文件，请看下面第 4 节。

## 3. `npm ci` 与 `npm install` 怎么选

| 你的场景 | 推荐命令 |
| --- | --- |
| 只是拉代码并启动项目 | `npm ci` |
| 你修改了依赖（增删包、升级版本） | `npm install` |
| 只想刷新锁文件，不真正安装所有依赖 | `npm install --package-lock-only` |

简单记法：

- 普通使用者优先 `npm ci`
- 维护依赖的人用 `npm install`

## 4. `npm ci` 报错时怎么处理

常见报错：

- `package.json and package-lock.json are not in sync`
- `Invalid: lock file's ... does not satisfy ...`

处理步骤：

```bash
npm install --package-lock-only
npm ci
```

如果你是仓库维护者，请把更新后的 [../package-lock.json](../package-lock.json) 一并提交。

## 5. 启动后做三个验证

```bash
npm run lint
npm run build
npm run dev
```

这三个命令分别验证：

- 语法和规范检查
- 生产构建是否通过
- 本地开发服务是否可用

## 6. 常见问题

### 问题 1：`eslint: command not found`

原因：依赖还没安装完整。  
解决：重新执行 `npm ci`（或维护场景用 `npm install`）。

### 问题 2：Node 23/24 出现 engine warning

原因：模板按 Node 22 作为统一基线。  
解决：切换回 Node 22（`nvm use`）。

### 问题 3：我应该改哪个文件来配置语言模式

直接改 [../content/site.json](../content/site.json)。  
参数说明见 [./CONTENT-MANAGEMENT.md](./CONTENT-MANAGEMENT.md) 的 i18n 小节。

## English Quick Notes

If you are using this template for the first time:

1. Use Node `22.x` from [../.nvmrc](../.nvmrc)
2. Run `nvm install && nvm use && npm ci && npm run dev`
3. If `npm ci` fails due to lock mismatch, run `npm install --package-lock-only` once, then retry `npm ci`
4. For dependency maintainers: use `npm install` when changing packages
