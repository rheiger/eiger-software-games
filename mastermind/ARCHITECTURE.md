# Mastermind Game Architecture & Documentation

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
    Start([User loads Mastermind page])
    Start --> UI[UI rendered from index.html]
    UI --> Options[User selects game mode/difficulty]
    Options --> NewGame[game.js initializes board and secret code]
    NewGame --> Board[Board displayed, user places pegs]
    Board --> Guess[User submits guess]
    Guess --> Feedback[Game provides feedback]
    Feedback --> Win[User cracks the code]
    Feedback --> NextAttempt[User tries again]
    Win --> Overlay[Show win message]
    NextAttempt --> Board
    Board --> GiveUp[User gives up]
    GiveUp --> Reveal[Game reveals code]
    Board --> PWA[User installs as PWA]
    PWA --> Offline[Service worker enables offline play]
```

---

## File Roles & Structure

- **index.html**: Sets up the UI, loads all resources, integrates PWA features, and initializes the game.
- **game.js**: Handles board creation, user input, game state, code generation, feedback, and win/loss logic.
- **game.css**: Styles the board, pegs, controls, overlays, and ensures responsive design.
- **translations.js**: Provides all UI text in 12 languages for full localization.
- **manifest.json**: Configures PWA installability, icons, and theme.
- **service-worker.js**: Caches files for offline play and updates cache as needed.
- **../css/common.css**: Shared styles for consistent look and feel.
- **../js/common.js**: Shared language, i18n, and release note utilities.

---

## Game Rules, Controls, and User Interactions

- **Goal**: Guess the secret code (colors or digits) in as few attempts as possible. Feedback is given after each guess (black/white pegs for correct color/digit and position).
- **Controls**:
  - Select game mode (colors/digits, with/without repetition, code length)
  - Place pegs by clicking or dragging
  - Submit guess
  - Restart game
  - Give up to reveal the code
  - Language selection (via shared/common.js, if enabled)
- **Feedback**:
  - Black/white pegs for guess accuracy
  - Win/loss messages and overlays

---

## Unique Features & PWA Aspects

- Multiple game modes (colors, digits, repetition, code length)
- Fully localized UI (12 languages)
- Responsive and mobile-friendly design
- PWA installability and offline support
- Drag-and-drop and click placement of pegs
- Uses shared resources for consistency

---

## Notable Implementation Details

- Board is dynamically rendered for each attempt
- Secret code generation supports multiple modes
- Modular JS with global event handling and error management
- Service worker caches all required files for offline play
- Easily extensible for new features, translations, or UI improvements 