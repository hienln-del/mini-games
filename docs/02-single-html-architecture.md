# Single-HTML Architecture

The generated game must be one complete HTML document. It should run by opening the file directly in a modern mobile browser, with portrait mobile as the primary and required target.

## File Skeleton

The HTML file should contain these parts in order:

1. `<!doctype html>` and normal `<html>`, `<head>`, `<body>` structure with `viewport-fit=cover` in the viewport meta tag.
2. Inline `<style>` with all layout, canvas, overlay, and responsive styles.
3. One `<canvas>` for the game renderer.
4. Minimal HTML UI overlays for menus, pause, win/loss, and accessibility text.
5. One inline `<script>` containing all game code.

Do not use external files, imports, modules, CDN scripts, remote fonts, remote images, or remote audio.

## Runtime Shape

Use vanilla JavaScript. Organize the script into clear sections:

- Constants and configuration.
- DOM and canvas setup.
- Input manager.
- Audio manager.
- Game state model.
- Entity helpers.
- Level or wave generation.
- Update functions.
- Render functions.
- UI sync functions.
- Main loop bootstrap.

Use plain objects and arrays unless a small class improves readability. Keep code easy to inspect in one file.

## Canvas And Scaling

- Render to a fixed portrait internal resolution such as `360x640`, `390x844`, `414x736`, or a grid-derived portrait resolution.
- Scale the canvas with CSS to fill portrait viewport height while preserving gameplay readability.
- Support high-DPI screens by using `devicePixelRatio` carefully.
- Keep gameplay coordinates independent from CSS pixel size.
- Recompute canvas backing size on resize.
- Prevent page scrolling during gameplay.
- Avoid landscape letterboxing as the primary experience.

## Portrait Mobile Layout

Target portrait mobile only unless the user explicitly requests another orientation.

Required mobile rules:

- Use `width=device-width, initial-scale=1, viewport-fit=cover`.
- Use `touch-action: none` on gameplay surfaces.
- Use `overscroll-behavior: none` and `overflow: hidden` for the page during play.
- Respect safe areas with `env(safe-area-inset-top)`, `env(safe-area-inset-bottom)`, `env(safe-area-inset-left)`, and `env(safe-area-inset-right)` where UI touches screen edges.
- Use touch-safe buttons of at least `44px` in both dimensions.
- Keep HUD and overlay text readable at `360px` viewport width.
- Do not place critical controls where mobile browser bars or notches can cover them.

## Grid And Board Fit

Grid games must derive board geometry from explicit bounds instead of eyeballed constants.

Required rules:

- Define a board rectangle with `boardX`, `boardY`, `boardW`, and `boardH`.
- Compute `cellSize` from the smaller of available width and height after gaps and padding.
- Compute board width as `cols * cellSize + (cols - 1) * gap` and board height as `rows * cellSize + (rows - 1) * gap`.
- Center the board within its rectangle and keep every tile inside board bounds.
- Clamp animated pieces, selection rings, glows, shadows, and particles so they do not visually spill into HUD or lower panels unless the effect is intentional and short-lived.
- Include a `validateLayout()` helper or equivalent assertions that check the last row and last column fit inside the board rectangle.

For match-3 games on `390x844`, prefer 7x7 or a carefully sized 8x8 board. An 8x8 board must reduce cell size and gaps enough to fit, rather than overflowing the frame.

## Portrait Screen Composition

Use the whole portrait screen with clear zones:

- Top zone: compact score, moves, target, pause/mute.
- Middle zone: main board or action playfield.
- Bottom zone: objective details, selected item info, boosters, combo meter, hint, or next-step prompt.

The lower 20% to 30% of the screen should not be empty during gameplay. If no active controls are needed, use that space for progress, objectives, level flavor, combo feedback, or helpful status.

## Main Loop

Use `requestAnimationFrame`. Prefer a fixed-step update for deterministic gameplay.

Required behavior:

- Clamp large frame deltas after tab switches.
- Accumulate time and step updates at a stable rate, such as 60 updates per second.
- Render once per animation frame.
- Skip gameplay updates while paused, on title screen, or after win/loss unless animations should continue.

Example timing model:

```js
const STEP = 1 / 60;
let lastTime = 0;
let accumulator = 0;

function frame(nowMs) {
  const now = nowMs / 1000;
  const delta = Math.min(0.05, now - lastTime || 0);
  lastTime = now;
  accumulator += delta;

  while (accumulator >= STEP) {
    update(STEP);
    accumulator -= STEP;
  }

  render(accumulator / STEP);
  requestAnimationFrame(frame);
}
```

## Game States

Use explicit states instead of scattered booleans.

Required states:

- `title`
- `playing`
- `paused`
- `won`
- `lost`

Optional states:

- `levelIntro`
- `transition`
- `settings`
- `credits`

Every state must define which inputs are accepted, whether gameplay updates run, and which overlay appears.

## Save Data

Use `localStorage` only for small optional data such as best score, unlocked level, mute preference, or accessibility preference.

Rules:

- Game must work if `localStorage` fails.
- Wrap reads and writes in `try/catch`.
- Keep save schema tiny and versioned when needed.
- Never require network or account login.

## Error And Performance Guardrails

- Avoid unbounded particles, enemies, or projectiles.
- Pool or cap short-lived objects when many are created.
- Keep all per-frame loops proportional to current active objects.
- Avoid layout reads during gameplay loop.
- Do not log continuously in the console.
- Provide clear fallback if audio cannot start before user interaction.

## Required Browser Checks

Before marking a generated game complete, verify these viewport sizes conceptually or with browser automation:

- `390x844` portrait mobile.
- `360x740` portrait mobile.
- Optional desktop fallback, only to confirm keyboard support does not break mobile layout.

Reject the game if text overlaps, buttons clip, canvas uses a landscape-first layout, touch controls are missing, a grid overflows its bounds, the lower screen is unused, or gameplay cannot be completed on portrait mobile.
