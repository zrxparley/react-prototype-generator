# TDesign React 使用说明（需构建工具）

TDesign React **不支持 CDN/UMD**，必须通过构建工具使用。

---

## 方式一：Vite 项目（推荐）

### 1. 创建项目

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
```

### 2. 安装 TDesign React

```bash
npm install tdesign-react
```

### 3. 引入样式和使用

```jsx
// main.jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Button, Input } from 'tdesign-react';
import 'tdesign-react/es/style/index.css';
import App from './App.jsx';

ReactDOM.createRoot(document.getElementById('app')).render(<App />);
```

```jsx
// App.jsx
import { Button, Layout, Menu } from 'tdesign-react';
const { Header, Content, Aside } = Layout;

function App() {
    return (
        <Layout>
            <Header>Header</Header>
            <Layout>
                <Aside>Aside</Aside>
                <Content>Content</Content>
            </Layout>
        </Layout>
    );
}

export default App;
```

### 4. 启动开发服务器

```bash
npm run dev
```

---

## 方式二：在线 IDE（无需本地环境）

### StackBlitz

访问 https://stackblitz.com/fork/github/tdesign-react/starter 快速创建在线项目。

### CodeSandbox

访问 https://codesandbox.io/s/tdesign-react-starter 快速创建在线项目。

---

## 方式三：我帮你生成代码，你复制到本地项目

如果你已经有 vite + React 项目，告诉我需要什么页面，我生成组件代码，你直接复制到项目中即可。

---

## TDesign React 常用组件

| 组件 | 引入方式 | 说明 |
|------|-----------|------|
| Button | `import { Button } from 'tdesign-react'` | 按钮 |
| Input | `import { Input } from 'tdesign-react'` | 输入框 |
| Form | `import { Form, FormItem } from 'tdesign-react'` | 表单 |
| Table | `import { Table } from 'tdesign-react'` | 表格 |
| Layout | `import { Layout } from 'tdesign-react'` | 布局 |
| Menu | `import { Menu } from 'tdesign-react'` | 菜单 |
| Dialog | `import { DialogPlugin } from 'tdesign-react'` | 对话框 |
| Message | `import { MessagePlugin } from 'tdesign-react'` | 消息提示 |

**注意**：使用 TDesign React 时，需要同时引入样式：
```jsx
import 'tdesign-react/es/style/index.css';
```

---

## 与 Ant Design React 对比

| 功能 | Ant Design (antd) | TDesign React |
|------|---------------------|----------------|
| CDN 支持 | ✅ 支持（UMD） | ❌ 不支持 |
| 全局对象 | `antd` | 无（需构建工具） |
| 消息提示 | `antd.message.success()` | `MessagePlugin.success()` |
| 对话框 | `antd.Modal.confirm()` | `DialogPlugin.confirm()` |
| 按钮主题 | `type="primary"` | `theme="primary"` |
| 表单 | `Form` + `Form.Item` | `Form` + `FormItem` |

---

## 推荐方案

- **快速原型 / 演示**：使用 **Ant Design React（CDN 方式）**，无需安装，直接生成 HTML 文件。
- **正式项目 / 生产环境**：使用 **TDesign React（Vite 构建）**，按需加载，支持 Tree-shaking。
