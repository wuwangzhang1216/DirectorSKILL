# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.0] - 2026-05-25

### Added

- `CONTRIBUTING.md` — bilingual guide covering how to add a director style, AI video tool adapter, output mode, or eval case; project layout; style conventions; PR checklist; copyright-safety rule.
- `CHANGELOG.md` — this file.
- `references/director_styles/example_comparisons.md` — same scene treated by four different directors (Spielberg, Kubrick, Wong Kar-wai, Bi Gan), demonstrating how a style overlay actually changes blocking, camera grammar, color, sound, and prompt template.

### Changed

- `references/director_styles/README.md` — links to `example_comparisons.md`.
- Top-level `README.md` — references CONTRIBUTING and CHANGELOG; minor wording polish.

## [1.1.0] - 2026-05-25

### Added

- Four contemporary director-style overlays (now 14 total):
  - `11_villeneuve.md` — monumental scale, mist, geometric symmetry, low-rumble silence.
  - `12_fincher.md` — surgical control, teal-amber palette, procedural investigation, restrained dread.
  - `13_refn.md` — neon color blocks, symmetric ritual framing, slow gaze, sudden violence.
  - `14_bi_gan.md` — misty SW-China small towns, single ultra-long take, dream-memory loops, poetic voice-over.
- GitHub Actions workflows:
  - `.github/workflows/markdownlint.yml` (DavidAnson/markdownlint-cli2-action)
  - `.github/workflows/links.yml` (lycheeverse/lychee-action, `--offline` mode)
- `.markdownlint.json` calibrated for compact prose-heavy bilingual markdown.
- Four style-overlay eval cases (now 7 total):
  - `kubrick-style-corporate-office`
  - `wong-kar-wai-style-rain-street` (overlay variant of `rain-street-image-to-video`)
  - `villeneuve-style-desert-encounter`
  - `bi-gan-style-small-town-walk`
- CI status badges in README (markdownlint, links).

### Changed

- `SKILL.md` frontmatter `description:`, YAML `director_style:` enum, Step 3 "Available styles:" line, and "When to activate" bullet now include the four new directors.
- `SKILL.md` `version` bumped to `1.1.0`.
- `references/director_styles/README.md` table extended to 14 rows.
- Top-level `README.md` EN and 中文 director tables extended; repo-structure tree extended.
- `.markdownlint.json` disables MD022, MD031, MD032 — the director-style files use compact prose-under-heading by design, and the rules don't add real value for this content.
- The three ASCII-diagram fences in `README.md` are tagged `text` so MD040 stays useful.

## [1.0.0] - 2026-05-25

### Added

- Initial release of the `cinematic-director` skill.
- `SKILL.md` — 10-step directorial pipeline: script breakdown → beat map → director style selection → director's book → blocking → shot list → keyframe strategy → AI video prompt construction → tool adapter selection → QC & repair.
- 6 output modes: Director Analysis, Shot Plan, Keyframe Prompt Pack, Video Motion Prompt Pack, Continuity Bible, QC & Repair.
- 10 director-style overlays in `references/director_styles/`: Spielberg, Hitchcock, Kubrick, Kurosawa, Scorsese, Fellini, Bergman, Tarkovsky, Wong Kar-wai, Nolan.
- 6 AI video tool adapters in `references/ai-video-tool-adapters.md`: Runway, Veo, Kling, Luma, 即梦/Dreamina/Seedance, Wanxiang.
- Shared references: `cinematic-language.md`, `continuity-bible.md`.
- Reusable templates in `assets/`: `shot-plan-template.md`, `keyframe-prompt-template.md`, `video-prompt-template.md`, `qc-checklist.md`.
- `evals/evals.json` with 3 baseline cases.
- Bilingual README (EN + 中文), MIT license.

[Unreleased]: https://github.com/wuwangzhang1216/DirectorSKILL/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/wuwangzhang1216/DirectorSKILL/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/wuwangzhang1216/DirectorSKILL/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/wuwangzhang1216/DirectorSKILL/releases/tag/v1.0.0
