# 从零部署 CELEUS × Jev 网站到 GitHub Pages

这份教程使用电脑浏览器操作，不需要终端，不需要写部署代码。
已有 GitHub 账号就直接登录；没有账号先在 GitHub 注册并验证邮箱。

**最终你会得到一个公开网址：**

```text
https://你的GitHub用户名.github.io/celeus-jev/
```

这里的 `celeus-jev` 是本教程建议的仓库名，不是已经创建好的网站。
文件包准备好了，但它还没有上传到你的账号，也尚未部署到公网。

## 先理解三个词

**Repository（仓库）**：GitHub 上存放这几个网站文件的地方。

**Commit（提交）**：把本次上传或修改正式保存到仓库。

**GitHub Pages**：把仓库里的静态网页文件发布成一个能在浏览器访问的网站。

GitHub Free 可以为 Public（公开）仓库提供 Pages。下面只走这一种最简单的部署方式。

## 第 1 步：下载并解压文件包

下载 `celeus-jev-github-pages.zip` 后，在电脑上解压。

Windows：右键压缩包 → 全部解压 / Extract All。
Mac：通常双击压缩包即可解压。

打开解压后的 `celeus-jev-github-pages` 文件夹，确认里面有：

```text
index.html
data.json
README.md
DEPLOY.zh-CN.md
DATA_SCHEMA.md
.nojekyll
```

`.nojekyll` 是隐藏的空文件，电脑可能不显示。看不到它不影响先上传本版本的可见文件。
真正必需的是 `index.html` 和 `data.json`。

所有评测数字保持 0，暂时不用修改数据。

## 第 2 步：创建一个 GitHub 仓库

登录 GitHub，在浏览器打开：

```text
https://github.com/new
```

按下面填写：

| 选项 | 选择 / 填写 |
|---|---|
| Owner | 你自己的账号 |
| Repository name | `celeus-jev` |
| Description | `CELEUS × Jev evaluation dashboard`（也可不填） |
| Visibility | **Public** |
| Add README | 开启 / 勾选 |
| Add .gitignore | No .gitignore / 不添加 |
| License | 暂时不用选 |

点击 **Create repository**。

这里选 Public 是为了使用免费公开托管。上传的文件会公开；不要上传密钥和私有数据。
本教程只需这个独立的网站仓库，不必上传你的 CELEUS 完整研究代码。

## 第 3 步：上传解压后的文件

进入刚创建的仓库，在 **Code** 页点击：

```text
Add file → Upload files
```

打开电脑上解压后的文件夹，将**文件夹里面的文件**拖到上传区域。
也可以点击 **choose your files**，选中这些文件。

**不要上传 ZIP 本身。不要把外层 `celeus-jev-github-pages` 文件夹整层拖进去。**

上传预览中应该直接出现：

```text
index.html
data.json
README.md
DEPLOY.zh-CN.md
DATA_SCHEMA.md
```

而不是：

```text
celeus-jev-github-pages/index.html
```

网页文件必须直接放在仓库第一层，也就是“根目录”。

上传包里的 README 会替换创建仓库时自动生成的 README；这是预期行为。

## 第 4 步：保存上传

在上传页面找到提交区域，Commit message 写：

```text
Add CELEUS Jev dashboard
```

在你自己新建、未设置保护规则的仓库中，选择：

```text
Commit directly to the main branch
```

然后点击 **Commit changes**。

如果页面提供的是“新建分支 / Propose changes”，先确认没有选择该选项；
本教程用直接保存到 main，避免多一个 Pull request 步骤。
若组织策略强制新分支，需按该策略合并到 main 后再发布。

提交完成后，仓库文件列表里应该直接看到 `index.html` 和 `data.json`。

文件列表左上方是当前分支名。新仓库通常为 `main`；后面选择的发布分支必须与这里一致。

## 第 5 步：开启 GitHub Pages

在这个仓库顶部点击 **Settings**。这是仓库的 Settings，不是头像菜单里的个人设置。

在左侧菜单找到 **Pages**。在 **Build and deployment** 区域设置：

```text
Source       Deploy from a branch
Branch       main
Folder       / (root)
```

点击 **Save**。

这个版本不需要自定义 GitHub Actions 工作流，不要改成 GitHub Actions，也不要选择 `/docs`。
GitHub 底层仍可能显示它自动创建的 Pages 部署任务，这不需要你写任何配置。

**Custom domain 保持空白。** 先使用 GitHub 给的免费网址，不需要买域名。

如果没有可选的 main，通常是还没有保存上传，或你的分支叫其他名字。先回到 Code 检查。

## 第 6 步：等待部署并打开网站

稍等，刷新 **Settings → Pages**。
GitHub 官方说明，发布变更可能需要最多约 10 分钟。

成功后页面会提供类似下面的提示和按钮：

```text
Your site is live at ...
Visit site
```

点击 **Visit site**，这是你应该分享的网站地址。

假设用户名是 `your-name`，仓库名是 `celeus-jev`：

```text
仓库地址（看文件）：
https://github.com/your-name/celeus-jev

网站地址（看网页）：
https://your-name.github.io/celeus-jev/
```

不要把仓库地址当成网页地址。
也不需要创建名为 `your-name.github.io` 的仓库；这里部署的是一个项目网站。

## 第 7 步：确认上线成功

打开网站后，检查：

- 顶部四张指标卡、性能图、费用 / 时间区间图和结果矩阵都出现。
- 所有评测值为 0，并标明等待实验 / placeholder；不是程序出错。
- ECD / ToolBench 等筛选按钮、柱状 / 点区间切换可以点击。
- Download JSON 与 Export CSV 可以下载文件。

在结果表下方应能看到 `Published data.json` 字样。
这表示页面已从公开网站成功读取数据文件。

## 以后如何修改结果？

### 方法 A：在 GitHub 网页直接修改（最简单）

打开仓库 **Code → data.json**，点击右上角的**铅笔图标**。
修改需要更新的字段，然后点击 **Commit changes**，保存到 main。

等待 Pages 再次部署，刷新网站，所有访问者都会看到新内容。
无需修改 `index.html`、无需运行 Python，也无需重新打开 Pages 配置。

不要直接删除整个 JSON 再只粘贴一小段示例；所有字段和四个 benchmark 都需要保留。
JSON 的字段名和字符串用英文双引号，数字不加引号；注意逗号，不能写注释。

### 第一次可以只修改一条文字，确认更新流程

在 `data.json` 搜索第一条 benchmark 的 `notes`，把它改成：

```json
"notes": "First GitHub Pages update successful. Evaluation results are still pending."
```

保持其他字段不变并提交。部署后，在网站的结果表点击 ECD 展开行，应该能看到新说明。
这种测试不会伪造任何实验数字，也不需要把 `isPlaceholder` 改成 false。

### 正式填真实实验结果时

把最上面的：

```json
"isPlaceholder": true
```

改为：

```json
"isPlaceholder": false
```

再填写真实样本数、得分、区间、成本、时间和运行信息。
否则程序会拒绝“声称全零占位但混入非零结果”的数据。

字段的精确含义见 [DATA_SCHEMA.md](DATA_SCHEMA.md)。
尤其要保持 `stoppingSample ≤ evaluated ≤ poolSize`，区间下界 ≤ 估计值 ≤ 上界。
不要因为网页能显示区间，就把尚未验证的区间标为 certified。

### 方法 B：先本地预览，再上传

在网站点击 **Import JSON**，选择你本地已经准备好的结果文件。
页面会立刻预览，帮助你检查格式、图表和数字。

**这一步不会发布，也不会把文件上传到 GitHub。其他人仍看到原来的数据。**

确认后点击 **Download JSON**，得到 `data.json`。
回到 GitHub 仓库根目录，用 **Add file → Upload files** 上传这个文件，覆盖旧的 `data.json`，提交到 main。
等待重新部署后才算公开更新。
注意浏览器重复下载可能把文件命名为 `data (1).json`；上传前改回 `data.json`。

## 修改 Paper / Source / Documentation 链接

也在 `data.json` 中，找到：

```json
"links": {
  "paper": "https://example.com/paper",
  "code": "https://example.com/code",
  "documentation": "https://example.com/documentation"
}
```

把对应引号里面的网址改成真实网址，保留结构并提交。
Source 通常填你的 GitHub 仓库网址。占位链接不是部署故障。

## 常见问题

### 网站显示 404

确认你打开的是 Pages 网站地址，不是猜测的其他路径。
确认 `index.html` 直接在根目录，名称是全小写，不是 `Index.html` 或 `index.html.txt`。
确认 Pages 的来源是正确分支和 `/ (root)`，并且发布已经完成。
在仓库顶部 **Actions** 可以查看自动部署任务是否成功。失败任务通常会有错误详情。

### 只看到一个文件夹，或只有 ZIP 文件

说明上传层级不对。回到根目录重新上传解压后的 `index.html`、`data.json` 等文件。
重点是根目录必须有网站入口，不要再上传一个新的外层文件夹。

### 网站提示 Could not load data.json

这是本版本新增的明确提示，避免把读取失败误当成真实的 0 分。
确认 `data.json` 与 `index.html` 在同一层，文件名称正确、JSON 格式有效。
也可以直接访问你的网站地址后加 `data.json`，确认这个文件能打开。
修正并提交后等待部署，再刷新页面。

### 修改后仍是旧数据

先确认改的是 GitHub 仓库里的 `data.json`，不是只用了网页 Import JSON。
查看 Actions 部署是否完成，再刷新网站或用无痕窗口检查。
浏览器和托管端可能有短暂缓存，不要看到旧内容就重复修改实验数据。

### 双击电脑上的 index.html，却没有显示旁边 JSON 的更新

这是本地 file:// 模式的预期行为。出于兼容性，它不自动读取相邻数据文件，
而是显示内嵌的零数据。请用 Import JSON 预览，或打开已部署的网址。

### 手机上上传不方便

请用电脑浏览器完成初次部署和文件上传。上线后网页支持手机访问。

### 需要 Jev API key 吗？

**部署和浏览这个展示网站不需要。** 网站不会自动跑实验或调用模型。
你的实验仍在本地 / 服务器运行，实验完成后只上传公开结果摘要。

千万不要把 `TYPESAFE_API_KEY`、密码、`.env` 或私有数据放到这个仓库。
本教程的仓库和 Pages 网页都是公开的。

## 官方参考

部署操作依据 GitHub 官方文档核对于 2026-09-21：

- [GitHub Pages 是什么](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
- [创建 Pages 网站](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
- [设置发布来源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [上传文件](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)
- [网页编辑文件](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files)
- [排查 404](https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)
