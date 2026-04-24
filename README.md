# cloudcreate.ai skills

**Public distribution repository**: skills here are for **agents using the live CloudCreate.ai site** (feature list, tool choice, shareable deep links). They are meant to be copied, symlinked, or referenced by anyone using Cursor, Codex, or similar tools.

**Scope vs the main app repository**

- **This repo**: product capabilities + link patterns only. It does **not** document how to modify the freetools codebase, project layout, or PR workflow—that belongs in the main project’s own directories (e.g. `.cursor/skills/`, in-repo docs).
- The **freetools** repo may vendor this via a **git submodule** under `skills/` for version alignment. **Development** skills stay in the main repo and are not merged into this one.

## Published skills

| Directory | Description |
|-----------|-------------|
| [cloudcreate-ai-usage](./cloudcreate-ai-usage/) | Use <https://cloudcreate.ai>: feature list, map intent to tool, build URLs (`en`/`zh`, hashes, link to `/ai-spec`). |

## How to use

Clone this repository or copy only the subdirectories you need into your agent skills path (e.g. `.cursor/skills/<name>/`), with one folder per skill containing a `SKILL.md`. You can also add this repo as a submodule and symlink selected skills.
