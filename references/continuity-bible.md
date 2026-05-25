# Continuity Bible Template

Use this when the project has recurring characters, locations, props, or several generated clips that must cut together.

## Character continuity

```yaml
characters:
  - id: character_a
    name: ""
    age_range: ""
    body_type: ""
    face: ""
    hair: ""
    costume: ""
    color_palette: ""
    props: []
    performance_baseline: ""
    must_keep: []
    must_avoid: []
    reference_assets: []
```

## Location continuity

```yaml
locations:
  - id: location_a
    name: ""
    era: ""
    geography: ""
    architecture: ""
    lighting_sources: []
    weather: ""
    props: []
    color_palette: ""
    must_keep: []
    must_avoid: []
    reference_assets: []
```

## Shot-to-shot continuity

```yaml
shots:
  - shot_id: "01"
    start_state: ""
    end_state: ""
    character_position: ""
    camera_position: ""
    eyeline: ""
    props_state: ""
    lighting_state: ""
    must_match_next: []
```

## Continuity repair rules

- If face changes: reduce action, use closer reference, restate face/costume preservation, avoid long duration.
- If location changes: use image-to-video from a fixed location keyframe, restate no scene change.
- If clothing changes: mention exact costume in continuity anchors, not just style.
- If action jumps: define start → motion → end, or use first/last frame.
- If camera feels random: use locked camera or one named move.
