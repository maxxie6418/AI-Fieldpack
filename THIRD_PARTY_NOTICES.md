# THIRD_PARTY_NOTICES

本文件登记仓库内收录的第三方内容及其许可，供合规核查与溯源。

## 登记规则

- 只收录允许再分发的内容；许可不明时只放链接与说明，不复制原始文件。
- 每条登记五项：名称、作者 / 来源 URL、许可类型、在本库中的位置、用途说明。
- 从 `_sandbox/` 分流进来的第三方内容，完成登记后才能进入成果区。
- 完整规则见 [AGENTS.md](AGENTS.md) 的「收录第三方内容」一节。

## 登记表

| 名称 | 作者 / 来源 | 许可 | 本库位置 | 用途说明 |
| ---- | ----------- | ---- | -------- | -------- |
| algorithmic-art | 包内未署名；内容指向 Anthropic 品牌体系，上游 URL 未能联网核实 | Apache-2.0（见包内 `LICENSE.txt`；版权人栏仍为 `[yyyy] [name of copyright owner]` 占位） | `packs/skills/algorithmic-art/` | p5.js 算法艺术创作，随机种子可复现 |
| brand-guidelines | 包内未署名；内容指向 Anthropic 品牌体系，上游 URL 未能联网核实 | Apache-2.0（同上，版权人栏为占位） | `packs/skills/brand-guidelines/` | 将 Anthropic 品牌色与字体排版应用到产物上 |
| internal-comms | 包内未署名；上游 URL 未能联网核实 | Apache-2.0（同上，版权人栏为占位） | `packs/skills/internal-comms/` | 撰写内部沟通材料（3P 更新、简报、FAQ） |
| screenshot | 包内未署名；上游 URL 未能联网核实 | Apache-2.0（同上，版权人栏为占位） | `packs/skills/screenshot/` | macOS / Windows 系统级桌面与窗口截图 |
| security-best-practices | 包内未署名；上游 URL 未能联网核实 | Apache-2.0（同上，版权人栏为占位） | `packs/skills/security-best-practices/` | 按语言与框架做安全审查（Python / JS-TS / Go） |
| slides | 包内未署名；上游 URL 未能联网核实 | Apache-2.0（见包内 `LICENSE.txt`，版权人栏为 `Copyright (c) Microsoft Corporation.`） | `packs/skills/slides/` | 用 PptxGenJS 生成 pptx 并渲染校验 |
| theme-factory | 包内未署名；上游 URL 未能联网核实 | Apache-2.0（同上，版权人栏为占位） | `packs/skills/theme-factory/` | 为作品套用十套预设主题 |
| web-artifacts-builder | 包内未署名；上游 URL 未能联网核实 | Apache-2.0（同上，版权人栏为占位） | `packs/skills/web-artifacts-builder/` | 构建并打包 React + Tailwind + shadcn 的 HTML 作品 |
| composition-patterns | vercel（frontmatter `author: vercel`） | MIT（frontmatter `license: MIT`，包内无 LICENSE 文件） | `packs/skills/composition-patterns/` | React 组合模式与 API 设计规范 |
| git-commit | 包内未署名 | MIT（frontmatter `license: MIT`，包内无 LICENSE 文件） | `packs/skills/git-commit/` | 约定式提交消息与智能暂存 |
| react-best-practices | vercel（frontmatter `author: vercel`） | MIT（同上，包内无 LICENSE 文件） | `packs/skills/react-best-practices/` | React / Next.js 性能规则库（66 条） |
| react-native-skills | vercel（frontmatter `author: vercel`） | MIT（同上，包内无 LICENSE 文件） | `packs/skills/react-native-skills/` | React Native / Expo 性能与 UI 规范 |
| redis-development | redis（frontmatter `author: redis`；metadata 记为「Redis, Inc.」） | MIT（同上，包内无 LICENSE 文件） | `packs/skills/redis-development/` | Redis 数据建模、查询与向量检索规范 |

### 登记说明

- 上表的许可结论来自包内 `LICENSE.txt` 或 `SKILL.md` frontmatter 的自我声明，未与上游仓库核对：本会话 `web_fetch` 对所有域名均返回 `resolves to a non-public IP address`，`web_search` 又缺少 API Key，无法联网核验。若日后能访问上游，应补记作者与来源 URL。
- 8 个 Apache-2.0 包中，7 个的 `LICENSE.txt` 版权人栏仍是 Apache 官方模板占位符 `[yyyy] [name of copyright owner]`，署名信息不完整；仅 `slides` 已填写。这不影响 Apache-2.0 的授权本身，但再分发时的署名义务无法据此完成。
- 3 个包的目录名与 frontmatter `name` 不一致：`composition-patterns`（`vercel-composition-patterns`）、`react-best-practices`（`vercel-react-best-practices`）、`react-native-skills`（`vercel-react-native-skills`）。为避免破坏宿主调用名，入库时保留原目录名，见 [AGENTS.md](AGENTS.md) 的「二、命名与查找」。

## 待办

- `_sandbox/skills/` 余 39 个 skill 尚未登记：其中 37 个无任何许可声明、2 个有 Apache-2.0 但存在质量缺口（`canvas-design`、`frontend-skill`）。完成登记或清理前，不要并入成果区。
- `_sandbox/manual/` 下的 15 篇 `*-mimo.md` 拷贝尚未登记。
