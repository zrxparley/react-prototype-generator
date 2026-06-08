# Tailwind CSS v4 + Radix UI 参考指南

## 概述
本指南介绍如何使用 Tailwind CSS v4 和 Radix UI 构建现代化 React 原型。

## 技术栈
- **Tailwind CSS v4**: 最新的 CSS 框架，使用 CSS 原生配置
- **Radix UI**: Headless UI 组件库，提供无障碍的底层组件
- **Vite**: 构建工具
- **React 18+**: UI 框架
- **TypeScript**: 类型安全

## Tailwind CSS v4 重大变化

### 1. 配置方式改变
**v3 (旧版)**:
```js
// tailwind.config.js
module.exports = {
  content: ['./src/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: {
      colors: {
        primary: '#2563eb',
      },
    },
  },
}
```

**v4 (新版)**:
```css
/* src/index.css */
@import "tailwindcss";

@theme {
  --color-primary-50: #eff6ff;
  --color-primary-500: #3b82f6;
  --color-primary-900: #1e3a8a;
}
```

### 2. Vite 插件必需
v4 需要使用 `@tailwindcss/vite` 插件：

```typescript
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

### 3. 不再需要 postcss.config.js
v4 不需要 PostCSS 配置。

### 4. 不再需要 tailwind.config.js
所有配置都在 CSS 文件中通过 `@theme` 指令完成。

## 安装步骤

### 1. 创建 Vite + React + TypeScript 项目
```bash
npm create vite@latest my-project -- --template react-ts
cd my-project
```

### 2. 安装 Tailwind v4 和 Radix UI
```bash
npm install tailwindcss @tailwindcss/vite
npm install @radix-ui/react-dialog @radix-ui/react-dropdown-menu @radix-ui/react-tabs @radix-ui/react-popover @radix-ui/react-tooltip @radix-ui/react-progress
npm install lucide-react  # 图标库
```

### 3. 配置 vite.config.ts
```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

### 4. 创建 src/index.css
```css
@import "tailwindcss";

@theme {
  --color-primary-50: #eff6ff;
  --color-primary-100: #dbeafe;
  --color-primary-200: #bfdbfe;
  --color-primary-300: #93c5fd;
  --color-primary-400: #60a5fa;
  --color-primary-500: #3b82f6;
  --color-primary-600: #2563eb;
  --color-primary-700: #1d4ed8;
  --color-primary-800: #1e40af;
  --color-primary-900: #1e3a8a;
}

body {
  background-color: var(--color-gray-50);
  color: var(--color-gray-900);
}
```

### 5. 在 src/main.tsx 中导入 CSS
```typescript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```

## 使用 Radix UI 组件

### Dialog (对话框)
```typescript
import * as Dialog from '@radix-ui/react-dialog'

function MyDialog() {
  return (
    <Dialog.Root>
      <Dialog.Trigger asChild>
        <button className="btn-primary">打开对话框</button>
      </Dialog.Trigger>
      <Dialog.Portal>
        <Dialog.Overlay className="fixed inset-0 bg-black/50" />
        <Dialog.Content className="fixed left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 bg-white p-6 rounded-lg shadow-lg">
          <Dialog.Title className="text-lg font-semibold">对话框标题</Dialog.Title>
          <Dialog.Description className="mt-2 text-gray-600">
            对话框内容描述
          </Dialog.Description>
          <Dialog.Close className="absolute top-4 right-4">
            <X size={20} />
          </Dialog.Close>
        </Dialog.Content>
      </Dialog.Portal>
    </Dialog.Root>
  )
}
```

### Dropdown Menu (下拉菜单)
```typescript
import * as DropdownMenu from '@radix-ui/react-dropdown-menu'

function MyDropdown() {
  return (
    <DropdownMenu.Root>
      <DropdownMenu.Trigger asChild>
        <button className="btn-secondary">
          选项 <ChevronDown size={16} />
        </button>
      </DropdownMenu.Trigger>
      <DropdownMenu.Portal>
        <DropdownMenu.Content className="bg-white rounded-lg shadow-lg p-2 min-w-[150px]">
          <DropdownMenu.Item className="px-3 py-2 hover:bg-gray-100 rounded cursor-pointer">
            选项 1
          </DropdownMenu.Item>
          <DropdownMenu.Item className="px-3 py-2 hover:bg-gray-100 rounded cursor-pointer">
            选项 2
          </DropdownMenu.Item>
        </DropdownMenu.Content>
      </DropdownMenu.Portal>
    </DropdownMenu.Root>
  )
}
```

### Tabs (标签页)
```typescript
import * as Tabs from '@radix-ui/react-tabs'

function MyTabs() {
  return (
    <Tabs.Root defaultValue="tab1">
      <Tabs.List className="flex border-b">
        <Tabs.Trigger value="tab1" className="px-4 py-2 border-b-2 border-transparent data-[state=active]:border-primary-600">
          标签 1
        </Tabs.Trigger>
        <Tabs.Trigger value="tab2" className="px-4 py-2 border-b-2 border-transparent data-[state=active]:border-primary-600">
          标签 2
        </Tabs.Trigger>
      </Tabs.List>
      <Tabs.Content value="tab1" className="p-4">
        内容 1
      </Tabs.Content>
      <Tabs.Content value="tab2" className="p-4">
        内容 2
      </Tabs.Content>
    </Tabs.Root>
  )
}
```

## Tailwind v4 常用工具类

### 布局
- `flex`, `grid`, `block`, `hidden`
- `items-center`, `justify-between`
- `grid-cols-1`, `grid-cols-2`, `lg:grid-cols-3`

### 间距
- `p-4`, `px-6`, `py-2` (padding)
- `m-4`, `mx-auto`, `mt-8` (margin)
- `gap-4`, `gap-6` (gap)

### 颜色
- `bg-white`, `bg-gray-50`, `bg-primary-600`
- `text-gray-900`, `text-primary-600`, `text-red-500`
- `border-gray-300`, `border-primary-600`

### 圆角和阴影
- `rounded`, `rounded-lg`, `rounded-full`
- `shadow`, `shadow-lg`, `shadow-none`

### 交互
- `hover:bg-primary-700`, `hover:text-white`
- `focus:outline-none`, `focus:ring-2`

## CSS 变量使用
在 Tailwind v4 中，可以使用 CSS 变量定义自定义样式：

```css
/* src/index.css */
@theme {
  --color-brand: #ff6347;
}

/* 在组件中使用 */
<div className="bg-[var(--color-brand)]">
  自定义颜色
</div>
```

## 常见问题

### 1. 构建错误："Can't resolve 'tailwindcss'"
**原因**: `tailwindcss` 包没有正确安装在项目的 `node_modules` 中。

**解决**:
```bash
npm install tailwindcss @tailwindcss/vite --save-dev
rm -rf node_modules dist
npm install
npm run build
```

### 2. `@import "tailwindcss"` 不生效
**原因**: `@tailwindcss/vite` 插件没有正确配置。

**解决**: 确保在 `vite.config.ts` 中正确导入和使用插件：
```typescript
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

### 3. 自定义颜色不生效
**原因**: `@theme` 指令语法错误。

**解决**: 确保在 `@theme` 块中正确定义变量：
```css
@theme {
  --color-primary-500: #3b82f6;
}
```

## 项目结构示例

```
my-project/
├── src/
│   ├── components/
│   │   ├── Sidebar.tsx
│   │   ├── Header.tsx
│   │   └── Dashboard.tsx
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── public/
├── index.html
├── package.json
├── tsconfig.json
└── vite.config.ts
```

## 下一步
- 学习 Radix UI 官方文档: https://www.radix-ui.com/primitives
- 学习 Tailwind CSS v4 文档: https://tailwindcss.com/docs
- 探索 Lucide React 图标库: https://lucide.dev/
