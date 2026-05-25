# Video Motion Prompt Template

## Image-to-video single-shot template

```text
[Camera behavior]. Starting from the input image, [subject] begins [start state], then [one primary action with speed/direction]. [Environment or costume element] moves subtly in response. End with [clear final state/composition]. Maintain [identity, costume, location, lighting, era]. Avoid [specific failure modes].
```

## First/last-frame template

```text
Use the first image as the opening frame and the second image as the ending frame. The shot transitions from [first-frame state] to [last-frame state] through [one continuous action]. Camera [movement]. Motion should feel [pace/emotion]. Preserve [identity/costume/location/lighting]. No [failure modes].
```

## Text-to-video template

```text
[Format and style]. [Subject with concrete identity/costume]. [Location, era, time, atmosphere]. [Primary action]. [Shot size, angle, camera movement]. [Lighting, lens, composition]. [Sound if supported]. [Constraints].
```

## Multi-shot/timestamp template

```text
Overall: [story theme, tone, style, continuity rules].
[00:00-00:03] Shot 1: [shot size/angle]. [character action]. Camera [movement]. Emotion: [state]. Sound: [if supported].
[00:03-00:06] Shot 2: [shot size/angle]. [character action]. Camera [movement]. Emotion: [state]. Sound: [if supported].
[00:06-00:10] Shot 3: [shot size/angle]. [character action]. Camera [movement]. Emotion: [state]. Sound: [if supported].
```

## Prompt compression rules

- Put action before style when using image-to-video.
- Keep one primary action per shot.
- Use concrete verbs: lifts, turns, hesitates, grips, steps, lowers, recoils.
- Avoid vague verbs: struggles, feels, realizes, becomes emotional, experiences trauma.
- Replace emotion-only direction with visible behavior:
  - Bad: “he is scared.”
  - Good: “his shoulders tense, his breath stops, his eyes flick toward the door.”
