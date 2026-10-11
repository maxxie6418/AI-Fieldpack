# Changelog

本文件记录 AI Fieldpack 的变更，格式与时机以本说明为准。日期倒序，最新在最上面；日期作小标题，条目用无序列表并以类型标签开头（`[Added]` `[Changed]` `[Fixed]` `[Removed]` `[Deprecated]` `[Security]`）；同类小事合并成一条，一件事一句话，单句不超过 150 字；有提交的在同一批提交的最后一条记录末尾附 `——commit: <短哈希>`，没有提交则不写；同一天有多批改动时共用一个日期小标题，条目按时间倒序连续排列；跨年后如需区分年份，日期小标题改用 `YYYYMMDD`。

结构、成果区定稿或约定本身发生变化时记一条；错别字、措辞、补链接等小修不记。

## 1011

- [Added] 成果区 `packs/skills/` 迁入余下 36 个 skill（合计 519 个文件），包内目录结构原样保留，该目录现为 52 个包，`_sandbox/skills/` 随之清空。——commit: `5f1264d`
- [Changed] 第三方收录规则由「只收录允许再分发的内容」改为默认收录：除非内容明确声明禁止再分发，否则不因许可不明拒绝收录，收录时保留其许可与版权声明文件并在登记处写明归属；`AGENTS.md`「四、收录第三方内容」与 `THIRD_PARTY_NOTICES.md` 登记规则同步。
- [Changed] `THIRD_PARTY_NOTICES.md` 登记表按上游核对结果重写：`screenshot`、`security-best-practices`、`slides` 的来源由 Anthropic 更正为 `openai/skills`，15 条补齐作者、仓库路径与许可，并记录本地为中文化派生版、6 个 Anthropic 包署名行丢失。——commit: `c014c25`
- [Added] 成果区 `packs/skills/` 新增 `frontend-skill`：单一 `SKILL.md` 的视觉设计方法（落地页、应用界面、图像、文案、动效与检验清单），184 行、无外部引用、无断链，原样收录未作改动。——commit: `5a92b9f`
- [Added] 成果区 `packs/skills/` 新增 `canvas-design`：原包只有设计理念、没有输出路径，本库新增 `references/rendering.md` 写明无头浏览器与 Pillow 两条渲染路线及字体使用规则，随包迁入 81 个 SIL OFL 字体文件，并按 Apache-2.0 第 4(b) 条标注改动。——commit: `5ffcc30`
- [Added] 成果区 `packs/skills/` 新增 `vibecoding-standards`：15 篇自有开发规范并入包内 `references/`，技能内路径由工作区绝对引用改为包内相对引用，此前指向工作区外的断链随之消除。——commit: `fb0294a`
- [Changed] 格式要求改为只约束落档前：`AGENTS.md`「二、命名与查找」新增限定段并删掉 `packs/skills/` 专项豁免，落档时以成品自身格式为准；`README.md`、`THIRD_PARTY_NOTICES.md` 与交付前自检同步。——commit: `afc136f`
- [Added] 新建成果区 `packs/skills/`，从 `_sandbox/skills/` 迁入 13 个有明示许可的 skill，保留各包原有目录结构与 `SKILL.md` 入口。
- [Added] `THIRD_PARTY_NOTICES.md` 登记这 13 个 skill 的作者、许可与本库位置，「待办」改写为 `_sandbox/` 剩余未登记内容。
- [Changed] `AGENTS.md` 的「二、命名与查找」新增唯一豁免：`packs/skills/` 保留 skill 原目录名（含 `-`）与 `SKILL.md` 入口名，改名会使包无法被宿主调用。——commit: `76c5e90`
- [Changed] 记录格式调整：同一天的多批改动合并到同一个日期小标题下，条目按时间倒序连续排列，不再按批次重复小标题。——commit: `3b4aa9b`
- [Added] 建立一级目录骨架 `_drafts/`、`_lab/`、`_archive/`、`handbook/`、`examples/`、`packs/`、`assets/`，空目录用 `.gitkeep` 占位；新增 `_drafts/todolist.md`。
- [Changed] SOP 采集阶段的状态分组改为待讨论、讨论中、已展开、已搁置、已关闭；`todolist.md` 作为分组容器不写状态标记；`README.md` 结构总览补 `.gitattributes`。——commit: `66282e2`
- [Changed] `AGENTS.md` 的 SOP 构思阶段补充：讨论稿开始衍生其他文档或需携带附属资源时升级为同名文件夹并建齐文档；确定执行后整体移入 `_lab/`，原验证阶段重复的一句删除。——commit: `c4e5316`
- [Changed] `AGENTS.md` 的「项目 SOP」补写五阶段正文：采集（状态分组、只移动不删除）、构思（讨论稿收全并原样保留）、验证、定稿、维护，后两阶段暂留待定。
- [Changed] 删掉「一、放哪，何时搬」里被 SOP 取代的四步走法，状态标记由英文五态改为指向 SOP 的中文分组；`README.md` 同步。——commit: `24dfeec`
- [Changed] `AGENTS.md` 新增第 8 条「联动更新自行完成」，原第 8 条顺延为第 9 条，交付前自检同步加一条。
- [Added] 新增 `.gitattributes`，仓库内文本文件行尾统一为 LF。
- [Changed] `README.md` 的「怎么用」补齐项目 SOP 与项目经验两节；`THIRD_PARTY_NOTICES.md` 失效的章节引用改为按小节名引用。——commit: `b89e15f`
- [Added] 收录 `.gitignore`、`LICENSE`（MIT）、`THIRD_PARTY_NOTICES.md`，仓库骨架文件至此全部入库。
- [Changed] `AGENTS.md` 人工修订：规则 2、3、4、6 的措辞调整，新增「六、项目经验」章节。——commit: `6c3293c`

## 1010

- [Changed] `AGENTS.md` 硬性规则新增第 5 条「隐私与密钥严禁入库」，交付前自检与 `README.md` 约定概览同步更新。——commit: `dbe4a16`
- [Changed] 重写 `AGENTS.md`：合并 `_todo/` 与 `_drafts/` 为 `_drafts/`，硬性规则扩至 7 条（含完成即提交、不碰他人改动、不确定先问），新增「项目 SOP」占位章节。
- [Changed] 文件名分隔符由 `-` 统一改为 `_`；`README.md` 同步更新工作区说明、结构总览与「怎么用」。——commit: `726fa20`
- [Added] 建立仓库骨架文档：`AGENTS.md`、`LICENSE`（MIT）、`CHANGELOG.md`（含记录格式）、`THIRD_PARTY_NOTICES.md`、`.gitignore`。
- [Changed] 将 `_sandbox/` 定义为临时收件箱，并在 `AGENTS.md` 中补充分流规则与执行清单。
- [Added] `README.md` 新增「项目库介绍」一节，说明三个分区与六类可复用资产。
- [Added] 建立仓库，创建 `README.md`，写明项目目的与目录结构。——commit: `df4b441`
