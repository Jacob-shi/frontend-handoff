# Frontend Handoff

`frontend-handoff` 是一组用于 AI 原型交接、UI 页面复刻和旧功能迁移的 Agent Skills。

包含 3 个 Skill：

- `prototype-handoff`：原型完成后生成 `page-structure.md`
- `ui-handoff`：根据已有 UI、原型 URL 或 `page-structure.md` 实现页面
- `feature-migration`：将旧系统中的完整功能迁移到当前项目

## 安装

将需要的 Skill 复制到当前项目：

```text
<project>/.agents/skills/
```

可以安装全部，也可以只安装其中一个。

例如：

```text
.agents/
└── skills/
    ├── prototype-handoff/
    ├── ui-handoff/
    └── feature-migration/
```

## prototype-handoff

适用于产品经理已经使用 AI 完成原型，并且当前 AI 仍然保留完整原型上下文的场景。

原型确认后执行：

```text
/prototype-handoff

当前原型已经确认完成，请根据最终版本生成 page-structure.md。
```

如果有多个页面：

```text
/prototype-handoff

请为当前已经确认的「入库订单列表」页面生成 page-structure.md。
```

输出：

```text
page-structure.md
```

然后将该文件交给前端。

## ui-handoff

适用于根据已有 UI 在当前项目中复刻或实现页面。

既可以用于产品经理的 AI 原型项目，也可以用于正式前端项目。

### 已有 page-structure.md

```text
/ui-handoff

根据这个 page-structure.md，在当前项目中实现页面。
```

也可以直接指定文件：

```text
/ui-handoff docs/ui-handoff/inbound-order/page-structure.md
```

### 只有原型 URL

```text
/ui-handoff https://prototype.example.com/inbound-order
```

Skill 会先提取页面结构，再结合当前项目完成页面实现。

### 产品经理复刻已有原型

如果正在使用 AI 搭建 HTML 原型，也可以直接参考已有页面：

```text
/ui-handoff

参考下面这个已有页面，在当前原型项目中实现新的「出库订单列表」页面：

https://prototype.example.com/order-list
```

默认只实现 UI、Mock 数据和前端交互，不接后台 API。

## feature-migration

适用于旧系统中已经存在完整运行功能，需要迁移到当前项目的场景。

提供旧功能 URL：

```text
/feature-migration https://old.example.com/order/list
```

Skill 会分析页面 UI、交互和实际网络请求，并生成：

```text
feature-implementation-plan.md
```

默认先生成迁移方案。

确认后：

```text
按照 feature-implementation-plan.md 开始实现。
```

如果希望直接迁移：

```text
/feature-migration

把下面这个旧系统功能迁移到当前项目：

https://old.example.com/order/list

分析完成后直接开始实现。
```

## 怎么选择

```text
产品原型已经完成，需要交给前端
→ prototype-handoff

已有 UI / 原型 URL / page-structure.md，需要复刻或实现页面
→ ui-handoff

旧系统已经有完整功能，需要迁移
→ feature-migration
```

正常使用时直接调用对应 Skill 即可，不需要手工阅读 Skill 内部规则。