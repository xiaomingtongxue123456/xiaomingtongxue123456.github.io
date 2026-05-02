---
title: hexo博客发布流程
date: 2026-05-02 17:13:17
tags: 教程
---

Hexo博客发布完整流程

Hexo 是一款基于 Node.js 的快速、简洁且高效的静态博客框架，支持使用 Markdown 编写文章，一键生成静态网页，并可免费部署到 GitHub Pages 等平台。本文将带你从零开始，完成从本地搭建到线上发布的完整流程。

## 一、前置环境准备

在开始之前，你需要先安装两个基础工具：**Node.js** 和 **Git**。

### 1. 版本要求

- **Node.js**：Hexo 7.0+ 要求 Node.js 版本 ≥ 14.0.0，Hexo 8.0+ 要求 ≥ 20.19.0，推荐安装最新的 LTS 长期支持版本（如 20.x）。
- **Git**：用于代码版本管理和部署推送。

### 2. 安装方式

#### Windows / Mac

- 访问 [Node.js 官网](https://nodejs.org/) 下载对应系统的安装包，安装时勾选 `Add to PATH` 自动配置环境变量。
- 访问 [Git 官网](https://git-scm.com/) 下载 Git 安装包，默认选项安装即可。

#### Linux（Ubuntu/Debian）

```bash
# 安装 Node.js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# 安装 Git
sudo apt-get install git
```

### 3. 验证安装

打开终端（Windows 用 CMD/PowerShell，Mac/Linux 用 Terminal），执行以下命令，若能输出版本号则说明安装成功：

```bash
node -v
npm -v
git -v
```

## 二、本地搭建 Hexo 博客

### 1. 安装 Hexo 命令行工具

全局安装 Hexo 的 CLI 工具，用于后续的项目初始化和命令操作：

```bash
npm install -g hexo-cli
```

安装完成后，验证是否安装成功：

```bash
hexo -v
```

若输出 Hexo 版本信息，则说明安装成功。

### 2. 初始化博客项目

1. 新建一个文件夹用于存放博客项目，比如 `hexo-blog`，然后进入该文件夹：

```bash
mkdir hexo-blog
cd hexo-blog
```

1. 初始化 Hexo 项目，这会自动生成博客的基础目录结构和默认配置：

```bash
hexo init
```

1. 安装项目依赖：

```bash
npm install
```

### 3. 本地启动预览

执行以下命令启动本地开发服务：

```bash
hexo server
# 简写：hexo s
```

启动成功后，在浏览器中访问 `http://localhost:4000`，你就能看到 Hexo 默认的博客页面了：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=M2ZhOWFlYmQ2M2I2ZjE1NzYzYWI4NjNhYTMzMzM0NTFfb2NGdXFJdXZ4dDVNZFhPOWZiaTNHcGduTW54NUZDV1pfVG9rZW46SnFzOWJ1dHQ5b0VtN0x4TGdWVGNmVG9obnViXzE3Nzc3MTQyNjA6MTc3NzcxNzg2MF9WNA&add_watermark=true&scene_type=CCM_DOUBAO)

按下 `Ctrl + C` 可以停止本地服务。

### 4. 撰写第一篇文章

1. 执行以下命令新建一篇文章：

```bash
hexo new "我的第一篇文章"
# 简写：hexo n "我的第一篇文章"
```

1. 这会在 `source/_posts/` 目录下生成一个名为 `我的第一篇文章.md` 的 Markdown 文件，你可以用任意 Markdown 编辑器（如 Typora、VS Code）打开它，编写文章内容：

```markdown
---
title: 我的第一篇文章
date: 2025-05-02 16:00:00
tags: [Hexo, 博客]
---

# Hello Hexo
这是我的第一篇 Hexo 博客文章！
使用 Markdown 就可以轻松写出排版美观的文章~
```

1. 重新启动本地服务 `hexo s`，刷新浏览器，就能看到你刚写的文章了。

## 三、部署到 GitHub Pages（免费托管）

GitHub Pages 是 GitHub 提供的免费静态网站托管服务，我们可以把 Hexo 生成的静态博客部署到这里，让全世界都能访问。

### 前置步骤：创建 GitHub 仓库

1. 登录你的 GitHub 账号，点击右上角 `New repository` 新建仓库。
2. **仓库名称必须设置为** **`你的GitHub用户名.github.io`**（比如你的用户名是 `test`，则仓库名是 `test.github.io`），这是 GitHub Pages 的固定规则。
3. 选择 `Public`（公开），点击 `Create repository` 完成创建。

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MmUzMWQwY2I2ODNhMTkyMzhlMzY2MmQwNDg0Nzk2ZmRfdHF3dUgxY2lRODBBWE9mNjZGTGx0T1VzT1FKU3ZLUUNfVG9rZW46S09HTmJMT25Yb2hXVGN4WVNWcmNQUWlobm9mXzE3Nzc3MTQyNjA6MTc3NzcxNzg2MF9WNA&add_watermark=true&scene_type=CCM_DOUBAO)

接下来，你可以选择以下两种部署方式中的一种：

### 方式一：GitHub Actions 自动部署（官方推荐）

这种方式会把你的博客源码推送到 GitHub，由 GitHub 自动帮你构建和部署，无需本地构建，更适合长期维护。

1. **配置 Git 信息**（首次使用 Git 需要配置）：

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

1. **初始化本地 Git 仓库并关联远程**： 在博客根目录执行：

```bash
# 初始化Git仓库
git init

# 添加所有文件到暂存区
git add .

# 提交代码
git commit -m "初始化博客源码"

# 关联远程仓库（替换成你自己的仓库地址）
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git

# 推送到main分支
git push -u origin main
```

1. **配置 GitHub Actions 工作流**： 在博客根目录创建文件夹 `.github/workflows`，然后在里面新建文件 `pages.yml`，写入以下内容（注意把 `node-version: "20"` 替换成你本地的 Node.js 大版本，比如你本地是 20.12.0，就写 20）：

```yaml
name: Pages
on:
  push:
    branches:
      - main # 默认分支
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          submodules: recursive
      - name: Use Node.js 20
        uses: actions/setup-node@v4
        with:
          node-version: "20"
      - name: Cache NPM dependencies
        uses: actions/cache@v4
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

1. **设置 GitHub Pages 源**： 打开你的 GitHub 仓库，进入 `Settings > Pages`，把 `Source` 修改为 `GitHub Actions`，保存即可。
2. **提交并推送代码**： 把刚才新建的工作流文件提交并推送到远程：

```bash
git add .
git commit -m "添加Actions部署配置"
git push
```

之后，GitHub 会自动开始构建和部署，等待几分钟后，你就可以访问 `https://你的用户名.github.io` 查看你的博客了！

### 方式二：一键部署（传统本地构建方式）

这种方式是在本地构建好静态文件，然后直接推送到 GitHub，操作更简单，适合新手快速上手。

1. **安装部署插件**：

```bash
npm install hexo-deployer-git --save
```

1. **配置部署信息**： 打开博客根目录下的 `_config.yml` 文件，拉到最底部，找到 `deploy` 部分，修改为以下内容（替换成你自己的仓库地址）：

```yaml
deploy:
  type: git
  repo: https://github.com/你的用户名/你的用户名.github.io.git
  branch: gh-pages # 注意：这里是gh-pages分支，不要写错，避免覆盖源码
```

1. **执行部署**： 执行以下命令，一键清理缓存、生成静态文件并部署到 GitHub：

```bash
hexo clean && hexo generate && hexo deploy
# 简写：hexo clean && hexo g && hexo d
```

1. **身份验证**： 第一次部署时，会提示你输入 GitHub 的用户名和密码：

- 用户名：你的 GitHub 用户名
- 密码：如果你开启了双重验证，**不能用账号密码**，需要使用 [Personal Access Token（个人访问令牌）](#附如何创建-personal-access-token)，直接把 Token 当密码输入即可。

部署完成后，等待几分钟，访问 `https://你的用户名.github.io` 就能看到你的博客了！

## 四、更换主题（以热门的 NexT 主题为例）

Hexo 默认的主题比较简洁，你可以更换成更美观、功能更丰富的主题，其中 **NexT** 是最受欢迎的 Hexo 主题之一，风格优雅简洁。

### 1. 安装 NexT 主题

在博客根目录执行以下命令安装主题：

```bash
# 推荐方式：npm安装
npm install hexo-theme-next
```

或者你也可以用 Git 克隆的方式安装（方便后续更新主题）：

```bash
git clone https://github.com/next-theme/hexo-theme-next themes/next
```

### 2. 启用主题

打开博客根目录的 `_config.yml` 文件，找到 `theme` 配置，把默认的 `landscape` 修改为 `next`：

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```

### 3. 预览主题

重新启动本地服务 `hexo s`，刷新浏览器，就能看到新的主题界面了：

你还可以根据 NexT 的官方文档，配置评论系统、侧边栏、动画等个性化功能。

## 五、日常发布新文章流程

当你搭建好博客之后，后续发布新文章的流程非常简单：

1. **新建文章**：

```bash
hexo new "新文章标题"
```

1. **编辑文章**：打开 `source/_posts` 下对应的 Markdown 文件，编写内容。
2. **本地预览**：

```bash
hexo clean && hexo g && hexo s
```

访问 `http://localhost:4000` 检查文章效果是否正常。 4. **部署上线**：

- 如果你用的是 **Actions 部署**：把修改后的代码提交并推送到 main 分支，GitHub 会自动部署：

  - ```bash
    git add .
    git commit -m "添加新文章：xxx"
    git push
    ```

- 如果你用的是 **一键部署**：直接执行部署命令即可：

  - ```bash
    hexo clean && hexo g && hexo d
    ```

## 六、常见问题与注意事项

### 1. 部署后页面空白 / 样式丢失

这通常是 `_config.yml` 中的 `url` 配置错误导致的。如果你的博客是 `用户名.github.io`，请确保 `url` 配置为：

```yaml
url: https://你的用户名.github.io
```

如果是项目页（仓库名不是用户名.[github.io](github.io)），则需要配置为：

```yaml
url: https://你的用户名.github.io/仓库名
```

### 2. 分支错误导致源码丢失

一键部署时，`deploy` 配置中的 `branch` 必须是 `gh-pages`，如果写错成 `main` 或 `master`，会导致你的博客源码被静态文件覆盖，造成数据丢失！

### 3. 权限错误 / 部署失败

如果提示权限错误，检查你的 Personal Access Token 是否勾选了 `repo` 权限，并且没有过期。

## 附：如何创建 Personal Access Token

如果你开启了 GitHub 双重验证，部署时需要用 Token 代替密码，创建步骤如下：

1. 登录 GitHub，点击右上角头像 → `Settings`。
2. 左侧拉到最底部，点击 `Developer settings`。
3. 点击 `Personal access tokens` → `Tokens (classic)`。
4. 点击 `Generate new token` → `Generate new token (classic)`。
5. 给 Token 起个名字，比如 `hexo-deploy`，过期时间选择 `No expiration`（或者自定义）。
6. 权限勾选 `repo`（全部 repo 相关的权限即可）。
7. 拉到最底部，点击 `Generate token`。
8. **立即复制生成的 Token**，这个 Token 只会显示一次，丢失了需要重新创建。

之后部署时，用户名填你的 GitHub 用户名，密码填这个 Token 即可。

## 可选：绑定自定义域名

如果你有自己的域名，可以绑定到博客上，让访问地址更个性化：

1. 在博客的 `source` 目录下新建一个名为 `CNAME` 的文件，里面写入你的域名，比如 `www.example.com`。
2. 到你的域名服务商后台，添加解析记录：
   1. CNAME 记录：主机记录填 `www`，记录值填 `你的用户名.github.io`。
   2. 或者添加 4 条 A 记录，指向 GitHub Pages 的 IP：`185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`。
3. 重新部署博客，等待解析生效后，就可以用自己的域名访问博客了。
