# answer-me-with-html 拆解与借鉴

> 状态：参考基线 ｜ 录入：2026-10-12 ｜ 来源：<https://github.com/QingYunA/answer-me-with-html>（v0.5.2 / MIT / Node ≥ 20）
>
> 本文只做拆解与借鉴评估，不搬运其代码与文案；下载件在临时目录，**未入库**。核实方式为源码走读（261 个文件，只读）加 CLI 实测。文中以引用块或「原话」标出的句子为逐字引用。

## 一、一句话结论

它和本项目追的是同一件事，而且已经走通：**模型只写内容，排版交给固定渲染层**。真正值得抄的不是页面长相，而是它用**契约 + 校验器**替代了「提示词约束」——组件是注册表里的对象、主题是 18 个变量、错误是带正确写法的返回值、样张同时是文档与测试。

最要紧的一条发现：我们 68 个模块「样式雷同、改一处动十处」的根因，是模块同时管了「写什么」和「长什么样」两层职责；它的 10 个组件只管「怎么画」，所以能画出任意页面而不雷同。

## 二、它是什么

一个 Agent Skill 加一份自带 CLI。模型只写一份「扩展 Markdown」的内容草稿，CLI 把它渲染成一页自包含的单文件 HTML——版面、配色、明暗、图坐标全部由 CLI 决定。

SKILL.md 第 20 行把边界写死了：

> You write only the **content draft** (extended Markdown). The `am` CLI does all layout, colours, dark mode and diagram coordinates. **Do not hand-write HTML / CSS / SVG.**

它主张的面很广（description 里要求「proactively and liberally, without being asked」：只要一页图比一屏文字更有用就该出页），判据是四条：

- ≥ 3 个相互关联的概念，且读者需要看清它们的关系；
- 有流程、协议、调用链或状态迁移（尤其带分支或多个参与方）；
- 有 ≥ 3 维的对比、方案取舍，或一张「能 / 不能」清单；
- 有层级，或随时间演化。

**它给出的量化收益**（README.zh-CN.md，统计 9 页模型手写的 HTML）：

| 手写 HTML 的组成部分 | 占比 | 用它之后 |
| --- | ---: | --- |
| SVG 图的坐标与路径 | 47% | 由 CLI 生成 |
| CSS | 15% | 由 CLI 生成 |
| HTML 标签 | 17% | 由 CLI 生成 |
| 正文文字 | 21% | 模型写，写成 Markdown |

模型要写的 token 从 4893 降到 612（约 1/8），耗时 31 秒 → 12 秒。它的对比对象是 Archify（JSON 规格 → 一张可交互图）与 dsh-genui（聊天里的组件）。

## 三、它是怎么设计的

### 3.1 产出的形态：一份能再次处理的单文件

- 流水线写在 `src/render.js` 文件头：`parse → STE lint → render panels (markdown / components / raw) → apply template → inline CSS and runtime`。
- 入口是 `renderDoc(source, overrides = {}, defaults = {}, {...}) → { html, warnings, stats, meta, language }`。
- 产物零外部依赖：CSS 全内联、图片转 data URI、公式在构建期出 MathML、无运行时网络请求。
- **页面自带重建数据**：`src/page.js:29` 的 `sourceTag(source)` 把原始草稿写进页面末尾的 `<textarea id="am-source" hidden readonly>`，`readPage()` 从 `<html>` 属性加这个 textarea 反读。所以单文件页面本身是可再处理的源，不只是渲染残渣——`am patch` 靠它做单面板原地替换。

### 3.2 输入：一份「扩展 Markdown」草稿

三层分离，没有 JSON 数据模型：

| 层 | 写法 | 变成什么 |
| --- | --- | --- |
| frontmatter | `template` / `theme` / `title` / `subtitle` / `cols` / `source` | 页面元信息；其他键显示在页头 meta 行 |
| `##` 标题 | `## A 面板标题 {span=2 meta="..."}` | 一个面板；字母 ID 可省，自动派 A、B、C… |
| fence 块 | 语言名即组件名 | 一个组件；未命中注册表的语言退化成代码块 |

它规定的写作顺序是：**先在脑子里列出 3–8 个面板，每个面板只回答一个子问题**，再按信息的形状挑组件，最后一次性渲染。

选择规则里有几条值得注意：结论先行（第一个面板或 lead 给核心答案，后面给证据）；一个面板只回答一个问题，超过 8 个面板就拆页；`span` 只是提示而不是控制，浏览器里由模板按内容自动排。

### 3.3 组件层：形状渲染器

`src/components/index.js` 全文 18 行，首注释就是契约：

> Component registry: fenced-block language name → component. Each component exports `{ name, summary, syntax, example, render(text, ctx) }`.

```js
const ALL = [callout, kv, timeline, annot, tree, limits, sequence, flow, er, ask];
export const COMPONENTS = new Map(ALL.map((c) => [c.name, c]));
export const RAW_LANGS = new Set(['html', 'svg']);
```

十个组件，每个对应一种「纯段落说不清」的信息形状：

| 组件 | 信息形状 | 关键设计 |
| --- | --- | --- |
| `callout` | 结论 / 警告 | 三种 kind 加别名（warning → warn） |
| `kv` | 元数据 / 参数表 | `cols` 列数限制在 1–6 |
| `timeline` | 先后顺序 | 不给方向时按条数自动选横竖（> 6 条转竖） |
| `annot` | 逐词注释一句话 | **把注释锚到具体片段**，错误词用 `{!...}` 标红 |
| `tree` | 层级 / 目录 / 分类 | 缩进即层级，另有 list 形态 |
| `limits` | 当前值 vs 允许值 | `niceScale(peak)` 自动取整齐刻度 |
| `sequence` | 多方往返时序 | 参与者 + 箭头 + `== 阶段 ==` 分隔 |
| `flow` | 任意拓扑流程 | dagre 算坐标，**作者只写关系** |
| `er` | 数据模型与基数 | 实体 + 缩进字段 + PK / FK / UK |
| `ask` | 需要用户先决定 | 唯一可出现在页面上并回传答复的组件 |

三条比组件本身更要紧的结构性设计：

- **未知语言零成本退化**：`renderFence` 命中 COMPONENTS 才调 `comp.render(...)`，否则整块当代码块走 `src/code.js`。
- **错误带正确写法**：`ComponentError(message, line = 0)` 经 `renderFence` 换算成源文件行，再由 `RenderError` 补上组件名与 `example`。
- **组件可自带能力位**：`ask.js` 是唯一带 `lint()` 钩子的组件（把选项行改写成 Markdown 列表再交给写作检查），并用 `pageOnly / panelOnly` 声明自己只能出现在哪。

另外 `src/delta.js` 不是组件，而是 flow / tree / er 共享的变更基础设施：`SIGN = { added:'+', removed:'−', changed:'~' }`（removed 用真正的减号 U+2212），标记符后必须跟空格，所以 `-Gateway` 不会被误判成删除。

### 3.4 主题层：变量契约

- 一套主题 = 注册表字段 + 变量 + 装饰 CSS。`src/themes/registry.js` 首注释原样：`the only place the rest of the code learns which themes exist.`
- `src/themes/check.js` 冻结 **18 个颜色变量**，注释写明「Every color a component reads. Light and dark must each set all of them.」：

  `--bg`、`--paper`、`--ink`、`--ink-2`、`--ink-3`、`--line`、`--line-2`、`--fill`、`--accent`、`--accent-bg`、`--ok`、`--ok-bg`、`--err`、`--err-bg`、`--warn`、`--warn-bg`、`--head-bg`、`--head-fg`

- 切换只改一个属性：`src/themes/index.js` 把令牌编译成 `html[data-theme="<name>"]` 下的 CSS 变量；暗色再追加 `@media (prefers-color-scheme: dark)` 供 auto 模式使用。
- `base.css`（498 行）首行声明：只用主题变量、绝不写死颜色——并注明由测试守住；装饰 CSS 的每个选择器必须以 `&` 开头，由 `scoped()` 换成该主题的根选择器。
- **自动选主题极简**：`pickTheme({ scope, template, visuals })` 全文三行——video 恒 blueprint；`template === 'doc' || !visuals ? 'paper' : 'blueprint'`。`visuals` 的判定是「有任一块是 fence 且属于组件或 raw 语言」。
- **auto 在渲染期被固化成具体名字**，注释给出的理由是：这样页面、摘要与后续 patch 都能说出用的是哪个主题。
- **体检**：`checkColors` 检查正文对 ≥ 4.5:1、徽标对 ≥ 3:1（徽标落在 3–4.5 只告警不拦截），消息形如 `light: --ink on --paper has contrast 3.21:1, needs 4.5:1`；用户主题坏文件只跳过并报告，`never stops a render that uses another theme`。
- **按需注入**：`pageCss(list, { diff, delta, rtl, math, update })` 只在页面真用到时才拼对应 CSS（注释给出的量级：数学样式约 20 KB）。

### 3.5 版式层：由代码算

- 三种模板：`sheet`（多面板网格，默认，一屏概览）、`doc`（单栏长文，按步阅读）、`video`。
- `span` 只是提示：`sheet.js` 的 `minSpan(panel)` 按表格列数（4 列以上算宽表，每 2 列抬一档）与 SVG 宽度（每档 560px）自动抬升，`fillRows` 再补满行尾空隙。
- `src/runtime/layout-plan.js` 是纯函数、无 DOM、**必须可内联**：`planLayout({ width, gap, cols, panels }) → { rows, maxScale }`，用动态规划决定断行，按 `STEP = 10` 搜列宽，代价是 `cost = waste/1000 + PREF_WEIGHT * dev * H`。
- **缩放带是它真正的巧思**：同页图表的缩放被限制在 `BAND_RATIO = 1.25` 的带内（`MAX_SCALE = 1.25`、`MIN_SCALE = 0.75`）。注释原样：`The band starts no higher than the largest scale the page allows the least roomy diagram, so one wide diagram lowers the band for the others.`
- `layout-dom.js` 兜底三层次：`justify()` 最多 3 pass 直到容器宽度稳定 → 仍不稳就 `restore()` 回退朴素 CSS grid → 整段 try/catch 再回退；外加「无 JS / 打印 / 窄屏一律用 grid」。

### 3.6 检查层：受控写作

- 是 ASD-STE100 风格的受控语言检查，写在 `src/render.js` 第 7 步、在渲染面板之前运行。
- 阈值：`LIMITS = { zh: { procedural: 35, descriptive: 45 }, en: { procedural: 20, descriptive: 25 } }`，段长上限 6 句。
- 中文三张词表，来源注释原样：`the part of the Simplified Technical Chinese word list … that is almost never wrong`——**只收几乎不会错的条目，拿不准的语境界定项一律不收**。
- 强度三档：`off` / `80`（默认，只告警）/ `strict`（有告警就不出页）。
- 两个聪明的开关：表格里状态是 `no` 或 `✗` 的行整行跳过（允许写反例）；组件可通过注册表提供自己的检查文本。
- 它自己承认的边界：全是正则与长度阈值，不做句法分析，是「提示器」而不是「判卷器」。

### 3.7 出错时怎么办

报错格式本身是设计的一部分（SKILL.md 第 2 节）：

- `✓ <path>`：成功。
- `✗ L<line> [component] …` 加 `Correct example:`：按示例改那一行再渲染（此时不写页面）。
- `STE n warnings` / `code n warnings`：按要求重写；**重试上限 2 轮**，仍有警告就保留最后一版并说明。
- 每次在 `✓` 之后重渲染必须加 `--replace <上次的路径>`，CLI 会删掉旧页——**一问一页**。

### 3.8 分发与自我维护

- 分发形态：一个 skill 目录 = SKILL.md + `scripts/am.mjs`（799976 字节的单文件，无依赖安装，只要 Node 20+）。
- **样张即文档即测试**：`site/presets/` 的 18 份 md（6 个场景页 + 12 个组件最小示例）同时充当组件语法文档、官网画廊、首页演示素材、回归测试输入、主题对比素材；`site/build.mjs` 的 `copyPresets` 用 5 行代码把它们打包成 `presets/index.json`，页面一次 fetch 全取。
- **playground**：左编辑器右预览，`setTimeout(…, 120)` 防抖加序号丢弃过期结果；预览用 `srcdoc` 沙箱 iframe 且双 iframe 轮换避免闪白；「Break it」按钮**按模型最常见的错法改一行**（` -> ` 换成 ` => `、去掉 `|`、去掉 `:`），错误展示是三元组：位置（行号 + 组件名）、消息、正确写法高亮。
- 浏览器跑同一套引擎（`site/src/engine.js` 直接 import `src/`），只对预期错误类做转换；构建产物扫描禁词（`require(`、`process.`、`Buffer`、`node:`），命中即失败。

## 四、我们遇到的问题，它怎么解

| 我们的问题 | 它的解法 | 证据位置 |
| --- | --- | --- |
| 不同 AI 输出视觉漂移 | 把版面、配色、明暗、图坐标从模型手里收走，只留内容 | SKILL.md 第 20 行；渲染链路全在 CLI |
| 68 个模块样式雷同（只用了四种容器） | 组件只有 10 个，但每个是**形状渲染器**；内容与呈现分层 | `src/components/index.js` |
| 样例被当成范例，做得很浅 | 样张即文档即测试：每份都是能直接渲染的最小可用示例，且被测试天天跑 | `site/presets/`、`site/build.mjs` |
| 162K 单文件改一处要重写全文 | 页面末尾内嵌 `<textarea id="am-source">`，`am patch --panel` 原地替换单个面板 | `src/page.js:29`、`readPage()` |
| 换主题要改一大堆地方 | 18 个颜色变量契约 + 组件只读变量 + 自动体检对比度 | `COLOR_TOKENS`、`checkColors` |
| 模型写错语法就整页崩 | 错误是返回值，带行号、组件名与正确写法；未知语言退化成代码块 | `ComponentError` → `RenderError` |
| 内容说废话、句子太长 | STE 受控写作，阈值分「步骤 / 描述」两类，三档强度 | `src/lint/ste.js` |
| 规格写在提示词里执行不下去 | 把规格变成**契约 + 校验器**：注册表、变量清单、阈值、体检命令 | 全篇；`am theme check` 会生成含全部组件的样张 |
| 一次渲染容易反复重来 | 明确的重试上限（2 轮）与「一问一页」的 `--replace` 语义 | SKILL.md 第 2 节 |

## 五、可借鉴清单

### 第一档：不依赖架构决定，现在就能用

1. **错误信息必须带正确写法**。我们的骨架校验现在只报「通过 / 未通过」，应改成带行号、组件名与一条正确示例。
2. **让模块能声明自己的必填项**。每个模块声明「我必须有哪些字段、最少几条」，由统一检查器查——这正是 14.1 规格卡要的硬下限，只是从文档搬进了代码。
3. **样张即文档即测试**。每个模块的样例改成能直接渲染的最小可用示例，并让它同时充当回归样例。
4. **受控写作的词表与阈值**。中文三张表可直接取用；「只收几乎不会错的条目」这条取舍跟着搬；阈值必须按块类型放宽（它自己的 45 字对速查手册偏紧）。
5. **auto 必须固化**。任何「自动选择」都要在生成期解析成具体值写进产物，否则后续无法复现。

### 第二档：要先定「排版交给谁」

6. **组件注册表契约**：`{ name, summary, syntax, example, render }` 加一张 Map。加模块 = 加文件加注册，解析与渲染零改动。
7. **主题 = 18 个颜色变量**，亮暗各写全，组件只读变量；配一个体检命令。
8. **按信息形状选组件**：一张「形状 → 渲染器 → 最小语法」表。我们的「属性触发」可以照这个形式改写。
9. **版面由代码算**（若走渲染器路线）。但只取两个子想法：同页同类图尺寸差 ≤ 1.25 倍；宽表宽图自动占满一行。
10. **稳健性三层兜底**：宁可退回朴素版式，也不能出白页。

### 第三档：长期

11. **按需注入 CSS**：只有含公式的页面才带数学样式。
12. **playground 与「Break it」**：一个能用最常见错法一键搞坏样例的试验台，比读规范更快暴露规则缺口。

## 六、不可借鉴清单

| 不采纳 | 原因 |
| --- | --- |
| 作者用 `span / rows / cols` 控制版面 | 会诱使内容作者纠结排版。手册应把定位权收归模板 |
| 整套 justified 布局（约 410 行 + 「必须可内联」的架构约束 + 两组测试） | 优化目标是「一屏塞满」，与分章节、可打印、可检索的手册不是一回事 |
| video 模板 | 服务逐场景动画；手册不需要 |
| ask / Reply / 批注回帖闭环 | 服务「模型在对话里审草稿」的循环。手册一次成稿、读者只读不回 |
| `am patch` 的页面内嵌源加原地打补丁 | 若手册用版本控制加重新生成管更新，这层复杂度可整段省掉。**但也要承认：它是目前唯一现成的「162K 单文件改一处」方案，取舍未定** |
| 用户自定义主题那一整套（JSON + 校验 + 对比度体检流程） | 前提是有一批人会写主题；我们要的是固定的五套槽位。但 18 个变量的清单要留下 |
| 它的写作阈值原样照搬 | 步骤 20 词 / 35 字、描述 25 词 / 45 字，对速查手册偏紧；术语定义、来源说明、案例叙述的合理句长并不相同 |
| 双语成对文件 | 服务它的官网中英双语；但可以保留「缺键即构建失败」这条硬约束 |

## 七、它留下的未决问题

1. **排版交给谁**：纯 skill + 模板（轻，但版面仍靠模型填——营养学样本 221 处 inline style 就是这么来的）对比 skill + 渲染器（稳定，代价是维护代码）。它用实测把票投给后者，但这个结论建立在「一问一页、篇幅短」的前提上；我们的手册是 18–21 节的长文，前提不同，需要自己判断。
2. **它不做知识分型**：模板只有 sheet / doc / video 三种，没有「按知识类型换骨架」这一层，得靠我们自己。
3. **它的规模假设不同**：3–8 个面板、一屏概览；我们的骨架是 18–21 节、要长期回查。它那套自适应版式主要解决「一屏塞满」，不是「长文可导航」。
4. **它的组件偏工程结构**：flow / er / sequence 服务于代码与系统说明；我们需要的术语卡、自测题库、常见误区、共识与争议，它一个都没有。
