# Extract UI Spec From Prototype URL

根据提供的已运行 UI 原型地址，分析页面并生成符合 `SPEC.md` 的 `page-structure.md`。

本任务用于：

- 原型已经生成完成；
- 原来的 AI 生成上下文已经不存在；
- 当前只有可以访问的原型 URL。

## 核心目标

尽可能通过页面本身的结构、内容和交互获取信息，而不是仅依赖截图猜测页面。

最终输出必须符合 `SPEC.md`。

---

## 分析顺序

### 1. 打开原型

访问用户提供的 Prototype URL。

等待页面正常完成渲染。

---

### 2. 分析默认页面

首先读取当前默认页面中可访问的内容和 UI 元素。

识别主要页面区域，例如：

- Header
- Sidebar
- Breadcrumb
- SearchArea
- Toolbar
- Form
- Table
- Card
- Tabs
- Pagination
- Drawer
- Dialog
- Tree
- Collapse
- Steps

记录页面的父子层级关系。

---

### 3. 优先读取结构信息

优先根据页面实际元素识别：

- 文字
- Label
- Placeholder
- Button
- Input
- Select
- Checkbox
- Radio
- Switch
- Table
- Table Columns
- Tabs
- Links
- Form Controls

不要仅根据截图推断可以直接从页面获取的信息。

---

### 4. 分析重要视觉属性

记录会明显影响 UI 还原的视觉信息，例如：

- 页面主要区域排列方式
- 一行字段数量
- Drawer / Dialog 大小
- Table 列宽
- 固定列
- Tabs 排列
- 主要元素间距
- 特殊宽度
- 特殊高度
- 特殊颜色语义

不要尝试复制完整 CSS。

只记录：

如果缺少该信息，会导致前端 Agent 明显还原错误的属性。

---

### 5. 探索 UI 交互

主动检查当前页面中明显存在的 UI 交互入口，例如：

- 新增
- 编辑
- 查看
- 展开
- 收起
- 更多
- Tabs
- Dropdown
- Drawer
- Dialog
- Collapse
- Switch
- Radio
- Checkbox
- 条件字段
- 高级搜索

操作这些元素，观察 UI 如何变化。

只探索 UI 行为。

不要执行具有不可逆副作用的真实业务操作。

---

### 6. 检查隐藏 UI

重点确认默认页面中不可见、但用户操作后会出现的内容，例如：

- Drawer
- Dialog
- Dropdown Menu
- Popover
- Tooltip
- Advanced Search
- Tab Content
- Collapse Content
- Edit Mode
- Create Mode
- Conditional Fields

将这些内容加入 UI Tree 或对应组件的交互描述。

---

### 7. 控制探索范围

不要穷举所有可能的操作组合。

优先探索：

1. 会显示新 UI 区域的操作；
2. 会改变组件结构的操作；
3. 会改变组件可见性的操作；
4. 明显属于页面主要功能的操作。

例如普通查询按钮如果只是改变表格数据，而不会改变 UI 结构，则不需要反复执行不同查询条件。

---

### 8. 使用截图作为补充

当页面结构信息不足以判断以下内容时，可以使用截图辅助分析：

- 整体布局
- 空间关系
- 视觉层级
- 间距
- 对齐
- 特殊样式
- 无法从页面结构准确识别的区域

截图用于补充结构分析。

不要默认仅依靠截图生成整个 Spec。

---

## 输出

最终生成：

`page-structure.md`

必须符合 `SPEC.md`。

不要：

- 描述后台 API；
- 描述 Vue 或 React 实现；
- 猜测无法从当前原型确认的交互；
- 增加原型不存在的功能；
- 为简单 UI 创建复杂状态机；
- 输出页面源码。

如果某个隐藏状态无法安全确认，则省略该细节，不要猜测。

最终只输出 `page-structure.md` 内容。
