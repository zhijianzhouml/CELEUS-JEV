# CELEUS × Jev — GitHub Pages

A single-page research dashboard for certified performance, evaluated sample size,
and evaluation cost and time across ECD, ToolBench, UNSW-NB15, and IEEE-CIS.

**所有评测结果和区间端点均为 0 占位值。不是已经完成的实验结果。**

## 从这里开始

**第一次部署，请打开 [中文逐步部署教程](DEPLOY.zh-CN.md)。**

不需要安装 Node.js、Python、Git 或 VS Code；不需要自己的服务器。
此版本没有构建步骤。不要再使用旧版本的 `build.py`。

## 文件

| 文件 | 用途 |
|---|---|
| `index.html` | 网站入口；内含样式、交互和全零备用数据。 |
| `data.json` | 网站上线后读取的公开数据；更新结果和链接只需改它。 |
| `.nojekyll` | 空文件，跳过 Jekyll 处理；可能在电脑上被隐藏。 |
| `DEPLOY.zh-CN.md` | 中文部署、更新、排错教程。 |
| `DATA_SCHEMA.md` | 每个数据字段、单位和区间类型的说明。 |
| `README.md` | 本说明。 |

## 部署设置

在你的 GitHub 仓库中：

```text
Settings → Pages → Build and deployment
Source: Deploy from a branch
Branch: main
Folder: / (root)
Save
```

`index.html` 和 `data.json` 必须直接位于仓库根目录。
不要只上传 ZIP，也不要额外套一层文件夹。

GitHub Free 的部署路径使用 **Public** 仓库。
网站地址由 GitHub 提供，形式为：

```text
https://YOUR-USERNAME.github.io/celeus-jev/
```

网站与仓库是两个不同地址；在 Settings → Pages 点击 **Visit site** 查看网站。

## 更新公开结果

在 GitHub 的文件列表打开 `data.json`，点击铅笔图标，修改后 Commit changes。
等待 Pages 完成部署，刷新网站。只改 JSON 不需要重新构建 HTML。

所有图表、表格、Paper / Source / Documentation 链接都从同一份数据读取。
`links` 中仍是 `example.com` 占位网址，请在正式发布时替换。

### 公开数据与本地预览不是一回事

- 访问已部署网站：读取同目录的 `data.json`。
- Import JSON：仅改变当前浏览器页面，不会写入 GitHub，不会发布。
- Download JSON：导出名为 `data.json` 的文件；仓库所有者可上传到根目录发布。
- 双击本地 `index.html`：显示内嵌的全零预览。浏览器不会自动读取旁边的 JSON；请用 Import JSON。
- 在线 JSON 缺失、格式不对或超时：显示明确错误提示和全零备用数据，不假装加载了真实结果。

## 安全与统计说明

此网站只展示已经计算好的结果，不调用 Jev，不运行 CELEUS，不产生模型调用费用。
它只读取本站的公开 `data.json`，没有第三方脚本、外部字体依赖或后台服务。

**不要上传 API key、密码、`.env`、私有实验记录或未经许可公开的原始数据。**
Public 仓库及普通 Pages 网站是公开的。

置信区间必须由实验程序提供。网页不会从一组总成本或总时间自动构造有效区间。
只有经过相应统计方法验证的区间才能标为 certified。

所有免费托管可用性与部署规则以 GitHub 官方文档为准：
[GitHub Pages 简介](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
和 [配置发布来源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。
