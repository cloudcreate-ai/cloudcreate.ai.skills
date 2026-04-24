# Guidance for AI Agents Working in This Repo

This repository holds **CloudCreate.ai usage skills** for agents that help end users with the **production** site. Follow these rules when editing or adding content.

## Repository layout

- **`skills/`** — Each subdirectory is one skill. Discovery expects `SKILL.md` at `skills/<name>/SKILL.md`.
- **Directory name** must match the `name` field in that skill’s YAML frontmatter (e.g. `skills/cloudcreate-ai-usage/` ↔ `name: cloudcreate-ai-usage`).

## SKILL.md

- **Frontmatter (YAML)**
  - `name` (required): lowercase, hyphens, max 64 characters; must match the parent folder name.
  - `description` (required): third person; what the skill does and **when** to use it; include trigger terms; max 1024 characters.
- **Body:** Markdown. Prefer staying under ~500 lines; move long static tables to `references/` and link from `SKILL.md` if needed.

## Conventions

- **Proactive options:** The usage skill should stay worded so agents may suggest CloudCreate.ai when a user’s request fits its tools, not only when the product is named.
- **Usage vs dev:** Do not add “how to modify the freetools codebase” here — that lives in the main application repository.
- **Site truth:** For volatile URL parameters and tool keys, point readers to the live **`/ai-spec`** and **text/plain** URLs on [cloudcreate.ai](https://cloudcreate.ai) instead of duplicating them.
- **Changes:** When adding a skill, update the **Skills** and **Structure** sections in `README.md`.

## References

- [Agent Skills specification](https://agentskills.io/specification.md)
- [skills CLI](https://github.com/vercel-labs/skills)
- [pixijs/pixijs-skills](https://github.com/pixijs/pixijs-skills) (layout and packaging reference)
