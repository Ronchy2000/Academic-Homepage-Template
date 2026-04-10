# 部署指南 / Deployment Guide

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

### 1. 部署前先看这些文件

- 构建配置： [../next.config.mjs](../next.config.mjs)
- 访问时自动进入对应语言页面： [../proxy.ts](../proxy.ts)
- 静态部署时自动进入对应语言页面： [../app/(redirects)](../app/%28redirects%29)
- EdgeOne 配置： [../edgeone.json](../edgeone.json)
- 语言参数： [../content/site.json](../content/site.json)

### 2. Vercel 部署（推荐）

步骤：

1. 把仓库推到 GitHub
2. 在 Vercel 导入仓库
3. Framework 保持 `Next.js`
4. 配置环境变量
5. 部署

变量参考： [../.env.example](../.env.example)

- 必填：`NEXT_PUBLIC_CONTACT_EMAIL_B64`
- 选填：`NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`
- 选填：`NEXT_PUBLIC_REPOSITORY_URL`

说明：

- 不需要 `vercel.json`
- 默认是标准 Next.js 输出

### 3. EdgeOne Pages 部署（静态导出）

构建命令：

```bash
EDGEONE=1 npm run build
```

关键点：

- 输出目录是 `out`
- 会把 `/en` 自动改成 `/en/`，把 `/zh` 自动改成 `/zh/`
- `EDGEONE=1` 时使用 `trailingSlash: true`

对应文件： [../next.config.mjs](../next.config.mjs) 和 [../edgeone.json](../edgeone.json)

### 4. 语言默认策略

文件： [../content/site.json](../content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

规则：

- `primaryLocale: "en"`：固定英文默认，不识别浏览器语言
- `primaryLocale: "zh"`：固定中文默认，不识别浏览器语言
- `primaryLocale: ""`：仅留空时识别浏览器语言

优先级：

1. `locale` cookie
2. 浏览器语言（仅 `primaryLocale` 为空时）
3. 回退英文

### 5. 部署后检查页面地址

- `/`
- `/en`
- `/en/`
- `/zh`
- `/zh/`
- `/en/research`
- `/zh/research`
- `/en/contact`
- `/zh/contact`

检查点：

- 首次打开时页面语言是否符合预期
- 是否有 404
- 静态资源是否正常
- CV 下载和邮箱 reveal 是否正常

### 6. 常见问题

问题：EdgeOne 上 `/en` 与 `/en/` 打开结果不一致  
处理：确认 [../edgeone.json](../edgeone.json) 的 308 设置和 [../next.config.mjs](../next.config.mjs) 的 `trailingSlash`。

问题：默认语言和预期不一致  
处理：检查 [../content/site.json](../content/site.json) 的 `primaryLocale`。

问题：Vercel 改了环境变量但页面没变  
处理：重新部署一次。

---

<a id="en-start"></a>

### 1. Check these files before deployment

- Build config: [../next.config.mjs](../next.config.mjs)
- Automatic language-page entry during request handling: [../proxy.ts](../proxy.ts)
- Automatic language-page entry for static deployments: [../app/(redirects)](../app/%28redirects%29)
- EdgeOne config: [../edgeone.json](../edgeone.json)
- Locale parameters: [../content/site.json](../content/site.json)

### 2. Vercel deployment (recommended)

Steps:

1. Push repository to GitHub
2. Import repository in Vercel
3. Keep framework as `Next.js`
4. Configure environment variables
5. Deploy

Variables: [../.env.example](../.env.example)

- Required: `NEXT_PUBLIC_CONTACT_EMAIL_B64`
- Optional: `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`
- Optional: `NEXT_PUBLIC_REPOSITORY_URL`

Notes:

- `vercel.json` is not required
- Standard Next.js output is used

### 3. EdgeOne Pages deployment (static export)

Build command:

```bash
EDGEONE=1 npm run build
```

Key points:

- output directory is `out`
- `/en` is automatically changed to `/en/`, and `/zh` is automatically changed to `/zh/`
- `trailingSlash: true` is enabled for `EDGEONE=1`

See [../next.config.mjs](../next.config.mjs) and [../edgeone.json](../edgeone.json).

### 4. Default locale strategy

File: [../content/site.json](../content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

Rules:

- `primaryLocale: "en"`: first visit is fixed to English, browser-language detection is disabled
- `primaryLocale: "zh"`: first visit is fixed to Chinese, browser-language detection is disabled
- `primaryLocale: ""`: browser-language detection runs only when empty

Priority:

1. `locale` cookie
2. browser language (only when `primaryLocale` is empty)
3. fallback to English

### 5. URLs to test after deployment

- `/`
- `/en`
- `/en/`
- `/zh`
- `/zh/`
- `/en/research`
- `/zh/research`
- `/en/contact`
- `/zh/contact`

Checks:

- first-open language should match your expected behavior
- no 404
- static assets load
- CV download and email reveal

### 6. Common issues

Issue: `/en` and `/en/` behave differently on EdgeOne  
Fix: verify 308 rules in [../edgeone.json](../edgeone.json) and `trailingSlash` in [../next.config.mjs](../next.config.mjs).

Issue: default locale is not expected  
Fix: verify `primaryLocale` in [../content/site.json](../content/site.json).

Issue: Vercel env var changed but page did not update  
Fix: redeploy.
