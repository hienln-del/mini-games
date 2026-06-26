# Review Checklist

Use this checklist after an AI generates the single HTML game in `output/`.

## File Location

- [ ] Generated game is stored in `output/`.
- [ ] Filename is lowercase kebab-case, such as `flappy-bird.html`.
- [ ] No extra source, asset, build, or dependency files were created.

## Launcher Integration

- [ ] `output/index.html` exists.
- [ ] Generated game appears in the inline `GAMES` array.
- [ ] Manifest entry includes `slug`, `title`, `file`, `genre`, `description`, `controls`, `status`, `tags`, and `createdAt`.
- [ ] Manifest `file` points to a sibling filename such as `flappy-bird.html`.
- [ ] Existing manifest entries were preserved.
- [ ] Launcher Play loads the game in the iframe.
- [ ] Launcher Open links directly to the game HTML file.
- [ ] Search/filter can find the game by title, genre, controls, or tags.

## Single-File Purity

- [ ] Output is one complete `.html` document.
- [ ] No external CSS, JavaScript, images, fonts, JSON, audio, or CDN dependencies.
- [ ] All CSS is inline.
- [ ] All JavaScript is inline.
- [ ] Game runs by opening the file directly in a browser.

## Portrait Mobile Target

- [ ] Game is designed for portrait mobile only.
- [ ] Internal resolution is 9:16-ish, such as `360x640`, `390x844`, or `414x736`.
- [ ] Game fills portrait screens without landscape letterboxing.
- [ ] Touch input is primary and works for all required actions.
- [ ] Keyboard controls are optional fallback, not required for mobile play.
- [ ] Page does not scroll during gameplay.
- [ ] UI respects safe-area insets where controls approach screen edges.
- [ ] Buttons are at least `44px` in both dimensions when visible.
- [ ] HUD, menus, and instructions fit at `360px` viewport width.
- [ ] Game is playable at `390x844` and `360x740` portrait viewports.

## Startup And Screens

- [ ] Title/menu appears first.
- [ ] Controls are visible before gameplay starts.
- [ ] Start action works.
- [ ] Pause works during gameplay.
- [ ] Win screen can appear.
- [ ] Loss screen can appear.
- [ ] Restart works after win or loss without page reload.
- [ ] Mute works and persists if the game saves preferences.

## Gameplay Completeness

- [ ] Core loop from the brief is implemented.
- [ ] If the user gave only a short request, missing design details were inferred into a complete game.
- [ ] Game defaults to finite completion unless user explicitly asked for endless mode.
- [ ] A content budget exists, such as gates, waves, levels, objectives, or time limit.
- [ ] Spawn logic and win logic both use the content budget.
- [ ] Player can complete a full session.
- [ ] Win condition is reachable.
- [ ] Loss condition is reachable.
- [ ] Game never continues in `playing` after all meaningful content is exhausted.
- [ ] No empty scrolling, exhausted spawns, or dead gameplay state occurs.
- [ ] Score, progress, timer, health, or objective updates correctly.
- [ ] Difficulty changes over time or across levels.
- [ ] No obvious soft lock exists.

## Flappy-Style Completion

- [ ] Tap/click is the primary input.
- [ ] If the target is 30 gates, at least 30 gates can spawn.
- [ ] Gates continue spawning until the score goal is reached.
- [ ] If gates stop spawning, game is already in `won`, `lost`, or another non-playing state.
- [ ] Bird/player cannot continue through empty space after the final gate.
- [ ] Win/loss/restart are all reachable on portrait mobile.

## Controls

- [ ] Keyboard controls work as documented.
- [ ] Movement/action input feels responsive.
- [ ] Pressed/released actions do not fire repeatedly by accident.
- [ ] Pause/restart/mute inputs do not conflict with gameplay.
- [ ] Pointer or touch controls work if included.

## Rendering And Resize

- [ ] Canvas displays correctly on portrait mobile size.
- [ ] Game remains playable after mobile viewport resize or browser UI changes.
- [ ] HUD text remains readable.
- [ ] No important text overlaps or leaves its container.
- [ ] Player, hazards, and rewards are visually distinct.

## Animation, VFX, And Audio

- [ ] Important events have clear feedback.
- [ ] Particles or effects do not hide gameplay.
- [ ] Screen shake, flash, and hit stop are brief and readable.
- [ ] WebAudio starts only after user interaction.
- [ ] Game still works if audio is blocked or muted.
- [ ] No rapid full-screen flashing.

## Accessibility And Usability

- [ ] Game can be played with keyboard on desktop.
- [ ] Critical information is not color-only.
- [ ] Text contrast is high enough to read.
- [ ] Font sizes are readable on small screens.
- [ ] Mute control is available.
- [ ] Failure and success are understandable.

## Browser Quality

- [ ] No console errors during normal play.
- [ ] No continuous console spam.
- [ ] No missing asset warnings.
- [ ] No severe frame drops during normal play.
- [ ] Page does not require a local server.

## Final Acceptance

Accept the generated game only if all critical items pass:

- [ ] One-file HTML purity.
- [ ] Complete playable loop.
- [ ] Clear controls.
- [ ] Reachable win/loss/restart.
- [ ] No broken assets.
- [ ] No runtime errors.
