# Single-HTML Game Prompt Guide

This workspace contains a reusable documentation pack for prompting an AI to generate a complete portrait-mobile arcade or puzzle game from one prompt. The target output is always one self-contained `.html` file stored in `output/`, using vanilla JavaScript and Canvas 2D.

## Start Here

1. For a quick start, give the AI a simple request such as `make flappy bird game` together with `docs/07-ai-generation-prompt.md`.
2. For more control, fill out `docs/01-game-brief.md` and paste it into the prompt.
3. The AI should infer any missing design details, create a complete game, save it as `output/<game-slug>.html`, and add it to `output/index.html`.
4. Open `output/index.html` to play all generated games from one library.
5. Review the generated HTML and hub entry with `docs/08-review-checklist.md`.

## Simple Prompt Mode

The documentation is designed so the user does not need to write a full game design document. If the user only provides a short request, the AI must expand it into a complete internal brief before coding.

Examples of valid user requests:

- `make flappy bird game`
- `make snake but with portals`
- `make a cozy match-3 game about tea`
- `make a one-button climbing arcade game`

When the request is short, the AI should choose sensible mobile-first defaults for touch controls, goals, scoring, progression, portrait art style, audio, and polish. It should not stop to ask questions unless the request is unsafe or impossible.

## Hard Output Rules

The AI must generate exactly one game `.html` file inside `output/` and update the launcher manifest in `output/index.html`. The game file must include all CSS, JavaScript, art, audio, data, and configuration inline.

Required constraints:

- No build step.
- No imports or module loading.
- No external images, fonts, audio, JSON, CSS, or JavaScript files.
- No CDN dependencies.
- No server requirement.
- Store the generated game at `output/<game-slug>.html`.
- Add one manifest entry to `output/index.html` and preserve existing entries.
- Use Canvas 2D as the main renderer.
- Use `requestAnimationFrame` for the main loop.
- Target portrait mobile only: use a 9:16-ish internal resolution such as `360x640`, `390x844`, or `414x736`.
- Touch input is primary. Keyboard can be included only as a desktop fallback.
- Fill portrait screens without landscape letterboxing, horizontal scrolling, or clipped UI.
- Include title/menu, gameplay, pause, win/loss, restart, and clear controls.
- Default to finite, completable games unless the user explicitly asks for endless mode.
- Never let gameplay continue after all hazards, rewards, waves, pipes, gates, or objectives are exhausted.
- Avoid explanatory text outside the generated HTML unless explicitly requested.

## Recommended Prompt Assembly Order

Use this order when building a single prompt:

1. User request or game brief from `docs/01-game-brief.md`.
2. Single-file architecture rules from `docs/02-single-html-architecture.md`.
3. System rules from `docs/03-game-systems.md`.
4. Animation and VFX rules from `docs/04-animation-vfx.md`.
5. Art and audio direction from `docs/05-art-style-audio.md`.
6. Game feel requirements from `docs/06-game-feel-polish.md`.
7. Final instruction block from `docs/07-ai-generation-prompt.md`.

## What Complete Means

A generated game is complete when a player can find it in `output/index.html`, open it from `output/` on a portrait phone screen, understand touch controls, play a full session, win or lose, restart, and experience responsive feedback without console errors, missing assets, exhausted content, or empty gameplay states.

## Portrait Mobile Target

Generated games prioritize portrait mobile screens. The game must be comfortable at `390x844` and `360x740` viewport sizes.

Required portrait rules:

- Design for one-hand or two-thumb touch play.
- Use visible touch-safe controls or full-screen tap/drag input.
- Keep HUD, buttons, and instructions readable on narrow screens.
- Support safe-area insets with `env(safe-area-inset-*)` where controls approach screen edges.
- Prevent page scroll and browser gesture conflicts during play.
- Do not use landscape-only layouts or wide playfields as the primary experience.

## Completion Rules

Generated games must be complete, not demos.

- Finite games must declare a content budget such as `TARGET_COUNT`, `TOTAL_WAVES`, `LEVELS`, `TIME_LIMIT`, or `TOTAL_OBJECTIVES`.
- Spawn logic and win logic must use that same content budget.
- If a game needs 30 gates, at least 30 gates must spawn or the game must win before spawning stops.
- Endless games are allowed only when the user explicitly asks for endless mode, and they must keep spawning meaningful hazards/rewards forever.
- A game must never continue in `playing` state after all meaningful content is gone.
- The launcher entry should use `status: 'Playable'` only after the game passes the mobile and completion checklist.

## Layout And Polish Rules

Generated games must use the full portrait screen intentionally.

- Board games must compute board size from available portrait space; pieces must never overflow grid cells or board bounds.
- The play area, HUD, objective panel, controls, and feedback area should be balanced so the lower screen is not empty.
- Match-3 games should reserve lower screen space for useful content: move counter, target progress, selected candy info, booster buttons, combo meter, hint, or level objective.
- Special-piece effects must feel premium: layered animation, clear direction, particles, glow, sound, and board reaction. A white line or tiny icon alone is not enough.
- Reject games with overflowing pieces, unused empty bottom panels, cheap-looking special effects, or unclear special-candy behavior.

## Output Launcher

`output/index.html` is the static library that wires generated games together. It owns the canonical `GAMES` manifest.

For every new game, update the inline `GAMES` array with one entry:

- `slug`: lowercase kebab-case identifier.
- `title`: display title.
- `file`: sibling HTML filename such as `flappy-bird.html`.
- `genre`: short genre label.
- `description`: one-sentence game summary.
- `controls`: visible controls summary.
- `status`: usually `Playable`.
- `tags`: short searchable labels.
- `createdAt`: `YYYY-MM-DD` date.

Do not remove or overwrite unrelated games. If a slug already exists, update it only when intentionally replacing that exact game.

## Folder Map

- `docs/01-game-brief.md`: fill-in game design template.
- `docs/02-single-html-architecture.md`: one-file HTML structure and runtime rules.
- `docs/03-game-systems.md`: gameplay systems and state rules.
- `docs/04-animation-vfx.md`: animation, particles, shake, transitions, polish effects.
- `docs/05-art-style-audio.md`: procedural visuals and WebAudio rules.
- `docs/06-game-feel-polish.md`: responsiveness and tactile feel checklist.
- `docs/07-ai-generation-prompt.md`: paste-ready final prompt template.
- `docs/08-review-checklist.md`: acceptance checklist for generated games.
- `output/index.html`: launcher for all generated games.
- `output/`: generated single-file HTML games go here.
