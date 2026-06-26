# Game Systems

Use this document to specify the behavior expected inside the generated game.

## Input System

Input must be responsive, remappable in code, and easy to understand.

Required features:

- Treat touch/pointer input as primary for generated games.
- Support tap, hold, drag, or swipe according to the game genre.
- Keep touch targets at least `44px` square when visible controls exist.
- Track key down, key pressed this frame, and key released this frame.
- Support arrow keys and WASD as optional desktop fallback when movement exists.
- Support `Space` or `Enter` as optional desktop fallback for menu confirm and primary action.
- Support `P` or `Esc` for pause.
- Support `R` for restart after win/loss.
- Support `M` for mute.
- Prevent page scroll and browser gesture conflicts during active play.

Input should be ignored or remapped per state. For example, movement should not affect the player on the title screen.

## Entity Model

Represent active gameplay objects as entities with explicit properties.

Common fields:

- `x`, `y`: position.
- `vx`, `vy`: velocity when movement exists.
- `w`, `h` or `radius`: collision size.
- `type`: object category.
- `alive`: removal flag.
- `timer`: local animation or lifetime.

Keep entity behavior readable. Use helper functions for spawning, collision checks, and removal.

## Physics And Collision

Choose collision based on game shape:

- Circle collision for free-moving arcade objects.
- Axis-aligned rectangles for platformers and tile hazards.
- Grid coordinates for puzzle boards.
- Swept or stepwise collision for fast projectiles when needed.

Collision rules must be deterministic and visible to the player. Hitboxes should match visuals closely enough to feel fair. Favor generous player collision for rewards and slightly forgiving collision for hazards.

## Scoring And Rewards

Score should reinforce desired play.

Use combinations of:

- Base points for collecting, clearing, solving, surviving, or defeating.
- Combo multiplier for repeated skillful actions.
- Time bonus for fast completion.
- Accuracy or health bonus for clean play.
- Best score saved locally.

Show score changes with floating text, particles, sound, or HUD pulse.

## Levels And Difficulty

Progression should be understandable and finite unless the user explicitly asks for endless score attack.

Recommended structures:

- 5 to 10 designed waves for small arcade games.
- 3 to 6 puzzle levels for mechanic-focused games.
- Endless mode only when explicitly requested, with continuous spawning and clear difficulty ramp.

Difficulty can increase through speed, density, spawn rate, target count, puzzle constraints, or mixed hazards. Introduce one major idea at a time.

## Completion And Spawn Invariants

Every game must prove through its own logic that it cannot become empty while still playing.

Required rules:

- Declare a content budget constant, such as `TARGET_COUNT`, `TOTAL_WAVES`, `LEVELS`, `TIME_LIMIT`, or `TOTAL_OBJECTIVES`.
- Connect spawn logic and win logic to that same budget.
- If the game is finite, trigger `won` when the objective is complete and stop gameplay updates cleanly.
- If the game is endless, keep spawning meaningful hazards, rewards, and objectives indefinitely.
- Never let `playing` continue after all waves, gates, pipes, enemies, rewards, or objectives are exhausted.
- Include a `validateProgression()` helper or equivalent startup/runtime sanity check when content is generated.

Flappy-style games must follow these rules:

- Tap/click is the primary input.
- If the goal is 30 gates, at least 30 gates must be spawnable.
- New gates must continue spawning until the score goal is reached.
- If spawning stops, the game must already be in `won`, `lost`, or another non-playing end state.
- Do not allow empty scrolling after the last pipe or gate.

## Win, Loss, Pause, Restart

Required behavior:

- Title screen starts fresh game.
- Pause freezes gameplay and shows resume/restart/mute controls.
- Win screen appears immediately after objective completion.
- Loss screen appears immediately after failure.
- Restart resets all gameplay state without reloading the page.
- Mute works before and during gameplay.

Avoid soft locks. The player must always have a clear action after win, loss, or pause.

## HUD And Feedback

HUD must show only information needed for play.

Common HUD items:

- Score.
- Lives or health.
- Timer.
- Level, wave, or progress.
- Current objective.
- Combo or powerup duration.

HUD changes should animate lightly when values change.

## Accessibility Basics

Include these by default:

- Clear text labels for controls.
- High contrast between player, hazards, rewards, and background.
- Avoid relying on color alone for critical information.
- Include mute toggle.
- Avoid rapid full-screen flashing.
- Keep font sizes readable on small screens.
- Provide keyboard-only play for desktop.
