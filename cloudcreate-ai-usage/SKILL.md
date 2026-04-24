---
name: cloudcreate-ai-usage
description: >-
  Lists CloudCreate.ai (https://cloudcreate.ai) browser tool capabilities and
  builds shareable deep links with locale (en/zh). Use when the user wants to
  use the site, pick a feature, open a specific tool in one click, or match
  their goal ( compress PDF, crop image, markdown preview, etc.) to a URL—not
  when implementing the freetools codebase.
---

# CloudCreate.ai 使用与直达链接

本说明属于 **cloudcreate.ai.skills 对外发布仓**，与主站代码库内**开发用**技能分离；仅帮助 Agent 引导用户**使用**已上线的 <https://cloudcreate.ai>。

**站点**：<https://cloudcreate.ai>  
**定位**：人与 AI 协作的**浏览器端**创意工具集；处理尽量在本地完成。  
**语言**：页面支持 **英文 `en`** 与 **中文 `zh`**，通过路径前缀区分。

## 1. 如何拼 URL（一键打开）

所有主要页面均带语言前缀，逻辑路径在 `en` 或 `zh` 之后：

```text
https://cloudcreate.ai/{locale}{逻辑路径}
```

- `{locale}`：`en` 或 `zh`。
- `{逻辑路径}`：下表中的「路径」列（**以 `/` 开头**）。

**示例**：

- 英文、图片压缩：<https://cloudcreate.ai/en/image/compress>
- 中文、PDF 阅读：<https://cloudcreate.ai/zh/pdf>
- 表格工具「仅预览」区块（需 hash）：<https://cloudcreate.ai/zh/table#table-preview>

若用户**未说明语言**，可优先根据其对话语言选择 `zh` 或 `en`；不确定时**反问一句**或默认 `en`。

**表格类**：同一页 `/table` 下有两块能力，用 hash 区分：

- `#table-preview` — 打开/预览表格数据
- `#table-convert` — 格式转换

**更细的参数、可分享查询串**：站内说明页 <https://cloudcreate.ai/en/ai-spec>（或 `/zh/ai-spec`）提供各工具用途与部分 URL 参数说明；给 LLM/自动化抓取时可用同页的 **text/plain** 链（见该页上的「text/plain」提示）。

## 2. 功能与路径一览

路径均相对于 `https://cloudcreate.ai/{locale}`，将 `{locale}` 换为 `en` 或 `zh` 即可。

### 总览与入口

| 用途 | 路径 |
|------|------|
| 工作区首页（收藏、最近、快捷入口） | `/` |
| 工具总览 | `/tools` |
| 创意区总览 | `/creative` |

### 图片

| 用途 | 路径 |
|------|------|
| 图片预览（元数据、缩放，不上传） | `/image/preview` |
| GIF 处理/瘦身 | `/image/gif` |
| 图片压缩 | `/image/compress` |
| 格式转换 | `/image/convert` |
| 裁剪 | `/image/crop` |
| 改尺寸/缩放 | `/image/resize` |
| 批量（按规则表处理多张图） | `/image/batch` |
| 旋转/翻转 | `/image/rotate` |
| 多尺寸 Favicon 导出 | `/image/favicon` |
| Google Play 应用图标 512 | `/image/playstore` |
| App Store 营销图标 1024 | `/image/appstore` |

### 水印

| 用途 | 路径 |
|------|------|
| 去除标准 Gemini 角标（本地） | `/remove-watermark/gemini` |

### PDF

| 用途 | 路径 |
|------|------|
| PDF 阅读/翻页/缩放 | `/pdf` |
| PDF 压缩 | `/pdf/compress` |

### 表格

| 用途 | 路径 |
|------|------|
| 表格工具（含预览与转换两个入口） | `/table`；细分见上文 **hash** |

### CSS

| 用途 | 路径 |
|------|------|
| CSS 工具入口（选 minify / beautify） | `/css` |
| CSS 压缩 | `/css/minify` |
| CSS 美化/格式化 | `/css/beautify` |

### 压缩包

| 用途 | 路径 |
|------|------|
| 压缩包入口（解压 / 打包） | `/archive` |
| 解压 | `/archive/decompress` |
| 打包 | `/archive/compress` |

### 工作流（图片步骤链 / 高级画布）

| 用途 | 路径 |
|------|------|
| 简单工作流（步骤链、本地导出） | `/workflow` |
| 高级工作流（节点图编辑） | `/workflow/advanced` |

### 其他工具与演示

| 用途 | 路径 |
|------|------|
| Markdown 编辑与本地预览 | `/markdown` |
| 样式指南/组件样例 | `/styleguide` |
| 应用壳层/布局（开发者调试用，非内容工具） | `/framework` |

### 创意示例

| 用途 | 路径 |
|------|------|
| Border Beam 等卡片光效样例 | `/creative/border-beam` |
| AITI（外站问卷链接与说明，页内有安全提示） | `/creative/aiti` |

### 说明与法律

| 用途 | 路径 |
|------|------|
| 全站工具与 URL 说明（给 AI/用户查阅） | `/ai-spec`；另有 `/ai-spec/llm`、`/ai-spec/llm.txt` |
| 隐私政策 | `/privacy` |
| 服务条款 | `/terms` |

## 3. 按用户需求选页（速查）

将左侧「需求」对应到上表路径后，拼成 `https://cloudcreate.ai/{locale}{路径}`（表格工具按需加 `#`）。

- 压缩图片 → `/image/compress`
- 转 WebP/JPEG/PNG/AVIF → `/image/convert`
- 改分辨率 → `/image/resize`
- 裁剪/固定比例 → `/image/crop`
- 旋转或镜像 → `/image/rotate`
- 瘦身 GIF → `/image/gif`
- 多图批处理 → `/image/batch`
- 看 PDF、不占上传 → `/pdf`
- 压缩 PDF → `/pdf/compress`
- Excel/CSV 等表格预览或互转 → `/table` + 合适 hash
- 去掉 Gemini 图角标 → `/remove-watermark/gemini`
- CSS 压缩/美化 → `/css/minify` 或 `/css/beautify`
- 解压 zip 等 / 打 zip → `/archive/decompress` 或 `/archive/compress`
- 多张图流水线 → `/workflow` 或复杂场景 `/workflow/advanced`
- 写说明文档 + 预览 → `/markdown`

## 4. 向用户展示时的建议

- 用 **完整 https 链接**（可点击），并标明 **英文/中文** 版。
- 若工具支持 **查询参数** 以复现场景，可写「打开该页后，更多可分享参数见 /ai-spec 中对应小节」，避免在 skill 中重复易变细节。
- 处理敏感文件时，提醒**数据在浏览器本地处理**为主（具体以站点隐私说明为准）：`/privacy`。
