---
name: cloudcreate-freetools
description: >-
  Develops and maintains the CloudCreate.ai (cloudcreate.ai) freetools web app:
  SvelteKit 2 + Svelte 5, browser-first image/PDF/table/CSS/archive/workflow
  tools, i18n (en/zh), agent prompt panels, and static deploy to Cloudflare
  Pages. Use when working in this repository, adding or changing tool routes,
  workspace UI, SEO/sitemap, or when the user mentions CloudCreate, freetools,
  or cloudcreate.ai.
---

# CloudCreate.ai · freetools 仓库

面向 **人与 AI 协作的浏览器端工具集**（图片、PDF、表格、CSS、压缩包、工作流等），代码仓通常名为 `freetools`，线上 <https://cloudcreate.ai>。

## 技术栈

| 层级 | 选型 |
|------|------|
| 框架 | SvelteKit 2、Svelte 5（`$effect` / runes）、Vite |
| 输出 | `@sveltejs/adapter-static` 静态预渲染 |
| 样式 | Tailwind 4、Skeleton、全站 CSS 变量 `--ccw-*`（见 `src/app.css`） |
| 部署 | `npm run deploy` → Wrangler → Cloudflare Pages（见 `package.json`） |

## 关键路径速查

- **路由（按语言）**：`src/routes/[[locale]]/…`，`locale` 为 `en` / `zh`。
- **侧栏与首页工具列表**：`src/lib/toolList.js` 中的 `TOOL_GROUPS`。
- **工具页与 AI 说明元数据（顺序 = 全站说明页）**：`src/lib/toolPageSpec/registry.js` 的 `TOOL_PAGE_SPECS`；`id` 须与 `registerAgentPrompt({ templateKey: 'agentPrompt.' + id })` 一致。
- **预渲染与站点地图的 pathname 单源**：`src/lib/site-paths.js` 的 `PATHS_AFTER_LOCALE`；新增公开页必须更新此处（并确认 `svelte.config.js` prerender entries 与 `scripts/generate-sitemap.mjs` 的用法与之一致）。
- **文案（中英）**：`src/lib/i18n.js` 大对象；工具说明长文可在 `src/lib/i18n/agentPromptToolSpecData.js` 等；`agentPrompt.toolSpecDetail.<specId>.*` 与 registry 的 `id` 对应。
- **布局与壳**：`WorkspacePageShell`、`AppHeader`、`AppSidebar`；工具页公共头：`ToolPageHeader`。
- **AI 侧栏提示词注册**：各工具 `+page.svelte` 中 `registerAgentPrompt`（`$lib/stores/agentPromptStore.js`）。

## 新工具 / 新页面（检查清单）

1. 在 `src/routes/[[locale]]/<路径>/+page.svelte`（及需要的 `+page.js` 等）实现页面。
2. **注册展示与说明**：在 `TOOL_PAGE_SPECS` 增加 `{ id, path, titleKey? }`；`id` 与 `registerAgentPrompt` 的 `agentPrompt.<id>` 一致。
3. **导航**：在 `toolList.js` 合适分组中增加 `href` 与 `titleKey`（及图标等）。
4. **静态路由**：在 `site-paths.js` 的 `PATHS_AFTER_LOCALE` 增加路径；跑 `npm run build` 确认预渲染与 sitemap 无遗漏。
5. **i18n**：在 `i18n.js`（及相关 agentPrompt 数据文件）为 `en` / `zh` 补全键；`titleKey` 所指向的键需存在。
6. **（若适用）** 在目标页 `registerAgentPrompt`；`templateKey` 形如 `agentPrompt.imageResize`，与 `specId` 一致。

## UI 与交互（必读）

- 仓库内 **`.cursor/rules/ui-style-guidelines.mdc`**：只使用 `--ccw-*` 主题变量、复用 `control-btn` / `workspace-content-block` / `workspace-primary-actions`、主按钮 Skeleton preset、**勿** 在 `app.css` 用 Svelte 的 `:global()` 包裹（构建会丢）。
- 图片类生成/处理页：**`.cursor/rules/image-tools-preview.mdc`** — 需预览入口，优先 `SliderComparePreview` 做原图/结果对比。

## 构建与质量

- 本地：`npm run dev`；发布前：`npm run build`（含 sitemap 生成脚本）。
- 不要引入与「浏览器端、本地处理」目标冲突的仅服务端 API，除非产品明确要求。

## 可选延伸阅读

- 与 SEO 相关的头信息与路径规范化：参考 `SeoHead`、`seoMeta.js` 及现有 `+page` 的用法。
