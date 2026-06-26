# Animation And VFX

Animation and effects should make the game easier to read and more satisfying without hiding gameplay information.

## Animation Principles

Use short, purposeful motion:

- Idle motion for alive objects.
- Anticipation before strong attacks, spawns, or hazards.
- Squash and stretch on jumps, bounces, hits, and landings.
- Ease-out on score pops and pickups.
- Quick transitions between states.

Keep gameplay-critical objects readable at all times.

## Timing Defaults

Recommended durations:

- Button or HUD pulse: `80ms` to `160ms`.
- Pickup burst: `200ms` to `400ms`.
- Hit flash: `80ms` to `120ms`.
- Screen shake: `100ms` to `250ms`.
- Hit stop: `40ms` to `90ms`.
- Level transition: `300ms` to `700ms`.

Use shorter timings for arcade action and slightly longer timings for puzzle clarity.

## Particles

Use particles for feedback events:

- Pickup collected.
- Enemy defeated.
- Player damaged.
- Combo gained.
- Level completed.
- Hazard impact.

Particle rules:

- Cap total active particles.
- Remove particles when lifetime reaches zero.
- Use simple circles, squares, streaks, triangles, or small sprite stamps.
- Use color tied to event type.
- Do not cover hazards or player during active play.

## Screen Shake

Use screen shake sparingly.

Good triggers:

- Player hit.
- Heavy landing.
- Large combo.
- Boss or wave clear.
- Explosion or wall impact.

Rules:

- Keep shake amplitude small enough to preserve readability.
- Scale shake by event strength.
- Disable or reduce shake if accessibility setting exists.
- Never use constant shake as background decoration.

## Hit Stop

Hit stop is a tiny freeze after a strong impact.

Use it for:

- Successful dash hit.
- Enemy defeat.
- Perfect match or clear.
- Player damage.

Rules:

- Freeze gameplay updates, not UI input needed for pause.
- Keep duration under `100ms`.
- Combine with sound and particle burst.

## Transitions

Use transitions to communicate state changes.

Examples:

- Fade from title to gameplay.
- Slide or scale overlay for pause.
- Burst and slow motion on win.
- Desaturate or dim background on loss.
- Countdown before level starts.

Transitions must not block restart or pause controls longer than necessary.

## Visual Feedback Checklist

Every important action should have at least two feedback channels:

- Visual change.
- Sound effect.
- Motion change.
- HUD update.
- Particle or flash.
- Brief text callout.

Examples:

- Pickup: object disappears, particle burst, score floats, sound plays.
- Damage: player flashes, health changes, shake happens, sound plays.
- Level clear: confetti burst, objective text changes, fanfare plays.

## Premium Special Effects

Special items should feel valuable, not like plain debug marks.

Use layered effects:

- Anticipation: brief pulse, glow, scale-up, or charge ring before activation.
- Action: directional beam, row/column sweep, radial burst, lightning arc, color wave, or shock ring.
- Board reaction: affected cells flash, shake, lift, pop, or dissolve in sequence.
- Reward: score ticks, combo text, particles, and sound rise with effect size.
- Afterglow: short sparkle trail or fading residue that does not block gameplay.

Match-3 special candy expectations:

- Striped candy: visible stripes wrapped around the candy, plus a full row or column sweep when triggered.
- Wrapped/bomb candy: swelling pulse, radial blast, screen bump, and ring particles.
- Color bomb: prismatic glow, color-linked arcs to matching candies, then staggered pops.
- Special combinations: larger combined effect with clear order and capped duration.

Avoid cheap effects:

- A single white line drawn on top of the candy.
- Static icons with no activation animation.
- Particles that appear unrelated to the cleared cells.
- Effects that hide the board for too long or make cleared cells unclear.
