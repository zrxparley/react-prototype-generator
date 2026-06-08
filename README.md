# React Prototype Generator Skill

> WorkBuddy Code Skill — 双架构 React 原型生成器

## 简介

一键生成完整可运行的 React 原型项目，支持两套主流技术架构：

| 架构 | 技术栈 | 适用场景 |
|------|---------|---------|
| **国内架构** | Vite + TypeScript + Ant Design | 企业后台、中文项目、开箱即用 |
| **国际架构** | Vite + TypeScript + Tailwind CSS v4 + Radix UI | 现代化 UI、高度定制、无头组件 |

## 如何使用

将本 Skill 安装到 WorkBuddy 后，直接用自然语言描述需求即可触发：

```
用 Ant Design 做一个慢病管理平台的 Dashboard 首页
用国际架构做一个登录页面
用 Tailwind 做一个数据可视化大屏
```

未指定架构时，**默认使用国内架构（Ant Design）**。

## 安装

将 `antd-react-prototype/` 文件夹复制到你的 WorkBuddy Skills 目录：

```bash
cp -r antd-react-prototype ~/.workbuddy/skills/
```

## 生成的项目结构

```
<project-name>/
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   └── index.css
└── dist/          # npm run build 输出
```

生成后直接运行：

```bash
cd <project-name>
npm install
npm run dev      # 启动开发服务器（http://localhost:5173）
npm run build     # 构建生产版本
```

## 技术栈

- **React 18** + **TypeScript**（全部源码为 `.tsx`，非 JavaScript）
- **Vite 8.x**（HMR、极速构建）
- **Ant Design 6.x** / **Tailwind CSS v4** + **Radix UI**
- **Lucide React**（图标库）

## 注意事项

### Ant Design 6.x 废弃 API 替换

| 废弃 API | 正确写法 | 组件 |
|---------|---------|------|
| `Statistic.valueStyle` | `styles.content` | Statistic |
| `Alert.message` | `title` | Alert |
| `List` 组件 | 手动 `div` 渲染 | List |

### Tailwind CSS v4 要点

- 使用 `@tailwindcss/vite` Vite 插件（不再需要 `postcss.config.js`）
- 自定义主题变量写在 `src/index.css` 的 `@theme { }` 块中（不再需要 `tailwind.config.js`）
- 确保 CSS 文件中有 `@source "../src/**/*.{tsx,ts,jsx,js}";` 以正确扫描类名

## 文件说明

```
antd-react-prototype/
├── SKILL.md                    # Skill 主文件（触发词、生成流程）
├── assets/
│   └── template-antd.html      # Ant Design HTML 模板参考
└── references/
    ├── antd-components.md      # Ant Design 组件 API 参考
    ├── tailwind-radix-guide.md # Tailwind v4 + Radix UI 配置指南
    ├── tdesign-components.md
    └── tdesign-react-setup.md
```

## 版本历史

| 版本 | 日期 | 说明 |
|------|------|------|
| v1.0.0 | 2026-06-08 | 首次发布，支持双架构 |

## License

MIT
