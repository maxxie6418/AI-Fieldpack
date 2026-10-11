# THIRD_PARTY_NOTICES

本文件登记仓库内收录的第三方内容及其许可，供合规核查与溯源。

## 登记规则

- 默认收录：除非内容明确声明禁止再分发，否则不因许可不明而拒绝收录；许可与作者能考证就写实，考证不到的注明「未能考证」。
- 收录时保留内容自带的 `LICENSE` 与版权声明文件，并在下表中写明版权归属。
- 每条登记五项：名称、作者 / 来源 URL、许可类型、在本库中的位置、用途说明。
- 从 `_sandbox/` 分流进来的第三方内容，完成登记后才能进入成果区。
- 完整规则见 [AGENTS.md](AGENTS.md) 的「收录第三方内容」一节。

## 登记表

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| algorithmic-art | Anthropic，`github.com/anthropics/skills` 的 `skills/algorithmic-art/` | Apache-2.0（上游 `LICENSE.txt` 附录写 `Copyright 2026 Anthropic, PBC.`；本地副本为占位符，署名行已丢失） | `packs/skills/algorithmic-art/` | p5.js 算法艺术创作，随机种子可复现 |
| brand-guidelines | Anthropic，`github.com/anthropics/skills` 的 `skills/brand-guidelines/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/brand-guidelines/` | 将 Anthropic 品牌色与字体排版应用到产物上 |
| canvas-design | Anthropic，`github.com/anthropics/skills` 的 `skills/canvas-design/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/canvas-design/` | 静态视觉设计（海报、封面等），输出 .png / .pdf；本库补写了输出路径，见下 |
| frontend-skill | Anthropic，`github.com/anthropics/skills` 的 `skills/frontend-design/`（本地改名为 `frontend-skill`、删去 frontmatter 的 `license` 字段、description 中文化） | Apache-2.0（上游 `LICENSE.txt`；上游该副本的版权人栏本就未填） | `packs/skills/frontend-skill/` | 视觉表现力优先的落地页 / 网站 / 应用 / 原型 / 游戏 UI 设计方法 |
| internal-comms | Anthropic，`github.com/anthropics/skills` 的 `skills/internal-comms/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/internal-comms/` | 撰写内部沟通材料（3P 更新、简报、FAQ） |
| screenshot | OpenAI，`github.com/openai/skills` 的 `skills/.curated/screenshot/` | Apache-2.0（上游版权人栏为 `[yyyy] [name of copyright owner]` 占位符；本地副本另把 170 行的行首缩进去掉） | `packs/skills/screenshot/` | macOS / Windows 系统级桌面与窗口截图 |
| security-best-practices | OpenAI，`github.com/openai/skills` 的 `skills/.curated/security-best-practices/` | Apache-2.0（同上） | `packs/skills/security-best-practices/` | 按语言与框架做安全审查（Python / JS-TS / Go） |
| slides | OpenAI，`github.com/openai/skills` 的 `skills/.curated/slides/`（该目录已于 2026-04-16 被上游删除，commit `fdf90d65`） | Apache-2.0（本地 `LICENSE.txt` 版权行写 `Copyright (c) Microsoft Corporation.`，与上游同族占位符写法不同，来源待查） | `packs/skills/slides/` | 用 PptxGenJS 生成 pptx 并渲染校验 |
| theme-factory | Anthropic，`github.com/anthropics/skills` 的 `skills/theme-factory/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/theme-factory/` | 为作品套用十套预设主题 |
| web-artifacts-builder | Anthropic，`github.com/anthropics/skills` 的 `skills/web-artifacts-builder/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/web-artifacts-builder/` | 构建并打包 React + Tailwind + shadcn 的 HTML 作品 |
| composition-patterns | Vercel，`github.com/vercel-labs/agent-skills` 的 `skills/composition-patterns/` | MIT（各技能 `SKILL.md` frontmatter 自带 `license: MIT` 与 `metadata.author: vercel`；该仓库顶层无 `LICENSE`，`package.json` 的 `license` 字段为空） | `packs/skills/composition-patterns/` | React 组合模式与 API 设计规范 |
| git-commit | GitHub，`github.com/github/awesome-copilot` 的 `skills/git-commit/` | MIT（`Copyright GitHub, Inc.`；与本地 frontmatter 的 `license: MIT` 一致） | `packs/skills/git-commit/` | 约定式提交消息与智能暂存 |
| react-best-practices | Vercel，`github.com/vercel-labs/agent-skills` 的 `skills/react-best-practices/`（本地为较早快照，上游另多 4 条规则） | MIT（同上） | `packs/skills/react-best-practices/` | React / Next.js 性能规则库（本地 66 条） |
| react-native-skills | Vercel，`github.com/vercel-labs/agent-skills` 的 `skills/react-native-skills/` | MIT（同上） | `packs/skills/react-native-skills/` | React Native / Expo 性能与 UI 规范 |
| redis-development | Redis，`github.com/redis/agent-skills` 的 `skills/redis-development/`（该技能已于 2026-05-27 被上游退役，commit `18da4e42`；本地缺 `evals/README.md` 与 `.cursor-plugin/plugin.json`） | MIT（`Copyright (c) 2026 Redis, Inc.`） | `packs/skills/redis-development/` | Redis 数据建模、查询与向量检索规范 |

### 登记说明

- 本地收录的第三方 skill 都是**中文化派生版**：每个 `SKILL.md` 的 `description` 由英文改写为中文，行尾统一为 CRLF。上游同族仓库（`anthropics/skills`、`cloudflare/skills`、`openai/skills`、`larksuite/cli`、`obra/superpowers` 等）均为 LF，比对时须先做行尾归一。
- **署名行丢失**：6 个来自 `anthropics/skills` 的包（`algorithmic-art`、`brand-guidelines`、`canvas-design`、`internal-comms`、`theme-factory`、`web-artifacts-builder`），上游 `LICENSE.txt` 附录写的是 `Copyright 2026 Anthropic, PBC.`，本地副本却全部退回 Apache 官方模板占位符 `[yyyy] [name of copyright owner]`。再分发时无法据此完成署名，如需合规应补回。
- 版权人栏留占位符本身是常见现象：`cloudflare/skills`、`openai/skills` 的上游 `LICENSE.txt` 同样是占位符，不构成许可缺陷。
- 3 个包的目录名与 frontmatter `name` 不一致：`composition-patterns`（`vercel-composition-patterns`）、`react-best-practices`（`vercel-react-best-practices`）、`react-native-skills`（`vercel-react-native-skills`）。入库时保留其原目录名与 `SKILL.md` 入口名：skill 的调用名由目录名与 frontmatter 的 `name` 共同决定，改名会使包无法被宿主调用。按 [AGENTS.md](AGENTS.md) 的「二、命名与查找」，落档以成品自身的格式要求为准。
- `packs/skills/vibecoding-standards/` 不属于第三方内容，故不在上表：其 15 篇规范文档由用户本人整理，是本库自有内容，无需登记与署名。
- `packs/skills/canvas-design/` 收录的是上游包的**修改版**：本库新增 `references/rendering.md`（输出路径与字体使用说明），并把 `SKILL.md` 中一段字体指引改为优先使用包内 `canvas-fonts/`。按 Apache-2.0 第 4(b) 条，这两处改动都带显著说明——`SKILL.md` frontmatter 之后与 `references/rendering.md` 标题下各有一条 `Modified/Added by AI Fieldpack` 标注。包内随附的 81 个字体文件（54 个字重、27 个族）为 SIL OFL 1.1，各族的 `*-OFL.txt` 随文件保留。

## 待办

- `_sandbox/skills/` 余 36 个第三方 skill 尚未登记。按上面的登记规则，不再以「许可不明」为由阻挡收录；补登记后即可并入成果区。
- 这 36 个的来源与许可以下 31 个已考证（均可复用于登记表）：`cloudflare`、`cloudflare-one`、`agents-sdk`、`durable-objects`、`turnstile-spin`、`nextjs-on-cloudflare`、`workers-best-practices`、`wrangler`、`web-perf` → `cloudflare/skills`（Apache-2.0）；`codebase-design`、`code-review`、`diagnosing-bugs`、`domain-modeling`、`grilling`、`research`、`setup-matt-pocock-skills`、`teach` → `mattpocock/skills`（MIT，`Copyright (c) 2026 Matt Pocock`）；`brainstorming`、`writing-plans`、`executing-plans`、`test-driven-development` → `obra/superpowers`（MIT，`Copyright (c) 2025 Jesse Vincent`，基线为 v5.0.6 / v5.0.7）；`lark-apps`、`lark-doc`、`lark-markdown`、`lark-vc-agent` → `larksuite/cli`（MIT，`Copyright (c) 2026 Lark Technologies Pte. Ltd.`）；`json-canvas`、`defuddle` → `kepano/obsidian-skills`（MIT）；`electron`、`dogfood` → `vercel-labs/agent-browser`（Apache-2.0）；`shadcn` → `shadcn-ui/ui`（MIT）；`doc-coauthoring` → `anthropics/skills`（该技能目录上游没有 `LICENSE.txt`，仓库根目录也没有许可文件）。
- 余 5 个未考证来源与许可：`agent-browser`、`find-skills`、`web-design-guidelines`、`caveman`、`gh-cli`。
