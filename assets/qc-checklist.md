# QC Checklist and Repair Guide

## Story QC

- [ ] Does every shot have a story function?
- [ ] Does the shot order create an emotional arc?
- [ ] Is the subtext visible through action, staging, or framing?
- [ ] Are there any pretty but useless shots?

## Direction QC

- [ ] Is the visual thesis consistent?
- [ ] Does camera movement have motivation?
- [ ] Is blocking clear: start → motion → end?
- [ ] Is lighting motivated by a source or stylized rule?
- [ ] Are transitions intentional?

## Continuity QC

- [ ] Same character face/body/costume across shots.
- [ ] Same location architecture, era, props, and lighting.
- [ ] End state of previous shot matches start state of next shot.
- [ ] No sudden extra characters, modern objects, text, or watermark.
- [ ] Props and weather remain consistent.

## AI video QC

- [ ] One primary action per prompt.
- [ ] One dominant camera movement.
- [ ] Clear end state.
- [ ] Prompt focuses on motion if using image-to-video.
- [ ] No contradictory instructions.
- [ ] Duration matches complexity.
- [ ] Reference images are visually compatible.

## Common failures and fixes

| Failure | Likely cause | Fix |
|---|---|---|
| Looks like slideshow | No real action; prompt only describes image | Add start → motion → end; add environmental reaction |
| Face changes | Too long/too much movement; weak reference | Shorten shot; use closer keyframe; restate identity anchors |
| Camera random | Too many camera moves | Use locked camera or one slow move |
| Subject does not perform action | Action too abstract | Use visible body mechanics |
| Bad transition between shots | End/start states mismatch | Create last frame for shot A and first frame for shot B |
| Distorted limbs | Fast/complex motion | Slow down, simplify, crop closer, reduce duration |
| Extra objects/people | Prompt ambiguity | Add negative constraints and tighter composition |
| Era breaks | Model fills modern details | State era + forbidden modern items + use period location keyframe |
