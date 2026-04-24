# cloudcreate.ai skills

本仓库为 **CloudCreate.ai** 相关 Agent Skills，供 Cursor / Codex 等工具读取，统一描述仓库约定与开发流程。

## 已收录

| 目录 | 说明 |
|------|------|
| [cloudcreate-ai-usage](./cloudcreate-ai-usage/) | **使用** <https://cloudcreate.ai>：功能列表、按需求选工具、拼带语义的直达 URL（en/zh、hash、与 /ai-spec 的关系） |

## 在项目中使用

将本仓克隆为子模块或单独克隆后，把需要的 skill 目录**复制或符号链接**到项目的 `.cursor/skills/<name>/`（或编辑器文档中说明的个人 skills 目录），确保每个 skill 为包含 `SKILL.md` 的独立文件夹。

在 **freetools** 主仓中，本库通常以 git submodule 挂于 `skills/`。
