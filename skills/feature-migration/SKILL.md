---
name: feature-migration
version: 1.0.0
display_name: 旧版前端页面与功能迁移
display_name_en: Legacy Frontend Page & Feature Migration
description: 将旧系统中已经完整运行的功能迁移到当前前端项目。
description_zh: 分析旧系统中已经完整运行的页面、交互和实际网络请求，并将功能迁移到当前前端项目。
description_en: Analyze an existing production feature, including its UI, interactions, and network requests, and migrate it into the current frontend project.
disable-model-invocation: true
argument-hint: "<原功能URL>"
---

---

# Feature Migration

分析用户提供的已运行功能 URL，并为当前项目生成迁移方案。

## 流程

1. 打开原功能 URL，分析页面 UI、交互和实际网络请求。
2. 无法从页面或 Network 确认的信息不要猜测。
3. 优先使用 `codebase-memory-mcp` 分析当前项目，寻找可复用实现。
4. 结合原功能和当前项目，生成 `feature-implementation-plan.md`。
5. 默认只生成迁移方案，不修改代码；用户明确要求实现后再开始编码。

## 原则

- 原功能的实际 UI、交互和请求行为是迁移依据。
- 当前 Codebase 只用于决定如何在新项目中实现。
- 优先复用已有实现，没有合适实现时再新建。
