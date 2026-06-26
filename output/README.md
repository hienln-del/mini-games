# Output Folder

Generated single-file HTML games belong in this folder. `index.html` is the launcher that wires them together.

Expected format:

- `output/<game-slug>.html`
- One complete self-contained HTML document per game.
- No external assets, dependencies, or build files.
- One manifest entry per game inside `output/index.html`.
- Existing manifest entries must be preserved when adding a new game.

Example:

- `output/flappy-bird.html`

Launcher manifest shape:

```js
{
  slug: 'flappy-bird',
  title: 'Flappy Bird',
  file: 'flappy-bird.html',
  genre: 'Arcade',
  description: 'Short summary of the game.',
  controls: 'Space/click/tap to flap. P pauses. R restarts. M mutes.',
  status: 'Playable',
  tags: ['one-button', 'score attack'],
  createdAt: '2026-06-26'
}
```
