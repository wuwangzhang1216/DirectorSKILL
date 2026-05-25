# Cinematic Director Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Claude Skill](https://img.shields.io/badge/Claude_Skill-cinematic--director-blue)
![Version](https://img.shields.io/badge/version-1.1.0-green)
[![markdownlint](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/markdownlint.yml/badge.svg)](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/markdownlint.yml)
[![links](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/links.yml/badge.svg)](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/links.yml)

A Claude Code / Claude Agent skill that turns a script, prose, or a single keyframe into a complete cinematic production plan — beats, director's book, blocking, shot list, keyframe prompts, AI video motion prompts, tool-specific adapters, and a QC repair loop. Optionally apply one of ten director-style overlays (Spielberg, Hitchcock, Kubrick, Kurosawa, Scorsese, Fellini, Bergman, Tarkovsky, Wong Kar-wai, Nolan) as a coherent lens over the entire workflow.

> [中文版本](#中文版本)

---

## Why this exists

Most "cinematic" AI prompts are adjective soup — *cinematic, dramatic, masterpiece, 8K*. They don't tell a model where to put the camera, what the subject is doing, where the action ends, or which continuity anchors to keep. The result is the slideshow look: pretty stills that drift between shots.

This skill replaces adjective soup with **directorial reasoning**:

- **A shot is a story decision**, not a style descriptor.
- **Blocking comes before framing.** Camera placement follows what bodies do in space.
- **Continuity is engineered**, not hoped for — characters, locations, lighting, and props are tracked across shots.
- **Tool adapters** convert generic direction into the prompt shape each model (Runway, Veo, Kling, Luma, 即梦/Dreamina/Seedance, Wanxiang) actually controls.
- **Style is a lens**, not a costume. Picking "Kubrick" means the whole pass favors symmetry, cold formalism, and reaction-after-revelation — not just "add zooms."

## Features

- 10-step pipeline from raw idea to executable AI video prompts
- 6 output modes: Director Analysis · Shot Plan · Keyframe Prompt Pack · Video Motion Prompt Pack · Continuity Bible · QC & Repair
- 10 director-style overlays with consistent section structure for easy switching and extension
- Tool adapters for the most common AI video models, including bilingual (EN/中文) templates for 即梦/Dreamina/Seedance
- A diagnostic QC loop for "slideshow," face-change, missing-endpoint, and camera-logic failures
- Templates for shot lists, keyframes, video prompts, and a continuity bible

## Architecture

```text
┌─────────────────────────────────────────────────────────────────┐
│  SKILL.md  (main pipeline)                                      │
│                                                                 │
│   1. Script & subtext breakdown                                 │
│   2. Beat map                                                   │
│   3. Director style selection  ◄── loads one file from          │
│   4. Director's book               references/director_styles/  │
│   5. Blocking & staging                                         │
│   6. Shot list                                                  │
│   7. Keyframe strategy                                          │
│   8. AI video prompt construction                               │
│   9. Tool adapter selection    ◄── reads                        │
│  10. QC & repair                   references/ai-video-         │
│                                    tool-adapters.md             │
└─────────────────────────────────────────────────────────────────┘

       ▲                                       ▲
       │ references / assets / evals           │ uses templates
       │                                       │
┌──────┴──────────────┐              ┌─────────┴────────────────┐
│  references/        │              │  assets/                 │
│    cinematic-       │              │    shot-plan-template    │
│    language.md      │              │    keyframe-template     │
│    ai-video-tool-   │              │    video-prompt-template │
│    adapters.md      │              │    qc-checklist          │
│    continuity-      │              └──────────────────────────┘
│    bible.md         │
│    director_styles/ │ ← 10 style modules + index
└─────────────────────┘
```

**One skill, optional style overlay.** The main `SKILL.md` is always the entry point. When the user names a director, Step 3 loads that single style file as a coherent lens that overrides defaults at Steps 4, 6, and 8. Style files are reference modules — they are *not* separately registered skills, so the host agent never has to disambiguate.

## Installation

Skill files live in `~/.claude/skills/<skill-name>/` (user-level) or `.claude/skills/<skill-name>/` (project-level). The folder name must match the `name:` field in `SKILL.md` (`cinematic-director`).

```bash
# User-level (available across all projects)
git clone https://github.com/wuwangzhang1216/DirectorSKILL.git \
  ~/.claude/skills/cinematic-director

# Project-level (this project only)
git clone https://github.com/wuwangzhang1216/DirectorSKILL.git \
  .claude/skills/cinematic-director
```

Reload Claude Code (or your host agent) and the skill becomes available. Trigger it with any of the prompts below.

## Quick start

### Plain directorial pass

```text
You: Turn this into a 4-shot AI video plan for Runway, 16:9.
     "A courier hesitates outside a Republican-era Shanghai apartment door
      before knocking, then slips an envelope under it and walks away."
```

The skill will produce: beat map → director's book → shot list (with story function, shot size, camera, blocking, continuity anchors per shot) → Runway-shaped video prompts → QC notes.

### With a director-style overlay

```text
You: Same scene, but direct it in the style of Wong Kar-wai.
```

The skill loads `references/director_styles/09_wong_kar_wai.md` and overrides defaults: handheld in narrow corridors, neon practicals, frame-within-frame through doorways, slow-motion on the slip-and-leave, optional voice-over from the courier, soundtrack as emotional anchor. Same 4 shots, very different lens.

### Repairing a failed clip

```text
You: My generation looks like a slideshow — character barely moves, rain is
     frozen. Diagnose and rewrite this prompt: [paste prompt]
```

The skill runs the QC diagnostic order (asset mismatch → prompt overload → weak action → missing endpoint → bad camera logic → continuity gap → tool mismatch), names the most likely cause, and outputs a revised prompt with explicit subject motion, environmental reaction, and a clear end state.

## Director style overlays

| # | Director | Lens in one line |
|---|---|---|
| 01 | Steven Spielberg 斯皮尔伯格 | Emotional mainstream narrative, family stakes, awe via reaction-before-reveal |
| 02 | Alfred Hitchcock 希区柯克 | Suspense via shared knowledge, voyeurism, mistaken identity |
| 03 | Stanley Kubrick 库布里克 | Symmetry, one-point perspective, cold formalism, philosophical allegory |
| 04 | Akira Kurosawa 黑泽明 | Epic ensemble, humanism, weather as drama, dynamic action space |
| 05 | Martin Scorsese 斯科塞斯 | Urban energy, guilt, voice-over, kinetic camera, moral fall |
| 06 | Federico Fellini 费里尼 | Dream logic, circus parade, autobiographical fantasy |
| 07 | Ingmar Bergman 伯格曼 | Interior psychological drama, face close-ups, existential silence |
| 08 | Andrei Tarkovsky 塔可夫斯基 | Poetic time, long takes, water and fire, spiritual search |
| 09 | Wong Kar-wai 王家卫 | Urban loneliness, missed connections, neon, fragmented memory |
| 10 | Christopher Nolan 诺兰 | High-concept structure, time puzzles, IMAX-scale practical spectacle |
| 11 | Denis Villeneuve 维伦纽瓦 | Monumental scale, mist, geometric symmetry, low-rumble silence |
| 12 | David Fincher 芬奇 | Surgical control, teal-amber palette, procedural investigation, restrained dread |
| 13 | Nicolas Winding Refn 雷弗恩 | Neon color blocks, symmetric ritual framing, slow gaze, sudden violence |
| 14 | Bi Gan 毕赣 | Misty SW-China small towns, single ultra-long take, dream-memory loops, poetic voice-over |

Each style file follows the same 9-section structure (适用场景 / 核心风格关键词 / 叙事方法 / 镜头语言 / 灯光与色彩 / 剪辑节奏 / 声音与音乐 / 人物与表演 / 可迁移拍摄清单 / 提示词模板), so adding an 11th director is a single new file plus one row in `references/director_styles/README.md`.

## AI video tool adapters

The main pipeline writes directorial intent. Step 9 reshapes it for the target model. Adapters currently included:

| Tool | Strength used by adapter |
|---|---|
| Runway | Image-to-video motion, scene motion, camera motion, style descriptors |
| Veo | Visual style + sound + timestamped multi-shot + first/last-frame |
| Kling | Physical action, expressive performance, longer single-shot progression |
| Luma | Keyframes, character references, camera tags, loop/extend |
| 即梦 / Dreamina / Seedance | Bilingual prompts, first/last-frame, smooth motion, concise EN/中文 templates |
| Wanxiang 万相 | Text-to-video, image-to-video, multi-shot timestamps |

Add a new tool by appending an "X-style adapter" block to `references/ai-video-tool-adapters.md` with prompt priorities, a template, and any constraints — no other file changes needed.

## Output modes

The skill picks the right output shape based on the request. Modes can be combined.

- **Mode A — Director Analysis** · dramatic core, subtext, emotional arc, visual thesis, direction rules
- **Mode B — Shot Plan** · table per `assets/shot-plan-template.md`
- **Mode C — Keyframe Prompt Pack** · per `assets/keyframe-prompt-template.md`
- **Mode D — Video Motion Prompt Pack** · per `assets/video-prompt-template.md`
- **Mode E — Continuity Bible** · per `references/continuity-bible.md`
- **Mode F — QC & Repair** · per `assets/qc-checklist.md`

## Repository structure

```text
cinematic-director/
├── SKILL.md                              # Main pipeline (10 steps, 6 output modes)
├── README.md                             # This file
├── LICENSE                               # MIT
├── .gitignore
├── references/
│   ├── cinematic-language.md             # Shot functions, sizes, angles, movement, lighting, composition, editing
│   ├── ai-video-tool-adapters.md         # Runway / Veo / Kling / Luma / 即梦 / Wanxiang adapters
│   ├── continuity-bible.md               # Character / location / prop tracking
│   └── director_styles/                  # Director-style overlays
│       ├── README.md                     # Style index + how-to-add-new
│       ├── 01_spielberg.md
│       ├── 02_hitchcock.md
│       ├── 03_kubrick.md
│       ├── 04_kurosawa.md
│       ├── 05_scorsese.md
│       ├── 06_fellini.md
│       ├── 07_bergman.md
│       ├── 08_tarkovsky.md
│       ├── 09_wong_kar_wai.md
│       ├── 10_nolan.md
│       ├── 11_villeneuve.md
│       ├── 12_fincher.md
│       ├── 13_refn.md
│       └── 14_bi_gan.md
├── assets/                               # Reusable templates the skill fills in
│   ├── shot-plan-template.md
│   ├── keyframe-prompt-template.md
│   ├── video-prompt-template.md
│   └── qc-checklist.md
└── evals/
    └── evals.json                        # Eval cases for the main pipeline
```

## Extending

- **Add a director**: drop `references/director_styles/NN_<slug>.md` using the existing 9-section template, then add a row to the styles README and a name to the `director_style` enum in `SKILL.md`.
- **Add an AI video tool**: append an adapter block to `references/ai-video-tool-adapters.md`. The main pipeline auto-references the file at Step 9.
- **Add an output mode**: extend `SKILL.md` "Output modes" section and (optionally) drop a template in `assets/`.
- **Add an eval**: append a case to `evals/evals.json`.

## Usage rule and disclaimer

The director-style modules describe **high-level methods** — narrative tendencies, camera grammar, lighting logic, editing rhythm, sound, performance, transferable shot checklists. They are **not** licensed to copy specific shots, dialogue, characters, plots, or any other copyrighted expression from any director's actual films. Use them as lenses that inform original work.

## License

MIT — see [LICENSE](LICENSE).

The MIT grant covers the skill files (SKILL.md, references, assets, templates). The usage rule above applies to *how* you use the directorial knowledge with respect to existing films, which is a separate concern from software licensing.

---

<a id="中文版本"></a>

# Cinematic Director Skill（中文版本）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Claude Skill](https://img.shields.io/badge/Claude_Skill-cinematic--director-blue)
![Version](https://img.shields.io/badge/version-1.1.0-green)
[![markdownlint](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/markdownlint.yml/badge.svg)](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/markdownlint.yml)
[![links](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/links.yml/badge.svg)](https://github.com/wuwangzhang1216/DirectorSKILL/actions/workflows/links.yml)

一个 Claude Code / Claude Agent skill：把剧本、散文或一张关键帧，转化为完整的电影化制作方案——节拍图、导演书、走位、分镜表、关键帧提示词、AI 视频动作提示词、工具专属适配器、QC 修复流程。可选择叠加十位导演（斯皮尔伯格、希区柯克、库布里克、黑泽明、斯科塞斯、费里尼、伯格曼、塔可夫斯基、王家卫、诺兰）中任一位的风格作为整套流程的统一镜头语言。

## 为什么需要它

大多数"电影感"AI 提示词只是形容词堆砌——*cinematic、dramatic、masterpiece、8K*。它们不告诉模型镜头放哪、主体在做什么、动作终点在哪、需要保留哪些连贯性锚点。结果就是 PPT 感：每张静帧都很美，但镜头之间是漂移的。

本 skill 把形容词堆砌替换为**导演式推理**：

- **镜头是叙事决策**，不是风格描述。
- **走位先于构图**。摄影机的位置取决于身体在空间中的动作。
- **连贯性是设计出来的**，不是祈祷出来的——人物、场景、灯光、道具会被跨镜头追踪。
- **工具适配器**把通用的导演意图翻译成每个模型（Runway / Veo / Kling / Luma / 即梦 / Dreamina / Seedance / 万相）真正能控制的提示词形态。
- **风格是镜头**，不是外套。选"库布里克"意味着整套流程偏向对称、冷峻形式、揭示后的反应——不是简单地"多加几个推镜"。

## 功能

- 从原始构思到可执行 AI 视频提示词的 10 步流水线
- 6 种输出模式：导演分析 · 分镜方案 · 关键帧提示词包 · 视频动作提示词包 · 连贯性圣经 · QC 与修复
- 10 个导演风格模块，统一的小节结构，便于切换和扩展
- 主流 AI 视频模型适配器，含即梦/Dreamina/Seedance 的中英双语模板
- 针对"PPT 感"、换脸、动作终点缺失、镜头逻辑错误等失败模式的诊断 QC 流程
- 分镜表、关键帧、视频提示词、连贯性圣经的模板

## 架构

```text
┌─────────────────────────────────────────────────────────────────┐
│  SKILL.md  （主流水线）                                          │
│                                                                 │
│   1. 剧本与潜文本分析                                            │
│   2. 节拍图                                                      │
│   3. 导演风格选择     ◄── 加载                                  │
│   4. 导演书 / 视觉方案     references/director_styles/ 下的一个 │
│   5. 走位与调度                                                  │
│   6. 分镜表                                                      │
│   7. 关键帧策略                                                  │
│   8. AI 视频提示词构造                                           │
│   9. 工具适配器选择   ◄── 读                                    │
│  10. QC 与修复            references/ai-video-                  │
│                           tool-adapters.md                      │
└─────────────────────────────────────────────────────────────────┘
```

**一个 skill，可选风格叠加。** 主 `SKILL.md` 始终是入口。当用户点名某位导演时，Step 3 加载对应的风格文件作为一组统一的镜头默认值，覆盖 Step 4 / 6 / 8 的相关字段。风格文件是参考模块——它们*不会*被宿主 agent 单独注册为 skill，所以不会触发歧义。

## 安装

skill 文件放在 `~/.claude/skills/<skill-name>/`（用户级）或 `.claude/skills/<skill-name>/`（项目级）。文件夹名必须与 `SKILL.md` 中的 `name:` 字段一致（`cinematic-director`）。

```bash
# 用户级（所有项目可用）
git clone https://github.com/wuwangzhang1216/DirectorSKILL.git \
  ~/.claude/skills/cinematic-director

# 项目级（只在当前项目下生效）
git clone https://github.com/wuwangzhang1216/DirectorSKILL.git \
  .claude/skills/cinematic-director
```

重新加载 Claude Code（或宿主 agent）后即可触发。

## 快速开始

### 纯导演式流程

```text
你：把这段做成 Runway 的 4 镜头 AI 视频方案，16:9。
    "民国上海，一个信差在一户公寓门口犹豫，敲了一下门，又把信封从门缝塞进去，转身离开。"
```

skill 会输出：节拍图 → 导演书 → 分镜表（每个镜头含叙事功能、景别、镜头运动、走位、连贯性锚点）→ Runway 形态的视频提示词 → QC 注记。

### 叠加导演风格

```text
你：同一场戏，用王家卫的风格来拍。
```

skill 加载 `references/director_styles/09_wong_kar_wai.md`，把默认值覆盖为：狭窄走廊的手持摄影、霓虹与实用光源、门框/镜子的画中画构图、塞信和离开的慢动作、可选的信差独白、作为情绪锚点的怀旧音乐。同样 4 个镜头，完全不同的镜头语言。

### 修复失败的生成

```text
你：我生成的片子像 PPT——人物几乎不动，雨是静止的。诊断并重写这条提示词：[粘贴提示词]
```

skill 按 QC 诊断顺序（资产不一致 → 提示词超载 → 动作太弱 → 终点缺失 → 镜头逻辑错误 → 连贯性缺口 → 工具不匹配）定位最可能的原因，输出含明确主体运动、环境反应、明确结束状态的修复版提示词。

## 导演风格清单

| # | 导演 | 一句话风格 |
|---|---|---|
| 01 | Steven Spielberg 斯皮尔伯格 | 情感驱动的经典商业叙事，家庭羁绊，先反应再揭示的奇观 |
| 02 | Alfred Hitchcock 希区柯克 | 信息差悬念、窥视、误认、控制式揭露 |
| 03 | Stanley Kubrick 库布里克 | 对称构图、单点透视、冷峻形式、哲学寓言 |
| 04 | Akira Kurosawa 黑泽明 | 史诗群像、人道主义、把天气当戏剧、动态动作空间 |
| 05 | Martin Scorsese 斯科塞斯 | 都市能量、罪感、旁白、动感摄影、道德坠落 |
| 06 | Federico Fellini 费里尼 | 梦境逻辑、马戏巡游、自传性幻想 |
| 07 | Ingmar Bergman 伯格曼 | 室内心理剧、脸部特写、存在主义沉默 |
| 08 | Andrei Tarkovsky 塔可夫斯基 | 诗意时间、长镜头、水与火、精神探索 |
| 09 | Wong Kar-wai 王家卫 | 都市孤独、错过、霓虹、碎片记忆、旁白 |
| 10 | Christopher Nolan 诺兰 | 高概念结构、时间谜题、IMAX 级实拍奇观 |
| 11 | Denis Villeneuve 维伦纽瓦 | 宏大尺度、雾霭、几何对称、低频轰鸣的寂静 |
| 12 | David Fincher 芬奇 | 外科手术级控制、青绿琥珀调色、程序化调查、克制式恐惧 |
| 13 | Nicolas Winding Refn 雷弗恩 | 霓虹色块、对称仪式构图、缓慢凝视、突发暴力 |
| 14 | Bi Gan 毕赣 | 西南雾镇、超长长镜头、梦境记忆循环、诗歌旁白 |

每个风格文件都遵循统一的 9 节结构（适用场景 / 核心风格关键词 / 叙事方法 / 镜头语言 / 灯光与色彩 / 剪辑节奏 / 声音与音乐 / 人物与表演 / 可迁移拍摄清单 / 提示词模板），所以加第 11 位导演只需新建一个文件，外加在 `references/director_styles/README.md` 加一行。

## AI 视频工具适配器

主流水线产出的是导演意图。Step 9 把它整形成目标模型的输入。当前内置：

| 工具 | 适配器使用的强项 |
|---|---|
| Runway | 图生视频运动、场景动作、镜头运动、风格描述 |
| Veo | 视觉风格 + 声音 + 时间戳多镜头 + 首尾帧 |
| Kling | 物理动作、表演表现力、更长的单镜头展开 |
| Luma | 关键帧、人物引用、镜头标签、循环/续接 |
| 即梦 / Dreamina / Seedance | 双语提示词、首尾帧、平滑运动、简洁的中英模板 |
| 万相 Wanxiang | 文生视频、图生视频、多镜头时间戳 |

新加一个工具，只需在 `references/ai-video-tool-adapters.md` 追加一段"X-style adapter"——提示词优先级、模板、约束——其他文件不用动。

## 输出模式

skill 会根据请求选择合适的输出形态，模式可组合：

- **Mode A — 导演分析**：戏剧内核、潜文本、情绪弧、视觉论点、导演规则
- **Mode B — 分镜方案**：使用 `assets/shot-plan-template.md`
- **Mode C — 关键帧提示词包**：使用 `assets/keyframe-prompt-template.md`
- **Mode D — 视频动作提示词包**：使用 `assets/video-prompt-template.md`
- **Mode E — 连贯性圣经**：使用 `references/continuity-bible.md`
- **Mode F — QC 与修复**：使用 `assets/qc-checklist.md`

## 扩展方式

- **加导演**：在 `references/director_styles/` 下新建 `NN_<slug>.md`，沿用现有 9 节模板；然后在风格索引 README 加一行，并在 `SKILL.md` 的 `director_style` 枚举里加名字。
- **加 AI 视频工具**：在 `references/ai-video-tool-adapters.md` 追加一段适配器。主流水线 Step 9 自动引用该文件。
- **加输出模式**：扩展 `SKILL.md` 的"Output modes"小节，可选地在 `assets/` 加模板。
- **加 eval**：在 `evals/evals.json` 追加用例。

## 使用规则与免责声明

导演风格模块描述的是**高层方法**——叙事倾向、镜头语法、灯光逻辑、剪辑节奏、声音、表演、可迁移拍摄清单。它们**不授权**复制任何导演真实电影中的具体镜头、台词、角色、剧情或其他受版权保护的表达。请把它们当作镜头来启发原创作品。

## 许可证

MIT，见 [LICENSE](LICENSE)。

MIT 授权覆盖的是 skill 文件本身（SKILL.md、references、assets、模板）。上方"使用规则"约束的是*如何*把这些导演知识应用到已有电影上，是与软件许可分开的另一个问题。
