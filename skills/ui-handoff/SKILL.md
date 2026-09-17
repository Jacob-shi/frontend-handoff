---
name: ui-handoff
description: 根据产品原型 URL 或已有 page-structure.md，在当前前端项目中完成 UI 页面还原。
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
