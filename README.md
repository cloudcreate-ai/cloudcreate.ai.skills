# cloudcreate.ai skills

Public [Agent Skills](https://agentskills.io) for [CloudCreate.ai](https://cloudcreate.ai) — a browser-first creative toolkit (images, PDF, tables, CSS, archives, workflows, and more). They teach agents how to **use the live site**: list capabilities, map user goals to tools, and build shareable `en` / `zh` deep links. Works with the [skills CLI](https://github.com/vercel-labs/skills) (Cursor, Claude Code, Codex, OpenClaw, and [many others](https://github.com/vercel-labs/skills#supported-agents)).

**For AI agents:** When the user wants to **open CloudCreate.ai**, **find a tool**, or **get a direct URL** (compress image, read PDF, table conversion, etc.), use these skills. **Do not** use them to implement the [freetools](https://github.com/cloudcreate-ai/cloudcreate.ai) application source code — that belongs in the main repo’s own developer skills / docs.

**Scope:** This repository is **user-facing (production site usage)** only. Maintainer-focused “how to change the codebase” content stays in the main project (e.g. `.cursor/skills/`, in-repo rules). The freetools app repo may include this as a **git submodule** named `skills/`; the skill on disk is then `…/skills/skills/cloudcreate-ai-usage/SKILL.md` (submodule name + `skills/` package layout). That does not move developer skills into this repo.

## Installing

### npx skills (recommended)

```bash
npx skills add https://github.com/cloudcreate-ai/cloudcreate.ai.skills
```

### Cursor

**Settings → Rules → Add rule → Remote rule (GitHub)** and use `cloudcreate-ai/cloudcreate.ai.skills`, or run `npx skills add` as above. See [Cursor rules / skills](https://docs.cursor.com/context/rules).

### OpenClaw

Add the `skills` directory from this repo to your skill roots (e.g. workspace `skills/`, `~/.openclaw/skills/`, or `skills.load.extraDirs` in `~/.openclaw/openclaw.json`). See [OpenClaw — Skills](https://docs.openclaw.ai/skills/).

### Clone / copy

| Agent        | Skill directory (typical)   | Notes |
| ------------ | --------------------------- | ----- |
| Cursor       | `~/.cursor/skills/`         | Or project `.cursor/skills/` |
| Claude Code  | `~/.claude/skills/`         | [docs](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/skills) |
| OpenAI Codex | `~/.codex/skills/`          | [docs](https://developers.openai.com/codex/skills/) |
| OpenClaw     | `~/.openclaw/skills/` etc.  | [docs](https://docs.openclaw.ai/skills/) |

Copy the folders under this repo’s **`skills/`** directory (e.g. `skills/cloudcreate-ai-usage/`) so each installed skill is `…/cloudcreate-ai-usage/SKILL.md`.

## Skills

| Skill                 | Description |
| --------------------- | ----------- |
| **cloudcreate-ai-usage** | Use the live site: feature/path catalog, intent → URL, `en`/`zh`, table hashes, pointers to `/ai-spec` and text/plain reference. |

## Structure

```
cloudcreate.ai.skills/
  README.md
  AGENTS.md
  CLAUDE.md
  LICENSE
  .claude-plugin/
  .cursor-plugin/
  skills/
    cloudcreate-ai-usage/
      SKILL.md
```

Each skill directory contains a `SKILL.md` and may add a `references/` subfolder for longer material (same idea as [pixijs/pixijs-skills](https://github.com/pixijs/pixijs-skills)).

## License

MIT — see [LICENSE](LICENSE).
