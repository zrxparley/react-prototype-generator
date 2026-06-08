# Ant Design React 组件参考 (antd@4.x)

> ⚠️ **重要说明：** 本文档适用于 **Ant Design 4.x**（支持 CDN/UMD）。  
> Ant Design 5.x **不支持 CDN**，已移除 UMD 构建。

通过 CDN 引入后，所有组件通过 `antd` 全局对象访问。

---

## CDN 引入方式 (antd@4)

```html
<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<!-- ✅ Ant Design 4.x 支持 UMD/CDN -->
<script crossorigin src="https://unpkg.com/antd@4/dist/antd.min.js"></script>
<link rel="stylesheet" href="https://unpkg.com/antd@4/dist/antd.min.css">
```

---

## 布局组件 (Layout)

### Layout / Header / Content / Sider / Footer

```javascript
const { Layout, Menu } = antd;
const { Header, Content, Sider, Footer } = Layout;

<Layout>
    <Sider>Sider</Sider>
    <Layout>
        <Header>Header</Header>
        <Content>Content</Content>
        <Footer>Footer</Footer>
    </Layout>
</Layout>
```

### Menu

```javascript
<Menu mode="inline" defaultSelectedKeys={['1']} theme="dark">
    <Menu.Item key="1" icon={<span>🏠</span>}>首页</Menu.Item>
    <Menu.Item key="2">关于</Menu.Item>
</Menu>
```

---

## 表单组件 (Form)

### Button

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| type | 'primary' \| 'default' \| 'dashed' \| 'text' \| 'link' | 'default' | 按钮类型 |
| danger | boolean | false | 危险按钮 |
| disabled | boolean | false | 禁用 |
| loading | boolean \| { delay: number } | false | 加载中 |
| onClick | function | - | 点击回调 |
| icon | ReactNode | - | 图标 |
| shape | 'circle' \| 'round' | - | 形状 |
| size | 'large' \| 'middle' \| 'small' | 'middle' | 尺寸 |

```javascript
const { Button } = antd;

<Button type="primary" onClick={() => console.log('clicked')}>
    Primary Button
</Button>

<Button type="primary" danger>Delete</Button>

<Button type="primary" loading>Loading</Button>
```

### Input

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string | - | 输入框值 |
| placeholder | string | - | 占位符 |
| disabled | boolean | false | 禁用 |
| size | 'large' \| 'middle' \| 'small' | 'middle' | 尺寸 |
| onChange | function(e) | - | 值变化回调 |
| onPressEnter | function(e) | - | 回车回调 |
| prefix | ReactNode | - | 前缀图标 |
| suffix | ReactNode | - | 后缀图标 |
| allowClear | boolean | false | 可清空 |

```javascript
const { Input } = antd;

<Input placeholder="请输入内容" onChange={(e) => console.log(e.target.value)} />

<Input prefix={<span>🔍</span>} placeholder="带图标" />
```

### Form / Form.Item

```javascript
const { Form, Input, Button } = antd;

<Form onFinish={(values) => console.log(values)}>
    <Form.Item label="用户名" name="username" rules={[{ required: true }]}>
        <Input />
    </Form.Item>
    <Form.Item label="密码" name="password" rules={[{ required: true }]}>
        <Input.Password />
    </Form.Item>
    <Form.Item>
        <Button type="primary" htmlType="submit">登录</Button>
    </Form.Item>
</Form>
```

### Select

```javascript
const { Select } = antd;

const options = [
    { value: '1', label: '选项一' },
    { value: '2', label: '选项二' },
    { value: '3', label: '选项三' },
];

<Select options={options} placeholder="请选择" style={{ width: 300 }} />
<Select mode="multiple" options={options} placeholder="多选" />
```

### DatePicker

```javascript
const { DatePicker } = antd;

<DatePicker placeholder="选择日期" />
<DatePicker.RangePicker />
```

---

## 数据展示 (Data Display)

### Table

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| data | array | - | 表格数据（AntD 用 `dataSource`） |
| columns | array | - | 列配置 |
| rowKey | string \| function | 'key' | 行键 |
| bordered | boolean | false | 显示边框 |
| loading | boolean | false | 加载中 |
| pagination | object \| false | - | 分页配置 |
| size | 'large' \| 'middle' \| 'small' | 'middle' | 尺寸 |

```javascript
const { Table } = antd;

const columns = [
    { title: '姓名', dataIndex: 'name', key: 'name' },
    { title: '年龄', dataIndex: 'age', key: 'age' },
    { title: '地址', dataIndex: 'address', key: 'address' },
];

const data = [
    { key: '1', name: '张三', age: 25, address: '北京' },
    { key: '2', name: '李四', age: 30, address: '上海' },
];

<Table dataSource={data} columns={columns} rowKey="key" />
```

### Card

```javascript
const { Card, Button } = antd;

<Card 
    title="卡片标题" 
    extra={<a href="#">更多</a>}
    actions={[
        <Button type="link">操作一</Button>,
        <Button type="link">操作二</Button>
    ]}
>
    卡片内容
</Card>
```

### Tag

```javascript
const { Tag } = antd;

<Tag color="blue">标签</Tag>
<Tag color="green">成功</Tag>
<Tag color="orange">警告</Tag>
<Tag color="red">错误</Tag>
```

### Badge

```javascript
const { Badge, Button } = antd;

<Badge count={5}>
    <Button>消息</Button>
</Badge>

<Badge status="success" text="成功" />
```

### Statistic（统计数值）

```javascript
const { Statistic } = antd;

<Statistic title="活跃用户" value={112893} />
<Statistic title="增长率" value={11.28} precision={2} suffix="%" />
```

---

## 导航组件 (Navigation)

### Menu

（见上方布局组件部分）

### Tabs

```javascript
const { Tabs } = antd;

<Tabs defaultActiveKey="1">
    <Tabs.TabPane tab="标签一" key="1">内容一</Tabs.TabPane>
    <Tabs.TabPane tab="标签二" key="2">内容二</Tabs.TabPane>
</Tabs>
```

### Breadcrumb

```javascript
const { Breadcrumb } = antd;

<Breadcrumb>
    <Breadcrumb.Item>首页</Breadcrumb.Item>
    <Breadcrumb.Item>用户管理</Breadcrumb.Item>
    <Breadcrumb.Item>用户列表</Breadcrumb.Item>
</Breadcrumb>
```

### Pagination

```javascript
const { Pagination } = antd;

<Pagination defaultCurrent={1} total={50} />
```

---

## 反馈组件 (Feedback)

### Modal（对话框）

```javascript
const { Modal, Button } = antd;

const showModal = () => {
    Modal.confirm({
        title: '确认',
        content: '确定要执行此操作吗？',
        onOk: () => console.log('confirmed'),
        onCancel: () => console.log('cancelled'),
    });
};

<Button type="primary" onClick={showModal}>显示对话框</Button>
```

### message（全局提示）

```javascript
const { message, Button } = antd;

// 注意：AntD 用 antd.message，不是 MessagePlugin
message.success('操作成功');
message.error('操作失败');
message.warning('警告');
message.info('提示');

<Button onClick={() => message.success('成功！')}>显示消息</Button>
```

### notification（通知提醒）

```javascript
const { notification } = antd;

notification.open({
    message: '通知标题',
    description: '这是一条通知消息',
    onClick: () => console.log('clicked'),
});
```

### Spin / Loading

```javascript
const { Spin, Alert } = antd;

<Spin spinning={true} tip="加载中...">
    <Alert message="加载完成后的内容" />
</Spin>
```

---

## 通用组件

### Alert（警告提示）

```javascript
const { Alert } = antd;

<Alert message="成功提示" type="success" showIcon />
<Alert message="消息提示" type="info" showIcon />
<Alert message="警告提示" type="warning" showIcon />
<Alert message="错误提示" type="error" showIcon />
<Alert message="可关闭的警告" type="info" closable />
```

### Space（间距）

```javascript
const { Space, Button } = antd;

<Space>
    <Button>按钮一</Button>
    <Button>按钮二</Button>
    <Button>按钮三</Button>
</Space>

<Space direction="vertical">
    <Button>按钮一</Button>
    <Button>按钮二</Button>
</Space>
```

### Typography（排版）

```javascript
const { Typography } = antd;
const { Title, Text, Paragraph } = Typography;

<Title level={1}>一级标题</Title>
<Title level={2}>二级标题</Title>
<Text strong>加粗文本</Text>
<Text type="secondary">次要文本</Text>
<Paragraph>段落文本内容...</Paragraph>
```

---

## Ant Design vs TDesign 对照表

| 功能 | Ant Design (antd) | TDesign React |
|------|---------------------|----------------|
| 消息提示 | `antd.message.success()` | `MessagePlugin.success()` |
| 对话框 | `antd.Modal.confirm()` | `DialogPlugin.confirm()` |
| 布局子组件 | `antd.Layout.Header` | `Header` (直接解构) |
| 按钮主题 | `type="primary"` | `theme="primary"` |
| 输入框 | `Input` | `Input` |
| 表格数据 | `dataSource` | `data` |
| 加载中 | `Spin` | `Loading` |
| 全局对象 | `antd` | `TDesignReact` |

---

## 常用组合示例

### 登录页面

```javascript
const { Form, Input, Button, Card, message, Typography } = antd;
const { Title } = Typography;

function LoginPage() {
    const onFinish = (values) => {
        message.success('登录成功！');
    };
    
    return (
        <div style={{ maxWidth: 400, margin: '100px auto', padding: 24 }}>
            <Card>
                <Title level={3} style={{ textAlign: 'center' }}>用户登录</Title>
                <Form onFinish={onFinish}>
                    <Form.Item label="用户名" name="username" rules={[{ required: true, message: '请输入用户名' }]}>
                        <Input placeholder="请输入用户名" />
                    </Form.Item>
                    <Form.Item label="密码" name="password" rules={[{ required: true, message: '请输入密码' }]}>
                        <Input.Password placeholder="请输入密码" />
                    </Form.Item>
                    <Form.Item>
                        <Button type="primary" htmlType="submit" block>登录</Button>
                    </Form.Item>
                </Form>
            </Card>
        </div>
    );
}
```

### 后台管理布局

```javascript
const { Layout, Menu, Typography } = antd;
const { Header, Content, Sider } = Layout;
const { Title } = Typography;

function Dashboard() {
    return (
        <Layout style={{ minHeight: '100vh' }}>
            <Sider width={232} theme="dark">
                <div style={{ height: 64, color: '#fff', display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: 18, fontWeight: 'bold' }}>
                    后台管理系统
                </div>
                <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                    <Menu.Item key="1">仪表盘</Menu.Item>
                    <Menu.Item key="2">用户管理</Menu.Item>
                    <Menu.Item key="3">设置</Menu.Item>
                </Menu>
            </Sider>
            <Layout>
                <Header style={{ background: '#fff', padding: '0 24px' }}>
                    <Title level={4} style={{ margin: 0 }}>后台管理系统</Title>
                </Header>
                <Content style={{ margin: 24, padding: 24, background: '#fff' }}>
                    内容区域
                </Content>
            </Layout>
        </Layout>
    );
}
```
