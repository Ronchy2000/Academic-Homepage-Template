# Deployment Guide / 部署指南

本项目支持两条部署路径：

1. Vercel（推荐）
2. EdgeOne Pages（静态导出）

下面内容按“第一次部署的人”来写，你可以直接照做。

## 1. 先确认这些关键文件

- Node 版本基线： [../.nvmrc](../.nvmrc)
- 构建行为： [../next.config.mjs](../next.config.mjs)
- 请求时语言跳转： [../proxy.ts](../proxy.ts)
- 静态导出兜底跳转： [../app/(redirects)](../app/%28redirects%29)
- EdgeOne 配置： [../edgeone.json](../edgeone.json)
- 语言模式配置： [../content/site.json](../content/site.json)

## 2. Vercel 部署（推荐）

为什么推荐：

- 配置最少
- 标准 Next.js 行为
- `proxy.ts` 可以在请求阶段处理语言入口跳转

部署步骤：

1. 把仓库推送到 GitHub
2. 在 Vercel 导入仓库
3. Framework 保持 `Next.js`
4. 在 Vercel 项目设置里填环境变量
5. 点击 Deploy

环境变量建议：

- 必填：`NEXT_PUBLIC_CONTACT_EMAIL_B64`
- 选填：`NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`
- 选填：`NEXT_PUBLIC_REPOSITORY_URL`

变量说明可直接看： [../.env.example](../.env.example)

注意：

- 本模板不需要 `vercel.json`
- 默认走标准 Next.js 输出，不是 `output: "export"`

## 3. EdgeOne Pages 部署（可选）

适合你已经确定要用 EdgeOne Pages 的情况。

构建命令：

```bash
EDGEONE=1 npm run build
```

模板已内置这些关键兼容：

- 静态导出目录 `out`
- 顶层语言入口重定向 `/en -> /en/`、`/zh -> /zh/`
- `trailingSlash: true`（仅 EdgeOne 构建路径生效）

对应配置文件：

- [../next.config.mjs](../next.config.mjs)
- [../edgeone.json](../edgeone.json)
- [../app/(redirects)](../app/%28redirects%29)

## 4. 语言默认策略一定要对齐

配置文件： [../content/site.json](../content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

规则：

- `primaryLocale: "en"`：固定英文默认，不启用浏览器语言识别
- `primaryLocale: "zh"`：固定中文默认，不启用浏览器语言识别
- `primaryLocale: ""`：只有留空才启用浏览器语言识别；识别不到时回退英文

优先级：

1. 先看 `locale` cookie
2. 无 cookie 且 `primaryLocale` 为空时，才看浏览器语言
3. 仍无法判断则回退英文

## 5. 部署后必测路径

- `/`
- `/en`
- `/en/`
- `/zh`
- `/zh/`
- `/en/research`
- `/zh/research`
- `/en/contact`
- `/zh/contact`

重点检查：

- 顶层语言入口是否稳定跳转
- 语言路由是否出现 404
- 头像、样式、脚本等静态资源是否正常
- 简历下载是否正常
- 联系页邮箱 reveal 是否正常

## 6. 常见问题

### 问题 1：EdgeOne 上 `/en` 可以访问但 `/en/` 才正常

这是静态托管常见路径差异。请确认：

- [../edgeone.json](../edgeone.json) 的 308 重定向规则存在
- [../next.config.mjs](../next.config.mjs) 在 `EDGEONE=1` 时启用了 `trailingSlash`

### 问题 2：语言入口与预期不一致

请先检查 [../content/site.json](../content/site.json) 里的 `primaryLocale`：

- 不是空字符串时，不会进行浏览器语言识别

### 问题 3：Vercel 环境变量改完不生效

请重新触发部署。前端公开变量需要重新构建后才会生效。

## Official References

- [Vercel](https://vercel.com)
- [Next.js on Vercel](https://vercel.com/docs/frameworks/nextjs)
- [Tencent EdgeOne Pages](https://edgeone.ai/products/pages)
- [edgeone.json Configuration Guide](https://pages.edgeone.ai/document/edgeone-json)
