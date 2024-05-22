---
title: "使用 Jekyll 搭建博客"
tags:
    - Jekyll
    - 博客
    - markdown
date: "2024-05-22"
bookmark: true
thumbnail: "/assets/img/thumbnail/bricks.webp"
---

# 使用 Jekyll 搭建博客

Jekyll 是一个静态网站生成器，可以将 Markdown 文件转换为静态网站。它非常适合搭建博客。本文将指导你如何在本地环境中使用 Jekyll 搭建一个简单的博客。

## 前提条件

在开始之前，请确保你的系统满足以下条件：

1. 已安装 [Ruby](https://www.ruby-lang.org/en/downloads/)
2. 已安装 [RubyGems](https://rubygems.org/pages/download)
3. 已安装 [Bundler](https://bundler.io/)

你可以通过运行以下命令来检查是否已安装这些工具：

```bash
ruby -v
gem -v
bundle -v
```

## 步骤一：安装 Jekyll 和 Bundler

在终端中运行以下命令安装 Jekyll 和 Bundler：

```bash
gem install jekyll bundler
```

## 步骤二：创建新的 Jekyll 网站

使用 Jekyll 命令行工具创建一个新的 Jekyll 网站：

```bash
jekyll new myblog
cd myblog
```

这将生成一个名为 `myblog` 的目录，包含 Jekyll 的默认文件结构。

## 步骤三：安装依赖

在项目目录中运行以下命令安装所需的依赖：

```bash
bundle install
```

## 步骤四：启动 Jekyll 服务器

运行以下命令启动 Jekyll 服务器：

```bash
bundle exec jekyll serve
```

打开浏览器并访问 `http://localhost:4000`，你应该能看到 Jekyll 默认生成的博客页面。

## 步骤五：自定义配置

编辑 `_config.yml` 文件来自定义你的博客配置。例如，可以修改站点标题、作者信息等：

```yaml
title: My Awesome Blog
author: John Doe
email: john.doe@example.com
description: >- # this means to ignore newlines until "baseurl:"
  A simple blog built with Jekyll.
baseurl: "" # the subpath of your site, e.g. /blog
url: "http://example.com" # the base hostname & protocol for your site
```

## 步骤六：添加新文章

在 `_posts` 目录中添加新的 Markdown 文件来创建文章。文件名格式为 `YYYY-MM-DD-title.md`，例如 `2024-05-21-welcome-to-jekyll.md`。以下是一个示例文章内容：

```markdown
---
layout: post
title: "Welcome to Jekyll!"
date: 2024-05-21 12:00:00 -0000
categories: jekyll update
---

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `bundle exec jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. For example, the following are valid post filenames:

```markdown
2021-04-25-welcome-to-jekyll.md
2021-04-25-welcome-to-jekyll.textile
```

You can find more information about creating posts [in the Jekyll documentation](https://jekyllrb.com/docs/posts/).

Enjoy blogging with Jekyll!

```

## 步骤七：部署博客

你可以将 Jekyll 生成的静态文件部署到任何静态文件托管服务，如 GitHub Pages。以下是在 GitHub Pages 上部署的简要步骤：

1. 创建一个新的 GitHub 仓库。
2. 在 `_config.yml` 文件中设置 `baseurl` 和 `url`。
3. 将你的 Jekyll 项目推送到 GitHub 仓库。

## 结论

通过以上步骤，你已经在本地环境中成功搭建了一个 Jekyll 博客。Jekyll 提供了丰富的自定义选项和插件，可以根据你的需求进行扩展和美化。享受你的博客创作之旅吧！

---

如果你在使用过程中遇到问题，可以参考 Jekyll 的[官方文档](https://jekyllrb.com/docs/)或在社区寻求帮助。
```
