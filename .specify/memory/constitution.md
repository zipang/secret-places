<!--
Sync Impact Report:
- Version change: 1.6.1 → 1.6.2
- Modified sections:
    - None (Template-only change)
- Templates requiring updates:
    - ✅ .specify/templates/tasks-template.md
- Follow-up TODOs: None
-->
# silent-places Constitution

## Core Principles

### I. Mobile-First PWA
The project is a mobile-first progressive web app (PWA), ensuring a seamless experience on all devices.

### II. Perfect Lighthouse scores
The application must be optimized for speed, accessibility with the goal of achieving a perfect 100 in every Lighthouse performance category.

### IV. Keep It Stupid Simple (KISS)
All design and implementation decisions must follow the "Keep It Stupid Simple" (KISS) principle.

### V. Architecture
The codebase will adhere to a simplified interpretation of Clean Code and Atomic Design principles to ensure a decoupled, maintainable, and scalable component architecture.
-   **Layered Components:** A strict layering system is enforced. Application-level components (e.g., pages, organisms) MUST only be built by composing components from the `base` and `ui` layers.
-   **`src/components/base`:** This directory contains foundational layout components and "atoms" (e.g., `Container`, `HStack`, `Text`). These are the ONLY components allowed to directly use the underlying UI library (e.g., Chakra UI, Material UI) and are solely responsible for applying the project's design system (colors, typography, etc.).
-   **`src/components/ui`:** This directory contains interactive UI elements and "molecules" (e.g., `Button`, `Card`, `Select`), which are composed from `base` components.
-   **Strict Encapsulation:** Higher-level components (pages, organisms) MUST NOT directly access the underlying UI library. This encapsulation ensures that the UI library can be swapped without refactoring the entire application.

### VI. Local Content
All application text (menus, sections, etc.) is managed as code and commited inside the git repository. Content is stored in Markdown files with front-matter inside the `src/content` directory. This approach enables version control, collaboration, and compatibility with git-based CMS workflows. Internationalization (i18n) is handled via language-specific subfolders (e.g., `src/content/en`, `src/content/fr`).

### VII. Web Standards First
To maintain simplicity and leverage the modern web platform, this project exclusively targets evergreen browsers. Development MUST prioritize standardized, modern web APIs (e.g., `fetch`) over obsolete or non-standard alternatives. Any third-party library that relies on polyfills or deprecated features MUST be avoided to ensure the smallest possible bundle size and adherence to web standards.

### VIII. Documented & Readable Code
Code is written for humans first.
-   **JSDoc:** Every function and method MUST have a JSDoc block explaining its purpose and parameters.
-   **Component Props:** All component props MUST be defined in an interface, with each property having a clear JSDoc description.
-   **Naming:** Variable and function names MUST be clear and self-explanatory.
-   **Directory Documentation:** Every key directory MUST contain a `README.md` file that explains the contents, purpose, and any rules associated with that directory.

## Technical Stack

To align with our principles of Performance and Simplicity (KISS), the following technical stack is mandated:

*   **Language:** TypeScript is the single language for both backend and frontend code.
*   **Runtime & Tooling:** `bun` is the exclusive runtime, test runner, and builder. All scripts in `package.json` MUST be executed via `bun`.
*   **Content:** `content-collections` is used to validate and load all application content from local Markdown files.
*   **Schema Validation:** `arktype` is the standard library for all data and schema validation.
*   **Testing:** Unit tests MUST use the `bun test` API. Test files will be co-located with their corresponding source files and use the `.spec.ts` extension.
*   **Linting/Formatting:** BiomeJS will be used for all code linting and formatting, replacing any other tools like ESLint or Prettier.

## Development Standards

* **Testing:** To maintain simplicity, unit tests are required only for core business logic and utility functions (e.g., in `src/lib` or `src/utils`). UI components and pages will not have dedicated tests. Test files MUST use the `bun test` API, be named `*.spec.ts`, and be co-located with the source file.
* **Code Style:** A consistent code style will be enforced using automated tools.

## Workflow

* **Version Control:** All code changes will be managed through a Git repository.

## Governance

This constitution is the single source of truth for project principles. Any amendments must be proposed and agreed upon by the team.

**Version**: 1.6.2 | **Ratified**: 2025-10-16 | **Last Amended**: 2025-10-16