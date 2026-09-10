# enzopodwiki.github.io

个人项目展示站：Hugo（Stack 主题）+ GitHub Pages 自动部署 + Pages CMS 网页后台管理。

- 网站地址：<https://enzopodwiki.github.io>
- 后台管理：<https://app.pagescms.org>（用 GitHub 账号登录，选择本仓库）

## 日常用法：在 Pages CMS 后台维护（推荐）

1. 打开 <https://app.pagescms.org>，用 GitHub 账号登录，选择 `enzopodwiki/enzopodwiki.github.io` 仓库。
2. 左侧「项目」里可以新建 / 编辑 / 删除项目；「关于页」可以编辑自我介绍。
3. 封面图直接在编辑器里上传，自动存入 `static/images/`。
4. 点保存后 CMS 自动提交到 GitHub，Actions 约 1-2 分钟后网站自动更新。

字段说明：

| 字段 | 作用 |
| --- | --- |
| 项目名称 | 卡片标题，也用于生成文件名 |
| 一句话简介 | 显示在卡片标题下方 |
| 封面图 | 卡片配图，建议 1200x630 |
| 标签 | 显示在卡片底部，可加多个 |
| 相关链接 | 显示在项目页底部（GitHub / 在线演示等） |
| 项目详情 | 正文，进入项目页后显示 |

后台不需要写命令行，也不会用到本仓库以外的东西。

## 命令行方式（备选）

```bash
# 本地预览：浏览器打开 http://localhost:1313
hugo server -D

# 写完内容后发布：提交推送即可自动部署
git add -A && git commit -m "更新项目" && git push
```

## 以后要加博客板块（两步）

1. 创建目录 `content/post/`，放入文章 md（front matter 用 title/date/draft/description/tags）。
2. 打开本仓库根目录的 `.pages.yml`，取消 `posts` 那一段的注释并提交——CMS 后台就会出现「博客文章」菜单。

想让博客文章出现在首页列表的话，把 `hugo.yaml` 里 `params.mainSections` 改为：

```yaml
mainSections:
    - projects
    - post
```

## 目录结构

```
├── hugo.yaml            # 站点配置（标题、菜单、侧栏、主题参数）
├── .pages.yml           # Pages CMS 后台配置（项目/关于页的字段）
├── content/
│   ├── projects/        # 项目页（首页卡片对应这里）
│   └── about.md         # 关于页
├── static/images/       # 封面图等静态图片
├── themes/hugo-theme-stack  # Stack 主题（git submodule，锁定 v4.0.3）
└── .github/workflows/hugo.yml  # GitHub Actions 自动部署
```

## 升级主题

```bash
git -C themes/hugo-theme-stack fetch --tags
git -C themes/hugo-theme-stack checkout <新版本号>
git add themes/hugo-theme-stack && git commit -m "升级主题" && git push
```
