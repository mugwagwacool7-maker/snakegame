# Snake

A single-file browser version of classic Snake. No build step, no dependencies — open `snake.html` in any browser and play.

## Play

Open `snake.html` in a web browser (double-click the file, or drag it into a browser tab).

**Controls**
- Arrow keys or `WASD` to move
- `Space` to start/restart after game over
- On-screen arrow buttons for touch/mobile

**Rules**
- Eat the orange fruit to grow one segment and score 10 points
- The game speeds up slightly with each fruit eaten
- Hitting a wall or your own body ends the run
- Your best score is tracked for the current session (resets on page reload)

## Files

| File | Purpose |
|---|---|
| `snake.html` | The entire game — HTML, CSS, and JavaScript in one file |

## How it works

- Rendered on an HTML `<canvas>` (400×400px, 20×20 grid of 20px cells)
- Game loop runs on `setTimeout`, re-scheduling itself each tick at the current speed (`tickMs`), which decreases (down to a 60ms floor) as the snake eats
- Snake is stored as an array of `{x, y}` grid coordinates; moving = unshift a new head, and pop the tail unless fruit was just eaten (that's what makes it grow)
- Fruit spawns at a random grid cell, re-rolling if it lands on the snake
- Direction changes are buffered (`nextDir`) and applied on the next tick, with a check to block reversing directly into the snake's own body

## Customizing

A few constants near the top of the `<script>` block make it easy to tweak:

```js
const CELL = 20;   // pixel size of each grid cell
const COLS = 20;   // board width in cells
const ROWS = 20;   // board height in cells
```

And in `resetState()`:

```js
tickMs = 130;      // starting speed in ms per tick (lower = faster)
```

## Ideas for extending it

- Persist best score across sessions (e.g. `localStorage`, if running outside a sandboxed environment)
- Add walls/obstacles or a second fruit type worth more points
- Wrap-around edges instead of wall collision
- Add a pause key
