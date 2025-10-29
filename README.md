# 简约主页说明

这是一个简约的个人主页模板，参考了 [zhuohan123.github.io](https://github.com/zhuohan123/zhuohan123.github.io) 的设计风格。

## 文件结构

```
.
├── index.html              # 主页 HTML 文件
├── assets/
│   ├── css/               # 样式文件
│   │   ├── font_sans_serif.css
│   │   ├── style-no-dark-mode.css
│   │   └── publications-no-dark-mode.css
│   ├── js/                # JavaScript 文件
│   │   └── scale.fix.js
│   └── img/               # 图片资源
│       ├── avatar.png     # 头像图片（需要提供）
│       └── favicon.png    # 网站图标（可选）
└── README.md       # 本说明文件
```

## 使用方法

1. **替换头像**：将你的头像图片放在 `assets/img/avatar.png` 或 `assets/img/avatar.jpg`
2. **修改个人信息**：编辑 `index.html` 文件，更新：
   - 姓名、邮箱
   - 社交链接
   - 关于我、教育背景、项目、出版物等信息
3. **部署**：直接推送到 GitHub Pages，或者通过其他静态网站托管服务部署

## 关于 Hugo

如果你不再需要 Hugo，可以删除以下文件/文件夹：
- `content/` - Hugo 内容文件
- `config/` - Hugo 配置文件
- `layouts/` - Hugo 布局文件
- `hugo.yaml`, `hugo_stats.json` 等 Hugo 相关文件
- `go.mod`, `go.sum` - Go 模块文件
- `package.json`, `package-lock.json`, `node_modules/` - Node.js 依赖（如果不再需要）

保留的文件：
- `index.html` - 主页
- `assets/` - 静态资源
- `static/` - 如果需要保留某些静态文件

## 自定义

- 修改颜色：编辑 `assets/css/style-no-dark-mode.css` 中的颜色值（如 `#39c`）
- 修改字体：编辑 `assets/css/font_sans_serif.css`
- 添加内容：直接在 `index.html` 中添加新的 section

