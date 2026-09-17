# Minimum UI Handoff Spec 1.0

## Purpose

本协议用于将 AI 生成的可运行 UI 原型转换为前端 Agent 可读取的页面结构描述。

目标：

- 帮助前端 Agent 在不重新分析整个原型页面的情况下还原 UI。
- 描述页面结构、关键视觉属性和 UI 交互。
- 保持协议足够简单，避免重复描述前端实现细节。

本协议只描述 UI。

不描述：

- 后台 API
- 网络请求
- Vue 实现方式
- 状态管理实现
- 测试实现
- 原型中不存在的功能

---

# 1. Page

每个页面必须包含基本信息。

```yaml
page:
  id: warehouse-list
  name: 仓库管理
  type: list
```

`type` 不要求严格枚举，只需要帮助 Agent 理解页面的大致性质，例如：

- list
- form
- detail
- dashboard
- mixed

---

# 2. UI

使用树形结构描述页面。

组件的重要属性直接写在组件自身，不单独建立 Properties。

示例：

```yaml
ui:
  - type: SearchArea
    layout:
      columns: 4
      gap: 16

    children:
      - type: Input
        field: warehouseName
        label: 仓库名称
        placeholder: 请输入仓库名称

      - type: Select
        field: status
        label: 状态
        options:
          - 启用
          - 停用

      - type: Button
        text: 查询
        appearance: primary
        action: filterTable

      - type: Button
        text: 重置
        action: resetFilter

  - type: Toolbar

    children:
      - type: Button
        text: 新增

        onClick:
          open: warehouseEditor
          mode: create

  - type: Table
    id: warehouseTable

    columns:
      - title: 仓库编码
        field: warehouseCode
        width: 160

      - title: 仓库名称
        field: warehouseName

      - title: 状态
        field: status

      - title: 操作
        width: 160

        actions:
          - text: 编辑

            onClick:
              open: warehouseEditor
              mode: edit
              data: currentRow

  - type: Drawer
    id: warehouseEditor
    width: 640
    default: closed

    modes:
      create:
        title: 新增仓库
        data: empty

      edit:
        title: 编辑仓库
        data: currentRow

    children:
      - type: Input
        field: warehouseCode
        label: 仓库编码

      - type: Input
        field: warehouseName
        label: 仓库名称

      - type: Button
        text: 取消

        onClick:
          close: warehouseEditor

      - type: Button
        text: 确定
        appearance: primary

        onClick:
          close: warehouseEditor
```

如果同一个数据概念同时出现在多个 UI 区域，应使用相同且稳定的 `field`。

例如「揽收时间」同时出现在查询区、表格和修改时间弹窗时，三处都使用：

```yaml
field: pickupTime
```

不要使用“同上”“对应 D12-D24”“与上述字段一致”等模糊引用代替 `field`。

---

# 3. Interactions

简单交互应直接写在对应组件上，例如：

```yaml
onClick:
  open: warehouseEditor
```

或者：

```yaml
onClick:
  close: warehouseEditor
```

只有当一个交互同时影响多个组件、无法在单个组件内部清楚表达时，才增加独立的 `interactions`。

例如：

```yaml
interactions:
  - when:
      field: warehouseType
      equals: thirdParty

    show:
      - supplierField

    hide:
      - internalWarehouseConfig
```

不要为简单交互建立状态机、Transition 或 Flow。

---

# 4. IDs

不是所有组件都必须拥有 `id`。

只有以下情况建议提供：

- 会被其他组件引用
- 会被打开或关闭
- 会被显示或隐藏
- 存在多个展示模式
- 需要参与跨组件交互

例如：

```yaml
id: warehouseEditor
```

普通 Input、Button 如果没有被其他地方引用，可以不设置 ID。

---

# 5. Mock Data

默认不要求单独提供 Mock Data 文件。

少量展示数据可以直接包含在页面协议中。

只有以下情况才考虑额外生成 `mock-data.json`：

- 表格数据较多
- Tree 数据较复杂
- 多个组件共享相同数据
- 大量 Select Options
- 数据本身会明显影响 UI 展示

---

# 6. Assets

默认不要求生成 assets 目录。

只有原型包含无法通过现有 UI 组件还原的图片、插画、SVG 或其他资源时，才单独输出对应资源。

---

# 7. Generation Rules

生成页面协议时：

1. 以当前最终原型为依据。
2. 不增加原型中不存在的功能。
3. 不描述后台 API。
4. 不描述 Vue 具体实现方式。
5. 保留主要页面层级。
6. 保留影响视觉还原的重要属性。
7. 保留用户能够观察到的 UI 交互。
8. 简单交互就近写在组件上。
9. 不为了追求完整而增加不必要字段。
10. 无法确定的信息不要猜测。
11. 排除只用于原型制作、PRD 评审、设计标注或开发辅助的内容，例如 `prdAnchor`、PRD 对照入口、评审说明等。

---

# 8. Core Principle

协议只记录：

> 如果不告诉前端 Agent，它就可能明显还原错误的信息。

不要试图完整描述整个前端程序。
