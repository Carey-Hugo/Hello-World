---
name: personal-intro-page
overview: 将现有的 Hello World 单页改造为完整的个人介绍网页，包含姓名头像、个人简介、技能展示、联系方式四大模块，保持现有暗色科技风格。
design:
  architecture:
    framework: html
  styleKeywords:
    - Glassmorphism
    - 暗色科技风
    - 紫色渐变主题
    - 微动效
    - 极简布局
  fontSystem:
    fontFamily: Poppins
    heading:
      size: 48px
      weight: 700
    subheading:
      size: 24px
      weight: 600
    body:
      size: 16px
      weight: 400
  colorSystem:
    primary:
      - "#667eea"
      - "#764ba2"
    background:
      - "#0f172a"
      - "#1e293b"
      - rgba(255,255,255,0.04)
    text:
      - "#ffffff"
      - "#94a3b8"
      - "#64748b"
    functional:
      - "#22d3ee"
      - "#f472b6"
      - "#34d399"
todos:
  - id: build-personal-page
    content: 改造 index.html，新增导航栏、Hero、About、Skills、Contact 四大区块及完整样式与交互
    status: completed
---

## 用户需求

将现有的 `index.html` Hello World 单页改造为一个完整的**个人介绍网页**，保留现有暗色科技风设计风格，扩展为多模块滚动页面。

## 产品概述

一个基于纯 HTML + CSS 的单文件个人主页，采用暗色背景配紫色渐变主题，支持响应式布局，兼容桌面与移动端浏览器。

## 核心功能

- **Hero 区域**：展示头像（圆形渐变占位头像）、姓名、职位描述，配有入场动效
- **About Me 区域**：个人简介段落，卡片式布局，含左侧装饰线
- **Skills 区域**：技能标签云 + 带动态加载进度条的技能展示
- **Contact 区域**：邮箱、GitHub、LinkedIn 等联系方式图标链接
- **导航栏**：顶部固定导航，点击锚点平滑滚动至对应区域
- **滚动动效**：页面滚动时各模块依次淡入，增强视觉层次感

## 技术栈

- **结构**：纯 HTML5 语义化标签
- **样式**：原生 CSS3（CSS 变量、Flexbox、Grid、动画、媒体查询）
- **交互**：原生 JavaScript（IntersectionObserver 滚动动效、平滑导航）
- **字体**：Google Fonts（Poppins）
- **图标**：SVG 内联图标（零依赖）

## 实现方案

在现有文件基础上全面扩展，保留 `--primary-gradient`、`--bg-color`、`bg-glow` 等已有 CSS 变量和视觉元素，将单屏布局改为多区块垂直滚动页面。

### 关键技术决策

1. **单文件方案**：所有 CSS、JS 内联于 `index.html`，无需构建工具，与现有项目结构保持一致
2. **IntersectionObserver**：替代 scroll 事件监听，性能更优，实现各区块入场动效
3. **CSS 进度条动画**：使用 `@keyframes` + CSS 变量控制宽度，纯 CSS 实现，无需 JS 操控 DOM 样式
4. **CSS Grid + Flexbox**：Skills 区域使用 Grid 布局，Contact 使用 Flexbox，响应式断点 `640px`

## 架构设计

```
index.html
├── <head>  Google Fonts + CSS变量扩展
├── <nav>   固定顶部导航（锚点链接）
├── <main>
│   ├── #hero     头像 / 姓名 / 职位 / CTA按钮
│   ├── #about    个人简介卡片
│   ├── #skills   技能标签 + 进度条
│   └── #contact  联系方式图标列表
└── <script> IntersectionObserver 滚动动效
```

## 目录结构

```
e:/AI小程序&智能体/Hello World/
└── index.html   # [MODIFY] 在现有文件基础上全面扩展，保留暗色科技风视觉体系，新增 nav/hero/about/skills/contact 四大区块及对应样式与交互脚本
```

## 实现注意事项

- 保留现有 `bg-glow` 背景光晕效果，移至 Hero 区域作为装饰
- 进度条动画通过 `data-width` 属性配合 IntersectionObserver 触发，避免页面加载即播放
- 导航栏使用 `backdrop-filter: blur` 实现磨玻璃效果，与暗色背景融合
- 移动端导航折叠为汉堡菜单，断点 `768px`

## 设计风格

延续现有暗色科技风基调，在 `#0f172a` 深蓝黑背景上，以 `#667eea → #764ba2` 紫色渐变为主题色，融合 Glassmorphism 玻璃拟态卡片与微动效，打造高级感个人主页。

### 页面结构

**导航栏（Nav）**
固定顶部，高度 64px，半透明磨玻璃背景 `rgba(15,23,42,0.8) + backdrop-filter:blur(12px)`，左侧品牌名渐变文字，右侧 Hero / About / Skills / Contact 锚点链接，hover 时下划线动效。

**Hero 区块**
全屏高度居中布局，顶部保留 bg-glow 光晕。圆形头像（100px，渐变边框描边）+ 姓名（48px，渐变文字）+ 职位标签（chip 样式）+ 一句话简介 + "联系我" CTA 按钮（渐变填充，hover 上浮阴影）。入场动效：fadeInDown + fadeInUp 交替。

**About Me 区块**
居中最大宽度 720px 卡片，`rgba(255,255,255,0.04)` 玻璃背景 + `1px` 渐变边框，左侧 4px 紫色竖线装饰，正文字号 1.1rem，行高 1.8，字色 `#94a3b8`。滚动进入时 fadeInUp。

**Skills 区块**
上方技能标签云（flex wrap，每个 tag 渐变描边圆角 pill），下方 4 条进度条（标签 + 百分比数字 + 动态填充条），进度条背景 `rgba(255,255,255,0.08)`，填充渐变与主题一致。滚动触发进度条动画。

**Contact 区块**
三个联系方式卡片水平排列（Grid 3列，移动端 1列），每卡片含 SVG 图标 + 平台名 + 地址文字，hover 时卡片上浮 + 边框高亮。底部版权信息。