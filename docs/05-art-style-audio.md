# Art Style And Audio

The generated game must create its visuals and sounds inside the single HTML file.

## Procedural Art Policy

Allowed asset methods:

- Canvas drawing primitives.
- Canvas-generated offscreen sprites.
- Inline SVG strings converted to data URIs.
- CSS gradients for page and overlay styling.
- Procedural patterns, noise, stars, tiles, or grids.
- WebAudio synthesis for sound effects and simple loops.

Forbidden asset methods:

- Remote images.
- Remote fonts.
- Remote audio.
- CDN libraries.
- Separate asset files.
- Base64 blobs copied from unknown sources without explanation.

## Art Direction Template

Define these before generation:

- Theme: `[Space garden, neon kitchen, clockwork dungeon, etc.]`
- Shape language: `[Circles friendly, triangles dangerous, squares stable]`
- Palette: `[5 to 8 colors with roles]`
- Background style: `[Grid, parallax dots, soft pattern, tile field]`
- Player silhouette: `[Readable shape and color]`
- Hazard silhouette: `[Distinct shape and color]`
- Reward silhouette: `[Distinct shape and color]`
- UI style: `[Flat, pixel, arcade, rounded panels, crisp labels]`

## Palette Rules

Use a small palette with assigned roles.

Recommended roles:

- Background dark or neutral.
- Playfield surface.
- Player primary.
- Player accent.
- Hazard color.
- Reward color.
- UI text.
- Success and failure colors.

Do not use color alone to identify hazards or rewards. Pair color with shape, motion, or icon pattern.

## Readability Rules

- Player must stand out at a glance.
- Hazards must be visually distinct from rewards.
- Projectiles and moving threats must contrast with background.
- UI text must remain readable over gameplay.
- Avoid excessive bloom, blur, or opacity stacking.
- Keep camera and effects from hiding exact positions.

## Procedural Sprite Guidance

Use helper functions to draw repeated objects.

Examples:

- `drawPlayer(ctx, player, t)`
- `drawEnemy(ctx, enemy, t)`
- `drawGem(ctx, gem, t)`
- `drawHazard(ctx, hazard, t)`
- `drawButton(ctx, label, rect, state)`

For richer visuals, generate small offscreen canvases once and draw them repeatedly. This keeps the file self-contained while avoiding expensive redraw logic.

## Audio Policy

Use WebAudio for procedural sound. Audio must start only after user interaction due to browser autoplay rules.

Recommended sounds:

- Menu confirm.
- Pickup.
- Damage.
- Jump, dash, rotate, or swap.
- Combo increase.
- Level clear.
- Win.
- Loss.

Audio rules:

- Include mute toggle.
- Keep sounds short and non-irritating.
- Use volume envelopes to prevent clicks.
- Avoid continuous loud tones.
- Use simple oscillator, gain, filter, and noise nodes.
- If audio creation fails, game still plays silently.

## Music

Music is optional. If included, generate a simple loop with WebAudio and keep it subtle.

Recommended approach:

- Start music after first interaction.
- Use a tiny note pattern or ambient pulse.
- Lower volume under sound effects.
- Respect mute setting.
