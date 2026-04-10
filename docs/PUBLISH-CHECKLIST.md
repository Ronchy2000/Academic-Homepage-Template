# 发布检查清单 / Publish Checklist

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

### 1. 构建检查

```bash
nvm install && nvm use
npm ci
npm run lint
npm run build
```

要求：无报错。

### 2. 语言配置检查

文件： [../content/site.json](../content/site.json)

确认：

- `mode` 是你要的模式
- `primaryLocale` 符合你的默认语言策略

规则：

- `"en"` 或 `"zh"`：固定默认语言
- `""`：仅留空时启用浏览器语言识别

### 3. 内容替换检查

至少确认这些文件已替换为你的数据：

- [../content/profile.json](../content/profile.json)
- [../content/pages/home.json](../content/pages/home.json)
- [../content/research.json](../content/research.json)
- [../content/publications.json](../content/publications.json)
- [../content/projects.json](../content/projects.json)
- [../content/timeline.json](../content/timeline.json)
- [../content/awards.json](../content/awards.json)
- [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg)
- [../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)

### 4. 占位词搜索

请全文搜索并替换：

- `your-handle`
- `example.com`
- `Example University`
- `YOUR_ID`
- `0000-0000-0000-0000`
- `Alex Chen`
- `陈明远`

### 5. 环境变量检查

参考： [../.env.example](../.env.example)

- `NEXT_PUBLIC_CONTACT_EMAIL_B64` 已设置
- 需要邮件标题时设置 `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`
- 需要仓库链接时设置 `NEXT_PUBLIC_REPOSITORY_URL`

### 6. 页面地址检查

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

要求：无 404，首次打开页面语言正确，联系邮箱和 CV 下载正常。

### 7. 平台专项检查

Vercel：

- 可直接导入仓库
- 环境变量已配置
- 首次打开页面语言正确

EdgeOne：

- 使用 `EDGEONE=1 npm run build`
- `/en -> /en/` 正常
- `/zh -> /zh/` 正常
- [../edgeone.json](../edgeone.json) 自动改写页面地址的规则存在

### 8. 仓库最终确认

- 保留 [../package.json](../package.json)
- 保留 [../package-lock.json](../package-lock.json)
- 保留 [../next-env.d.ts](../next-env.d.ts)
- 保留 [../.nvmrc](../.nvmrc)
- 保留 [../edgeone.json](../edgeone.json)
- 不提交隐私信息和临时调试文件

Template 发布设置说明： [GITHUB-TEMPLATE.md](./GITHUB-TEMPLATE.md)

---

<a id="en-start"></a>

### 1. Build checks

```bash
nvm install && nvm use
npm ci
npm run lint
npm run build
```

Requirement: no errors.

### 2. Locale checks

File: [../content/site.json](../content/site.json)

Confirm:

- `mode` matches your target
- `primaryLocale` matches your default-locale policy

Rules:

- `"en"` or `"zh"`: fixed default locale
- `""`: browser-language detection runs only when empty

### 3. Content replacement checks

At least verify these files are replaced with your data:

- [../content/profile.json](../content/profile.json)
- [../content/pages/home.json](../content/pages/home.json)
- [../content/research.json](../content/research.json)
- [../content/publications.json](../content/publications.json)
- [../content/projects.json](../content/projects.json)
- [../content/timeline.json](../content/timeline.json)
- [../content/awards.json](../content/awards.json)
- [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg)
- [../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)

### 4. Placeholder search

Search and replace:

- `your-handle`
- `example.com`
- `Example University`
- `YOUR_ID`
- `0000-0000-0000-0000`
- `Alex Chen`
- `陈明远`

### 5. Environment variable checks

Reference: [../.env.example](../.env.example)

- `NEXT_PUBLIC_CONTACT_EMAIL_B64` is set
- Set `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT` if needed
- Set `NEXT_PUBLIC_REPOSITORY_URL` if needed

### 6. URL checks

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

Requirement: no 404, first-open language is correct, and contact reveal/CV download work.

### 7. Platform checks

Vercel:

- repository import works
- environment variables configured
- first-open language is correct

EdgeOne:

- run `EDGEONE=1 npm run build`
- `/en -> /en/` works
- `/zh -> /zh/` works
- automatic URL rewrite rules exist in [../edgeone.json](../edgeone.json)

### 8. Final repository checks

- keep [../package.json](../package.json)
- keep [../package-lock.json](../package-lock.json)
- keep [../next-env.d.ts](../next-env.d.ts)
- keep [../.nvmrc](../.nvmrc)
- keep [../edgeone.json](../edgeone.json)
- do not commit private data or temporary debug files

Template publishing setup: [GITHUB-TEMPLATE.md](./GITHUB-TEMPLATE.md)
