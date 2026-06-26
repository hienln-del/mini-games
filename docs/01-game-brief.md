# Game Brief Template

Fill this document before using the generation prompt when you want control over the result. If the user only gives a short request, the AI should infer these fields internally and proceed without asking questions.

## Simple Request Expansion

When the request is short, such as `make flappy bird game`, infer a complete portrait-mobile arcade/puzzle brief before coding.

Required inference defaults:

- Choose a clear title and filename slug.
- Choose touch-first controls and optional keyboard fallback.
- Define finite win/loss rules unless the user explicitly asks for endless score attack.
- Define a content budget such as target score, gates, waves, levels, objectives, or time limit.
- Define scoring, difficulty ramp, spawn budget, and restart behavior.
- Choose readable procedural art and WebAudio sounds.
- Include title, gameplay, pause, win/loss or game-over, and restart screens.
- Ensure hazards, rewards, pipes, gates, waves, or objectives cannot run out while gameplay continues.
- Save the generated game to `output/<game-slug>.html`.

## Core Concept

- Game title: `[Short memorable title]`
- Genre: `[Arcade, puzzle, action puzzle, survival, score attack, platform puzzle, etc.]`
- One-sentence pitch: `[Player does X to achieve Y while avoiding Z]`
- Player fantasy: `[What the player should feel like: clever pilot, nimble thief, tiny wizard, etc.]`
- Target player: `[Casual, arcade fan, puzzle player, kids, speedrunner, etc.]`
- Session length: `[30 seconds, 2 minutes, 5 minutes, etc.]`
- Target screen: `Portrait mobile only, 9:16-ish viewport`

## Core Loop

Describe one repeatable loop in 3 to 5 steps.

1. `[Player observes current situation]`
2. `[Player makes a movement or action choice]`
3. `[Game reacts with risk, reward, or new obstacle]`
4. `[Player gains score, progress, power, or information]`
5. `[Difficulty increases or next challenge appears]`

## Controls

Use touch controls first. Add keyboard only as a desktop fallback.

- Move: `[tap lane / drag / swipe / virtual stick / none]`
- Primary action: `[tap / hold / release / swipe / drag]`
- Secondary action: `[Optional]`
- Desktop fallback: `[Arrow keys / WASD / Space / Enter, optional]`
- Pause: `P` or `Esc`
- Restart: `R`
- Mute: `M`

## Goals And Failure

- Win condition: `[Reach level, survive timer, solve board, collect all items, defeat boss]`
- Loss condition: `[Health reaches zero, timer expires, board locks, enemy catches player]`
- Score rules: `[Points for actions, combo rules, time bonus, accuracy bonus]`
- Content budget: `[Example: 30 gates, 6 waves, 5 levels, 90 seconds, 12 objectives]`
- Progression: `[Levels, waves, puzzle stages, increasing speed, new mechanics]`
- Completion invariant: `[Example: spawn gates until score reaches 30, then immediately trigger win]`

## World And Objects

- Player object: `[Shape, role, abilities, size, speed]`
- Main obstacle: `[Hazards, enemies, locked tiles, falling pieces]`
- Main reward: `[Coins, stars, gems, rescued units, solved cells]`
- Special objects: `[Powerups, switches, keys, portals, combo pieces]`
- Level shape: `[Single arena, scrolling map, grid, lanes, rooms, board]`

## Desired Feel

- Movement feel: `[Snappy, floaty, heavy, slippery, precise]`
- Difficulty feel: `[Relaxed, tense, escalating, strategic, chaotic]`
- Visual feel: `[Readable, bold, neon, paper cutout, toy-like, clean geometric]`
- Audio feel: `[Soft blips, crunchy arcade, musical tones, quiet ambience]`

## Required Screens

- Title/menu with title, controls, and start action.
- Gameplay HUD with score/progress and current objective.
- Pause overlay with resume/restart/mute instructions.
- Win screen with result, score, and restart action.
- Loss screen with result, score, and restart action.

## Non-Negotiables

List 3 to 7 things the generated game must include.

- `[Example: player must be able to dash]`
- `[Example: game must have 5 levels]`
- `[Example: no text-heavy tutorial]`

## Avoid

List anything the AI should not make.

- `[Example: no external images]`
- `[Example: no violent theme]`
- `[Example: no complex inventory]`
