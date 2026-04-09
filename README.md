# 🚀 极简学术主页模板 (Minimal Academic Homepage)

这是一个基于 HTML/CSS 的极简学术主页模板，专为研究人员、学生和学者设计。它具有响应式设计、深色模式支持、优雅的排版以及易于定制的特点。

> [!TIP]
> 如果你觉得这个模板对你有帮助，欢迎给一个 Star 🌟！

## ✨ 特性

- **极简设计**：聚焦内容，去除冗余，参考了 [Claude.ai](https://claude.ai) 的视觉风格。
- **响应式布局**：在手机、平板和桌面端都有良好的显示效果。
- **深色模式**：支持手动切换和系统自动随动。
- **学术友好**：内置教育背景、研究经历、项目展示、论文列表（支持图标链接）和获奖情况等板块。
- **易于部署**：纯静态页面，无需任何构建步骤，直接托管在 GitHub Pages。

## 🛠️ 快速开始：定制你的主页

你可以通过以下步骤快速创建属于自己的主页：

### 1. Fork 本仓库
点击仓库右上角的 **Fork** 按钮，将代码克隆到你自己的 GitHub 账号下。

### 2. 修改个人信息
打开 `index.html` 文件，搜索并替换以下内容：
- **基本信息**：姓名、邮箱、头像路径。
- **社交链接**：修改 `social-icons` 部分的链接（GitHub, Google Scholar, LinkedIn 等）。
- **板块内容**：
  - `About Me`：简短的自我介绍。
  - `Education`：替换学校 Logo 和学位信息。
  - `Experience`：添加你的实习或研究经历。
  - `Publications`：按照格式添加你的论文。
  - `Awards`：列出你的荣誉。

### 3. 替换资源文件
- **头像**：将你的头像放入 `assets/img/` 并命名为 `avatar.png`。
- **Logo**：将学校或机构的 Logo 放入 `assets/img/`。
- **简历**：将你的 PDF 简历放入 `assets/cv/`。

### 4. 开启 GitHub Pages
在你的仓库设置中：
1. 进入 `Settings` -> `Pages`。
2. 在 `Build and deployment` 下，选择 `Deploy from a branch`。
3. 选择 `main` 分支和 `/ (root)` 目录，点击 `Save`。
4. 几分钟后，你的主页就会在 `https://<your-username>.github.io` 上线。

## 🎨 进阶定制

### 修改主题颜色
如果你想修改主题色（如链接颜色、强调色），可以编辑 `assets/css/theme-claude.css`。

### 访客地图
主页集成了 [ClustrMaps](https://clustrmaps.com/)。你可以去官网注册并获取你自己的地图 ID，然后替换 `index.html` 中 `updateMap` 函数里的相关参数。

## 📄 许可证
本项目采用 [MIT License](LICENSE.md) 开源。

---
由 [Yuheng Yang](https://github.com/wzsyyh) 维护。
