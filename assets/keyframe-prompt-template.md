# Keyframe Prompt Template

Use for generating still images that will become first frames, last frames, or storyboard panels.

## Keyframe prompt structure

```text
[Shot ID]. [Shot size and angle]. [Subject identity and costume]. [Exact pose/action implication]. [Location and era]. [Lighting source and atmosphere]. [Composition rule]. [Texture/film style]. [Continuity constraints]. No text, no watermark, no modern objects.
```

## First-frame prompt

```text
Keyframe [shot_id] first frame: [subject] starts [pose/state], placed [position in frame], in [location]. [lighting/style]. The image should imply the next action: [next motion]. Maintain [continuity anchors]. No text, no watermark.
```

## Last-frame prompt

```text
Keyframe [shot_id] last frame: [subject] has completed [action], ending [pose/state], in the same [location/light/style]. This frame should match the first frame's identity, costume, and environment while clearly showing the new end state. No text, no watermark.
```

## Storyboard panel rule

A storyboard/keyframe should not be only a beautiful pose. It must imply either:

- a motion about to begin,
- a motion just completed,
- a reveal,
- a power relationship,
- or a story clue.
