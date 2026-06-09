---
name: antd-react-prototype
description: Generate React UI prototypes using dual architecture - Vite + TypeScript + Ant Design (国内架构) OR Next.js 15 (App Router) + TypeScript + Tailwind CSS v4 + shadcn/ui (国际架构). Use this skill when user requests creating React prototypes/pages. Triggers include "用 React 做一个...", "生成 React 页面", "用 Ant Design 做一个...", "React 原型", "国际架构", "Next.js", "shadcn".
agent_created: true
---

# React UI Prototype Generator (Dual Architecture)

Generate React prototypes with **two professional architectures**:

1. **国内架构**: Vite + TypeScript + **Ant Design (antd)**
2. **国际架构**: Next.js 15 (App Router) + TypeScript + **Tailwind CSS v4 + shadcn/ui**

## Architecture Selection

Ask user which architecture to use:
- **国内架构** (Ant Design): Enterprise UI, rich components, Chinese-friendly
- **国际架构** (Next.js + shadcn/ui): Modern full-stack, beautiful design system, international standard

If user doesn't specify, **default to 国内架构 (Ant Design)**.

## Overview

This skill generates complete projects (not single HTML files) because:
- Ant Design **does NOT support CDN/UMD** (requires build tools)
- Next.js requires build tools (node_modules, bundler)
- TypeScript provides type safety, better DX, and is the industry standard
- Vite (国内) / Next.js (国际) provide best DX (HMR, fast builds, TypeScript support)

---

## Approach 1: 国内架构 (Ant Design + Vite)

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

## Approach 2: 国际架构 (Next.js 15 + Tailwind CSS v4 + shadcn/ui)

**⚠️ Important**: Use **Next.js 15 (App Router)** + **Tailwind CSS v4** + **shadcn/ui**

### Why shadcn/ui?

shadcn/ui is NOT a npm package — it's a **copy-paste component collection**:
- Built on **Radix UI** (accessible primitives) + **Tailwind CSS** (styling)
- You own the component source code (fully customizable)
- 40+ beautiful, accessible components out of the box
- Recommended by **Vercel** (Next.js creators)
- The current international standard for React UI

### Step 1: Generate Next.js Project

```bash
# 1. Create Next.js project (App Router + TypeScript)
npx create-next-app@latest <project-name> --typescript --tailwind --eslint --app --src-dir --import-alias "@/*"
cd <project-name>

# 2. Initialize shadcn/ui
npx shadcn@latest init

# 3. Install commonly used shadcn components
npx shadcn@latest add button card dialog dropdown-menu input label select table tabs badge avatar
```

### Step 2: Project Structure

Generate these files:

```
<project-name>/
├── src/app/
│   ├── layout.tsx        # Root layout (fonts, ThemeProvider)
│   ├── page.tsx          # Home page
│   ├── globals.css       # Tailwind + shadcn variables
│   └── fonts/
├── src/components/
│   └── ui/              # shadcn/ui components (button.tsx, card.tsx, etc.)
├── next.config.ts
├── tailwind.config.ts     # (if using v3) or CSS @theme (if using v4)
├── tsconfig.json
└── package.json
```

### Step 3: Configure Tailwind CSS v4

**⚠️ Tailwind v3 vs v4 — Check which version is installed!**

**If Tailwind v4** (`tailwindcss` v4.x):
```css
/* src/app/globals.css */
@import "tailwindcss";

@theme {
  --color-primary-500: #3b82f6;
  /* ... custom theme variables */
}

body {
  background-color: var(--color-gray-50);
  color: var(--color-gray-900);
}
```

```typescript
// next.config.ts — NO tailwind plugin needed in v4
import type { NextConfig } from "next";

const nextConfig: NextConfig = {};

export default nextConfig;
```

**If Tailwind v3** (`tailwindcss` v3.x):
```javascript
// tailwind.config.ts
import type { Config } from "tailwindcss";

const config: Config = {
  content: [
    "./src/components/**/*.{ts,tsx}",
    "./src/app/**/*.{ts,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        primary: "#3b82f6",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
};

export default config;
```

```css
/* src/app/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Step 4: Configure shadcn/ui

After running `npx shadcn@latest init`, the CLI will:
1. Ask for **base color** (choose: `slate` / `gray` / `zinc` — `zinc` is most popular)
2. Create `src/components/ui/` folder with base components
3. Add CSS variables to `globals.css`

**Example `components.json`** (auto-generated):
```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "src/app/globals.css",
    "baseColor": "zinc",
    "cssVariables": true
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils"
  }
}
```

### Step 5: Create Dashboard Page (Example)

**src/app/page.tsx**:
```tsx
import { Button } from "@/components/ui/button"
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "@/components/ui/card"
import { Badge } from "@/components/ui/badge"

export default function DashboardPage() {
  return (
    <div className="flex min-h-screen w-full flex-col">
      <main className="flex flex-1 flex-col gap-4 p-4 md:gap-8 md:p-6">
        <div className="grid gap-4 md:grid-cols-2 md:gap-8 lg:grid-cols-4">
          <Card>
            <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
              <CardTitle className="text-sm font-medium">
                Total Revenue
              </CardTitle>
            </CardHeader>
            <CardContent>
              <div className="text-2xl font-bold">$45,231.89</div>
              <p className="text-xs text-muted-foreground">
                +20.1% from last month
              </p>
            </CardContent>
          </Card>
        </div>
      </main>
    </div>
  )
}
```

**src/app/layout.tsx**:
```tsx
import type { Metadata } from "next"
import { Inter } from "next/font/google"
import "./globals.css"

const inter = Inter({ subsets: ["latin"] })

export const metadata: Metadata = {
  title: "Dashboard",
  description: "Generated by Next.js + shadcn/ui",
}

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className={inter.className}>{children}</body>
    </html>
  )
}
```

### Step 6: Deliver

After generating the project:

1. **Provide the complete project structure** (all files)
2. **Tell user how to run it**:
   ```bash
   cd <project-name>
   npm install
   npm run dev        # http://localhost:3000
   ```
3. **Tell user how to add more shadcn components**:
   ```bash
   npx shadcn@latest add <component-name>
   # e.g., npx shadcn@latest add dialog table form
   ```
4. **Tell user how to build for production**:
   ```bash
   npm run build       # Output: .next/ folder
   npm start           # Start production server
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

### For 国内架构 (Ant Design + Vite):
- **NO CDN approach** - Ant Design requires build tools (Vite/webpack)
- **Use TypeScript** - Type safety, better DX, industry standard
- **Use Vite** - Best DX (HMR, fast builds, TypeScript support out of the box)
- **Ant Design 6.x** - Uses CSS-in-JS (no separate CSS import needed)
- **Build output** - `npm run build` generates `dist/` folder (can be deployed to any static server)
- **Hot Module Replacement (HMR)** - Vite provides instant updates during development

### For 国际架构 (Next.js + shadcn/ui):
- **Next.js 15 App Router** - File-system routing, React Server Components
- **Use Tailwind CSS v4** - Latest version with CSS-based configuration
- **shadcn/ui is NOT a npm package** - Components are copied into your project
- **Owns the code** - You can modify any shadcn/ui component freely
- **Use `npx shadcn@latest add <component>` to add more components**
- **Fonts** - Use `next/font/google` (built-in, no extra requests)
- **Build output** - `npm run build` generates `.next/` folder

---

## shadcn/ui Component Reference

### Most Used Components

| Component | Command | Usage |
|-----------|----------|-------|
| Button | `npx shadcn@latest add button` | `<Button variant="outline">` |
| Card | `npx shadcn@latest add card` | `<Card><CardHeader>...` |
| Input | `npx shadcn@latest add input` | `<Input placeholder="..." />` |
| Label | `npx shadcn@latest add label` | `<Label htmlFor="...">` |
| Select | `npx shadcn@latest add select` | `<Select><SelectTrigger>...` |
| Dialog | `npx shadcn@latest add dialog` | `<Dialog><DialogTrigger>...` |
| Dropdown Menu | `npx shadcn@latest add dropdown-menu` | `<DropdownMenu>...` |
| Table | `npx shadcn@latest add table` | `<Table><TableHeader>...` |
| Tabs | `npx shadcn@latest add tabs` | `<Tabs><TabsList>...` |
| Badge | `npx shadcn@latest add badge` | `<Badge variant="secondary">` |
| Avatar | `npx shadcn@latest add avatar` | `<Avatar><AvatarImage>...` |
| Form | `npx shadcn@latest add form` | Uses React Hook Form |

### Full component list: https://ui.shadcn.com/docs/components

---

## Tailwind CSS v4 vs v3 Key Differences

### Configuration

**v3 (Old)**:
```js
// tailwind.config.ts
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
/* src/app/globals.css */
@import "tailwindcss";

@theme {
  --color-primary-500: #3b82f6;
}
```

### Vite Config (for reference)

**v3**: Uses PostCSS (`postcss.config.js`)
**v4**: Uses Vite plugin (`@tailwindcss/vite`)

> **Note**: Next.js with Tailwind v4 auto-configures via PostCSS, no manual plugin setup needed.

---

## References

- `references/antd-components.md` - Ant Design component API reference
- `references/next-shadcn-guide.md` - Next.js 15 + shadcn/ui setup guide (国际架构)
- `references/tailwind-radix-guide.md` - Tailwind CSS v4 + Radix UI setup guide (legacy)

---

## Example: Complete Project Generation

### Example 1: 国内架构

When user says **"用 Ant Design 做一个登录页面"**:

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

### Example 2: 国际架构

When user says **"用国际架构做一个登录页面"** or **"用 Next.js + shadcn 做一个..."**:

1. Create Next.js project (App Router + TypeScript + Tailwind)
2. Initialize shadcn/ui (`npx shadcn@latest init`)
3. Add shadcn components: `button`, `input`, `label`, `card`
4. Generate `src/app/layout.tsx`, `src/app/page.tsx`, `src/app/globals.css`
5. Use `next/font/google` for fonts
6. Provide instructions to run:
   ```bash
   cd login-page
   npm install
   npm run dev        # http://localhost:3000
   ```
