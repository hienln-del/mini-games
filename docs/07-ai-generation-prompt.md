# AI Generation Prompt Template

Use this as the final prompt with either a simple user request or a completed `docs/01-game-brief.md`. The AI must expand short requests into complete game specs, create the game file in `output/`, and add the game to `output/index.html`.

## Prompt

```text
You are an expert game developer. Generate one complete portrait-mobile arcade/puzzle browser game as a single self-contained HTML file stored in the `output/` folder.

USER REQUEST OR GAME BRIEF
[Paste a simple request such as "make flappy bird game" or paste completed docs/01-game-brief.md content here.]

SIMPLE REQUEST EXPANSION
- If the user request is short or incomplete, silently expand it into a complete internal game brief before coding.
- Infer title, filename slug, genre, player fantasy, touch-first controls, finite win/loss rules, scoring, progression, content budget, portrait art style, audio style, and required screens.
- Use familiar genre conventions when the request references a known game type, but create original procedural art, naming, and details.
- Do not ask follow-up questions unless the request is unsafe, impossible, or directly contradictory.
- Prefer a finished playable game over a tiny prototype.
- Default to finite and completable unless the user explicitly asks for endless mode.

FILE OUTPUT RULES
- Create the generated game at `output/<game-slug>.html`.
- Use a lowercase kebab-case filename, for example `output/flappy-bird.html`.
- Create the `output/` folder if it does not exist.
- Do not create any other game source, asset, build, or dependency files.
- Add one game entry to the inline `GAMES` array in `output/index.html`.
- Preserve all existing `GAMES` entries and all unrelated game files.
- If the slug already exists, update that manifest entry only when intentionally replacing that exact game.
- After creating the game and updating the launcher, respond with the game path, launcher path, and a short note only.

LAUNCHER MANIFEST RULES
- `output/index.html` is the static game library hub and owns the canonical game list.
- Each manifest entry must include `slug`, `title`, `file`, `genre`, `description`, `controls`, `status`, `tags`, and `createdAt`.
- `file` must point to a sibling HTML file such as `flappy-bird.html`, not `output/flappy-bird.html`.
- Use `status: 'Playable'` for completed games.
- Use `createdAt` in `YYYY-MM-DD` format.

HTML RULES
- The saved file must contain exactly one complete HTML document.
- The game must run by saving the output as an `.html` file and opening it in a modern browser.
- Use no build step, no imports, no modules, no CDN, no external files, no remote images, no remote fonts, and no remote audio.
- Put all CSS inside one inline `<style>` block.
- Put all JavaScript inside one inline `<script>` block.
- Use Canvas 2D as the primary renderer.
- Use procedural Canvas drawing, inline SVG strings, CSS, and WebAudio only for assets.

PORTRAIT MOBILE RULES
- Target portrait mobile only.
- Use a 9:16-ish internal resolution such as `360x640`, `390x844`, or `414x736`.
- Include `viewport-fit=cover` in the viewport meta tag.
- Fill portrait screens without landscape letterboxing, horizontal scrolling, or clipped UI.
- Use `touch-action: none`, prevent page scroll during play, and respect safe-area insets near screen edges.
- Touch input must be primary. Keyboard controls may exist only as desktop fallback.
- All HUD text, menu text, and buttons must fit at `360px` viewport width.
- Visible buttons must be touch-safe, at least `44px` in both dimensions.
- Use the full portrait screen intentionally: top HUD, middle playfield, and bottom objective/control/feedback area.
- Do not leave the lower screen empty during gameplay unless the main playfield intentionally fills that space.
- No board pieces, selection rings, glows, shadows, or animated tiles may overflow the grid or visual container.

REQUIRED GAME STRUCTURE
- Include title/menu, gameplay, pause, win screen, loss screen, restart, mute, and visible controls.
- Use explicit game states: `title`, `playing`, `paused`, `won`, and `lost`.
- Use `requestAnimationFrame` for the main loop.
- Use a fixed-step update or equivalent stable timing model with large delta clamping.
- Keep gameplay coordinates separate from CSS scaling.
- Handle browser resize and high-DPI canvas rendering.
- Keep the game playable with touch. Add keyboard support only as fallback.
- Use `localStorage` only for optional small preferences or best score, and wrap it in `try/catch`.

GAMEPLAY SYSTEMS
- Implement the full core loop from the user request or inferred brief.
- Include deterministic player input, collision, scoring/progress, difficulty ramp, and win/loss checks.
- Declare a content budget constant such as `TARGET_COUNT`, `TOTAL_WAVES`, `LEVELS`, `TIME_LIMIT`, or `TOTAL_OBJECTIVES`.
- Connect spawn logic and win logic to the same content budget.
- Include a `validateProgression()` helper or equivalent internal sanity check so generated content cannot run out while gameplay continues.
- For finite games, trigger `won` immediately when the objective is complete.
- For endless games, keep spawning meaningful hazards/rewards/objectives forever and do not stop content generation.
- Never allow `playing` to continue after all hazards, rewards, waves, pipes, gates, or objectives are exhausted.
- Show only useful HUD information: score, lives/health/timer/progress/objective as relevant.
- Restart must reset gameplay state without reloading the page.
- Pause must freeze gameplay and show resume/restart/mute instructions.
- Avoid soft locks. Every screen must have a clear next action.

ANIMATION, VFX, AND FEEDBACK
- Add readable animation for player, hazards, rewards, and UI changes.
- Add particles, score pops, flashes, screen shake, or hit stop where they improve feedback.
- Important events need at least two feedback channels, such as visual change plus sound.
- Cap particle counts and avoid effects that hide gameplay information.
- Avoid rapid full-screen flashing.

ART AND AUDIO
- Use a coherent procedural art style based on the user request or inferred brief.
- Use a small palette with clear roles for player, hazards, rewards, background, UI, success, and failure.
- Hazards and rewards must differ by both shape and color.
- Use WebAudio for short procedural sound effects after user interaction.
- Include a mute toggle. If audio fails, gameplay must continue silently.

GAME FEEL
- Make controls responsive and readable.
- Add input buffering, coyote time, grace periods, or magnetism only when relevant to the genre.
- Add polish such as HUD pulse, pickup burst, hit flash, level clear celebration, and best score feedback.
- The player should understand the objective and controls within 5 seconds.

MATCH-3 / CANDY PUZZLE CONTRACT
- If the request is `make candy crush`, `make match-3`, or similar, compute board layout from available portrait space.
- Define `boardX`, `boardY`, `boardW`, `boardH`, `cellSize`, and `gap`; prove the last row and last column fit inside the board.
- Prefer 7x7 for portrait mobile unless 8x8 can fit cleanly with readable candies and no overflow.
- Keep candies, selection rings, swap animations, shadows, glows, and particles inside board bounds except for brief intentional bursts.
- Use the bottom zone for useful gameplay information: moves, target progress, selected candy info, boosters, combo, hint, or objective text.
- Do not leave a large empty section below the board.
- Ensure the board always has at least one legal move after cascades; reshuffle if needed.
- Lock input while swap, clear, drop, refill, and cascade animations resolve.
- Special candies must have premium effects: anticipation pulse, clear directional or radial activation, affected-cell feedback, particles, sound, score/combo response, and short afterglow.
- A single white line/icon on a candy is not enough for a special candy.

QUALITY BAR
- The final HTML must be complete, playable, and polished.
- It must have no missing assets, no placeholder TODOs, no console spam, and no known runtime errors.
- It must work after mobile viewport resize or orientation UI changes.
- It must be readable and playable on portrait mobile viewports `390x844` and `360x740`.
- It must not contain dead gameplay states, empty scrolling, exhausted spawns, or unreachable win conditions.
- It must not contain overflowing grid layouts, unused lower-screen dead space, or cheap special-item effects.
- It must include comments only where they clarify non-obvious logic.

FLAPPY-STYLE CONTRACT
- If the request is `make flappy bird game` or similar, make it portrait mobile and tap-first.
- If the goal is finite, such as 30 gates, at least that many gates must spawn or the game must win before content ends.
- Continue spawning gates until the score goal is reached, or make it a true endless score attack only if the user explicitly asks for endless.
- Never allow the bird to keep flying after the last pipe/gate with no new obstacles.

Now create `output/<game-slug>.html` with the complete single-file game and update `output/index.html` so the game appears in the library.
```

## Optional Sample Brief Snippet

Use this tiny sample to test the prompt structure.

```text
make flappy bird game
```

Expected AI behavior: infer complete portrait-mobile mechanics, use tap-first controls, spawn enough gates for the target score, make win/loss/restart reachable, prevent empty continuation after obstacles end, save it to `output/flappy-bird.html`, and add it to `output/index.html`.

## Optional Match-3 Sample Brief Snippet

```text
make candy crush saga game
```

Expected AI behavior: infer a portrait-mobile match-3 game, compute a board that fits inside its grid, use the bottom screen for useful progress/booster/objective UI, create premium special-candy effects, prevent no-move boards, make win/loss/restart reachable, save it to `output/candy-crush-saga.html`, and add it to `output/index.html`.
