# Connect Four Game Architecture & Documentation

## Component Architecture Diagram

```mermaid
graph TD
  A["index.html (UI Entry Point)"]
  B["game.js (Game Logic)"]
  C["game.css (Game Styles)"]
  D["translations.js (Game Translations)"]
  E["manifest.json (PWA Manifest)"]
  F["service-worker.js (Offline Support)"]
  G["../css/common.css (Shared Styles)"]
  H["../js/common.js (Shared JS)"]
  I["Shared translations.js (Root)"]

  A --> B
  A --> C
  A --> D
  A --> E
  A --> F
  A --> G
  A --> H
  B --> D
  B --> H
  B --> G
  F --> G
  F --> H
  H --> I
  C --> G
  D --> I
```

## User Flow Diagram

```mermaid
flowchart TD
    Start([User loads Connect Four page])
    Start --> UI[UI rendered from index.html]
    UI --> Controls[User clicks New Game]
    Controls --> NewGame[game.js initializes board]
    NewGame --> Board[Board displayed, user clicks cell]
    Board --> Drop[Disc drops, board updates]
    Drop --> Check[Game checks for win/draw]
    Check --> Win[User/computer wins]
    Check --> Draw[Game is a draw]
    Check --> NextTurn[Switch player, continue]
    Win --> Overlay[Show win message/animation]
    Draw --> Overlay[Show draw message]
    Board --> PWA[User installs as PWA]
    PWA --> Offline[Service worker enables offline play]
```

---

## File Roles & Structure

- **index.html**: Sets up the UI, loads all resources, integrates PWA features, and initializes the game.
- **game.js**: Handles board creation, user input, game state, AI opponent, win/draw logic, and animations.
- **game.css**: Styles the board, cells, controls, and win/draw overlays. Responsive and animated.
- **translations.js**: Provides all UI text in 12 languages for full localization.
- **manifest.json**: Configures PWA installability, icons, and theme.
- **service-worker.js**: Caches files for offline play and updates cache as needed.
- **../css/common.css**: Shared styles for consistent look and feel.
- **../js/common.js**: Shared language, i18n, and release note utilities.

---

## Game Rules, Controls, and User Interactions

- **Goal**: Drop discs into a 7x6 grid to connect four of your color in a row (horizontally, vertically, or diagonally) before the computer does.
- **Controls**:
  - Click a column to drop your disc
  - New Game: Reset the board
  - Language selection (via shared/common.js, if enabled)
- **Feedback**:
  - Animated disc drops
  - Win/draw messages and overlays
  - Computer opponent moves automatically

---

## Unique Features & PWA Aspects

- Fully localized UI (12 languages)
- Responsive and mobile-friendly design
- PWA installability and offline support
- Animated overlays and feedback (fireworks, proud computer)
- AI opponent using minimax algorithm
- Uses shared resources for consistency

---

## Notable Implementation Details

- Board is a 2D array, rendered as a grid of clickable cells
- Minimax-based AI for computer moves
- CSS variables and shared styles for maintainability
- Modular JS with global event handling and error management
- Service worker caches all required files for offline play
- Easily extensible for new features, translations, or UI improvements 