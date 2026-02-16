# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Leah's Websites is a collection of browser-based games built with vanilla HTML, CSS, and JavaScript. No build tools, frameworks, or npm dependencies are used.

## Running the Project

Open any `.html` file directly in a browser, or use a local server:

```bash
python -m http.server 8000
# Then visit http://localhost:8000/index.html
```

## Architecture

### Entry Points
- **`index.html`** - Main game hub that renders games from a `GAMES` array and links to individual game files
- **`all-games.html`** - Alternative launcher that embeds games as base64 strings and runs them in sandboxed iframes via blob URLs

### Individual Games
Games are located in the `games/` subdirectory. Each game is a **self-contained single HTML file** with embedded CSS and JavaScript:
- `games/math-game.html` - Octo-Math: turn-based math quiz with Canvas confetti effects
- `games/ski-game.html` - Ski & Snow: real-time 2D action game with Canvas rendering and physics

### Common Patterns

**Screen Management:** Multiple divs toggled with `.hidden` class

**Game Loop:** `requestAnimationFrame` for animation/physics

**State:** Simple `let/const` variables, high scores persisted to `localStorage`

**Input:** Direct `addEventListener` for keyboard + touch button overlays for mobile

**Styling:** CSS custom properties (`:root`), gradients, glassmorphism, responsive via `clamp()` and viewport units

### Adding a New Game

1. Create a new self-contained HTML file in `games/` following the existing game structure
2. Add an entry to the `GAMES` array in `index.html`:
```javascript
{
  id: 'my-game',
  title: 'My Game',
  desc: 'Game description',
  icon: '🎮',
  theme: 'blue',
  url: 'games/my-game.html'
}
```

## Project Standards

### Game Index Requirements

- **All games must be linked from `index.html`** - This file serves as the central directory for accessing every game in the project.
- When adding a new game, you **must** also update `index.html` to include an entry in the `GAMES` array.
- No game should exist in isolation without being discoverable from the main hub.

### Mobile Optimization Standards

- **All pages must be optimized for mobile devices**, including `index.html` and individual game pages.
- Design layouts so key content is visible "above the fold" whenever reasonably possible.
- If the list of games grows long:
  - Use a responsive layout (e.g., two columns on mobile where appropriate)
  - Make the list scrollable in a clean and user-friendly way
  - Avoid layouts that require excessive vertical scrolling before users can see available games
- Use touch-friendly controls: buttons sized appropriately for touch input, adequate spacing between interactive elements.

### Shared Components and Styling

- **Reuse common UI components** across games whenever possible (e.g., instructional modals, back buttons, settings panels).
- **Extract shared styles** into a common `/css` folder instead of duplicating styles across individual game files.
- Keep shared components consistent in design and behavior across the project.
- Prefer modular, reusable CSS and utility patterns to reduce duplication and improve maintainability.
- When creating new shared components, document their usage and expected behavior.
