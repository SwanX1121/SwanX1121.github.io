---
title: Hexo个人博客部署与使用记录
date: 2026-10-05 19:54:51
tags: 工具使用
---

## 1. Hexo 是什么

Hexo 是一个静态博客框架。

基本工作流程可以理解为：

```
Markdown
   ↓
Hexo
   ↓
HTML / CSS / JavaScript
   ↓
GitHub Pages
   ↓
个人博客
```

因此平时真正需要维护的主要是 Markdown 源文件，而不是手工编写网页。

## 2. 环境准备

本次使用的环境为 Windows。

需要准备：

- Git
- Node.js
- npm
- Hexo

Git 在之前已经安装，因此首先安装 Node.js。

安装完成后检查：

```
node -v
npm -v
```

只要两个命令都能正常返回版本号，就说明 Node.js 和 npm 环境已经准备完成。

需要注意的是，npm 会随着 Node.js 一起安装，一般不需要单独安装。

## 3. 安装 Hexo

使用 npm 全局安装 Hexo CLI：

```
npm install -g hexo-cli
```

检查安装：

```
hexo -v
```

如果可以看到 Hexo、Node.js 等版本信息，就说明安装成功。

## 4. 创建 Hexo 博客

创建一个新的博客项目：

```
hexo init my-blog
cd my-blog
npm install
```

此时项目大致包含：

```
my-blog/
├── _config.yml
├── package.json
├── scaffolds/
├── source/
│   └── _posts/
└── themes/
```

其中我目前最关心的几个目录和文件是：

### `_config.yml`

Hexo 的主要配置文件。

以后修改网站名称、作者、网站地址等信息，主要都会操作这个文件。

### `source/_posts`

保存博客文章。

以后绝大多数学习记录都会写在这里。

### `themes`

保存博客主题。

目前暂时使用默认主题，等博客的基本工作流稳定后再考虑更换主题。

## 5. 本地运行博客

执行：

```
hexo server
```

然后打开：

```
http://localhost:4000
```

即可在浏览器中查看博客。

这一步非常有用，因为以后每次写完文章，可以先在本地检查：

- Markdown 是否正常渲染；
- 标题是否正确；
- 代码块是否正常；
- 图片是否正常；
- 页面排版是否有问题。

确认无误后再发布到 GitHub。

## 6. 创建博客文章

Hexo 可以使用：

```
hexo new "文章标题"
```

创建文章。

例如这篇文章就是通过：

```
hexo new "Hexo个人博客部署与使用记录"
```

创建的。

生成的 Markdown 文件保存在：

```
source/_posts/
```

文章顶部包含一段 Front Matter，例如：

```
---
title: Hexo个人博客部署与使用记录
date: 2026-10-05
tags:
  - Hexo
  - Git
  - GitHub
categories:
  - 学习记录
---
```

其中：

- `title`：文章标题；
- `date`：发布时间；
- `tags`：标签；
- `categories`：分类。

目前我计划将博客主要作为学习记录，因此分类不会设置得过于复杂。

## 7. 使用 Git 管理博客

首先初始化 Git：

```
git init
git branch -M main
```

然后添加文件：

```
git add .
```

第一次提交时出现了：

```
Author identity unknown
```

这是因为 Git 还不知道 commit 的作者信息。

因此进行了全局配置：

```
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

检查配置：

```
git config --global --list
```

然后重新提交：

```
git add .
git commit -m "Initial Hexo blog"
```

## 8. 将博客上传到 GitHub

创建 GitHub 仓库：

```
username.github.io
```

其中 `username` 替换成自己的 GitHub 用户名。

然后关联远程仓库：

```
git remote add origin https://github.com/username/username.github.io.git
```

第一次推送：

```
git push -u origin main
```

之后就只需要：

```
git push
```

## 9. 使用 GitHub Actions 自动部署

博客源码保存在 GitHub 的 `main` 分支。

当代码 push 到 GitHub 后，通过 GitHub Actions：

```
main
  ↓
GitHub Actions
  ↓
安装 Node.js 依赖
  ↓
Hexo Build
  ↓
生成 public/
  ↓
GitHub Pages
```

因此不需要每次手动把生成后的网页文件上传到 GitHub。

这也是我比较喜欢这种方案的原因：

> GitHub 保存的是博客源码，而网站部署由自动化流程完成。

## 10. 我的日常写作流程

博客部署完成之后，日常使用实际上非常简单。

### 第一步：创建文章

```
hexo new "新的学习笔记"
```

### 第二步：写 Markdown

编辑：

```
source/_posts/新的学习笔记.md
```

### 第三步：本地预览

```
hexo server
```

访问：

```
http://localhost:4000
```

### 第四步：提交

```
git add .
git commit -m "Add new study note"
```

### 第五步：发布

```
git push
```

之后 GitHub Actions 自动完成构建和部署。

因此完整流程可以归纳为：

```
学习
 ↓
写 Markdown
 ↓
hexo server
 ↓
本地检查
 ↓
git add
 ↓
git commit
 ↓
git push
 ↓
GitHub Actions
 ↓
博客自动更新
```

## 11. 后续计划

目前暂时不准备给博客增加太复杂的功能。

下一步可能逐渐加入：

- 更简洁的主题；
- 数学公式支持；
- 代码高亮；
- 文章分类和标签；
- 搜索；
- 自定义域名。

但目前最重要的目标还是：

> 保持记录，而不是花大量时间折腾博客本身。

先让写博客成为学习流程的一部分，再逐渐优化网站。
