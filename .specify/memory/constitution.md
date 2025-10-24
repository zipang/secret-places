<!--
Sync Impact Report:
- Version change: 1.6.2 → 1.7.0
- Modified sections:
    - I. Mobile-First PWA → Combined into Best Practices
    - II. Perfect Lighthouse scores → Combined into Best Practices
    - VII. Web Standards First → Combined into Best Practices
- Added sections: None
- Removed sections: None
- Templates requiring updates:
    - ⚠ .specify/templates/plan-template.md
    - ⚠ .specify/templates/spec-template.md
    - ⚠ .specify/templates/tasks-template.md
- Follow-up TODOs: Update templates to align with the new "Best Practices" principle.
-->

# silent-places Constitution

## Core Principles

### Mobile-First PWA
The application is designed as a mobile-first progressive web app (PWA). This approach provides several key benefits:

- **Installability**: Users can install the application on their desktop or mobile devices, making it accessible directly from their home screen without relying on a browser.
- **App-Like Performance**: PWAs deliver a native app-like experience, including offline functionality and smooth interactions, by leveraging service workers and caching strategies.
- **Cross-Platform Compatibility**: A single codebase based on Web technologies instead of native UI components ensure good support across different devices and platforms, reducing development and maintenance overhead.

### Best Practices
The project aligns to current best practices to ensure a high-quality user experience and achieve an optimal score of 100 in every Lighthouse categories. These include:

- **Speed Optimization**: The application must prioritize perceived speed by minimizing initial load times. This includes:
  - Using deferred scripts to load non-critical resources after the main content.
  - Leveraging service workers for caching and offline support.
  - Instant pages transitions by using links preload strategies.
  - Optimizing assets (e.g., images, stylesheets) to reduce payload size.

- **Accessibility**: The application must adhere to accessibility standards to ensure inclusivity. This includes:
  - Implementing ARIA (Accessible Rich Internet Applications) roles and attributes.
  - Ensuring keyboard navigability with clear focus states and screen reader compatibility.
  - Providing sufficient color contrast and scalable text.

- **SEO Best Practices**: The application must follow SEO guidelines to improve discoverability. This includes:
  - Using semantic HTML to structure content meaningfully (`<nav>`, `<aside>`, `<main>`, `<header>`, `<section>`, `<article>`, ...).
  - Providing meta tags for titles, canonical URL, descriptions, and Open Graph data for sharing.
  - Ensuring fast page load times to improve search engine rankings.

- **Web Standards**: Ensure usage of standardized, modern web APIs (e.g., `fetch`) over obsolete or non-standard alternatives (e.g., `axios`, `XMLHttpRequest`). Third-party libraries that rely on polyfills or deprecated features must be avoided to ensure the smallest possible bundle size and adherence to web standards. Target evergreen browsers only.

### IV. Keep It Stupid Simple (KISS)
All design and implementation decisions must follow the "Keep It Stupid Simple" (KISS) principle.

### V. Architecture

The codebase will adhere to a simplified interpretation of Clean Code and Atomic Design principles to ensure a decoupled, maintainable, and scalable architecture. The architecture is structured as follows:

#### **Frontend: Atomic Design Principles**
The frontend components are organized following the Atomic Design principles to provide a clear hierarchy:

```
src/
├── components/
│   ├── base/         # (Atoms) Foundational layout components
│   │   ├── Container
│   │   ├── Grid
│   │   ├── HStack
│   │   ├── VStack
│   │   ├── Text
│   │   └── ...
│   ├── ui/           # (Molecules) Interactive UI elements
│   │   ├── Button
│   │   ├── Card
│   │   ├── Select
│   │   └── ...
│   └── app/          # (Organisms) App-specific block elements
│       ├── HeroSection
│       ├── MapSection
│       ├── MainHeader
│       └── ...
└── routes/
    └── pages/        # (Pages) Page-level components that compose organisms
        └── ...
```

- **Strict Encapsulation:** Higher-level components (pages, organisms) MUST NOT directly access the underlying UI/styling library. This encapsulation ensures that the UI library can be swapped by rewriting base and ui without refactoring the entire application.

#### **Backend Architecture**
The backend follows the rules of separation of concern to allow reusability of entities between the frontend and backend, and the services are decoupled from the API entry points:

- **REST API:** The backend resides in `src/routes/api` and provides RESTful endpoints for the application.
- **Typed Entities:** Common entities are defined and shared between the frontend and backend to ensure type safety and consistency.
- **Data Validation:** All data exchanged between the frontend and backend must be validated to ensure correctness and security.
- **Separation of Concern:** The backend is structured to separate API entry points from service implementations, ensuring reusability and modularity. This allows for the addition of new communication layers (e.g., WebSockets) without duplicating logic.

#### **Backend Directory Structure**
The backend is organized as follows:
```
src/
├── routes/
│   ├── api/                # REST API entry points
│   │   ├── places.ts       # API routes for places
│   │   ├── users.ts        # API routes for users
│   │   └── ...             # Other API routes
│   └── ws/                 # WebSocket entry points (future layer)
│       ├── places.ts       # WebSocket handlers for places
│       ├── users.ts        # WebSocket handlers for users
│       └── ...             # Other WebSocket handlers
├── services/               # Business logic and data handling
│   ├── placesService.ts    # Service for places logic
│   ├── usersService.ts     # Service for users logic
│   └── ...                 # Other services
```

#### **Shared Principles**
- **Single Codebase:** Both the frontend and backend reside in the same codebase to simplify development and deployment.
- **Minimal Overhead:** The architecture avoids over-engineering and focuses on the essential requirements of the application.
- **Separation of Concern:** Each layer and module in the codebase has a clear and distinct responsibility, ensuring maintainability and reducing coupling between components.
- **Directory Documentation:** Every key directory MUST contain a `README.md` file that explains the contents, purpose, and any rules associated with that directory.

### VI. Local Content
All application text (menus, labels, sections, etc.) is managed as code and committed inside the git repository. Content is stored in Markdown files with front-matter inside the `src/content` directory. This approach enables version control, collaboration, and compatibility with git-based CMS workflows. Internationalization (i18n) is handled via language-specific subfolders (e.g., `src/content/en`, `src/content/fr`).

### VIII. Maintanability : Documented & Readable Code
Code is written for humans first.
- **JSDoc:** Every function and method MUST have a JSDoc block explaining its purpose and parameters.
- **Component Props:** All component props MUST be defined in an interface, with each property having a clear JSDoc description.
- **Naming:** Variable and function names MUST be clear and self-explanatory.
- **Tests Colocation:** Tests are colocated with their source files. For example, tests for `placesService.ts` will reside in the same directory as `placesService.spec.ts`. This ensures that tests are easily discoverable and maintainable.
- **Directory Documentation:** Every key directory MUST contain a `README.md` file that explains the contents, purpose, and any rules associated with that directory.

## Technical Stack

To align with our principles of Performance and Simplicity (KISS), the following technical stack is choosen:

* **Language:** TypeScript is the single language for both backend and frontend code.
* **Runtime & Tooling:** `bun` is the exclusive runtime, test runner, and builder. All scripts in `package.json` MUST be executed via `bun`.
* **Content:** `content-collections` is used to validate and load all application content from local Markdown files.
* **Schema Validation:** `arktype` is the standard library for all data and schema validation.
* **Testing:** Unit tests MUST use the `bun test` API. Test files will be co-located with their corresponding source files and use the `.spec.ts` extension.
* **Linting/Formatting:** BiomeJS will be used for all code linting and formatting, replacing any other tools like ESLint or Prettier.

## Development Standards

* **Testing:** To maintain simplicity, unit tests are required only for core business logic and utility functions (e.g., in `src/lib` or `src/utils`). UI components and pages will not have dedicated tests. Test files MUST use the `bun test` API, be named `*.spec.ts`, and be co-located with the source file.
* **Code Style:** A consistent code style will be enforced using automated tools.

## Workflow

* **Version Control:** All code changes will be managed through a Git repository. Git commits MUST follow the semantic tags convention to ensure clarity and consistency. For example:
  - `feat:` for new features.
  - `fix:` for bug fixes.
  - `docs:` for documentation updates.
  - `refactor:` for code restructuring without changing functionality.
  - `test:` for adding or updating tests.
  - `chore:` for maintenance tasks (e.g., dependency updates).

## Governance

This constitution is the single source of truth for project principles. Any amendments must be proposed and agreed upon by the team.

**Version**: 1.7.0 | **Ratified**: 2025-10-16 | **Last Amended**: 2025-10-23