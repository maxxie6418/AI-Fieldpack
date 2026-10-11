# THIRD_PARTY_NOTICES

本文件登记仓库内收录的第三方内容及其许可，供合规核查与溯源。

## 登记规则

- 默认收录：除非内容明确声明禁止再分发，否则不因许可不明而拒绝收录；许可与作者能考证就写实，考证不到的注明「未能考证」。
- 收录时保留内容自带的 `LICENSE` 与版权声明文件，并在下表中写明版权归属。
- 每条登记五项：名称、作者 / 来源 URL、许可类型、在本库中的位置、用途说明。
- 从 `_sandbox/` 分流进来的第三方内容，完成登记后才能进入成果区。
- 完整规则见 [AGENTS.md](AGENTS.md) 的「收录第三方内容」一节。

## 登记表

### 来自 `anthropics/skills`

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| algorithmic-art | Anthropic，`github.com/anthropics/skills` 的 `skills/algorithmic-art/` | Apache-2.0（上游 `LICENSE.txt` 附录写 `Copyright 2026 Anthropic, PBC.`；本地副本为占位符，署名行已丢失） | `packs/skills/algorithmic-art/` | p5.js 算法艺术创作，随机种子可复现 |
| brand-guidelines | Anthropic，同上 `skills/brand-guidelines/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/brand-guidelines/` | 将 Anthropic 品牌色与字体排版应用到产物上 |
| canvas-design | Anthropic，同上 `skills/canvas-design/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/canvas-design/` | 静态视觉设计（海报、封面等），输出 .png / .pdf；本库补写了输出路径，见下 |
| doc-coauthoring | Anthropic，同上 `skills/doc-coauthoring/` | 上游该目录与仓库根目录都没有许可文件 | `packs/skills/doc-coauthoring/` | 与用户协作撰写文档（含子代理流程与降级分支） |
| frontend-skill | Anthropic，同上 `skills/frontend-design/`（本地改名为 `frontend-skill`、删去 frontmatter 的 `license` 字段、description 中文化） | Apache-2.0（上游 `LICENSE.txt`；上游该副本的版权人栏本就未填） | `packs/skills/frontend-skill/` | 视觉表现力优先的落地页 / 网站 / 应用 / 原型 / 游戏 UI 设计方法 |
| internal-comms | Anthropic，同上 `skills/internal-comms/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/internal-comms/` | 撰写内部沟通材料（3P 更新、简报、FAQ） |
| theme-factory | Anthropic，同上 `skills/theme-factory/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/theme-factory/` | 为作品套用十套预设主题 |
| web-artifacts-builder | Anthropic，同上 `skills/web-artifacts-builder/` | Apache-2.0（同上，本地署名行已丢失） | `packs/skills/web-artifacts-builder/` | 构建并打包 React + Tailwind + shadcn 的 HTML 作品 |

### 来自 `openai/skills`（路径均在 `skills/.curated/` 下）

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| screenshot | OpenAI，`github.com/openai/skills` 的 `skills/.curated/screenshot/` | Apache-2.0（上游版权人栏为 `[yyyy] [name of copyright owner]` 占位符；本地副本另把 170 行的行首缩进去掉） | `packs/skills/screenshot/` | macOS / Windows 系统级桌面与窗口截图 |
| security-best-practices | OpenAI，同上 `skills/.curated/security-best-practices/` | Apache-2.0（同上） | `packs/skills/security-best-practices/` | 按语言与框架做安全审查（Python / JS-TS / Go） |
| slides | OpenAI，同上 `skills/.curated/slides/`（该目录已于 2026-04-16 被上游删除，commit `fdf90d65`） | Apache-2.0（本地 `LICENSE.txt` 版权行写 `Copyright (c) Microsoft Corporation.`，与上游同族占位符写法不同，来源待查） | `packs/skills/slides/` | 用 PptxGenJS 生成 pptx 并渲染校验 |

### 来自 `cloudflare/skills`（Apache-2.0）

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| agents-sdk | Cloudflare，`github.com/cloudflare/skills` 的 `skills/agents-sdk/` | Apache-2.0（上游版权人栏同为占位符） | `packs/skills/agents-sdk/` | 用 Agents SDK 构建有状态 AI agent |
| cloudflare | Cloudflare，同上 `skills/cloudflare/` | Apache-2.0（同上） | `packs/skills/cloudflare/` | Cloudflare 全产品线开发参考（57 个产品目录、288 篇文档） |
| cloudflare-one | Cloudflare，同上 `skills/cloudflare-one/` | Apache-2.0（同上） | `packs/skills/cloudflare-one/` | Zero Trust / SASE 接入与配置 |
| durable-objects | Cloudflare，同上 `skills/durable-objects/` | Apache-2.0（同上） | `packs/skills/durable-objects/` | Durable Objects 状态、并发与测试规则 |
| nextjs-on-cloudflare | Cloudflare，同上 `skills/nextjs-on-cloudflare/` | Apache-2.0（同上） | `packs/skills/nextjs-on-cloudflare/` | Next.js 部署到 Cloudflare 的路由选择 |
| turnstile-spin | Cloudflare，同上 `skills/turnstile-spin/` | Apache-2.0（同上） | `packs/skills/turnstile-spin/` | Turnstile 验证码接入与校验脚本 |
| web-perf | Cloudflare，同上 `skills/web-perf/` | Apache-2.0（同上） | `packs/skills/web-perf/` | 用 Chrome DevTools 分析页面性能 |
| workers-best-practices | Cloudflare，同上 `skills/workers-best-practices/` | Apache-2.0（同上） | `packs/skills/workers-best-practices/` | Workers 生产环境实践规则 |
| wrangler | Cloudflare，同上 `skills/wrangler/` | Apache-2.0（同上） | `packs/skills/wrangler/` | Wrangler CLI 用法 |

### 来自 `vercel-labs` 各仓库（许可逐行另注）

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| composition-patterns | Vercel，`github.com/vercel-labs/agent-skills` 的 `skills/composition-patterns/` | MIT | `packs/skills/composition-patterns/` | React 组合模式与 API 设计规范 |
| react-best-practices | Vercel，同上 `skills/react-best-practices/`（本地为较早快照，上游另多 4 条规则） | MIT | `packs/skills/react-best-practices/` | React / Next.js 性能规则库（本地 66 条） |
| react-native-skills | Vercel，同上 `skills/react-native-skills/` | MIT | `packs/skills/react-native-skills/` | React Native / Expo 性能与 UI 规范 |
| web-design-guidelines | Vercel，`github.com/vercel-labs/agent-skills` 的 `skills/web-design-guidelines/` | 该仓库无 `LICENSE` 文件、`package.json` 无 `license` 字段；唯一声明是 README「## License」段的一个词 `MIT`，未声明版权人；技能 frontmatter 也无 `license` 字段 | `packs/skills/web-design-guidelines/` | 按 Web Interface Guidelines 审查 UI |
| electron | Vercel，`github.com/vercel-labs/agent-browser` 的 `skill-data/electron/` | Apache-2.0 | `packs/skills/electron/` | 调试 Electron 应用（经 agent-browser CLI） |
| dogfood | Vercel，同上 `skill-data/dogfood/` | Apache-2.0 | `packs/skills/dogfood/` | 对 CLI / 工具做端到端试用并出报告 |

### 来自 `mattpocock/skills`（MIT，`Copyright (c) 2026 Matt Pocock`）

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| codebase-design | Matt Pocock，`github.com/mattpocock/skills` 的 `skills/engineering/codebase-design/` | MIT | `packs/skills/codebase-design/` | 模块与接口的深化设计（含并行子代理流程） |
| code-review | Matt Pocock，同上 `skills/engineering/code-review/` | MIT | `packs/skills/code-review/` | 按团队标准做代码审查 |
| diagnosing-bugs | Matt Pocock，同上 `skills/engineering/diagnosing-bugs/` | MIT | `packs/skills/diagnosing-bugs/` | 系统化定位缺陷根因（含人机回环脚本） |
| domain-modeling | Matt Pocock，同上 `skills/engineering/domain-modeling/` | MIT | `packs/skills/domain-modeling/` | 维护领域术语与 ADR（本地 `CONTEXT-FORMAT.md` 对应上游 `GLOSSARY-FORMAT.md`，文件名被改） |
| research | Matt Pocock，同上 `skills/engineering/research/` | MIT | `packs/skills/research/` | 做有出处的调研 |
| setup-matt-pocock-skills | Matt Pocock，同上 `skills/engineering/setup-matt-pocock-skills/` | MIT | `packs/skills/setup-matt-pocock-skills/` | 为项目装配套件（issue tracker、triage 标签、领域文档） |
| grilling | Matt Pocock，同上 `skills/productivity/grilling/` | MIT | `packs/skills/grilling/` | 对方案做不间断质询以打磨 |
| teach | Matt Pocock，同上 `skills/productivity/teach/` | MIT | `packs/skills/teach/` | 按用户水平持续教学（含任务、学习记录、词汇表格式） |

### 其余来源

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| brainstorming | Jesse Vincent，`github.com/obra/superpowers` 的 `skills/brainstorming/`（基线 v5.0.6 / v5.0.7） | MIT（`Copyright (c) 2025 Jesse Vincent`） | `packs/skills/brainstorming/` | 把模糊想法发散成方案再收敛为设计稿 |
| writing-plans | Jesse Vincent，同上 `skills/writing-plans/` | MIT（同上） | `packs/skills/writing-plans/` | 把设计写成可逐步执行的实现计划 |
| executing-plans | Jesse Vincent，同上 `skills/executing-plans/` | MIT（同上） | `packs/skills/executing-plans/` | 按既定计划逐任务执行并收尾 |
| test-driven-development | Jesse Vincent，同上 `skills/test-driven-development/` | MIT（同上） | `packs/skills/test-driven-development/` | TDD 红绿重构流程与反模式 |
| lark-apps | Lark，`github.com/larksuite/cli` 的 `skills/lark-apps/`（基线 CLI v1.0.96，commit `32d1988`） | MIT（`Copyright (c) 2026 Lark Technologies Pte. Ltd.`） | `packs/skills/lark-apps/` | 飞书妙搭应用开发（29 篇命令参考 + 创意设计子技能） |
| lark-doc | Lark，同上 `skills/lark-doc/` | MIT（同上） | `packs/skills/lark-doc/` | 飞书云文档读写与体裁模板（15 + 28 篇） |
| lark-markdown | Lark，同上 `skills/lark-markdown/` | MIT（同上） | `packs/skills/lark-markdown/` | 飞书文档的 markdown 子命令（fetch / create / patch / diff / overwrite） |
| lark-vc-agent | Lark，同上 `skills/lark-vc-agent/` | MIT（同上） | `packs/skills/lark-vc-agent/` | 飞书会议 VC agent；包内是 15 行转发桩，指向未随包提供的上级技能，实质不可用 |
| json-canvas | Steph Ango，`github.com/kepano/obsidian-skills` 的 `skills/json-canvas/` | MIT（`Copyright (c) 2026 Steph Ango (@kepano)`） | `packs/skills/json-canvas/` | 生成与校验 JSON Canvas 画布文件 |
| defuddle | Steph Ango，同上 `skills/defuddle/` | MIT（同上） | `packs/skills/defuddle/` | 用 defuddle CLI 把网页清洗成 markdown |
| shadcn | shadcn，`github.com/shadcn-ui/ui` 的 `skills/shadcn/` | MIT（`Copyright (c) 2023 shadcn`） | `packs/skills/shadcn/` | shadcn/ui 组件安装与定制 |
| git-commit | GitHub，`github.com/github/awesome-copilot` 的 `skills/git-commit/` | MIT（`Copyright GitHub, Inc.`） | `packs/skills/git-commit/` | 约定式提交消息与智能暂存 |
| redis-development | Redis，`github.com/redis/agent-skills` 的 `skills/redis-development/`（该技能已于 2026-05-27 被上游退役，commit `18da4e42`；本地缺 `evals/README.md` 与 `.cursor-plugin/plugin.json`） | MIT（`Copyright (c) 2026 Redis, Inc.`） | `packs/skills/redis-development/` | Redis 数据建模、查询与向量检索规范 |
| agent-browser | Vercel，`github.com/vercel-labs/agent-browser` 的 `skills/agent-browser/`（tag v0.23.0） | Apache-2.0（仓库根 `LICENSE`）；未填写具名版权人，仓库无 `NOTICE` / `AUTHORS` / `COPYING` | `packs/skills/agent-browser/` | 用 agent-browser CLI 做浏览器自动化与调试 |
| find-skills | Vercel，`github.com/vercel-labs/skills` 的 `skills/find-skills/` | MIT（`Copyright (c) 2026 Vercel, Inc.`） | `packs/skills/find-skills/` | 在 skills 生态里检索可安装的技能 |
| caveman | Julius Brussee，`github.com/juliusbrussee/caveman` 的 `skills/caveman/`（tag v2.7.0） | MIT（`Copyright (c) 2026 Julius Brussee`）；该版本 `LICENSING.md` 明确 `skills/` 归 MIT，而上游自 3.0.0 起整仓改为 Apache-2.0 | `packs/skills/caveman/` | 用极简电报式语言压缩输出 |
| gh-cli | GitHub，`github.com/github/awesome-copilot` 的 `skills/gh-cli/`（该文件已被上游移除，现存于 2026-03-09 的存档快照） | MIT（`Copyright GitHub, Inc.`） | `packs/skills/gh-cli/` | GitHub CLI 全命令参考（2187 行） |

### 登记说明

- 本地收录的第三方 skill 都是**中文化派生版**：每个 `SKILL.md` 的 `description` 由英文改写为中文，行尾统一为 CRLF。上游同族仓库（`anthropics/skills`、`cloudflare/skills`、`openai/skills`、`larksuite/cli`、`obra/superpowers` 等）均为 LF，比对时须先做行尾归一。
- **署名行丢失**：6 个来自 `anthropics/skills` 的包（`algorithmic-art`、`brand-guidelines`、`canvas-design`、`internal-comms`、`theme-factory`、`web-artifacts-builder`），上游 `LICENSE.txt` 附录写的是 `Copyright 2026 Anthropic, PBC.`，本地副本却全部退回 Apache 官方模板占位符 `[yyyy] [name of copyright owner]`。再分发时无法据此完成署名，如需合规应补回。
- 版权人栏留占位符本身是常见现象：`cloudflare/skills`、`openai/skills` 的上游 `LICENSE.txt` 同样是占位符，不构成许可缺陷；`vercel-labs/agent-skills` 与 `redis/agent-skills` 的仓库顶层没有 `LICENSE`，MIT 只写在各技能自己的 frontmatter 里。
- 本地副本多为**上游较早的快照**，几处已知差异：`cloudflare` 比上游多 21 个产品目录（本地 289 文件 / 上游 185）；`react-best-practices` 比上游少 4 条规则；`domain-modeling` 的 `CONTEXT-FORMAT.md` 对应上游 `GLOSSARY-FORMAT.md`；`wrangler`、`teach` 各被删减了一段说明。升级时应按上游 tag 对齐，不要直接取 main。
- 本轮新迁入的 36 个包归属均已比对到具体上游路径与版本（见上表）；其中 `agent-browser`、`find-skills`、`caveman`、`gh-cli` 为逐字级命中，差异只在 frontmatter 的 `description` 汉化与行尾 CRLF 两处。`caveman` 的 `README.md` 与 `SKILL.md` 内容自相矛盾（`ultra` 档是否用缩写与箭头、合法档位清单缺 `full` 与 `wenyan-*` / `off`），经核实是上游 v2.7.0 自身的问题，本地未作改动。
- 3 个包的目录名与 frontmatter `name` 不一致：`composition-patterns`（`vercel-composition-patterns`）、`react-best-practices`（`vercel-react-best-practices`）、`react-native-skills`（`vercel-react-native-skills`）。入库时保留其原目录名与 `SKILL.md` 入口名：skill 的调用名由目录名与 frontmatter 的 `name` 共同决定，改名会使包无法被宿主调用。按 [AGENTS.md](AGENTS.md) 的「二、命名与查找」，落档以成品自身的格式要求为准。
- `packs/skills/vibecoding-standards/` 不属于第三方内容，故不在上表：其 15 篇规范文档由用户本人整理，是本库自有内容，无需登记与署名。
- `packs/skills/canvas-design/` 收录的是上游包的**修改版**：本库新增 `references/rendering.md`（输出路径与字体使用说明），并把 `SKILL.md` 中一段字体指引改为优先使用包内 `canvas-fonts/`。按 Apache-2.0 第 4(b) 条，这两处改动都带显著说明——`SKILL.md` frontmatter 之后与 `references/rendering.md` 标题下各有一条 `Modified/Added by AI Fieldpack` 标注。包内随附的 81 个字体文件（54 个字重、27 个族）为 SIL OFL 1.1，各族的 `*-OFL.txt` 随文件保留。

## 待办

- `slides` 本地 `LICENSE.txt` 的 `Copyright (c) Microsoft Corporation.` 与上游同族的占位符写法不一致，来源未查清；`slides` 与 `redis-development` 两件的 `LICENSE.txt` 尚未与上游逐字节比对。
- `web-design-guidelines` 的上游没有 `LICENSE` 文件，只有 README 里的一个词 `MIT`，是否足以支撑再分发属法务判断，需要时再议。
- `gh-cli`、`slides`、`redis-development` 三件的上游已各自删除或退役该技能，本地是这些下架版本的留存，升级时无新版可对齐。
- `_sandbox/skills/` 已清空，`_sandbox/` 下仅余一个来源不明的 [AGENTS.md](_sandbox/AGENTS.md)（另一项目的模板，与本库约定无关），待确认后删除。
