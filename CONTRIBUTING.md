# Contributing to Cinematic Director Skill

Thanks for considering a contribution. This skill is meant to grow horizontally — more director-style lenses, more AI video tool adapters, more output modes — without changing the shape of the main pipeline. This guide shows how to add each kind of contribution and what to check before opening a PR.

> [中文版本](#中文)

---

## What this skill is (and is not)

This is a **prompt skill**, not application code. The deliverables are markdown files that a Claude-family agent loads at runtime. There is no build step, no test runner in the traditional sense — the `evals/evals.json` file is the unit-of-behavior contract.

Goals:

- Keep `SKILL.md` as a single coherent pipeline. New capability should slot in as a new step, mode, style, or adapter — not as a parallel skill.
- Keep style modules **descriptive of methods**, not derivative of specific films. The copyright safety rule is non-negotiable.
- Keep additions cheap: a new director should be one file plus three small registrations; a new tool adapter should be one block in one file.

## Project layout

```text
SKILL.md                              # Main pipeline (10 steps, 6 modes)
references/
  cinematic-language.md               # Shot vocab the pipeline references
  ai-video-tool-adapters.md           # Tool-specific prompt shapes
  continuity-bible.md                 # Cross-shot continuity tracking
  director_styles/                    # Style overlays (one file per director)
    README.md                         # Style index (table + how-to)
    NN_<slug>.md                      # Each director
    example_comparisons.md            # Same scene × multiple directors
assets/
  shot-plan-template.md
  keyframe-prompt-template.md
  video-prompt-template.md
  qc-checklist.md
evals/
  evals.json                          # Behavior contract
```

## How to add a new director-style overlay

A "director style" is a reusable lens — narrative tendencies, camera grammar, lighting, editing, sound, performance — applied at Step 3 of the main pipeline.

1. **Create the file.** Add `references/director_styles/NN_<slug>.md` with the next available `NN` prefix. Match the existing 9-section structure:

   ```markdown
   ---
   name: <slug>
   title: <Director> 导演风格 Skill
   description: <one line; mention "Do not copy specific shots, lines, characters, or copyrighted expression">
   ---

   # <title>

   ## 适用场景
   ## 核心风格关键词
   ## 叙事方法
   ## 镜头语言
   ## 灯光与色彩
   ## 剪辑节奏
   ## 声音与音乐
   ## 人物与表演
   ## 可迁移拍摄清单
   ## 提示词模板
   ```

2. **Register the style** in three places:

   - `references/director_styles/README.md` — add a row to the table.
   - `SKILL.md` frontmatter `description:` — append the director name to the parenthetical list.
   - `SKILL.md` YAML schema `director_style:` enum — append `| <slug>`.
   - `SKILL.md` Step 3 "Available styles:" line — append `<slug>`.
   - `SKILL.md` "When to activate this skill" bullet — append the director's name.
   - Top-level `README.md` — add a row to both the EN and 中文 director tables, and add the file to the repo-structure tree.

3. **Add an eval case** in `evals/evals.json` that verifies the overlay actually changes camera / color / pacing / sound defaults vs. the unstyled baseline, plus a copyright-safety assertion.

4. **Run CI locally if you can** (`npx markdownlint-cli2 "**/*.md"` and `lychee --offline "**/*.md"`), or just push and let GitHub Actions check.

### Copyright safety

Style modules describe **high-level methods only**. Do not include:

- Specific shot descriptions from real films (e.g. "the corridor scene in The Shining")
- Character names, lines of dialogue, or plot beats from real films
- Imagery so specific to one film that it's a paraphrase rather than a method

If a sentence wouldn't apply equally to several films in the director's body of work, it's probably too specific.

## How to add a new AI video tool adapter

Each adapter lives as a block in `references/ai-video-tool-adapters.md`. Append a new section:

```markdown
## <Tool>-style adapter

Best for: <2-3 capabilities the tool actually controls well>.

Prompt priorities:
1. <thing the model leans on most>
2. ...

Template:
\`\`\`text
<minimal prompt skeleton>
\`\`\`

<Any tool-specific rules: dialogue syntax, character binding, language preference, max duration, etc.>
```

The main pipeline picks the adapter automatically when the user names a target tool. No changes needed in `SKILL.md` for the common case.

If the tool has a feature that affects the pipeline globally (e.g. "supports 60-second single-shot generation, so prefer fewer/longer shots"), add a one-line note in `SKILL.md` "Default assumptions" so it's visible upstream.

## How to add a new output mode

If a new mode is genuinely distinct from Modes A–F (Director Analysis / Shot Plan / Keyframe Pack / Video Motion Pack / Continuity Bible / QC & Repair):

1. Add `### Mode G — <Name>` under "Output modes" in `SKILL.md`.
2. If it needs a reusable scaffold, add a template in `assets/<name>-template.md`.
3. Add at least one eval case that triggers the new mode.

Don't add a mode that's just a stylistic variant of an existing one — adjust the existing mode instead.

## How to add an eval case

`evals/evals.json` is a flat JSON file. Each case:

```json
{
  "id": "short-kebab-case",
  "prompt": "What the user types",
  "expected_output": "Plain-English description of what a good response looks like",
  "assertions": [
    "Specific, checkable claim about the response",
    "..."
  ]
}
```

Aim for assertions that are:

- **Observable** in the output text (don't assert about hidden reasoning).
- **Specific** ("uses one dominant camera movement" beats "looks cinematic").
- **Decoupled** from each other (each one tests a different facet).

For style-overlay cases, always include a copyright-safety assertion ("does not copy specific shots / characters / dialogue from any actual X film").

## Style conventions

- **Compact prose-heavy markdown.** Bullets directly under H2 are fine; no need for blank lines around every heading/list/fence. `.markdownlint.json` is calibrated for this.
- **Language.** `SKILL.md`, top-level `README.md`, `LICENSE`, `CHANGELOG.md`, `CONTRIBUTING.md`, and `references/cinematic-language.md` / `references/ai-video-tool-adapters.md` / `references/continuity-bible.md` are English. Director style files are written in Chinese (matches existing 14). The bilingual README has full EN + 中文 mirror sections.
- **No emoji** in any file unless a contributor explicitly requests it for a specific use case.
- **No marketing language.** "Cinematic, dramatic, masterpiece" is the failure mode this whole skill argues against — don't put it in the skill's own docs.

## Pull request checklist

Before opening a PR:

- [ ] CI is green (markdownlint + links workflows)
- [ ] If adding a director: registered in all 6 places listed above + new eval case
- [ ] If adding a tool adapter: new block in `references/ai-video-tool-adapters.md`
- [ ] If changing pipeline shape: `SKILL.md` step numbering still 1..N, updated `README.md` architecture diagram, updated `CHANGELOG.md` Unreleased section
- [ ] No specific shots / dialogue / characters from real films
- [ ] Bilingual README tables stay in sync (EN and 中文 should list the same directors)

## Reporting issues

Issues live at https://github.com/wuwangzhang1216/DirectorSKILL/issues. Useful issue types:

- "The skill produces X when I expect Y" — include the prompt and the (problematic) output
- "Style overlay for director X is too generic / too derivative" — include a paragraph of what's off
- "Tool adapter for X is outdated" — link to the tool's current documentation page

---

<a id="中文"></a>

# 贡献指南（中文）

感谢你考虑贡献。本 skill 设计为横向扩展——更多导演风格镜头、更多 AI 视频工具适配器、更多输出模式——而不改变主流水线的形状。本文说明如何添加各类贡献，以及开 PR 前需要检查的事。

## 这个 skill 是什么（不是什么）

这是一个 **prompt skill**，不是应用代码。交付物是 markdown 文件，由 Claude 系列 agent 在运行时加载。没有传统意义的构建步骤或测试运行器——`evals/evals.json` 是行为契约的单位。

目标：

- 保持 `SKILL.md` 为单一一致的流水线。新能力应作为新步骤/模式/风格/适配器插入，而不是另起平行 skill。
- 保持风格模块**描述方法**，不衍生自具体电影。版权安全规则不可妥协。
- 保持添加成本低：新导演 = 一个文件加 3 处小注册；新工具适配器 = 一个文件里加一段。

## 如何添加新的导演风格模块

1. **建文件**：`references/director_styles/NN_<slug>.md`，沿用现有 9 节结构。
2. **登记**到 6 处：风格索引 README、`SKILL.md` 的 frontmatter description、YAML enum、Step 3 列表、激活触发列表，顶层 README 的 EN+中文 表和结构树。
3. **加 eval 用例**验证 overlay 切实改变了镜头/色彩/节奏/声音默认值，且包含版权安全断言。
4. **本地跑 CI** 或 push 后等 GitHub Actions 检查。

### 版权安全

风格模块只描述**高层方法**。不要包含具体镜头、角色名、台词、剧情节拍。如果一句话不能同样适用于该导演若干部作品，那它就太具体了。

## 如何添加新的 AI 视频工具适配器

在 `references/ai-video-tool-adapters.md` 追加一段 "<Tool>-style adapter"，写清擅长点、提示词优先级、模板、工具特定规则。主流水线会在用户点名该工具时自动调用，常规情况不必改 `SKILL.md`。

如果工具有影响全流水线的特性（如"支持 60 秒单镜头生成"），在 `SKILL.md` 的 "Default assumptions" 加一行说明。

## 如何添加新的输出模式

若新模式与 Mode A–F 真正不同：在 `SKILL.md` 加 `### Mode G — <Name>`；如需模板放在 `assets/`；至少加一个触发该模式的 eval 用例。不要为已有模式的风格变体新开一个模式。

## 如何添加 eval 用例

每条用例是 `{id, prompt, expected_output, assertions}`。断言要求：可在输出文本中观察、具体、相互解耦。风格 overlay 用例必须包含版权安全断言。

## 风格规范

- **紧凑散文式 markdown**：H2 下直接接 bullet 不需要空行。`.markdownlint.json` 已配套放宽。
- **语言**：`SKILL.md`、顶层 README、LICENSE、CHANGELOG、本 CONTRIBUTING、`references/cinematic-language.md` / `ai-video-tool-adapters.md` / `continuity-bible.md` 都是英文；导演风格文件保持中文（与现有 14 位一致）；顶层 README 双语镜像。
- **不用 emoji**。
- **不用营销语言**。"Cinematic / dramatic / masterpiece" 是本 skill 反对的失败模式，不要出现在 skill 自己的文档里。

## PR 检查清单

开 PR 前请确认：

- [ ] CI 全绿（markdownlint + links）
- [ ] 加导演 = 6 处都登记 + 新 eval 用例
- [ ] 加工具适配器 = `references/ai-video-tool-adapters.md` 加一段
- [ ] 改流水线形状 = `SKILL.md` 步骤编号连续、`README.md` 架构图同步、`CHANGELOG.md` Unreleased 加一行
- [ ] 没有任何具体镜头/台词/角色出现在风格模块里
- [ ] 双语 README 的导演表保持一致

## 报 issue

issue 见 https://github.com/wuwangzhang1216/DirectorSKILL/issues 。常见类型：

- "skill 输出 X 而我期待 Y"：附上 prompt 和（有问题的）输出
- "导演 X 的风格模块太泛/太抄"：写一段说明问题
- "工具 X 的适配器过时了"：附上该工具最新文档链接
