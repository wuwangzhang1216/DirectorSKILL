# Example: one scene, four director styles

This file shows the same scene treated by four very different director-style overlays. Read it to feel what a style overlay actually changes downstream — blocking, camera grammar, color, sound, prompt template — and what stays the same (the underlying dramatic situation, the continuity rules, the visual thesis discipline).

> Usage rule: the four treatments below describe high-level methods only. None copies specific shots, dialogue, characters, or plots from any real film. Use them as lenses for original work.

## The scene (input)

> A middle-aged man stands outside a 6th-floor apartment door at dusk, holding a wilted bouquet. He raises his hand to knock, lowers it, then knocks twice and waits.

Constraints shared by all four treatments:

- 10–12 second AI video clip, 16:9
- Same subject (the man, the bouquet, the door)
- Same dramatic question: will the person inside answer?
- Same continuity anchors: man's face, costume, bouquet, door, corridor

What differs is the **lens** — and the lens changes everything downstream.

---

## 1. Spielberg style (`01_spielberg`)

**Visual thesis** — An ordinary man carrying a small emotional weight, seen with warmth before the reveal.

### Beats

1. Wide low-angle of him at the end of a warm corridor (we see the scale of his walk).
2. Push-in on his face as he raises and lowers his hand (reaction first, before we know why).
3. Over-shoulder of his hand reaching, bouquet visible in the foreground.
4. Hold on his face as he knocks, music swells, then cuts on the second knock.

**Camera** — slow dolly-in on the corridor; push-in on his face; over-shoulder on the hand. Movement is purposeful, never showy. Always shows us the spatial relationship between the man, the door, and the corridor's depth.

**Color & lighting** — warm tungsten ceiling lamps; golden-hour spill from a window at the far end of the corridor; soft backlight rims his hair and the wilted petals.

**Sound** — muted footsteps; distant TV from a neighbor's door; a single melodic motif on strings that swells as his hand reaches.

### Sample image-to-video prompt

```text
Warm-light apartment corridor at dusk, locked camera with a slow push-in on the man's face. He starts holding a wilted bouquet at chest height, raises his right hand toward the door, lowers it again, then knocks twice. Golden window light at the far end of the corridor softens the air. End on his held breath after the second knock. Maintain his face, the muted brown coat, the bouquet's wilted petals, and the warm corridor light. No extra people, no modern technology, no text, no watermark.
```

---

## 2. Kubrick style (`03_kubrick`)

**Visual thesis** — A small human ritual performed inside an indifferent geometric corridor.

### Beats

1. Dead-center symmetrical wide of the corridor; he stands at the far end.
2. Slow mechanical dolly-in (constant speed, no acceleration) until he is medium-framed.
3. Overhead insert of his shoes centered on the tile pattern.
4. Locked frontal medium as he knocks twice — no reaction shot.

**Camera** — symmetric one-point perspective down the corridor; locked or pure dolly only; no handheld, no orbit. The corridor's geometry is the second subject.

**Color & lighting** — cold white fluorescent ceiling banks, dead even; no warm fill; the bouquet's faded pink reads as a single off-color note against the gray-white walls.

**Sound** — fluorescent hum; the rhythmic squeak of his shoes on tile; two flat, evenly spaced knocks; no music.

### Sample image-to-video prompt

```text
Locked camera, dead-center symmetric composition, one-point perspective down a fluorescent-lit gray apartment corridor. The man begins standing precisely at the end of the corridor holding a wilted bouquet, then a slow pure-dolly push-in begins at constant speed and continues throughout. He raises his hand, lowers it once, then knocks exactly twice, evenly spaced. End at medium frame, still locked, no reaction. Maintain the cold fluorescent palette, the geometric tile pattern, the man's face, the bouquet. No camera shake, no orbit, no warm light spill.
```

---

## 3. Wong Kar-wai style (`09_wong_kar_wai`)

**Visual thesis** — A small "almost" between two people who may not actually meet.

### Beats

1. Handheld narrow frame through the corridor's window arch, neon sign visible outside.
2. Slow-motion of his hand rising toward the door — held for almost the full clip.
3. Voice-over (his thought) overlays the slowed gesture.
4. Two knocks at near-normal speed land sharply against the slowed image.

**Camera** — handheld, narrow framing, often through an obstruction (window mullion, door frame, glass). Slow-motion or step-print for the hesitation; normal speed only for the knock.

**Color & lighting** — green-pink neon practical from a sign outside the corridor window; wet reflections on the floor from an earlier rain; everything else fades into dark.

**Sound** — a Mandarin pop song from inside another apartment; ambient rain on the far side of the building; voice-over begins before the gesture and continues past the knock.

### Sample image-to-video prompt

```text
Handheld, narrow corridor framed through a window mullion at dusk. Pink and green neon from a sign outside throws color onto wet reflective floor. The man begins with bouquet at his side, lifts his hand toward the door in slow motion — step-print feel, almost a full hold — then on the last beat the motion returns to normal speed and he knocks twice. End on the second knock with the neon flickering once. Maintain his face, the wilted bouquet, the neon palette, the wet floor reflections. No extra people in the corridor, no modern phone or screen visible, no text, no watermark.
```

---

## 4. Bi Gan style (`14_bi_gan`)

**Visual thesis** — A memory looking for its own origin; the corridor is the inside of someone's head.

### Beats

1. Long take starts on a wet street outside the building, camera floats forward.
2. Through the lobby, into the stairwell (flickering tube light, peeling posters).
3. Up the stairs in real time; we hear distant transistor radio from somewhere.
4. Arrives at the door on the 6th floor; he raises his hand, lowers it, raises it again, knocks twice; poetic voice-over throughout.

**Camera** — one continuous handheld follow shot from street to door; no cuts. Camera moves with the breath of the walker, not with the precision of a dolly.

**Color & lighting** — practical incandescent in the stairwell; wet asphalt reflections at the start; fluorescent flicker on the landings; mixed warm/cold light throughout, low saturation, humid.

**Sound** — distant rain; footsteps; a transistor radio playing an old song one floor below; a poetic voice-over that does not match the visible action — it speaks of someone else, somewhere else, at a different time.

### Sample image-to-video prompt (long clip — give it 30s+ if the tool supports it)

```text
One continuous handheld long take. Begin on a wet asphalt street at dusk, camera floats forward toward the lit lobby of a small apartment building. Without cut, pass through the lobby and enter the stairwell — flickering fluorescent tube, peeling posters, faint sound of an old Mandarin song from a transistor radio one floor up. Climb in real time to the 6th floor. The man with the wilted bouquet is already at the door; he raises his hand, lowers it once, then knocks twice. A quiet poetic voice-over runs throughout, speaking of a different person and a different rain. End on the door, just before any answer. Maintain the man's face, the bouquet, the humid low-saturation palette, the wet reflections. No cut, no jump, no modern screens, no text.
```

---

## What changed across the four

Same scene, same character, same dramatic question — but:

| Dimension | Spielberg | Kubrick | Wong Kar-wai | Bi Gan |
|---|---|---|---|---|
| Camera | slow dolly, push-in, over-shoulder | locked + pure dolly, symmetric | handheld, narrow, through obstruction | one continuous handheld long take |
| Lighting | warm tungsten + golden-hour spill | cold even fluorescent | neon practical, wet floor | mixed warm/cold incandescent, humid |
| Pace | musical, builds to the knock | mechanical, even | time-distorted (slow-mo) | real-time long-take |
| Sound | melodic motif + distant TV | fluorescent hum + clean knocks | Mandarin pop + voice-over | rain + transistor + poetic voice-over |
| Editing | classical (4 shots, reaction-then-reveal) | minimal, almost no cuts | one slow-mo held gesture | no cuts at all |
| Prompt center | reaction before reveal | symmetric geometric ritual | almost-missed connection | memory walking the body |

The continuity anchors (face, bouquet, door, corridor) are the same in all four. The lens decides everything else.

## Try it yourself

Copy any of the four prompts into your image-to-video tool of choice (use the corresponding adapter in [`../ai-video-tool-adapters.md`](../ai-video-tool-adapters.md) to translate language register if needed). Generate side-by-side. The differences should be obvious in the first second.

If they aren't, the failure is usually one of:

- The input image already strongly fixes a lens (e.g. it was generated with "cinematic neon" style baked in) — start from a more neutral keyframe.
- The tool is ignoring camera/movement instructions — use the corresponding adapter's keyword conventions.
- You combined two director styles in one prompt — pick exactly one.
