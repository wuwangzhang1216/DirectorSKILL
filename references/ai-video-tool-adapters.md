# AI Video Tool Adapters

Use this file when the user names a target video model or platform. The goal is to adapt directing language to the tool's likely control surface.

## General AI video rule

Most image-to-video tools perform best when the input image defines: identity, composition, lighting, setting, costume, and visual style. The text prompt should primarily define motion, camera behavior, timing, and end state.

## Runway-style adapter

Best for: image-to-video motion, scene motion, camera motion, style descriptors.

Prompt priorities:
1. subject motion
2. scene/environment motion
3. camera motion
4. pace/style descriptor
5. constraints

Template:
```text
[Subject] [primary action]. [Scene element] reacts/moves [specific way]. Camera [locked / slowly dollies in / pans left / handheld follows]. Motion is [slow / subtle / tense / natural]. Maintain [identity/style]. No [failure modes].
```

## Veo-style adapter

Best for: visual style + sound + timestamped sequences + first/last-frame transitions when available.

For multi-shot:
```text
Overall style: [style, tone, continuity rules].
[00:00-00:02] [Shot size and angle]. [Action]. [Camera]. [Sound].
[00:02-00:05] [Shot size and angle]. [Action]. [Camera]. [Sound].
```

For first/last frame:
```text
Starting from the first provided image and ending on the second provided image, the camera [transition movement]. The subject [continuous action]. The transition should feel [emotion/pace]. Maintain [identity/location/style].
```

## Kling-style adapter

Best for: physical action, expressive performance, longer single-shot or multi-beat progression, dialogue/audio if supported.

Prompt priorities:
1. audience-visible action progression
2. physical body mechanics
3. camera reaction to motion
4. clear character labels for dialogue
5. image-as-anchor for image-to-video

Template:
```text
Using the input image as the first frame, [Character A] starts [pose]. Over [duration], [Character A] [physical action in sequence]. The camera [movement] to follow/emphasize [story point]. End with [final pose/composition]. Keep [identity/costume/location].
```

Dialogue rule:
```text
[Character A: unique visual label, voice/emotion]: "line"
Immediately, [Character B: unique visual label, voice/emotion]: "line"
```
Avoid pronouns when multiple characters speak.

## Luma-style adapter

Best for: keyframes, character references, visual references, camera tags, loops, extend.

Use:
- `@character` or explicit character reference binding when available.
- keyframe tab for first-frame animation or first/last-frame transition.
- visual reference for style/composition matching.
- camera tags/options such as pan, orbit, zoom when available.

Template:
```text
@character [does one clear action]. Camera [pan/orbit/zoom/locked]. Environment [subtle motion]. End with [clear endpoint]. Preserve @character face, outfit, and proportions.
```

## 即梦 / Dreamina / Seedance-style adapter

Best for: Chinese-language ideation, first/last-frame video, image-to-video, smooth motion, short-form cinematic clips.

Use Chinese, English, or bilingual prompts depending on the user's workflow. For Chinese UI, concise Chinese often works well.

Template in Chinese:
```text
固定/缓慢推进镜头。画面从首帧开始，主体先处于[起始状态]，随后[单一主要动作，说明速度和方向]。环境中[雨水/灯光/烟雾/衣料等]发生细微运动。结尾停在[明确结束状态]。保持同一人物面部、服装、场景、光线，不出现现代物件、文字、水印、额外人物。
```

Template in English:
```text
Locked camera / slow push-in. Starting from the first frame, the subject begins [state], then [one primary action with speed and direction]. [Environmental element] moves subtly. End on [final state]. Preserve the same face, costume, setting, and lighting. No modern objects, no text, no watermark, no extra people.
```

If using first + last frame, ensure the two frames are visually related. If the distance between them is too large, split into more clips.

## Wanxiang-style adapter

For text-to-video:
```text
Subject + scene + motion + aesthetic control + style.
```

For image-to-video:
```text
Motion + camera movement.
```

For multi-shot:
```text
Overall description: [story, style, emotion, continuity].
Shot 1 [0-3s]: [action, shot size, camera, emotion].
Shot 2 [3-6s]: [action, shot size, camera, emotion].
Shot 3 [6-10s]: [action, shot size, camera, emotion].
```

## Universal negative constraints

Use only relevant constraints, not all of them:

- no text, no subtitles, no watermark
- no extra people
- no face change, no costume change
- no modern objects
- no distorted hands, no warped face
- no jitter, no flicker, no sudden camera shake
- no scene change unless requested
- no exaggerated motion
- no random zoom or rotation
