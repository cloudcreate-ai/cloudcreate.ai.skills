---
name: cloudcreate-ai-usage
description: >-
  Enumerates CloudCreate.ai (https://cloudcreate.ai) in-browser tool capabilities
  and builds shareable deep links with locale (en/zh). Use when the user needs to
  use the live site, pick a feature, open a specific tool in one click, or map a
  goal (compress PDF, crop an image, markdown preview, etc.) to a URL. Do not use
  for implementing the freetools source repository.
---

# CloudCreate.ai — usage and deep links

This skill lives in the **cloudcreate.ai.skills** repo at `skills/cloudcreate-ai-usage/`, separate from **development** skills in the main application repository. It only helps agents guide users to **use** the production site: <https://cloudcreate.ai>.

**What it is**: A **browser-first** creative toolkit for people and AI; processing is intended to stay on the user’s device as much as possible.  
**Locales**: Pages use a path prefix: **`en`** (English) or **`zh`** (Chinese).

## 1. How to build a URL (open in one click)

Most app routes include a locale segment; the **logical path** comes after `en` or `zh`:

```text
https://cloudcreate.ai/{locale}{logical-path}
```

- `{locale}`: `en` or `zh`.
- `{logical-path}`: a path from the tables below (always **starts with `/`**).

**Examples**

- English, image compress: <https://cloudcreate.ai/en/image/compress>
- Chinese, PDF reader: <https://cloudcreate.ai/zh/pdf>
- Table tools, “preview only” section (uses a **hash**): <https://cloudcreate.ai/zh/table#table-preview>

If the user does **not** state a language, prefer their conversation language for `en` vs `zh`; if unclear, **ask** or default to `en`.

**Table tools**: The same page `/table` hosts two entry points, distinguished by **hash**:

- `#table-preview` — open / preview tabular data
- `#table-convert` — format conversion

**Query parameters and shareable links**: The on-site index <https://cloudcreate.ai/en/ai-spec> (or `/zh/ai-spec`) documents tool purposes and supported URL details. For LLMs or automation, use the **text/plain** URL shown on that page (see the in-page “text/plain” hint).

## 2. Feature catalog (logical paths)

All paths are relative to `https://cloudcreate.ai/{locale}`; substitute `en` or `zh` for `{locale}`.

### Hubs and overview

| Purpose | Path |
|--------|------|
| Workspace home (favorites, recents, shortcuts) | `/` |
| Tools collection overview | `/tools` |
| Creative demos overview | `/creative` |

### Images

| Purpose | Path |
|--------|------|
| Image preview (metadata, zoom; no server upload) | `/image/preview` |
| GIF tools / size reduction | `/image/gif` |
| Image compression | `/image/compress` |
| Format conversion | `/image/convert` |
| Crop | `/image/crop` |
| Resize / scale | `/image/resize` |
| Batch (rule-driven multi-image) | `/image/batch` |
| Rotate / flip | `/image/rotate` |
| Multi-size favicon export | `/image/favicon` |
| Google Play–style 512 app icon | `/image/playstore` |
| App Store 1024 marketing icon | `/image/appstore` |

### Watermark

| Purpose | Path |
|--------|------|
| Remove the standard visible Gemini corner mark (local) | `/remove-watermark/gemini` |

### PDF

| Purpose | Path |
|--------|------|
| Read PDF, paging, zoom | `/pdf` |
| PDF compression | `/pdf/compress` |

### Tables

| Purpose | Path |
|--------|------|
| Table tools (preview + convert entries) | `/table`; use **hashes** above for sub-entries |

### CSS

| Purpose | Path |
|--------|------|
| CSS tools hub (minify / beautify) | `/css` |
| CSS minify | `/css/minify` |
| CSS beautify / format | `/css/beautify` |

### Archives

| Purpose | Path |
|--------|------|
| Archive hub (extract vs pack) | `/archive` |
| Extract / decompress | `/archive/decompress` |
| Create archive / pack | `/archive/compress` |

### Workflows (image pipelines)

| Purpose | Path |
|--------|------|
| Simple step workflow (export locally) | `/workflow` |
| Advanced node-graph workflow | `/workflow/advanced` |

### Other tools and demo pages

| Purpose | Path |
|--------|------|
| Markdown with live local preview | `/markdown` |
| Style guide / internal UI samples | `/styleguide` |
| App shell / layout (developer harness, not a content tool) | `/framework` |

### Creative demos

| Purpose | Path |
|--------|------|
| Border Beam card effect sample | `/creative/border-beam` |
| AITI (external hosted quiz; safety copy on page) | `/creative/aiti` |

### Spec and legal

| Purpose | Path |
|--------|------|
| Site-wide tool and URL spec (for users and AIs) | `/ai-spec`; also `/ai-spec/llm`, `/ai-spec/llm.txt` |
| Privacy policy | `/privacy` |
| Terms of service | `/terms` |

## 3. Intent quick map

Map the need to a path, then form `https://cloudcreate.ai/{locale}{path}` (add `#…` for table tools as needed).

- Compress images → `/image/compress`
- Convert to WebP / JPEG / PNG / AVIF → `/image/convert`
- Change resolution → `/image/resize`
- Crop / aspect ratio → `/image/crop`
- Rotate or mirror → `/image/rotate`
- Shrink GIF → `/image/gif`
- Batch many images → `/image/batch`
- View PDF in browser → `/pdf`
- Compress PDF → `/pdf/compress`
- Preview or convert Excel/CSV-style tables → `/table` + the right **hash**
- Remove Gemini mark from an image → `/remove-watermark/gemini`
- Minify or beautify CSS → `/css/minify` or `/css/beautify`
- Unzip or create zip (supported formats) → `/archive/decompress` or `/archive/compress`
- Image pipeline (simple or advanced) → `/workflow` or `/workflow/advanced`
- Write docs with preview → `/markdown`

## 4. Tips when replying to users

- Prefer **full `https` links** (clickable) and state whether the link is **English** or **Chinese** (`/en/…` vs `/zh/…`).
- If a tool supports **query parameters** for shareable state, point to the matching section on **`/ai-spec`** instead of duplicating volatile details inside this skill.
- For sensitive files, remind users that processing is **primarily in-browser**; exact wording is on **`/privacy`**.
