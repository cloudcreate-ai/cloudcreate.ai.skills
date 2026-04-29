# ClawHub listing guide

This document is the release checklist and fill-in template for publishing this repo's skill to ClawHub.

Source reference:
- OpenClaw docs: `https://docs.openclaw.ai/tools/clawhub`
- Publish command: `clawhub skill publish <path>`

## 1) Required fields

`clawhub skill publish` supports these listing fields:

- `--slug`: unique skill slug in ClawHub
- `--name`: display name shown in ClawHub
- `--version`: semver version (`x.y.z`)
- `--changelog`: release notes for this version
- `--tags`: comma-separated tags (default includes `latest`)

## 2) Recommended values for this repo

Use the values below for the current skill:

- `path`: `./skills/cloudcreate-tools`
- `slug`: `cloudcreate-tools`
- `name`: `CloudCreate Tools`
- `version`: keep in sync with the skill release you want to publish
- `tags`: `latest,cloudcreate,image,pdf,css,archive,workflow,table,markdown`

Suggested changelog format:

```text
<version> - <date>
- Renamed skill to cloudcreate-tools
- Added capability matrix in README
- Improved CLI-first link generation guidance
```

## 3) Pre-publish checklist

1. Confirm skill directory and frontmatter match:
   - folder: `skills/cloudcreate-tools/`
   - `SKILL.md` frontmatter: `name: cloudcreate-tools`
2. Confirm dry-run package is clean:
   - `npm publish --dry-run --access public`
3. Confirm local install command works:
   - `npx --yes skills add https://github.com/cloudcreate-ai/cloudcreate.ai.skills --skill cloudcreate-tools --agent codex -y --copy`
4. Confirm changelog text is ready.

## 4) Login

Install CLI if needed:

```bash
npm i -g clawhub
```

Login (browser flow):

```bash
clawhub login
```

Optional token flow:

```bash
clawhub login --token <your_token>
```

Verify:

```bash
clawhub whoami
```

## 5) Publish command (copy-paste)

```bash
clawhub skill publish ./skills/cloudcreate-tools \
  --slug cloudcreate-tools \
  --name "CloudCreate Tools" \
  --version 1.0.2 \
  --changelog "1.0.2 - renamed skill to cloudcreate-tools; added capability matrix and docs refinements." \
  --tags latest,cloudcreate,image,pdf,css,archive,workflow,table,markdown
```

## 6) Post-publish checks

1. Check the listing page in ClawHub search.
2. Install by slug in a clean workspace:
   - `openclaw skills install cloudcreate-tools`
   - or `clawhub install cloudcreate-tools`
3. Start a new session and verify the skill is loaded.

## 7) Roll-forward update template

For next release:

```bash
clawhub skill publish ./skills/cloudcreate-tools \
  --slug cloudcreate-tools \
  --name "CloudCreate Tools" \
  --version <next_version> \
  --changelog "<next_version> - <summary>" \
  --tags latest,cloudcreate,image,pdf,css,archive,workflow,table,markdown
```
