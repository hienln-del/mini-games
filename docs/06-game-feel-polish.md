# Game Feel And Polish

Game feel is the difference between functional and satisfying. The generated game should respond quickly, clearly, and fairly.

## Responsiveness

Required defaults:

- Immediate response to movement input.
- No input lag from animations or transitions during gameplay.
- Restart works without page reload.
- Pause works during active gameplay.
- Pointer/touch controls do not fight browser scrolling.

For action games, allow tiny forgiveness features when relevant:

- Input buffering for jump, dash, swap, or fire actions.
- Coyote time for platformer jumps.
- Grace period after player damage.
- Slight magnetism for collectibles.
- Forgiving collision against hazards.

## Movement Feel

Choose one movement identity and tune around it.

Examples:

- Snappy grid movement: instant tile steps, buffered turns, clear landing tick.
- Smooth arcade movement: acceleration, friction, max speed, gentle turning.
- Platform movement: gravity, jump cut, coyote time, landing squash.
- Puzzle cursor: crisp selection, hover highlight, swap pulse.

Do not mix conflicting movement models unless the brief asks for it.

## Camera And Framing

Use a stable camera by default.

Camera rules:

- Keep player and threats visible.
- Avoid nausea-inducing motion.
- Use small camera lead only if helpful.
- Use shake as temporary offset, then restore cleanly.
- Keep HUD independent from world camera.

## UI Feel

Menus and overlays should be quick and clear.

Required polish:

- Title screen shows goal and controls.
- Buttons or prompts react to hover, focus, click, or key confirm.
- HUD pulses when score, health, timer, or objective changes.
- Pause overlay dims gameplay but leaves context visible.
- Win/loss screen shows final score and restart instruction.

## Difficulty Feel

The first 10 seconds should teach the core action safely. Difficulty should rise after the player has seen the mechanic.

Good ramp methods:

- Increase speed gradually.
- Add one new hazard at a time.
- Reduce available time slightly.
- Combine old mechanics after they are understood.
- Reward skill with combo opportunities.

Avoid unfair difficulty spikes, invisible hazards, instant unavoidable failure, or random outcomes that override skill.

## Juice Checklist

Add these where relevant:

- Pickup burst.
- Score pop text.
- Tiny squash/stretch on player action.
- Hit flash.
- Short hit stop on major impact.
- Screen shake on strong events.
- Button/HUD pulse.
- Level clear celebration.
- Distinct win and loss audio.
- Best score celebration.

## Finish Quality Bar

The generated game should feel complete after one pass.

Minimum finish bar:

- Player understands what to do within 5 seconds.
- Controls are visible before play starts.
- Every state has a way forward.
- Failure is clearly explained by visuals or rules.
- Success feels different from normal play.
- Game remains playable after resizing window.
- No missing art, missing audio, or console errors.
