# Shared Resources Documentation

This document provides a comprehensive overview of the shared resources used across the Eiger Software Game Collection. It covers the purpose, structure, usage, and improvement opportunities for each shared resource, and offers guidance for developers.

---

## 1. css/common.css

**Purpose:**
- Provides shared styling for all games and the main entry point.

**Key Features:**
- Uses CSS variables for color palette and UI constants (e.g., --primary-color, --secondary-color, --text-color).
- Implements modern, responsive design with Flexbox and animated backgrounds.
- Styles for language selector, release notes, and consistent UI components.
- Color scheme: blue (primary), green (secondary), red (highlight), orange (tiles), etc.
- Accessibility: high-contrast text, interactive button states.

**Usage:**
- All games and the entry point import this file for consistent look and feel.
- Developers should use the defined CSS variables for colors and UI elements.

**Improvement Opportunities:**
- Consider modularizing styles for easier maintenance.
- Add comments for custom classes and variables.

---

## 2. js/common.js

**Purpose:**
- Provides shared JavaScript utilities for language selection, internationalization, and release notes display.

**Key Features:**
- Defines supported languages and their metadata (emoji, name).
- Dynamically creates language selection buttons and manages language switching.
- Dispatches a custom `languageChanged` event for games to react to language changes.
- Handles release/version notes display and initialization.
- Exposes key functions globally (`detectLanguage`, `getMessage`, `setLanguage`).

**Usage:**
- Used by the main entry point and all games for consistent language and release note handling.
- Relies on a global `translations` object (from translations.js) and a `releaseInfo` object for version notes.

**Improvement Opportunities:**
- Modularize further for tree-shaking or per-game customization.
- Improve error handling for missing translation keys or DOM elements.
- Add JSDoc comments for public functions.

---

## 3. translations.js

**Purpose:**
- Contains all UI translation strings for the entry point and shared UI.

**Key Features:**
- Supports 12 languages (en, de, fr, it, sv, sk, es, pt, no, fi, pl, cs).
- Each language has a consistent set of keys (e.g., title, welcome, sudokuBtn, etc.).
- Used by js/common.js and referenced via `data-i18n` in HTML.

**Usage:**
- All games and the entry point use this file for multi-language support.
- Developers should add new keys to all languages for consistency.

**Improvement Opportunities:**
- Extract translation keys to a constants file for easier maintenance.
- Add comments or documentation for translators.
- Expand to support more UI elements or error messages as needed.

---

## 4. Guidance for Developers

- **Use the shared resources for all new games and UI components to ensure consistency.**
- **When adding new UI elements or features:**
  - Add corresponding styles to `css/common.css` using CSS variables.
  - Add utility functions to `js/common.js` if they are shared across games.
  - Add new translation keys to all languages in `translations.js`.
- **Test shared resources in isolation and in the context of each game.**
- **Document any new shared resource or significant change in this file.**

---

**Summary:**
- All shared resources are well-structured and support modular, multi-language, and maintainable development.
- No missing translation keys were found in the main shared translations.js.
- Improvement opportunities are minor and mostly relate to maintainability and documentation. 