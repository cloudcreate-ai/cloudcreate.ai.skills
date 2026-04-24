# cloudcreate.ai skills

**对外发布仓**：本仓库只收录面向 **Agent 直接使用线上站点** 的技能（列功能、选工具、拼直达 URL 等），供任意人在 Cursor / Codex 等环境订阅或拷贝使用。

**与主项目代码仓的分工**：

- **本仓**：站点能力说明 + 可分享链接，**不** 承担「如何改 freetools 源码、目录约定、提 PR」等开发向内容；这类说明放在主项目**自己的**专属目录（例如主仓的 `.cursor/skills/`、项目内文档），由主仓维护。
- **freetools 主仓** 将本库以 **git 子模块** 挂在 `skills/`，仅是为了版本对齐与复用；开发用 skill 仍放在主仓内，不并入本库。

## 已收录

| 目录 | 说明 |
|------|------|
| [cloudcreate-ai-usage](./cloudcreate-ai-usage/) | 使用 <https://cloudcreate.ai>：功能列表、按需求选工具、拼直达 URL（en/zh、hash、与 /ai-spec 的关系） |

## 使用方式

将本仓克隆，或只拷贝需要的子目录，放入 Agent 的 skills 配置路径（如 `.cursor/skills/<name>/`），每个 skill 为包含 `SKILL.md` 的独立文件夹。也可引用本仓作为子模块，再对具体 skill 建符号链接。
