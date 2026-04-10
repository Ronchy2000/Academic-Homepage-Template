# Publish Checklist / 发布检查清单

上线前按这个清单逐条过一遍，能显著减少“发布后才发现配置错误”的概率。

## 1. 构建与质量检查

```bash
nvm install && nvm use
npm ci
npm run lint
npm run build
```

通过标准：

- 无安装报错
- 无 lint error
- build 成功输出

## 2. 语言模式与默认语言检查

文件： [../content/site.json](../content/site.json)

重点确认：

- `mode` 是否符合你的站点目标（双语/单语）
- `primaryLocale` 语义是否符合预期

规则提醒：

- `"en"` 或 `"zh"`：固定默认语言，不启用浏览器语言识别
- `""`：仅留空时才启用浏览器语言识别

## 3. 内容替换检查

请至少检查以下文件已替换为你的真实信息：

- [../content/profile.json](../content/profile.json)
- [../content/pages/home.json](../content/pages/home.json)
- [../content/research.json](../content/research.json)
- [../content/publications.json](../content/publications.json)
- [../content/projects.json](../content/projects.json)
- [../content/timeline.json](../content/timeline.json)
- [../content/awards.json](../content/awards.json)
- [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg)
- [../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)

## 4. 占位词全文搜索

发布个人站前，建议全文搜索这些关键词并替换：

- `your-handle`
- `example.com`
- `Example University`
- `YOUR_ID`
- `0000-0000-0000-0000`
- `Alex Chen`
- `陈明远`

## 5. 环境变量检查

参考文件： [../.env.example](../.env.example)

至少确认：

- `NEXT_PUBLIC_CONTACT_EMAIL_B64` 已设置
- 需要邮件标题时设置 `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`
- 需要页脚仓库链接时设置 `NEXT_PUBLIC_REPOSITORY_URL`

## 6. 路由与页面可用性检查

至少访问以下路径：

- `/`
- `/en`
- `/en/`
- `/zh`
- `/zh/`
- `/en/research`
- `/zh/research`
- `/en/projects`
- `/zh/projects`
- `/en/contact`
- `/zh/contact`
- `/en/cv`
- `/zh/cv`

通过标准：

- 不出现 404
- 语言切换行为符合预期
- 联系邮箱可正常 reveal
- CV 下载可用

## 7. 部署路径专项检查

### Vercel

- 仓库可直接导入
- 环境变量已配置
- 根路径语言跳转符合预期（由 [../proxy.ts](../proxy.ts) 处理）

### EdgeOne

- 使用 `EDGEONE=1 npm run build`
- `/en -> /en/` 正常
- `/zh -> /zh/` 正常
- [../edgeone.json](../edgeone.json) 的重定向规则存在

## 8. 仓库最终确认

- 保留 [../package.json](../package.json)
- 保留 [../package-lock.json](../package-lock.json)
- 保留 [../.nvmrc](../.nvmrc)
- 保留 [../edgeone.json](../edgeone.json)
- 没有误提交私人链接、真实隐私信息或临时调试文件

## English Quick Pass

Before publishing:

1. Run `npm ci && npm run lint && npm run build`
2. Verify [../content/site.json](../content/site.json) mode and `primaryLocale`
3. Replace placeholder data and assets
4. Confirm required environment variables from [../.env.example](../.env.example)
5. Test locale routes and contact/CV behavior
