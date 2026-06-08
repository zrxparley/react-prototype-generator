# ⚠️ 重要说明

TDesign React **不支持 CDN/UMD 引入**，必须通过构建工具（vite/webpack）使用。

- 如需 CDN 方式快速生成原型，请使用 **Ant Design React**（本 Skill 已支持，参见 `references/antd-components.md`）
- 如需使用 TDesign React，请参考 `references/design-react-setup.md` 的 vite 配置方案

---

# TDesign React 组件参考

本文档提供 TDesign React 常用组件的 API 参考，用于 vite/webpack 项目开发。

## CDN 引入方式

```html
<!-- TDesign CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/tdesign-react/es/style/index.css">

<!-- React 18 -->
<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

<!-- Babel Standalone (JSX 转换) -->
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

<!-- TDesign React UMD -->
<script src="https://cdn.jsdelivr.net/npm/tdesign-react/umd/tdesign-react.umd.js"></script>
```

通过 CDN 引入后，所有组件可通过 `TDesignReact` 全局对象访问。

---

## 布局组件 (Layout)

### Layout, Header, Content, Aside, Footer

页面整体布局结构。

```javascript
const { Layout, Header, Content, Aside, Footer } = TDesignReact;

<Layout>
    <Header>Header</Header>
    <Layout>
        <Aside>Aside</Aside>
        <Content>Content</Content>
    </Layout>
    <Footer>Footer</Footer>
</Layout>
```

### Grid / Row / Col

栅格系统。

```javascript
const { Row, Col } = TDesignReact;

<Row>
    <Col span={6}>Col-6</Col>
    <Col span={6}>Col-6</Col>
    <Col span={6}>Col-6</Col>
    <Col span={6}>Col-6</Col>
</Row>
```

---

## 表单组件 (Form)

### Button

按钮组件。

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| theme | 'default' \| 'primary' \| 'success' \| 'warning' \| 'danger' | 'default' | 按钮主题 |
| variant | 'base' \| 'outline' \| 'dashed' \| 'text' \| 'ghost' | 'base' | 按钮变体 |
| size | 'small' \| 'medium' \| 'large' | 'medium' | 尺寸 |
| disabled | boolean | false | 禁用状态 |
| loading | boolean | false | 加载状态 |
| onClick | function | - | 点击回调 |

```javascript
const { Button } = TDesignReact;

<Button theme="primary" onClick={() => console.log('clicked')}>
    Primary Button
</Button>
```

### Input

输入框组件。

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string | - | 输入框值 |
| placeholder | string | - | 占位符 |
| disabled | boolean | false | 禁用 |
| size | 'small' \| 'medium' \| 'large' | 'medium' | 尺寸 |
| onChange | function | - | 值变化回调 |
| onEnter | function | - | 回车回调 |

```javascript
const { Input } = TDesignReact;

<Input placeholder="请输入内容" onChange={(val) => console.log(val)} />
```

### Form / FormItem

表单容器和表单项。

```javascript
const { Form, FormItem } = TDesignReact;

<Form>
    <FormItem label="用户名">
        <Input placeholder="请输入用户名" />
    </FormItem>
    <FormItem label="密码">
        <Input type="password" placeholder="请输入密码" />
    </FormItem>
</Form>
```

### Select

下拉选择器。

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string / number / array | - | 选中值 |
| options | array | - | 选项数据 |
| placeholder | string | - | 占位符 |
| multiple | boolean | false | 多选 |
| onChange | function | - | 变化回调 |

```javascript
const { Select } = TDesignReact;

const options = [
    { label: '选项一', value: '1' },
    { label: '选项二', value: '2' },
    { label: '选项三', value: '3' },
];

<Select options={options} placeholder="请选择" />
```

---

## 数据展示 (Data Display)

### Table

数据表格。

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| data | array | [] | 表格数据 |
| columns | array | [] | 列配置 |
| rowKey | string | 'id' | 行键 |
| bordered | boolean | false | 显示边框 |
| stripe | boolean | false | 斑马纹 |

```javascript
const { Table } = TDesignReact;

const columns = [
    { colKey: 'name', title: '姓名' },
    { colKey: 'age', title: '年龄' },
    { colKey: 'address', title: '地址' },
];

const data = [
    { id: '1', name: '张三', age: 25, address: '北京' },
    { id: '2', name: '李四', age: 30, address: '上海' },
];

<Table data={data} columns={columns} rowKey="id" />
```

### Card

卡片容器。

```javascript
const { Card } = TDesignReact;

<Card title="卡片标题" actions={<Button>操作</Button>}>
    卡片内容
</Card>
```

### Tag

标签组件。

```javascript
const { Tag } = TDesignReact;

<Tag theme="primary">标签</Tag>
<Tag theme="success">成功</Tag>
<Tag theme="warning">警告</Tag>
<Tag theme="danger">危险</Tag>
```

---

## 导航组件 (Navigation)

### Menu

导航菜单。

```javascript
const { Menu } = TDesignReact;

const menuItems = [
    { path: '/dashboard', label: '仪表盘' },
    { path: '/users', label: '用户管理' },
    { path: '/settings', label: '设置' },
];

<Menu value="/dashboard">
    {menuItems.map(item => (
        <Menu.Item key={item.path} value={item.path}>
            {item.label}
        </Menu.Item>
    ))}
</Menu>
```

### Tabs

标签页切换。

```javascript
const { Tabs } = TDesignReact;

<Tabs defaultValue="tab1">
    <Tabs.TabPanel value="tab1" label="标签一">
        内容一
    </Tabs.TabPanel>
    <Tabs.TabPanel value="tab2" label="标签二">
        内容二
    </Tabs.TabPanel>
</Tabs>
```

### Breadcrumb

面包屑导航。

```javascript
const { Breadcrumb } = TDesignReact;

<Breadcrumb>
    <Breadcrumb.Item>首页</Breadcrumb.Item>
    <Breadcrumb.Item>用户管理</Breadcrumb.Item>
    <Breadcrumb.Item>用户列表</Breadcrumb.Item>
</Breadcrumb>
```

---

## 反馈组件 (Feedback)

### Dialog

对话框/模态框。

```javascript
const { DialogPlugin, Button } = TDesignReact;
const [visible, setVisible] = React.useState(false);

const showDialog = () => {
    DialogPlugin.confirm({
        header: '确认',
        body: '确定要执行此操作吗？',
        onConfirm: () => console.log('confirmed'),
        onCancel: () => console.log('cancelled'),
    });
};

<Button onClick={showDialog}>显示对话框</Button>
```

### MessagePlugin

消息提示。

```javascript
const { MessagePlugin, Button } = TDesignReact;

const showMessage = () => {
    MessagePlugin.success('操作成功');
    // 也支持: warning, error, info, question
};

<Button onClick={showMessage}>显示消息</Button>
```

### Loading

加载指示器。

```javascript
const { Loading } = TDesignReact;

<Loading loading={true} text="加载中...">
    <div>内容区域</div>
</Loading>
```

---

## 常用组合示例

### 登录页面

```javascript
function LoginPage() {
    const [formData, setFormData] = React.useState({ username: '', password: '' });
    
    const handleLogin = () => {
        MessagePlugin.success('登录成功');
    };
    
    return (
        <div style={{ maxWidth: 400, margin: '100px auto', padding: 24 }}>
            <Card title="用户登录">
                <Form>
                    <FormItem label="用户名">
                        <Input 
                            value={formData.username} 
                            onChange={(val) => setFormData({...formData, username: val})}
                            placeholder="请输入用户名"
                        />
                    </FormItem>
                    <FormItem label="密码">
                        <Input 
                            type="password"
                            value={formData.password} 
                            onChange={(val) => setFormData({...formData, password: val})}
                            placeholder="请输入密码"
                        />
                    </FormItem>
                    <Button theme="primary" block onClick={handleLogin}>
                        登录
                    </Button>
                </Form>
            </Card>
        </div>
    );
}
```

### 后台管理布局

```javascript
function DashboardLayout() {
    const [activeMenu, setActiveMenu] = React.useState('/dashboard');
    
    return (
        <Layout style={{ height: '100vh' }}>
            <Aside style={{ width: 232, background: '#fff' }}>
                <Menu 
                    value={activeMenu} 
                    onChange={(val) => setActiveMenu(val)}
                >
                    <Menu.Item value="/dashboard">仪表盘</Menu.Item>
                    <Menu.Item value="/users">用户管理</Menu.Item>
                    <Menu.Item value="/settings">设置</Menu.Item>
                </Menu>
            </Aside>
            <Layout>
                <Header style={{ background: '#fff', padding: '0 24px' }}>
                    <h3>后台管理系统</h3>
                </Header>
                <Content style={{ padding: 24, background: '#f0f2f5' }}>
                    内容区域
                </Content>
            </Layout>
        </Layout>
    );
}
```
