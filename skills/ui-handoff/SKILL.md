---
name: ui-handoff
version: 1.0.0
display_name: UI 页面复刻与实现
display_name_en: UI Page Recreation & Implementation
description: 根据已有 UI、原型 URL 或 page-structure.md，在当前项目中复刻或实现页面。
description_zh: 根据已有 UI、产品原型 URL 或 page-structure.md，在当前项目中复刻或实现 UI 页面。
description_en: Recreate or implement UI pages in the current project from an existing UI, prototype URL, or page-structure.md.
disable-model-invocation: true
argument-hint: "<原型URL | page-structure.md>"
---

# UI Handoff

如果已有 `page-structure.md`：

1. 按 `references/CONSUME_PAGE_SPEC.md` 分析当前项目。
2. 生成 `ui-implementation-plan.md`。
3. 根据 `page-structure.md` 和 `ui-implementation-plan.md` 实现页面。

如果只有原型 URL：

1. 按 `references/SPEC.md` 和 `references/EXTRACT_FROM_URL.md` 生成 `page-structure.md`。
2. 按 `references/CONSUME_PAGE_SPEC.md` 分析当前项目。
3. 生成 `ui-implementation-plan.md`。
4. 根据 `page-structure.md` 和 `ui-implementation-plan.md` 实现页面。

代码库分析时，优先使用 `codebase-memory-mcp`；不可用时使用 Agent 自带代码搜索能力。

当前只实现 UI、Mock 数据和前端交互，不接后台 API。
