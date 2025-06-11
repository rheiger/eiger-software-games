# 15 Puzzle Game Architecture & Documentation

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
    Start([User loads 15 Puzzle page])
    Start --> UI[UI rendered from index.html]
    UI --> Controls[User selects puzzle type, shuffles, or solves]
    Controls --> NewGame[game.js initializes board]
    NewGame --> Board[Board displayed, user moves tiles]
    Board --> Move[User moves a tile]
    Move --> Check[Game checks for win]
    Check --> Win[User solves puzzle]
    Win --> Overlay[Show congratulations overlay]
    Controls --> Solve[User requests computer solve]
    Solve --> Computer[Computer solves puzzle]
    Board --> PWA[User installs as PWA]
    PWA --> Offline[Service worker enables offline play]
```

---

## File Roles & Structure

- **index.html**: Sets up the UI, loads all resources, integrates PWA features, and initializes the game.
- **game.js**: Handles board creation, user input, game state, tile movement, shuffling, computer solving, and win logic.
- **game.css**: Styles the board, tiles, controls, overlays, and ensures responsive design.
- **translations.js**: Provides all UI text in 12 languages for full localization.
- **manifest.json**: Configures PWA installability, icons, and theme.
- **service-worker.js**: Caches files for offline play and updates cache as needed.
- **../css/common.css**: Shared styles for consistent look and feel.
- **../js/common.js**: Shared language, i18n, and release note utilities.

---

## Game Rules, Controls, and User Interactions

- **Goal**: Arrange the tiles in order (1-8 or 1-15) by sliding them into the empty space. Solve the puzzle in as few moves as possible.
- **Controls**:
  - Select puzzle type (8 or 15)
  - Shuffle: Randomize the board
  - Solve: Let the computer solve the puzzle
  - Move tiles by clicking
  - Language selection (via shared/common.js, if enabled)
- **Feedback**:
  - Move counters for player, random, and computer moves
  - Congratulations overlay when solved
  - Computer solving progress and giving up message

---

## Unique Features & PWA Aspects

- Option for 8-puzzle or 15-puzzle
- Computer can solve the puzzle (with progress feedback)
- Fully localized UI (12 languages)
- Responsive and mobile-friendly design
- PWA installability and offline support
- Uses shared resources for consistency

---

## Notable Implementation Details

- Board is dynamically rendered for each puzzle type
- Computer solver uses advanced search algorithms (IDA*, heuristics)
- Modular JS with global event handling and error management
- Service worker caches all required files for offline play
- Easily extensible for new features, translations, or UI improvements 