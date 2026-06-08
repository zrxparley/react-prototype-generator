---
name: antd-react-prototype
description: Generate React UI prototypes using dual architecture - Vite + TypeScript + Ant Design (国内架构) OR Vite + TypeScript + Tailwind CSS v4 + Radix UI (国际架构). Use this skill when user requests creating React prototypes/pages. Triggers include "用 React 做一个...", "生成 React 页面", "用 Ant Design 做一个...", "React 原型", "国际架构", "Tailwind".
agent_created: true
---

# React UI Prototype Generator (Dual Architecture)

Generate React prototypes using **Vite + TypeScript** with choice of UI framework:

1. **国内架构**: Vite + TypeScript + **Ant Design (antd)**
2. **国际架构**: Vite + TypeScript + **Tailwind CSS v4 + Radix UI**

## Architecture Selection

Ask user which architecture to use:
- **国内架构** (Ant Design): Enterprise UI, rich components, Chinese-friendly
- **国际架构** (Tailwind + Radix UI): Modern, customizable, headless components

If user doesn't specify, **default to 国内架构 (Ant Design)**.

## Overview

This skill generates complete Vite + TypeScript projects (not single HTML files) because:
- Ant Design **does NOT support CDN/UMD** (requires build tools)
- Tailwind CSS v4 requires build tools (Vite plugin)
- TypeScript provides type safety, better DX, and is the industry standard
- Vite provides best DX (HMR, fast builds, TypeScript support out of the box)

## When to Use This Skill

Trigger this skill when the user:
- Asks to create a React page/prototype (e.g., "用 React 做一个登录页面")
- Wants to use Ant Design components ("用 Ant Design 做一个...")
- Says "生成 React 原型", "React 后台管理"
- Mentions "国际架构", "Tailwind", "Radix UI"

---

## Approach 1: 国内架构 (Ant Design)

### Step 1: Generate Vite Project

Create a complete Vite + React + TypeScript project structure:

```bash
# 1. Create Vite project (TypeScript template)
npm create vite@latest <project-name> -- --template react-ts
cd <project-name>

# 2. Install Ant Design
npm install antd --save

# 3. (Optional) Install icons
npm install @ant-design/icons --save
```

### Step 2: Project Structure

Generate these files:

```
<project-name>/
├── index.html              # Vite entry HTML
├── package.json           # Dependencies
├── tsconfig.json          # TypeScript config
├── vite.config.ts         # Vite config (TypeScript)
├── src/
│   ├── main.tsx           # React entry
│   ├── App.tsx            # Main App component
│   ├── App.css            # App styles
│   └── style.css          # Global styles
└── dist/                  # Build output (after npm run build)
```

### Step 3: Template Files

**src/main.tsx**:
```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { ConfigProvider } from 'antd'
import zhCN from 'antd/locale/zh_CN'
import App from './App'
import './style.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <ConfigProvider locale={zhCN}>
      <App />
    </ConfigProvider>
  </React.StrictMode>
)
```

**src/App.tsx** (Example with Ant Design):
```tsx
import React, { useState, type FC } from 'react'
import { Layout, Menu, Button, Card, Table, Tag } from 'antd'
import type { MenuProps } from 'antd'
import { UserOutlined } from '@ant-design/icons'

const { Header, Sider, Content } = Layout

const App: FC = () => {
  const [collapsed, setCollapsed] = useState<boolean>(false)

  const menuItems: MenuProps['items'] = [
    { key: '1', icon: <UserOutlined />, label: '导航项1' },
    { key: '2', icon: <UserOutlined />, label: '导航项2' }
  ]

  return (
    <Layout style={{ minHeight: '100vh' }}>
      <Sider collapsible collapsed={collapsed} onCollapse={setCollapsed}>
        <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']} items={menuItems} />
      </Sider>
      <Layout>
        <Header style={{ background: 'white', padding: '0 16px' }}>
          <h3>页面标题</h3>
        </Header>
        <Content style={{ margin: 16 }}>
          <Card title="卡片标题">
            <Button type="primary">按钮</Button>
          </Card>
        </Content>
      </Layout>
    </Layout>
  )
}

export default App
```

### Step 4: Deliver

After generating the project:

1. **Provide the complete project structure** (all files)
2. **Tell user how to run it**:
   ```bash
   cd <project-name>
   npm install
   npm run dev
   ```
3. **Tell user how to build for production**:
   ```bash
   npm run build  # Output: dist/ folder
   ```

---

## Approach 2: 国际架构 (Tailwind CSS v4 + Radix UI)

**⚠️ Important**: Use **Tailwind CSS v4** (NOT v3)

### Step 1: Generate Vite Project

```bash
# 1. Create Vite project (TypeScript template)
npm create vite@latest <project-name> -- --template react-ts
cd <project-name>

# 2. Install Tailwind CSS v4 + Vite plugin
npm install tailwindcss @tailwindcss/vite --save-dev

# 3. Install Radix UI primitives
npm install @radix-ui/react-dialog @radix-ui/react-dropdown-menu @radix-ui/react-tabs @radix-ui/react-popover @radix-ui/react-tooltip @radix-ui/react-progress

# 4. Install icons library
npm install lucide-react
```

### Step 2: Configure Vite

**vite.config.ts**:
```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

### Step 3: Configure Tailwind CSS v4

**src/index.css**:
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

### Step 4: Import CSS in main.tsx

**src/main.tsx**:
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

### Step 5: Create Components with Radix UI

**src/App.tsx**:
```tsx
import React, { useState, type FC } from 'react'
import { LayoutDashboard, Users, Pill, Activity, Bell, Settings, Menu, X, ChevronDown } from 'lucide-react'

// Sidebar Component
const Sidebar: FC<{ isOpen: boolean; onClose: () => void }> = ({ isOpen, onClose }) => {
  const menuItems = [
    { icon: <LayoutDashboard size={20} />, label: 'Dashboard', active: true },
    { icon: <Users size={20} />, label: '患者信息', active: false },
    { icon: <Pill size={20} />, label: '用药管理', active: false },
  ]

  return (
    <>
      {/* Mobile overlay */}
      {isOpen && (
        <div 
          className="fixed inset-0 z-40 bg-black/50 lg:hidden"
          onClick={onClose}
        />
      )}
      
      {/* Sidebar */}
      <aside className={`
        fixed left-0 top-0 z-50 h-screen w-64 transform bg-primary-900 transition-transform duration-200 ease-in-out lg:translate-x-0 lg:static lg:z-0
        ${isOpen ? 'translate-x-0' : '-translate-x-full'}
      `}>
        <div className="flex h-16 items-center justify-between px-6">
          <h1 className="text-xl font-bold text-white">慢病管理平台</h1>
          <button 
            onClick={onClose}
            className="text-white lg:hidden"
          >
            <X size={20} />
          </button>
        </div>
        
        <nav className="mt-8 px-4">
          {menuItems.map((item, index) => (
            <a
              key={index}
              href="#"
              className={`
                mb-2 flex items-center gap-3 rounded-lg px-4 py-3 text-sm font-medium transition-colors
                ${item.active 
                  ? 'bg-primary-800 text-white' 
                  : 'text-primary-100 hover:bg-primary-800 hover:text-white'
                }
              `}
            >
              {item.icon}
              {item.label}
            </a>
          ))}
        </nav>
      </aside>
    </>
  )
}

// Main App Component
const App: FC = () => {
  const [sidebarOpen, setSidebarOpen] = useState(false)

  return (
    <div className="min-h-screen bg-gray-50">
      <Sidebar isOpen={sidebarOpen} onClose={() => setSidebarOpen(false)} />
      
      <div className="lg:pl-64">
        <header className="sticky top-0 z-30 flex h-16 items-center justify-between border-b bg-white px-6 shadow-sm">
          <button 
            onClick={() => setSidebarOpen(true)}
            className="text-gray-600 lg:hidden"
          >
            <Menu size={24} />
          </button>
          
          <h2 className="text-lg font-semibold text-gray-900">Dashboard</h2>
          
          <div className="flex items-center gap-4">
            <button className="relative rounded-full p-2 text-gray-600 hover:bg-gray-100">
              <Bell size={20} />
              <span className="absolute right-1 top-1 flex h-5 w-5 items-center justify-center rounded-full bg-red-500 text-xs text-white">
                3
              </span>
            </button>
          </div>
        </header>
        
        <main className="p-6">
          <h1 className="text-2xl font-bold text-gray-900">Welcome to Tailwind v4 + Radix UI</h1>
        </main>
      </div>
    </div>
  )
}

export default App
```

### Step 6: Deliver

After generating the project:

1. **Provide the complete project structure** (all files)
2. **Tell user how to run it**:
   ```bash
   cd <project-name>
   npm install
   npm run dev
   ```
3. **Tell user how to build for production**:
   ```bash
   npm run build  # Output: dist/ folder
   ```

---

## Ant Design 6.x Important API Changes

### ⚠️ Deprecated APIs (DO NOT USE)

| Deprecated API | Replacement | Component |
|----------------|-------------|-----------|
| `Statistic.valueStyle` | `styles.content` | Statistic |
| `Alert.message` | `title` | Alert |
| `List` component | Custom rendering with `div` | List |

### ✅ Correct Usage Examples

**Statistic with custom color:**
```tsx
// ❌ Deprecated
<Statistic valueStyle={{ color: 'red' }} />

// ✅ Correct (Ant Design 6)
<Statistic styles={{ content: { color: 'red' } }} />
```

**Alert with title:**
```tsx
// ❌ Deprecated
<Alert message="标题" description="内容" />

// ✅ Correct (Ant Design 6)
<Alert title="标题" description="内容" />
```

---

## TypeScript Best Practices

### Define Interfaces for Data

```typescript
interface User {
  id: string
  name: string
  age: number
  status: 'active' | 'inactive'
}

interface TableRecord {
  key: string
  name: string
  age: number
  status: string
}
```

### Use Ant Design Type Exports

```typescript
import type { MenuProps, TableColumnsType } from 'antd'

const menuItems: MenuProps['items'] = [...]
const columns: TableColumnsType<TableRecord> = [...]
```

### Component Type Definition

```typescript
import type { FC } from 'react'

const App: FC = () => { ... }
// or with props
interface AppProps {
  title: string
}
const App: FC<AppProps> = ({ title }) => { ... }
```

---

## Important Notes

### For 国内架构 (Ant Design):
- **NO CDN approach** - Ant Design requires build tools (Vite/webpack)
- **Use TypeScript** - Type safety, better DX, industry standard
- **Use Vite** - Best DX (HMR, fast builds, TypeScript support out of the box)
- **Ant Design 6.x** - Uses CSS-in-JS (no separate CSS import needed)
- **Build output** - `npm run build` generates `dist/` folder (can be deployed to any static server)
- **Hot Module Replacement (HMR)** - Vite provides instant updates during development

### For 国际架构 (Tailwind + Radix UI):
- **Use Tailwind CSS v4** - Latest version with CSS-based configuration
- **Install @tailwindcss/vite plugin** - Required for Vite integration
- **NO tailwind.config.js** - All configuration in CSS via `@theme` directive
- **NO postcss.config.js** - Not needed in v4
- **Use Radix UI for components** - Headless, accessible, customizable
- **Use lucide-react for icons** - Modern, tree-shakeable icon library

---

## Tailwind CSS v4 Key Differences

### Configuration

**v3 (Old)**:
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

**v4 (New)**:
```css
/* src/index.css */
@import "tailwindcss";

@theme {
  --color-primary-500: #3b82f6;
}
```

### Vite Config

**v3**: Uses PostCSS

**v4**: Uses Vite plugin
```typescript
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

---

## References

- `references/antd-components.md` - Ant Design component API reference
- `references/tailwind-radix-guide.md` - Tailwind CSS v4 + Radix UI setup guide (国际架构)
- `references/vite-setup.md` - Vite configuration guide

---

## Example: Complete Project Generation

When user says "用 Ant Design 做一个登录页面":

1. Create Vite project structure with TypeScript
2. Generate `index.html`, `src/main.tsx`, `src/App.tsx`, `package.json`, `tsconfig.json`
3. Include Ant Design components (Form, Input, Button, Card, etc.)
4. Add TypeScript interfaces for form data
5. Provide instructions to run:
   ```bash
   cd login-page
   npm install
   npm run dev
   ```

When user says "用国际架构做一个登录页面" or "用 Tailwind 做一个...":

1. Create Vite project structure with TypeScript
2. Install Tailwind CSS v4 + Radix UI
3. Configure vite.config.ts with @tailwindcss/vite plugin
4. Generate `src/index.css` with @import "tailwindcss" and @theme
5. Create components using Tailwind utility classes + Radix UI primitives
6. Provide instructions to run:
   ```bash
   cd login-page
   npm install
   npm run dev
   ```
