‎# Director Style Modules

Style overlays used by the main `cinematic-director` skill. Each file is a high-level lens — narrative tendencies, camera grammar, lighting, editing rhythm, sound, performance, transferable shot checklist, and a prompt template — that overrides defaults in the main workflow when the user asks for an "in the style of X" treatment.

These are **reference modules**, not standalone skills. They do not get loaded by the host agent on their own. They are pulled in by the main skill at Step 3 (Director style selection) when a style is named.

> Usage rule: these files describe high-level methods only. Do not copy specific shots, lines, characters, plots, or other copyrighted expression from any director's actual films. Use them to inform original work.

## Available styles

| File | Director | Lens in one line |
|---|---|---|
| [01_spielberg.md](01_spielberg.md) | Steven Spielberg 斯皮尔伯格 | Emotional mainstream narrative, family stakes, awe via reaction-before-reveal |
| [02_hitchcock.md](02_hitchcock.md) | Alfred Hitchcock 希区柯克 | Suspense via shared knowledge, voyeurism, mistaken identity, controlled withholding |
| [03_kubrick.md](03_kubrick.md) | Stanley Kubrick 库布里克 | Symmetry, one-point perspective, cold formalism, philosophical allegory |
| [04_kurosawa.md](04_kurosawa.md) | Akira Kurosawa 黑泽明 | Epic ensemble, humanism, weather as drama, dynamic action space |
| [05_scorsese.md](05_scorsese.md) | Martin Scorsese 斯科塞斯 | Urban energy, guilt, voice-over, kinetic camera, moral fall |
| [06_fellini.md](06_fellini.md) | Federico Fellini 费里尼 | Dream logic, circus parade, autobiographical fantasy, grotesque tenderness |
| [07_bergman.md](07_bergman.md) | Ingmar Bergman 伯格曼 | Interior psychological drama, face close-ups, existential silence |
| [08_tarkovsky.md](08_tarkovsky.md) | Andrei Tarkovsky 塔可夫斯基 | Poetic time, long takes, water and fire, spiritual search |
| [09_wong_kar_wai.md](09_wong_kar_wai.md) | Wong Kar-wai 王家卫 | Urban loneliness, missed connections, neon, fragmented memory, voice-over |
| [10_nolan.md](10_nolan.md) | Christopher Nolan 诺兰 | High-concept structure, time puzzles, IMAX-scale practical spectacle |
| [11_villeneuve.md](11_villeneuve.md) | Denis Villeneuve 维伦纽瓦 | Monumental scale, mist, geometric symmetry, low-rumble silence |
| [12_fincher.md](12_fincher.md) | David Fincher 芬奇 | Surgical control, teal-amber palette, procedural investigation, restrained dread |
| [13_refn.md](13_refn.md) | Nicolas Winding Refn 雷弗恩 | Neon color blocks, symmetric ritual framing, slow gaze, sudden violence |
| [14_bi_gan.md](14_bi_gan.md) | Bi Gan 毕赣 | Misty SW-China small towns, single ultra-long take, dream-memory loops, poetic voice-over |

## How the main skill uses these

1. The user names a director or asks for "in the style of X" — or supplies one via `project.director_style` in the input schema.
2. The main skill loads the matching file and treats its sections as default overrides for:
   - Step 4 (Director's book): camera grammar, lighting logic, color palette, editing rhythm, sound direction, performance style
   - Step 6 (Shot list): preferred shot families, camera moves
   - Step 8 (AI video prompt construction): prompt template tendencies (pace, framing, language register)
3. If no director is named, the main skill uses the project's own tone and genre to set defaults.

Only one style should be active at a time. Mixing two directors usually produces incoherent output — pick one lens and let it govern the whole pass.

## Adding a new style

Create a new file in this directory using the same section structure as the existing ten:

```markdown
---
name: <slug>
title: <Director> 导演风格 Style Module
description: <one line on what this lens is for>
---

## 适用场景 / When to use
## 核心风格关键词 / Core keywords
## 叙事方法 / Narrative methods
## 镜头语言 / Shot language
## 灯光与色彩 / Lighting and color
## 剪辑节奏 / Editing rhythm
## 声音与音乐 / Sound and music
## 人物与表演 / Characters and performance
## 可迁移拍摄清单 / Transferable shot checklist
## 提示词模板 / Prompt template
```

Then add a row to the table above. The numbered prefix controls sort order; pick the next available number.
