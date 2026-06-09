# React Prototype Generator Skill

> WorkBuddy Code Skill — 双架构 React 原型生成器

## 简介

一键生成完整可运行的 React 原型项目，支持两套主流技术架构：

| 架构 | 技术栈 | 适用场景 |
|------|---------|---------|
| **国内架构** | Vite + TypeScript + Ant Design | 企业后台、中文项目、开箱即用 |
| **国际架构** | Next.js 15 (App Router) + TypeScript + Tailwind CSS v4 + shadcn/ui | 现代化 UI、国际标准、全栈能力 |

## 如何使用

将本 Skill 安装到 WorkBuddy 后，直接用自然语言描述需求即可触发：

```
用 Ant Design 做一个慢病管理平台的 Dashboard 首页
用国际架构做一个登录页面
用 Next.js + shadcn 做一个数据可视化大屏
```

未指定架构时，**默认使用国内架构（Ant Design）**。

---

## 安装

将 `antd-react-prototype/` 文件夹复制到你的 WorkBuddy Skills 目录：

```bash
cp -r antd-react-prototype ~/.workbuddy/skills/
```

---

## 架构一：国内架构（Ant Design + Vite）

### 技术栈

- **Vite 8.x** — 极速 HMR、TypeScript 原生支持
- **React 18** + **TypeScript**
- **Ant Design 6.x** — 企业级 UI 组件库
- **@ant-design/icons** — 图标库

### 生成后使用

```bash
cd <project-name>
npm install
npm run dev      # 启动开发服务器（http://localhost:5173）
npm run build     # 构建生产版本（输出 dist/）
```

---

## 架构二：国际架构（Next.js 15 + shadcn/ui）

### shadcn/ui 是什么？

shadcn/ui **不是 npm 包**，而是一套**可复制源码的组件集合**：

- 底层基于 **Radix UI**（无障碍原语）+ **Tailwind CSS**（样式）
- 组件源码直接复制到你的项目（`src/components/ui/`）
- 你完全拥有代码，可以自由修改
- 40+ 现成组件，开箱即专业设计
- **Vercel 官方推荐**，Next.js 生态首选 UI 方案

### 技术栈

- **Next.js 15** (App Router) — 文件系统路由、React Server Components
- **React 19** + **TypeScript**
- **Tailwind CSS v4** — 最新版，CSS 原生配置
- **shadcn/ui** — 40+ 专业设计组件
- **Lucide React** — 图标库
- **next/font/google** — 字体优化（内置，无额外请求）

### 生成后使用

```bash
cd <project-name>
npm install
npm run dev        # 启动开发服务器（http://localhost:3000）
npx shadcn@latest add <component>   # 添加更多 shadcn 组件
npm run build      # 构建生产版本（输出 .next/）
npm start          # 启动生产服务器
```

### 常用 shadcn/ui 组件

```bash
npx shadcn@latest add button       # 按钮
npx shadcn@latest add card         # 卡片
npx shadcn@latest add dialog       # 模态框
npx shadcn@latest add input        # 输入框
npx shadcn@latest add select       # 下拉选择
npx shadcn@latest add table        # 表格
npx shadcn@latest add form         # 表单（配合 React Hook Form）
```

完整组件列表：https://ui.shadcn.com/docs/components

---

## 注意事项

### Ant Design 6.x 废弃 API 替换

| 废弃 API | 正确写法 | 组件 |
|---------|---------|------|
| `Statistic.valueStyle` | `styles.content` | Statistic |
| `Alert.message` | `title` | Alert |
| `List` 组件 | 手动 `div` 渲染 | List |

### Next.js + shadcn/ui 要点

- **shadcn/ui 不是 npm 包** — 组件源码复制到项目，完全可定制
- **App Router 是默认路由方式** — 文件系统路由（`src/app/page.tsx` = `/`）
- **Server Components 是默认** — 需要客户端交互时加 `"use client"` 指令
- **Tailwind v4** — 使用 `@theme {}` CSS 指令配置（不再需要 `tailwind.config.js`）
- **字体优化** — 使用 `next/font/google`（内置，无需额外 CDN）

---

## 生成的项目结构

### 国内架构（Vite + Ant Design）

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

### 国际架构（Next.js + shadcn/ui）

```
<project-name>/
├── src/
│   ├── app/
│   │   ├── layout.tsx        # 根布局
│   │   ├── page.tsx          # 首页
│   │   └── globals.css       # 全局样式
│   ├── components/
│   │   └── ui/              # shadcn/ui 组件
│   │       ├── button.tsx
│   │       ├── card.tsx
│   │       └── ...
│   └── lib/
│       └── utils.ts          # cn() 工具函数
├── next.config.ts
├── tailwind.config.ts         # v3 需要；v4 不需要
├── tsconfig.json
└── package.json
```

---

## 文件说明

```
antd-react-prototype/
├── SKILL.md                         # Skill 主文件（触发词、生成流程）
├── README.md                        # 本文件
├── assets/
│   └── template-antd.html         # Ant Design HTML 模板参考
└── references/
    ├── antd-components.md          # Ant Design 组件 API 参考
    ├── next-shadcn-guide.md      # Next.js 15 + shadcn/ui 配置指南
    ├── tailwind-radix-guide.md    # Tailwind v4 + Radix UI 配置指南（旧版）
    ├── tdesign-components.md
    └── tdesign-react-setup.md
```

---

## 版本历史

| 版本 | 日期 | 说明 |
|------|------|------|
| v1.0.0 | 2026-06-08 | 首次发布，支持双架构（国内：Vite+Antd，国际：Vite+Tailwind+Radix） |
| v1.1.0 | 2026-06-08 | 国际架构升级：Vite+Tailwind+Radix → **Next.js 15 + shadcn/ui** |

---

## License

MIT
